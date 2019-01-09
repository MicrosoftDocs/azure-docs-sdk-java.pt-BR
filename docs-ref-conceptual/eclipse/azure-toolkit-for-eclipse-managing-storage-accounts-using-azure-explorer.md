---
title: Gerenciar contas de armazenamento usando o Azure Explorer para Eclipse
description: Saiba como gerenciar suas contas de armazenamento do Azure usando o Azure Explorer para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: dc39298d88f2fb0b2f56d6fbc0071b68b8d27989
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636652"
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="137d8-103">Gerenciar contas de armazenamento usando o Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="137d8-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="137d8-104">O Azure Explorer, que faz parte do Kit de ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar contas de armazenamento em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) Eclipse.</span><span class="sxs-lookup"><span data-stu-id="137d8-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="137d8-105">Criar uma conta de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="137d8-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="137d8-106">Para criar uma conta de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="137d8-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="137d8-107">Entre em sua conta do Azure usando as [Instruções de conexão para o Kit de ferramentas do Azure para Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="137d8-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

1. <span data-ttu-id="137d8-108">Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Contas de Armazenamento** e, em seguida, clique em **Criar Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="137d8-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando para Criar Conta de Armazenamento][CS01]

1. <span data-ttu-id="137d8-110">Na caixa de diálogo **Criar Conta de Armazenamento**, especifique as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="137d8-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Caixa de diálogo Criar Nova Conta de Armazenamento][CS02]

   * <span data-ttu-id="137d8-112">**Nome**: especifica o nome que você deseja usar para a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="137d8-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="137d8-113">**Assinatura**: especifica a assinatura do Azure que você deseja usar para a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="137d8-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="137d8-114">**Grupo de Recursos**: especifica o grupo de recursos para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="137d8-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="137d8-115">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="137d8-115">Select one of the following options:</span></span>
      * <span data-ttu-id="137d8-116">**Criar novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="137d8-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="137d8-117">**Usar existente**: especifica que você selecionará em uma lista de grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="137d8-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="137d8-118">**Região**: especifica a localização em que sua conta de armazenamento será criada (por exemplo, "Oeste dos EUA").</span><span class="sxs-lookup"><span data-stu-id="137d8-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="137d8-119">**Tipo de conta**: especifica o tipo de conta de armazenamento a ser criada (por exemplo, "Armazenamento de Blobs").</span><span class="sxs-lookup"><span data-stu-id="137d8-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="137d8-120">Para saber mais, confira [Sobre as contas de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="137d8-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="137d8-121">**Desempenho**: especifica qual oferta de conta de armazenamento usar do editor selecionado (por exemplo "Premium").</span><span class="sxs-lookup"><span data-stu-id="137d8-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="137d8-122">Para saber mais, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="137d8-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="137d8-123">**Replicação**: especifica a replicação para a conta de armazenamento (por exemplo "Com Redundância de Zona").</span><span class="sxs-lookup"><span data-stu-id="137d8-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="137d8-124">Para saber mais, veja [Replicação de Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="137d8-124">For more information, see [Azure storage replication].</span></span>

1. <span data-ttu-id="137d8-125">Quando você tiver especificado todas as opções anteriores, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="137d8-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="137d8-126">Criar um contêiner de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="137d8-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="137d8-127">Para criar um contêiner de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="137d8-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="137d8-128">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na conta de armazenamento em que deseja criar um contêiner e, em seguida, clique em **Criar contêiner de blob**.</span><span class="sxs-lookup"><span data-stu-id="137d8-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Comando Criar contêiner de blob][CC01]

1. <span data-ttu-id="137d8-130">Na caixa de diálogo **Criar Contêiner de Blob**, especifique o nome do seu contêiner e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="137d8-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="137d8-131">Para saber mais sobre como nomear contêineres de armazenamento, veja [Nomeando e referenciando contêineres, blobs e metadados].</span><span class="sxs-lookup"><span data-stu-id="137d8-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Caixa de diálogo Criar contêiner de blob][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="137d8-133">Excluir um contêiner de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="137d8-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="137d8-134">Para excluir um contêiner de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="137d8-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="137d8-135">Na exibição **Azure Explorer**, clique com o botão direito do mouse no contêiner de armazenamento e, em seguida, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="137d8-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Comando Excluir contêiner de armazenamento][DC01]

1. <span data-ttu-id="137d8-137">Na janela de confirmação, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="137d8-137">In the confirmation window, click **OK**.</span></span>

   ![Janela de confirmação de Excluir contêiner de armazenamento][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="137d8-139">Excluir uma conta de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="137d8-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="137d8-140">Para excluir uma conta de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="137d8-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="137d8-141">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na conta de armazenamento e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="137d8-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Comando Excluir conta de armazenamento][DS01]

1. <span data-ttu-id="137d8-143">Na janela de confirmação, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="137d8-143">In the confirmation window, click **OK**.</span></span>

   ![Janela de confirmação de Excluir conta de armazenamento][DS02]

## <a name="next-steps"></a><span data-ttu-id="137d8-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="137d8-145">Next steps</span></span>

<span data-ttu-id="137d8-146">Para saber mais sobre os tamanhos, preços e contas de armazenamento do Azure, veja os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="137d8-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="137d8-147">[Introdução ao Armazenamento do Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="137d8-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="137d8-148">[Sobre as contas de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="137d8-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="137d8-149">Tamanhos de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="137d8-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="137d8-150">[Tamanhos das contas de armazenamento do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="137d8-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="137d8-151">[Tamanhos das contas de armazenamento do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="137d8-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="137d8-152">Preços da conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="137d8-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="137d8-153">[Preços da conta de armazenamento do Windows]</span><span class="sxs-lookup"><span data-stu-id="137d8-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="137d8-154">[Preços da conta de armazenamento do Linux]</span><span class="sxs-lookup"><span data-stu-id="137d8-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Introdução ao Armazenamento do Microsoft Azure]: /azure/storage/storage-introduction
[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction
[Sobre as contas de armazenamento do Azure]: /azure/storage/storage-create-storage-account
[About Azure storage accounts]: /azure/storage/storage-create-storage-account
[Replicação de Armazenamento do Azure]: /azure/storage/storage-redundancy
[Azure storage replication]: /azure/storage/storage-redundancy
[Metas de desempenho e escalabilidade do Armazenamento do Azure]: /azure/storage/storage-scalability-targets
[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets
[Nomeando e referenciando contêineres, blobs e metadados]: http://go.microsoft.com/fwlink/?LinkId=255555
[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tamanhos das contas de armazenamento do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das contas de armazenamento do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços da conta de armazenamento do Windows]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Windows storage-account pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Preços da conta de armazenamento do Linux]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/
[Linux storage-account pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
