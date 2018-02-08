---
title: "Gerenciar máquinas virtuais usando o Azure Explorer para IntelliJ"
description: "Saiba como gerenciar suas máquinas virtuais do Azure usando o Azure Explorer para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 213efa7fc31705b0ffcba6f2fe40e7186a365fae
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="c76ac-103">Gerenciar máquinas virtuais usando o Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c76ac-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="c76ac-104">O Azure Explorer, que faz parte do Kit de ferramentas do Azure para IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar máquinas virtuais em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c76ac-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="c76ac-105">Criar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c76ac-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c76ac-106">Para criar uma máquina virtual usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c76ac-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="c76ac-107">Entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="c76ac-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="c76ac-108">Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Máquinas Virtuais** e, em seguida, clique em **Criar VM**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="c76ac-109">![O comando Criar VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="c76ac-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="c76ac-110">O assistente para **Criar uma nova Máquina Virtual** é aberto.</span><span class="sxs-lookup"><span data-stu-id="c76ac-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c76ac-111">Na caixa de diálogo **Escolha uma Assinatura**, selecione sua assinatura e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![A janela Escolha uma Assinatura][CR02]

4. <span data-ttu-id="c76ac-113">Na janela **Selecionar uma Imagem de Máquina Virtual**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c76ac-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="c76ac-114">**Localização**: especifica o local onde sua máquina virtual será criada (por exemplo, *Oeste dos EUA*).</span><span class="sxs-lookup"><span data-stu-id="c76ac-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="c76ac-115">**Imagem recomendada**: especifica que você escolherá uma imagem de uma lista abreviada de imagens usadas com frequência.</span><span class="sxs-lookup"><span data-stu-id="c76ac-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="c76ac-116">**Imagem personalizada**: especifica que você escolherá uma imagem personalizada fornecendo as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c76ac-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="c76ac-117">**Editor**: especifica o editor que criou a imagem que você usará para sua máquina virtual (por exemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c76ac-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="c76ac-118">**Oferta**: especifica qual oferta de máquina virtual do editor selecionado será usada (por exemplo *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c76ac-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="c76ac-119">**Sku**: especifica qual SKU (unidade de manutenção de estoque) da oferta selecionada será usada (por exemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c76ac-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="c76ac-120">**No. de Versão**: especifica qual versão do SKU selecionado será usada.</span><span class="sxs-lookup"><span data-stu-id="c76ac-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![A janela Selecionar uma Imagem de Máquina Virtual][CR03]

5. <span data-ttu-id="c76ac-122">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-122">Click **Next**.</span></span> 

6. <span data-ttu-id="c76ac-123">Na janela **Configurações Básicas de Máquina Virtual**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c76ac-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="c76ac-124">**Nome da máquina virtual**: especifica o nome para sua nova máquina virtual, que deve começar com uma letra e conter somente letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="c76ac-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c76ac-125">**Tamanho**: especifica o número de núcleos e a memória para alocar para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c76ac-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="c76ac-126">**Nome de usuário**: especifica a conta de administrador a criar para gerenciar sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c76ac-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="c76ac-127">**Senha** e **Confirmar**: especifica a senha para sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="c76ac-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![A janela Configurações Básicas de Máquina Virtual][CR04]

7. <span data-ttu-id="c76ac-129">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-129">Click **Next**.</span></span> 

8. <span data-ttu-id="c76ac-130">Na janela **Recursos Associados**, insira as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c76ac-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="c76ac-131">**Grupo de recursos**: especifica o grupo de recursos para suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c76ac-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="c76ac-132">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="c76ac-132">Select one of the following options:</span></span>
      * <span data-ttu-id="c76ac-133">**Criar novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c76ac-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="c76ac-134">**Usar existente**: especifica que você quer selecionar em uma lista de grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c76ac-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![A janela Recursos Associados][CR07]

   * <span data-ttu-id="c76ac-136">**Conta de armazenamento**: especifica a conta de armazenamento que será usada para armazenar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c76ac-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="c76ac-137">Escolha uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="c76ac-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="c76ac-138">Se você escolher **Criar Nova**, a caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="c76ac-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![A caixa de diálogo Criar Conta de Armazenamento][CR05]

   * <span data-ttu-id="c76ac-140">**Rede Virtual** e **Sub-rede**: especifica a rede virtual e a sub-rede as quais sua máquina virtual se conectará.</span><span class="sxs-lookup"><span data-stu-id="c76ac-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c76ac-141">Use uma rede e sub-rede existentes, ou crie uma nova rede e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c76ac-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c76ac-142">Se você selecionar **Criar novo**, a caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="c76ac-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![A caixa de diálogo Criar Rede Virtual][CR06]

   * <span data-ttu-id="c76ac-144">**Endereço IP público**: especifica um endereço IP externo para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c76ac-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c76ac-145">Você pode optar por criar um novo endereço IP ou, se sua máquina virtual não tiver um endereço IP público, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c76ac-146">**Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c76ac-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c76ac-147">Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c76ac-148">**Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer.</span><span class="sxs-lookup"><span data-stu-id="c76ac-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c76ac-149">Selecione um conjunto de disponibilidade existente, crie um novo conjunto de disponibilidade ou, se sua máquina virtual não for pertencer a um conjunto de disponibilidade, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="c76ac-150">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-150">Click **Finish**.</span></span>  
    <span data-ttu-id="c76ac-151">Sua nova máquina virtual aparece na janela de ferramentas do Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="c76ac-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Nova máquina virtual na exibição do Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="c76ac-153">Reiniciar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c76ac-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c76ac-154">Para reiniciar uma máquina virtual usando o Azure Explorer no IntelliJ, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c76ac-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="c76ac-155">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![O comando Reiniciar da máquina virtual][RE01]

2. <span data-ttu-id="c76ac-157">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-157">In the confirmation window, click **Yes**.</span></span> 

   ![A janela de confirmação de reinicialização da máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="c76ac-159">Desligar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c76ac-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c76ac-160">Para desligar uma máquina virtual em execução usando o Azure Explorer no IntelliJ, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c76ac-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="c76ac-161">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![O comando Desligar da máquina virtual][SH01]

2. <span data-ttu-id="c76ac-163">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-163">In the confirmation window, click **Yes**.</span></span> 

   ![A janela de confirmação de desligamento da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="c76ac-165">Excluir uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c76ac-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c76ac-166">Para excluir uma máquina virtual usando o Azure Explorer no IntelliJ, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c76ac-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="c76ac-167">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![O comando Excluir da máquina virtual][DE01]

2. <span data-ttu-id="c76ac-169">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c76ac-169">In the confirmation window, click **Yes**.</span></span> 

   ![A janela de confirmação de exclusão da máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="c76ac-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c76ac-171">Next steps</span></span>

<span data-ttu-id="c76ac-172">Para saber mais sobre os tamanhos e preços das máquinas virtuais do Azure, veja os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c76ac-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="c76ac-173">Tamanhos de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c76ac-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c76ac-174">[Tamanhos das máquinas virtuais do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="c76ac-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c76ac-175">[Tamanhos das máquinas virtuais do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="c76ac-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c76ac-176">Preços de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c76ac-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c76ac-177">[Preços de máquinas virtuais do Windows]</span><span class="sxs-lookup"><span data-stu-id="c76ac-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c76ac-178">[Preços de máquinas virtuais do Linux]</span><span class="sxs-lookup"><span data-stu-id="c76ac-178">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquinas virtuais do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquinas virtuais do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
