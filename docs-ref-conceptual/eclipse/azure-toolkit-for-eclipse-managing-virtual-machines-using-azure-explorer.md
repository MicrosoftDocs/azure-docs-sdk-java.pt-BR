---
title: "Gerenciar máquinas virtuais usando o Azure Explorer para Eclipse"
description: "Saiba como gerenciar suas máquinas virtuais do Azure usando o Azure Explorer para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: f7526a49e8ba6432d6bf6af54a725a285a61fc07
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="6e078-103">Gerenciar máquinas virtuais usando o Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e078-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="6e078-104">O Azure Explorer, que faz parte do Kit de ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java uma solução fácil de usar para gerenciar máquinas virtuais em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6e078-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6e078-105">Criar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e078-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="6e078-106">Para criar uma máquina virtual usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6e078-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="6e078-107">Entre em sua conta do Azure usando as (Instruções de conexão para o Kit de ferramentas do Azure para Eclipse).</span><span class="sxs-lookup"><span data-stu-id="6e078-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

1. <span data-ttu-id="6e078-108">Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Máquinas Virtuais** e, em seguida, clique em **Criar VM**.</span><span class="sxs-lookup"><span data-stu-id="6e078-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   ![Comando Criar VM][CR01]  

   <span data-ttu-id="6e078-110">O assistente para **Criar uma nova Máquina Virtual** é aberto.</span><span class="sxs-lookup"><span data-stu-id="6e078-110">The **Create new Virtual Machine** wizard opens.</span></span>

1. <span data-ttu-id="6e078-111">Na caixa de diálogo **Escolha uma Assinatura**, selecione sua assinatura e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="6e078-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![A janela Escolha uma Assinatura][CR02]

1. <span data-ttu-id="6e078-113">Na janela **Selecionar uma Imagem de Máquina Virtual**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6e078-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="6e078-114">**Localização**: especifica o local no qual sua máquina virtual será criada (por exemplo, *Oeste dos EUA*).</span><span class="sxs-lookup"><span data-stu-id="6e078-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="6e078-115">**Editor**: especifica o editor que criou a imagem que você usará para criar sua máquina virtual (por exemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="6e078-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="6e078-116">**Oferta**: especifica qual oferta de máquina virtual do editor selecionado será usada (por exemplo *JDK*).</span><span class="sxs-lookup"><span data-stu-id="6e078-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="6e078-117">**Sku**: especifica qual SKU (unidade de manutenção de estoque) da oferta selecionada será usada (por exemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="6e078-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="6e078-118">**No. de Versão**: especifica qual versão do SKU selecionado será usada.</span><span class="sxs-lookup"><span data-stu-id="6e078-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![A janela Selecionar uma Imagem de Máquina Virtual][CR03]

1. <span data-ttu-id="6e078-120">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="6e078-120">Click **Next**.</span></span>

1. <span data-ttu-id="6e078-121">Na janela **Configurações Básicas de Máquina Virtual**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6e078-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="6e078-122">**Nome da Máquina Virtual**: especifica o nome para sua nova máquina virtual, que deve começar com uma letra e conter somente letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="6e078-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="6e078-123">**Tamanho**: especifica o número de núcleos e a memória para alocar para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e078-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="6e078-124">**Nome de usuário**: especifica a conta de administrador a criar para gerenciar sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e078-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="6e078-125">**Senha** e **Confirmar**: especifica a senha para sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="6e078-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![A janela Configurações Básicas de Máquina Virtual][CR04]

1. <span data-ttu-id="6e078-127">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="6e078-127">Click **Next**.</span></span>

