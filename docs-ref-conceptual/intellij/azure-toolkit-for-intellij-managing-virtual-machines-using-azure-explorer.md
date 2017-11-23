---
title: "Gerenciar máquinas virtuais usando o Azure Explorer para IntelliJ"
description: "Saiba como gerenciar suas máquinas virtuais do Azure usando o Azure Explorer para IntelliJ."
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: d0fe2a90fd12d2badf277659c7ce4ee768f6943c
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a>Gerenciar máquinas virtuais usando o Azure Explorer para IntelliJ

O Azure Explorer, que faz parte do Kit de ferramentas do Azure para IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar máquinas virtuais em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Criar uma máquina virtual no IntelliJ

Para criar uma máquina virtual usando o Azure Explorer, faça o seguinte: 

1. Entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ].

2. Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Máquinas Virtuais** e, em seguida, clique em **Criar VM**. 

   ![O comando Criar VM][CR01]  
    O assistente para **Criar uma nova Máquina Virtual** é aberto.

3. Na caixa de diálogo **Escolha uma Assinatura**, selecione sua assinatura e clique em **Avançar**. 

   ![A janela Escolha uma Assinatura][CR02]

4. Na janela **Selecionar uma Imagem de Máquina Virtual**, insira as seguintes informações:

   * **Localização**: especifica o local onde sua máquina virtual será criada (por exemplo, *Oeste dos EUA*). 

   * **Imagem recomendada**: especifica que você escolherá uma imagem de uma lista abreviada de imagens usadas com frequência.

   * **Imagem personalizada**: especifica que você escolherá uma imagem personalizada fornecendo as seguintes informações:

      * **Editor**: especifica o editor que criou a imagem que você usará para sua máquina virtual (por exemplo, *Microsoft*).

      * **Oferta**: especifica qual oferta de máquina virtual do editor selecionado será usada (por exemplo *JDK*).

      * **Sku**: especifica qual SKU (unidade de manutenção de estoque) da oferta selecionada será usada (por exemplo, *JDK_8*).

      * **No. de Versão**: especifica qual versão do SKU selecionado será usada.

   ![A janela Selecionar uma Imagem de Máquina Virtual][CR03]

5. Clique em **Avançar**. 

6. Na janela **Configurações Básicas de Máquina Virtual**, insira as seguintes informações:

   * **Nome da máquina virtual**: especifica o nome para sua nova máquina virtual, que deve começar com uma letra e conter somente letras, números e hifens.

   * **Tamanho**: especifica o número de núcleos e a memória para alocar para sua máquina virtual.

   * **Nome de usuário**: especifica a conta de administrador a criar para gerenciar sua máquina virtual.

   * **Senha** e **Confirmar**: especifica a senha para sua conta de administrador.

   ![A janela Configurações Básicas de Máquina Virtual][CR04]

7. Clique em **Avançar**. 

8. Na janela **Recursos Associados**, insira as informações a seguir:

   * **Grupo de recursos**: especifica o grupo de recursos para suas máquinas virtuais. Selecione uma das seguintes opções:
      * **Criar novo**: especifica que você deseja criar um novo grupo de recursos.
      * **Usar existente**: especifica que você quer selecionar em uma lista de grupos de recursos associados à sua conta do Azure.

       ![A janela Recursos Associados][CR07]

   * **Conta de armazenamento**: especifica a conta de armazenamento que será usada para armazenar a máquina virtual. Escolha uma conta de armazenamento existente ou crie uma nova. Se você escolher **Criar Nova**, a caixa de diálogo a seguir será exibida:

      ![A caixa de diálogo Criar Conta de Armazenamento][CR05]

   * **Rede Virtual** e **Sub-rede**: especifica a rede virtual e a sub-rede as quais sua máquina virtual se conectará. Use uma rede e sub-rede existentes, ou crie uma nova rede e sub-rede. Se você selecionar **Criar novo**, a caixa de diálogo a seguir será exibida:

      ![A caixa de diálogo Criar Rede Virtual][CR06]

   * **Endereço IP público**: especifica um endereço IP externo para sua máquina virtual. Você pode optar por criar um novo endereço IP ou, se sua máquina virtual não tiver um endereço IP público, selecione **(Nenhum)**. 

   * **Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual. Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**. 

   * **Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer. Selecione um conjunto de disponibilidade existente, crie um novo conjunto de disponibilidade ou, se sua máquina virtual não for pertencer a um conjunto de disponibilidade, selecione **(Nenhum)**.

9. Clique em **Concluir**.  
    Sua nova máquina virtual aparece na janela de ferramentas do Azure Explorer. 

   ![Nova máquina virtual na exibição do Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Reiniciar uma máquina virtual no IntelliJ

Para reiniciar uma máquina virtual usando o Azure Explorer no IntelliJ, faça o seguinte:

1. Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Reiniciar**.

   ![O comando Reiniciar da máquina virtual][RE01]

2. Na janela de confirmação, clique em **Sim**. 

   ![A janela de confirmação de reinicialização da máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Desligar uma máquina virtual no IntelliJ

Para desligar uma máquina virtual em execução usando o Azure Explorer no IntelliJ, faça o seguinte:

1. Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Desligar**.

   ![O comando Desligar da máquina virtual][SH01]

2. Na janela de confirmação, clique em **Sim**. 

   ![A janela de confirmação de desligamento da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Excluir uma máquina virtual no IntelliJ

Para excluir uma máquina virtual usando o Azure Explorer no IntelliJ, faça o seguinte:

1. Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Excluir**.

   ![O comando Excluir da máquina virtual][DE01]

2. Na janela de confirmação, clique em **Sim**. 

   ![A janela de confirmação de exclusão da máquina virtual][DE02]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os tamanhos e preços das máquinas virtuais do Azure, veja os recursos a seguir:

* Tamanhos de máquinas virtuais do Azure
  * [Tamanhos das máquinas virtuais do Windows no Azure]
  * [Tamanhos das máquinas virtuais do Linux no Azure]
* Preços de máquinas virtuais do Azure
  * [Preços de máquinas virtuais do Windows]
  * [Preços de máquinas virtuais do Linux]

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
