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
ms.openlocfilehash: 58016d4eef7d6548b2bd5302abcebf78f9cd7bcf
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-machine-libraries"></a>Bibliotecas de máquina virtual do Azure

## <a name="overview"></a>Visão geral

Recursos de computação escalonáveis, sob demanda que executam Linux ou Windows.

Para começar a usar máquinas virtuais do Azure, consulte [Criar uma máquina virtual Linux com o portal do Azure](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API de Gerenciamento

Criar, configurar e expandir máquinas virtuais Windows e Linux no Azure a partir do seu código com a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.1.2</version>
</dependency>
```   


## <a name="example"></a>Exemplo

Criar uma nova máquina virtual Linux em um novo grupo de recursos do Azure.

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
> [Explorar as APIs de Gerenciamento](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a>Exemplos

[Gerenciar máquinas virtuais][1]   
[Gerenciar redes virtuais][6]   
[Criar uma máquina virtual com base em uma imagem personalizada][2]   
[Criar máquinas virtuais entre regiões em paralelo][5]    
[Criar um conjunto de dimensionamento de máquinas virtuais com um balanceador de carga][7]    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

Explorar mais [exemplos de código Java para máquinas virtuais do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que você pode usar em seus aplicativos.