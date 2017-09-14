---
title: "Bibliotecas de Máquina Virtual do Azure para Java"
description: 
keywords: "Azure, Java, SDK, API, Computação, Máquinas Virtuais"
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: b414f4dc9289958c2562ddc6d41133279f47a45e
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="c74aa-103">Bibliotecas de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="c74aa-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="c74aa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c74aa-104">Overview</span></span>

<span data-ttu-id="c74aa-105">Recursos de computação escalonáveis, sob demanda que executam Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="c74aa-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="c74aa-106">Para começar a usar máquinas virtuais do Azure, consulte [Criar uma máquina virtual Linux com o portal do Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="c74aa-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="c74aa-107">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c74aa-107">Management API</span></span>

<span data-ttu-id="c74aa-108">Criar, configurar e expandir máquinas virtuais Windows e Linux no Azure a partir do seu código com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c74aa-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="c74aa-109">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c74aa-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.2.1</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="c74aa-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c74aa-110">Example</span></span>

<span data-ttu-id="c74aa-111">Criar uma nova máquina virtual Linux em um novo grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c74aa-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c74aa-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c74aa-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a><span data-ttu-id="c74aa-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c74aa-113">Samples</span></span>

<span data-ttu-id="c74aa-114">[Gerenciar máquinas virtuais][1] </span><span class="sxs-lookup"><span data-stu-id="c74aa-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="c74aa-115">[Gerenciar redes virtuais][6] </span><span class="sxs-lookup"><span data-stu-id="c74aa-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="c74aa-116">[Criar uma máquina virtual com base em uma imagem personalizada][2] </span><span class="sxs-lookup"><span data-stu-id="c74aa-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="c74aa-117">[Criar máquinas virtuais entre regiões em paralelo][5]  </span><span class="sxs-lookup"><span data-stu-id="c74aa-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="c74aa-118">[Criar um conjunto de dimensionamento de máquinas virtuais com um balanceador de carga][7]</span><span class="sxs-lookup"><span data-stu-id="c74aa-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="c74aa-119">Explorar mais [exemplos de código Java para máquinas virtuais do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c74aa-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>