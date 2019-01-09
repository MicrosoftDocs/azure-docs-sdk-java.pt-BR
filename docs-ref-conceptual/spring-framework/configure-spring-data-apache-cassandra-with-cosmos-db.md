---
title: Como usar a API do Apache Cassandra do Spring Data com o Azure Cosmos DB
description: Saiba como usar a API do Apache Cassandra do Spring Data com o Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991957"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a>Como usar a API do Apache Cassandra do Spring Data com o Azure Cosmos DB

## <a name="overview"></a>Visão geral

Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações usando a [API do Cassandra do Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction).

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.
* [Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.
* Um cliente [Git](https://git-scm.com/downloads).

## <a name="create-an-azure-cosmos-db-account"></a>Criar uma conta do Azure Cosmos DB

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a>Criar uma conta do Cosmos DB usando o portal do Azure

> [!NOTE]
> 
> Veja informações mais detalhadas sobre como criar contas do Azure Cosmos DB na [documentação do Azure Cosmos DB](/azure/cosmos-db/).

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Azure Cosmos DB**.

   ![Criar uma conta do Azure Cosmos DB][COSMOSDB01]

1. Especifique as seguintes informações:

   - **Assinatura**: especifique a assinatura do Azure para usar.
   - **Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.
   - **Nome da conta**: Escolha um nome exclusivo para sua conta do Cosmos DB. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyscassandra.documents.azure.com*.
   - **API**: Especifique `Cassandra` para este tutorial.
   - **Localização**: especifique a região geográfica mais próxima do banco de dados.

   ![Especificar as configurações de conta do Cosmos DB][COSMOSDB02]
   
1. Após inserir todas as informações acima, clique em **Revisar + Criar**.

1. Se estiver tudo correto na página de revisão, clique em **Criar**.

   ![Revisar as configurações de conta do Cosmos DB][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a>Adicionar um keyspace à sua conta do Azure Cosmos DB

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **Todos os Recursos** e, em seguida, clique na conta do Azure Cosmos DB que você acabou de criar.

   ![Escolher a conta do Azure Cosmos DB][COSMOSDB04]

1. Clique em **Data Explorer** e em **Novo Keyspace**. Insira um identificador exclusivo para sua **id do Keyspace** e, em seguida, clique em **OK**.

   ![Criar um keyspace do Cosmos DB][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a>Recuperar as configurações de conexão da conta do Azure Cosmos DB

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **Todos os Recursos** e, em seguida, clique na conta do Azure Cosmos DB que você acabou de criar.

   ![Escolher a conta do Azure Cosmos DB][COSMOSDB04]

1. Clique em **Cadeias de conexão** e copie os valores dos campos **Ponto de Contato**, **Porta**, **Nome de Usuário** e **Senha Primária**. Você usará esses valores para configurar seu aplicativo mais tarde.

   ![Recuperar as configurações de conexão do Cosmos DB][COSMOSDB05]

## <a name="configure-the-sample-application"></a>Configurar o aplicativo de exemplo

1. Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.

1. Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `spring.data.cassandra.contact-points` | Especifica o **Ponto de Contato** neste artigo. |
   | `spring.data.cassandra.port` | Especifica a **Porta** neste artigo. |
   | `spring.data.cassandra.username` | Especifica seu **Nome de Usuário** neste artigo. |
   | `spring.data.cassandra.password` | Especifica sua **Senha Primária** neste artigo. |

1. Salve e feche o arquivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empacotar e testar o aplicativo de exemplo 

1. Crie seu aplicativo de exemplo com o Maven. Por exemplo:

   ```shell
   mvn clean package
   ```

1. Inicie o aplicativo de exemplo. Por exemplo:

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   Seu aplicativo deve retornar valores como os seguintes:

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   Seu aplicativo deve retornar valores como os seguintes:

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Resumo

Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações usando a API do Cassandra do Azure Cosmos DB.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.

> [!div class="nextstepaction"]
> [Spring no Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionais

Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].

<!-- URL List -->

[Azure para desenvolvedores Java]: /java/azure/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Como trabalhar com o Java e o Azure DevOps]: /azure/devops/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
