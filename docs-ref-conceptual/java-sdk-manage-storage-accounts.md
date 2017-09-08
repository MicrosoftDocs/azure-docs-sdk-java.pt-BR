---
title: Gerenciar contas de armazenamento do Azure com Java | Microsoft Docs
description: "Exemplo de código para gerenciar as contas de armazenamento do Azure usando o SDK do Azure para Java"
author: rloutlaw
manager: douge
ms.assetid: 49be8b66-3b56-4c10-8f14-9d326d815cb4
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 5945164b2b04e1fa9169590a71f6c5f9f45842d6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a><span data-ttu-id="f58e1-103">Gerenciar contas de armazenamento do Azure a partir dos seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="f58e1-103">Manage Azure storage accounts from your Java applications</span></span>

<span data-ttu-id="f58e1-104">[Este exemplo](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) cria uma conta de [Armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-introduction) e funciona com as chaves de acesso da conta usando as [bibliotecas de gerenciamento de Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="f58e1-104">[This sample](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) creates an [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) account and works with the account access keys using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="f58e1-105">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="f58e1-105">Run the sample</span></span>

<span data-ttu-id="f58e1-106">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f58e1-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="f58e1-107">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="f58e1-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

<span data-ttu-id="f58e1-108">Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="f58e1-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="f58e1-109">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="f58e1-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a><span data-ttu-id="f58e1-110">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f58e1-110">Create a storage account</span></span>

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

<span data-ttu-id="f58e1-111">O nome de armazenamento fornecido deve ser exclusivo entre todos os nomes no Azure e conter apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="f58e1-111">The storage name provided must be unique across all names in Azure and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="f58e1-112">O perfil de desempenho e replicação padrão usado para essa conta é [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="f58e1-112">The default performance and replication profile used for this account is [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span></span>

## <a name="list-keys-in-a-storage-account"></a><span data-ttu-id="f58e1-113">Listar chaves em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f58e1-113">List keys in a storage account</span></span>
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

<span data-ttu-id="f58e1-114">Duas chaves são fornecidas em cada conta de armazenamento do Azure para que você possa regenerar uma chave e ainda permitir acesso ao armazenamento usando a outra chave.</span><span class="sxs-lookup"><span data-stu-id="f58e1-114">Two keys are provided in each Azure storage account so that you can regenerate one key while still allowing access to storage using the other key.</span></span>

## <a name="regenerate-a-key-in-a-storage-account"></a><span data-ttu-id="f58e1-115">Regenerar uma chave em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f58e1-115">Regenerate a key in a storage account</span></span>

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

<span data-ttu-id="f58e1-116">Depois de gerar um novo, você deve atualizar todos os aplicativos e recursos do Azure com a nova chave.</span><span class="sxs-lookup"><span data-stu-id="f58e1-116">You must update all Azure resources and applications with the new key after generating a new one.</span></span>

## <a name="list-all-storage-accounts-in-a-resource-group"></a><span data-ttu-id="f58e1-117">Listar todas as contas de armazenamento em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f58e1-117">List all storage accounts in a resource group</span></span>
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

<span data-ttu-id="f58e1-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) fornece um conjunto de métodos úteis para inspecionar a configuração de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f58e1-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) provides a set of useful methods to inspect the configuration of a storage account.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="f58e1-119">Excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f58e1-119">Delete a storage account</span></span>
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> <span data-ttu-id="f58e1-120">Contas de armazenamento com imagens de disco em uso conectadas a máquinas virtuais ou discos em uso por outros artefatos não podem remover esses métodos.</span><span class="sxs-lookup"><span data-stu-id="f58e1-120">Storage accounts with in-use disk images connected to virtual machines or disks in use by other artifacts may not remove with these methods.</span></span> <span data-ttu-id="f58e1-121">Desanexe o armazenamento desses recursos antes de remover a conta.</span><span class="sxs-lookup"><span data-stu-id="f58e1-121">Detach the storage from these resources before removing the account.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="f58e1-122">Explicação do exemplo</span><span class="sxs-lookup"><span data-stu-id="f58e1-122">Sample explanation</span></span>

<span data-ttu-id="f58e1-123">[Exemplo de código no GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span><span class="sxs-lookup"><span data-stu-id="f58e1-123">[The sample code on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span></span>

- <span data-ttu-id="f58e1-124">cria uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f58e1-124">creates a storage account</span></span>
- <span data-ttu-id="f58e1-125">lê e regenera as chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="f58e1-125">reads and regenerates access keys</span></span>
- <span data-ttu-id="f58e1-126">lista todas as contas de armazenamento em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f58e1-126">lists all storage accounts in a resource group</span></span>
- <span data-ttu-id="f58e1-127">elimina a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f58e1-127">deletes the storage account</span></span> 

| <span data-ttu-id="f58e1-128">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="f58e1-128">Class used in sample</span></span> | <span data-ttu-id="f58e1-129">Observações</span><span class="sxs-lookup"><span data-stu-id="f58e1-129">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="f58e1-130">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="f58e1-130">StorageAccount</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | <span data-ttu-id="f58e1-131">Representação de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f58e1-131">Representation of an Azure storage account.</span></span> <span data-ttu-id="f58e1-132">Use os métodos na classe para obter informações sobre a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f58e1-132">Use the methods in the class to get information about the storage account.</span></span>
| [<span data-ttu-id="f58e1-133">StorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="f58e1-133">StorageAccountKey</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | <span data-ttu-id="f58e1-134">`StorageAccount.getKeys()` retorna as chaves da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f58e1-134">`StorageAccount.getKeys()` returns the storage account keys.</span></span> <span data-ttu-id="f58e1-135">Use os métodos `regenerateKey` em `StorageAccount` para atualizar as chaves.</span><span class="sxs-lookup"><span data-stu-id="f58e1-135">Use the `regenerateKey` methods in `StorageAccount` to update the keys.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f58e1-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f58e1-136">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]