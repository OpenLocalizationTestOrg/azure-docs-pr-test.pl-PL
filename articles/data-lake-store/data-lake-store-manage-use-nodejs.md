---
title: "aaaGet wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu Azure SDK dla środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toowork Node.js z konta usługi Data Lake Store i hello systemu plików."
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
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu Azure SDK dla środowiska Node.js
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> Przekazywanie i pobieranie dużej ilości danych (duże pliki, dużą liczbę plików lub oba), zaleca się używanie hello [zestaw SDK Python](data-lake-store-get-started-python.md), hello [zestawu .NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), lub [programu Azure PowerShell](data-lake-store-get-started-powershell.md). Te opcje mają lepszą wydajność, ponieważ używają one wiele wątków tooparallelize hello przenoszenia danych.
> 
> 

Dowiedz się, jak toouse hello Azure SDK dla środowiska Node.js toocreate konta usługi Azure Data Lake Store i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md). Obecnie hello zestaw SDK obsługuje

* **Środowisko Node.js w wersji 0.10.0 lub wyższej**
* **Wersja interfejsu API REST dla konta: 2015-10-01-preview**
* **Wersja interfejsu API REST dla systemu plików: 2015-10-01-preview**

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Utworzenie aplikacji usługi Azure Active Directory**. Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD. Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Jak tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Uwierzytelnianie za pomocą usługi Azure Active Directory
Poniższe fragmenty kodu Hello zawierają dwa oddzielne sposoby uwierzytelniania z usługą Data Lake Store za pomocą usługi Azure AD. Szczegółowe omówienie na różnych metod toouse do uwierzytelniania przy użyciu usługi Data Lake Store, zobacz [Uwierzytelnij z usługą Data Lake Store za pomocą usługi Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

Poniższy fragment Hello wymaga danych wejściowych, takie jak nazwa domeny usługi Azure AD, identyfikator klienta aplikacji usługi Azure AD itp. Te informacje mogą być pobierane z aplikacji Azure AD, która należy utworzyć, hello szczegółowe informacje, które znajdują się również w łącze powyżej.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Utwórz hello Data Lake magazynu klientów
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Utwórz konto usługi Data Lake Store
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
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
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a>Utwórz plik z zawartością
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

## <a name="get-a-list-of-files-and-folders"></a>Pobierz listę plików i folderów
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

## <a name="see-also"></a>Zobacz też
* [Zestaw Microsoft Azure SDK dla środowiska Node.js](https://github.com/azure/azure-sdk-for-node)
* [Zestaw Microsoft Azure SDK for Node.js — Data Lake Analytics zarządzania](https://www.npmjs.com/package/azure-arm-datalake-analytics)

