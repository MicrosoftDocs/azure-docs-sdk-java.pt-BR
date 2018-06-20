---
title: Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ
description: Saiba como se inscrever no Microsoft Azure usando o Kit de ferramentas do Azure para IntelliJ.
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
ms.openlocfilehash: 4e24dac285fa38bad4293f1cce2830242c2fe151
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954387"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="c70f8-103">Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c70f8-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="c70f8-104">O Kit de ferramentas do Azure para IntelliJ fornece dois métodos para entrar em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="c70f8-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="c70f8-105">**Automatizada**: crie um arquivo de credenciais que pode ser usado para entrar automaticamente em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c70f8-105">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>
  * <span data-ttu-id="c70f8-106">**Interativo**: insira suas credenciais do Azure sempre que você entrar em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c70f8-106">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>

<span data-ttu-id="c70f8-107">As seções a seguir descrevem como usar cada método.</span><span class="sxs-lookup"><span data-stu-id="c70f8-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="c70f8-108">Entrar em sua conta do Azure automaticamente</span><span class="sxs-lookup"><span data-stu-id="c70f8-108">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="c70f8-109">Esta seção fornece uma orientarão pela criação de um arquivo de credenciais contendo os dados de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="c70f8-109">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="c70f8-110">Após a conclusão desse processo, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure sempre que você abrir o projeto.</span><span class="sxs-lookup"><span data-stu-id="c70f8-110">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="c70f8-111">Abra seu projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c70f8-111">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="c70f8-112">No menu **Ferramentas**, aponte para **Azure** e clique em **Entrar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-112">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![O comando de Entrada do IntelliJ Azure][A01]

1. <span data-ttu-id="c70f8-114">Na janela **Entrar no Azure**, selecione **Automatizado** e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-114">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![A janela Entrar no Azure com Automatizado selecionado][A02]

1. <span data-ttu-id="c70f8-116">Na janela da **caixa de diálogo Logon no Azure**, insira suas credenciais do Azure e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-116">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![A janela da caixa de diálogo Logon no Azure][A03]

1. <span data-ttu-id="c70f8-118">Na janela **Criar Arquivos de Autenticação**, selecione as assinaturas que quer usar, escolha o diretório de destino e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-118">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![A janela Criar Arquivos de Autenticação][A04]

1. <span data-ttu-id="c70f8-120">Na caixa de diálogo **Status de Criação da Entidade de Serviço**, após a criação dos arquivos, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-120">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![A caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. <span data-ttu-id="c70f8-122">Na janela **Entrar no Azure**, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-122">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A06]

1. <span data-ttu-id="c70f8-124">Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-124">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="c70f8-126">Sair de sua conta do Azure depois de entrar automaticamente</span><span class="sxs-lookup"><span data-stu-id="c70f8-126">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="c70f8-127">Depois de configurar sua conta usando as etapas anteriores, o Kit de ferramentas do Azure conectará automaticamente você à sua conta do Azure sempre que reiniciar o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c70f8-127">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="c70f8-128">No entanto, para sair de sua conta do Azure e impedir que o Kit de ferramentas do Azure promova sua entrada automaticamente, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c70f8-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="c70f8-129">No IntelliJ IDEA, no menu **Ferramentas**, aponte para **Azure** e clique em **Sair do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-129">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![O comando de Saída do IntelliJ Azure][L01]

1. <span data-ttu-id="c70f8-131">Na janela de confirmação **Sair do Azure**, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-131">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![A janela de confirmação Sair do Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="c70f8-133">Entre em sua conta do Azure automaticamente usando um arquivo de credenciais existente</span><span class="sxs-lookup"><span data-stu-id="c70f8-133">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="c70f8-134">Se você sair de sua conta do Azure enquanto usa o IntelliJ IDEA, será necessário usar um arquivo de credenciais existente para entrar automaticamente na conta novamente.</span><span class="sxs-lookup"><span data-stu-id="c70f8-134">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="c70f8-135">Para configurar o Kit de ferramentas do Azure para Eclipse a fim de usar um arquivo de credenciais existente, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c70f8-135">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="c70f8-136">Abra seu projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c70f8-136">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="c70f8-137">No menu **Ferramentas**, aponte para **Azure** e clique em **Entrar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-137">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![O comando de Entrada do IntelliJ Azure][A01]

1. <span data-ttu-id="c70f8-139">Na janela **Entrar no Azure**, selecione **Automatizado** e clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-139">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![A janela Entrar no Azure com Automatizado selecionado][A02]

1. <span data-ttu-id="c70f8-141">Na caixa de diálogo **Selecionar Arquivo de Autenticação**, selecione um arquivo de credenciais criado anteriormente e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-141">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![A caixa de diálogo Selecionar Arquivo de Autenticação][A08]

1. <span data-ttu-id="c70f8-143">Na janela **Entrar no Azure**, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-143">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![A janela Entrar no Azure com Automatizado selecionado][A06]

1. <span data-ttu-id="c70f8-145">Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-145">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="c70f8-147">Entrar em sua conta do Azure interativamente</span><span class="sxs-lookup"><span data-stu-id="c70f8-147">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="c70f8-148">Para entrar no Azure inserindo manualmente suas credenciais do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c70f8-148">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="c70f8-149">Abra seu projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c70f8-149">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="c70f8-150">Clique em **Ferramentas**, aponte para **Azure** e clique em **Entrar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-150">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![O comando de Entrada do IntelliJ Azure][I01]

1. <span data-ttu-id="c70f8-152">Na caixa de diálogo **Entrar no Azure**, selecione **Interativo** e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-152">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![A janela Entrar no Azure com Interativo selecionado][I02]

1. <span data-ttu-id="c70f8-154">Na caixa de diálogo **Logon no Azure**, insira suas credenciais do Azure e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-154">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![A janela da caixa de diálogo Logon no Azure][I03]

1. <span data-ttu-id="c70f8-156">Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-156">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="c70f8-158">Sair de sua conta do Azure depois de entrar interativamente</span><span class="sxs-lookup"><span data-stu-id="c70f8-158">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="c70f8-159">Depois de configurar sua conta usando as etapas anteriores, você sairá automaticamente de sua conta do Azure sempre que reiniciar o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c70f8-159">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="c70f8-160">No entanto, se você quiser sair de sua conta do Azure *sem* reiniciar o IntelliJ IDEA, faça o seguinte.</span><span class="sxs-lookup"><span data-stu-id="c70f8-160">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="c70f8-161">No IntelliJ IDEA, no menu **Ferramentas**, aponte para **Azure** e clique em **Sair do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-161">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![O comando de Saída do IntelliJ Azure][L01]

1. <span data-ttu-id="c70f8-163">Na janela de confirmação **Sair do Azure**, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c70f8-163">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![A janela de confirmação Sair do Azure][L02]

## <a name="next-steps"></a><span data-ttu-id="c70f8-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c70f8-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
