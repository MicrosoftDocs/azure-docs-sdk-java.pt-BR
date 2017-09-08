---
title: "Padrões e conceitos de uso das bibliotecas de gerenciamento do Azure para Java"
description: 
keywords: "Azure, Java, SDK, API, Maven, Gradle, autenticação, active directory, entidade de serviço"
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
ms.openlocfilehash: 052c4de1e8f9ff0ece5f36d1c3514bad8c04cfec
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-concepts"></a><span data-ttu-id="c14c2-103">Conceitos de biblioteca de gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c14c2-103">Azure management library concepts</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="c14c2-104">Crie recursos por meio de uma interface fluente</span><span class="sxs-lookup"><span data-stu-id="c14c2-104">Build resources through a fluent interface</span></span>

<span data-ttu-id="c14c2-105">Uma interface fluente é um padrão que cria objetos usando uma cadeia de método que configura corretamente os atributos do objeto.</span><span class="sxs-lookup"><span data-stu-id="c14c2-105">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="c14c2-106">Por exemplo, para criar uma nova conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c14c2-106">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="c14c2-107">Conforme você percorre a cadeia do método, o IDE sugere o próximo método a ser chamado na conversa fluente.</span><span class="sxs-lookup"><span data-stu-id="c14c2-107">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![Conclusão de comando GIF de IntelliJ trabalhando ao longo de uma cadeia fluente](media/intelliJFluent.gif)

<span data-ttu-id="c14c2-109">Encadeie os métodos sugeridos pelo IDE, contanto que eles façam sentido para o recurso do Azure que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="c14c2-109">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="c14c2-110">Se estiver faltando um método necessário na cadeia o seu IDE irá realçá-lo com um erro.</span><span class="sxs-lookup"><span data-stu-id="c14c2-110">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="c14c2-111">Coleções de recursos</span><span class="sxs-lookup"><span data-stu-id="c14c2-111">Resource collections</span></span>

<span data-ttu-id="c14c2-112">A biblioteca de gerenciamento tem um único ponto de entrada por meio do objeto `com.microsoft.azure.management.Azure` de nível superior para criar e atualizar os recursos.</span><span class="sxs-lookup"><span data-stu-id="c14c2-112">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="c14c2-113">Selecione o tipo de recurso para trabalhar usando os métodos de coleção de recursos definidos no objeto `Azure`.</span><span class="sxs-lookup"><span data-stu-id="c14c2-113">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="c14c2-114">Por exemplo, Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="c14c2-114">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="c14c2-115">Listas e iterações</span><span class="sxs-lookup"><span data-stu-id="c14c2-115">Lists and iterations</span></span>

