---
title: Implantar um aplicativo MicroProfile na nuvem com Docker e Azure
description: Saiba como implantar um aplicativo MicroProfile na nuvem usando Instâncias de Contêiner do Azure e Docker.
services: container-instances;container-retistry
documentationcenter: java
author: brborges
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: brborges
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c6254d11ee1596a23076931c9a2a2370b5f52409
ms.sourcegitcommit: 3d0896f821907278547c283c54b53fbd7f4f30f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43153897"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a>Implantar um aplicativo MicroProfile na nuvem com Docker e Azure

Este artigo demonstra como empacotar um aplicativo [MicroProfile.io] em um contêiner do Docker e executá-lo nas Instâncias de Contêiner do Azure.

> [!NOTE]
>
> Este procedimento funciona com qualquer implementação de MicroProfile.io, desde que a imagem de contêiner do Docker seja executada automaticamente (ou seja, inclui o tempo de execução).

## <a name="prerequisites"></a>Pré-requisitos

Para concluir as etapas neste tutorial, você precisará ter os seguintes pré-requisitos:

* Uma assinatura do Azure; se ainda não tiver uma, inscreva-se para uma [conta do Azure gratuita].
* A[CLI (interface de linha de comando) do Azure].
* Um JDK (Java Development Kit) versão 1.8 ou posterior atualizado.
* A ferramenta de build do [Maven] do Apache (versão 3+).
* Um cliente [Git].

## <a name="microprofile-hello-azure-sample"></a>Exemplo do MicroProfile Hello Azure

Para este artigo, usaremos o exemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):

### <a name="clone-build-and-run-locally"></a>Clonar, compilar e executar localmente

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

Você pode testar o aplicativo chamando `curl` ou visitando através de um [navegador](http://localhost:8080/api/hello):

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a>Implantar no Azure

Agora vamos colocar esse aplicativo na nuvem usando os serviços [Instâncias de Contêiner do Azure] e [Registro de Contêiner do Azure].

### <a name="build-a-docker-image"></a>Compilar uma imagem do docker

O exemplo de projeto já fornece um Dockerfile que você pode usar. No entanto, você não precisa do Docker instalado, já que usaremos o recurso de Build do Registro de Contêiner do Azure para compilar a imagem na nuvem.

Para compilar a imagem e se preparar para compilá-la no Azure, você terá que seguir estas etapas:

1. Instalar e fazer logon com a CLI do Azure
1. Criar um grupo de recursos do Azure
1. Criar um Registro de Contêiner do Azure (ACR)
1. Criar a imagem de Docker
1. Publicar a imagem do Docker no ACR criado anteriormente
1. (Opcionalmente) Compilar e publicar no ACR com um comando


#### <a name="set-up-azure-cli"></a>Configurar a CLI do Azure

Verifique se você tem uma assinatura do Azure, [CLI do Azure instalada](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), e que você está autenticado na sua conta:

```bash
az login
```

#### <a name="create-a-resource-group"></a>Criar um grupo de recursos

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a>Cria uma instância do Registro de Contêiner do Azure

Esse comando criará um registro de contêiner globalmente exclusivo (se tudo der certo) usando um nome básico com um número aleatório.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Criar a imagem de Docker

Enquanto você pode facilmente criar a imagem do Docker localmente usando o próprio Docker, você talvez queira considerar criá-lo na Nuvem por alguns motivos:

1. Não há necessidade de instalar o Docker localmente
1. Muito mais rápido, já que a compilação ocorrerá em outro lugar (com exceção de tempo de carregamento do contexto)
1. O processo na nuvem tem acesso à Internet mais rápida, portanto, os downloads são mais rápidos
1. A imagem vai diretamente para o Registro de Contêiner

Por esses motivos, vamos criar a imagem usando o recurso de [Build do Registro de Contêiner do Azure]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a>Implantar a imagem do Docker do Registro de Contêiner do Azure (ACR) nas Instâncias de Contêiner (ACI)

Agora que a imagem está disponível em seu ACR, vamos enviar por push e instanciar uma instância de contêiner na ACI. Mas primeiro, é preciso certificar-se de que podemos autenticar para o ACR:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Testar seu aplicativo MicroProfile implantado

Seu aplicativo agora deve estar em execução. Para testá-lo a partir da linha de comando, execute o seguinte comando:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Parabéns! Você compilou e implantou um aplicativo MicroProfile como um contêiner do Docker no Microsoft Azure com êxito.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:

* [Faça logon no Azure na CLI do Azure](/azure/xplat-cli-connect)

<!-- URL List -->

[Build do Registro de Contêiner do Azure]: https://docs.microsoft.com/en-us/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
