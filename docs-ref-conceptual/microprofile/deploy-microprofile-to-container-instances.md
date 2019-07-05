---
title: Implantar um aplicativo do MicroProfile na nuvem usando o Docker e o Azure
description: Saiba como implantar um aplicativo do MicroProfile na nuvem usando o Docker e as Instâncias de Contêiner do Azure.
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533609"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a>Implantar um aplicativo do MicroProfile na nuvem usando o Docker e o Azure

Este artigo demonstra como empacotar um aplicativo [MicroProfile.io] em um contêiner do Docker e executá-lo nas Instâncias de Contêiner do Azure.

> [!NOTE]
> Este procedimento funciona com qualquer implementação do MicroProfile.io, desde que a imagem de contêiner do Docker seja autoexecutável (ou seja, a imagem inclui o tempo de execução).

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este tutorial, você precisará dos seguintes pré-requisitos:

* Uma assinatura do Azure. Caso ainda não tenha uma assinatura do Azure, inscreva-se em uma [conta gratuita do Azure].
* A [CLI do Azure] instalada.
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para uso durante o desenvolvimento no Azure, confira [Suporte de longo prazo do Java para o Azure e o Azure Stack](https://aka.ms/azure-jdks).
* A ferramenta de build [Apache Maven] (versão 3 ou posterior).
* Um cliente [Git].

## <a name="microprofile-hello-azure-sample"></a>Exemplo do MicroProfile Hello Azure

Neste artigo, você usará a amostra [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure). Clone, compile e execute-a localmente usando os seguintes comandos:

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

Teste o aplicativo chamando `curl` ou usando um [navegador](http://localhost:8080/api/hello):

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a>Implantar o aplicativo no Azure

Agora leve esse aplicativo ao Azure usando os serviços [Instâncias de Contêiner do Azure] e [Registro de Contêiner do Azure].

### <a name="build-a-docker-image"></a>Compilar uma imagem do docker

O projeto de exemplo fornece um Dockerfile que você poderá usar. No entanto, você não precisa ter o Docker instalado, pois usará o recurso Build do Registro de Contêiner do Azure para compilar a imagem na nuvem.

Para compilar a imagem e se preparar para executá-la no Azure, faça o seguinte:

1. Instale a CLI do Azure e entre nela.
1. Crie um grupo de recursos do Azure.
1. Crie uma instância do Registro de Contêiner do Azure.
1. Compile uma imagem do Docker.
1. Publique a imagem do Docker na instância do registro de contêiner criada anteriormente.
1. (Opcional) Compile e publique a imagem na instância do registro de contêiner em um comando.


#### <a name="set-up-the-azure-cli"></a>Configurar a CLI do Azure

Verifique se você tem uma assinatura do Azure, se instalou [a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) e se está autenticado em sua conta:

```bash
az login
```

#### <a name="create-a-resource-group"></a>Criar um grupo de recursos

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a>Criar uma instância do registro de contêiner

Este comando deverá criar uma instância do registro de contêiner global exclusiva globalmente com um nome básico e um número aleatório.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Criar a imagem de Docker

Embora você possa compilar a imagem do Docker localmente com facilidade usando o próprio Docker, talvez queira considerar compilá-la na nuvem por alguns motivos:

* Não é necessário instalar o Docker localmente.
* Isso é muito mais rápido, porque o build ocorre em outro lugar (com exceção do tempo de upload do contexto).
* O processo na nuvem tem um acesso mais rápido à Internet e, portanto, downloads mais rápidos.
* A imagem vai diretamente para a instância do registro de contêiner.

Por esses motivos, você compilará a imagem usando o recurso [Build do Registro de Contêiner do Azure]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a>Implantar a imagem do Docker por meio da instância do Registro de Contêiner do Azure nas Instâncias de Contêiner

Agora que a imagem está disponível na instância do registro de contêiner, envie uma instância de contêiner por push e crie uma instância dela nas Instâncias de Contêiner. Mas primeiro, verifique se você consegue se autenticar na instância do registro de contêiner:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Testar o aplicativo do MicroProfile implantado

Seu aplicativo agora deve estar em execução. Para testá-lo na interface de linha de comando, use o seguinte comando:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Parabéns! Você criou um aplicativo do MicroProfile como um contêiner do Docker e o implantou no Azure com êxito.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as várias tecnologias abordadas neste artigo, confira:

* [Entrar no Azure por meio da CLI do Azure](/azure/xplat-cli-connect)

<!-- URL List -->

[Build do Registro de Contêiner do Azure]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI do Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Instâncias de Contêiner do Azure]: https://docs.microsoft.com/azure/container-instances/
[Registro de Contêiner do Azure]:  https://docs.microsoft.com/azure/container-registry
