---
title: Criar VMs em várias regiões em paralelo | Microsoft Docs
description: Exemplo de código para criar máquinas virtuais em diferentes regiões do Azure em paralelo usando o SDK do Azure para Java
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
ms.locfileid: "21931192"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a>Criar máquinas virtuais em várias regiões a partir de seus aplicativos Java

[Este exemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) cria máquinas virtuais em paralelo em diferentes regiões do Azure usando as [bibliotecas de gerenciamento do Azure para Java](https://github.com/Azure/azure-sdk-for-java).

> [!IMPORTANT]
> O exemplo cria um total de 48 VMs executando Ubuntu 16.04 LTS de [tamanho STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) em quatro regiões. O exemplo de código exclui essas máquinas virtuais antes de sair. Certifique-se de [verificar seus limites de serviço e cota](http://docs.microsoft.com/azure/azure-subscription-service-limits) antes de executar esse exemplo com o número padrão de máquinas virtuais.

## <a name="run-the-sample"></a>Execute o exemplo

Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador. Em seguida, execute:

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).

## <a name="authenticate-with-azure"></a>Autenticar com o Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a>Definir locais e contagens para as máquinas virtuais

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

Esse `Map` é usado posteriormente no exemplo para definir a distribuição das VMs em todo o mundo.

## <a name="create-a-resource-group"></a>Criar um grupo de recursos 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

Cada recurso no exemplo é gerenciado por este grupo de recursos. Isso facilita a posterior limpeza dos recursos através da exclusão do grupo de recursos.

## <a name="define-the-virtual-machines"></a>Definir as máquinas virtuais
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

O loop `for` externo acima itera em cada região, definindo uma rede virtual Creatable e uma conta de armazenamento Creatable para uso por todas as máquinas virtuais nessa região. Saiba mais sobre como usar [Creatables](java-sdk-azure-concepts.md#Creatables) para criar recursos conforme necessário ao usar as bibliotecas de gerenciamento.

O loop `for` interno obtém um endereço IP público Creatable para a máquina virtual e, em seguida, define uma máquina virtual Creatable usando o Creatables para a rede virtual, a conta de armazenamento e o endereço IP público definido anteriormente.  A máquina virtual Creatable é então adicionada à lista `creatableVirtualMachines`.

## <a name="create-the-virtual-machines"></a>Criar as máquinas virtuais

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

A chamada `azure.virtualMachines().create(creatableVirtualMachines)` cria todas as máquinas virtuais definidas na lista `creatableVirtualMachines` em paralelo em todas as regiões.

Use o objeto `CreatedResources<VirtualMachine>` retornado para acessar qualquer recurso criado na assinatura do Azure durante o método `create()`, não apenas o tipo `VirtualMachine` retornado. Converter o valor retornado de `createdRelatedResources()` para o tipo correto. 

Saiba mais sobre como trabalhar com `Creatable<T>` e `CreatedResources` em nosso [artigo sobre conceitos de biblioteca](java-sdk-azure-concepts.md).

## <a name="delete-the-resource-group"></a>Exclua o grupo de recursos 

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

Esse bloco exclui recursos criados no exemplo antes da saída do exemplo.

## <a name="sample-explanation"></a>Explicação do exemplo

Exibição de exemplo de código completo no [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).

O exemplo usa objetos `Creatable` para definir uma rede virtual e conta de armazenamento para cada região que hospeda as máquinas virtuais. Os objetos `Creatable` são então definidos para o endereço IP público para cada máquina virtual. O exemplo define as máquinas virtuais usando esses objetos `Creatable` e o exemplo adiciona a definição da VM à lista `virtualMachineCreatable`.

Depois que o código adiciona a definição de cada máquina virtual à lista, `azure.virtualMachines().create(creatableVirtualMachines)` cria cada máquina virtual em paralelo no Azure.

O exemplo de código, em seguida, obtém os endereços IP para todas as máquinas virtuais criadas a partir do objeto retornado CreatedResources para criar um [Gerenciador de Tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) para distribuir a carga entre as máquinas virtuais. 

O bloco `finally` exclui os recursos de sua assinatura do Azure, mesmo no caso de um erro.

| Classe usada no exemplo | Observações
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Consulta propriedades e gerencia o estado das máquinas virtuais. Recuperar em formato de lista com `azure.virtualMachines().list()` ou pelo nome ou ID `azure.virtualMachines().getByResourceGroup()`
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Valores estáticos que são mapeados para [opções de tamanho de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) para uso como um parâmetro para `withSize()` durante a definição de uma máquina virtual.
| [PublicIpAddress](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | Definido, mas não imediatamente criado para cada máquina virtual por meio de `azure.publicIpAddresses().define()`. Armazenar a chave para cada `Creatable` e recuperar mais tarde por meio de `createdRelatedResource()`
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Conjunto de opções de máquina virtual Linux usado como um parâmetro para o método `withPopularLinuxImage()` durante a definição de uma máquina virtual.
| [Rede](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | O exemplo define uma rede virtual para cada região por meio de `azure.networks().define()` . 

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [next-steps](includes/java-next-steps.md)]