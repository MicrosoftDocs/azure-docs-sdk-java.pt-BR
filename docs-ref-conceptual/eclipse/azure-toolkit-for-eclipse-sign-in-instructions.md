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
ms.openlocfilehash: eb6099ab0c19bf3588cb7fd668f070771e58fe74
ms.sourcegitcommit: 8230cf6b15ac51a9f8a209e9b76411a0385029aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2018
ms.locfileid: "34216020"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse

O Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:

  * **Automatizado** – quando você estiver usando esse método, você criará um arquivo de credenciais que conterá os dados da entidade de serviço, após o qual você poderá usar o arquivo de credenciais para entrar automaticamente em sua conta do Azure.
  * **Interativo** – quando você estiver usando esse método, você inserirá suas credenciais do Azure sempre que entrar na conta do Azure.

As etapas nas seções a seguir descreverão como usar cada método.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Entrar automaticamente em sua conta do Azure e criar um arquivo de credenciais para usar no futuro

As etapas a seguir lhe orientarão na criação de um arquivo de credenciais que contém os dados da entidade de serviço. Depois de concluir essas etapas, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure toda vez que você abrir o projeto.

1. Abra seu projeto com o Eclipse.

1. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.

   ![Menu do Eclipse para Entrar no Azure][A01]

1. Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Automatizado** e, em seguida, clique em **Novo**.

   ![Caixa de diálogo Entrar][A02]

1. Quando a caixa de diálogo **Logon no Azure** for exibida, digite as credenciais do Azure e, em seguida, clique em **Entrar**.

   ![Caixa de Diálogo de Logon do Azure][A03]

1. Quando a caixa de diálogo **Criar Arquivos de Autenticação** for exibida, selecione as assinaturas que deseja usar, escolha o diretório de destino e, em seguida, clique em **Iniciar**.

   ![Caixa de diálogo Logon no Azure][A04]

1. A caixa de diálogo **Status de Criação da Entidade de Serviço** será exibida e, depois que os arquivos tiverem sido criados com êxito, clique em **OK**.

   ![Caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. Quando a caixa de diálogo **Entrar no Azure** for exibida, clique em **Entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

1. Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Sair de sua conta do Azure quando você entrou automaticamente

Depois de configurar as etapas na seção anterior, o Kit de ferramentas do Azure realizará sua entrada automaticamente em sua conta do Azure toda vez que você reiniciar o Eclipse. No entanto, para sair de sua conta do Azure e impedir que o Kit de ferramentas do Azure promova sua entrada automaticamente, use as etapas a seguir.

1. No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.

   ![Menu do Eclipse para saída do Azure][L01]

1. Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.

   ![Caixa de diálogo Saída do Azure][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Entre automaticamente em sua conta do Azure usando um arquivo de credenciais que você já criou

Se você sair do Azure quando você estiver usando o Eclipse, você precisará reconfigurar o Kit de ferramentas do Azure para Eclipse para usar um arquivo de credenciais criado antes que você possa entrar automaticamente em sua conta do Azure. As etapas a seguir explicam como configurar o Kit de ferramentas do Azure para usar um arquivo de credenciais existente.

1. Abra seu projeto com o Eclipse.

1. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.

   ![Menu do Eclipse para Entrar no Azure][A01]

1. Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Automatizado** e, em seguida, clique em **Procurar**.

   ![Caixa de diálogo Entrar][A02]

1. Quando a caixa de diálogo **Selecionar Arquivo Autenticado** for exibida, selecione um arquivo de credenciais criado anteriormente e clique em **Abrir**.

   ![Caixa de diálogo Entrar][A08]

1. Quando a caixa de diálogo **Entrar no Azure** for exibida, clique em **Entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

1. Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-into-your-azure-account-interactively"></a>Entrar em sua conta do Azure interativamente

As etapas a seguir ilustrarão como se inscrever no Azure inserindo manualmente suas credenciais do Azure.

1. Abra seu projeto com o Eclipse.

1. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.

   ![Menu do Eclipse para Entrar no Azure][I01]

1. Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Interativo** e, em seguida, clique em **Entrar**.

   ![Caixa de diálogo Entrar][I02]

1. Quando a caixa de diálogo **Logon no Azure** for exibida, digite as credenciais do Azure e, em seguida, clique em **Entrar**.

   ![Caixa de Diálogo de Logon do Azure][I03]

1. Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![Caixa de diálogo Selecionar Assinaturas][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Sair de sua conta do Azure quando você entrou no modo interativo

Depois de configurar as etapas na seção anterior, você sairá automaticamente de sua conta do Azure toda vez que reiniciar o Eclipse. No entanto, se você quiser sair de sua conta do Azure sem reiniciar o Eclipse, use as etapas a seguir.

1. No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.

   ![Menu do Eclipse para saída do Azure][L01]

1. Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

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
