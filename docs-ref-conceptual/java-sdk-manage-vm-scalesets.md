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
ms.openlocfilehash: 4653726b387369c18942b6c11392f15b9f0351f3
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893487"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a><span data-ttu-id="8c78a-103">Gerenciar conjuntos de dimensionamento das máquinas virtuais do Azure a partir dos seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="8c78a-103">Manage Azure virtual machine scale sets from your Java applications</span></span>

<span data-ttu-id="8c78a-104">[Este exemplo](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) cria um [conjunto de dimensionamento de máquina virtual](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) usando as [bibliotecas de gerenciamento do Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="8c78a-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) creates a  [virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="8c78a-105">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="8c78a-105">Run the sample</span></span>

<span data-ttu-id="8c78a-106">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8c78a-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="8c78a-107">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="8c78a-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

<span data-ttu-id="8c78a-108">Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span><span class="sxs-lookup"><span data-stu-id="8c78a-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="8c78a-109">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="8c78a-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a><span data-ttu-id="8c78a-110">Criar uma rede virtual para o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8c78a-110">Create a virtual network for the scale set</span></span>

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

<span data-ttu-id="8c78a-111">Configurar uma rede virtual e balanceador de carga antes de criar a definição do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8c78a-111">Set up a virtual network and load balancer before creating the scale set definition.</span></span> <span data-ttu-id="8c78a-112">O conjunto de dimensionamento utiliza esses recursos para sua configuração inicial.</span><span class="sxs-lookup"><span data-stu-id="8c78a-112">The scale set uses these resources for its initial configuration.</span></span>

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a><span data-ttu-id="8c78a-113">Criar um balanceador de carga para distribuir a carga em todo o conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8c78a-113">Create a load balancer to distribute load across the scale set</span></span>

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

 <span data-ttu-id="8c78a-114">O balanceador de carga define dois pools de endereço de rede de back-end, um para balancear a carga em HTTP (`backendPoolName1`) e o outro para balancear a carga em HTTPS (`backendPoolName2`).</span><span class="sxs-lookup"><span data-stu-id="8c78a-114">The load balancer defines two backend network address pools-one to balance load across HTTP (`backendPoolName1`) and the other to balance load across HTTPS (`backendPoolName2`).</span></span>  <span data-ttu-id="8c78a-115">Os métodos `defineHttpProbe()` configuram os [pontos de extremidade de investigação de integridade](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) nos balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="8c78a-115">The `defineHttpProbe()` methods set up [health probe endpoints](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) on the load balancers.</span></span> <span data-ttu-id="8c78a-116">As regras NAT expõem as portas 22 e 23 nas máquinas virtuais do conjunto de dimensionamento para acesso SSH e telnet.</span><span class="sxs-lookup"><span data-stu-id="8c78a-116">NAT rules expose ports 22 and 23 on the scale set virtual machines for telnet and SSH access.</span></span>

## <a name="create-a-scale-set"></a><span data-ttu-id="8c78a-117">Criar um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="8c78a-117">Create a scale set</span></span>
 
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

<span data-ttu-id="8c78a-118">Use a definição de rede virtual e as definições de balanceador de carga criadas na etapa anterior para criar um conjunto de dimensionamento com três instâncias do Linux (`withCapacity(3)`) e três discos de dados de 100 GB cada.</span><span class="sxs-lookup"><span data-stu-id="8c78a-118">Use the virtual network definition and load balancer definitions created in the previous step to create a scale set with three Linux instances (`withCapacity(3)`) and three 100GB data disks each.</span></span> <span data-ttu-id="8c78a-119">A cadeia do método `defineNewExtension()` instala o servidor web Apache em cada VM.</span><span class="sxs-lookup"><span data-stu-id="8c78a-119">The `defineNewExtension()` method chain installs the Apache web server on each VM.</span></span>

## <a name="list-virtual-machine-scale-set-network-interfaces"></a><span data-ttu-id="8c78a-120">Listar as interfaces de rede do conjunto de dimensionamento da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8c78a-120">List virtual machine scale set network interfaces</span></span>

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a><span data-ttu-id="8c78a-121">Obter cadeias de conexão SSH para cada máquina virtual do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8c78a-121">Get SSH connection strings for each scale set virtual machine</span></span>

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

<span data-ttu-id="8c78a-122">O pool NAT criado anteriormente mapeou as portas SSH e telnet (22 e 23, respectivamente) nas máquinas virtuais para as portas no balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8c78a-122">The NAT pool created earlier mapped the SSH and telnet ports (22 and 23, respectively) on the virtual machines to ports on the load balancer.</span></span> <span data-ttu-id="8c78a-123">Esse código cria a cadeia de conexão SSH para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c78a-123">This code builds the SSH connection string for each virtual machine.</span></span>

## <a name="stop-the-virtual-machine-scale-set"></a><span data-ttu-id="8c78a-124">Parar o conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8c78a-124">Stop the virtual machine scale set</span></span>

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

<span data-ttu-id="8c78a-125">As máquinas virtuais interrompidas continuam a consumir recursos reservados.</span><span class="sxs-lookup"><span data-stu-id="8c78a-125">Stopped virtual machines continue to consume reserved resources.</span></span> <span data-ttu-id="8c78a-126">Use `deallocate()` para parar o sistema operacional nas máquinas virtuais e liberar seus recursos de computação.</span><span class="sxs-lookup"><span data-stu-id="8c78a-126">Use `deallocate()` to stop the operating system on the virtual machines and release their compute resources.</span></span>

## <a name="deallocate-the-virtual-machine-scale-set"></a><span data-ttu-id="8c78a-127">Desalocar o conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8c78a-127">Deallocate the virtual machine scale set</span></span>

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

<span data-ttu-id="8c78a-128">Deallocate() desliga o sistema operacional nas máquinas virtuais e libera os recursos de computação e de rede (como endereços IP) usados pelas instâncias do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8c78a-128">Deallocate() shuts down the operating system on the virtual machines and frees up the compute and network resources (such as IP addresses) used by the scale set instances.</span></span> <span data-ttu-id="8c78a-129">Você continuará a pagar o armazenamento de discos (incluindo o sistema operacional) conectados às máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8c78a-129">You continue to accrue storage charges for any disks (including the OS) attached to the virtual machines.</span></span>

## <a name="start-a-virtual-machine-scale-set"></a><span data-ttu-id="8c78a-130">Iniciar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8c78a-130">Start a virtual machine scale set</span></span>

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a><span data-ttu-id="8c78a-131">Atualize o número de instâncias de máquinas virtuais no conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8c78a-131">Update the number of virtual machines instances in the scale set</span></span>
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

<span data-ttu-id="8c78a-132">Aumentar o número de máquinas virtuais no conjunto de dimensionamento usando `withCapacity()` e dimensionar a capacidade de cada máquina virtual usando `withSku()`.</span><span class="sxs-lookup"><span data-stu-id="8c78a-132">Scale the number of virtual machines in the scale set using `withCapacity()` and scale the capacity of each virtual machine using `withSku()`.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="8c78a-133">Explicação do exemplo</span><span class="sxs-lookup"><span data-stu-id="8c78a-133">Sample explanation</span></span>

<span data-ttu-id="8c78a-134">[O exemplo de código](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) primeiro cria uma rede virtual para o conjunto de dimensionamento para se comunicar e um balanceador de carga para distribuir o tráfego entre as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8c78a-134">[The sample code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) first creates a virtual network for the scale set to communicate across and a load balancer to distribute traffic across the virtual machines.</span></span> <span data-ttu-id="8c78a-135">A cadeia de método `azure.virtualMachineScaleSets().define()...create()` cria o conjunto de dimensionamento com três instâncias Linux executando o servidor Web Apache.</span><span class="sxs-lookup"><span data-stu-id="8c78a-135">The `azure.virtualMachineScaleSets().define()...create()` method chain creates the scale set with three Linux instances running the Apache web server.</span></span>    
   
| <span data-ttu-id="8c78a-136">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="8c78a-136">Class used in sample</span></span> | <span data-ttu-id="8c78a-137">Observações</span><span class="sxs-lookup"><span data-stu-id="8c78a-137">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="8c78a-138">VirtualMachineScaleSet</span><span class="sxs-lookup"><span data-stu-id="8c78a-138">VirtualMachineScaleSet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | <span data-ttu-id="8c78a-139">Consultar, iniciar, parar, atualizar e excluir todas as máquinas virtuais no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8c78a-139">Query, start, stop, update and delete all virtual machines in the scale set.</span></span>
| [<span data-ttu-id="8c78a-140">VirtualMachineScaleSetVM</span><span class="sxs-lookup"><span data-stu-id="8c78a-140">VirtualMachineScaleSetVM</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | <span data-ttu-id="8c78a-141">Recuperados de `virtualMachineScaleSet.virtualMachines().get()` ou `list()`, permite consultar, iniciar, parar, configurar e excluir as máquinas virtuais no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8c78a-141">Retrieved from `virtualMachineScaleSet.virtualMachines().get()` or `list()`, allows you to query, start, stop, configure and delete virtual machines in the scale set.</span></span>
| [<span data-ttu-id="8c78a-142">VirtualMachineScaleSetNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8c78a-142">VirtualMachineScaleSetNetworkInterface</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | <span data-ttu-id="8c78a-143">Retornado de `virtualMachineScaleSet.listNetworkInterfaces()`, representação somente leitura de uma interface de rede em uma máquina virtual em um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8c78a-143">Returned from `virtualMachineScaleSet.listNetworkInterfaces()`, read-only representation of a network interface on a virtual machine in a scale set.</span></span>
| [<span data-ttu-id="8c78a-144">VirtualMachineScaleSetSkuTypes</span><span class="sxs-lookup"><span data-stu-id="8c78a-144">VirtualMachineScaleSetSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | <span data-ttu-id="8c78a-145">Classe de campos estáticos usada para definir a [camada do conjunto de dimensionamento de máquina virtual](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) usado para definir o quanto os membros do conjunto de dimensionamento de recursos podem consumir.</span><span class="sxs-lookup"><span data-stu-id="8c78a-145">Class of static fields used to set the [virtual machine scale set tier](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) used to define how much resources scale set members can consume.</span></span>
| [<span data-ttu-id="8c78a-146">VirtualMachineScaleSetNicIpConfiguration</span><span class="sxs-lookup"><span data-stu-id="8c78a-146">VirtualMachineScaleSetNicIpConfiguration</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | <span data-ttu-id="8c78a-147">Usado para consultar a configuração de IP associada a uma interface de rede em uma máquina de virtual do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8c78a-147">Used to query the IP configuration associated with a network interface on a scale set virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c78a-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c78a-148">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]