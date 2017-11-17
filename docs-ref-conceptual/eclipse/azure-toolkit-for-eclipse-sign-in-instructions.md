---
title: "Instruções de entrada para o Kit de Ferramentas do Azure para Eclipse"
description: Saiba como se inscrever no Microsoft Azure usando o Kit de ferramentas do Azure para Eclipse.
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
ms.openlocfilehash: 6c10d3e11dd75679fca0736e02d15de1d782dcec
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="eae22-103">Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="eae22-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="eae22-104">O Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="eae22-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="eae22-105">**Automatizado** – quando você estiver usando esse método, você criará um arquivo de credenciais que conterá os dados da entidade de serviço, após o qual você poderá usar o arquivo de credenciais para entrar automaticamente em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae22-105">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>
  * <span data-ttu-id="eae22-106">**Interativo** – quando você estiver usando esse método, você inserirá suas credenciais do Azure sempre que entrar na conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae22-106">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>

<span data-ttu-id="eae22-107">As etapas nas seções a seguir descreverão como usar cada método.</span><span class="sxs-lookup"><span data-stu-id="eae22-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="eae22-108">Entrar automaticamente em sua conta do Azure e criar um arquivo de credenciais para usar no futuro</span><span class="sxs-lookup"><span data-stu-id="eae22-108">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="eae22-109">As etapas a seguir lhe orientarão na criação de um arquivo de credenciais que contém os dados da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="eae22-109">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="eae22-110">Depois de concluir essas etapas, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure toda vez que você abrir o projeto.</span><span class="sxs-lookup"><span data-stu-id="eae22-110">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="eae22-111">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eae22-111">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="eae22-112">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-112">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][A01]

1. <span data-ttu-id="eae22-114">Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Automatizado** e, em seguida, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="eae22-114">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Caixa de diálogo Entrar][A02]

1. <span data-ttu-id="eae22-116">Quando a caixa de diálogo **Logon no Azure** for exibida, digite as credenciais do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-116">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][A03]

1. <span data-ttu-id="eae22-118">Quando a caixa de diálogo **Criar Arquivos de Autenticação** for exibida, selecione as assinaturas que deseja usar, escolha o diretório de destino e, em seguida, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-118">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Caixa de diálogo Logon no Azure][A04]

1. <span data-ttu-id="eae22-120">A caixa de diálogo **Status de Criação da Entidade de Serviço** será exibida e, depois que os arquivos tiverem sido criados com êxito, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eae22-120">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. <span data-ttu-id="eae22-122">Quando a caixa de diálogo **Entrar no Azure** for exibida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-122">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][A06]

1. <span data-ttu-id="eae22-124">Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eae22-124">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="eae22-126">Sair de sua conta do Azure quando você entrou automaticamente</span><span class="sxs-lookup"><span data-stu-id="eae22-126">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="eae22-127">Depois de configurar as etapas na seção anterior, o Kit de ferramentas do Azure realizará sua entrada automaticamente em sua conta do Azure toda vez que você reiniciar o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eae22-127">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="eae22-128">No entanto, para sair de sua conta do Azure e impedir que o Kit de ferramentas do Azure promova sua entrada automaticamente, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="eae22-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="eae22-129">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="eae22-129">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

1. <span data-ttu-id="eae22-131">Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="eae22-131">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="eae22-133">Entre automaticamente em sua conta do Azure usando um arquivo de credenciais que você já criou</span><span class="sxs-lookup"><span data-stu-id="eae22-133">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="eae22-134">Se você sair do Azure quando você estiver usando o Eclipse, você precisará reconfigurar o Kit de ferramentas do Azure para Eclipse para usar um arquivo de credenciais criado antes que você possa entrar automaticamente em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae22-134">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="eae22-135">As etapas a seguir explicam como configurar o Kit de ferramentas do Azure para usar um arquivo de credenciais existente.</span><span class="sxs-lookup"><span data-stu-id="eae22-135">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="eae22-136">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eae22-136">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="eae22-137">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-137">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][A01]

1. <span data-ttu-id="eae22-139">Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Automatizado** e, em seguida, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-139">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Caixa de diálogo Entrar][A02]

1. <span data-ttu-id="eae22-141">Quando a caixa de diálogo **Selecionar Arquivo Autenticado** for exibida, selecione um arquivo de credenciais que você criou anteriormente e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-141">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Caixa de diálogo Entrar][A08]

1. <span data-ttu-id="eae22-143">Quando a caixa de diálogo **Entrar no Azure** for exibida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-143">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][A06]

1. <span data-ttu-id="eae22-145">Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eae22-145">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="eae22-147">Entrar em sua conta do Azure interativamente</span><span class="sxs-lookup"><span data-stu-id="eae22-147">Signing into your Azure account interactively</span></span>

<span data-ttu-id="eae22-148">As etapas a seguir ilustrarão como se inscrever no Azure inserindo manualmente suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae22-148">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="eae22-149">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eae22-149">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="eae22-150">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-150">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][I01]

1. <span data-ttu-id="eae22-152">Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Interativo** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-152">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Entrar][I02]

1. <span data-ttu-id="eae22-154">Quando a caixa de diálogo **Logon no Azure** for exibida, digite as credenciais do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="eae22-154">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][I03]

1. <span data-ttu-id="eae22-156">Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eae22-156">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="eae22-158">Sair de sua conta do Azure quando você entrou no modo interativo</span><span class="sxs-lookup"><span data-stu-id="eae22-158">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="eae22-159">Depois de configurar as etapas na seção anterior, você sairá automaticamente de sua conta do Azure toda vez que reiniciar o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eae22-159">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="eae22-160">No entanto, se você quiser sair de sua conta do Azure sem reiniciar o Eclipse, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="eae22-160">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="eae22-161">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="eae22-161">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

1. <span data-ttu-id="eae22-163">Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="eae22-163">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="next-steps"></a><span data-ttu-id="eae22-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eae22-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
