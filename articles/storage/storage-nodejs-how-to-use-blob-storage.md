---
title: "Jak używać magazynu obiektów Blob w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 38c3fd3cd271c3f9d60c44fff17715062b4979ae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="51446-103">Jak używać Magazynu obiektów Blob w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="51446-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="51446-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="51446-104">Overview</span></span>
<span data-ttu-id="51446-105">W tym artykule przedstawiono sposób wykonywania typowych scenariuszy przy użyciu magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="51446-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="51446-106">Przykłady są napisane przy użyciu interfejsu API środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="51446-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="51446-107">Omówione scenariusze obejmują jak przekazywanie, listy, pobieranie i usuwanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="51446-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="51446-108">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="51446-108">Create a Node.js application</span></span>
<span data-ttu-id="51446-109">Aby uzyskać instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie aplikacji sieci web Node.js w usłudze Azure App Service], [tworzenia i wdrażania aplikacji Node.js do usługi w chmurze platformy Azure] — za pomocą środowiska Windows PowerShell lub [tworzenie i wdrażanie aplikacji sieci web Node.js na platformie Azure przy użyciu Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="51446-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="51446-110">Konfigurowanie aplikacji dostęp do magazynu</span><span class="sxs-lookup"><span data-stu-id="51446-110">Configure your application to access storage</span></span>
<span data-ttu-id="51446-111">Korzystanie z usługi Azure storage, wymaga zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z magazynu usługi REST.</span><span class="sxs-lookup"><span data-stu-id="51446-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="51446-112">Umożliwia uzyskanie pakietu węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="51446-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="51446-113">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), aby przejść do folderu, w którym utworzono aplikację przykładową.</span><span class="sxs-lookup"><span data-stu-id="51446-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="51446-114">Typ **magazyn azure instalacji narzędzia npm** w oknie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="51446-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="51446-115">Dane wyjściowe polecenia jest podobny do poniższego przykładu kodu.</span><span class="sxs-lookup"><span data-stu-id="51446-115">Output from the command is similar to the following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="51446-116">Możesz ręcznie uruchomić **ls** polecenie, aby sprawdzić, czy **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="51446-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="51446-117">W tym folderze, Znajdź **magazyn azure** pakiet, który zawiera bibliotek, które wymagają dostępu do magazynu.</span><span class="sxs-lookup"><span data-stu-id="51446-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="51446-118">Importowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="51446-118">Import the package</span></span>
<span data-ttu-id="51446-119">Za pomocą Notatnika lub innego edytora tekstu, Dodaj następujący element do góry **server.js** pliku aplikacji, których zamierzasz używać magazynu:</span><span class="sxs-lookup"><span data-stu-id="51446-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="51446-120">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="51446-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="51446-121">Moduł Azure odczyta zmiennych środowiskowych `AZURE_STORAGE_ACCOUNT` i `AZURE_STORAGE_ACCESS_KEY`, lub `AZURE_STORAGE_CONNECTION_STRING`, aby uzyskać informacje wymagane do łączenia się z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51446-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="51446-122">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie podczas wywoływania metody **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="51446-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="51446-123">Ustawianie zmiennych środowiskowych, na przykład [portalu Azure](https://portal.azure.com) dla aplikacji sieci web platformy Azure, zobacz [aplikacji sieci web Node.js przy użyciu usługi Azure tabeli].</span><span class="sxs-lookup"><span data-stu-id="51446-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="51446-124">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="51446-124">Create a container</span></span>
<span data-ttu-id="51446-125">**BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="51446-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="51446-126">Poniższy kod tworzy **BlobService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="51446-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="51446-127">Dodaj następujący kod w górnej części **server.js**:</span><span class="sxs-lookup"><span data-stu-id="51446-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="51446-128">Dostęp obiektu blob anonimowo za pomocą **createBlobServiceAnonymous** i podając adres hosta.</span><span class="sxs-lookup"><span data-stu-id="51446-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="51446-129">Na przykład użyć `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="51446-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="51446-130">Aby utworzyć nowy kontener, użyj **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="51446-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="51446-131">Poniższy przykład kodu tworzy nowy kontener o nazwie "mojkontener":</span><span class="sxs-lookup"><span data-stu-id="51446-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="51446-132">Jeśli kontener jest nowo utworzony, `result.created` ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="51446-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="51446-133">Jeśli kontener już istnieje, `result.created` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="51446-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="51446-134">`response`zawiera informacje na temat operacji, w tym informacje o ETag kontenera.</span><span class="sxs-lookup"><span data-stu-id="51446-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="51446-135">Kontener zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="51446-135">Container security</span></span>
<span data-ttu-id="51446-136">Domyślnie nowe kontenery są prywatne i nie można uzyskać dostępu do anonimowo.</span><span class="sxs-lookup"><span data-stu-id="51446-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="51446-137">Aby udostępnić kontenera, dzięki czemu można do niego dostęp anonimowo, można ustawić dostępu do kontenera poziom **obiektu blob** lub **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="51446-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="51446-138">**Obiekt blob** — umożliwia anonimowy dostęp do odczytu do zawartości obiektu blob i metadanych, w tym kontenerze, ale nie do kontenera metadane, takie jak wyświetlanie listy wszystkich obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="51446-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="51446-139">**kontener** — umożliwia anonimowy dostęp do odczytu do zawartości obiektu blob i metadanych, tak jak metadanych kontenera</span><span class="sxs-lookup"><span data-stu-id="51446-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="51446-140">Poniższy przykład kodu pokazuje ustawienie poziom dostępu **obiektu blob**:</span><span class="sxs-lookup"><span data-stu-id="51446-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="51446-141">Alternatywnie można zmodyfikować poziom dostępu do kontenera za pomocą **setContainerAcl** określa poziom dostępu.</span><span class="sxs-lookup"><span data-stu-id="51446-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="51446-142">Poniższy przykład kodu zmienia poziom dostępu do kontenera:</span><span class="sxs-lookup"><span data-stu-id="51446-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="51446-143">Wynik zawiera informacje na temat operacji, łącznie z bieżącej **ETag** kontenera.</span><span class="sxs-lookup"><span data-stu-id="51446-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="51446-144">Filtry</span><span class="sxs-lookup"><span data-stu-id="51446-144">Filters</span></span>
<span data-ttu-id="51446-145">Opcjonalne operacjach filtrowania może dotyczyć operacje wykonywane przy użyciu **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="51446-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="51446-146">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę o sygnaturze są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="51446-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="51446-147">Po wykonaniu przetwarzanie wstępne opcje żądania, metoda musi wywołać "dalej", przekazywanie wywołania zwrotnego z następującą sygnaturą:</span><span class="sxs-lookup"><span data-stu-id="51446-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="51446-148">W tym wywołania zwrotnego, a po przetworzeniu returnObject (odpowiedź z żądania do serwera) wywołania zwrotnego musi wywołać obok, jeśli istnieje kontynuować przetwarzanie inne filtry lub po prostu Wywołaj finalCallback na koniec wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="51446-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="51446-149">Dwa filtry, które implementują logikę ponawiania wchodzą w skład zestawu Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="51446-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="51446-150">Tworzy następujące **BlobService** obiekt, który używa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="51446-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="51446-151">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="51446-151">Upload a blob into a container</span></span>
<span data-ttu-id="51446-152">Istnieją trzy typy obiektów blob: blokowe obiekty BLOB, stronicowe i uzupełnialne.</span><span class="sxs-lookup"><span data-stu-id="51446-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="51446-153">Blokowe obiekty BLOB zezwala na przekazywanie bardziej wydajne dużej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="51446-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="51446-154">Dołącz obiekty BLOB są zoptymalizowane pod kątem operacji dołączania.</span><span class="sxs-lookup"><span data-stu-id="51446-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="51446-155">Stronicowe obiekty BLOB są zoptymalizowane pod kątem operacji odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="51446-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="51446-156">Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="51446-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="51446-157">Obiekty BLOB typu Block</span><span class="sxs-lookup"><span data-stu-id="51446-157">Block blobs</span></span>
<span data-ttu-id="51446-158">Aby przekazać dane do blokowego obiektu blob, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="51446-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="51446-159">**createBlockBlobFromLocalFile** — tworzy nowy obiekt blob blokowy i przekazuje zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="51446-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="51446-160">**createBlockBlobFromStream** — tworzy nowy obiekt blob blokowy i przekazuje zawartość strumienia</span><span class="sxs-lookup"><span data-stu-id="51446-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="51446-161">**createBlockBlobFromText** — tworzy nowy obiekt blob blokowy i przekazuje zawartości ciągu</span><span class="sxs-lookup"><span data-stu-id="51446-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="51446-162">**createWriteStreamToBlockBlob** — zawiera strumień zapisu do blokowego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="51446-163">Poniższy przykład kodu przekazuje zawartość **test.txt** pliku do **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="51446-164">`result` Zwrócony przy użyciu tej metody zawiera informacje na temat działania, takie jak **ETag** obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="51446-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="51446-165">Uzupełnialnych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51446-165">Append blobs</span></span>
<span data-ttu-id="51446-166">Aby przekazać dane do nowy uzupełnialny obiekt blob, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="51446-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="51446-167">**createAppendBlobFromLocalFile** — tworzy nowy uzupełnialny obiekt blob i przekazuje zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="51446-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="51446-168">**createAppendBlobFromStream** — tworzy nowy uzupełnialny obiekt blob i przekazuje zawartość strumienia</span><span class="sxs-lookup"><span data-stu-id="51446-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="51446-169">**createAppendBlobFromText** — tworzy nowy uzupełnialny obiekt blob i przekazuje zawartości ciągu</span><span class="sxs-lookup"><span data-stu-id="51446-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="51446-170">**createWriteStreamToNewAppendBlob** — tworzy nowy uzupełnialny obiekt blob, a następnie oferuje strumienia do zapisu</span><span class="sxs-lookup"><span data-stu-id="51446-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="51446-171">Poniższy przykład kodu przekazuje zawartość **test.txt** pliku do **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="51446-172">Aby dołączyć blok do istniejących uzupełnialny obiekt blob, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="51446-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="51446-173">**appendFromLocalFile** -dołącza zawartość pliku do istniejącej uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="51446-174">**appendFromStream** -Dołącz zawartość strumienia do istniejących uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="51446-175">**appendFromText** -Dołącz zawartość ciąg do istniejącego uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="51446-176">**appendBlockFromStream** -Dołącz zawartość strumienia do istniejących uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="51446-177">**appendBlockFromText** -Dołącz zawartość ciąg do istniejącego uzupełnialnego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="51446-178">appendFromXXX interfejsów API wykona niektórych po stronie klienta niepowodzenie sprawdzania poprawności szybko uniknąć niepotrzebnych serwera wywołania.</span><span class="sxs-lookup"><span data-stu-id="51446-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="51446-179">nie będzie appendBlockFromXXX.</span><span class="sxs-lookup"><span data-stu-id="51446-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="51446-180">Poniższy przykład kodu przekazuje zawartość **test.txt** pliku do **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="51446-181">Stronicowe obiekty blob</span><span class="sxs-lookup"><span data-stu-id="51446-181">Page blobs</span></span>
<span data-ttu-id="51446-182">Aby przekazać dane do stronicowych obiektów blob, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="51446-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="51446-183">**createPageBlob** — tworzy nowy stronicowych obiektów blob o określonej długości</span><span class="sxs-lookup"><span data-stu-id="51446-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="51446-184">**createPageBlobFromLocalFile** — tworzy nowy stronicowych obiektów blob i przekazuje zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="51446-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="51446-185">**createPageBlobFromStream** — tworzy nowy stronicowych obiektów blob i przekazuje zawartość strumienia</span><span class="sxs-lookup"><span data-stu-id="51446-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="51446-186">**createWriteStreamToExistingPageBlob** — zawiera strumień zapisu do istniejącego obiektu blob strony</span><span class="sxs-lookup"><span data-stu-id="51446-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="51446-187">**createWriteStreamToNewPageBlob** — tworzy nowy stronicowych obiektów blob, a następnie oferuje strumienia do zapisu</span><span class="sxs-lookup"><span data-stu-id="51446-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="51446-188">Poniższy przykład kodu przekazuje zawartość **test.txt** pliku do **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="51446-189">Stronicowe obiekty BLOB składać się z 512-bajtowych "stron".</span><span class="sxs-lookup"><span data-stu-id="51446-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="51446-190">Podczas przekazywania danych o rozmiarze, który nie jest wielokrotnością 512, zostanie zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="51446-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="51446-191">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="51446-191">List the blobs in a container</span></span>
<span data-ttu-id="51446-192">Aby wyświetlić listę obiektów blob w kontenerze, należy użyć **listBlobsSegmented** metody.</span><span class="sxs-lookup"><span data-stu-id="51446-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="51446-193">Jeśli chcesz przywrócić obiekty BLOB z określonym prefiksem, użyj **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="51446-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="51446-194">`result` Zawiera `entries` kolekcji, która jest Tablica obiektów, które opisują każdy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="51446-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="51446-195">Jeśli nie można zwrócić wszystkie obiekty BLOB, `result` udostępnia również `continuationToken`, którego można użyć jako drugiego parametru do pobrania dodatkowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="51446-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="51446-196">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="51446-196">Download blobs</span></span>
<span data-ttu-id="51446-197">Aby pobrać dane z obiektu blob, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="51446-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="51446-198">**getBlobToLocalFile** -zapisuje zawartość obiektu blob do pliku</span><span class="sxs-lookup"><span data-stu-id="51446-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="51446-199">**getBlobToStream** -zapisuje zawartość obiektu blob do strumienia</span><span class="sxs-lookup"><span data-stu-id="51446-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="51446-200">**getBlobToText** -zapisuje zawartość obiektu blob na ciąg</span><span class="sxs-lookup"><span data-stu-id="51446-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="51446-201">**createReadStream** — zawiera strumień do odczytu z obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="51446-202">Poniższy przykład kodu pokazuje, za pomocą **getBlobToStream** do pobrania zawartości **mojblob** obiektu blob i zapisze go do **output.txt** pliku przy użyciu strumienia:</span><span class="sxs-lookup"><span data-stu-id="51446-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="51446-203">`result` Zawiera informacje dotyczące obiektów blob, łącznie z **ETag** informacji.</span><span class="sxs-lookup"><span data-stu-id="51446-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="51446-204">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="51446-204">Delete a blob</span></span>
<span data-ttu-id="51446-205">Na koniec można usunąć obiektu blob, należy wywołać **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="51446-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="51446-206">Poniższy przykład kodu usuwa obiektu blob o nazwie **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="51446-207">Współbieżny dostęp</span><span class="sxs-lookup"><span data-stu-id="51446-207">Concurrent access</span></span>
<span data-ttu-id="51446-208">Aby obsługiwać równoczesny dostęp do obiektu blob z wielu klientów lub wielu wystąpień procesu, można użyć **elementy etag** lub **dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="51446-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="51446-209">**Element etag** — pozwala wykryć, że obiekt blob lub kontener został zmodyfikowany przez inny proces</span><span class="sxs-lookup"><span data-stu-id="51446-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="51446-210">**Dzierżawy** — pozwala uzyskać wyłącznej, odnawialnymi, zapisu albo usuwania dostępu do obiektu blob w danym okresie czasu</span><span class="sxs-lookup"><span data-stu-id="51446-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="51446-211">Element ETag</span><span class="sxs-lookup"><span data-stu-id="51446-211">ETag</span></span>
<span data-ttu-id="51446-212">Elementy etag Użyj, jeśli konieczne jest zezwolenie na wielu klientów lub wystąpień do zapisu blokowych obiektów Blob lub strony Blob jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="51446-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="51446-213">Element ETag pozwala określić, czy kontener lub obiekt blob był modyfikowany od początku odczytu lub utworzone, dzięki czemu można uniknąć zastępowania zmian dokonanych przez innego klienta lub inny proces.</span><span class="sxs-lookup"><span data-stu-id="51446-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="51446-214">Można ustawić warunki ETag przy użyciu opcjonalnego `options.accessConditions` parametru.</span><span class="sxs-lookup"><span data-stu-id="51446-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="51446-215">Poniższy kod przykładowy tylko przekazywanie **test.txt** pliku, jeśli obiekt blob już istnieje i ma wartość ETag zawarty w `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="51446-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="51446-216">Jeśli używasz elementy etag ogólne wzorzec jest:</span><span class="sxs-lookup"><span data-stu-id="51446-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="51446-217">Uzyskaj element ETag w wyniku tworzenia, lista lub operacji get.</span><span class="sxs-lookup"><span data-stu-id="51446-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="51446-218">Wykonaj akcję, sprawdzanie, czy wartość ETag nie zostały zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="51446-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="51446-219">Jeśli wartość została zmieniona, to wskazuje, że innego klienta lub wystąpienia obiektu blob lub kontener ponieważ uzyskać wartość ETag.</span><span class="sxs-lookup"><span data-stu-id="51446-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="51446-220">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="51446-220">Lease</span></span>
<span data-ttu-id="51446-221">Możesz uzyskać nową dzierżawę za pomocą **acquireLease** metoda określania obiektu blob lub kontenera, który chcesz uzyskać dzierżawę na.</span><span class="sxs-lookup"><span data-stu-id="51446-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="51446-222">Na przykład następujący kod uzyskuje dzierżawę na **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="51446-223">Kolejne operacje na **mojblob** podać `options.leaseId` parametru.</span><span class="sxs-lookup"><span data-stu-id="51446-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="51446-224">Identyfikator jest zwracana jako dzierżawy `result.id` z **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="51446-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="51446-225">Domyślnie czas trwania dzierżawy to nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="51446-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="51446-226">Można określić czas trwania — bez ograniczeń czasowych (od 15 do 60 sekund) podając `options.leaseDuration` parametru.</span><span class="sxs-lookup"><span data-stu-id="51446-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="51446-227">Aby usunąć dzierżawę, użyj **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="51446-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="51446-228">Aby przerwać dzierżawy, ale uniemożliwić innym użytkownikom uzyskiwanie nową dzierżawę, dopóki wygasł czas trwania oryginalnej, użyj **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="51446-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="51446-229">Praca z sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="51446-229">Work with shared access signatures</span></span>
<span data-ttu-id="51446-230">Sygnatury dostępu współdzielonego (SAS) to bezpieczny sposób zapewnienia szczegółowego dostępu do obiektów blob i kontenery bez podawania Twojej nazwy konta magazynu i klucze.</span><span class="sxs-lookup"><span data-stu-id="51446-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="51446-231">Sygnatury dostępu współdzielonego są często używane w celu zapewnienia ograniczony dostęp do danych, na przykład pozwala aplikacji mobilnej, aby uzyskać dostępu do obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="51446-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="51446-232">Gdy, możesz również zezwolić na anonimowy dostęp do obiektów blob, sygnatur dostępu współdzielonego umożliwiają zapewniają więcej kontrolowany dostęp, jak należy wygenerować sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="51446-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="51446-233">Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnatur dostępu współdzielonego przy użyciu **generateSharedAccessSignature** z **BlobService**i udostępnia go do niezaufanych lub częściowo zaufanych aplikacji takich jak aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="51446-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="51446-234">Udostępnione dostępu podpisy są generowane przy użyciu zasad, które opisano rozpoczęcia i zakończenia dat, w których są prawidłowe sygnatury dostępu współdzielonego, jak również poziom dostępu przyznane posiadacz sygnatur dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="51446-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="51446-235">Poniższy przykład kodu generuje nowe zasady dostępu współdzielonego, które umożliwia posiadacz sygnatur dostępu współdzielonego do wykonywania operacji odczytu na **mojblob** obiektu blob i wygasa 100 minut po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="51446-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="51446-236">Należy pamiętać, że informacji o hoście należy podać również, jak jest wymagany, gdy posiadacz sygnatur dostępu współdzielonego próbuje uzyskać dostępu do kontenera.</span><span class="sxs-lookup"><span data-stu-id="51446-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="51446-237">Następnie aplikacja kliencka używa sygnatur dostępu współdzielonego z **BlobServiceWithSAS** wykonywanie operacji względem obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="51446-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="51446-238">Następujące pobiera informacje **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="51446-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="51446-239">Ponieważ sygnatur dostępu współdzielonego zostały wygenerowane z dostępem tylko do odczytu, jeśli próby modyfikowania obiektu blob, zostanie zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="51446-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="51446-240">Listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="51446-240">Access control lists</span></span>
<span data-ttu-id="51446-241">Listy kontroli dostępu (ACL) umożliwia także ustawić zasady dostępu dla sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="51446-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="51446-242">Jest to przydatne, jeśli chcesz umożliwić wielu klientom dostęp do kontenera, ale zapewnia różne zasady dostępu dla każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="51446-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="51446-243">Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="51446-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="51446-244">Poniższy przykład kodu definiuje dwie zasady, jeden dla "Użytkownik1" i jeden dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="51446-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="51446-245">Poniższy przykładowy kod pobiera bieżącej listy ACL dla **mojkontener**, a następnie dodaje nowe zasady przy użyciu **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="51446-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="51446-246">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="51446-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="51446-247">Po ustawieniu listy ACL, następnie można utworzyć na podstawie Identyfikatora zasady sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="51446-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="51446-248">Poniższy przykład kodu tworzy nowe sygnatury dostępu współdzielonego dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="51446-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="51446-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51446-249">Next steps</span></span>
<span data-ttu-id="51446-250">Aby uzyskać więcej informacji zobacz następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="51446-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="51446-251">[Magazyn Azure SDK dla węzła dokumentacja interfejsu API][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="51446-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="51446-252">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="51446-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="51446-253">[Zestaw Azure SDK magazynu dla węzła] [ Azure Storage SDK for Node] repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="51446-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="51446-254">Centrum deweloperów środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="51446-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="51446-255">Transfer danych za pomocą narzędzia wiersza polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="51446-255">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="51446-256">[tworzenie aplikacji sieci web Node.js w usłudze Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="51446-256">[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="51446-257">[aplikacji sieci web Node.js przy użyciu usługi Azure tabeli]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span><span class="sxs-lookup"><span data-stu-id="51446-257">[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span></span>
<span data-ttu-id="51446-258">[tworzenie i wdrażanie aplikacji sieci web Node.js na platformie Azure przy użyciu Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span><span class="sxs-lookup"><span data-stu-id="51446-258">[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span></span>
[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
<span data-ttu-id="51446-259">[tworzenia i wdrażania aplikacji Node.js do usługi w chmurze platformy Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span><span class="sxs-lookup"><span data-stu-id="51446-259">[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span></span>
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
