---
title: Adicionar um certificado raiz do Azure ao repositório CA de Java
description: Saiba como adicionar um certificado raiz de CA (autoridade de certificação) para o repositório de certificado CA (cacerts) de Java para uso com o Microsoft Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 07/02/2018
ms.author: robmcm
ms.openlocfilehash: 3f2de63f7eb1422ff1dd6db45d68e02f4af188b8
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37864036"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="0fc76-103">Adicionar um certificado raiz ao repositório de certificados CA de Java</span><span class="sxs-lookup"><span data-stu-id="0fc76-103">Adding a root certificate to the Java CA certificates store</span></span>

<span data-ttu-id="0fc76-104">Aplicativos que usam os serviços do Azure (por exemplo, o Barramento de Serviço do Azure) precisam confiar no certificado raiz de Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="0fc76-104">Applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="0fc76-105">Talvez esse certificado já esteja instalado em seu sistema, mas se não estiver, as etapas neste tutorial mostrarão como usar o **keytool** da Oracle para adicionar o certificado raiz da autoridade de certificação (CA) necessário para o repositório de certificados de Java (cacerts) que você usará para os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc76-105">This certificate may already be installed on your system, but if it is not, the steps in this tutorial will show you how to use Oracle's **keytool** to add the required certificate authority (CA) root certificate to the Java CA certificate (cacerts) store that you will use for Azure services.</span></span>

<span data-ttu-id="0fc76-106">O utilitário de keytool da Oracle é uma _Ferramenta de gerenciamento de certificado e chave_ que permite aos desenvolvedores gerenciar a lista de certificados confiáveis para uso com Java.</span><span class="sxs-lookup"><span data-stu-id="0fc76-106">Oracle's keytool utility is a _Key and Certificate Management Tool_, which allows developers to manage the list of trusted certificates for use with Java.</span></span> <span data-ttu-id="0fc76-107">Você pode usar o keytool para adicionar o certificado de autoridade de certificação antes de compactar seu JDK e adicionar a sua pasta **approot** do projeto do Azure ou executar uma tarefa de inicialização do Azure que usa keytool para adicionar o certificado.</span><span class="sxs-lookup"><span data-stu-id="0fc76-107">You can use keytool to add the CA certificate before zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span>

