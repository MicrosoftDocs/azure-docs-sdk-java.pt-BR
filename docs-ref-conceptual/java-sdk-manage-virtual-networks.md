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
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a><span data-ttu-id="9f153-103">Criar e gerenciar redes virtuais do Azure de seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="9f153-103">Create and manage Azure virtual networks from your Java apps</span></span>

<span data-ttu-id="9f153-104">[Este exemplo](https://github.com/Azure-Samples/network-java-manage-virtual-network) cria uma [rede virtual](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) para isolar os recursos do Azure no segmento de rede que você controla.</span><span class="sxs-lookup"><span data-stu-id="9f153-104">[This sample](https://github.com/Azure-Samples/network-java-manage-virtual-network) creates a [virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) to isolate your Azure resources on network segment you control.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="9f153-105">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="9f153-105">Run the sample</span></span>

<span data-ttu-id="9f153-106">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f153-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="9f153-107">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="9f153-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

<span data-ttu-id="9f153-108">Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span><span class="sxs-lookup"><span data-stu-id="9f153-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="9f153-109">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="9f153-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a><span data-ttu-id="9f153-110">Criar um grupo de segurança de rede para bloquear o tráfego de Internet</span><span class="sxs-lookup"><span data-stu-id="9f153-110">Create a network security group to block Internet traffic</span></span>

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

<span data-ttu-id="9f153-111">Essa [regra de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) bloqueia o tráfego de Internet público de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="9f153-111">This [network security rule](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) blocks both inbound and outbound public Internet traffic.</span></span> <span data-ttu-id="9f153-112">Esse grupo de segurança de rede não terá efeito até que ele seja aplicado a uma sub-rede na sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9f153-112">This network security group will not have an effect until applied to a subnet in your virtual network.</span></span>

## <a name="create-a-virtual-network-with-two-subnets"></a><span data-ttu-id="9f153-113">Criar uma rede virtual com duas sub-redes</span><span class="sxs-lookup"><span data-stu-id="9f153-113">Create a virtual network with two subnets</span></span>

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

<span data-ttu-id="9f153-114">A sub-rede de back-end nega acesso de Internet usando as regras definidas no grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="9f153-114">The backend subnet denies Internet access usingfollowing the rules set in the network security group.</span></span> <span data-ttu-id="9f153-115">A sub-rede de front-end usa as [regras padrões](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) que permitem o tráfego de saída para a Internet.</span><span class="sxs-lookup"><span data-stu-id="9f153-115">The front end subnet uses the [default rules](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) which allow outbound traffic to the Internet.</span></span>

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a><span data-ttu-id="9f153-116">Criar um grupo de segurança de rede para permitir o tráfego HTTP de entrada</span><span class="sxs-lookup"><span data-stu-id="9f153-116">Create a network security group to allow inbound HTTP traffic</span></span>
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

<span data-ttu-id="9f153-117">Essa regra de segurança de rede abre o tráfego de entrada na porta 80 da Internet pública e bloqueia o tráfego de saída de dentro da rede para a Internet pública.</span><span class="sxs-lookup"><span data-stu-id="9f153-117">This network security rule opens up inbound traffic on port 80 from the public Internet, and blocks all outbound traffic from inside the network to the public Internet.</span></span> 

## <a name="update-a-virtual-network"></a><span data-ttu-id="9f153-118">Atualizar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="9f153-118">Update a virtual network</span></span>
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

<span data-ttu-id="9f153-119">Atualize a sub-rede de front-end para permitir o tráfego HTTP de entrada usando a regra de segurança de rede criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="9f153-119">Update the front end subnet to allow inbound HTTP traffic using the network security rule created in the previous step.</span></span>

## <a name="create-a-virtual-machine-on-a-subnet"></a><span data-ttu-id="9f153-120">Criar uma máquina virtual em uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="9f153-120">Create a virtual machine on a subnet</span></span>
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

<span data-ttu-id="9f153-121">`withExistingPrimaryNetwork()`e `withSubnet()` configuram a máquina virtual para usar a sub-rede de front-end em uma rede virtual criada nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="9f153-121">`withExistingPrimaryNetwork()` and `withSubnet()` configure the virtual machine to use the front-end subnet on the virtual network created in the previous steps.</span></span>

## <a name="list-virtual-networks-in-a-resource-group"></a><span data-ttu-id="9f153-122">Lista as redes virtuais em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9f153-122">List virtual networks in a resource group</span></span>
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

<span data-ttu-id="9f153-123">Você pode listar e inspecionar o objeto `Network` usando a coleção externa ou iterar por meio de cada recurso filho para cada rede usando o loop foreach aninhado, como mostrado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9f153-123">You can list and inspect `Network` object using the outer collection or iterate through each child resource for each network using the nested for-each loop as seen in this example.</span></span>

## <a name="delete-a-virtual-network"></a><span data-ttu-id="9f153-124">Excluir uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="9f153-124">Delete a virtual network</span></span>
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

<span data-ttu-id="9f153-125">Remover uma rede virtual exclui as sub-redes na rede, mas não exclui as regras do grupo de segurança de rede aplicadas às sub-redes.</span><span class="sxs-lookup"><span data-stu-id="9f153-125">Removing a virtual network deletes the subnets on the network but does not delete the network security group rules applied to the subnets.</span></span> <span data-ttu-id="9f153-126">Essas definições podem ser reaplicadas para outras sub-redes.</span><span class="sxs-lookup"><span data-stu-id="9f153-126">Those definitions can be reapplied to other subnets.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="9f153-127">Explicação do exemplo</span><span class="sxs-lookup"><span data-stu-id="9f153-127">Sample explanation</span></span>

<span data-ttu-id="9f153-128">Este exemplo cria uma rede virtual com duas sub-redes e uma máquina virtual em cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9f153-128">This sample creates a virtual network with two subnets and with one virtual machine on each subnet.</span></span> <span data-ttu-id="9f153-129">A sub-rede de fundo é separada da Internet pública.</span><span class="sxs-lookup"><span data-stu-id="9f153-129">The back subnet is cut off from the public Internet.</span></span> <span data-ttu-id="9f153-130">A sub-rede frontal aceita tráfego de HTTP de entrada da Internet.</span><span class="sxs-lookup"><span data-stu-id="9f153-130">The front-facing subnet accepts inbound HTTP traffic from the Internet.</span></span> <span data-ttu-id="9f153-131">As máquinas virtuais e a rede virtual se comunicam entre si através das regras do grupo de segurança de rede padrão.</span><span class="sxs-lookup"><span data-stu-id="9f153-131">Both virtual machines in the virtual network communicate with each other through the default network security group rules.</span></span>

| <span data-ttu-id="9f153-132">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="9f153-132">Class used in sample</span></span> | <span data-ttu-id="9f153-133">Observações</span><span class="sxs-lookup"><span data-stu-id="9f153-133">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="9f153-134">Rede</span><span class="sxs-lookup"><span data-stu-id="9f153-134">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="9f153-135">Representação de objeto de local da rede virtual criada a partir de `azure.networks().define()...create()` .</span><span class="sxs-lookup"><span data-stu-id="9f153-135">Local object representation of the virtual network created from `azure.networks().define()...create()` .</span></span> <span data-ttu-id="9f153-136">Use a cadeia fluente `update()...apply()` para atualizar uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="9f153-136">Use the `update()...apply()` fluent chain to update an existing virtual network.</span></span>
| [<span data-ttu-id="9f153-137">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="9f153-137">Subnet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | <span data-ttu-id="9f153-138">Criar sub-redes na rede virtual ao definir ou atualizar a rede usando `withSubnet()`.</span><span class="sxs-lookup"><span data-stu-id="9f153-138">Create subnets on the virtual network when defining or updating the network using `withSubnet()`.</span></span> <span data-ttu-id="9f153-139">Obter representações de objeto de uma sub-rede a partir de `Network.subnets().get()` ou `Network.subnets().entrySet()`.</span><span class="sxs-lookup"><span data-stu-id="9f153-139">Get object representations of a subnet from `Network.subnets().get()` or `Network.subnets().entrySet()`.</span></span> <span data-ttu-id="9f153-140">Esses objetos possuem métodos para consultar propriedades de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9f153-140">These objects have methods to query subnet properties.</span></span>
| [<span data-ttu-id="9f153-141">NetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9f153-141">NetworkSecurityGroup</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | <span data-ttu-id="9f153-142">Criado usando a cadeia fluente `azure.networkSecurityGroups().define()...create()` e, em seguida, aplicado às sub-redes através da atualização ou criação de sub-redes em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9f153-142">Created using the `azure.networkSecurityGroups().define()...create()` fluent chain and then applied to subnets through the updating or creating subnets in a virtual network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9f153-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f153-143">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]