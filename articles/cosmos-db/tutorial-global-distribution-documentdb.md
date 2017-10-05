---
title: "Samouczek usługi Azure DB rozwiązania Cosmos dystrybucji globalne dla interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować bazy danych Azure rozwiązania Cosmos dystrybucji globalnego przy użyciu interfejsu API usługi DocumentDB."
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="04f2f-104">Konfigurowanie bazy danych Azure rozwiązania Cosmos dystrybucji globalnego przy użyciu interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="04f2f-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="04f2f-105">W tym artykule zostanie przedstawiony sposób instalacji bazy danych Azure rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu interfejsu API usługi DocumentDB za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="04f2f-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="04f2f-106">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="04f2f-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="04f2f-107">Skonfiguruj globalne dystrybucji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="04f2f-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="04f2f-108">Skonfigurować globalne dystrybucji za pomocą [interfejsów API usługi DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="04f2f-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="04f2f-109">Łączenie z preferowanego regionu przy użyciu interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="04f2f-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="04f2f-110">Aby korzystać z [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić listy uporządkowanej preferencji regionów ma być używany do wykonywania operacji dokumentu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="04f2f-111">Można to zrobić przez ustawienie zasad połączenia.</span><span class="sxs-lookup"><span data-stu-id="04f2f-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="04f2f-112">Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos, bieżącej dostępności regionalnych i na liście preferencji określone, optymalny punkt końcowy zostanie wybrany przez zestaw SDK usługi DocumentDB do wykonywania zapisu i operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="04f2f-113">Ta lista preferencji został określony podczas inicjowania połączenia przy użyciu zestawów SDK usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="04f2f-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="04f2f-114">Zestawy SDK zaakceptować opcjonalny parametr "PreferredLocations" oznacza to uporządkowana lista regionów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="04f2f-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="04f2f-115">Zestaw SDK będzie automatycznie wysyłać zapisuje wszystkie dane w bieżącej zapisu regionu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="04f2f-116">Wszystkie operacje odczytu zostaną wysłane do pierwszy dostępny region na liście PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="04f2f-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="04f2f-117">Jeśli żądanie kończy się niepowodzeniem, klient się nie powieść w dół na liście, aby następny region i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="04f2f-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="04f2f-118">Zestawy SDK podejmie próbę odczytu z określonych w PreferredLocations regionów.</span><span class="sxs-lookup"><span data-stu-id="04f2f-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="04f2f-119">Tak na przykład, jeśli konto bazy danych jest dostępne w trzech regionów, ale klient tylko określa dwóch regionach i do zapisu dla PreferredLocations, następnie odczyty nie zostanie obsłużona poza region zapisu, nawet w przypadku pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="04f2f-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="04f2f-120">Aplikacja może sprawdź bieżący punkt końcowy zapisu i odczytu punktu końcowego wybrany przez zestaw SDK, sprawdzając dwie właściwości WriteEndpoint i ReadEndpoint dostępne w wersji zestawu SDK 1.8 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="04f2f-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="04f2f-121">Jeśli nie ustawiono właściwości PreferredLocations, zostanie obsłużona wszystkie żądania z bieżącego obszaru zapisu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="04f2f-122">Zestaw SDK .NET</span><span class="sxs-lookup"><span data-stu-id="04f2f-122">.NET SDK</span></span>
<span data-ttu-id="04f2f-123">Zestaw SDK może służyć bez wprowadzania żadnych zmian kodu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="04f2f-124">W takim przypadku zestawu SDK automatycznie kieruje zarówno odczytuje i zapisuje bieżący obszar zapisu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="04f2f-125">W wersji 1.8 i później zestawu .NET SDK parametr ConnectionPolicy dla konstruktora DocumentClient ma właściwość o nazwie Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="04f2f-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="04f2f-126">Ta właściwość jest typu kolekcji `<string>` i powinien zawierać listę nazw regionu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="04f2f-127">Ciągi sformatowane w kolumnie Nazwa regionu na [regiony platformy Azure] [ regions] strony nie może zawierać spacji przed lub po pierwszy i ostatni znak odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="04f2f-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="04f2f-128">Bieżący zapisu i odczytu punkty końcowe są odpowiednio dostępne w DocumentClient.WriteEndpoint i DocumentClient.ReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="04f2f-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="04f2f-129">Nie należy traktować jako długotrwałe stałe adresy URL punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="04f2f-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="04f2f-130">Usługa może aktualizować je w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="04f2f-130">The service may update these at any point.</span></span> <span data-ttu-id="04f2f-131">Zestaw SDK obsługuje automatycznie tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="04f2f-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="04f2f-132">NodeJS, JavaScript i zestawy SDK Python</span><span class="sxs-lookup"><span data-stu-id="04f2f-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="04f2f-133">Zestaw SDK może służyć bez wprowadzania żadnych zmian kodu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="04f2f-134">W takim przypadku zestawu SDK będą automatycznie bezpośrednie, odczytów i zapisów do bieżącego zapisu regionu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="04f2f-135">W wersji 1.8 i nowszych każdego zestawu SDK, ConnectionPolicy parametr dla konstruktora DocumentClient nową właściwość o nazwie DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="04f2f-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="04f2f-136">Ten parametr jest tablicą ciągów przyjmuje listę nazw regionu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="04f2f-137">Nazwy są sformatowane w kolumnie Nazwa regionu w [regiony platformy Azure] [ regions] strony.</span><span class="sxs-lookup"><span data-stu-id="04f2f-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="04f2f-138">Umożliwia także stałe wstępnie zdefiniowane w obiekcie wygody AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="04f2f-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="04f2f-139">Bieżący zapisu i odczytu punkty końcowe są odpowiednio dostępne w DocumentClient.getWriteEndpoint i DocumentClient.getReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="04f2f-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="04f2f-140">Nie należy traktować jako długotrwałe stałe adresy URL punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="04f2f-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="04f2f-141">Usługa może aktualizować je w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="04f2f-141">The service may update these at any point.</span></span> <span data-ttu-id="04f2f-142">Zestaw SDK zostanie automatycznie obsłużyć tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="04f2f-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="04f2f-143">Poniżej podano przykładowy kod NodeJS/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="04f2f-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="04f2f-144">Python i Java są zgodne z tego samego wzorca.</span><span class="sxs-lookup"><span data-stu-id="04f2f-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="04f2f-145">REST</span><span class="sxs-lookup"><span data-stu-id="04f2f-145">REST</span></span>
<span data-ttu-id="04f2f-146">Gdy konto bazy danych został udostępniony w wielu regionach, klienci mogą wykonywać kwerendę jego dostępność, wykonując na następujący identyfikator URI żądania GET.</span><span class="sxs-lookup"><span data-stu-id="04f2f-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="04f2f-147">Usługa zwróci listę regionów i ich odpowiednich bazy danych Azure rozwiązania Cosmos punktu końcowego identyfikatorów URI dla replik.</span><span class="sxs-lookup"><span data-stu-id="04f2f-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="04f2f-148">Bieżący obszar zapisu zostanie wskazany w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="04f2f-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="04f2f-149">Klient może następnie wybrać odpowiednie punktu końcowego wszystkie kolejne żądania interfejsu API REST w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="04f2f-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="04f2f-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="04f2f-150">Example response</span></span>

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


* <span data-ttu-id="04f2f-151">Przejdź do zapisu wskazany identyfikator URI żądania PUT, POST i DELETE</span><span class="sxs-lookup"><span data-stu-id="04f2f-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="04f2f-152">Pobiera wszystkie i inne żądania tylko do odczytu (na przykład kwerendy) może go do dowolnego punktu końcowego wybór klienta</span><span class="sxs-lookup"><span data-stu-id="04f2f-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="04f2f-153">Zapisu żądania do regionów tylko do odczytu zakończy się niepowodzeniem z kodem błędu HTTP 403 ("Dostęp zabroniony").</span><span class="sxs-lookup"><span data-stu-id="04f2f-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="04f2f-154">Jeśli region zapisu zmieni się po fazie początkowe wykrywanie klienta, kolejnych zapisów do poprzedniego regionu zapisu zakończy się niepowodzeniem z kodem błędu HTTP 403 ("Dostęp zabroniony").</span><span class="sxs-lookup"><span data-stu-id="04f2f-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="04f2f-155">Klienta, należy UZYSKAĆ listę regionów ponownie, aby pobrać regionu zaktualizowane zapisu.</span><span class="sxs-lookup"><span data-stu-id="04f2f-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="04f2f-156">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="04f2f-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="04f2f-157">Znajdują się informacje dotyczące zarządzania spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="04f2f-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="04f2f-158">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="04f2f-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04f2f-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04f2f-159">Next steps</span></span>

<span data-ttu-id="04f2f-160">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="04f2f-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04f2f-161">Skonfiguruj globalne dystrybucji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="04f2f-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="04f2f-162">Skonfiguruj globalne dystrybucji przy użyciu interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="04f2f-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="04f2f-163">Możesz teraz przejść do następnym samouczku, aby dowiedzieć się, jak opracowywać lokalnie przy użyciu emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="04f2f-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04f2f-164">Opracowywanie lokalnie w emulatorze</span><span class="sxs-lookup"><span data-stu-id="04f2f-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

