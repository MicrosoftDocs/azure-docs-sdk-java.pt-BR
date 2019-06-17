---
title: Como usar o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB
description: Saiba como configurar um aplicativo criado com o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB.
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
ms.workload: data-services
ms.openlocfilehash: f00afbdd09ce617f863ed758f4bdddcb40701e27
ms.sourcegitcommit: 5bbf64121a99019207ed8cca29280fc5183c7314
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2019
ms.locfileid: "66840844"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a>Como usar o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB

## <a name="overview"></a>Visão geral

O Azure Cosmos DB é um serviço de banco de dados distribuído globalmente que permite aos desenvolvedores trabalhar com os dados usando várias APIs padrão, como as APIs SQL, MongoDB, Graph e de Tabela. O Inicializador do Spring Boot da Microsoft permite aos desenvolvedores usar aplicativos Spring Boot que se integram facilmente ao Azure Cosmos DB por meio da API SQL.

Este artigo demonstra como criar um Azure Cosmos DB usando o portal do Azure e, em seguida, usar o **[Spring Initializr]** para criar um aplicativo Spring Boot personalizado e adicionar o [Iniciador Spring Boot do Cosmos DB para Azure] ao aplicativo personalizado para armazenar e recuperar dados do Azure Cosmos DB usando o Spring Data e a API SQL do Cosmos DB.

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Criar um Azure Cosmos DB usando o portal do Azure

1. Navegue até o Portal do Azure em <https://portal.azure.com/> e clique em **+Criar um recurso**.

   ![Portal do Azure][AZ01]

1. Clique em **Bancos de Dados** e, em seguida, clique em **Azure Cosmos DB**.

   ![Portal do Azure][AZ02]

1. Na página **Azure Cosmos DB**, insira as seguintes informações:

   * Escolha a **Assinatura** você deseja usar para seu banco de dados.
   * Especifique se deseja criar um novo **Grupo de recursos** para seu banco de dados ou escolher um grupo de recursos existente.
   * Insira um **Nome da Conta** exclusivo, que será usado como o URI do banco de dados. Por exemplo: *wingtiptoysdata*.
   * Escolha **Core (SQL)** para a API.
   * Especifique o **Local** para seu banco de dados.

   Depois de especificar essas opções, clique em **Examinar + criar** para criar o banco de dados.

   ![Portal do Azure][AZ03]

1. Quando seu banco de dados for criado, ele será listado no seu **Painel** do Azure, bem como nas páginas **Todos os Recursos** e **Azure Cosmos DB**. Você pode clicar no banco de dados em qualquer um desses locais para abrir a página de propriedades do seu cache.

   ![Portal do Azure][AZ04]

