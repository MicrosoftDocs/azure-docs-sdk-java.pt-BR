---
title: Bibliotecas do Azure Application Insights para Java
description: Documentação de referência para a API de gerenciamento de Java para o Azure Application Insights
keywords: Azure, Java, SDK, API, AppInsights, telemetria, diagnósticos, rastreamento, logs, desempenho
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appinsights
ms.openlocfilehash: d881ff66ad806e13f7d2cbafff6ce85c23240304
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823759"
---
# <a name="azure-application-insights-libraries-for-java"></a>Bibliotecas do Azure Application Insights para Java

## <a name="overview"></a>Visão geral

Detectar, fazer triagem e diagnosticar problemas em seus serviços e aplicativos Web com o [Application Insights](/azure/application-insights/app-insights-overview).

Para começar a usar o Application Insights, consulte [Introdução ao Application Insights em um projeto Web Java](/azure/application-insights/app-insights-java-get-started).

## <a name="client-library"></a>Biblioteca do cliente

Adicionar telemetria para acompanhar eventos, exceções e métricas de usuário em seus aplicativos com a biblioteca de cliente do Application Insights.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Criar uma nova entrada de métrica e registrar um valor para ela.

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [Explorar as APIs de cliente](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a>Exemplos

Explorar mais [exemplos de código Java para o Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) que você pode usar em seus aplicativos.
