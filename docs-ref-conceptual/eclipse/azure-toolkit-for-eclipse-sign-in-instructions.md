---
title: Instruções de entrada para o Kit de Ferramentas do Azure para Eclipse
description: Saiba como se inscrever no Microsoft Azure usando o Kit de ferramentas do Azure para Eclipse.
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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575313"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="f4589-103">Instruções de entrada para o Kit de Ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="f4589-103">Sign-in instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="f4589-104">O Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="f4589-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  - [<span data-ttu-id="f4589-105">Entre em sua conta do Azure com o Logon no Dispositivo</span><span class="sxs-lookup"><span data-stu-id="f4589-105">Sign in to your Azure account by Device Login</span></span>](#sign-in-to-your-azure-account-by-device-login)
  - [<span data-ttu-id="f4589-106">Entre em sua conta do Azure com a Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="f4589-106">Sign in to your Azure account by Service Principal</span></span>](#sign-in-to-your-azure-account-by-service-principal)

<span data-ttu-id="f4589-107">[Também são fornecidos métodos para **Sair**](#sign-out-of-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="f4589-107">[**Sign out**](#sign-out-of-your-azure-account) methods are also provided.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a><span data-ttu-id="f4589-108">Entre em sua conta do Azure com o Logon no Dispositivo</span><span class="sxs-lookup"><span data-stu-id="f4589-108">Sign in to your Azure account by Device Login</span></span>

<span data-ttu-id="f4589-109">Para entrar no Azure por logon no dispositivo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f4589-109">To sign in Azure by device login, do the following:</span></span>

1. <span data-ttu-id="f4589-110">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f4589-110">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="f4589-111">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="f4589-112">![Menu do Eclipse para Entrada no Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="f4589-112">![Eclipse Menu for Azure Sign In][I01]</span></span>

3. <span data-ttu-id="f4589-113">Na caixa de diálogo **Entrar no Azure**, selecione **Logon no Dispositivo** e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-113">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in**.</span></span>

   ![A janela Entrar no Azure com o logon no dispositivo selecionado][I02]

4. <span data-ttu-id="f4589-115">Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f4589-115">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![A janela da caixa de diálogo Logon no Azure][I03]

> [!NOTE]
>
> <span data-ttu-id="f4589-117">Se o navegador não abrir, configure o Eclipse para usar um navegador externo, como o Internet Explorer, o Firefox ou o Chrome:</span><span class="sxs-lookup"><span data-stu-id="f4589-117">If the browser doesn't open, configure Eclipse to use an external browser like Internet Explorer, Firefox, or Chrome:</span></span>
>
> 1. <span data-ttu-id="f4589-118">Abra Preferências -> Geral -> Navegador da Web -> Usar navegador da Web externo no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f4589-118">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="f4589-119">Selecione o navegador que você prefere usar</span><span class="sxs-lookup"><span data-stu-id="f4589-119">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="f4589-120">No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-120">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![O navegador de logon do dispositivo][I04]

6. <span data-ttu-id="f4589-122">Por fim, na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4589-122">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a><span data-ttu-id="f4589-124">Entre em sua conta do Azure com a Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="f4589-124">Sign in to your Azure account by Service Principal</span></span>

<span data-ttu-id="f4589-125">Esta seção fornece uma orientarão pela criação de um arquivo de credenciais contendo os dados de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="f4589-125">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="f4589-126">Após a conclusão desse processo, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure quando você abrir o projeto.</span><span class="sxs-lookup"><span data-stu-id="f4589-126">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure when open your project.</span></span>

1. <span data-ttu-id="f4589-127">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f4589-127">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="f4589-128">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-128">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="f4589-129">![O comando de Entrada do Azure para Eclipse][A01]</span><span class="sxs-lookup"><span data-stu-id="f4589-129">![The Eclipse Azure Sign In command][A01]</span></span>

3. <span data-ttu-id="f4589-130">Na janela **Entrar no Azure**, selecione **Entidade de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="f4589-130">In the **Azure Sign In** window, select **Service Principal**.</span></span> <span data-ttu-id="f4589-131">Se você ainda não tiver o arquivo de autenticação de entidade de serviço, clique em **Novo** para criá-lo.</span><span class="sxs-lookup"><span data-stu-id="f4589-131">If you do not have the service principal authentication file yet, click **New** to create one.</span></span> <span data-ttu-id="f4589-132">Caso contrário, você pode clicar em **Procurar** abri-lo e ir para a etapa 8.</span><span class="sxs-lookup"><span data-stu-id="f4589-132">Otherwise you can click **Browse** to open it and jump to step 8.</span></span>

   ![A janela Entrada do Azure com a entidade de serviço selecionada][A02]

4. <span data-ttu-id="f4589-134">Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f4589-134">Click **Copy&Open** in **Azure Device Login** dialog.</span></span>

   ![A janela da caixa de diálogo Logon no Azure][A08]

> [!NOTE]
>
> <span data-ttu-id="f4589-136">Se o navegador não abrir, configure o Eclipse para usar um navegador externo, como o IE ou o Chrome:</span><span class="sxs-lookup"><span data-stu-id="f4589-136">If the browser doesn't open, configure eclipse to use an external browser like IE or Chrome:</span></span>
>
> 1. <span data-ttu-id="f4589-137">Abra Preferências -> Geral -> Navegador da Web -> Usar navegador da Web externo no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f4589-137">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="f4589-138">Selecione o navegador que você prefere usar</span><span class="sxs-lookup"><span data-stu-id="f4589-138">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="f4589-139">No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-139">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![O navegador de logon do dispositivo][A03]

6. <span data-ttu-id="f4589-141">Na janela **Criar Arquivos de Autenticação**, selecione as assinaturas que quer usar, escolha o diretório de destino e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-141">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![A janela Criar Arquivos de Autenticação][A04]

7. <span data-ttu-id="f4589-143">Na caixa de diálogo **Status de Criação da Entidade de Serviço**, clique em **OK** após a criação bem-sucedida dos arquivos.</span><span class="sxs-lookup"><span data-stu-id="f4589-143">In the **Service Principal Creation Status** dialog box, click **OK** after your files have been created successfully.</span></span>

   ![A caixa de diálogo Status de Criação da Entidade de Serviço][A05]

8. <span data-ttu-id="f4589-145">O endereço do arquivo criado será automaticamente preenchido na janela **Entrar no Azure**, agora clique **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f4589-145">Address of the created file will be automatically filled in the **Azure Sign In** window, now click **Sign in**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A06]

9. <span data-ttu-id="f4589-147">Por fim, na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4589-147">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][A07]

## <a name="sign-out-of-your-azure-account"></a><span data-ttu-id="f4589-149">Sair de sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="f4589-149">Sign out of your Azure account</span></span>

<span data-ttu-id="f4589-150">Depois que você configurou sua conta seguindo as etapas anteriores, será conectado automaticamente sempre que iniciar o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f4589-150">After you have configured your account by preceding steps, you will be automatically signed in each time you start Eclipse.</span></span> <span data-ttu-id="f4589-151">No entanto, se desejar sair de sua conta do Azure, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4589-151">However, if you want to sign out of your Azure account, use the following steps.</span></span>

1. <span data-ttu-id="f4589-152">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="f4589-152">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

2. <span data-ttu-id="f4589-154">Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f4589-154">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="next-steps"></a><span data-ttu-id="f4589-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4589-156">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
