---
title: Gerenciar máquinas virtuais do Azure com Java | Microsoft Docs
description: Exemplo de código para gerenciar as máquinas virtuais do Azure usando o SDK do Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 388b68bfb0fdac70efed5ad5d0f7c957ce915449
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592561"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a><span data-ttu-id="c4d1d-103">Gerenciar máquinas virtuais do Azure a partir dos seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="c4d1d-103">Manage Azure virtual machines from your Java applications</span></span>

<span data-ttu-id="c4d1d-104">[Este exemplo](https://github.com/Azure-Samples/compute-java-manage-vm/) usa as [bibliotecas de gerenciamento do Azure para Java](https://github.com/Azure/azure-sdk-for-java) para criar e trabalhar com máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-vm/) uses the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java) to create and work with Azure virtual machines.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="c4d1d-105">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="c4d1d-105">Run the sample</span></span>

<span data-ttu-id="c4d1d-106">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="c4d1d-107">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="c4d1d-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

<span data-ttu-id="c4d1d-108">Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span><span class="sxs-lookup"><span data-stu-id="c4d1d-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="c4d1d-109">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="c4d1d-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a><span data-ttu-id="c4d1d-110">Criar uma máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="c4d1d-110">Create a Windows virtual machine</span></span>

```java
// Prepare a data disk for VM
Disk dataDisk = azure.disks().define(SdkContext.randomResourceName("dsk", 30))
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withData()
            .withSizeInGB(50)
            .create();

// create the windows virtual machine with the data disk            
VirtualMachine windowsVM = azure.virtualMachines().define(windowsVmName)
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularWindowsImage(KnownWindowsVirtualMachineImage.WINDOWS_SERVER_2012_R2_DATACENTER)
            .withAdminUsername(userName)
            .withAdminPassword(password)
            .withNewDataDisk(10)
            .withNewDataDisk(dataDiskCreatable)
            .withExistingDataDisk(dataDisk)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

<span data-ttu-id="c4d1d-111">Esse código:</span><span class="sxs-lookup"><span data-stu-id="c4d1d-111">This code:</span></span>   

0. <span data-ttu-id="c4d1d-112">Define um Creatable `Disk` com um tamanho de 50 GB e um nome aleatório para uso com uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-112">Defines a `Disk` Creatable with a 50GB size and random name for use with a virtual machine.</span></span>
0. <span data-ttu-id="c4d1d-113">Usa a cadeia `azure.virtualMachines().define()..create()` para criar a máquina virtual do Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-113">Uses the `azure.virtualMachines().define()..create()` chain to create the Windows Server 2012 virtual machine.</span></span> <span data-ttu-id="c4d1d-114">A API cria o `Disk` definido na etapa anterior, ao mesmo tempo em que a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-114">The API creates the `Disk` defined in the previous step the same time as the virtual machine.</span></span> <span data-ttu-id="c4d1d-115">Um disco de dados de 10 GB também está anexado à máquina virtual por meio de `withNewDataDisk(10)`.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-115">A 10GB data disk is also attached to the virtual machine through `withNewDataDisk(10)`.</span></span>

<span data-ttu-id="c4d1d-116">Saiba mais sobre como usar [Creatable<T> objetos](java-sdk-azure-concepts.md#Creatables) para definir representações locais de recursos e criá-los assim que outro recurso do Azure precisar deles.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-116">Learn more about using [Creatable<T> objects](java-sdk-azure-concepts.md#Creatables) to define local representations of resources and create them just as other Azure resources need them.</span></span>

## <a name="stop-start-and-restart-a-virtual-machine"></a><span data-ttu-id="c4d1d-117">Parar, iniciar e reiniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4d1d-117">Stop, start, and restart a virtual machine</span></span>

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

<span data-ttu-id="c4d1d-118">`powerOff()` para o sistema operacional da máquina virtual, mas não desaloca os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-118">`powerOff()` stops the virtual machine operating system but does not deallocate its resources.</span></span>

## <a name="add-a-virtual-machine-to-an-existing-network"></a><span data-ttu-id="c4d1d-119">Adicionar uma máquina virtual a uma rede existente</span><span class="sxs-lookup"><span data-stu-id="c4d1d-119">Add a virtual machine to an existing network</span></span>

```java
// Get the virtual network the current virtual machine is using
Network network = windowsVM.getPrimaryNetworkInterface().primaryIPConfiguration().getNetwork();

// Create a Linux VM in the same subnet
VirtualMachine linuxVM = azure.virtualMachines().define(linuxVmName)
           .withRegion(region)
           .withExistingResourceGroup(rgName)
           .withExistingPrimaryNetwork(network)
           .withSubnet("subnet1") // default subnet name when no name specified at creation
           .withPrimaryPrivateIPAddressDynamic()
           .withoutPrimaryPublicIPAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withRootPassword(password)
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
```

<span data-ttu-id="c4d1d-120">Use `withPopularLinuxImage` para definir uma VM do Linux, em vez de uma do Windows.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-120">Use `withPopularLinuxImage` to define a Linux VM instead of a Windows one.</span></span>


## <a name="list-virtual-machines"></a><span data-ttu-id="c4d1d-121">Listar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="c4d1d-121">List virtual machines</span></span>

```java
// get a list of VMs in the same resource group as an existing VM
String resourceGroupName = windowsVM.resourceGroupName();
PagedList<VirtualMachine> resourceGroupVMs = azure.virtualMachines()
        .listByResourceGroup(resourceGroupName); 

// for each vitual machine in the resource group, log their name and plan
for (VirtualMachine virtualMachine : azure.virtualMachines().listByResourceGroup(resourceGroupName)) {
    System.out.println("VM " + virtualMachine.computerName() + 
        " has plan " + virtualMachine.plan());
}
```

<span data-ttu-id="c4d1d-122">Liste todas as máquinas virtuais para uma assinatura usando `azure.virtualMachines().list()` e faça a iteração no Mapa retornado por `tags()` para gerenciar coleções marcadas de máquinas virtuais nos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-122">List all virtual machines for a subscription using `azure.virtualMachines().list()` and iterate through the Map returned by `tags()` to manage tagged collections of virtual machines across resource groups.</span></span>

## <a name="update-a-virtual-machine"></a><span data-ttu-id="c4d1d-123">Atualizar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4d1d-123">Update a virtual machine</span></span>

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

<span data-ttu-id="c4d1d-124">Atualizar a configuração da máquina virtual usando `update()...apply()` e os mesmos métodos usados para configurar a máquina virtual quando ela é criada por meio de `define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-124">Update the virtual machine configuration using `update()...apply()` and the same methods used to configure the virtual machine when created through `define()...create()`.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="c4d1d-125">Excluir uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4d1d-125">Delete a virtual machine</span></span>

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a><span data-ttu-id="c4d1d-126">Explicação do exemplo</span><span class="sxs-lookup"><span data-stu-id="c4d1d-126">Sample explanation</span></span>

<span data-ttu-id="c4d1d-127">[O exemplo de código](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) cria uma máquina virtual do Windows com um disco de dados de 50 GB.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-127">[The sample code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) creates a Windows virtual machine with a 50GB data disk.</span></span> <span data-ttu-id="c4d1d-128">O exemplo cria um segundo disco de dados de 10GB e conecta-o a esta máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-128">The sample then creates a second 10GB data disk and attaches it to this Windows virtual machine.</span></span>
<span data-ttu-id="c4d1d-129">Em seguida, o exemplo cria uma máquina virtual Linux na mesma rede virtual que a máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-129">Then the sample creates a Linux virtual machine in the same virtual network as the Windows virtual machine.</span></span>

<span data-ttu-id="c4d1d-130">O exemplo registra informações sobre as duas máquinas virtuais e exclui-os antes de concluir.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-130">The sample logs information about both virtual machines and deletes them both before completing.</span></span>

| <span data-ttu-id="c4d1d-131">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="c4d1d-131">Class used in sample</span></span> | <span data-ttu-id="c4d1d-132">Observações</span><span class="sxs-lookup"><span data-stu-id="c4d1d-132">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="c4d1d-133">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="c4d1d-133">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="c4d1d-134">Consulta propriedades e gerencia o estado das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-134">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="c4d1d-135">Recuperar em formato de lista com`azure.virtualMachines().list()` ou pelo nome ou ID `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="c4d1d-135">Retrieved in list form  with`azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="c4d1d-136">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="c4d1d-136">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="c4d1d-137">Classe com valores estáticos que são mapeados para [opções de tamanho de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), usada pelo método `withSize()` para definir os recursos alocados para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-137">Class with static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), used by the `withSize()` method to define the resources allocated to the VM.</span></span>
| [<span data-ttu-id="c4d1d-138">Disco</span><span class="sxs-lookup"><span data-stu-id="c4d1d-138">Disk</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | <span data-ttu-id="c4d1d-139">Criar um disco para armazenar dados usando `withData()` ou a imagem do sistema operacional usando o método `withLinux` ou `withWindows` apropriado ao definir o disco.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-139">Create a disk to store data using `withData()` or operating system image using the appropriate `withLinux` or `withWindows` method when defining the disk.</span></span> <span data-ttu-id="c4d1d-140">Anexar discos para máquinas virtuais no momento da criação (`using withNewDataDisk` ou `withExistingDataDisk`) ou após a criação por `update()..apply()` no objeto VirtualMachine.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-140">Attach disks to virtual machines either at the time of creation (`using withNewDataDisk` or `withExistingDataDisk`) or after creation by `update()..apply()` on the VirtualMachine object.</span></span>
| [<span data-ttu-id="c4d1d-141">DiskSkuTypes</span><span class="sxs-lookup"><span data-stu-id="c4d1d-141">DiskSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | <span data-ttu-id="c4d1d-142">Classe com valores estáticos para definir um disco com um plano de armazenamento standard ou [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="c4d1d-142">Class with static values to define a disk with a standard or [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) storage plan.</span></span>
| [<span data-ttu-id="c4d1d-143">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="c4d1d-143">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="c4d1d-144">Classe com um conjunto de opções de máquina virtual Linux para uso com o método `withPopularLinuxImage()` durante a definição de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-144">Class with a set of Linux virtual machine options for use with the `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="c4d1d-145">KnownWindowsVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="c4d1d-145">KnownWindowsVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | <span data-ttu-id="c4d1d-146">Classe com um conjunto de opções de imagem de máquina virtual Windows para uso com o método `withPopularWindowsImage()` durante a definição de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4d1d-146">Class with a set of Windows virtual machine image options for use with the `withPopularWindowsImage()` method when defining a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4d1d-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4d1d-147">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]