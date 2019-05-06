---
title: Exibindo o Conteúdo do Javadoc no Eclipse para o Pacote de Bibliotecas do Azure para Java
description: Como exibir o conteúdo do Javadoc para as Bibliotecas do Azure no Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: bfed1a879bacf82436b71654c0ceca2826381eed
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61590596"
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="c5f05-103">Exibindo o Conteúdo do Javadoc no Eclipse para o Pacote de Bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="c5f05-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>

<span data-ttu-id="c5f05-104">O conteúdo do Javadoc para as bibliotecas do Azure para Java pode ser exibido em seu ambiente do Eclipse associando o conteúdo do Javadoc às bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="c5f05-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="c5f05-105">As etapas a seguir mostram como usar essa funcionalidade no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c5f05-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="c5f05-106">Este procedimento pressupõe que você já adicionou a Biblioteca do Azure para Java ao seu caminho de compilação.</span><span class="sxs-lookup"><span data-stu-id="c5f05-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="c5f05-107">Para exibir o conteúdo do Javadoc no Eclipse para as Bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="c5f05-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>

1. <span data-ttu-id="c5f05-108">No Explorador de projeto do Eclipse, na seção **Bibliotecas Referenciadas** do seu projeto, abra o menu de contexto para a Biblioteca do Azure para Java JAR.</span><span class="sxs-lookup"><span data-stu-id="c5f05-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="c5f05-109">Por exemplo, **microsoft-windowsazure-api-0.1.0.jar** (o número de versão pode ser diferente, dependendo de qual versão você instalou).</span><span class="sxs-lookup"><span data-stu-id="c5f05-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

1. <span data-ttu-id="c5f05-110">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-110">Click **Properties**.</span></span>

1. <span data-ttu-id="c5f05-111">Na caixa de diálogo **Propriedades**, no painel à esquerda, cliquem em **Javadoc Location**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="c5f05-112">A caixa de diálogo **Javadoc local** será exibida.</span><span class="sxs-lookup"><span data-stu-id="c5f05-112">The **Javadoc Location** dialog is displayed.</span></span>

1. <span data-ttu-id="c5f05-113">Você pode especificar uma **URL Javadoc**, ou um **Javadoc no arquivo**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="c5f05-114">Se você optar por especificar uma **URL do Javadoc**, use URLs como **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="c5f05-115">Se optar por usar **Javadoc no arquivo**, você pode especificar um arquivo externo ou um arquivo de workspace.</span><span class="sxs-lookup"><span data-stu-id="c5f05-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="c5f05-116">Faça sua escolha e procure/valide conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="c5f05-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="c5f05-117">O exemplo a seguir associa as Bibliotecas do Azure para Java com o Javadoc JAR correspondente que foi baixado localmente para uma pasta chamada **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![Exiba o conteúdo do Javadoc.][ic553487]

1. <span data-ttu-id="c5f05-119">*Etapa opcional*: Clique em **Validar**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-119">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="c5f05-120">Problemas potenciais com o Javadoc JAR podem ser exibidos aqui.</span><span class="sxs-lookup"><span data-stu-id="c5f05-120">Potential issues with the Javadoc JAR could be displayed here.</span></span>

1. <span data-ttu-id="c5f05-121">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5f05-121">Click **OK**.</span></span>

<span data-ttu-id="c5f05-122">Quando associado à biblioteca, o conteúdo do Javadoc deve exibir seu IDE do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c5f05-122">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="c5f05-123">Por exemplo, se `blob` definido do tipo `CloudBlockBlob` dentro de seu código, o seguinte é um exemplo do conteúdo do Javadoc que aparece quando você digita `blob.acquireLease` no código:</span><span class="sxs-lookup"><span data-stu-id="c5f05-123">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![Exiba o conteúdo do Javadoc.][ic553488]

## <a name="next-steps"></a><span data-ttu-id="c5f05-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5f05-125">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

<!-- IMG List -->

[ic553487]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png
