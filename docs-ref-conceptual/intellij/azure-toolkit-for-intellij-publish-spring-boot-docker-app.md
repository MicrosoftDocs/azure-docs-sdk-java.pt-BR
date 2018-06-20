---
title: Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ
description: Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ.
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
ms.openlocfilehash: 4228352efa4354bfe4969c1a5ecd3f3b40483f85
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954727"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ

O [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores do Java a criar aplicativos de nível empresarial. Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.

O [Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos executados em contêineres.

Este tutorial explica as etapas para implantação de um aplicativo Spring Boot como um contêiner do Docker no Microsoft Azure usando o Kit de Ferramentas do Azure para IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Clonar o repositório padrão do Spring Boot Docker

As etapas a seguir explicam a clonagem do repositório do Spring Boot Docker usando o IntelliJ. Se desejar usar uma linha de comando, consulte [Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure][Deploy Spring Boot on Linux in AKS].

1. Abra o IntelliJ.

1. Na tela de boas-vindas, selecione a opção **GitHub** na lista **Fazer Check-out do Controle de Versão**.

   ![Opção do GitHub para controle de versão][CL01]

1. Se você for solicitado a fazer logon, insira suas credenciais.

   * Se você estiver usando um nome de usuário e uma senha para fazer logon no GitHub: 

      ![Caixa de diálogo para inserir o nome de usuário e a senha do GitHub][CL02a]

   * Se você estiver usando um token para fazer logon no GitHub: 

      ![Caixa de diálogo para inserção de um token do GitHub][CL02b]

1. Insira **https://github.com/spring-guides/gs-spring-boot-docker.git** como a URL do repositório, especifique o caminho local e as informações de pasta e, em seguida, clique em **Clonar**.

   ![Caixa de diálogo Clonar Repositório][CL03]

1. Quando solicitado a criar um projeto do IntelliJ, selecione **Não**.

   ![Recusar-se a criar um projeto do IntelliJ][CL04]

1. Na página inicial, clique em **Importar Projeto**.

   ![Seleção Importar Projeto][CL05]

1. Localize o caminho em que você clonou o repositório do Spring Boot, selecione a pasta **complete** na raiz e, depois, clique em **OK**.

   ![Selecionar uma pasta para importação][CL06]

1. Quando solicitado, selecione **Criar projeto com base nas fontes existentes**.

   ![Opção para criar um projeto com base nas fontes existentes][CL07]

1. Especifique o nome do projeto ou aceite o padrão, confirme o caminho correto para a pasta **complete** e, em seguida, clique em **Avançar**.

   ![Especifique o nome do projeto][CL08]

1. Personalize quaisquer diretórios para importação e, em seguida, clique em **Próximo**.

   ![Escolher diretórios][CL09]

1. Examine as bibliotecas para importar e, em seguida, clique em **Próximo**.

   ![Examine as bibliotecas do projeto][CL10]

1. Examine a estrutura do módulo e, em seguida, clique em **Próximo**.

   ![Examinar a estrutura do módulo][CL11]

1. Especifique o seu JDK e, em seguida, clique em **Próximo**.

   ![Especificar um JDK][CL12]

1. Clique em **Concluir**.

   ![Botão Concluir][CL13]

O IntelliJ importa o aplicativo Spring Boot como um projeto e exibe a estrutura após a conclusão da importação.

![Aplicativo Spring Boot no IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Criar seu aplicativo Spring Boot

### <a name="build-the-app-by-using-the-maven-pom"></a>Criar o aplicativo usando o POM do Maven

1. Abra a janela de ferramentas do Maven, caso ela ainda não esteja aberta. Clique em **Exibir** > **Janelas de Ferramentas** > **Projetos do Maven**.

   ![Comandos da Janela de Ferramentas e Projetos do Maven][BU01]

1. Na janela de ferramentas do Maven, clique com o botão direito do mouse em **Pacote** e selecione **Executar Build do Maven**. (Se o projeto do Maven não for mostrado automaticamente, clique no ícone **Reimportar** na barra de ferramentas do Maven.)

   ![Executar o comando de Build do Maven][BU02]

1. O IntelliJ deverá exibir uma mensagem **ÊXITO NO BUILD** quando o aplicativo Spring Boot for criado com êxito.

   ![Mensagem ÊXITO NO BUILD][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Criar um artefato pronto para implantação

Para publicar o aplicativo Spring Boot, você precisa criar um artefato pronto para implantação. Use as seguintes etapas:

1. Abra seu projeto de aplicativo Web no IntelliJ.

1. Clique em **Arquivo** e depois em **Estrutura do Projeto**.

   ![Comando Estrutura do Projeto][ART01]

1. Clique no símbolo de sinal de adição verde (**+**) para adicionar um artefato, clique em **JAR** e, em seguida, em **Vazio**.

   ![Adicionar um artefato][ART02]

1. Nomeie seu artefato sem adicionar a extensão ".jar" e, em seguida, especifique a pasta de destino para a saída do Maven.

   ![Especificar as propriedades do artefato][ART03]

1. Crie um manifesto para o artefato (opcional):

   a. Clique em **Criar Manifesto**.

      ![Clicar no botão Criar Manifesto][ART04a]

   b. Escolha o caminho padrão para o artefato e clique em **OK**.

      ![Especificar o caminho do artefato][ART04b]

   c. Clique nas reticências (**…**) para localizar a classe principal.

      ![Localizar a classe principal][ART04c]

   d. Escolha sua classe principal e, em seguida, clique em **OK**.

      ![Especificar a classe principal][ART04d]

1. Clique em **OK**.

   ![Fechar a caixa de diálogo Estrutura do Projeto][ART05]

> [!NOTE]
> Para obter mais informações sobre como criar artefatos no IntelliJ, consulte [Configurar Artefatos] no site da JetBrains.
>

### <a name="build-the-artifact-for-deployment"></a>Faça o build do artefato para implantação

1. Clique em **Criar** e, em seguida, clique em **Artefatos**.

   ![Comando Criar Artefatos][BU04]

1. Quando o menu de contexto **Criar Artefato** for exibido, clique em **Criar**.

   ![Menu de contexto Criar Artefato][BU05]

O IntelliJ deverá exibir o artefato concluído para o aplicativo Spring Boot na janela de ferramentas do projeto.

   ![Artefato criado][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicar seu aplicativo Web no Azure usando um contêiner do Docker

1. Se você não entrou em sua conta do Azure, siga as etapas em [Instruções de conexão para o Kit de Ferramentas do Azure para IntelliJ][Azure Sign In for IntelliJ].

1. Na janela de ferramentas do Explorador de Projeto, clique com o botão direito do mouse no projeto e, em seguida, selecione **Azure** > **Publicar como Contêiner Docker**.

   ![Comando Publicar como Contêiner do Docker][PU01]

1. Quando a caixa de diálogo **Implantar Contêiner do Docker no Azure** for exibida, todos os hosts existentes do Docker serão exibidos. Se você optar por implantar em um host existente, poderá pular para a etapa 4. Caso contrário, use as seguintes etapas para criar um host:

   a. Clique no símbolo de sinal de adição verde (**+**).

      ![Adicionar um novo host do Docker][PU02]

   b. Quando a caixa de diálogo **Criar Host do Docker** for exibida, você poderá optar por aceitar os padrões ou especificar configurações personalizadas para o novo host do Docker. (Para obter descrições detalhadas das várias configurações, consulte [Publicar um aplicativo Web como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **Próximo** quando tiver especificado as configurações a serem usadas.

      ![Especificar opções de host do Docker][PU03a]

   c. Você pode optar por usar as credenciais de logon existentes de um Azure Key Vault ou inserir novas credenciais de logon do Docker. Clique em **Concluir** quando tiver especificado suas opções.

      ![Especificar as credenciais de host do Docker][PU03b]

1. Selecione o host do Docker e, em seguida, clique em **Avançar**.

   ![Selecionar o host do Docker a ser usado][PU04]

1. Na última página da caixa de diálogo **Implantar o Contêiner do Docker no Azure**, especifique as seguintes opções:

   a. Você pode optar por especificar um nome personalizado para o contêiner que hospedará o contêiner do Docker ou aceitar o padrão.

   b. Insira as portas TCP do host do Docker usando a seguinte sintaxe: *[external port]*:*[internal port]*. Por exemplo, **80:8080** especifica uma porta externa 80 e a porta interna padrão 8080 do Spring Boot.
   
      Se você tiver personalizado a porta interna (por exemplo, editando o arquivo application.yml), precisará especificar o número da porta para o roteamento correto ocorrer no Azure.

   c. Depois de configurar essas opções, clique em **Concluir**.

   ![Implantar um contêiner do Docker no Azure][PU05]

1. Quando o Kit de Ferramentas do Azure concluir a publicação, o Log de Atividades do Azure exibirá **Publicado** como o status.

   ![Host do Docker implantado com êxito][PU06]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre outros métodos para criar aplicativos Spring Boot usando o IntelliJ, consulte [Criando projetos do Spring Boot](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) no site da JetBrains.

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configurar Artefatos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
