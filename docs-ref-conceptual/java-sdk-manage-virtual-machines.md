---
title: "Gerenciar máquinas virtuais do Azure com Java | Microsoft Docs"
description: "Exemplo de código para gerenciar as máquinas virtuais do Azure usando o SDK do Azure para Java"
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e3048b3317477f4b1fb8edf93e4bebad6b7fafce
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a>Gerenciar máquinas virtuais do Azure a partir dos seus aplicativos Java

[Este exemplo](https://github.com/Azure-Samples/compute-java-manage-vm/) usa as [bibliotecas de gerenciamento do Azure para Java](https://github.com/Azure/azure-sdk-for-java) para criar e trabalhar com máquinas virtuais do Azure.

## <a name="run-the-sample"></a>Execute o exemplo

Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador. Em seguida, execute:

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).

## <a name="authenticate-with-azure"></a>Autenticar com o Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a>Criar uma máquina virtual do Windows

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

Esse código:   

0. Define um Creatable `Disk` com um tamanho de 50 GB e um nome aleatório para uso com uma máquina virtual.
0. Usa a cadeia `azure.virtualMachines().define()..create()` para criar a máquina virtual do Windows Server 2012. A API cria o `Disk` definido na etapa anterior, ao mesmo tempo em que a máquina virtual. Um disco de dados de 10 GB também está anexado à máquina virtual por meio de `withNewDataDisk(10)`.

Saiba mais sobre como usar [Creatable<T> objetos](java-sdk-azure-concepts.md#Creatables) para definir representações locais de recursos e criá-los assim que outro recurso do Azure precisar deles.

## <a name="stop-start-and-restart-a-virtual-machine"></a>Parar, iniciar e reiniciar uma máquina virtual

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

`powerOff()` para o sistema operacional da máquina virtual, mas não desaloca os seus recursos.

## <a name="add-a-virtual-machine-to-an-existing-network"></a>Adicionar uma máquina virtual a uma rede existente

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

Use `withPopularLinuxImage` para definir uma VM do Linux, em vez de uma do Windows.


## <a name="list-virtual-machines"></a>Listar máquinas virtuais

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

Liste todas as máquinas virtuais para uma assinatura usando `azure.virtualMachines().list()` e faça a iteração no Mapa retornado por `tags()` para gerenciar coleções marcadas de máquinas virtuais nos grupos de recursos.

## <a name="update-a-virtual-machine"></a>Atualizar uma máquina virtual

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

Atualizar a configuração da máquina virtual usando `update()...apply()` e os mesmos métodos usados para configurar a máquina virtual quando ela é criada por meio de `define()...create()`.

## <a name="delete-a-virtual-machine"></a>Excluir uma máquina virtual

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a>Explicação do exemplo

[O exemplo de código](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) cria uma máquina virtual do Windows com um disco de dados de 50 GB. O exemplo cria um segundo disco de dados de 10GB e conecta-o a esta máquina virtual do Windows.
Em seguida, o exemplo cria uma máquina virtual Linux na mesma rede virtual que a máquina virtual do Windows.

O exemplo registra informações sobre as duas máquinas virtuais e exclui-os antes de concluir.

| Classe usada no exemplo | Observações
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Consulta propriedades e gerencia o estado das máquinas virtuais. Recuperar em formato de lista com`azure.virtualMachines().list()` ou pelo nome ou ID `azure.virtualMachines().getByResourceGroup()`
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Classe com valores estáticos que são mapeados para [opções de tamanho de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), usada pelo método `withSize()` para definir os recursos alocados para a máquina virtual.
| [Disco](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | Criar um disco para armazenar dados usando `withData()` ou a imagem do sistema operacional usando o método `withLinux` ou `withWindows` apropriado ao definir o disco. Anexar discos para máquinas virtuais no momento da criação (`using withNewDataDisk` ou `withExistingDataDisk`) ou após a criação por `update()..apply()` no objeto VirtualMachine.
| [DiskSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | Classe com valores estáticos para definir um disco com um plano de armazenamento standard ou [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Classe com um conjunto de opções de máquina virtual Linux para uso com o método `withPopularLinuxImage()` durante a definição de uma máquina virtual.
| [KnownWindowsVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | Classe com um conjunto de opções de imagem de máquina virtual Windows para uso com o método `withPopularWindowsImage()` durante a definição de uma máquina virtual.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [next-steps](includes/java-next-steps.md)]