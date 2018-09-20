---
title: Como usar o Iniciador do Spring Data Gremlin com a API SQL do Azure Cosmos DB
description: Saiba como configurar um aplicativo criado com o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 3e7ec1a2f6b15ec9444dc6ee8d8f2d0f779b1f10
ms.sourcegitcommit: e017de4677c5bedd6ef88c8c1b6da279dc973efe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2018
ms.locfileid: "45639789"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a>Como usar o Iniciador do Spring Data Gremlin com a API SQL do Azure Cosmos DB

## <a name="overview"></a>Visão geral

O Iniciador do Spring Data Gremlin fornece suporte ao Spring Data para a linguagem de consulta Gremlin do Apache, que os desenvolvedores podem usar com qualquer armazenamento de dados compatíveis com Gremlin.

Este artigo demonstra como criar um Azure Cosmos DB usando o portal do Azure para uso com a API do Gremlin. Depois, como usar o **[Spring Initializr]** para criar um aplicativo Java personalizado e, em seguida, como adicionar a funcionalidade de Iniciador do Spring Data Gremlin ao seu aplicativo personalizado para armazenar e recuperar dados de seu Azure Cosmos DB usando Gremlin.

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].
* Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

> [!IMPORTANT]
>
> É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a>Criar um Azure Cosmos DB usando o portal do Azure

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a>Criar seu Azure Cosmos DB para uso com a API do Gremlin

1. Navegue até o Portal do Azure em <https://portal.azure.com/> e clique em **+Criar um recurso**.

   ![Criar um recurso][AZ01]

1. Clique em **Bancos de Dados** e, em seguida, clique em **Azure Cosmos DB**.

   ![Criar Azure Cosmos DB][AZ02]

1. Na página **Azure Cosmos DB**, insira as seguintes informações:

   * Insira uma **ID** exclusiva, que você usará como parte do URI do Gremlin para o banco de dados. Por exemplo: se você inseriu **wingtiptoysdata** para a **ID**, o URI do Gremlin deve ser *wingtiptoysdata.gremlin.cosmosdb.azure.com*.
   * Escolha **Gremlin (Grafo)** para a API.
   * Escolha a **Assinatura** você deseja usar para seu banco de dados.
   * Especifique se deseja criar um novo **Grupo de recursos** para seu banco de dados ou escolher um grupo de recursos existente.
   * Especifique o **Local** para seu banco de dados.
   
   Quando você tiver especificado essas opções, clique em **Criar** para criar o banco de dados.

   ![Especificar as opções do Azure Cosmos DB][AZ03]

1. Quando seu banco de dados for criado, ele será listado no seu **Painel** do Azure, bem como nas páginas **Todos os Recursos** e **Azure Cosmos DB**. Você pode clicar no banco de dados em qualquer um desses locais para abrir a página de propriedades do seu cache.

   ![Todos os Recursos][AZ04]

1. Quando a página de propriedades para o banco de dados for exibida, clique em **Chaves de acesso** e copie o URI e as chaves de acesso para seu banco de dados. Você usará esses valores em seu aplicativo Spring Boot.

   ![Chaves de acesso][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a>Adicionar um grafo ao seu Azure Cosmos DB

1. Clique em **Data Explorer** e em **Novo Graph**.

   ![Novo grafo][AZ06]

1. Quando a página **Adicionar Graph** for exibida, insira as seguintes informações:

   * Especifique uma **ID de banco de dados** exclusiva para seu banco de dados.
   * Especifique uma **ID do Graph** exclusiva para seu grafo.
   * Você pode optar por especificar sua **Capacidade de armazenamento** ou pode aceitar a opção padrão.
   * Especifique sua **Produtividade**, e para este exemplo, você pode escolher 400 Unidades de Solicitação (RUs).
   
   Quando você tiver especificado essas opções, clique em **OK** para criar o grafo.

   ![Adicionar Graph][AZ07]

1. Após a criação do grafo, você pode usar o **Data Explorer** para visualizá-lo.

   ![Exibição das propriedades do Graph][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Criar um aplicativo Spring Boot simples com o Spring Initializr

1. Navegue até <https://start.spring.io/>.

1. Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para seu aplicativo, especifique a versão do **Spring Boot** com uma versão que seja igual ou superior a 2.0 e, em seguida, clique em **Gerar Projeto**.

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote; por exemplo: *com.example.wintiptoysdata.
   >

1. Quando solicitado, baixe o projeto para um caminho no computador local.

   ![Baixe o projeto personalizado do Spring Boot][SI02]

1. Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.

   ![Arquivos de projeto Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a>Configure seu aplicativo Spring Boot para usar o Iniciador do Spring Data Gremlin

1. Localize o arquivo *pom.xml* no diretório do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   -ou-

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Salve o arquivo pom.xml][PM01]

1. Abra o arquivo *pom.xml* em um editor de texto e adicione o Iniciador do Spring Data Gremlin à lista de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Edição do arquivo pom.xml][PM02]

1. Salve e feche o arquivo *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Configure seu aplicativo Spring Boot para usar seu Azure Cosmos DB

1. Localize o diretório *resources* do seu aplicativo, e crie um novo arquivo chamado *application.yml*. Por exemplo: 

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Criar o arquivo application.yml][RE01]