<span data-ttu-id="0fc76-108">A partir de 15 de abril de 2013, o Azure começou a migrar do certificado raiz GTE CyberTrust Global para o certificado raiz Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="0fc76-108">Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global root certificate to the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="0fc76-109">As etapas a seguir mostram como usar o keytool para adicionar o certificado raiz Baltimore CyberTrust ao repositório de certificados de CA (cacerts) para Java.</span><span class="sxs-lookup"><span data-stu-id="0fc76-109">The following steps show you how to use keytool to add the Baltimore CyberTrust root certificate to your Java CA certificate (cacerts) store.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="0fc76-110">Use as etapas neste artigo para configurar o SDK do Java para confiar nos certificados raiz de outras autoridades de certificação confiáveis.</span><span class="sxs-lookup"><span data-stu-id="0fc76-110">You can use the steps in this article to configure your Java SDK to trust the root certificates from other trusted certificate authorities.</span></span> <span data-ttu-id="0fc76-111">Por exemplo, você pode optar por um certificado raiz da lista de certificados em [Certificados raiz da GeoTrust](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="0fc76-111">For example, you might choose a root certificate from the list of certificates at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span>
> 

## <a name="determining-which-root-certificates-are-installed"></a><span data-ttu-id="0fc76-112">Determinar quais certificados raiz estão instalados</span><span class="sxs-lookup"><span data-stu-id="0fc76-112">Determining which root certificates are installed</span></span>

<span data-ttu-id="0fc76-113">O certificado Baltimore já pode estar instalado em seu repositório cacerts, portanto, você precisará usar as etapas a seguir para determinar se ele já foi instalado.</span><span class="sxs-lookup"><span data-stu-id="0fc76-113">The Baltimore certificate might already be installed in your cacerts store, so you need to use the following steps to determine if it has already been installed.</span></span>

1. <span data-ttu-id="0fc76-114">Em um prompt de comando de administrador, navegue até a pasta **jdk\jre\lib\security** de seu JDK e execute o seguinte comando para listar os certificados que estão instalados em seu sistema:</span><span class="sxs-lookup"><span data-stu-id="0fc76-114">At an administrator command prompt, navigate to your JDK's **jdk\jre\lib\security** folder, and then run the following command to list the certificates that are installed on your system:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

1. <span data-ttu-id="0fc76-115">Se você receber uma solicitação para a senha do repositório, a senha padrão será **changeit**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-115">If you are prompted for the store password, the default password is **changeit**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="0fc76-116">Se você quiser alterar a senha do repositório, confira a documentação do keytool em <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="0fc76-116">If you want to change the store password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>
   > 

1. <span data-ttu-id="0fc76-117">Se você não vir o certificado com a impressão digital do `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use as etapas na seção a seguir para baixar e instalar o certificado.</span><span class="sxs-lookup"><span data-stu-id="0fc76-117">If you do not see the certificate with the thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use the steps in the following section to download and install the certificate.</span></span>

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a><span data-ttu-id="0fc76-118">Para adicionar um certificado raiz ao repositório cacerts</span><span class="sxs-lookup"><span data-stu-id="0fc76-118">To add a root certificate to the cacerts store</span></span>

1. <span data-ttu-id="0fc76-119">Baixe o certificado raiz Baltimore CyberTrust em <https://cacert.omniroot.com/bc2025.crt> e salve em um arquivo local com a extensão **.cer** em sua pasta **jdk\jre\lib\security**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-119">Download the Baltimore CyberTrust root certificate from <https://cacert.omniroot.com/bc2025.crt>, and save to a local file with extension **.cer** in your **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="0fc76-120">Para este exemplo, vamos supor que você baixou o arquivo do certificado raiz do Baltimore CyberTrust como **bc2025.cer**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-120">For this example, assume that you downloaded the Baltimore CyberTrust root certificate file as **bc2025.cer**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="0fc76-121">O certificado raiz Baltimore CyberTrust tem um número de série `02:00:00:b9` e uma impressão digital SHA1 de `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span><span class="sxs-lookup"><span data-stu-id="0fc76-121">The Baltimore CyberTrust root certificate has a serial number of `02:00:00:b9`, and a SHA1 thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span></span>
   > 

2. <span data-ttu-id="0fc76-122">Importe o certificado para o repositório cacerts usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0fc76-122">Import the certificate to the cacerts store by using the following command:</span></span>

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   <span data-ttu-id="0fc76-123">Em que:</span><span class="sxs-lookup"><span data-stu-id="0fc76-123">Where:</span></span>

   |  <span data-ttu-id="0fc76-124">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0fc76-124">Parameter</span></span>   |                              <span data-ttu-id="0fc76-125">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="0fc76-125">Description</span></span>                               |
   |--------------|------------------------------------------------------------------------|
   | `keystore`   | <span data-ttu-id="0fc76-126">Especifica o repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="0fc76-126">Specifies the certificate store.</span></span>                                       |
   | `importcert` | <span data-ttu-id="0fc76-127">Especifica que você está importando um certificado.</span><span class="sxs-lookup"><span data-stu-id="0fc76-127">Specifies that you are importing a certificate.</span></span>                        |
   | `alias`      | <span data-ttu-id="0fc76-128">Especifica um alias para o certificado.</span><span class="sxs-lookup"><span data-stu-id="0fc76-128">Specifies an alias for the certificate.</span></span>                                |
   | `file`       | <span data-ttu-id="0fc76-129">Especifica o nome do arquivo do certificado raiz que você está importando.</span><span class="sxs-lookup"><span data-stu-id="0fc76-129">Specifies the filename of the root certificate that you are importing.</span></span> |


3. <span data-ttu-id="0fc76-130">Se você receber uma solicitação para confiar no certificado, verifique a impressão digital como `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` e digite **y** se a impressão digital estiver correta.</span><span class="sxs-lookup"><span data-stu-id="0fc76-130">If you are prompted to trust the certificate, verify the thumbprint as `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, and type **y** if the thumbprint is correct.</span></span>

4. <span data-ttu-id="0fc76-131">Execute o seguinte comando para garantir que o certificado de CA foi importado com êxito:</span><span class="sxs-lookup"><span data-stu-id="0fc76-131">Run the following command to ensure the CA certificate has been successfully imported:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

<span data-ttu-id="0fc76-132">Após adicionar com êxito o certificado raiz ao seu JDK, compacte o conteúdo do JDK e adicione-o à pasta **approot** do projeto do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc76-132">After you have successfully added the root certificate to your JDK, you can zip the contents of JDK and add it to your Azure project's **approot** folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc76-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fc76-133">Next steps</span></span>

<span data-ttu-id="0fc76-134">Para saber mais sobre o utilitário keytool, confira <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="0fc76-134">For more information about the keytool utility, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

<span data-ttu-id="0fc76-135">Para saber mais sobre Java, veja [Centro de desenvolvedores do Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="0fc76-135">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

<!-- For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx). -->
