---
title: Bibliotecas do Azure Data Lake Store para Java
description: "Documentação de referência para as bibliotecas do Data Lake Store de Java"
keywords: Azure, Java, SDK, API, big data, data lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 66ff566e74203d3b5a8e9bcc170f4c21cf310645
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-java"></a>Bibliotecas do Azure Data Lake Store para Java

## <a name="overview"></a>Visão geral

Capturar dados de qualquer tamanho, tipo e velocidade de ingestão em um único local para análise com o [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

Para começar a usar o Azure Data Lake Store, consulte [Introdução ao Azure Data Lake Store usando Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).


## <a name="client-library"></a>Biblioteca do cliente

Ler e gravar arquivos, definir permissões e metadados e gerenciar arquivos e diretórios no Data Lake Store com a biblioteca do cliente.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a>Exemplo

Criar um cliente do Data Lake a partir de um nome de domínio totalmente qualificado e um token de acesso OAuth2, em seguida, crie um arquivo no Data Lake e grave nele.

```java
// AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);
ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

// create directory
client.createDirectory("/a/b/w");
        
// create file and write some content
String filename = "/a/b/c.txt";
OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
PrintStream out = new PrintStream(stream);
for (int i = 1; i <= 10; i++) {
    out.println("This is line #" + i);
    out.format("This is the same line (%d), but using formatted output. %n", i);
}
out.close();
```

> [!div class="nextstepaction"]
> [Explorar as APIs de Cliente](/java/api/overview/azure/datalakestore/clientlibrary)


## <a name="management-api"></a>API de Gerenciamento

Use a API de gerenciamento para gerenciar provedores de identidade confiável, regras de firewall e contas do Data Lake Store.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar as APIs de Gerenciamento](/java/api/overview/azure/datalakestore/managementapi)

## <a name="samples"></a>Exemplos

[Introdução ao Azure Data Lake][1] 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

Explore mais [exemplos de código Java para o Banco de Dados do Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) que você pode usar em seus aplicativos.
