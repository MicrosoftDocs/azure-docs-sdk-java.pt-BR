---
title: "Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para Eclipse"
description: "Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: b54c10dc33324d902a0e778770df8ec4d71dc9a1
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para Eclipse

O [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores do Java a criar aplicativos de nível empresarial. Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.

O [Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos executados em contêineres.

Este tutorial explica as etapas para implantação de um aplicativo Spring Boot como um contêiner do Docker no Microsoft Azure usando o Kit de Ferramentas do Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>Clonar o repositório padrão do Spring Boot Docker

### <a name="import-the-public-repository"></a>Importar o repositório público

As etapas a seguir explicam a clonagem do repositório do Spring Boot Docker para o computador local usando o IntelliJ. Se desejar usar uma linha de comando, consulte [Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure][Deploy Spring Boot on Linux in AKS].

1. Abra o Eclipse.

1. Clique em **Arquivo** > **Importar**.

   ![Menu de Importação de Arquivo][CL01]

1. Quando a caixa de diálogo **Importação** se abrir:

   a. Expanda **Git**.

   b. Selecione **Projetos do Git**.
   
   c. Clique em **Próximo**.

   ![Caixa de diálogo de Importação][CL02]

1. Na página **Selecionar a Origem do Repositório**:

   a. Selecione **Clonar URI**.
   
   b. Clique em **Próximo**.

   ![Página Selecionar Origem do Repositório][CL03]

1. Na página **Repositório Git de Origem**:

   a. Em **URI**, insira `https://github.com/spring-guides/gs-spring-boot-docker.git`. Essa etapa deve popular automaticamente os campos **Host** e **Caminho do repositório** com os valores corretos.
   
   b. O repositório Spring Boot é público, assim, você não precisa inserir seu nome de usuário e senha do Git.
   
   c. Clique em **Próximo**.

   ![Página Repositório Git de Origem][CL04]

1. Na página **Seleção de Branch**, clique em **Avançar**.

   ![Página Seleção de Branch][CL05]

1. Na página **Destino Local**:

   a. Especifique a pasta local em que você deseja colocar seu repositório local.
   
   b. Clique em **Próximo**.

   ![Página Destino Local][CL06]

1. Na página **Selecionar um assistente a usar para importar projetos**:

   a. Selecione **Importar como um projeto geral**.
   
   b. Clique em **Próximo**.

   ![Página “Selecionar um assistente a ser usado para a importação de projetos”][CL07]

1. Na página **Importar Projetos**:

   a. Especifique o nome do projeto.
   
   b. Clique em **Concluir**.

   ![Página Importar Projetos][CL08]

1. Quando o repositório for clonado com êxito, você verá todos os arquivos listados no Eclipse.

   ![Repositório local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Criar um projeto do Maven por meio do repositório local

O repositório do Spring Boot Docker contém um projeto completo do Maven, que será usado neste tutorial. 

1. Clique em **Arquivo** > **Importar**.

   ![Comando Importar no menu Arquivo][CL01]

1. Quando a caixa de diálogo **Importação** se abrir:

   a. Expanda **Maven**.
   
   b. Selecione **Projetos Existentes do Maven**.
   
   c. Clique em **Próximo**.

   ![Caixa de diálogo de Importação][MV01]

1. Na página **Projetos Maven**:

   a. Em **Diretório Raiz**, especifique a pasta **complete** no repositório local.
   
   b. Expanda a seção **Avançado** e insira um nome personalizado para o **Modelo de nome**.
   
   c. Marque a caixa do arquivo **pom.xml** no projeto.
   
   d. Clique em **Concluir**.

   ![Página Projetos do Maven][MV02]

1. Quando o projeto do Maven for aberto com êxito, você verá um segundo projeto listado no Eclipse.

   ![Projeto do Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Criar o aplicativo Spring Boot usando o Maven

1. No Eclipse Project Explorer, selecione o projeto do Maven.

1. Clique em **Executar** > **Executar Como** > **Build do Maven**.

   ![Comandos a serem executados como build do Maven][BU01]

1. Quando o aplicativo é criado com êxito, a janela do console mostra o status.

   ![Build bem-sucedido do Maven][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicar seu aplicativo Web no Azure usando um contêiner do Docker

1. No Eclipse Project Explorer, selecione o projeto do Maven.

1. Clique no menu **Publicar** do Azure e, em seguida, clique em **Publicar como Contêiner do Docker**.

   ![Comando Publicar como Contêiner do Docker][PU01]

1. Quando a caixa de diálogo **Implantando Contêiner do Docker no Azure** for exibida:

   a. Insira um nome de imagem do Docker personalizado.
   
   b. Para **Artefato a ser implantado**, especifique o caminho para o arquivo **gs-spring-boot-docker-0.1.0.jar** que você acabou de criar.

   ![Especificar opções do Docker][PU02]

   Os hosts existentes do Docker são exibidos. 

1. Se você optar por implantar em um host existente, vá para a etapa 5. Caso contrário, use as seguintes etapas para criar um host:

   a. Clique em **Adicionar**.

      ![Adicionar um novo host do Docker][PU03]

   b. Quando a caixa de diálogo **Criar Host do Docker** for exibida, você poderá optar por aceitar os padrões ou especificar configurações personalizadas para o novo host do Docker. (Para obter descrições detalhadas das várias configurações, consulte [Publicar um aplicativo Web como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **Próximo** quando tiver especificado as configurações a serem usadas.

      ![Especificar opções de host do Docker][PU04]

   c. Você pode optar por usar as credenciais de logon existentes de um Azure Key Vault ou inserir novas credenciais de logon do Docker. Clique em **Concluir** quando tiver especificado suas opções.

      ![Especificar as credenciais de host do Docker][PU05]

1. Selecione o host do Docker e, em seguida, clique em **Avançar**.

   ![Selecione o host do Docker a usar][PU06]

1. Na última página da caixa de diálogo **Implantando o Contêiner do Docker no Azure**, especifique as seguintes opções:

   a. Você pode optar por especificar um nome personalizado para o contêiner que hospedará o contêiner do Docker ou aceitar o padrão.

   b. Insira as portas TCP do host do Docker usando a seguinte sintaxe: *[external port]*:*[internal port]*. Por exemplo, **80:8080** especifica uma porta externa 80 e a porta interna padrão 8080 do Spring Boot.
   
      Se você tiver personalizado a porta interna (por exemplo, editando o arquivo application.yml), precisará especificar o número da porta para o roteamento correto ocorrer no Azure.

   c. Depois de configurar essas opções, clique em **Concluir**.

   ![Implantar um contêiner do Docker no Azure][PU07]

1. Quando o Kit de Ferramentas do Azure concluir a publicação, o Log de Atividades do Azure exibirá **Publicado** como o status.

   ![Host do Docker implantado com êxito][PU08]

## <a name="next-steps"></a>Próximas etapas

Para obter recursos adicionais para o Docker, consulte o (site do Docker) oficial.

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
