---
title: Bibliotecas do Azure Data Lake Store para Java
description: Documentação de referência para as bibliotecas do Data Lake Store de Java
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
ms.openlocfilehash: bcd1fd17759f7d171006d7b2126019d00d06d1db
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823719"
---
# <a name="azure-data-lake-store-libraries-for-java"></a><span data-ttu-id="93274-104">Bibliotecas do Azure Data Lake Store para Java</span><span class="sxs-lookup"><span data-stu-id="93274-104">Azure Data Lake Store libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="93274-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="93274-105">Overview</span></span>

<span data-ttu-id="93274-106">Capturar dados de qualquer tamanho, tipo e velocidade de ingestão em um único local para análise com o [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="93274-106">Capture data of any size, type, and ingestion speed in a single place for analytics with [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="93274-107">Para começar a usar o Azure Data Lake Store, consulte [Introdução ao Azure Data Lake Store usando Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="93274-107">To get started with Data Lake Store, see [Get started with Azure Data Lake Store using Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span></span>


## <a name="client-library"></a><span data-ttu-id="93274-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="93274-108">Client library</span></span>

<span data-ttu-id="93274-109">Ler e gravar arquivos, definir permissões e metadados e gerenciar arquivos e diretórios no Data Lake Store com a biblioteca do cliente.</span><span class="sxs-lookup"><span data-stu-id="93274-109">Read and write files, set permissions and metadata, and manage files and directories in Data Lake Store with the client library.</span></span>

<span data-ttu-id="93274-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="93274-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="93274-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="93274-111">Example</span></span>

<span data-ttu-id="93274-112">Criar um cliente do Data Lake a partir de um nome de domínio totalmente qualificado e um token de acesso OAuth2, em seguida, crie um arquivo no Data Lake e grave nele.</span><span class="sxs-lookup"><span data-stu-id="93274-112">Create a Data Lake client from a fully qualified domain name and OAuth2 access token, then create a file in Data Lake and write to it.</span></span>

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
> [<span data-ttu-id="93274-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="93274-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a><span data-ttu-id="93274-114">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="93274-114">Management API</span></span>

<span data-ttu-id="93274-115">Use a API de gerenciamento para gerenciar provedores de identidade confiável, regras de firewall e contas do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="93274-115">Use the management API to manage Data Lake Store accounts, firewall rules, and trusted identity providers.</span></span>

<span data-ttu-id="93274-116">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="93274-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="93274-117">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="93274-117">Explore the Management APIs</span></span>](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="93274-118">Exemplos</span><span class="sxs-lookup"><span data-stu-id="93274-118">Samples</span></span>

<span data-ttu-id="93274-119">[Introdução ao Azure Data Lake][1]</span><span class="sxs-lookup"><span data-stu-id="93274-119">[Azure Data Lake Get Started][1]</span></span> 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

<span data-ttu-id="93274-120">Explore mais [exemplos de código Java para o Banco de Dados do Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="93274-120">Explore more [sample Java code for Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) you can use in your apps.</span></span>