1.  Abra o arquivo *application.yml* em um editor de texto e adicione as seguintes linhas ao arquivo, e substitua os valores de exemplo pelas propriedades adequadas para o seu banco de dados:

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   
   Em que:
   
   | Campo | DESCRIÇÃO |
   |---|---|
   | `endpoint` | Especifica o URI do Gremlin para o seu banco de dados, que é derivado da **ID** exclusiva que você especificou ao criar seu Azure Cosmos DB anteriormente no tutorial. |
   | `port` | Especifica a porta TCP/IP, que deve ser **443** para HTTPS. |
   | `username` | Especifica a **ID de banco de dados** e a **ID do Graph** exclusivas usadas ao adicionar o grafo anteriormente. Essa opção deve ser inserida usando a seguinte sintaxe: “/dbs/**{ID do banco de dados}**/colls/**{Id do Graph}**”. |
   | `password` | Especifica a **Chave de acesso** primária ou secundária copiada anteriormente neste tutorial. |
   | `telemetryAllowed` | Especifique **true** se você quiser habilitar a telemetria; caso contrário, **false**.

1. Salve e feche o arquivo *application.yml*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Adicione o código de exemplo para implementar a funcionalidade básica de banco de dados

Nesta seção, você cria as classes Java necessárias para armazenar dados em seu banco de dados.

### <a name="modify-the-main-application-class"></a>Modificar a classe principal do aplicativo

1. Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localize o arquivo Java do aplicativo][JV01]

1. Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. Salve e feche o arquivo Java do aplicativo principal.

### <a name="define-a-basic-class-for-storing-configuration-information"></a>Defina uma classe básica para armazenar informações de configuração

1. Crie uma pasta chamada *config* no diretório package do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. Crie um novo arquivo Java chamado *UserRepositoryConfiguration.java* no diretório *config* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. Salve e feche o arquivo *UserRepositoryConfiguration.java*.

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a>Defina um conjunto de classes que defina os elementos do banco de dados do seu grafo

1. Crie uma pasta chamada *domain* no diretório package do seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. Crie um novo arquivo Java chamado *Person.java* no diretório *domain* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. Salve e feche o arquivo *Person.java*.

1. Crie um novo arquivo Java chamado *Relation.java* no diretório *domain* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. Salve e feche o arquivo *Relation.java*.

1. Crie um novo arquivo Java chamado *Network.java* no diretório *domain* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. Salve e feche o arquivo *Network.java*.

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a>Defina um conjunto de classes que defina os repositórios do banco de dados de seu grafo

1. Crie uma pasta chamada *repository* no diretório package de seu aplicativo; por exemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. Crie um novo arquivo Java chamado *NetworkRepository.java* no diretório *repository* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. Salve e feche o arquivo *NetworkRepository.java*.

1. Crie um novo arquivo Java chamado *PersonRepository.java* no diretório *repository* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. Salve e feche o arquivo *PersonRepository.java*.

1. Crie um novo arquivo Java chamado *RelationRepository.java* no diretório *repository* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. Salve e feche o arquivo *RelationRepository.java*.

## <a name="build-and-test-your-app"></a>Crie e testar seu aplicativo

1. Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:

   `cd C:\SpringBoot\wingtiptoysdata`

   -ou-

   `cd /users/example/home/wingtiptoysdata`

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Seu aplicativo exibirá várias mensagens de tempo de execução e, se houver erros, você poderá usar o portal do Azure para exibir o conteúdo do Azure Cosmos DB. Para fazer isso, clique em **Data Explorer** na página de propriedades do banco de dados. Em seguida, clique em **Executar consulta de Gremlin** e depois selecione um item da lista de resultados para exibir os dados.

   ![Como usar o Gerenciador de Documentos para exibir seus dados][JV03]

## <a name="next-steps"></a>Próximas etapas

Confira estes artigos para obter mais informações sobre o suporte do Azure para Gremlin e API do Graph:

* [Introdução ao Azure Cosmos DB: API do Graph](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [Suporte do Azure Cosmos DB para grafo do Gremlin](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [Azure Cosmos DB: Criar um banco de dados de grafo usando o Java e o portal do Azure](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [Tutorial: Consultar a API do Graph do Azure Cosmos DB usando Gremlin](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* [Iniciador do Spring Data Gremlin]

Para obter mais informações sobre como usar o Azure Cosmos DB e Java, consulte os seguintes artigos:

* [Documentação do Azure Cosmos DB].

* [Azure Cosmos DB: Criar um banco de dados de documento usando o Java e o Portal do Azure][Build a SQL API app with Java]

* [Spring Data para a API do SQL do Azure Cosmos DB]

Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:

* [Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].

O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos. Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>. Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.


<!-- URL List -->

[Documentação do Azure Cosmos DB]: /azure/cosmos-db/
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data para a API do SQL do Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Iniciador do Spring Data Gremlin]: https://github.com/Microsoft/spring-data-gremlin
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
