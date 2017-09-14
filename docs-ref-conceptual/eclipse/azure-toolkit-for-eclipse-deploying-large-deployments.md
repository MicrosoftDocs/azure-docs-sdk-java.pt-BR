---
title: "Implantando Grandes Implantações"
description: "Saiba como implantar implantações grandes do Azure usando o Kit de Ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="48524-103">Implantando Grandes Implantações</span><span class="sxs-lookup"><span data-stu-id="48524-103">Deploying Large Deployments</span></span>

<span data-ttu-id="48524-104">Se sua implantação for muito grande para caber na pasta approot padrão, você pode usar um recurso de armazenamento local como a pasta raiz de implantação para seu JDK e servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="48524-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="48524-105">Para usar um recurso de armazenamento local como pasta raiz de implantação para grandes implantações</span><span class="sxs-lookup"><span data-stu-id="48524-105">To use a local storage resource as the deployment root folder for large deployments</span></span>

1. <span data-ttu-id="48524-106">Crie um recurso de armazenamento local novo.</span><span class="sxs-lookup"><span data-stu-id="48524-106">Create a new local storage resource.</span></span> <span data-ttu-id="48524-107">O nome do recurso não importa.</span><span class="sxs-lookup"><span data-stu-id="48524-107">The name of the resource does not matter.</span></span> <span data-ttu-id="48524-108">Os recursos de armazenamento são definidos no nível de função.</span><span class="sxs-lookup"><span data-stu-id="48524-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="48524-109">É a maneira mais rápida para acessar a caixa de diálogo de configuração de armazenamento local, da qual você pode criar um novo recurso de armazenamento local usando as etapas a seguir: Clique com o botão direito na função da exibição do **Explorador de Projeto** (expanda o nó do projeto do Azure se não vir a função), clique em **Azure**, e, em seguida, clique em **Armazenamento Local**.</span><span class="sxs-lookup"><span data-stu-id="48524-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="48524-110">Dentro da caixa de diálogo **Armazenamento Local**, clique em **Adicionar** para criar um novo recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="48524-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

1. <span data-ttu-id="48524-111">Defina o tamanho desejado para pelo menos 2048 MB (algo menor pode causar os mesmos problemas de tamanho de arquivo como haveria na approot).</span><span class="sxs-lookup"><span data-stu-id="48524-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

1. <span data-ttu-id="48524-112">A caixa **Limpar o conteúdo quando a instância de função é reciclada** deve estar marcada; isso ajudará a evitar que a lógica de inicialização da implantação seja executada em conflito com os arquivos pré-existentes no recurso quando a instância de função é reciclada.</span><span class="sxs-lookup"><span data-stu-id="48524-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

1. <span data-ttu-id="48524-113">O valor de **Variável de ambiente armazenando o caminho do diretório do recurso após a implantação** deve estar definido como a cadeia de caracteres **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="48524-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="48524-114">A caixa de diálogo de recurso de armazenamento local será semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="48524-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="48524-115">Como alternativa, se você usar **DEPLOYROOT** como o *nome* de seu recurso local e não alterar o nome da variável de ambiente gerado automaticamente (que, nesse caso, será definido como **DEPLOYROOT_PATH**), isso funcionaria para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48524-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="48524-116">Informações adicionais sobre como criar um recurso de armazenamento local podem ser encontradas em [Propriedades de armazenamento local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="48524-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="next-steps"></a><span data-ttu-id="48524-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48524-117">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
