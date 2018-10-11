---
title: Bibliotecas de Gerenciamento do Azure para Java – guia do desenvolvedor
description: Padrões e conceitos para uso das bibliotecas de gerenciamento Java para Java para gerenciar recursos de nuvem no Azure.
keywords: Azure, Java, SDK, API, Maven, Gradle, autenticação, active directory, entidade de serviço
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: f452468b-7aae-4944-abad-0b1aaf19170d
ms.openlocfilehash: 8b52981ddfaadb7227cea4c7df014011196339cb
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893627"
---
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a>Padrões e melhores práticas de desenvolvimento com as bibliotecas do Azure para Java 

Este artigo lista uma série de padrões e melhores práticas para usar as bibliotecas do Azure para Java em seus projetos. Desenvolva com esses padrões e diretrizes para reduzir a quantidade de código a ser mantida e facilitar a adição ou configuração de recursos adicionais em futuras atualizações das bibliotecas de gerenciamento.

## <a name="build-resources-through-a-fluent-interface"></a>Crie recursos por meio de uma interface fluente

Uma interface fluente é um padrão que cria objetos usando uma cadeia de método que configura corretamente os atributos do objeto. Por exemplo, para criar uma nova conta de Armazenamento do Azure

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

Conforme você percorre a cadeia do método, o IDE sugere o próximo método a ser chamado na conversa fluente.   

![GIF da conclusão do comando IntelliJ trabalhando através de uma cadeia fluente](media/intelliJFluent.gif)

Encadeie os métodos sugeridos pelo IDE, contanto que eles façam sentido para o recurso do Azure que está sendo definido. Se estiver faltando um método necessário na cadeia o seu IDE irá realçá-lo com um erro.

## <a name="resource-collections"></a>Coletas de recursos

A biblioteca de gerenciamento tem um único ponto de entrada por meio do objeto `com.microsoft.azure.management.Azure` de nível superior para criar e atualizar os recursos. Selecione o tipo de recurso para trabalhar usando os métodos de coleta de recursos definidos no objeto `Azure`. Por exemplo, Banco de Dados SQL:

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a>Listas e iterações

Cada coleta de recurso possui um método `list()` para retornar todas as instâncias desse recurso em sua assinatura atual. Por exemplo, `azure.sqlServers().list()` retorna todos os bancos de dados SQL na assinatura.

Use o método `listByResourceGroup(String groupname)` para definir o escopo da lista retornada para um determinado [grupo de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).  

Pesquise e itere sobre a coleta de `PagedList<T>` retornada, exatamente como faria com um `List<T>` normal:

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a>Coletas retornadas de consultas

As bibliotecas de gerenciamento retornam tipos de coletas específicos de consultas com base na estrutura dos resultados.

- `List<T>`: Dados não ordenados que sejam fáceis de pesquisar e iterar.
- `Map<T>`: Mapas são pares de chaves/valores com chaves exclusivas, mas não necessariamente valores exclusivos. Um exemplo de um Mapa seria as configurações do aplicativo para um aplicativo Web de um Serviço de Aplicativo.
- `Set<T>`: Conjuntos possuem valores e chaves exclusivos. Um exemplo de um Conjunto seria redes conectadas a uma máquina virtual, que teria um identificador exclusivo (a chave) e uma configuração de rede exclusiva (o valor).

## <a name="actionable-verbs"></a>Verbos acionáveis

Métodos com verbos em seus nomes executam uma ação imediata no Azure. Esses métodos funcionam de forma síncrona e bloqueiam a execução do thread atual até que sejam concluídos. 

| Verbo   |  Exemplo de uso |
|--------|---------------|
| create | `azure.virtualMachines().create(listOfVMCreatables)` |
| aplicar  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| excluir | `azure.disks().deleteById(id)` | 
| list   | `azure.sqlServers().list()` | 
| get    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> `define()` e `update()` são verbos, mas não bloquearão a menos que seguidos por um `create()` ou `apply()`.
 
Existem versões assíncronas de alguns desses métodos com o sufixo `Async` usando [Extensões reativas](https://github.com/ReactiveX/RxJava). 

Alguns objetos terão outros métodos que alteram o estado do recurso no Azure. Por exemplo, `restart()` ou `VirtualMachine`.

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
Esses métodos nem sempre possuem versões assíncronas e bloquearão a execução em seu thread até que sejam concluídos.

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a>Criação lenta de recursos

Um desafio ao criar recursos do Azure ocorre quando um novo recurso depende de outro recurso que ainda não existe. Um exemplo desse cenário é reservar um endereço IP público e configurar um disco ao criar uma nova máquina virtual. Você não deseja verificar a reserva do endereço ou a criação de disco, apenas deseja garantir que a máquina virtual tenha esses recursos quando ela é criada.

Os objetos `Creatable<T>` permitem que você defina recursos do Azure para uso no seu código sem ter que esperar que eles sejam criados na sua assinatura. As bibliotecas de gerenciamento adiam a criação de objetos `Creatable<T>` até que eles sejam necessários.

Gerar objetos `Creatable<T>` para os recursos do Azure por meio do verbo `define()`:

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

O recurso do Azure definido pelo `Creatable<PublicIPAddress>` neste exemplo ainda não existe na sua assinatura quando esse código é executado.  Use o objeto `publicIPAddressCreatable` para criar outros recursos do Azure com esse endereço IP. 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

Os recursos `Creatable<T>` são gerados em sua assinatura quando qualquer recurso que é definido usando o objeto é criado no Azure usando `create()`. Continuando o exemplo de máquina virtual e de endereço IP:

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

Passar o `Creatable<T>` para as chamadas `create()` retorna um objeto `CreatedResources` em vez de um objeto de recurso único.  O objeto `CreatedResources<T>` permite acessar todos os recursos criados pela chamada `create()`, não apenas o recurso digitado na chamada. Para acessar o endereço IP público criado no Azure para a máquina virtual criada no exemplo acima:

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a>Manipulação de exceção

As classes de Exceção das bibliotecas de gerenciamento estendem `com.microsoft.rest.RestException`. Capture as exceções geradas pelas bibliotecas de gerenciamento com um bloco `catch (RestException exception)` após a instrução `try` relevante.

## <a name="logs-and-trace"></a>Logs e rastreamento

Configure o total de logs da biblioteca de gerenciamento quando você cria o objeto do ponto de entrada`Azure`, usando `withLogLevel()`. Existem os seguintes níveis de rastreamento:

| Nível de rastreamento | Registro em log ativado 
| ------------ | ---------------
| com.microsoft.rest.LogLevel.NONE | Sem saída
| com.microsoft.rest.LogLevel.BASIC | Registra em log as URLs para chamadas REST, códigos de resposta e tempos subjacentes
| com.microsoft.rest.LogLevel.BODY | Tudo em BASIC mais os corpos de resposta e solicitação para as chamadas REST
| com.microsoft.rest.LogLevel.HEADERS | Tudo em BASIC mais os cabeçalhos de resposta e solicitação para as chamadas REST
| com.microsoft.rest.LogLevel.BODY_AND_HEADERS | Tudo no nível de log de BODY e HEADERS

Associe uma [implementação de registro em log SLF4J](https://www.slf4j.org/manual.html) se você precisa registrar a saída em uma estrutura de registros em log como [Log4J 2](https://logging.apache.org/log4j/2.x/).