1. Quando a página de propriedades do banco de dados for exibida, clique em **Chaves** e copie o URI e as chaves de acesso do banco de dados. Você usará esses valores no aplicativo Spring Boot.

   ![Portal do Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Criar um aplicativo Spring Boot simples com o Spring Initializr

1. Navegue até <https://start.spring.io/>.

1. Especifique que você deseja gerar um **Projeto Maven** com **Java**, especifique a versão do **Spring Boot**, insira os nomes de **Grupo** e de **Artefato** do aplicativo, adicione o **Suporte do Azure** nas dependências e, em seguida, clique no botão para **Gerar o Projeto**.

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote; por exemplo: *com.example.wintiptoysdata*.
   >

1. Quando solicitado, baixe o projeto em um caminho no computador local e extraia os arquivos.

   ![Extrair o projeto do Spring Boot personalizado][SI02]

1. Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.

   ![Arquivos de projeto Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-application-to-use-the-azure-spring-boot-starter"></a>Configurar o aplicativo Spring Boot para usar o Iniciador Spring Boot do Azure

1. Localize o arquivo *pom.xml* no diretório do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   -ou-

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Salve o arquivo pom.xml][PM01]

1. Abra o arquivo *pom.xml* em um editor de texto e adicione as seguintes linhas à lista de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-cosmosdb-spring-boot-starter</artifactId>
   </dependency>
   ```

   ![Edição do arquivo pom.xml][PM02]

1. Verifique se a versão do Spring Boot é a escolhida ao criar seu aplicativo com o Spring Initializr; por exemplo:

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.1.5.RELEASE</version>
      <relativePath/>
   </parent>
   ```

1. Verifique se você está usando a versão mais recente dos [iniciadores Spring Boot do Azure](https://github.com/microsoft/azure-spring-boot), por exemplo:

   ```xml
   <azure.version>2.1.6</azure.version>
   ```

1. Salve e feche o arquivo *pom.xml*.

## <a name="configure-your-spring-boot-application-to-use-your-azure-cosmos-db"></a>Configure o aplicativo Spring Boot para usar o Azure Cosmos DB

1. Localize o arquivo *application.properties* no diretório *recursos* do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Localize o arquivo application.properties][RE01]

1. Abra o arquivo *application.properties* em um editor de texto e adicione as seguintes linhas ao arquivo, então substitua os valores de exemplo pelas propriedades adequadas para seu banco de dados:

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.cosmosdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.cosmosdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.cosmosdb.database=wingtiptoysdata
   ```

   ![Edição do arquivo application.properties][RE02]

1. Salve e feche o arquivo *application.properties*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Adicione o código de exemplo para implementar a funcionalidade básica de banco de dados

Nesta seção, você criará duas classes Java para armazenamento de dados de usuário e, em seguida, modificará sua classe de aplicativo principal para criar uma instância da classe *Usuário* e salvá-la no banco de dados.

### <a name="define-a-base-class-for-storing-user-data"></a>Definir uma classe base para armazenar os dados do usuário

1. Criar um novo arquivo denominado *User.java* no mesmo diretório que o arquivo Java do seu aplicativo principal.

1. Abra o arquivo *User.java* em um editor de texto e adicione as seguintes linhas ao arquivo para definir uma classe de usuário genérica que armazena e recupera valores no seu banco de dados:

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;

      public User() {
      }

      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }

      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. Salve e feche o arquivo *User.java*.

### <a name="define-a-data-repository-interface"></a>Defina uma interface de repositório de dados

1. Criar um novo arquivo denominado *UserRepository.java* no mesmo diretório que o arquivo Java do seu aplicativo principal.

1. Abra o arquivo *UserRepository.java* em um editor de texto e adicione as seguintes linhas ao arquivo para definir uma interface de repositório do usuário que estende a interface do repositório do DocumentDB:

   ```java
   package com.example.wingtiptoysdata;

   import com.microsoft.azure.spring.data.cosmosdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { }
   ```

1. Salve e feche o arquivo *UserRepository.java*.

### <a name="modify-the-main-application-class"></a>Modificar a classe principal do aplicativo

1. Localize o arquivo Java principal do aplicativo no diretório do pacote do aplicativo, por exemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localize o arquivo Java do aplicativo][JV01]

1. Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:

   ```java
    package com.example.wingtiptoysdata;

    import org.springframework.boot.CommandLineRunner;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    import java.util.Optional;
    import java.util.UUID;

    @SpringBootApplication
    public class WingtiptoysdataApplication implements CommandLineRunner {

        private final UserRepository repository;

        public WingtiptoysdataApplication(UserRepository repository) {
            this.repository = repository;
        }

        public static void main(String[] args) {
            // Execute the command line runner.
            SpringApplication.run(WingtiptoysdataApplication.class, args);
            System.exit(0);
        }

        public void run(String... args) throws Exception {
            // Create a unique identifier.
            String uuid = UUID.randomUUID().toString();

            // Create a new User class.
            final User testUser = new User(uuid, "John", "Doe");

            // For this example, remove all of the existing records.
            repository.deleteAll();

            // Save the User class to the Azure database.
            repository.save(testUser);

            // Retrieve the database record for the User class you just saved by ID.
            Optional<User> result = repository.findById(testUser.getId());

            // Display the results of the database record retrieval.
            System.out.println("\nSaved user is: " + result + "\n")
        }
    }
   ```

1. Salve e feche o arquivo Java do aplicativo principal.

## <a name="build-and-test-your-app"></a>Crie e testar seu aplicativo

1. Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:

   `cd C:\SpringBoot\wingtiptoysdata`

   -ou-

   `cd /users/example/home/wingtiptoysdata`

1. Compile o aplicativo Spring Boot com Maven e execute-o, por exemplo:

   ```shell
   mvnw clean spring-boot:run
   ```

1. Seu aplicativo exibirá várias mensagens de execução e mostrará uma mensagem, como os exemplos a seguir, para indicar que os valores foram armazenados e recuperados com êxito no banco de dados.

   ```shell
   Saved user is: Optional[User: 24093cb5-55fe-4d2c-b459-cb8bafdd39fe John Doe]
   ```

   ![Saída bem-sucedida do aplicativo][JV02]

1. OPCIONAL: você pode usar o portal do Azure para exibir o conteúdo do Azure Cosmos DB na página de propriedades do seu banco de dados. Basta clicar em **Data Explorer** e selecionar um item na lista para exibir o conteúdo.

   ![Como usar o Gerenciador de Documentos para exibir seus dados][JV03]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.

> [!div class="nextstepaction"]
> [Spring no Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionais

Para obter mais informações sobre como usar o Azure Cosmos DB e Java, consulte os seguintes artigos:

* [Documentação do Azure Cosmos DB].

* [Banco de dados do Azure Cosmos DB: Criar um banco de dados de documentos usando o Java e o Portal do Microsoft Azure][Build a SQL API app with Java]

* [Spring Data para a API do SQL do Azure Cosmos DB]

Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:

* [Iniciador Spring Boot do Cosmos DB para Azure]

* [Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].

O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos. Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>. Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.

<!-- URL List -->

[Documentação do Azure Cosmos DB]: /azure/cosmos-db/
[Azure para desenvolvedores Java]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data para a API do SQL do Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Iniciador Spring Boot do Cosmos DB para Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Como trabalhar com o Java e o Azure DevOps]: https://azure.microsoft.com/services/devops/java/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
