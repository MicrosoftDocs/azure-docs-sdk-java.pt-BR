---
title: Bibliotecas do Azure Data Lake Analytics para Java
description: Documentação de referência para as bibliotecas do Data Lake Analytics de Java
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
ms.openlocfilehash: c14c89f961951d114362adee4fec6239e78cffb3
ms.sourcegitcommit: 33c70f921f1524c8bdb69ad5a1a3c1b4b1de97ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37026768"
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a>Bibliotecas do Azure Data Lake Analytics para Java

## <a name="overview"></a>Visão geral

Execute trabalhos de análise de big data dimensionados para grandes conjuntos de dados com o [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

Para começar a usar o Azure Data Lake Analytics, veja [Introdução ao Azure Data Lake Analytics com o SDK de Java](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).

## <a name="management-api"></a>API de gerenciamento

Use a API de gerenciamento para gerenciar contas, trabalhos, políticas e catálogos de Data Lake Analytics.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a>Exemplo

Enviar um novo trabalho de U-SQL para o Data Lake Analytics.

```java
// authenticate with service principal credentials
ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
DataLakeAnalyticsJobManagementClient adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);

// set up job parameters
UUID jobId = java.util.UUID.randomUUID();
USqlJobProperties properties = new USqlJobProperties();
properties.setScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();");
JobInformation parameters = new JobInformation();
parameters.setName("testJob");
parameters.setJobId(jobId);
parameters.setType(JobType.USQL);
parameters.setProperties(properties);

// create the job
JobInformation jobInfo = adlaJobClient.getJobOperations().create(accountName, jobId, parameters).getBody();

```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Exemplos

[Azure Data Lake Analytics usando o SDK de Java][1] 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) de exemplos do Azure Data Lake Analytics.
