---
title: "aaaAzure rozwiązania Cosmos bazy danych dystrybucji globalne samouczek dotyczący interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API usługi DocumentDB."
services: cosmos-db
keywords: "globalne dystrybucji, z usługi documentdb"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="45e80-104">Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="45e80-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="45e80-105">W tym artykule zostanie przedstawiony sposób toouse hello Azure toosetup portalu Azure DB rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="45e80-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="45e80-106">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="45e80-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="45e80-107">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="45e80-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="45e80-108">Skonfiguruj globalne dystrybucji przy użyciu hello [interfejsów API usługi DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="45e80-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="45e80-109">Łączenie preferowanego regionu tooa przy użyciu hello interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="45e80-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="45e80-110">W kolejności tootake zaletą [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić hello uporządkowana lista preferencji toobe regionów używanych tooperform dokumentu operacji.</span><span class="sxs-lookup"><span data-stu-id="45e80-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="45e80-111">Można to zrobić przez ustawienie hello zasad połączenia.</span><span class="sxs-lookup"><span data-stu-id="45e80-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="45e80-112">Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos hello bieżącej dostępności regionalnych i listy preferencji hello określone, powitalne większości optymalne punkt końcowy zostanie wybrany przez hello tooperform zestawu SDK usługi DocumentDB zapisu i odczytu operacji.</span><span class="sxs-lookup"><span data-stu-id="45e80-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="45e80-113">Ta lista preferencji określono podczas inicjowania połączenia przy użyciu hello zestawów SDK usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="45e80-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="45e80-114">Witaj zestawów SDK zaakceptować opcjonalny parametr "PreferredLocations" oznacza to uporządkowana lista regionów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="45e80-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="45e80-115">Witaj SDK będzie automatycznie wysyłać wszystkie zapisy toohello bieżącego zapisu regionu.</span><span class="sxs-lookup"><span data-stu-id="45e80-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="45e80-116">Wszystkie operacje odczytu zostaną wysłane jako pierwszy dostępny region toohello hello PreferredLocations listy.</span><span class="sxs-lookup"><span data-stu-id="45e80-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="45e80-117">W przypadku niepowodzenia żądania hello powitania klienta się nie powieść w dół listy hello toohello następny region i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="45e80-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="45e80-118">tylko tooread z określonych w PreferredLocations regionów hello zostanie podjęta próba Hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="45e80-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="45e80-119">Tak na przykład, jeśli hello konto bazy danych jest dostępne w trzech regionów, ale powitania klienta tylko określa dwa regiony i do zapisu hello PreferredLocations, następnie odczyty nie zostanie obsłużona poza region zapisu hello, nawet w przypadku hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="45e80-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="45e80-120">aplikacji Hello można Sprawdź hello bieżący punkt końcowy zapisu i odczytu punktu końcowego wybierany przez hello zestawu SDK przez sprawdzanie, czy dwie właściwości WriteEndpoint i ReadEndpoint dostępne w wersji zestawu SDK 1.8 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="45e80-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="45e80-121">Jeśli nie ustawiono właściwości PreferredLocations hello, wszystkie żądania będą udostępniane przez hello bieżący obszar zapisu.</span><span class="sxs-lookup"><span data-stu-id="45e80-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="45e80-122">Zestaw SDK .NET</span><span class="sxs-lookup"><span data-stu-id="45e80-122">.NET SDK</span></span>
<span data-ttu-id="45e80-123">Witaj zestawu SDK można bez wprowadzania żadnych zmian kodu.</span><span class="sxs-lookup"><span data-stu-id="45e80-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="45e80-124">W takim przypadku hello zestawu SDK automatycznie kieruje zarówno odczytuje i zapisuje bieżący obszar zapisu toohello.</span><span class="sxs-lookup"><span data-stu-id="45e80-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="45e80-125">W wersji 1.8 i nowszej hello zestawu .NET SDK hello ConnectionPolicy parametr dla konstruktora DocumentClient hello ma właściwość o nazwie Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="45e80-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="45e80-126">Ta właściwość jest typu kolekcji `<string>` i powinien zawierać listę nazw regionu.</span><span class="sxs-lookup"><span data-stu-id="45e80-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="45e80-127">wartości ciągu Hello są sformatowane w kolumnie Nazwa regionu hello na powitania [regiony platformy Azure] [ regions] strony nie może zawierać spacji przed lub po hello pierwszy i ostatni znak odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="45e80-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="45e80-128">punktów końcowych odczytu i zapisu bieżącego Hello są odpowiednio dostępne w DocumentClient.WriteEndpoint i DocumentClient.ReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="45e80-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="45e80-129">nie należy traktować jako długotrwałe stałe adresy URL Hello hello punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="45e80-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="45e80-130">Usługa Hello może zaktualizować je w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="45e80-130">hello service may update these at any point.</span></span> <span data-ttu-id="45e80-131">Witaj SDK automatycznie obsługuje tę zmianę.</span><span class="sxs-lookup"><span data-stu-id="45e80-131">hello SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="45e80-132">NodeJS, JavaScript i zestawy SDK Python</span><span class="sxs-lookup"><span data-stu-id="45e80-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="45e80-133">Witaj zestawu SDK można bez wprowadzania żadnych zmian kodu.</span><span class="sxs-lookup"><span data-stu-id="45e80-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="45e80-134">W takim przypadku powitalne SDK spowoduje automatyczne kierowanie zarówno odczytuje i zapisuje toohello bieżący obszar zapisu.</span><span class="sxs-lookup"><span data-stu-id="45e80-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="45e80-135">W wersji 1.8 i później każdego zestawu SDK, hello ConnectionPolicy parametr dla konstruktora DocumentClient hello nową właściwość o nazwie DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="45e80-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="45e80-136">Ten parametr jest tablicą ciągów przyjmuje listę nazw regionu.</span><span class="sxs-lookup"><span data-stu-id="45e80-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="45e80-137">nazwy Hello są sformatowane na powitania kolumnę Nazwa regionu w hello [regiony platformy Azure] [ regions] strony.</span><span class="sxs-lookup"><span data-stu-id="45e80-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="45e80-138">Umożliwia także stałe hello wstępnie zdefiniowane w obiekcie wygody hello AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="45e80-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="45e80-139">punktów końcowych odczytu i zapisu bieżącego Hello są odpowiednio dostępne w DocumentClient.getWriteEndpoint i DocumentClient.getReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="45e80-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="45e80-140">nie należy traktować jako długotrwałe stałe adresy URL Hello hello punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="45e80-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="45e80-141">Usługa Hello może zaktualizować je w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="45e80-141">hello service may update these at any point.</span></span> <span data-ttu-id="45e80-142">Witaj SDK zostanie automatycznie obsłużyć tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="45e80-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="45e80-143">Poniżej podano przykładowy kod NodeJS/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="45e80-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="45e80-144">Python i Java zastosują hello tego samego wzorca.</span><span class="sxs-lookup"><span data-stu-id="45e80-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="45e80-145">REST</span><span class="sxs-lookup"><span data-stu-id="45e80-145">REST</span></span>
<span data-ttu-id="45e80-146">Gdy konto bazy danych został udostępniony w wielu regionach, klienci mogą wykonywać kwerendę jego dostępność, wykonując na powitania następującego identyfikatora URI żądania GET.</span><span class="sxs-lookup"><span data-stu-id="45e80-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="45e80-147">Usługa Hello zwróci listę regionów i ich odpowiednich bazy danych Azure rozwiązania Cosmos punktu końcowego identyfikatorów URI dla replik hello.</span><span class="sxs-lookup"><span data-stu-id="45e80-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="45e80-148">bieżący obszar zapisu Hello zostanie wskazany w hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="45e80-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="45e80-149">powitania klienta można wybrać odpowiednie punktu końcowego hello na wszystkie kolejne żądania interfejsu API REST w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="45e80-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="45e80-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="45e80-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="45e80-151">Należy przejść do żądania PUT, POST i DELETE toohello wskazanych zapisu identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="45e80-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="45e80-152">Pobiera wszystkie i inne żądania tylko do odczytu (na przykład kwerendy) może go punktu końcowego tooany wyboru powitania klienta</span><span class="sxs-lookup"><span data-stu-id="45e80-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="45e80-153">Zapis regionów tylko do tooread żądań zakończy się niepowodzeniem z kodem błędu HTTP 403 ("Dostęp zabroniony").</span><span class="sxs-lookup"><span data-stu-id="45e80-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="45e80-154">Jeśli region zapisu hello zmieni się po fazie początkowe wykrywanie powitania klienta, kolejne zapisuje toohello poprzedniego region zapisu zakończy się niepowodzeniem z kodem błędu HTTP 403 ("Dostęp zabroniony").</span><span class="sxs-lookup"><span data-stu-id="45e80-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="45e80-155">powitania klienta należy następnie UZYSKAĆ hello listę regionów ponownie tooget hello zaktualizowane zapisu regionu.</span><span class="sxs-lookup"><span data-stu-id="45e80-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="45e80-156">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="45e80-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="45e80-157">Dowiedz się jak toomanage hello spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="45e80-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="45e80-158">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="45e80-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45e80-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="45e80-159">Next steps</span></span>

<span data-ttu-id="45e80-160">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="45e80-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45e80-161">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="45e80-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="45e80-162">Skonfiguruj globalne dystrybucji przy użyciu hello interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="45e80-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="45e80-163">Można teraz kontynuować toohello następny samouczek toolearn jak toodevelop lokalnie za pomocą hello emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="45e80-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="45e80-164">Opracowywanie lokalnie emulatorze hello</span><span class="sxs-lookup"><span data-stu-id="45e80-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

