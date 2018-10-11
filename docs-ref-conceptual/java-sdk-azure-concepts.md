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
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a><span data-ttu-id="1375a-104">Padrões e melhores práticas de desenvolvimento com as bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="1375a-104">Patterns and best practices for development with the Azure libraries for Java</span></span> 

<span data-ttu-id="1375a-105">Este artigo lista uma série de padrões e melhores práticas para usar as bibliotecas do Azure para Java em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="1375a-105">This article lists a series of patterns and best practices when using the Azure libraries for Java in your projects.</span></span> <span data-ttu-id="1375a-106">Desenvolva com esses padrões e diretrizes para reduzir a quantidade de código a ser mantida e facilitar a adição ou configuração de recursos adicionais em futuras atualizações das bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1375a-106">Develop with these patterns and guidelines to reduce the amount of code to maintain and make it easier to add or configure additional resources in future updates to the management libraries.</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="1375a-107">Crie recursos por meio de uma interface fluente</span><span class="sxs-lookup"><span data-stu-id="1375a-107">Build resources through a fluent interface</span></span>

<span data-ttu-id="1375a-108">Uma interface fluente é um padrão que cria objetos usando uma cadeia de método que configura corretamente os atributos do objeto.</span><span class="sxs-lookup"><span data-stu-id="1375a-108">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="1375a-109">Por exemplo, para criar uma nova conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1375a-109">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="1375a-110">Conforme você percorre a cadeia do método, o IDE sugere o próximo método a ser chamado na conversa fluente.</span><span class="sxs-lookup"><span data-stu-id="1375a-110">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![GIF da conclusão do comando IntelliJ trabalhando através de uma cadeia fluente](media/intelliJFluent.gif)

<span data-ttu-id="1375a-112">Encadeie os métodos sugeridos pelo IDE, contanto que eles façam sentido para o recurso do Azure que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="1375a-112">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="1375a-113">Se estiver faltando um método necessário na cadeia o seu IDE irá realçá-lo com um erro.</span><span class="sxs-lookup"><span data-stu-id="1375a-113">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="1375a-114">Coletas de recursos</span><span class="sxs-lookup"><span data-stu-id="1375a-114">Resource collections</span></span>

<span data-ttu-id="1375a-115">A biblioteca de gerenciamento tem um único ponto de entrada por meio do objeto `com.microsoft.azure.management.Azure` de nível superior para criar e atualizar os recursos.</span><span class="sxs-lookup"><span data-stu-id="1375a-115">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="1375a-116">Selecione o tipo de recurso para trabalhar usando os métodos de coleta de recursos definidos no objeto `Azure`.</span><span class="sxs-lookup"><span data-stu-id="1375a-116">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="1375a-117">Por exemplo, Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="1375a-117">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="1375a-118">Listas e iterações</span><span class="sxs-lookup"><span data-stu-id="1375a-118">Lists and iterations</span></span>

