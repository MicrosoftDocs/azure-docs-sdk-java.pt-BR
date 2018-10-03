---
title: CI/CD para aplicativos MicroProfile usando o Azure DevOps
description: Saiba como configurar um ciclo de lançamento de CI/CD para implantar um aplicativo MicroProfile em uma instância do Aplicativo Web para Contêineres do Azure usando o Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506259"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a>CI/CD para aplicativos MicroProfile usando o Azure DevOps

Este tutorial mostra como os desenvolvedores Java EE podem configurar facilmente um ciclo de lançamento de CI/CD para implantar seus aplicativos [MicroProfile](http://microprofile.io) em um Aplicativo Web para Contêineres usando o Azure DevOps (antes conhecido como VSTS).  Neste exemplo, usaremos um aplicativo MicroProfile que usa um [Payara Micro](https://www.payara.fish/payara_micro) como uma imagem básica.   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
Vamos começar o processo de colocação em contêiner do Azure DevOps criando uma imagem do Docker e enviando a imagem de contêiner para um Registro de Contêiner do Azure.  Em seguida, conclua com um pipeline de lançamento do Azure DevOps para implantar a imagem de contêiner em um aplicativo Web.

## <a name="prerequisites"></a>Pré-requisitos
- Copiar e salvar a URL Git do [Github](https://github.com/Azure-Samples/microprofile-hello-azure)
- Registrar-se ou fazer logon em sua conta do [Azure DevOps](https://dev.azure.com)
- Criar um novo [projeto do Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) e usar a URL Git acima para **importar um repositório**
- Criar um [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR)
- Criar um Aplicativo Web para Contêiner do Azure
> [!NOTE]
>
> Selecionar "Início Rápido" nas Configurações do Contêiner ao provisionar a instância do Aplicativo Web


## <a name="create-a-build-definition"></a>Criar a definição de build

A definição de build no Azure DevOps executa automaticamente todas as tarefas no build sempre que há uma confirmação no aplicativo de origem do Java EE.  Neste exemplo, o Azure DevOps usará Maven para compilar o projeto MicroProfile em Java.

1. Clique na guia "Build e Versão" na parte superior da página do projeto Azure DevOps.  Em seguida, selecione o link **Builds** 

<img src="media/VSTS/Buid-and-Release1.png">

2. Clique no botão **Novo Pipeline** e em **Continuar** para começar a definir as tarefas de build
3. Selecione "Maven" na lista de modelos e clique no botão **Aplicar** para compilar seu projeto Java
4. Use o menu suspenso no campo Pool de agentes para selecionar a opção **Versão prévia do Linux Hospedada**.
> [!NOTE]
>
> Isso informa ao Azure DevOps sobre qual servidor de build usar.  Você pode usar seu próprio servidor de build personalizado

5. Para configurar o build para a integração contínua, selecione a guia **Gatilhos** e marque a caixa de seleção **Habilitar integração contínua**.  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. Selecione a guia **Tarefas** para retornar à página do pipeline de build principal
7. Use o menu suspenso **Salvar e enfileirar** para selecionar a opção **Salvar**
 

## <a name="create-a-docker-build-image"></a>Criar uma Imagem de Build do Docker

Nessa tarefa, o Azure DevOps usa um Dockerfile com uma imagem básica do Payara Micro para criar uma imagem do Docker.  

1. Selecione a guia **Tarefas** para retornar à página do pipeline de build principal
2. Clique no ícone **+** para adicionar uma nova tarefa à definição de build
 
<img src="media/VSTS/Tasks-add4.png">
 
3. Selecione "Docker" na lista de modelos e clique no botão **Adicionar**
4. Insira um nome descritivo no campo **Nome de exibição**
5. Verifique se a opção **Registro de Contêiner do Azure** está selecionada no menu suspenso do **Tipo do registro de contêiner**.
> [!NOTE]
>
>  Se você estiver usando o Hub do Docker ou outro registro, selecione "Registro de Contêiner".  Em seguida, clique no botão "+ Novo" para fornecer as credenciais e as informações de conexão. Vá para a seção Comandos para continuar.

6. Use o menu suspenso **Assinatura do Azure** para selecionar a ID de sua assinatura do Azure.  Em seguida, clique no botão **Autorizar**
7. No menu suspenso **Registro de contêiner do Azure**, selecione o nome de registro criado no Azure.
8. Verifique se a opção **build** está selecionada no menu suspenso **Comando**.
9. Para o **Dockerfile**, clique no ícone de navegação do caminho ao lado da caixa de texto para selecionar o Dockerfile no projeto GitHub.  Em seguida, clique no botão **OK**.

<img src="media/VSTS/Dockerfile5.png">

10. No **Nome da imagem**, marque a caixa de seleção **Incluir marca mais recente**. 
11. Use o menu suspenso **Salvar e enfileirar** para selecionar a opção **Salvar**.

## <a name="push-docker-image-to-acr"></a>Enviar por push a Imagem do Docker para o ACR

Nessa tarefa, o Azure DevOps enviará por push a imagem do Docker para seu Registro de Contêiner do Azure.  Isso será usado para executar o aplicativo de API MicroProfile como um aplicativo Web Java em contêineres.

1. Como estamos usando o Docker no Azure DevOps, crie um novo modelo de Docker repetindo as etapas 1 a 7 acima na seção **Criar uma Imagem de Build do Docker**.
2. Selecione **push** no menu suspenso **Comando**.
3. Clique na guia **Salvar e enfileirar** e selecione a opção **Salvar e enfileirar**.
4. Verifique se a **Versão Prévia do Linux Hospedada** está selecionada para o Pool de agentes na janela pop-up.  Em seguida, clique no botão **Salvar e enfileirar**.
5. Clique no número de build para verificar se o pipeline de build do projeto Java foi concluído com êxito.

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a>Criar uma definição da versão para um aplicativo Java

O pipeline de lançamento no Azure DevOps dispara automaticamente a implantação de artefatos de build em um ambiente de destino, como o Azure, assim que o processo de compilação é concluído com êxito.   O pipeline de lançamento pode ser criado para ambientes de desenvolvimento, teste, preparo ou produção.

1. Clique na guia "Build e versão" na parte superior da página do projeto Azure DevOps.  Em seguida, selecione o link **Versões**.

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. Clique no botão “Novo pipeline”
3. Selecione **Implantar um aplicativo Java no Serviço de Aplicativo do Azure** na lista de modelos e clique no botão **Aplicar**.

<img src="media/VSTS/deploy-java-template8.png">
 
4. Defina um **Nome do estágio** (por exemplo, Desenvolvimento, Teste, Preparo ou Produção).  Em seguida, clique no botão **X** para fechar a janela pop-up
5. Clique no botão **+ Adicionar** na seção Artefatos.  Isso vinculará os artefatos da definição de build a essa definição da versão.  
6. Use o menu suspenso da **Fonte (pipeline de build)** para selecionar sua definição de build. Em seguida, clique no botão **Adicionar** para continuar.

<img src="media/VSTS/add-artifact9.png">
 
7. Clique na guia **Tarefas** no pipeline.  Depois, selecione o nome do estágio.
 
<img src="media/VSTS/release-stage10.png">

8. Use o menu suspenso **Assinatura do Azure** para selecionar a ID de sua assinatura do Azure.
9. Selecione **Aplicativo Linux** no menu suspenso **Tipo de aplicativo**.
10. Selecione o nome da instância do Aplicativo Web para Contêiner criado acima, no menu suspenso **Nome do serviço de aplicativo**
11. Insira o nome do registro de contêiner do Azure no campo **Registro ou Namespaces**.  Por exemplo, **myregistry.azure.io**
12. Insira o nome do registro no campo **Repositório**
13. Clique em **Implantar Serviço de Aplicativo do Azure**.  Insira a marca da imagem de contêiner na caixa de texto **Marca**. 
14. Clique em **Executar no agente**.  Selecione **Versão Prévia do Linux Hospedada** no menu suspenso Pool de agentes. 

## <a name="setup-environment-variables"></a>Configurar Variáveis de Ambiente

1. Clique na guia **Variáveis**.  Em seguida, clique no botão **+ Adicionar** para definir as variáveis de ambiente.
2. Adicione o nome da variável e valores para a URL do registro de contêiner, nome de usuário e senha.   Para maior segurança, clique no ícone de cadeado para ocultar o valor da senha.

Por exemplo: 
- registry.password
- registry.url
- registry.username

<img src="media/VSTS/environment-variables12.png">

3. Clique na guia **Tarefas** para retornar à página de definição do pipeline de lançamento principal.
4. Clique em **Implantar Serviço de Aplicativo do Azure**. 
5. Expanda a seção **Definições do Aplicativo e da Configuração** e clique no caminho de navegação do campo **Configurações do Aplicativo** para adicionar a variável de ambiente e conectar o registro de contêiner durante a implantação.
6. Clique no botão ** + Adicionar** para definir as configurações do aplicativo a seguir e atribuir as variáveis de ambiente.
- DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)
- DOCKER_REGISTRY_SERVER_URL = $(registry.url)
- DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)

<img src="media/VSTS/environment-variables14.png">
 
7. Clique no botão **OK** para continuar

## <a name="setup-continious-deployment--deploy-java-application"></a>Configurar Implantação Contínua e Implantar Aplicativo Java

1. Para habilitar a implantação contínua, clique na guia **Pipelines**
2. Na seção Artefatos, clique no ícone de raio.  Em seguida, defina o **Gatilho de implantação contínua** para Habilitado.

<img src="media/VSTS/release-enable-CD.png">
 
3. Clique no botão **Salvar** e no botão **OK** 
4. Clique no menu suspenso **+ Versão** e selecione o link **Criar uma versão**
5. Use o menu suspenso **Estágios para alterar gatilho de automático para manual** para marcar a caixa de seleção do nome do estágio
6. Clique no botão **Criar** para continuar
7. Clique no número da versão.  Em seguida, passe o cursor do mouse sobre o nome do estágio e clique no botão **Implantar**
8. Clique no botão **Implantar** na janela pop-up para iniciar o processo de implantação no Azure


## <a name="test-the-java-web-application"></a>Testar Aplicativo Web Java
1. Execute a URL do aplicativo Web no navegador da Web:  
https://{nome-do-serviço-de-aplicativo}.azurewebsites.net/api/hello

 
<img src="media/VSTS/web-app16.png">

2. A página da Web deverá mostrar **Olá Azure!**
 
<img src="media/VSTS/web-api17.png">
