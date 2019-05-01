---
title: Gerenciar conjuntos de dimensionamento de máquinas virtuais com Java | Microsoft Docs
description: Exemplo de código para gerenciar os conjuntos de dimensionamento das máquinas virtuais do Azure usando o SDK do Azure para Java
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ebc9657f9f148b89d9a3178547c50d5b7bbc86e0
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593221"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a>Gerenciar conjuntos de dimensionamento das máquinas virtuais do Azure a partir dos seus aplicativos Java

[Este exemplo](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) cria um [conjunto de dimensionamento de máquina virtual](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) usando as [bibliotecas de gerenciamento do Java](https://github.com/Azure/azure-sdk-for-java). 

## <a name="run-the-sample"></a>Execute o exemplo

Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador. Em seguida, execute:

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).

## <a name="authenticate-with-azure"></a>Autenticar com o Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a>Criar uma rede virtual para o conjunto de dimensionamento

```java
Network network = azure.networks().define(vnetName)
                    .withRegion(region)
                    .withNewResourceGroup(rgName)
                    .withAddressSpace("172.16.0.0/16")
                    .defineSubnet("Front-end")
                    .withAddressPrefix("172.16.1.0/24")
                    .attach()
                    .create();
```

Configurar uma rede virtual e balanceador de carga antes de criar a definição do conjunto de dimensionamento. O conjunto de dimensionamento utiliza esses recursos para sua configuração inicial.

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a>Criar um balanceador de carga para distribuir a carga em todo o conjunto de dimensionamento

```java
LoadBalancer loadBalancer1 = azure.loadBalancers().define(loadBalancerName1)
                    .withRegion(region)
                    .withExistingResourceGroup(rgName)
                    // assign a public IP address to the load balancer
                    .definePublicFrontend(frontendName)
                        .withExistingPublicIPAddress(publicIPAddress)
                        .attach()
                    // Add two backend address pools
                    .defineBackend(backendPoolName1)
                        .attach()
                    .defineBackend(backendPoolName2)
                        .attach()
                    // Add two health probes on 80 and 443
                    .defineHttpProbe(httpProbe)
                        .withRequestPath("/")
                        .withPort(80)
                        .attach()
                    .defineHttpProbe(httpsProbe)
                        .withRequestPath("/")
                        .withPort(443)
                        .attach()

                    // balance HTTP and HTTPs traffic
                    .defineLoadBalancingRule(httpLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(80)
                        .withProbe(httpProbe)
                        .withBackend(backendPoolName1)
                        .attach()
                    .defineLoadBalancingRule(httpsLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(443)
                        .withProbe(httpsProbe)
                        .withBackend(backendPoolName2)
                        .attach()

                    // Add NAT definitions to enable SSH and telnet to the VMs 
                    .defineInboundNatPool(natPool50XXto22)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(5000, 5099)
                        .withBackendPort(22)
                        .attach()
                    .defineInboundNatPool(natPool60XXto23)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(6000, 6099)
                        .withBackendPort(23)
                        .attach()
                    .create();
```

 O balanceador de carga define dois pools de endereço de rede de back-end, um para balancear a carga em HTTP (`backendPoolName1`) e o outro para balancear a carga em HTTPS (`backendPoolName2`).  Os métodos `defineHttpProbe()` configuram os [pontos de extremidade de investigação de integridade](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) nos balanceadores de carga. As regras NAT expõem as portas 22 e 23 nas máquinas virtuais do conjunto de dimensionamento para acesso SSH e telnet.

## <a name="create-a-scale-set"></a>Criar um conjunto de escala
 
```java
 // Create a virtual machine scale set with three virtual machines
 // And, install Apache Web servers on them
VirtualMachineScaleSet virtualMachineScaleSet = azure.virtualMachineScaleSets()
       .define(vmssName)
                .withRegion(region)
                .withExistingResourceGroup(rgName)
                .withSku(VirtualMachineScaleSetSkuTypes.STANDARD_D3_V2)
                .withExistingPrimaryNetworkSubnet(network, "Front-end")
                .withExistingPrimaryInternetFacingLoadBalancer(loadBalancer1)
                .withPrimaryInternetFacingLoadBalancerBackends(backendPoolName1, backendPoolName2)
                .withPrimaryInternetFacingLoadBalancerInboundNatPools(natPool50XXto22, natPool60XXto23)
                .withoutPrimaryInternalLoadBalancer()
                .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                .withRootUsername(userName)
                .withSsh(sshKey)
                .withNewDataDisk(100)
                .withNewDataDisk(100, 1, CachingTypes.READ_WRITE)
                .withNewDataDisk(100, 2, 
                     CachingTypes.READ_WRITE, StorageAccountTypes.STANDARD_LRS)
                .withCapacity(3)
                // Use a VM extension to install Apache Web servers
                .defineNewExtension("CustomScriptForLinux")
                    .withPublisher("Microsoft.OSTCExtensions")
                    .withType("CustomScriptForLinux")
                    .withVersion("1.4")
                    .withMinorVersionAutoUpgrade()
                    .withPublicSetting("fileUris", fileUris)
                    .withPublicSetting("commandToExecute", installCommand)
                    .attach()
                .create();
```