1. <span data-ttu-id="6e078-128">Na janela **Criar Nova Conta de Armazenamento**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6e078-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="6e078-129">**Grupo de Recursos**: especifica o grupo de recursos para suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6e078-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="6e078-130">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="6e078-130">Select one of the following options:</span></span>
      * <span data-ttu-id="6e078-131">**Criar novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6e078-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="6e078-132">**Usar existente**: especifica que você quer selecionar um grupo de recursos que já está associado à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e078-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![A caixa de diálogo Criar Nova Conta de Armazenamento][CR05]

   * <span data-ttu-id="6e078-134">**Conta de armazenamento**: especifica a conta de armazenamento que será usada para armazenar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e078-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="6e078-135">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="6e078-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="6e078-136">**Rede Virtual** e **Sub-rede**: especifica a rede virtual e a sub-rede as quais sua máquina virtual se conectará.</span><span class="sxs-lookup"><span data-stu-id="6e078-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="6e078-137">Use uma rede e sub-rede existentes ou crie uma nova rede e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="6e078-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="6e078-138">Se você selecionar **Criar nova**, a caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="6e078-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![A caixa de diálogo Criar Nova Rede Virtual][CR06]

1. <span data-ttu-id="6e078-140">Na janela **Recursos Associados**, insira as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e078-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="6e078-141">**Endereço IP público**: especifica um endereço IP externo para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e078-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="6e078-142">Você pode optar por criar um novo endereço IP ou, se sua máquina virtual não tiver um endereço IP público, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="6e078-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="6e078-143">**Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e078-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="6e078-144">Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="6e078-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="6e078-145">**Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer.</span><span class="sxs-lookup"><span data-stu-id="6e078-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="6e078-146">Você pode selecionar um conjunto de disponibilidade existente, criar um novo conjunto de disponibilidade ou, se sua máquina virtual não for pertencer a um conjunto de disponibilidade, selecionar **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="6e078-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![A janela Recursos Associados][CR07]

1. <span data-ttu-id="6e078-148">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="6e078-148">Click **Finish**.</span></span>  

   <span data-ttu-id="6e078-149">Sua nova máquina virtual aparece na janela de ferramentas do Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e078-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Nova máquina virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6e078-151">Reiniciar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e078-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="6e078-152">Para reiniciar uma máquina virtual usando o Azure Explorer no Eclipse, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6e078-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="6e078-153">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="6e078-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![O comando Reiniciar da máquina virtual][RE01]

1. <span data-ttu-id="6e078-155">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6e078-155">In the confirmation window, click **Yes**.</span></span>

   ![A janela de confirmação da reinicialização é aberta][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6e078-157">Desligar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e078-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="6e078-158">Para desligar uma máquina virtual em execução usando o Azure Explorer no Eclipse, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6e078-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="6e078-159">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="6e078-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![O comando Desligar da máquina virtual][SH01]

1. <span data-ttu-id="6e078-161">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6e078-161">In the confirmation window, click **Yes**.</span></span>

   ![A janela de confirmação de desligamento da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6e078-163">Excluir uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e078-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="6e078-164">Para excluir uma máquina virtual usando o Azure Explorer no Eclipse, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6e078-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="6e078-165">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="6e078-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![O comando Excluir da máquina virtual][DE01]

1. <span data-ttu-id="6e078-167">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6e078-167">In the confirmation window, click **Yes**.</span></span>

   ![A janela de confirmação de exclusão da máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="6e078-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e078-169">Next steps</span></span>

<span data-ttu-id="6e078-170">Para saber mais sobre os tamanhos e preços das máquinas virtuais do Azure, veja os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e078-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="6e078-171">Tamanhos de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="6e078-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="6e078-172">[Tamanhos das máquinas virtuais do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="6e078-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="6e078-173">[Tamanhos das máquinas virtuais do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="6e078-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="6e078-174">Preços de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="6e078-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="6e078-175">[Preços de máquinas virtuais do Windows]</span><span class="sxs-lookup"><span data-stu-id="6e078-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="6e078-176">[Preços de máquinas virtuais do Linux]</span><span class="sxs-lookup"><span data-stu-id="6e078-176">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquinas virtuais do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquinas virtuais do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
