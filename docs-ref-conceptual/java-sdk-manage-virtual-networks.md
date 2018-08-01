---
title: Gerenciar redes virtuais do Azure com Java | Microsoft Docs
description: Exemplo de código para gerenciar redes virtuais do Azure em seu código Java
author: rloutlaw
manager: douge
ms.assetid: 92736911-3df6-46e7-b751-25bb36bf89b9
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 3d21cdd890912c1fc58fc65a79ba972b8327edeb
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931082"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a>Criar e gerenciar redes virtuais do Azure de seus aplicativos Java

[Este exemplo](https://github.com/Azure-Samples/network-java-manage-virtual-network) cria uma [rede virtual](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) para isolar os recursos do Azure no segmento de rede que você controla.

## <a name="run-the-sample"></a>Execute o exemplo

Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador. Em seguida, execute:

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).

## <a name="authenticate-with-azure"></a>Autenticar com o Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a>Criar um grupo de segurança de rede para bloquear o tráfego de Internet

```java
// this NSG definition block traffic to and from the public Internet
NetworkSecurityGroup backEndSubnetNsg = azure.networkSecurityGroups()
              .define(vnet1BackEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .defineRule("DenyInternetInComing")
                        .denyInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

Essa [regra de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) bloqueia o tráfego de Internet público de entrada e saída. Esse grupo de segurança de rede não terá efeito até que ele seja aplicado a uma sub-rede na sua rede virtual.

## <a name="create-a-virtual-network-with-two-subnets"></a>Criar uma rede virtual com duas sub-redes

```java
// create the a virtual network with two subnets
// assign the backend subnet a rule blocking public internet traffic
Network virtualNetwork1 = azure.networks().define(vnetName1)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withAddressSpace("192.168.0.0/16")
                    .withSubnet(vnet1FrontEndSubnetName, "192.168.1.0/24")
                    .defineSubnet(vnet1BackEndSubnetName)
                        .withAddressPrefix("192.168.2.0/24")
                        .withExistingNetworkSecurityGroup(backEndSubnetNsg)
                        .attach()
                    .create();
```

A sub-rede de back-end nega acesso de Internet usando as regras definidas no grupo de segurança de rede. A sub-rede de front-end usa as [regras padrões](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) que permitem o tráfego de saída para a Internet.

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a>Criar um grupo de segurança de rede para permitir o tráfego HTTP de entrada
```java
// create a rule that allows inbound HTTP and blocks outbound Internet traffic
NetworkSecurityGroup frontEndSubnetNsg = azure.networkSecurityGroups()
               .define(vnet1FrontEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .defineRule("AllowHttpInComing")
                        .allowInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toPort(80)
                        .withProtocol(SecurityRuleProtocol.TCP)
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

Essa regra de segurança de rede abre o tráfego de entrada na porta 80 da Internet pública e bloqueia o tráfego de saída de dentro da rede para a Internet pública. 

## <a name="update-a-virtual-network"></a>Atualizar uma rede virtual
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

Atualize a sub-rede de front-end para permitir o tráfego HTTP de entrada usando a regra de segurança de rede criada na etapa anterior.

## <a name="create-a-virtual-machine-on-a-subnet"></a>Criar uma máquina virtual em uma sub-rede
```java
// attach the new VM to the front end subnet on the virtual network
VirtualMachine frontEndVM = azure.virtualMachines().define(frontEndVmName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withExistingPrimaryNetwork(virtualNetwork1) 
                    .withSubnet(vnet1FrontEndSubnetName)
                    .withPrimaryPrivateIpAddressDynamic()
                    .withNewPrimaryPublicIpAddress(publicIpAddressLeafDnsForFrontEndVm)
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();
```

`withExistingPrimaryNetwork()`e `withSubnet()` configuram a máquina virtual para usar a sub-rede de front-end em uma rede virtual criada nas etapas anteriores.

## <a name="list-virtual-networks-in-a-resource-group"></a>Lista as redes virtuais em um grupo de recursos
```java
// iterate over every virtual network in the resource group 
for (Network virtualNetwork : azure.networks().listByResourceGroup(rgName)) {
    // for each subnet on the virtual network, log the network address prefix 
    for (Map.Entry<String, Subnet> entry : virtualNetwork.subnets().entrySet()) {
        String subnetName = entry.getKey();
        Subnet subnet = entry.getValue();
        System.out.println("Address prefix for subnet " + subnetName + 
             " is " + subnet.addressPrefix());
    }
}
```       

Você pode listar e inspecionar o objeto `Network` usando a coleção externa ou iterar por meio de cada recurso filho para cada rede usando o loop foreach aninhado, como mostrado neste exemplo.

## <a name="delete-a-virtual-network"></a>Excluir uma rede virtual
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

Remover uma rede virtual exclui as sub-redes na rede, mas não exclui as regras do grupo de segurança de rede aplicadas às sub-redes. Essas definições podem ser reaplicadas para outras sub-redes.

## <a name="sample-explanation"></a>Explicação do exemplo

Este exemplo cria uma rede virtual com duas sub-redes e uma máquina virtual em cada sub-rede. A sub-rede de fundo é separada da Internet pública. A sub-rede frontal aceita tráfego de HTTP de entrada da Internet. As máquinas virtuais e a rede virtual se comunicam entre si através das regras do grupo de segurança de rede padrão.

| Classe usada no exemplo | Observações
|-------|-------|
| [Rede](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | Representação de objeto de local da rede virtual criada a partir de `azure.networks().define()...create()` . Use a cadeia fluente `update()...apply()` para atualizar uma rede virtual existente.
| [Sub-rede](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | Criar sub-redes na rede virtual ao definir ou atualizar a rede usando `withSubnet()`. Obter representações de objeto de uma sub-rede a partir de `Network.subnets().get()` ou `Network.subnets().entrySet()`. Esses objetos possuem métodos para consultar propriedades de sub-rede.
| [NetworkSecurityGroup](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | Criado usando a cadeia fluente `azure.networkSecurityGroups().define()...create()` e, em seguida, aplicado às sub-redes através da atualização ou criação de sub-redes em uma rede virtual. 

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [next-steps](includes/java-next-steps.md)]