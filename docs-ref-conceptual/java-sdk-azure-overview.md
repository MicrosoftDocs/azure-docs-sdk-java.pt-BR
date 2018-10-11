---
title: Bibliotecas do Azure para Java
description: Visão geral do gerenciamento do Azure e bibliotecas de serviço para Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892727"
---
# <a name="azure-libraries-for-java"></a>Bibliotecas do Azure para Java

As bibliotecas do Azure para Java ajudam a gerenciar recursos do Azure e conectam-se aos serviços do seu código do aplicativo. As bibliotecas estão disponíveis como [importações de Maven](java-sdk-azure-install.md) para uso em seus projetos de Java. 

## <a name="manage-azure-resources"></a>Gerenciar recursos do Azure

Criar e gerenciar recursos do Azure a partir de aplicativos Java usando as [bibliotecas de gerenciamento do Azure para Java](java-sdk-azure-get-started.md). Use essas bibliotecas para criar seus próprios serviços e ferramentas de automação do Azure. 

Por exemplo, para criar uma VM do Linux, você deve escrever o código a seguir:

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

Analise as [instruções de instalação](java-sdk-azure-install.md) para obter uma lista completa das bibliotecas e como importá-las para seus projetos e, em seguida, leia o [artigo de introdução](java-sdk-azure-get-started.md) para configurar a autenticação e executar o código de exemplo em relação a sua assinatura do Azure. 

## <a name="connect-to-azure-services"></a>Conectar-se aos serviços do Azure

Além de usar bibliotecas de Java para criar e gerenciar recursos no Azure, você também pode usar bibliotecas de Java para se conectar e usar esses recursos em seus aplicativos. Por exemplo, você pode atualizar um Banco de Dados SQL de tabela ou armazenar arquivos no Armazenamento do Azure. Selecione a biblioteca necessária para um serviço específico na [lista completa das bibliotecas](java-sdk-azure-install.md) e visite a [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/) para ver os tutoriais e exemplos de código e obter ajuda para usá-las em seus aplicativos.

Por exemplo, para imprimir o conteúdo de cada blob em um contêiner de armazenamento do Azure:

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a>Referência e código de exemplo

Os exemplos a seguir abordam tarefas comuns de automação com as bibliotecas de gerenciamento do Azure para Java e possuem códigos prontos para uso em seus próprios aplicativos:

- [Máquinas virtuais](java-sdk-azure-virtual-machine-samples.md)
- [Aplicativos Web](java-sdk-azure-web-apps-samples.md)
- [Banco de Dados SQL](java-sdk-azure-sql-database-samples.md)
   
Uma [referência](https://docs.microsoft.com/java/api) está disponível para todos os pacotes nas bibliotecas de serviço e de gerenciamento. Novos recursos, alterações significativas, e instruções de migração de versões anteriores estão disponíveis nas [notas de versão](java-sdk-azure-release-notes.md).