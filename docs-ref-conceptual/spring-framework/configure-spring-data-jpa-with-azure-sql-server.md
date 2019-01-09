---
title: Como usar o Spring Data JPA com o Banco de Dados SQL do Azure
description: Saiba como usar o Spring Data JPA com um banco de dados SQL do Azure.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 7119283bec250a4ab0854ba2c29b0906624448e9
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991959"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a>Como usar o Spring Data JPA com o Banco de Dados SQL do Azure

## <a name="overview"></a>Visão geral

Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações em um [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/) usando [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.
* [Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.
* Um cliente [Git](https://git-scm.com/downloads).

## <a name="create-an-azure-sql-satabase"></a>Criar um Banco de Dados SQL do Azure

### <a name="create-a-sql-database-server-using-the-azure-portal"></a>Criar um servidor de banco de dados SQL usando o Portal do Azure

> [!NOTE]
> 
> Você pode ler informações mais detalhadas sobre como criar bancos de dados SQL do Azure em [Criar um banco de dados SQL do Azure no portal do Azure](/azure/sql-database/sql-database-get-started-portal).

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Banco de Dados SQL**.

   ![Criar um banco de dados SQL][SQL01]

1. Especifique as seguintes informações:

   - **Nome do banco de dados**: escolha um nome exclusivo para seu banco de dados SQL. Ele será criado no SQL Server que você especificará posteriormente.
   - **Assinatura**: especifique a assinatura do Azure para usar.
   - **Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.
   - **Selecionar fonte**: No caso deste tutorial, escolha `Blank database` para criar um novo banco de dados.

   ![Especificar as propriedades do banco de dados SQL][SQL02]
   
1. Clique em **Servidor**, **Criar um novo servidor** e especifique as seguintes informações:

   - **Nome do servidor**: Escolha um nome exclusivo para seu SQL Server. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyssql.database.windows.net*.
   - **Logon de administrador do servidor**: especifique o nome do administrador do banco de dados.
   - **Senha** e **Confirmar senha**: especifique a senha para o administrador do banco de dados.
   - **Localização**: especifique a região geográfica mais próxima do banco de dados.

   ![Especificar o SQL Server][SQL03]

1. Após inserir todas as informações acima, clique em **Selecionar**.

1. No caso deste tutorial, especifique o **Tipo de preço** menos caro e clique em **Criar**.

   ![Criar o banco de dados SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a>Configurar uma regra de firewall para o SQL Server usando o Portal do Azure

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **Todos os Recursos** e, em seguida, clique no SQL Server que você acabou de criar.

   ![Escolher o SQL Server][SQL05]

1. Na seção **Visão geral**, clique em **Mostrar configurações de firewall**

   ![Mostrar configurações de firewall][SQL06]

1. Na seção **Firewalls e redes virtuais**, crie uma nova regra especificando um nome exclusivo para a regra, insira o intervalo de endereços IP que precisarão acessar seu banco de dados e clique em **Salvar**.

   ![Definir configurações de firewall][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a>Recuperar a cadeia de conexão para seu SQL Server usando o Portal do Azure

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **Todos os Recursos** e, em seguida, clique no banco de dados SQL que você acabou de criar.

   ![Escolher o banco de dados SQL][SQL08]

1. Clique em **Cadeias de conexão**, clique em **JDBC** e copie o valor no campo de texto JDBC.

   ![Recuperar sua cadeia de conexão JDBC][SQL09]

## <a name="configure-the-sample-application"></a>Configurar o aplicativo de exemplo

1. Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.

1. Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `spring.datasource.url` | Especifica a versão editada da cadeia de JDBC do SQL neste artigo. |
   | `spring.datasource.username` | Especifica o nome do administrador do SQL neste artigo com o nome abreviado do servidor anexado a ele. |
   | `spring.datasource.password` | Especifica sua senha de administrador do SQL neste artigo. |

1. Salve e feche o arquivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empacotar e testar o aplicativo de exemplo 

1. Crie seu aplicativo de exemplo com o Maven. Por exemplo:

   ```shell
   mvn clean package -P sql
   ```

1. Inicie o aplicativo de exemplo. Por exemplo:

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   Seu aplicativo deve retornar valores como os seguintes:

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   Seu aplicativo deve retornar valores como os seguintes:

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Resumo

Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações em um banco de dados SQL do Azure usando o JPA.

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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png
