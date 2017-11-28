---
title: "Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu Azure SDK dla środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pracować z konta usługi Data Lake Store i system plików za pomocą środowiska Node.js."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="1d233-103">Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu Azure SDK dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="1d233-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d233-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1d233-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1d233-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d233-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1d233-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1d233-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1d233-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="1d233-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1d233-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="1d233-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1d233-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1d233-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1d233-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d233-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1d233-111">Python</span><span class="sxs-lookup"><span data-stu-id="1d233-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="1d233-112">Przekazywanie i pobieranie dużej ilości danych (duże pliki, dużą liczbę plików lub oba), zaleca się używanie [zestaw SDK Python](data-lake-store-get-started-python.md), [zestawu .NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), lub [programu Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1d233-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="1d233-113">Te opcje cechują się lepszą wydajnością, ponieważ umożliwiają równoległe przenoszenie danych dzięki użyciu wielu wątków.</span><span class="sxs-lookup"><span data-stu-id="1d233-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="1d233-114">Dowiedz się, jak używać zestawu Azure SDK dla środowiska Node.js, aby utworzyć konto usługi Azure Data Lake Store i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d233-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="1d233-115">Obecnie zestaw SDK obsługuje</span><span class="sxs-lookup"><span data-stu-id="1d233-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="1d233-116">**Środowisko Node.js w wersji 0.10.0 lub wyższej**</span><span class="sxs-lookup"><span data-stu-id="1d233-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="1d233-117">**Wersja interfejsu API REST dla konta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="1d233-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="1d233-118">**Wersja interfejsu API REST dla systemu plików: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="1d233-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d233-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1d233-119">Prerequisites</span></span>
<span data-ttu-id="1d233-120">Przed rozpoczęciem korzystania z informacji zawartych w tym artykule należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="1d233-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="1d233-121">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d233-121">**An Azure subscription**.</span></span> <span data-ttu-id="1d233-122">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d233-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1d233-123">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d233-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1d233-124">Za pomocą aplikacji usługi Azure AD można uwierzytelnić aplikację usługi Data Lake Store w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d233-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1d233-125">Istnieją różne metody uwierzytelniania w usłudze Azure AD: **uwierzytelnianie użytkowników końcowych** i **uwierzytelnianie między usługami**.</span><span class="sxs-lookup"><span data-stu-id="1d233-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1d233-126">Instrukcje i dodatkowe informacje na temat uwierzytelniania można znaleźć w następujących artykułach: [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) (Uwierzytelnianie użytkowników końcowych) lub [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md) (Uwierzytelnianie między usługami).</span><span class="sxs-lookup"><span data-stu-id="1d233-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="1d233-127">Jak zainstalować</span><span class="sxs-lookup"><span data-stu-id="1d233-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="1d233-128">Uwierzytelnianie za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d233-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="1d233-129">Poniższe fragmenty kodu przedstawiono dwa oddzielne sposoby uwierzytelniania z usługą Data Lake Store za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d233-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="1d233-130">Szczegółowe omówienie różnych metod do użycia na potrzeby uwierzytelniania za pomocą usługi Data Lake Store, zobacz [Uwierzytelnij z usługą Data Lake Store za pomocą usługi Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1d233-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="1d233-131">Poniższy fragment wymaga danych wejściowych, takie jak nazwa domeny usługi Azure AD, identyfikator klienta aplikacji usługi Azure AD itp. Te informacje mogą być pobierane z usługi Azure AD aplikacji, która należy utworzyć, szczegółowe informacje, które znajdują się również w łącze powyżej.</span><span class="sxs-lookup"><span data-stu-id="1d233-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="1d233-132">Utwórz klientów usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1d233-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1d233-133">Utwórz konto usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1d233-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="1d233-134">Utwórz plik z zawartością</span><span class="sxs-lookup"><span data-stu-id="1d233-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="1d233-135">Pobierz listę plików i folderów</span><span class="sxs-lookup"><span data-stu-id="1d233-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="1d233-136">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1d233-136">See also</span></span>
* [<span data-ttu-id="1d233-137">Zestaw Microsoft Azure SDK dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="1d233-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="1d233-138">Zestaw Microsoft Azure SDK for Node.js — Data Lake Analytics zarządzania</span><span class="sxs-lookup"><span data-stu-id="1d233-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

