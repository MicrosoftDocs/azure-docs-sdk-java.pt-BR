---
title: Como usar o Inicializador do Spring Boot com a API do Armazenamento do Azure
description: Saiba como configurar um aplicativo iniciador do Spring Boot com a API do Armazenamento do Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 94f7b1148d9282d33bc67da0e0d97a284a81d4d4
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339050"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-storage-api"></a>Como usar o Inicializador do Spring Boot com a API do Armazenamento do Azure

## <a name="overview"></a>Visão geral

Este artigo orienta em relação à criação de um aplicativo personalizado usando o **Spring Initializr** e depois usando esse aplicativo para acessar o Armazenamento do Azure usando a API do Armazenamento do Azure.

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para uma [conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* A[CLI (interface de linha de comando) do Azure](http://docs.microsoft.com/cli/azure/overview).
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* [Maven](http://maven.apache.org/) do Apache, versão 3.0 ou posterior.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Criar um aplicativo personalizado usando o Spring Initializr

1. Navegue até <https://start.spring.io/>.

1. Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.

   ![Opções básicas do Initializr Basic](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > O Spring Initializr usará os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo: *com.contoso.wingtiptoysdemo*.
   >

1. Role para baixo, até a seção **Azure** e marque a caixa do **Armazenamento do Azure**.

   ![Opções do Spring Initilializr Completo](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. Role até a parte inferior da página e clique no botão **Gerar Projeto**.

   ![Opções do Spring Initilializr Completo](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. Quando solicitado, baixe o projeto para um caminho no computador local.

   ![Baixe o projeto personalizado do Spring Boot](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Entre no Azure e selecione a assinatura a ser usada

1. Abra um prompt de comando.

1. Entre em sua conta do Azure usando a CLI do Azure:

   ```azurecli
   az login
   ```
   Siga as instruções na tela para concluir o processo de entrada.

1. Liste suas assinaturas:

   ```azurecli
   az account list
   ```
   O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. Especifique o GUID para a conta que quer usar no Azure; por exemplo:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a>Criar uma conta de Armazenamento do Azure

1. Crie um grupo de recursos para os recursos do Azure que serão usados neste artigo. Por exemplo:
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Em que:

   | Parâmetro | Descrição |
   |---|---|
   | `name` | Especifica um nome exclusivo para o grupo de recursos. |
   | `location` | Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado. |

   A CLI do Azure exibirá os resultados da criação do grupo de recursos, por exemplo:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

2. Crie uma conta de armazenamento do Azure no grupo de recursos para seu aplicativo Spring Boot. Por exemplo:
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `name` | Especifica um nome exclusivo para sua conta de armazenamento. |
   | `resource-group` | Especifica o nome do grupo de recursos que você criou na etapa anterior. |
   | `location` | Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual sua conta de armazenamento será hospedada. |
   | `sku` | Especifica um dos seguintes: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`. |

   O Azure retornará uma cadeia de caracteres JSON longa, a qual contém o estado de provisionamento. Por exemplo: |

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

3. Recuperar a cadeia de conexão para sua conta de armazenamento. Por exemplo:
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   | ---|---|
   | `name` | Especifica um nome exclusivo da conta de armazenamento que você criou nas etapas anteriores. |
   | `resource-group` | Especifica o nome do grupo de recursos que você criou em etapas anteriores. |

   O Azure retornará uma cadeia de caracteres JSON que contém a cadeia de conexão para sua conta de armazenamento. Por exemplo:

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurar e compilar seu aplicativo Spring Boot

1. Extraia em um diretório os arquivos do projeto baixado.

1. Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.

1. Adicione a chave da sua conta de armazenamento. Por exemplo:
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. Navegue até a pasta */src/main/java/com/example/wingtiptoysdemo* no seu projeto e abra o arquivo *WingtiptoysdemoApplication.java* em um editor de texto.

1. Substitua o código existente do Java com o exemplo a seguir, o qual lista os blobs em um contêiner:

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > Os exemplo acima transmite automaticamente as configurações do armazenamento de conta que você definiu no arquivo *application.properties*.
   >

1. Compile e execute o aplicativo:
   ```shell
   mvn clean package spring-boot:run
   ```

   O aplicativo criará um contêiner e carregará um arquivo de texto como um blob ao contêiner, o qual será listado na sua conta de armazenamento no [portal do Azure](https://portal.azure.com).

   ![Listar blobs no portal do Azure](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > Quando você compila seu aplicativo, a seguinte mensagem de erro poderá ser exibida:
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > Se isso acontecer, talvez queira desabilitar teste do Maven Surefire. Para isso, adicione a seguinte entrada de plug-in no seu arquivo *pom.xml*:
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os iniciadores adicionais do Spring Boot disponíveis para o Microsoft Azure, consulte [Iniciadores do Spring Boot para o Azure](spring-boot-starters-for-azure.md).

Para obter informações adicionais sobre como integrar a funcionalidade do Azure em seus aplicativos baseados no Spring, consulte [Estrutura do Spring no Azure](/java/azure/spring-framework/).

Para obter informações detalhadas sobre APIs adicionais do armazenamento do Azure adicional que podem ser chamadas de seus aplicativos Spring Boot, consulte os seguintes artigos:
* [Como usar o armazenamento do Blob do Azure a partir do Java](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [Como usar o armazenamento de Fila do Azure a partir do Java](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [Como usar o armazenamento de Tabela do Azure a partir do Java](/azure/cosmos-db/table-storage-how-to-use-java)
* [Como usar o armazenamento de Arquivo do Azure a partir do Java](/azure/storage/files/storage-java-how-to-use-file-storage)
