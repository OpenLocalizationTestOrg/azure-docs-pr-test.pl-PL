---
title: "toouse aaaHow magazynu obiektów Blob w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
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
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="2b6bf-103">Jak toouse magazynu obiektów Blob w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="2b6bf-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="2b6bf-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2b6bf-104">Overview</span></span>
<span data-ttu-id="2b6bf-105">W tym artykule opisano sposób tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="2b6bf-106">Przykłady Hello są zapisywane przez hello interfejsu API środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="2b6bf-107">omówione scenariusze Hello obejmują jak tooupload, listy, pobieranie i usuwanie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="2b6bf-108">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="2b6bf-108">Create a Node.js application</span></span>
<span data-ttu-id="2b6bf-109">Aby uzyskać instrukcje dotyczące toocreate aplikacji Node.js, zobacz [tworzenie aplikacji sieci web Node.js w usłudze Azure App Service], [tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure] — za pomocą środowiska Windows PowerShell , lub [tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web].</span><span class="sxs-lookup"><span data-stu-id="2b6bf-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="2b6bf-110">Konfigurowanie magazynu tooaccess aplikacji</span><span class="sxs-lookup"><span data-stu-id="2b6bf-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="2b6bf-111">toouse magazynu Azure, należy hello zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="2b6bf-112">Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="2b6bf-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="2b6bf-113">Użyj interfejsu wiersza polecenia, takich jak **środowiska PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), toonavigate toohello folder, w którym utworzono przykładu aplikacja.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="2b6bf-114">Typ **magazyn azure instalacji narzędzia npm** w oknie polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="2b6bf-115">Dane wyjściowe polecenia hello jest toohello podobnie poniższy przykład kodu.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="2b6bf-116">Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="2b6bf-117">W tym folderze, Znajdź hello **magazyn azure** pakiet, który zawiera biblioteki hello konieczność tooaccess magazynu.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="2b6bf-118">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="2b6bf-118">Import hello package</span></span>
<span data-ttu-id="2b6bf-119">Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello hello **server.js** pliku aplikacji hello, w którym ma toouse magazynu:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="2b6bf-120">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="2b6bf-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="2b6bf-121">Hello Azure modułu odczyta zmiennych środowiskowych hello `AZURE_STORAGE_ACCOUNT` i `AZURE_STORAGE_ACCESS_KEY`, lub `AZURE_STORAGE_CONNECTION_STRING`, informacje wymagane tooconnect tooyour konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="2b6bf-122">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="2b6bf-123">Na przykład ustawienia zmiennych środowiskowych hello w hello [portalu Azure](https://portal.azure.com) dla aplikacji sieci web platformy Azure, zobacz [aplikacji sieci web Node.js w usłudze hello Azure usługa tabel].</span><span class="sxs-lookup"><span data-stu-id="2b6bf-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="2b6bf-124">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="2b6bf-124">Create a container</span></span>
<span data-ttu-id="2b6bf-125">Witaj **BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="2b6bf-126">Witaj poniższy kod tworzy **BlobService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="2b6bf-127">Dodaj następujące hello u góry hello **server.js**:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="2b6bf-128">Dostęp obiektu blob anonimowo za pomocą **createBlobServiceAnonymous** i podając adres hosta hello.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="2b6bf-129">Na przykład użyć `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="2b6bf-130">Użyj toocreate nowy kontener **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="2b6bf-131">Witaj poniższy przykład kodu tworzy nowy kontener o nazwie "mojkontener":</span><span class="sxs-lookup"><span data-stu-id="2b6bf-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="2b6bf-132">Jeśli kontener hello jest nowo utworzony, `result.created` ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="2b6bf-133">Jeśli istnieje już hello kontenera, `result.created` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="2b6bf-134">`response`zawiera informacje na temat operacji hello, w tym informacje o ETag hello hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="2b6bf-135">Kontener zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2b6bf-135">Container security</span></span>
<span data-ttu-id="2b6bf-136">Domyślnie nowe kontenery są prywatne i nie można uzyskać dostępu do anonimowo.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="2b6bf-137">kontener hello toomake publiczna, dzięki czemu można do niego dostęp anonimowo kontenera hello poziom dostępu można ustawić także**obiektu blob** lub **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="2b6bf-138">**Obiekt blob** — zezwala na zawartość tooblob anonimowy dostęp do odczytu i metadanych, w tym kontenerze, ale nie toocontainer metadane, takie jak wyświetlanie listy wszystkich obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="2b6bf-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="2b6bf-139">**kontener** — zezwala na zawartość tooblob anonimowy dostęp do odczytu i metadanych, tak jak metadanych kontenera</span><span class="sxs-lookup"><span data-stu-id="2b6bf-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="2b6bf-140">Witaj poniższy przykład kodu pokazuje poziom dostępu hello ustawienie zbyt**obiektu blob**:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="2b6bf-141">Alternatywnie można zmodyfikować poziomu dostępu hello kontenera za pomocą **setContainerAcl** poziom dostępu hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="2b6bf-142">Witaj poniższy kod toocontainer poziomu dostępu przykład zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="2b6bf-143">Witaj wynik zawiera informacje na temat operacji hello, łącznie z bieżącym hello **ETag** hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="2b6bf-144">Filtry</span><span class="sxs-lookup"><span data-stu-id="2b6bf-144">Filters</span></span>
<span data-ttu-id="2b6bf-145">Możesz zastosować opcjonalne filtrowania operacji toooperations wykonywane przy użyciu **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="2b6bf-146">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="2b6bf-147">Po wykonaniu przetwarzanie wstępne opcje żądania hello, metoda hello musi toocall "dalej", przekazywanie wywołania zwrotnego z powitania po podpisaniu:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="2b6bf-148">W tym wywołania zwrotnego, a po przetworzeniu hello returnObject (hello odpowiedź z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub po prostu Wywołaj finalCallback tooend hello usługi wywołania.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="2b6bf-149">Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="2b6bf-150">tworzy następujące Hello **BlobService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2b6bf-151">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="2b6bf-151">Upload a blob into a container</span></span>
<span data-ttu-id="2b6bf-152">Istnieją trzy typy obiektów blob: blokowe obiekty BLOB, stronicowe i uzupełnialne.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="2b6bf-153">Blokowe obiekty BLOB umożliwiają toomore wydajnie Przekaż dużej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="2b6bf-154">Dołącz obiekty BLOB są zoptymalizowane pod kątem operacji dołączania.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="2b6bf-155">Stronicowe obiekty BLOB są zoptymalizowane pod kątem operacji odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="2b6bf-156">Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6bf-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="2b6bf-157">Obiekty BLOB typu Block</span><span class="sxs-lookup"><span data-stu-id="2b6bf-157">Block blobs</span></span>
<span data-ttu-id="2b6bf-158">tooupload danych tooa blokowych obiektów blob, użyj hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="2b6bf-159">**createBlockBlobFromLocalFile** — tworzy nowy obiekt blob blokowy i przekazuje hello zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="2b6bf-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="2b6bf-160">**createBlockBlobFromStream** — tworzy nowy obiekt blob blokowy i przekazuje hello zawartość strumienia</span><span class="sxs-lookup"><span data-stu-id="2b6bf-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="2b6bf-161">**createBlockBlobFromText** — tworzy nowy obiekt blob blokowy i przekazuje ciąg hello zawartość</span><span class="sxs-lookup"><span data-stu-id="2b6bf-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="2b6bf-162">**createWriteStreamToBlockBlob** — zapewnia zapisu strumienia tooa blokowego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="2b6bf-163">Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="2b6bf-164">Witaj `result` zwrócony przy użyciu tej metody zawiera informacje na temat operacji hello, takiej jak hello **ETag** hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="2b6bf-165">Uzupełnialnych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-165">Append blobs</span></span>
<span data-ttu-id="2b6bf-166">nowe tooa danych tooupload Dołącz obiektów blob, należy użyć następującego hello:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="2b6bf-167">**createAppendBlobFromLocalFile** — tworzy nowy uzupełnialny obiekt blob i przekazuje hello zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="2b6bf-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="2b6bf-168">**createAppendBlobFromStream** — tworzy nowy uzupełnialny obiekt blob i przekazuje hello zawartość strumienia</span><span class="sxs-lookup"><span data-stu-id="2b6bf-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="2b6bf-169">**createAppendBlobFromText** — tworzy nowy uzupełnialny obiekt blob i przekazuje ciąg hello zawartość</span><span class="sxs-lookup"><span data-stu-id="2b6bf-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="2b6bf-170">**createWriteStreamToNewAppendBlob** — tworzy nowy uzupełnialny obiekt blob, a następnie oferuje tooit toowrite strumienia</span><span class="sxs-lookup"><span data-stu-id="2b6bf-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="2b6bf-171">Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="2b6bf-172">tooappend istniejących tooan bloku Dołącz obiektów blob, użyj hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="2b6bf-173">**appendFromLocalFile** -Dołącz zawartość hello tooan pliku istniejących Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="2b6bf-174">**appendFromStream** -Dołącz zawartość hello tooan strumienia istniejących Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="2b6bf-175">**appendFromText** -Dołącz zawartość hello tooan ciąg istniejących Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="2b6bf-176">**appendBlockFromStream** -Dołącz zawartość hello tooan strumienia istniejących Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="2b6bf-177">**appendBlockFromText** -Dołącz zawartość hello tooan ciąg istniejących Dołącz obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="2b6bf-178">interfejsy API appendFromXXX wykona niektóre połączenia serwera niepotrzebnych szybkiego tooavoid toofail weryfikacji po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="2b6bf-179">nie będzie appendBlockFromXXX.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="2b6bf-180">Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="2b6bf-181">Stronicowe obiekty blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-181">Page blobs</span></span>
<span data-ttu-id="2b6bf-182">tooupload danych tooa stronicowych obiektów blob, użyj hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="2b6bf-183">**createPageBlob** — tworzy nowy stronicowych obiektów blob o określonej długości</span><span class="sxs-lookup"><span data-stu-id="2b6bf-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="2b6bf-184">**createPageBlobFromLocalFile** — tworzy nowy stronicowych obiektów blob i przekazuje hello zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="2b6bf-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="2b6bf-185">**createPageBlobFromStream** — tworzy nowy stronicowych obiektów blob i przekazuje hello zawartość strumienia</span><span class="sxs-lookup"><span data-stu-id="2b6bf-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="2b6bf-186">**createWriteStreamToExistingPageBlob** — zapewnia zapisu strumienia tooan istniejących stronicowy obiekt blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="2b6bf-187">**createWriteStreamToNewPageBlob** — tworzy nowy stronicowych obiektów blob, a następnie oferuje tooit toowrite strumienia</span><span class="sxs-lookup"><span data-stu-id="2b6bf-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="2b6bf-188">Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="2b6bf-189">Stronicowe obiekty BLOB składać się z 512-bajtowych "stron".</span><span class="sxs-lookup"><span data-stu-id="2b6bf-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="2b6bf-190">Podczas przekazywania danych o rozmiarze, który nie jest wielokrotnością 512, zostanie zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="2b6bf-191">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="2b6bf-191">List hello blobs in a container</span></span>
<span data-ttu-id="2b6bf-192">toolist hello BLOB w kontenerze, użyj hello **listBlobsSegmented** metody.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="2b6bf-193">Jeśli chcesz obiektów blob tooreturn z określonego prefiksu, użyj **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="2b6bf-194">Witaj `result` zawiera `entries` kolekcji, która jest Tablica obiektów, które opisują każdy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="2b6bf-195">Jeśli nie można zwrócić wszystkie obiekty BLOB, hello `result` udostępnia również `continuationToken`, którego można użyć jako hello drugi parametr tooretrieve dodatkowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="2b6bf-196">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-196">Download blobs</span></span>
<span data-ttu-id="2b6bf-197">toodownload danych z obiektu blob, użyj następujących hello:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="2b6bf-198">**getBlobToLocalFile** -zapisuje toofile zawartość obiektu blob hello</span><span class="sxs-lookup"><span data-stu-id="2b6bf-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="2b6bf-199">**getBlobToStream** -zapisuje strumienia tooa zawartość obiektu blob hello</span><span class="sxs-lookup"><span data-stu-id="2b6bf-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="2b6bf-200">**getBlobToText** -zapisuje zawartość obiektu blob hello tooa ciąg</span><span class="sxs-lookup"><span data-stu-id="2b6bf-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="2b6bf-201">**createReadStream** — zapewnia tooread strumień z obiektu blob hello</span><span class="sxs-lookup"><span data-stu-id="2b6bf-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="2b6bf-202">Hello poniższy przykład kodu pokazuje przy użyciu **getBlobToStream** toodownload zawartość hello hello **mojblob** obiektu blob i zapisz go w toohello **output.txt** plików za pomocą Strumień:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="2b6bf-203">Witaj `result` zawiera informacje dotyczące obiektów blob hello, w tym **ETag** informacji.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="2b6bf-204">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2b6bf-204">Delete a blob</span></span>
<span data-ttu-id="2b6bf-205">Na koniec wywołania toodelete obiektu blob **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="2b6bf-206">Witaj, poniższy przykład kodu usuwa hello obiektu blob o nazwie **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="2b6bf-207">Współbieżny dostęp</span><span class="sxs-lookup"><span data-stu-id="2b6bf-207">Concurrent access</span></span>
<span data-ttu-id="2b6bf-208">toosupport współbieżny dostęp tooa dużego obiektu binarnego z wielu klientów lub wielu wystąpień procesu, można użyć **elementy etag** lub **dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="2b6bf-209">**Element etag** — zapewnia toodetect sposób, który hello obiektów blob lub kontener został zmodyfikowany przez inny proces</span><span class="sxs-lookup"><span data-stu-id="2b6bf-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="2b6bf-210">**Dzierżawy** — zapewnia zapisu sposób tooobtain wyłączności, może być wznawiane, lub usunąć obiektu blob tooa dostępu w danym okresie czasu</span><span class="sxs-lookup"><span data-stu-id="2b6bf-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="2b6bf-211">Element ETag</span><span class="sxs-lookup"><span data-stu-id="2b6bf-211">ETag</span></span>
<span data-ttu-id="2b6bf-212">Elementy etag należy użyć, jeśli potrzebujesz tooallow wielu klientów lub wystąpień toowrite toohello blokowych obiektów Blob lub strona obiektu Blob jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="2b6bf-213">Witaj ETag pozwala toodetermine Jeśli hello kontener lub obiekt blob został zmodyfikowany od czasu początkowo odczytu lub utworzone, dzięki czemu można tooavoid nadpisaniem zmian dokonanych przez innego klienta lub inny proces.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="2b6bf-214">Można ustawić warunki ETag przy użyciu hello opcjonalne `options.accessConditions` parametru.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="2b6bf-215">Witaj Poniższy przykładowy kod tylko przekazuje hello **test.txt** pliku, jeśli obiekt blob hello już istnieje i ma wartość ETag hello zawarty w `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="2b6bf-216">Jeśli używasz elementy etag wzorzec ogólne hello jest:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="2b6bf-217">Uzyskaj hello ETag wyniku hello Utwórz, listy lub operacji get.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="2b6bf-218">Wykonaj akcję, sprawdzanie tego hello wartość ETag nie został zmodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="2b6bf-219">Jeśli wartość hello został zmodyfikowany, to wskazuje, że innego klienta lub wystąpienia obiektu blob hello lub kontener ponieważ uzyskać wartość ETag hello.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="2b6bf-220">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="2b6bf-220">Lease</span></span>
<span data-ttu-id="2b6bf-221">Możesz uzyskać nową dzierżawę za pomocą hello **acquireLease** metoda określania hello blob lub kontenera, które chcesz tooobtain dzierżawę na.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="2b6bf-222">Na przykład powitania po kod uzyskuje dzierżawę na **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="2b6bf-223">Kolejne operacje na **mojblob** podać hello `options.leaseId` parametru.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="2b6bf-224">dzierżawy Hello identyfikator jest zwracana jako `result.id` z **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="2b6bf-225">Domyślnie czas trwania dzierżawy hello jest nieograniczony.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="2b6bf-226">Czas trwania — bez ograniczeń czasowych (od 15 do 60 sekund) można określić, zapewniając hello `options.leaseDuration` parametru.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="2b6bf-227">Użyj tooremove dzierżawę, **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="2b6bf-228">toobreak dzierżawy, ale uniemożliwia innym uzyskaniu nowej dzierżawy, dopóki nie wygasł czas trwania oryginalnego hello, użyj funkcji **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="2b6bf-229">Praca z sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="2b6bf-229">Work with shared access signatures</span></span>
<span data-ttu-id="2b6bf-230">Sygnatury dostępu współdzielonego (SAS) są tooblobs bezpieczny sposób tooprovide szczegółowego dostępu i kontenery bez podawania Twojej nazwy konta magazynu i klucze.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="2b6bf-231">Sygnatury dostępu współdzielonego są często używane tooprovide ograniczony dostęp tooyour dane, takie jak stosowanie aplikacji mobilnej tooaccess obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="2b6bf-232">Gdy, możesz również zezwolić tooblobs dostępu anonimowego, sygnatur dostępu współdzielonego pozwalają tooprovide więcej pod kontrolą dostępu, jak należy wygenerować hello sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="2b6bf-233">Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnatur dostępu współdzielonego przy użyciu hello **generateSharedAccessSignature** z hello **BlobService**i udostępnia go tooan niezaufanych lub częściowo zaufanych aplikacji takich jak aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="2b6bf-234">Dostępu współdzielonego podpisów, zostaną wygenerowane za pomocą zasad, które opisano hello rozpoczęcia i daty zakończenia, podczas których hello sygnatur dostępu współdzielonego są prawidłowe, a także hello dostęp do poziomu nadanego posiadacz sygnatur dostępu współdzielonego toohello.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="2b6bf-235">Witaj poniższy przykład kodu generuje nowe zasady dostępu współdzielonego, które umożliwia tooperform symbol zastępczy sygnatur dostępu hello udostępniony operacje na powitania odczytu **mojblob** obiektu blob i wygasa 100 minut po godzinie hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="2b6bf-236">Należy pamiętać, że informacji o hoście hello należy dostarczyć także zgodnie z wymaganiami podczas posiadacz sygnatur dostępu współdzielonego hello prób tooaccess hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="2b6bf-237">Witaj następnie aplikacja kliencka używa sygnatur dostępu współdzielonego z **BlobServiceWithSAS** tooperform operacji względem hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="2b6bf-238">Witaj następujące pobiera informacje **mojblob**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="2b6bf-239">Ponieważ sygnatur dostępu hello udostępnione zostały wygenerowane z dostępem tylko do odczytu, jeśli obiekt blob hello toomodify podejmowana jest próba, zostanie zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="2b6bf-240">Listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="2b6bf-240">Access control lists</span></span>
<span data-ttu-id="2b6bf-241">Umożliwia także zasady kontroli dostępu listę kontroli dostępu (ACL) tooset hello dostępu dla sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="2b6bf-242">Jest to przydatne, jeśli chcesz tooallow wielu klientów tooaccess kontener, ale zapewniają różne zasady dostępu dla każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="2b6bf-243">Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="2b6bf-244">Witaj poniższy przykład kodu definiuje dwie zasady, jeden dla "Użytkownik1" i jeden dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="2b6bf-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="2b6bf-245">powitania po pobiera przykładowy kod hello bieżącej listy ACL dla **mojkontener**, a następnie dodaje nowe zasady hello przy użyciu **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="2b6bf-246">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="2b6bf-246">This approach allows:</span></span>

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

<span data-ttu-id="2b6bf-247">Raz hello ustawione listy ACL, następnie można utworzyć na podstawie Identyfikatora hello zasad sygnatur dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="2b6bf-248">Witaj poniższy przykład kodu tworzy nowe sygnatury dostępu współdzielonego dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="2b6bf-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="2b6bf-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b6bf-249">Next steps</span></span>
<span data-ttu-id="2b6bf-250">Aby uzyskać więcej informacji zobacz następujące zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="2b6bf-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="2b6bf-251">[Magazyn Azure SDK dla węzła dokumentacja interfejsu API][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="2b6bf-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="2b6bf-252">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="2b6bf-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="2b6bf-253">[Zestaw Azure SDK magazynu dla węzła] [ Azure Storage SDK for Node] repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="2b6bf-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="2b6bf-254">Centrum deweloperów środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="2b6bf-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="2b6bf-255">Transfer danych za pomocą hello wiersza polecenia azcopy</span><span class="sxs-lookup"><span data-stu-id="2b6bf-255">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[tworzenie aplikacji sieci web Node.js w usłudze Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[aplikacji sieci web Node.js w usłudze hello Azure usługa tabel]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
