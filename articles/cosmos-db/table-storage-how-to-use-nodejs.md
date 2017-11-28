---
title: "Jak używać magazynu tabel Azure w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze za pomocą Magazynu tabel Azure, magazyn danych NoSQL."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 539212c6abe7738c022d67245f8992516f0899ff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="7192c-103">Jak używać magazynu tabel Azure w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="7192c-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="7192c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7192c-104">Overview</span></span>
<span data-ttu-id="7192c-105">W tym temacie przedstawiono sposób wykonywania typowych scenariuszy przy użyciu usługi Azure tabel w aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="7192c-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="7192c-106">Przykłady kodu, w tym temacie założono, że masz już aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="7192c-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="7192c-107">Aby uzyskać informacje o sposobie tworzenia aplikacji Node.js na platformie Azure, zobacz Tematy te:</span><span class="sxs-lookup"><span data-stu-id="7192c-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="7192c-108">Tworzenie aplikacji sieci web Node.js w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7192c-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="7192c-109">Tworzenie i wdrażanie aplikacji sieci web Node.js na platformie Azure za pomocą programu WebMatrix</span><span class="sxs-lookup"><span data-stu-id="7192c-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="7192c-110">[Tworzenie i wdrażanie aplikacji Node.js do usługi w chmurze platformy Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (przy użyciu programu Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7192c-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="7192c-111">Konfigurowanie aplikacji dostęp do magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="7192c-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="7192c-112">Korzystanie z usługi Azure Storage, wymaga zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z magazynu usługi REST.</span><span class="sxs-lookup"><span data-stu-id="7192c-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="7192c-113">Należy zainstalować pakiet węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="7192c-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="7192c-114">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **Terminal** (Mac), lub **Bash** (Unix) i przejdź do folderu, w którym utworzono aplikację.</span><span class="sxs-lookup"><span data-stu-id="7192c-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="7192c-115">Typ **magazyn azure instalacji narzędzia npm** w oknie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7192c-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="7192c-116">Dane wyjściowe polecenia jest podobny do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="7192c-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="7192c-117">Możesz ręcznie uruchomić **ls** polecenie, aby sprawdzić, czy **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="7192c-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="7192c-118">Wewnątrz tego folderu znajdują się **magazyn azure** pakiet, który zawiera biblioteki muszą uzyskać dostęp do magazynu.</span><span class="sxs-lookup"><span data-stu-id="7192c-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="7192c-119">Importowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7192c-119">Import the package</span></span>
<span data-ttu-id="7192c-120">Dodaj następujący kod do góry **server.js** plik w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="7192c-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="7192c-121">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="7192c-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="7192c-122">Moduł azure odczyta zmiennych środowiskowych AZURE\_MAGAZYNU\_konto i AZURE\_MAGAZYNU\_dostępu\_klucz lub AZURE\_MAGAZYNU\_połączenia\_ciąg informacje wymagane do łączenia się z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7192c-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="7192c-123">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie podczas wywoływania metody **TableService**.</span><span class="sxs-lookup"><span data-stu-id="7192c-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="7192c-124">Ustawianie zmiennych środowiskowych, na przykład [portalu Azure](https://portal.azure.com) dla witryny sieci Web Azure, zobacz [aplikacji sieci web Node.js przy użyciu usługi Azure tabeli](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="7192c-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="7192c-125">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="7192c-125">Create a table</span></span>
<span data-ttu-id="7192c-126">Poniższy kod tworzy **TableService** obiektu i używa jej do utworzenia nowej tabeli.</span><span class="sxs-lookup"><span data-stu-id="7192c-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="7192c-127">Dodaj następujący kod w górnej części **server.js**.</span><span class="sxs-lookup"><span data-stu-id="7192c-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="7192c-128">Wywołanie **createTableIfNotExists** spowoduje utworzenie nowej tabeli o określonej nazwie, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7192c-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="7192c-129">Poniższy przykład tworzy nową tabelę o nazwie "mytable", jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="7192c-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="7192c-130">`result.created` Będzie `true` Jeśli nowa tabela została utworzona, oraz `false` Jeśli tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="7192c-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="7192c-131">`response` Będzie zawierać informacje o żądaniu.</span><span class="sxs-lookup"><span data-stu-id="7192c-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="7192c-132">Filtry</span><span class="sxs-lookup"><span data-stu-id="7192c-132">Filters</span></span>
<span data-ttu-id="7192c-133">Opcjonalne operacjach filtrowania może odnosić się do operacji wykonywanych przy użyciu **TableService**.</span><span class="sxs-lookup"><span data-stu-id="7192c-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="7192c-134">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę o sygnaturze są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="7192c-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="7192c-135">Po wykonaniu przetwarzanie wstępne opcje żądania, metoda musi wywołać "dalej", przekazywanie wywołania zwrotnego z następującą sygnaturą:</span><span class="sxs-lookup"><span data-stu-id="7192c-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="7192c-136">W tym wywołania zwrotnego, a po przetworzeniu returnObject (odpowiedź z żądania do serwera) wywołania zwrotnego musi wywołać obok, jeśli istnieje kontynuować przetwarzanie inne filtry lub po prostu Wywołaj finalCallback inaczej na koniec wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="7192c-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="7192c-137">Dwa filtry, które implementują logikę ponawiania wchodzą w skład zestawu Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="7192c-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="7192c-138">Tworzy następujące **TableService** obiekt, który używa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="7192c-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="7192c-139">Dodawanie jednostki do tabeli</span><span class="sxs-lookup"><span data-stu-id="7192c-139">Add an entity to a table</span></span>
<span data-ttu-id="7192c-140">Aby dodać jednostkę, należy najpierw utworzyć obiekt, który definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="7192c-141">Musi zawierać wszystkie jednostki **PartitionKey** i **RowKey**, które są unikatowe identyfikatory dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="7192c-142">**PartitionKey** — Określa jednostki przechowywanego w partycji</span><span class="sxs-lookup"><span data-stu-id="7192c-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="7192c-143">**RowKey** — unikatowo identyfikuje jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="7192c-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="7192c-144">Zarówno **PartitionKey** i **RowKey** muszą być ciągami.</span><span class="sxs-lookup"><span data-stu-id="7192c-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="7192c-145">Aby uzyskać więcej informacji, zobacz [opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="7192c-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="7192c-146">Oto przykład Definiowanie jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="7192c-147">Należy pamiętać, że **Data ukończenia** jest zdefiniowana jako typ **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="7192c-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="7192c-148">Określenie typu jest opcjonalny i typy będzie można wywnioskować, jeśli nie została określona.</span><span class="sxs-lookup"><span data-stu-id="7192c-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="7192c-149">Istnieje również **sygnatury czasowej** pola dla każdego rekordu, który jest ustawiony przez platformę Azure, gdy jednostki są wstawiane lub aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="7192c-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="7192c-150">Można również użyć **entityGenerator** do tworzenia jednostek.</span><span class="sxs-lookup"><span data-stu-id="7192c-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="7192c-151">Poniższy przykład tworzy w tej samej zadań jednostki przy użyciu **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="7192c-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="7192c-152">Aby dodać jednostkę do tabeli, należy przekazać do obiektu jednostki **insertEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="7192c-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="7192c-153">Jeśli operacja się powiodła, `result` będzie zawierać [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) wstawionego rekordu i `response` będzie zawierać informacje na temat operacji.</span><span class="sxs-lookup"><span data-stu-id="7192c-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="7192c-154">Przykład odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="7192c-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="7192c-155">Domyślnie **insertEntity** nie zwraca jednostek wstawiony jako część `response` informacji.</span><span class="sxs-lookup"><span data-stu-id="7192c-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="7192c-156">Jeśli planowane jest wykonywanie innych operacji w tej jednostce lub chcesz buforowanie tych informacji mogą być przydatne jest zwracane jako część `result`.</span><span class="sxs-lookup"><span data-stu-id="7192c-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="7192c-157">Można to zrobić przez włączenie **echoContent** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7192c-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="7192c-158">Aktualizuj jednostkę</span><span class="sxs-lookup"><span data-stu-id="7192c-158">Update an entity</span></span>
<span data-ttu-id="7192c-159">Dostępnych jest kilka metod do zaktualizowania istniejącej jednostki:</span><span class="sxs-lookup"><span data-stu-id="7192c-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="7192c-160">**replaceEntity** -aktualizacji przez zastąpienie istniejącej jednostki</span><span class="sxs-lookup"><span data-stu-id="7192c-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="7192c-161">**mergeEntity** -aktualizuje istniejącą jednostkę przez scalenie nowej wartości właściwości istniejącej jednostki</span><span class="sxs-lookup"><span data-stu-id="7192c-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="7192c-162">**insertOrReplaceEntity** -aktualizacji przez zastąpienie istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="7192c-163">Jeśli jednostka nie istnieje, zostanie wstawiony nowy</span><span class="sxs-lookup"><span data-stu-id="7192c-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="7192c-164">**insertOrMergeEntity** — aktualizuje istniejące jednostki przez scalenie nowej wartości właściwości istniejącej.</span><span class="sxs-lookup"><span data-stu-id="7192c-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="7192c-165">Jeśli jednostka nie istnieje, zostanie wstawiony nowy</span><span class="sxs-lookup"><span data-stu-id="7192c-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="7192c-166">W poniższym przykładzie pokazano, aktualizowanie jednostki przy użyciu **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="7192c-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="7192c-167">Domyślnie aktualizowania jednostki nie Sprawdź, czy dane aktualizowana wcześniej zostały zmodyfikowane przez inny proces.</span><span class="sxs-lookup"><span data-stu-id="7192c-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="7192c-168">Do obsługi współbieżnych aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="7192c-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="7192c-169">Pobierz element ETag aktualizowany obiekt.</span><span class="sxs-lookup"><span data-stu-id="7192c-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="7192c-170">Ten błąd jest zwracany jako część `response` do żadnej operacji powiązanych jednostek i mogą zostać pobrane za pośrednictwem `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="7192c-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="7192c-171">Podczas wykonywania operacji update na jednostkę, Dodaj informacje ETag wcześniej pobrane do nowego obiektu.</span><span class="sxs-lookup"><span data-stu-id="7192c-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="7192c-172">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7192c-172">For example:</span></span>
>
>       <span data-ttu-id="7192c-173">entity2 .etag [.metadata] = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="7192c-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="7192c-174">Wykonaj operację aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7192c-174">Perform the update operation.</span></span> <span data-ttu-id="7192c-175">Jeśli jednostka została zmodyfikowana od czasu pobrania wartość ETag, takich jak inne wystąpienie aplikacji, `error` zostaną zwrócone z informacją nie był spełniony warunek aktualizacji określony w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="7192c-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="7192c-176">Z **replaceEntity** i **mergeEntity**, jeśli jednostka, która jest aktualizowana nie istnieje, operacja aktualizacji zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7192c-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="7192c-177">Dlatego jeśli chcesz przechowywać jednostki, niezależnie od tego, czy już istnieje, użyj **insertOrReplaceEntity** lub **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="7192c-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="7192c-178">`result` Dla pomyślnej aktualizacji będzie zawierać operacje **Etag** zaktualizowane jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="7192c-179">Praca z grupami jednostek</span><span class="sxs-lookup"><span data-stu-id="7192c-179">Work with groups of entities</span></span>
<span data-ttu-id="7192c-180">Czasami warto przesłać wiele operacji ze sobą w partii zapewnienie atomic przetwarzania przez serwer.</span><span class="sxs-lookup"><span data-stu-id="7192c-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="7192c-181">Celu, który należy użyć **TableBatch** klasa do tworzenia partii, a następnie użyj **executeBatch** metody **TableService** w celu wykonania operacji wsadowej.</span><span class="sxs-lookup"><span data-stu-id="7192c-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="7192c-182">W poniższym przykładzie pokazano, przesyłanie dwie jednostki w partii:</span><span class="sxs-lookup"><span data-stu-id="7192c-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="7192c-183">Dla operacji wsadowych pomyślne `result` będzie zawierać informacje dla każdej operacji w partii.</span><span class="sxs-lookup"><span data-stu-id="7192c-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="7192c-184">Praca z operacji wsadowych</span><span class="sxs-lookup"><span data-stu-id="7192c-184">Work with batched operations</span></span>
<span data-ttu-id="7192c-185">Dodane do partii operacje mogą być kontrolowane przez wyświetlanie `operations` właściwości.</span><span class="sxs-lookup"><span data-stu-id="7192c-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="7192c-186">Można także użyć następujących metod do pracy z operacjami:</span><span class="sxs-lookup"><span data-stu-id="7192c-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="7192c-187">**Wyczyść** — usuwa wszystkie operacje z partii</span><span class="sxs-lookup"><span data-stu-id="7192c-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="7192c-188">**getOperations** -pobiera operację z partii</span><span class="sxs-lookup"><span data-stu-id="7192c-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="7192c-189">**hasOperations** — zwraca wartość true, jeśli partia zawiera operacje</span><span class="sxs-lookup"><span data-stu-id="7192c-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="7192c-190">**removeOperations** — usuwa operacji</span><span class="sxs-lookup"><span data-stu-id="7192c-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="7192c-191">**rozmiar** — zwraca liczbę operacji w partii</span><span class="sxs-lookup"><span data-stu-id="7192c-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="7192c-192">Pobrać jednostek według klucza</span><span class="sxs-lookup"><span data-stu-id="7192c-192">Retrieve an entity by key</span></span>
<span data-ttu-id="7192c-193">Aby powrócić do określonej jednostki na podstawie **PartitionKey** i **RowKey**, użyj **retrieveEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="7192c-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="7192c-194">Po zakończeniu tej operacji `result` będzie zawierać jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="7192c-195">Zapytanie zestawu jednostek</span><span class="sxs-lookup"><span data-stu-id="7192c-195">Query a set of entities</span></span>
<span data-ttu-id="7192c-196">Aby sprawdzić tabelę, użyj **TableQuery** obiekt do zbudowania przy użyciu następujących klauzule wyrażenia zapytania:</span><span class="sxs-lookup"><span data-stu-id="7192c-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="7192c-197">**Wybierz** -pola, które mają być zwracane z kwerendy</span><span class="sxs-lookup"><span data-stu-id="7192c-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="7192c-198">**gdzie** -where — klauzula</span><span class="sxs-lookup"><span data-stu-id="7192c-198">**where** - the where clause</span></span>

  * <span data-ttu-id="7192c-199">**i** — `and` warunek where</span><span class="sxs-lookup"><span data-stu-id="7192c-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="7192c-200">**lub** — `or` warunek where</span><span class="sxs-lookup"><span data-stu-id="7192c-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="7192c-201">**TOP** -liczba elementów do pobrania</span><span class="sxs-lookup"><span data-stu-id="7192c-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="7192c-202">Poniższy przykład tworzy kwerendę, która zwraca pierwsze pięć elementy z PartitionKey "hometasks".</span><span class="sxs-lookup"><span data-stu-id="7192c-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="7192c-203">Ponieważ **wybierz** nie jest używany, zostaną zwrócone wszystkie pola.</span><span class="sxs-lookup"><span data-stu-id="7192c-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="7192c-204">Aby wykonać zapytania dotyczącego tabeli, należy użyć **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="7192c-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="7192c-205">W poniższym przykładzie użyto tego zapytania do zwrócenia jednostek z "mytable".</span><span class="sxs-lookup"><span data-stu-id="7192c-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="7192c-206">W przypadku powodzenia `result.entries` będzie zawierać tablicę jednostki, które pasują do zapytania.</span><span class="sxs-lookup"><span data-stu-id="7192c-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="7192c-207">Jeśli zapytanie nie może zwracać wszystkie jednostki `result.continuationToken` będzie inną niż*null* i mogą być używane jako trzeci parametr funkcji **queryEntities** można pobrać więcej wyników.</span><span class="sxs-lookup"><span data-stu-id="7192c-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="7192c-208">Początkowego zapytania można użyć *null* trzeci parametr.</span><span class="sxs-lookup"><span data-stu-id="7192c-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="7192c-209">Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="7192c-209">Query a subset of entity properties</span></span>
<span data-ttu-id="7192c-210">Zapytanie do tabeli może pobrać kilka pól jednostki.</span><span class="sxs-lookup"><span data-stu-id="7192c-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="7192c-211">To redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="7192c-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="7192c-212">Użyj **wybierz** klauzuli i przekazywać nazwy pól, które ma zostać zwrócona.</span><span class="sxs-lookup"><span data-stu-id="7192c-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="7192c-213">Na przykład poniższe zapytanie zwróci tylko **opis** i **Data ukończenia** pola.</span><span class="sxs-lookup"><span data-stu-id="7192c-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="7192c-214">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="7192c-214">Delete an entity</span></span>
<span data-ttu-id="7192c-215">Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="7192c-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="7192c-216">W tym przykładzie **task1** zawiera obiekt **RowKey** i **PartitionKey** wartości jednostki do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="7192c-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="7192c-217">Następnie obiekt został przekazany do **deleteEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="7192c-217">Then the object is passed to the **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="7192c-218">Należy rozważyć użycie elementy etag podczas usuwania elementów, aby upewnić się, że element nie została zmodyfikowana przez inny proces.</span><span class="sxs-lookup"><span data-stu-id="7192c-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="7192c-219">Zobacz [Aktualizuj jednostkę](#update-an-entity) informacji na temat używania elementy ETag.</span><span class="sxs-lookup"><span data-stu-id="7192c-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="7192c-220">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="7192c-220">Delete a table</span></span>
<span data-ttu-id="7192c-221">Poniższy kod usuwa tabelę z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7192c-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="7192c-222">Jeśli masz pewności, czy tabela istnieje, użyj **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="7192c-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="7192c-223">Używaj tokenów kontynuacji</span><span class="sxs-lookup"><span data-stu-id="7192c-223">Use continuation tokens</span></span>
<span data-ttu-id="7192c-224">Podczas wykonywania zapytań dotyczących tabel w przypadku dużych ilości wyników, należy wyszukać kontynuacji tokenów.</span><span class="sxs-lookup"><span data-stu-id="7192c-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="7192c-225">Mogą być duże ilości danych dostępne dla Twojego zapytania, które mogą nie okazuje się, jeśli nie Kompiluj rozpoznanie token kontynuacji jest obecny.</span><span class="sxs-lookup"><span data-stu-id="7192c-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="7192c-226">Obiekt wyniki zwrócone podczas wykonywania zapytania zestawów jednostek `continuationToken` właściwości, gdy obecny jest takie tokenu.</span><span class="sxs-lookup"><span data-stu-id="7192c-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="7192c-227">Następnie można to podczas wykonywania zapytania w dalszym ciągu porusza się na partycji i tabela jednostek.</span><span class="sxs-lookup"><span data-stu-id="7192c-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="7192c-228">Podczas wykonywania zapytania, między wystąpieniem obiektu zapytania i funkcja wywołania zwrotnego można podać parametru continuationToken:</span><span class="sxs-lookup"><span data-stu-id="7192c-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="7192c-229">Jeśli sprawdzenie `continuationToken` obiektu, można znaleźć właściwości takich jak `nextPartitionKey`, `nextRowKey` i `targetLocation`, które mogą służyć do iterowania po wszystkich wyników.</span><span class="sxs-lookup"><span data-stu-id="7192c-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="7192c-230">Istnieje również kontynuacji próbki w repozytorium Node.js magazynu Azure w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7192c-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="7192c-231">Wyszukaj `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="7192c-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="7192c-232">Praca z sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="7192c-232">Work with shared access signatures</span></span>
<span data-ttu-id="7192c-233">Sygnatury dostępu współdzielonego (SAS) to bezpieczny sposób zapewnienia szczegółowej dostępu do tabel bez podawania Twojej nazwy konta magazynu i klucze.</span><span class="sxs-lookup"><span data-stu-id="7192c-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="7192c-234">Skojarzenia zabezpieczeń są często używane do udzielany ograniczony dostęp do danych, na przykład pozwala aplikacji mobilnej, aby w rekordach zapytań.</span><span class="sxs-lookup"><span data-stu-id="7192c-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="7192c-235">Generuje zaufanych aplikacji, takich jak jest usługą opartą na chmurze przy użyciu sygnatury dostępu Współdzielonego **generateSharedAccessSignature** z **TableService**i udostępnia go do niezaufanych lub częściowo zaufanych aplikacji takich jak aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="7192c-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="7192c-236">Sygnatury dostępu Współdzielonego jest generowany przy użyciu zasad, opisujący daty rozpoczęcia i zakończenia, w których sygnatury dostępu Współdzielonego jest prawidłowy, a także poziom dostępu przyznane posiadacz sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7192c-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="7192c-237">Poniższy przykład generuje nowe zasady dostępu współdzielonego, które umożliwią SAS właścicielowi zapytania ("r") tabeli i wygasa 100 minut po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="7192c-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="7192c-238">Należy pamiętać, że informacje hosta należy podać również, jak jest wymagany, gdy właściciel SAS próbuje uzyskać dostęp w tabeli.</span><span class="sxs-lookup"><span data-stu-id="7192c-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="7192c-239">Następnie aplikacja kliencka używa SAS z **TableServiceWithSAS** wykonywanie operacji względem tabeli.</span><span class="sxs-lookup"><span data-stu-id="7192c-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="7192c-240">Poniższy przykład łączy do tabeli i wykonuje zapytania.</span><span class="sxs-lookup"><span data-stu-id="7192c-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="7192c-241">Ponieważ sygnatury dostępu Współdzielonego został wygenerowany z zapytania dostęp tylko, jeśli zostały podjęta próba Wstawianie, aktualizowanie lub usuwanie jednostek, czy zwracany błąd.</span><span class="sxs-lookup"><span data-stu-id="7192c-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="7192c-242">Listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="7192c-242">Access Control Lists</span></span>
<span data-ttu-id="7192c-243">Listy kontroli dostępu (ACL) umożliwia także ustawić zasady dostępu dla sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7192c-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="7192c-244">Jest to przydatne, jeśli chcesz umożliwić wielu klientów dostępu do tabeli, ale zawiera różne zasady dostępu dla każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="7192c-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="7192c-245">Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="7192c-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="7192c-246">W poniższym przykładzie zdefiniowano dwie zasady, jeden dla "Użytkownik1" i jeden dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="7192c-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="7192c-247">Poniższy przykład pobiera bieżącej listy ACL dla **hometasks** tabeli, a następnie dodanie nowych zasad za pomocą **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="7192c-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="7192c-248">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="7192c-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="7192c-249">Po ustawieniu listy ACL następnie można utworzyć na podstawie Identyfikatora zasady sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7192c-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="7192c-250">Poniższy przykład tworzy nowe sygnatury dostępu Współdzielonego dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="7192c-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="7192c-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7192c-251">Next steps</span></span>
<span data-ttu-id="7192c-252">Aby uzyskać więcej informacji zobacz następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="7192c-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="7192c-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatną aplikacją autonomiczną oferowaną przez firmę Microsoft, która umożliwia wizualną pracę z danymi w usłudze Azure Storage w systemach Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="7192c-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="7192c-254">[Zestaw Azure SDK magazynu dla węzła](https://github.com/Azure/azure-storage-node) repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7192c-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="7192c-255">Centrum deweloperów środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="7192c-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="7192c-256">Tworzenie i wdrażanie aplikacji Node.js do witryny sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7192c-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)