Use a definição de rede virtual e as definições de balanceador de carga criadas na etapa anterior para criar um conjunto de dimensionamento com três instâncias do Linux (`withCapacity(3)`) e três discos de dados de 100 GB cada. A cadeia do método `defineNewExtension()` instala o servidor web Apache em cada VM.

## <a name="list-virtual-machine-scale-set-network-interfaces"></a>Listar as interfaces de rede do conjunto de dimensionamento da máquina virtual

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a>Obter cadeias de conexão SSH para cada máquina virtual do conjunto de dimensionamento

```java
for (VirtualMachineScaleSetVM instance : virtualMachineScaleSet.virtualMachines().list()) {
    System.out.println("Scale set virtual machine instance #" + instance.instanceId());
    System.out.println(instance.id());
    PagedList<VirtualMachineScaleSetNetworkInterface> networkInterfaces = 
         instance.listNetworkInterfaces();
    // Pick the first NIC on the instance and use its primary IP address
    VirtualMachineScaleSetNetworkInterface networkInterface = networkInterfaces.get(0);
    for (VirtualMachineScaleSetNicIPConfiguration ipConfig : networkInterface.ipConfigurations().values()) {
        if (ipConfig.isPrimary()) {
            List<LoadBalancerInboundNatRule> natRules = ipConfig.listAssociatedLoadBalancerInboundNatRules();
            for (LoadBalancerInboundNatRule natRule : natRules) {
                // find rule matching the inbound SSH port on the backend for the IP address
                // and return the SSH connection string to that port on the load balancer
                if (natRule.backendPort() == 22) {
                    System.out.println("SSH connection string: " + userName + 
                        "@" + publicIPAddress.fqdn() + ":" + natRule.frontendPort());
                break;
                }
            }
            break;
        }
    }
}
```

O pool NAT criado anteriormente mapeou as portas SSH e telnet (22 e 23, respectivamente) nas máquinas virtuais para as portas no balanceador de carga. Esse código cria a cadeia de conexão SSH para cada máquina virtual.

## <a name="stop-the-virtual-machine-scale-set"></a>Parar o conjunto de dimensionamento de máquinas virtuais

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

As máquinas virtuais interrompidas continuam a consumir recursos reservados. Use `deallocate()` para parar o sistema operacional nas máquinas virtuais e liberar seus recursos de computação.

## <a name="deallocate-the-virtual-machine-scale-set"></a>Desalocar o conjunto de dimensionamento de máquina virtual

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

Deallocate() desliga o sistema operacional nas máquinas virtuais e libera os recursos de computação e de rede (como endereços IP) usados pelas instâncias do conjunto de dimensionamento. Você continuará a pagar o armazenamento de discos (incluindo o sistema operacional) conectados às máquinas virtuais.

## <a name="start-a-virtual-machine-scale-set"></a>Iniciar um conjunto de dimensionamento de máquinas virtuais

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a>Atualize o número de instâncias de máquinas virtuais no conjunto de dimensionamento
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

Aumentar o número de máquinas virtuais no conjunto de dimensionamento usando `withCapacity()` e dimensionar a capacidade de cada máquina virtual usando `withSku()`.

## <a name="sample-explanation"></a>Explicação do exemplo

[O exemplo de código](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) primeiro cria uma rede virtual para o conjunto de dimensionamento para se comunicar e um balanceador de carga para distribuir o tráfego entre as máquinas virtuais. A cadeia de método `azure.virtualMachineScaleSets().define()...create()` cria o conjunto de dimensionamento com três instâncias Linux executando o servidor Web Apache.    
   
| Classe usada no exemplo | Observações
|-------|-------|
| [VirtualMachineScaleSet](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | Consultar, iniciar, parar, atualizar e excluir todas as máquinas virtuais no conjunto de dimensionamento.
| [VirtualMachineScaleSetVM](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | Recuperados de `virtualMachineScaleSet.virtualMachines().get()` ou `list()`, permite consultar, iniciar, parar, configurar e excluir as máquinas virtuais no conjunto de dimensionamento.
| [VirtualMachineScaleSetNetworkInterface](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | Retornado de `virtualMachineScaleSet.listNetworkInterfaces()`, representação somente leitura de uma interface de rede em uma máquina virtual em um conjunto de dimensionamento.
| [VirtualMachineScaleSetSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | Classe de campos estáticos usada para definir a [camada do conjunto de dimensionamento de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) usado para definir o quanto os membros do conjunto de dimensionamento de recursos podem consumir.
| [VirtualMachineScaleSetNicIpConfiguration](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | Usado para consultar a configuração de IP associada a uma interface de rede em uma máquina de virtual do conjunto de dimensionamento.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [next-steps](includes/java-next-steps.md)]