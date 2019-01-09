---
title: Gerenciar máquinas virtuais usando o Azure Explorer para Eclipse
description: Saiba como gerenciar suas máquinas virtuais do Azure usando o Azure Explorer para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 7f3b4a6adb4234bbf11f0f7cddafbe99fa0ff3df
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636692"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Gerenciar máquinas virtuais usando o Azure Explorer para Eclipse

O Azure Explorer, que faz parte do Kit de ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java uma solução fácil de usar para gerenciar máquinas virtuais em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Criar uma máquina virtual no Eclipse

Para criar uma máquina virtual usando o Azure Explorer, faça o seguinte:

1. Entre em sua conta do Azure usando as [Instruções de conexão para o Kit de ferramentas do Azure para Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).

2. Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Máquinas Virtuais** e, em seguida, clique em **Criar VM**.

   ![Comando Criar VM][CR01]  

   O assistente para **Criar uma nova Máquina Virtual** é aberto.

3. Na caixa de diálogo **Escolha uma Assinatura**, selecione sua assinatura e clique em **Avançar**.

   ![A janela Escolha uma Assinatura][CR02]

4. Na janela **Selecionar uma Imagem de Máquina Virtual**, insira as seguintes informações:

   * **Localização**: especifica a localização onde sua máquina virtual será criada (por exemplo, *oeste dos EUA*).

   * **Editor**: especifica o editor que criou a imagem que você usará para criar sua máquina virtual (por exemplo, *Microsoft*).

   * **Oferta**: especifica qual oferta de máquina virtual do editor selecionado será usada (por exemplo *JDK*).

   * **Sku**: especifica qual SKU (unidade de manutenção de estoque) da oferta selecionada será usada (por exemplo, *JDK_8*).

   * **No. da versão**: especifica qual versão do SKU selecionado será usada.

   ![A janela Selecionar uma Imagem de Máquina Virtual][CR03]

5. Clique em **Próximo**.

6. Na janela **Configurações Básicas de Máquina Virtual**, insira as seguintes informações:

   * **Nome da máquina virtual**: especifica o nome para sua nova máquina virtual que deve começar com uma letra e conter somente letras, números e hifens.

   * **Tamanho**: especifica o número de núcleos e a memória para alocar para sua máquina virtual.

   * **Nome de usuário**: especifica a conta de administrador a ser criada para gerenciar sua máquina virtual.

   * **Senha** e **Confirmar**: especifica a senha para sua conta de administrador.

   ![A janela Configurações Básicas de Máquina Virtual][CR04]

7. Clique em **Próximo**.

8. Na janela **Criar Nova Conta de Armazenamento**, insira as seguintes informações:

   * **Grupo de Recursos**: especifica o grupo de recursos para sua máquina virtual. Selecione uma das seguintes opções:
     * **Criar novo**: especifica que você deseja criar um novo grupo de recursos.
     * **Usar existente**: especifica que você deseja escolher um grupo de recursos que já está associado à sua conta do Azure.

       ![A caixa de diálogo Criar Nova Conta de Armazenamento][CR05]

   * **Conta de armazenamento**: especifica a conta de armazenamento que será usada para armazenar a máquina virtual. Você pode usar uma conta de armazenamento existente ou criar uma nova.

   * **Rede virtual** e **Subrede**: especifica a rede virtual e a sub-rede às quais sua máquina virtual se conectará. Use uma rede e sub-rede existentes ou crie uma nova rede e sub-rede. Se você selecionar **Criar nova**, a caixa de diálogo a seguir será exibida:

      ![A caixa de diálogo Criar Nova Rede Virtual][CR06]

9. Na janela **Recursos Associados**, insira as informações a seguir:

   * **Endereço IP público**: especifica um endereço IP externo para sua máquina virtual. Você pode optar por criar um novo endereço IP ou, se sua máquina virtual não tiver um endereço IP público, selecione **(Nenhum)**.

   * **Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual. Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**.

   * **Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer. Você pode selecionar um conjunto de disponibilidade existente, criar um novo conjunto de disponibilidade ou, se sua máquina virtual não for pertencer a um conjunto de disponibilidade, selecionar **(Nenhum)**.

   ![A janela Recursos Associados][CR07]

10. Clique em **Concluir**.  

    Sua nova máquina virtual aparece na janela de ferramentas do Azure Explorer.

    ![Nova máquina virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Reiniciar uma máquina virtual no Eclipse

Para reiniciar uma máquina virtual usando o Azure Explorer no Eclipse, faça o seguinte:

1. Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Reiniciar**.

   ![O comando Reiniciar da máquina virtual][RE01]

1. Na janela de confirmação, clique em **Sim**.

   ![A janela de confirmação da reinicialização é aberta][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Desligar uma máquina virtual no Eclipse

Para desligar uma máquina virtual em execução usando o Azure Explorer no Eclipse, faça o seguinte:

1. Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Desligar**.

   ![O comando Desligar da máquina virtual][SH01]

1. Na janela de confirmação, clique em **Sim**.

   ![A janela de confirmação de desligamento da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Excluir uma máquina virtual no Eclipse

Para excluir uma máquina virtual usando o Azure Explorer no Eclipse, faça o seguinte:

1. Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Excluir**.

   ![O comando Excluir da máquina virtual][DE01]

1. Na janela de confirmação, clique em **Sim**.

   ![A janela de confirmação de exclusão da máquina virtual][DE02]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os tamanhos e preços das máquinas virtuais do Azure, veja os recursos a seguir:

* Tamanhos de máquinas virtuais do Azure
  * [Tamanhos das máquinas virtuais do Windows no Azure]
  * [Tamanhos das máquinas virtuais do Linux no Azure]
* Preços de máquinas virtuais do Azure
  * [Preços de máquinas virtuais do Windows]
  * [Preços de máquinas virtuais do Linux]

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquinas virtuais do Windows]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Preços de máquinas virtuais do Linux]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

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
