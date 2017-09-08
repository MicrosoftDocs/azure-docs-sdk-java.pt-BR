---
title: "Criar VMs em várias regiões em paralelo | Microsoft Docs"
description: "Exemplo de código para criar máquinas virtuais em diferentes regiões do Azure em paralelo usando o SDK do Azure para Java"
author: rloutlaw
manager: douge
ms.assetid: e5a36699-2d96-4571-84f9-a6af13f3c067
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e20feb555c3a360eceae60c1569af9a00a5cd027
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a><span data-ttu-id="6fee1-103">Criar máquinas virtuais em várias regiões a partir de seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="6fee1-103">Create virtual machines across multiple regions from your Java applications</span></span>

<span data-ttu-id="6fee1-104">[Este exemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) cria máquinas virtuais em paralelo em diferentes regiões do Azure usando as [bibliotecas de gerenciamento do Azure para Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="6fee1-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) creates virtual machines in parallel across different Azure regions using the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fee1-105">O exemplo cria um total de 48 VMs executando Ubuntu 16.04 LTS de [tamanho STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) em quatro regiões.</span><span class="sxs-lookup"><span data-stu-id="6fee1-105">The sample creates a total of 48 VMs running Ubuntu 16.04 LTS of [size STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) across four regions.</span></span> <span data-ttu-id="6fee1-106">O exemplo de código exclui essas máquinas virtuais antes de sair.</span><span class="sxs-lookup"><span data-stu-id="6fee1-106">The sample code deletes these virtual machines before exiting.</span></span> <span data-ttu-id="6fee1-107">Certifique-se de [verificar seus limites de serviço e cota](http://docs.microsoft.com/azure/azure-subscription-service-limits) antes de executar esse exemplo com o número padrão de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6fee1-107">Make sure to [check your service limits and quota](http://docs.microsoft.com/azure/azure-subscription-service-limits) before running this sample with the default number of VMs.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="6fee1-108">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="6fee1-108">Run the sample</span></span>

<span data-ttu-id="6fee1-109">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6fee1-109">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="6fee1-110">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="6fee1-110">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

<span data-ttu-id="6fee1-111">Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span><span class="sxs-lookup"><span data-stu-id="6fee1-111">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="6fee1-112">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="6fee1-112">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a><span data-ttu-id="6fee1-113">Definir locais e contagens para as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="6fee1-113">Set locations and counts for the virtual machines</span></span>

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

<span data-ttu-id="6fee1-114">Esse `Map` é usado posteriormente no exemplo para definir a distribuição das VMs em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="6fee1-114">This `Map` is used later in the sample to set the distrubtion of the VMs worldwide.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6fee1-115">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6fee1-115">Create a resource group</span></span> 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

<span data-ttu-id="6fee1-116">Cada recurso no exemplo é gerenciado por este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6fee1-116">Each resource in the sample is managed by this resource group.</span></span> <span data-ttu-id="6fee1-117">Isso facilita a posterior limpeza dos recursos através da exclusão do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6fee1-117">This makes the resources easy to clean up later by deleting the resource group.</span></span>

## <a name="define-the-virtual-machines"></a><span data-ttu-id="6fee1-118">Definir as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="6fee1-118">Define the virtual machines</span></span>
```java
// list to store the VirtualMachine definitions
List<Creatable<VirtualMachine>> creatableVirtualMachines = new ArrayList<>();
    
// outer loop: iterate through each region included in the map
for (Map.Entry<Region, Integer> entry : virtualMachinesByLocation.entrySet()) {
    Region region = entry.getKey();
    Integer vmCount = entry.getValue();

    // Define one virtual network Creatable per region for the VMs to share
    String networkName = SdkContext.randomResourceName("vnetCOPD-", 20);
    Creatable<Network> networkCreatable = azure.networks().define(networkName)
           .withRegion(region)
           .withExistingResourceGroup(resourceGroup)
           .withAddressSpace("172.16.0.0/16");

    // Define one storage account Creatable per region for storing VM disks
    String storageAccountName = SdkContext.randomResourceName("stgcopd", 20);
    Creatable<StorageAccount> storageAccountCreatable = azure.storageAccounts()
        .define(storageAccountName)
              .withRegion(region)
              .withExistingResourceGroup(resourceGroup);

    // generate a common prefix for every VM name
    String linuxVMNamePrefix = SdkContext.randomResourceName("vm-", 15);

    // inner loop: iterate once for every VM instance in the region
    for (int i = 1; i <= vmCount; i++) {

        // Create one public IP address Creatable for each VM
        Creatable<PublicIpAddress> publicIpAddressCreatable = azure.publicIpAddresses()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withLeafDomainLabel(SdkContext.randomResourceName("pip", 10));

        publicIpCreatableKeys.add(publicIpAddressCreatable.key());

        // Create one virtual machine Creatable 
        Creatable<VirtualMachine> virtualMachineCreatable = azure.virtualMachines()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withNewPrimaryNetwork(networkCreatable)
             .withPrimaryPrivateIpAddressDynamic()
             .withNewPrimaryPublicIpAddress(publicIpAddressCreatable)
             .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
             .withRootUsername(userName)
             .withSsh(sshKey)
             .withSize(VirtualMachineSizeTypes.STANDARD_DS3_V2)
             .withNewStorageAccount(storageAccountCreatable);
        // add the virtual machine Creatable to the list     
        creatableVirtualMachines.add(virtualMachineCreatable); 
     }
}
```

<span data-ttu-id="6fee1-119">O loop `for` externo acima itera em cada região, definindo uma rede virtual Creatable e uma conta de armazenamento Creatable para uso por todas as máquinas virtuais nessa região.</span><span class="sxs-lookup"><span data-stu-id="6fee1-119">The outer `for` loop above iterates through each region, defining a virtual network Creatable and storage account Creatable for use by all virtual machines in that region.</span></span> <span data-ttu-id="6fee1-120">Saiba mais sobre como usar [Creatables](java-sdk-azure-concepts.md#Creatables) para criar recursos conforme necessário ao usar as bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6fee1-120">Learn more about using [Creatables](java-sdk-azure-concepts.md#Creatables) to create resources only as needed when using the management libraries.</span></span>

<span data-ttu-id="6fee1-121">O loop `for` interno obtém um endereço IP público Creatable para a máquina virtual e, em seguida, define uma máquina virtual Creatable usando o Creatables para a rede virtual, a conta de armazenamento e o endereço IP público definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6fee1-121">The inner `for` loop gets a public IP address Creatable for the virtual machine and then defines a virtual machine Creatable using the Creatables for the virtual network, storage account, and public IP address defined previously.</span></span>  <span data-ttu-id="6fee1-122">A máquina virtual Creatable é então adicionada à lista `creatableVirtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="6fee1-122">This VirtualMachine Creatable is then added to the `creatableVirtualMachines` list.</span></span>

## <a name="create-the-virtual-machines"></a><span data-ttu-id="6fee1-123">Criar as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="6fee1-123">Create the virtual machines</span></span>

```java
// create all virtual machines defined in the list, return all Creatable objects used
// including networks, public IP addresses, and storage accounts
CreatedResources<VirtualMachine> virtualMachines = azure.virtualMachines().create(creatableVirtualMachines);

// list the IDs of each virtual machine created 
for (VirtualMachine virtualMachine : virtualMachines.values()) {
    System.out.println(virtualMachine.id());
}

// call createdRelatedResource(key) to get the resources used to define the virtual machines. 
// Save the key at the time you define the Creatable to use CreatedResources like this
for (String publicIpCreatableKey : publicIpCreatableKeys) {
    PublicIPAddress pip = 
         (PublicIPAddress) virtualMachines.createdRelatedResource(publicIpCreatableKey);
}
```

<span data-ttu-id="6fee1-124">A chamada `azure.virtualMachines().create(creatableVirtualMachines)` cria todas as máquinas virtuais definidas na lista `creatableVirtualMachines` em paralelo em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="6fee1-124">The `azure.virtualMachines().create(creatableVirtualMachines)` call creates all of the virtual machines defined in the `creatableVirtualMachines` List in parallel across the regions.</span></span>

<span data-ttu-id="6fee1-125">Use o objeto `CreatedResources<VirtualMachine>` retornado para acessar qualquer recurso criado na assinatura do Azure durante o método `create()`, não apenas o tipo `VirtualMachine` retornado.</span><span class="sxs-lookup"><span data-stu-id="6fee1-125">Use the returned `CreatedResources<VirtualMachine>` object to access any resources created in the Azure subscription during the the `create()` method, not just the returned `VirtualMachine` type.</span></span> <span data-ttu-id="6fee1-126">Converter o valor retornado de `createdRelatedResources()` para o tipo correto.</span><span class="sxs-lookup"><span data-stu-id="6fee1-126">Cast the returned value from `createdRelatedResources()` to the correct type.</span></span> 

<span data-ttu-id="6fee1-127">Saiba mais sobre como trabalhar com `Creatable<T>` e `CreatedResources` em nosso [artigo sobre conceitos de biblioteca](java-sdk-azure-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="6fee1-127">Learn more about working with `Creatable<T>` and `CreatedResources` in our [library concepts article](java-sdk-azure-concepts.md).</span></span>

## <a name="delete-the-resource-group"></a><span data-ttu-id="6fee1-128">Exclua o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6fee1-128">Delete the resource group</span></span> 

```java
// finally block deletes the resource group before the code exits
// deleting a resource group deletes all resources created in it
finally {
    try {
        System.out.println("Deleting Resource Group: " + rgName);
        azure.resourceGroups().deleteByName(rgName);
        System.out.println("Deleted Resource Group: " + rgName);
    } catch (NullPointerException npe) {
        System.out.println("Did not create any resources in Azure. No clean up is necessary");
    } catch (Exception g) {
        g.printStackTrace();
    }
}
```

<span data-ttu-id="6fee1-129">Esse bloco exclui recursos criados no exemplo antes da saída do exemplo.</span><span class="sxs-lookup"><span data-stu-id="6fee1-129">This block deletes resources created in the sample before the sample exits.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="6fee1-130">Explicação do exemplo</span><span class="sxs-lookup"><span data-stu-id="6fee1-130">Sample explanation</span></span>

<span data-ttu-id="6fee1-131">Exibição de exemplo de código completo no [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span><span class="sxs-lookup"><span data-stu-id="6fee1-131">View the complete sample code on [Github](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span></span>

<span data-ttu-id="6fee1-132">O exemplo usa objetos `Creatable` para definir uma rede virtual e conta de armazenamento para cada região que hospeda as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6fee1-132">The sample uses `Creatable` objects to define a virtual network and storage account for each region hosting the virtual machines.</span></span> <span data-ttu-id="6fee1-133">Os objetos `Creatable` são então definidos para o endereço IP público para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6fee1-133">`Creatable` objects are then defined for the public IP address for each virtual machine.</span></span> <span data-ttu-id="6fee1-134">O exemplo define as máquinas virtuais usando esses objetos `Creatable` e o exemplo adiciona a definição da VM à lista `virtualMachineCreatable`.</span><span class="sxs-lookup"><span data-stu-id="6fee1-134">The sample defines the virtual machines using these `Creatable` objects, and sample adds the VM definition to the `virtualMachineCreatable` list.</span></span>

<span data-ttu-id="6fee1-135">Depois que o código adiciona a definição de cada máquina virtual à lista, `azure.virtualMachines().create(creatableVirtualMachines)` cria cada máquina virtual em paralelo no Azure.</span><span class="sxs-lookup"><span data-stu-id="6fee1-135">After the code adds every virtual machine definition to the list, `azure.virtualMachines().create(creatableVirtualMachines)` creates each virtual machine in parallel in Azure.</span></span>

<span data-ttu-id="6fee1-136">O exemplo de código, em seguida, obtém os endereços IP para todas as máquinas virtuais criadas a partir do objeto retornado CreatedResources para criar um [Gerenciador de Tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) para distribuir a carga entre as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6fee1-136">The sample code then gets the IP addresses for all of the created virtual machines from the returned CreatedResources object to create a [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) to distribute load across the virtual machines.</span></span> 

<span data-ttu-id="6fee1-137">O bloco `finally` exclui os recursos de sua assinatura do Azure, mesmo no caso de um erro.</span><span class="sxs-lookup"><span data-stu-id="6fee1-137">The `finally` block deletes the resources from your Azure subscription even in the case of an error.</span></span>

| <span data-ttu-id="6fee1-138">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="6fee1-138">Class used in sample</span></span> | <span data-ttu-id="6fee1-139">Observações</span><span class="sxs-lookup"><span data-stu-id="6fee1-139">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="6fee1-140">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="6fee1-140">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="6fee1-141">Consulta propriedades e gerencia o estado das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6fee1-141">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="6fee1-142">Recuperar em formato de lista com `azure.virtualMachines().list()` ou pelo nome ou ID `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="6fee1-142">Retrieved in list form from `azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="6fee1-143">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="6fee1-143">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="6fee1-144">Valores estáticos que são mapeados para [opções de tamanho de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) para uso como um parâmetro para `withSize()` durante a definição de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6fee1-144">Static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for use as a parameter to `withSize()` when defining a virtual machine.</span></span>
| [<span data-ttu-id="6fee1-145">PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="6fee1-145">PublicIpAddress</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | <span data-ttu-id="6fee1-146">Definido, mas não imediatamente criado para cada máquina virtual por meio de `azure.publicIpAddresses().define()`.</span><span class="sxs-lookup"><span data-stu-id="6fee1-146">Defined, but not immediately created, for each virtual machine through `azure.publicIpAddresses().define()`.</span></span> <span data-ttu-id="6fee1-147">Armazenar a chave para cada `Creatable` e recuperar mais tarde por meio de `createdRelatedResource()`</span><span class="sxs-lookup"><span data-stu-id="6fee1-147">Store the key for each `Creatable` and retrieve later through `createdRelatedResource()`</span></span>
| [<span data-ttu-id="6fee1-148">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="6fee1-148">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="6fee1-149">Conjunto de opções de máquina virtual Linux usado como um parâmetro para o método `withPopularLinuxImage()` durante a definição de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6fee1-149">Set of Linux virtual machine options used as a parameter to `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="6fee1-150">Rede</span><span class="sxs-lookup"><span data-stu-id="6fee1-150">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="6fee1-151">O exemplo define uma rede virtual para cada região por meio de `azure.networks().define()` .</span><span class="sxs-lookup"><span data-stu-id="6fee1-151">The sample defines one virtual network for each region through  `azure.networks().define()` .</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6fee1-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fee1-152">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]