<span data-ttu-id="c14c2-116">Cada coleta de recurso possui um método `list()` para retornar todas as instâncias desse recurso em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="c14c2-116">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="c14c2-117">Por exemplo, `azure.sqlServers().list()` retorna todos os bancos de dados SQL na assinatura.</span><span class="sxs-lookup"><span data-stu-id="c14c2-117">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="c14c2-118">Use o método `listByResourceGroup(String groupname)` para definir o escopo da lista retornada para um determinado [grupo de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="c14c2-118">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="c14c2-119">Pesquisar e iterar na coleção `PagedList<T>` retornada exatamente como faria com um `List<T>` normal:</span><span class="sxs-lookup"><span data-stu-id="c14c2-119">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="c14c2-120">Coleções retornadas de consultas</span><span class="sxs-lookup"><span data-stu-id="c14c2-120">Collections returned from queries</span></span>

<span data-ttu-id="c14c2-121">As bibliotecas de gerenciamento retornam tipos de coleção específicos de consultas com base na estrutura dos resultados.</span><span class="sxs-lookup"><span data-stu-id="c14c2-121">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="c14c2-122">`List<T>`: Dados não ordenados que sejam fáceis de pesquisar e iterar.</span><span class="sxs-lookup"><span data-stu-id="c14c2-122">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="c14c2-123">`Map<T>`: Mapas são pares chave/valor com chaves exclusivas, mas não necessariamente valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="c14c2-123">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="c14c2-124">Um exemplo de um Mapa seria as configurações do aplicativo para um aplicativo Web de um Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c14c2-124">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="c14c2-125">`Set<T>`: Conjuntos possuem valores e chaves exclusivos.</span><span class="sxs-lookup"><span data-stu-id="c14c2-125">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="c14c2-126">Um exemplo de um Conjunto seria redes conectadas a uma máquina virtual, que teria um identificador exclusivo (a chave) e uma configuração de rede exclusiva (o valor).</span><span class="sxs-lookup"><span data-stu-id="c14c2-126">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="c14c2-127">Verbos acionáveis</span><span class="sxs-lookup"><span data-stu-id="c14c2-127">Actionable verbs</span></span>

<span data-ttu-id="c14c2-128">Métodos com verbos em seus nomes executam uma ação imediata no Azure.</span><span class="sxs-lookup"><span data-stu-id="c14c2-128">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="c14c2-129">Esses métodos funcionam de forma síncrona e bloqueiam a execução do thread atual até que sejam concluídos.</span><span class="sxs-lookup"><span data-stu-id="c14c2-129">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="c14c2-130">Verbo</span><span class="sxs-lookup"><span data-stu-id="c14c2-130">Verb</span></span>   |  <span data-ttu-id="c14c2-131">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="c14c2-131">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="c14c2-132">create</span><span class="sxs-lookup"><span data-stu-id="c14c2-132">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="c14c2-133">aplicar</span><span class="sxs-lookup"><span data-stu-id="c14c2-133">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="c14c2-134">excluir</span><span class="sxs-lookup"><span data-stu-id="c14c2-134">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="c14c2-135">list</span><span class="sxs-lookup"><span data-stu-id="c14c2-135">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="c14c2-136">get</span><span class="sxs-lookup"><span data-stu-id="c14c2-136">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="c14c2-137">`define()` e `update()` são verbos, mas não bloquearão a menos que seguidos por um `create()` ou `apply()`.</span><span class="sxs-lookup"><span data-stu-id="c14c2-137">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="c14c2-138">Existem versões assíncronas de alguns desses métodos com o sufixo `Async` usando [Extensões reativas](https://github.com/ReactiveX/RxJava).</span><span class="sxs-lookup"><span data-stu-id="c14c2-138">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="c14c2-139">Alguns objetos terão outros métodos que alteram o estado do recurso no Azure.</span><span class="sxs-lookup"><span data-stu-id="c14c2-139">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="c14c2-140">Por exemplo, `restart()` ou `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="c14c2-140">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="c14c2-141">Esses métodos nem sempre possuem versões assíncronas e bloquearão a execução em seu thread até que sejam concluídos.</span><span class="sxs-lookup"><span data-stu-id="c14c2-141">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="c14c2-142">Criação de recursos lento</span><span class="sxs-lookup"><span data-stu-id="c14c2-142">Lazy resource creation</span></span>

<span data-ttu-id="c14c2-143">Um desafio ao criar recursos do Azure ocorre quando um novo recurso depende de outro recurso que ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="c14c2-143">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="c14c2-144">Um exemplo desse cenário é reservar um endereço IP público e configurar um disco ao criar uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c14c2-144">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="c14c2-145">Você não deseja verificar a reserva do endereço ou a criação de disco, você apenas deseja garantir que a máquina virtual tem esses recursos quando ela é criado.</span><span class="sxs-lookup"><span data-stu-id="c14c2-145">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="c14c2-146">Os objetos `Creatable<T>` permitem que você defina recursos do Azure para uso no seu código sem ter que esperar que eles sejam criados na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c14c2-146">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="c14c2-147">As bibliotecas de gerenciamento adiam a criação de objetos `Creatable<T>` até que eles sejam necessários.</span><span class="sxs-lookup"><span data-stu-id="c14c2-147">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="c14c2-148">Gerar objetos `Creatable<T>` para os recursos do Azure por meio do verbo `define()`:</span><span class="sxs-lookup"><span data-stu-id="c14c2-148">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="c14c2-149">O recurso do Azure definido pelo `Creatable<PublicIPAddress>` neste exemplo ainda não existe na sua assinatura quando esse código é executado.</span><span class="sxs-lookup"><span data-stu-id="c14c2-149">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="c14c2-150">Use o objeto `publicIPAddressCreatable` para criar outros recursos do Azure com esse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="c14c2-150">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="c14c2-151">Os recursos `Creatable<T>` são gerados em sua assinatura quando qualquer recurso que é definido usando o objeto é criado no Azure usando `create()`.</span><span class="sxs-lookup"><span data-stu-id="c14c2-151">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="c14c2-152">Continuando o exemplo de máquina virtual e de endereço IP:</span><span class="sxs-lookup"><span data-stu-id="c14c2-152">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="c14c2-153">Passar o `Creatable<T>` para as chamadas `create()` retorna um objeto `CreatedResources` em vez de um objeto de recurso único.</span><span class="sxs-lookup"><span data-stu-id="c14c2-153">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="c14c2-154">O objeto `CreatedResources<T>` permite acessar todos os recursos criados pela chamada `create()`, não apenas o recurso digitado na chamada.</span><span class="sxs-lookup"><span data-stu-id="c14c2-154">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="c14c2-155">Para acessar o endereço IP público criado no Azure para a máquina virtual criada no exemplo acima:</span><span class="sxs-lookup"><span data-stu-id="c14c2-155">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="c14c2-156">Manipulação de exceção</span><span class="sxs-lookup"><span data-stu-id="c14c2-156">Exception handling</span></span>

<span data-ttu-id="c14c2-157">As classes de Exceção das bibliotecas de gerenciamento estendem `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="c14c2-157">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="c14c2-158">Capturar exceções geradas pelas bibliotecas de gerenciamento com um bloco `catch (RestException exception)` após a instrução `try` relevante.</span><span class="sxs-lookup"><span data-stu-id="c14c2-158">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="c14c2-159">Logs e rastreamento</span><span class="sxs-lookup"><span data-stu-id="c14c2-159">Logs and trace</span></span>

<span data-ttu-id="c14c2-160">Configurar a quantidade de log da biblioteca de gerenciamento quando você cria o objeto `Azure` do ponto de entrada usando `withLogLevel()`.</span><span class="sxs-lookup"><span data-stu-id="c14c2-160">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="c14c2-161">Existem os seguintes níveis de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="c14c2-161">The following trace levels exist:</span></span>

| <span data-ttu-id="c14c2-162">Nível de rastreamento</span><span class="sxs-lookup"><span data-stu-id="c14c2-162">Trace level</span></span> | <span data-ttu-id="c14c2-163">Registro em log ativado</span><span class="sxs-lookup"><span data-stu-id="c14c2-163">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="c14c2-164">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="c14c2-164">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="c14c2-165">Sem saída</span><span class="sxs-lookup"><span data-stu-id="c14c2-165">No output</span></span>
| <span data-ttu-id="c14c2-166">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="c14c2-166">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="c14c2-167">Registra em log as URLs para chamadas REST, códigos de resposta e tempos subjacentes</span><span class="sxs-lookup"><span data-stu-id="c14c2-167">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="c14c2-168">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="c14c2-168">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="c14c2-169">Tudo em BASIC mais os corpos de resposta e solicitação para as chamadas REST</span><span class="sxs-lookup"><span data-stu-id="c14c2-169">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="c14c2-170">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="c14c2-170">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="c14c2-171">Tudo em BASIC mais os cabeçalhos de resposta e solicitação para as chamadas REST</span><span class="sxs-lookup"><span data-stu-id="c14c2-171">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="c14c2-172">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="c14c2-172">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="c14c2-173">Tudo no nível de log de CORPO e CABEÇALHOS de nível de log</span><span class="sxs-lookup"><span data-stu-id="c14c2-173">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="c14c2-174">Associe uma [implementação de registro em log SLF4J](https://www.slf4j.org/manual.html) se você precisa registrar a saída em uma estrutura de registros em log como [Log4J 2](https://logging.apache.org/log4j/2.x/).</span><span class="sxs-lookup"><span data-stu-id="c14c2-174">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>