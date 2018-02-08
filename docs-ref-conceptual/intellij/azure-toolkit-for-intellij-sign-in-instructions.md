---
title: "Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ"
description: Saiba como se inscrever no Microsoft Azure usando o Kit de ferramentas do Azure para IntelliJ.
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
ms.openlocfilehash: 4e24dac285fa38bad4293f1cce2830242c2fe151
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ

O Kit de ferramentas do Azure para IntelliJ fornece dois métodos para entrar em sua conta do Azure:

  * **Automatizada**: crie um arquivo de credenciais que pode ser usado para entrar automaticamente em sua conta do Azure.
  * **Interativo**: insira suas credenciais do Azure sempre que você entrar em sua conta do Azure.

As seções a seguir descrevem como usar cada método.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a>Entrar em sua conta do Azure automaticamente

Esta seção fornece uma orientarão pela criação de um arquivo de credenciais contendo os dados de sua entidade de serviço. Após a conclusão desse processo, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure sempre que você abrir o projeto.

1. Abra seu projeto com o IntelliJ IDEA.

1. No menu **Ferramentas**, aponte para **Azure** e clique em **Entrar no Azure**.

   ![O comando de Entrada do IntelliJ Azure][A01]

1. Na janela **Entrar no Azure**, selecione **Automatizado** e clique em **Novo**.

   ![A janela Entrar no Azure com Automatizado selecionado][A02]

1. Na janela da **caixa de diálogo Logon no Azure**, insira suas credenciais do Azure e clique em **Entrar**.

   ![A janela da caixa de diálogo Logon no Azure][A03]

1. Na janela **Criar Arquivos de Autenticação**, selecione as assinaturas que quer usar, escolha o diretório de destino e clique em **Iniciar**.

   ![A janela Criar Arquivos de Autenticação][A04]

1. Na caixa de diálogo **Status de Criação da Entidade de Serviço**, após a criação dos arquivos, clique em **OK**.

   ![A caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. Na janela **Entrar no Azure**, clique em **Entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

1. Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![A caixa de diálogo Selecionar Assinaturas][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Sair de sua conta do Azure depois de entrar automaticamente

Depois de configurar sua conta usando as etapas anteriores, o Kit de ferramentas do Azure conectará automaticamente você à sua conta do Azure sempre que reiniciar o IntelliJ IDEA. No entanto, para sair de sua conta do Azure e impedir que o Kit de ferramentas do Azure promova sua entrada automaticamente, faça o seguinte:

1. No IntelliJ IDEA, no menu **Ferramentas**, aponte para **Azure** e clique em **Sair do Azure**.

   ![O comando de Saída do IntelliJ Azure][L01]

1. Na janela de confirmação **Sair do Azure**, clique em **Sim**.

   ![A janela de confirmação Sair do Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Entre em sua conta do Azure automaticamente usando um arquivo de credenciais existente

Se você sair de sua conta do Azure enquanto usa o IntelliJ IDEA, será necessário usar um arquivo de credenciais existente para entrar automaticamente na conta novamente. Para configurar o Kit de ferramentas do Azure para Eclipse a fim de usar um arquivo de credenciais existente, faça o seguinte:

1. Abra seu projeto com o IntelliJ IDEA.

1. No menu **Ferramentas**, aponte para **Azure** e clique em **Entrar no Azure**.

   ![O comando de Entrada do IntelliJ Azure][A01]

1. Na janela **Entrar no Azure**, selecione **Automatizado** e clique em **Procurar**.

   ![A janela Entrar no Azure com Automatizado selecionado][A02]

1. Na caixa de diálogo **Selecionar Arquivo de Autenticação**, selecione um arquivo de credenciais criado anteriormente e clique em **Selecionar**.

   ![A caixa de diálogo Selecionar Arquivo de Autenticação][A08]

1. Na janela **Entrar no Azure**, clique em **Entrar**.

   ![A janela Entrar no Azure com Automatizado selecionado][A06]

1. Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![A caixa de diálogo Selecionar Assinaturas][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a>Entrar em sua conta do Azure interativamente

Para entrar no Azure inserindo manualmente suas credenciais do Azure, faça o seguinte:

1. Abra seu projeto com o IntelliJ IDEA.

1. Clique em **Ferramentas**, aponte para **Azure** e clique em **Entrar no Azure**.

   ![O comando de Entrada do IntelliJ Azure][I01]

1. Na caixa de diálogo **Entrar no Azure**, selecione **Interativo** e clique em **Entrar**.

   ![A janela Entrar no Azure com Interativo selecionado][I02]

1. Na caixa de diálogo **Logon no Azure**, insira suas credenciais do Azure e clique em **Entrar**.

   ![A janela da caixa de diálogo Logon no Azure][I03]

1. Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![A caixa de diálogo Selecionar Assinaturas][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Sair de sua conta do Azure depois de entrar interativamente

Depois de configurar sua conta usando as etapas anteriores, você sairá automaticamente de sua conta do Azure sempre que reiniciar o IntelliJ IDEA. No entanto, se você quiser sair de sua conta do Azure *sem* reiniciar o IntelliJ IDEA, faça o seguinte.

1. No IntelliJ IDEA, no menu **Ferramentas**, aponte para **Azure** e clique em **Sair do Azure**.

   ![O comando de Saída do IntelliJ Azure][L01]

1. Na janela de confirmação **Sair do Azure**, clique em **Sim**.

   ![A janela de confirmação Sair do Azure][L02]

## <a name="next-steps"></a>Próximas etapas

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
