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
---
# <a name="azure-application-insights-libraries-for-java"></a><span data-ttu-id="4bc74-104">Bibliotecas do Azure Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="4bc74-104">Azure Application Insights libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="4bc74-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4bc74-105">Overview</span></span>

<span data-ttu-id="4bc74-106">Detectar, fazer triagem e diagnosticar problemas em seus serviços e aplicativos Web com o [Application Insights](/azure/application-insights/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="4bc74-106">Detect, triage, and diagnose issues in your web apps and services with [Application Insights](/azure/application-insights/app-insights-overview).</span></span>

<span data-ttu-id="4bc74-107">Para começar a usar o Application Insights, consulte [Introdução ao Application Insights em um projeto Web Java](/azure/application-insights/app-insights-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="4bc74-107">To get started with Application Insights, see [Get started with Application Insights in a Java web project](/azure/application-insights/app-insights-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="4bc74-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="4bc74-108">Client library</span></span>

<span data-ttu-id="4bc74-109">Adicionar telemetria para acompanhar eventos, exceções e métricas de usuário em seus aplicativos com a biblioteca de cliente do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4bc74-109">Add telemetry to track events, exceptions, and user metrics in your apps with the Application Insights client library.</span></span>

<span data-ttu-id="4bc74-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="4bc74-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="4bc74-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4bc74-111">Example</span></span>

<span data-ttu-id="4bc74-112">Criar uma nova entrada de métrica e registrar um valor para ela.</span><span class="sxs-lookup"><span data-stu-id="4bc74-112">Create a new metric entry and record a value for it.</span></span>

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4bc74-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="4bc74-113">Explore the Client APIs</span></span>](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a><span data-ttu-id="4bc74-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4bc74-114">Samples</span></span>

<span data-ttu-id="4bc74-115">Explorar mais [exemplos de código Java para o Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4bc74-115">Explore more [sample Java code for Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) you can use in your apps.</span></span>