<span data-ttu-id="1375a-119">Cada coleta de recurso possui um método `list()` para retornar todas as instâncias desse recurso em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="1375a-119">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="1375a-120">Por exemplo, `azure.sqlServers().list()` retorna todos os bancos de dados SQL na assinatura.</span><span class="sxs-lookup"><span data-stu-id="1375a-120">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="1375a-121">Use o método `listByResourceGroup(String groupname)` para definir o escopo da lista retornada para um determinado [grupo de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="1375a-121">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="1375a-122">Pesquise e itere sobre a coleta de `PagedList<T>` retornada, exatamente como faria com um `List<T>` normal:</span><span class="sxs-lookup"><span data-stu-id="1375a-122">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="1375a-123">Coletas retornadas de consultas</span><span class="sxs-lookup"><span data-stu-id="1375a-123">Collections returned from queries</span></span>

<span data-ttu-id="1375a-124">As bibliotecas de gerenciamento retornam tipos de coletas específicos de consultas com base na estrutura dos resultados.</span><span class="sxs-lookup"><span data-stu-id="1375a-124">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="1375a-125">`List<T>`: Dados não ordenados que sejam fáceis de pesquisar e iterar.</span><span class="sxs-lookup"><span data-stu-id="1375a-125">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="1375a-126">`Map<T>`: Mapas são pares de chaves/valores com chaves exclusivas, mas não necessariamente valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="1375a-126">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="1375a-127">Um exemplo de um Mapa seria as configurações do aplicativo para um aplicativo Web de um Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1375a-127">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="1375a-128">`Set<T>`: Conjuntos possuem valores e chaves exclusivos.</span><span class="sxs-lookup"><span data-stu-id="1375a-128">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="1375a-129">Um exemplo de um Conjunto seria redes conectadas a uma máquina virtual, que teria um identificador exclusivo (a chave) e uma configuração de rede exclusiva (o valor).</span><span class="sxs-lookup"><span data-stu-id="1375a-129">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="1375a-130">Verbos acionáveis</span><span class="sxs-lookup"><span data-stu-id="1375a-130">Actionable verbs</span></span>

<span data-ttu-id="1375a-131">Métodos com verbos em seus nomes executam uma ação imediata no Azure.</span><span class="sxs-lookup"><span data-stu-id="1375a-131">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="1375a-132">Esses métodos funcionam de forma síncrona e bloqueiam a execução do thread atual até que sejam concluídos.</span><span class="sxs-lookup"><span data-stu-id="1375a-132">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="1375a-133">Verbo</span><span class="sxs-lookup"><span data-stu-id="1375a-133">Verb</span></span>   |  <span data-ttu-id="1375a-134">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="1375a-134">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="1375a-135">create</span><span class="sxs-lookup"><span data-stu-id="1375a-135">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="1375a-136">aplicar</span><span class="sxs-lookup"><span data-stu-id="1375a-136">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="1375a-137">excluir</span><span class="sxs-lookup"><span data-stu-id="1375a-137">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="1375a-138">list</span><span class="sxs-lookup"><span data-stu-id="1375a-138">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="1375a-139">get</span><span class="sxs-lookup"><span data-stu-id="1375a-139">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="1375a-140">`define()` e `update()` são verbos, mas não bloquearão a menos que seguidos por um `create()` ou `apply()`.</span><span class="sxs-lookup"><span data-stu-id="1375a-140">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="1375a-141">Existem versões assíncronas de alguns desses métodos com o sufixo `Async` usando [Extensões reativas](https://github.com/ReactiveX/RxJava).</span><span class="sxs-lookup"><span data-stu-id="1375a-141">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="1375a-142">Alguns objetos terão outros métodos que alteram o estado do recurso no Azure.</span><span class="sxs-lookup"><span data-stu-id="1375a-142">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="1375a-143">Por exemplo, `restart()` ou `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="1375a-143">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="1375a-144">Esses métodos nem sempre possuem versões assíncronas e bloquearão a execução em seu thread até que sejam concluídos.</span><span class="sxs-lookup"><span data-stu-id="1375a-144">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="1375a-145">Criação lenta de recursos</span><span class="sxs-lookup"><span data-stu-id="1375a-145">Lazy resource creation</span></span>

<span data-ttu-id="1375a-146">Um desafio ao criar recursos do Azure ocorre quando um novo recurso depende de outro recurso que ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="1375a-146">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="1375a-147">Um exemplo desse cenário é reservar um endereço IP público e configurar um disco ao criar uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1375a-147">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="1375a-148">Você não deseja verificar a reserva do endereço ou a criação de disco, apenas deseja garantir que a máquina virtual tenha esses recursos quando ela é criada.</span><span class="sxs-lookup"><span data-stu-id="1375a-148">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="1375a-149">Os objetos `Creatable<T>` permitem que você defina recursos do Azure para uso no seu código sem ter que esperar que eles sejam criados na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="1375a-149">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="1375a-150">As bibliotecas de gerenciamento adiam a criação de objetos `Creatable<T>` até que eles sejam necessários.</span><span class="sxs-lookup"><span data-stu-id="1375a-150">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="1375a-151">Gerar objetos `Creatable<T>` para os recursos do Azure por meio do verbo `define()`:</span><span class="sxs-lookup"><span data-stu-id="1375a-151">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="1375a-152">O recurso do Azure definido pelo `Creatable<PublicIPAddress>` neste exemplo ainda não existe na sua assinatura quando esse código é executado.</span><span class="sxs-lookup"><span data-stu-id="1375a-152">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="1375a-153">Use o objeto `publicIPAddressCreatable` para criar outros recursos do Azure com esse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="1375a-153">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="1375a-154">Os recursos `Creatable<T>` são gerados em sua assinatura quando qualquer recurso que é definido usando o objeto é criado no Azure usando `create()`.</span><span class="sxs-lookup"><span data-stu-id="1375a-154">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="1375a-155">Continuando o exemplo de máquina virtual e de endereço IP:</span><span class="sxs-lookup"><span data-stu-id="1375a-155">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="1375a-156">Passar o `Creatable<T>` para as chamadas `create()` retorna um objeto `CreatedResources` em vez de um objeto de recurso único.</span><span class="sxs-lookup"><span data-stu-id="1375a-156">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="1375a-157">O objeto `CreatedResources<T>` permite acessar todos os recursos criados pela chamada `create()`, não apenas o recurso digitado na chamada.</span><span class="sxs-lookup"><span data-stu-id="1375a-157">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="1375a-158">Para acessar o endereço IP público criado no Azure para a máquina virtual criada no exemplo acima:</span><span class="sxs-lookup"><span data-stu-id="1375a-158">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="1375a-159">Manipulação de exceção</span><span class="sxs-lookup"><span data-stu-id="1375a-159">Exception handling</span></span>

<span data-ttu-id="1375a-160">As classes de Exceção das bibliotecas de gerenciamento estendem `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="1375a-160">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="1375a-161">Capture as exceções geradas pelas bibliotecas de gerenciamento com um bloco `catch (RestException exception)` após a instrução `try` relevante.</span><span class="sxs-lookup"><span data-stu-id="1375a-161">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="1375a-162">Logs e rastreamento</span><span class="sxs-lookup"><span data-stu-id="1375a-162">Logs and trace</span></span>

<span data-ttu-id="1375a-163">Configure o total de logs da biblioteca de gerenciamento quando você cria o objeto do ponto de entrada`Azure`, usando `withLogLevel()`.</span><span class="sxs-lookup"><span data-stu-id="1375a-163">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="1375a-164">Existem os seguintes níveis de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="1375a-164">The following trace levels exist:</span></span>

| <span data-ttu-id="1375a-165">Nível de rastreamento</span><span class="sxs-lookup"><span data-stu-id="1375a-165">Trace level</span></span> | <span data-ttu-id="1375a-166">Registro em log ativado</span><span class="sxs-lookup"><span data-stu-id="1375a-166">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="1375a-167">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="1375a-167">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="1375a-168">Sem saída</span><span class="sxs-lookup"><span data-stu-id="1375a-168">No output</span></span>
| <span data-ttu-id="1375a-169">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="1375a-169">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="1375a-170">Registra em log as URLs para chamadas REST, códigos de resposta e tempos subjacentes</span><span class="sxs-lookup"><span data-stu-id="1375a-170">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="1375a-171">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="1375a-171">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="1375a-172">Tudo em BASIC mais os corpos de resposta e solicitação para as chamadas REST</span><span class="sxs-lookup"><span data-stu-id="1375a-172">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="1375a-173">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="1375a-173">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="1375a-174">Tudo em BASIC mais os cabeçalhos de resposta e solicitação para as chamadas REST</span><span class="sxs-lookup"><span data-stu-id="1375a-174">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="1375a-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="1375a-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="1375a-176">Tudo no nível de log de BODY e HEADERS</span><span class="sxs-lookup"><span data-stu-id="1375a-176">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="1375a-177">Associe uma [implementação de registro em log SLF4J](https://www.slf4j.org/manual.html) se você precisa registrar a saída em uma estrutura de registros em log como [Log4J 2](https://logging.apache.org/log4j/2.x/).</span><span class="sxs-lookup"><span data-stu-id="1375a-177">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>