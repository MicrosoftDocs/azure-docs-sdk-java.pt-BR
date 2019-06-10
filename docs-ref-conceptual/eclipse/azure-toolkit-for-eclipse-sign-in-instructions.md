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
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Instruções de entrada para o Kit de Ferramentas do Azure para Eclipse

O Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:

  - [Entre em sua conta do Azure com o Logon no Dispositivo](#sign-in-to-your-azure-account-by-device-login)
  - [Entre em sua conta do Azure com a Entidade de Serviço](#sign-in-to-your-azure-account-by-service-principal)

[Também são fornecidos métodos para **Sair**](#sign-out-of-your-azure-account).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a>Entre em sua conta do Azure com o Logon no Dispositivo

Para entrar no Azure por logon no dispositivo, faça o seguinte:

1. Abra seu projeto com o Eclipse.

2. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.
   ![Menu do Eclipse para Entrada no Azure][I01]

3. Na caixa de diálogo **Entrar no Azure**, selecione **Logon no Dispositivo** e clique em **Entrar**.

   ![A janela Entrar no Azure com o logon no dispositivo selecionado][I02]

4. Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.

   ![A janela da caixa de diálogo Logon no Azure][I03]

> [!NOTE]
>
> Se o navegador não abrir, configure o Eclipse para usar um navegador externo, como o Internet Explorer, o Firefox ou o Chrome:
>
> 1. Abra Preferências -> Geral -> Navegador da Web -> Usar navegador da Web externo no Eclipse
>
> 2. Selecione o navegador que você prefere usar
>

5. No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.

   ![O navegador de logon do dispositivo][I04]

6. Por fim, na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e clique em **OK**.

   ![A caixa de diálogo Selecionar Assinaturas][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a>Entre em sua conta do Azure com a Entidade de Serviço

Esta seção fornece uma orientarão pela criação de um arquivo de credenciais contendo os dados de sua entidade de serviço. Após a conclusão desse processo, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure quando você abrir o projeto.

1. Abra seu projeto com o Eclipse.

2. Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.
   ![O comando de Entrada do Azure para Eclipse][A01]

3. Na janela **Entrar no Azure**, selecione **Entidade de Serviço**. Se você ainda não tiver o arquivo de autenticação de entidade de serviço, clique em **Novo** para criá-lo. Caso contrário, você pode clicar em **Procurar** abri-lo e ir para a etapa 8.

   ![A janela Entrada do Azure com a entidade de serviço selecionada][A02]

4. Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.

   ![A janela da caixa de diálogo Logon no Azure][A08]

> [!NOTE]
>
> Se o navegador não abrir, configure o Eclipse para usar um navegador externo, como o IE ou o Chrome:
>
> 1. Abra Preferências -> Geral -> Navegador da Web -> Usar navegador da Web externo no Eclipse
>
> 2. Selecione o navegador que você prefere usar
>

5. No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.

   ![O navegador de logon do dispositivo][A03]

6. Na janela **Criar Arquivos de Autenticação**, selecione as assinaturas que quer usar, escolha o diretório de destino e clique em **Iniciar**.

   ![A janela Criar Arquivos de Autenticação][A04]

7. Na caixa de diálogo **Status de Criação da Entidade de Serviço**, clique em **OK** após a criação bem-sucedida dos arquivos.

   ![A caixa de diálogo Status de Criação da Entidade de Serviço][A05]

8. O endereço do arquivo criado será automaticamente preenchido na janela **Entrar no Azure**, agora clique **Entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

9. Por fim, na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e clique em **OK**.

   ![A caixa de diálogo Selecionar Assinaturas][A07]

## <a name="sign-out-of-your-azure-account"></a>Sair de sua conta do Azure

Depois que você configurou sua conta seguindo as etapas anteriores, será conectado automaticamente sempre que iniciar o Eclipse. No entanto, se desejar sair de sua conta do Azure, use as etapas a seguir.

1. No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.

   ![Menu do Eclipse para saída do Azure][L01]

2. Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="next-steps"></a>Próximas etapas

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
