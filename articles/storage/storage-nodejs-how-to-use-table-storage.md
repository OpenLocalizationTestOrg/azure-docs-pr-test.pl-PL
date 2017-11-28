---
title: toouse aaaHow magazynu tabel Azure w oprogramowaniu Node.js | Dokumentacja firmy Microsoft
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="5d0bc-103">Jak toouse magazynu tabel Azure w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="5d0bc-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="5d0bc-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5d0bc-104">Overview</span></span>
<span data-ttu-id="5d0bc-105">W tym temacie przedstawiono, jak usługa tooperform typowych scenariuszy przy użyciu hello Azure tabeli w aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="5d0bc-106">Przykłady kodu Hello w tym temacie założono, że masz już aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="5d0bc-107">Aby uzyskać informacje na temat toocreate aplikacji Node.js na platformie Azure, zobacz jedną z poniższych tematów:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="5d0bc-108">Tworzenie aplikacji sieci web Node.js w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5d0bc-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="5d0bc-109">Tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą programu WebMatrix</span><span class="sxs-lookup"><span data-stu-id="5d0bc-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="5d0bc-110">[Tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (przy użyciu programu Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5d0bc-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="5d0bc-111">Konfigurowanie sieci tooaccess aplikacji usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5d0bc-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="5d0bc-112">toouse usługi Azure Storage, należy hello zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="5d0bc-113">Użyj pakietu hello tooinstall węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="5d0bc-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="5d0bc-114">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix) i przejdź do folderu toohello, w której utworzono aplikację.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="5d0bc-115">Typ **magazyn azure instalacji narzędzia npm** w oknie polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="5d0bc-116">Dane wyjściowe polecenia hello jest toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="5d0bc-117">Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="5d0bc-118">Wewnątrz tego folderu znajdują się hello **magazyn azure** pakiet, który zawiera biblioteki hello potrzebny jest magazyn tooaccess.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="5d0bc-119">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="5d0bc-119">Import hello package</span></span>
<span data-ttu-id="5d0bc-120">Dodaj następującego kodu toohello początku hello hello **server.js** plik w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5d0bc-121">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="5d0bc-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="5d0bc-122">Moduł Hello azure odczyta zmiennych środowiskowych hello AZURE\_MAGAZYNU\_konto i AZURE\_MAGAZYNU\_dostępu\_klucz lub AZURE\_MAGAZYNU\_połączenia \_Ciąg tooyour tooconnect informacje wymagane konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="5d0bc-123">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody **TableService**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="5d0bc-124">Na przykład ustawienia zmiennych środowiskowych hello w hello [portalu Azure](https://portal.azure.com) dla witryny sieci Web Azure, zobacz [aplikacji sieci web Node.js w usłudze hello Azure usługa tabel](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="5d0bc-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="5d0bc-125">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="5d0bc-125">Create a table</span></span>
<span data-ttu-id="5d0bc-126">Witaj poniższy kod tworzy **TableService** obiektu i używa go toocreate nową tabelę.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="5d0bc-127">Dodaj następujące hello u góry hello **server.js**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="5d0bc-128">Witaj wywołanie za**createTableIfNotExists** spowoduje utworzenie nowej tabeli o określonej nazwie hello, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="5d0bc-129">Witaj poniższy przykład tworzy nową tabelę o nazwie "mytable", jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="5d0bc-130">Witaj `result.created` będzie `true` Jeśli nowa tabela została utworzona, oraz `false` Jeśli hello tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="5d0bc-131">Witaj `response` będzie zawierać informacje o żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="5d0bc-132">Filtry</span><span class="sxs-lookup"><span data-stu-id="5d0bc-132">Filters</span></span>
<span data-ttu-id="5d0bc-133">Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **TableService**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="5d0bc-134">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="5d0bc-135">Po wykonaniu przetwarzanie wstępne opcje żądania hello, metoda hello musi toocall "dalej", przekazywanie wywołania zwrotnego z powitania po podpisaniu:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="5d0bc-136">W tym wywołania zwrotnego, a po przetworzeniu hello returnObject (hello odpowiedź z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub po prostu Wywołaj finalCallback inaczej hello tooend wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="5d0bc-137">Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="5d0bc-138">tworzy następujące Hello **TableService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="5d0bc-139">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="5d0bc-139">Add an entity tooa table</span></span>
<span data-ttu-id="5d0bc-140">tooadd jednostki, najpierw utwórz obiekt, który definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="5d0bc-141">Musi zawierać wszystkie jednostki **PartitionKey** i **RowKey**, które są unikatowych identyfikatorów dla jednostek hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="5d0bc-142">**PartitionKey** — Określa jednostki hello są przechowywane w partycji hello</span><span class="sxs-lookup"><span data-stu-id="5d0bc-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="5d0bc-143">**RowKey** — unikatowo identyfikuje hello jednostek w partycji hello</span><span class="sxs-lookup"><span data-stu-id="5d0bc-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="5d0bc-144">Zarówno **PartitionKey** i **RowKey** muszą być ciągami.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="5d0bc-145">Aby uzyskać więcej informacji, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d0bc-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="5d0bc-146">Witaj poniżej znajduje się przykład Definiowanie jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="5d0bc-147">Należy pamiętać, że **Data ukończenia** jest zdefiniowana jako typ **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="5d0bc-148">Określanie typu hello jest opcjonalny i typy będzie można wywnioskować, jeśli nie została określona.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="5d0bc-149">Istnieje również **sygnatury czasowej** pola dla każdego rekordu, który jest ustawiony przez platformę Azure, gdy jednostki są wstawiane lub aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="5d0bc-150">Można również użyć hello **entityGenerator** toocreate jednostek.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="5d0bc-151">Witaj poniższy przykład tworzy hello tej samej jednostki zadania przy użyciu hello **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="5d0bc-152">tooadd Tabela tooyour jednostek przekazać hello jednostki obiektu toohello **insertEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="5d0bc-153">Jeśli hello operacja się powiodła, `result` będzie zawierać hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) z hello dodaje rekord i `response` będzie zawierać informacje na temat operacji hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="5d0bc-154">Przykład odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="5d0bc-155">Domyślnie **insertEntity** nie zwraca jednostek hello wstawiony jako część hello `response` informacji.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="5d0bc-156">Jeśli planowane jest wykonywanie innych operacji w tej jednostce, lub chcesz informacji hello toocache, może być przydatne toohave zwrócony jako część hello `result`.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="5d0bc-157">Można to zrobić przez włączenie **echoContent** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="5d0bc-158">Aktualizuj jednostkę</span><span class="sxs-lookup"><span data-stu-id="5d0bc-158">Update an entity</span></span>
<span data-ttu-id="5d0bc-159">Istnieje wiele metod tooupdate dostępne istniejącego obiektu:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="5d0bc-160">**replaceEntity** -aktualizacji przez zastąpienie istniejącej jednostki</span><span class="sxs-lookup"><span data-stu-id="5d0bc-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="5d0bc-161">**mergeEntity** — aktualizuje istniejące jednostki przez scalenie nowej wartości właściwości istniejącej jednostki hello</span><span class="sxs-lookup"><span data-stu-id="5d0bc-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="5d0bc-162">**insertOrReplaceEntity** -aktualizacji przez zastąpienie istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="5d0bc-163">Jeśli jednostka nie istnieje, zostanie wstawiony nowy</span><span class="sxs-lookup"><span data-stu-id="5d0bc-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="5d0bc-164">**insertOrMergeEntity** -aktualizacji przez scalenie istniejących hello nowej wartości właściwości istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="5d0bc-165">Jeśli jednostka nie istnieje, zostanie wstawiony nowy</span><span class="sxs-lookup"><span data-stu-id="5d0bc-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="5d0bc-166">Witaj poniższym przykładzie pokazano aktualizowanie jednostki przy użyciu **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="5d0bc-167">Domyślnie aktualizowania jednostki nie sprawdza toosee Jeśli danych hello aktualizowana wcześniej został zmodyfikowany przez inny proces.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="5d0bc-168">toosupport równoczesnych aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="5d0bc-169">Pobierz hello ETag aktualizowany obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="5d0bc-170">Ten błąd jest zwracany jako część hello `response` do żadnej operacji powiązanych jednostek i mogą zostać pobrane za pośrednictwem `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="5d0bc-171">Podczas wykonywania operacji update na jednostkę, Dodaj hello ETag pobrać informacji o wcześniej toohello nowej jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="5d0bc-172">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-172">For example:</span></span>
>
>       <span data-ttu-id="5d0bc-173">entity2 .etag [.metadata] = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="5d0bc-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="5d0bc-174">Wykonaj operację aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-174">Perform hello update operation.</span></span> <span data-ttu-id="5d0bc-175">Jeśli jednostka hello został zmodyfikowany od czasu pobrania hello wartość ETag, takich jak inne wystąpienie aplikacji, `error` zostaną zwrócone z informacją hello aktualizacji warunek określony w żądaniu hello nie był spełniony.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="5d0bc-176">Z **replaceEntity** i **mergeEntity**, jeśli hello jednostki, która jest aktualizowana nie istnieje, operacja aktualizacji hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="5d0bc-177">Dlatego w razie potrzeby toostore jednostki niezależnie od tego, czy istnieje już używać **insertOrReplaceEntity** lub **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="5d0bc-178">Witaj `result` aktualizacji pomyślnych operacji będzie zawierać hello **Etag** z hello aktualizacji jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="5d0bc-179">Praca z grupami jednostek</span><span class="sxs-lookup"><span data-stu-id="5d0bc-179">Work with groups of entities</span></span>
<span data-ttu-id="5d0bc-180">Czasami powoduje toosubmit znaczeniu wiele operacji razem w tooensure partii przetwarzania przez serwer hello atomic.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="5d0bc-181">tooaccomplish, który Użyj hello **TableBatch** klasy toocreate partii, a następnie użyć hello **executeBatch** metody **TableService** tooperform hello umieścić w zadaniu wsadowym operacji.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="5d0bc-182">Witaj poniższy przykład przedstawia przesyłanie dwie jednostki w partii:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
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

<span data-ttu-id="5d0bc-183">Dla operacji wsadowych pomyślne `result` będzie zawierać informacje dla każdej operacji w partii hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="5d0bc-184">Praca z operacji wsadowych</span><span class="sxs-lookup"><span data-stu-id="5d0bc-184">Work with batched operations</span></span>
<span data-ttu-id="5d0bc-185">Operacje dodane partii tooa mogą być kontrolowane przez wyświetlanie hello `operations` właściwości.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="5d0bc-186">Można także użyć hello następujące metody toowork z operacjami:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="5d0bc-187">**Wyczyść** — usuwa wszystkie operacje z partii</span><span class="sxs-lookup"><span data-stu-id="5d0bc-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="5d0bc-188">**getOperations** -pobiera operację z hello partii</span><span class="sxs-lookup"><span data-stu-id="5d0bc-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="5d0bc-189">**hasOperations** — zwraca wartość true, jeśli hello partia zawiera operacje</span><span class="sxs-lookup"><span data-stu-id="5d0bc-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="5d0bc-190">**removeOperations** — usuwa operacji</span><span class="sxs-lookup"><span data-stu-id="5d0bc-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="5d0bc-191">**rozmiar** — zwraca hello liczba operacji w partii hello</span><span class="sxs-lookup"><span data-stu-id="5d0bc-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="5d0bc-192">Pobrać jednostek według klucza</span><span class="sxs-lookup"><span data-stu-id="5d0bc-192">Retrieve an entity by key</span></span>
<span data-ttu-id="5d0bc-193">określonej jednostki oparte na powitania tooreturn **PartitionKey** i **RowKey**, użyj hello **retrieveEntity** — metoda.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="5d0bc-194">Po zakończeniu tej operacji `result` będzie zawierać hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="5d0bc-195">Zapytanie zestawu jednostek</span><span class="sxs-lookup"><span data-stu-id="5d0bc-195">Query a set of entities</span></span>
<span data-ttu-id="5d0bc-196">tooquery tabelę, użyj hello **TableQuery** obiekt toobuild się przy użyciu powitania po klauzule wyrażenia zapytania:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="5d0bc-197">**Wybierz** -toobe pola hello zwracane z kwerendy hello</span><span class="sxs-lookup"><span data-stu-id="5d0bc-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="5d0bc-198">**gdzie** — Witaj gdzie klauzuli</span><span class="sxs-lookup"><span data-stu-id="5d0bc-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="5d0bc-199">**i** — `and` warunek where</span><span class="sxs-lookup"><span data-stu-id="5d0bc-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="5d0bc-200">**lub** — `or` warunek where</span><span class="sxs-lookup"><span data-stu-id="5d0bc-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="5d0bc-201">**TOP** — Witaj liczbę elementów toofetch</span><span class="sxs-lookup"><span data-stu-id="5d0bc-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="5d0bc-202">Witaj poniższy przykład tworzy kwerendę, która zwróci hello top pięć elementów PartitionKey "hometasks".</span><span class="sxs-lookup"><span data-stu-id="5d0bc-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="5d0bc-203">Ponieważ **wybierz** nie jest używany, zostaną zwrócone wszystkie pola.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="5d0bc-204">tooperform hello zapytania dotyczącego tabeli, użyj **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="5d0bc-205">Witaj poniższym przykładzie użyto jednostek tooreturn tego zapytania z "mytable".</span><span class="sxs-lookup"><span data-stu-id="5d0bc-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="5d0bc-206">W przypadku powodzenia `result.entries` będzie zawierać tablicę jednostek spełniających hello kwerendy.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="5d0bc-207">Jeśli zapytanie hello tooreturn wszystkie jednostki `result.continuationToken` będzie z systemem innym niż*null* i można go używać jako trzeci parametr funkcji hello **queryEntities** tooretrieve więcej wyników.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="5d0bc-208">Witaj początkowego zapytania można użyć *null* dla hello trzeci parametr.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="5d0bc-209">Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="5d0bc-209">Query a subset of entity properties</span></span>
<span data-ttu-id="5d0bc-210">Tabela tooa kwerend może pobrać kilka pól jednostki.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="5d0bc-211">To redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="5d0bc-212">Użyj hello **wybierz** zwrócił klauzuli i przekazać nazwy hello hello toobe pola.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="5d0bc-213">Na przykład hello następującej kwerendy zwróci tylko hello **opis** i **Data ukończenia** pola.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="5d0bc-214">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="5d0bc-214">Delete an entity</span></span>
<span data-ttu-id="5d0bc-215">Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="5d0bc-216">W tym przykładzie hello **task1** obiekt zawiera hello **RowKey** i **PartitionKey** wartości toobe jednostki hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="5d0bc-217">Następnie obiekt hello jest przekazywany toohello **deleteEntity** metody.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

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
> <span data-ttu-id="5d0bc-218">Należy rozważyć użycie elementy etag, gdy usunięcie elementów, tooensure, który hello elementu nie została zmodyfikowana przez inny proces.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="5d0bc-219">Zobacz [Aktualizuj jednostkę](#update-an-entity) informacji na temat używania elementy ETag.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="5d0bc-220">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="5d0bc-220">Delete a table</span></span>
<span data-ttu-id="5d0bc-221">Witaj następującego kodu usuwa tabelę z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="5d0bc-222">Jeśli masz pewności, czy tabela hello istnieje, użyj **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="5d0bc-223">Używaj tokenów kontynuacji</span><span class="sxs-lookup"><span data-stu-id="5d0bc-223">Use continuation tokens</span></span>
<span data-ttu-id="5d0bc-224">Podczas wykonywania zapytań dotyczących tabel w przypadku dużych ilości wyników, należy wyszukać kontynuacji tokenów.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="5d0bc-225">Może istnieć dużych ilości danych dostępne dla tej kwerendy, czy użytkownik może nie należy pamiętać, jeśli nie Konstruuj toorecognize, gdy token kontynuacji jest obecna.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="5d0bc-226">Obiekt Hello wyniki zwrócone podczas wykonywania zapytania zestawów jednostek `continuationToken` właściwości, gdy obecny jest takie tokenu.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="5d0bc-227">Następnie można to podczas przeprowadzania toomove toocontinue zapytania na powitania partycji i tabela jednostek.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="5d0bc-228">Podczas wykonywania zapytania, można podać parametru continuationToken między wystąpienie obiektu hello zapytania i funkcja wywołania zwrotnego hello:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

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

<span data-ttu-id="5d0bc-229">Jeśli inspekcja hello `continuationToken` obiektu, można znaleźć właściwości takich jak `nextPartitionKey`, `nextRowKey` i `targetLocation`, które mogą być używane tooiterate przez wszystkie wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="5d0bc-230">Istnieje również kontynuacji próbki w ramach hello repozytorium Node.js magazynu Azure w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="5d0bc-231">Wyszukaj `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="5d0bc-232">Praca z sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="5d0bc-232">Work with shared access signatures</span></span>
<span data-ttu-id="5d0bc-233">Sygnatury dostępu współdzielonego (SAS) są tootables szczegółowego dostępu tooprovide bezpieczny sposób, bez konieczności podawania Twojej nazwy konta magazynu lub kluczy.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="5d0bc-234">Skojarzenia zabezpieczeń są często używane tooprovide ograniczony dostęp tooyour dane, takie jak stosowanie aplikacji mobilnej tooquery rekordów.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="5d0bc-235">Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnaturę dostępu Współdzielonego przy użyciu hello **generateSharedAccessSignature** z hello **TableService**i udostępnia go tooan niezaufanych lub częściowo zaufanych aplikacji przykład aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="5d0bc-236">Hello sygnatury dostępu Współdzielonego jest generowany przy użyciu zasad, które opisano hello rozpoczęcia i daty zakończenia, podczas których hello SAS jest prawidłowy, a także hello posiadacz SAS toohello nadanego poziomu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="5d0bc-237">Witaj poniższy przykład generuje nowe zasady dostępu współdzielonego, które umożliwią hello SAS posiadacz tooquery (r) hello tabeli i wygasa 100 minut po uruchomieniu hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="5d0bc-238">Należy pamiętać, że informacji o hoście hello należy dostarczyć także zgodnie z wymaganiami podczas posiadacz SAS hello prób tooaccess hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="5d0bc-239">Witaj aplikacji klienckiej, a następnie używa hello SAS z **TableServiceWithSAS** tooperform operacji względem tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="5d0bc-240">Poniższy przykład Hello połączenie tabeli toohello i wykonuje zapytania.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="5d0bc-241">Ponieważ hello wygenerowano sygnaturę dostępu Współdzielonego tylko zapytania dostęp, próba dokonane tooinsert, aktualizowanie lub usuwanie jednostek, czy zwracany błąd.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="5d0bc-242">Listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="5d0bc-242">Access Control Lists</span></span>
<span data-ttu-id="5d0bc-243">Umożliwia także zasad dostępu hello tooset listy kontroli dostępu (ACL) dla sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="5d0bc-244">Jest to przydatne, jeśli chcesz tooallow wielu klientów tooaccess hello tabeli, ale zawiera różne zasady dostępu dla każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="5d0bc-245">Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="5d0bc-246">Poniższy przykład Hello definiuje dwie zasady, jeden dla "Użytkownik1" i jeden dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="5d0bc-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="5d0bc-247">powitania po pobiera przykład Witaj bieżącej listy ACL dla hello **hometasks** tabeli, a następnie dodanie nowych zasad hello przy użyciu **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="5d0bc-248">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="5d0bc-248">This approach allows:</span></span>

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

<span data-ttu-id="5d0bc-249">Raz hello ustawione listy ACL, następnie można utworzyć sygnatury dostępu Współdzielonego na podstawie Identyfikatora hello zasad.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="5d0bc-250">Witaj poniższy przykład powoduje utworzenie nowej sygnatury dostępu Współdzielonego dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="5d0bc-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="5d0bc-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d0bc-251">Next steps</span></span>
<span data-ttu-id="5d0bc-252">Aby uzyskać więcej informacji zobacz następujące zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="5d0bc-253">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="5d0bc-254">[Zestaw Azure SDK magazynu dla węzła](https://github.com/Azure/azure-storage-node) repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d0bc-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="5d0bc-255">Centrum deweloperów środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="5d0bc-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="5d0bc-256">Tworzenie i wdrażanie tooan aplikacji Node.js witryny sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="5d0bc-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
