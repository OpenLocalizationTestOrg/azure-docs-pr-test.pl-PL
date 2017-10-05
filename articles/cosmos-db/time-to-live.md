---
title: "Wygasić dane w usłudze Azure DB rozwiązania Cosmos z czasu wygaśnięcia | Dokumentacja firmy Microsoft"
description: "TTL bazy danych programu Microsoft Azure rozwiązania Cosmos zapewnia możliwość dokumentów automatycznie usunięte z systemu po upływie określonego czasu."
services: cosmos-db
documentationcenter: 
keywords: "czas wygaśnięcia"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="d1a90-104">Ważność danych w kolekcjach bazy danych rozwiązania Cosmos Azure automatycznie z czasu wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="d1a90-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="d1a90-105">Aplikacje można tworzyć i przechowywania dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="d1a90-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="d1a90-106">Niektóre z tych danych, takich jak machine generowane zdarzenie danych, dzienników i użytkownika sesji informacji przydaje się tylko ograniczone okres czasu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="d1a90-107">Gdy dane będą nadwyżka na potrzeby aplikacji jest bezpieczne przeczyścić tych danych i zmniejszyć wymagania dotyczące magazynu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="d1a90-108">"Czas wygaśnięcia" lub TTL bazy danych programu Microsoft Azure rozwiązania Cosmos zapewnia możliwość dokumentów automatycznie usunięte z bazy danych po upływie określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="d1a90-109">Domyślny czas wygaśnięcia można ustawić na poziomie kolekcji i zastąpiona na podstawie powiązany z dokumentem.</span><span class="sxs-lookup"><span data-stu-id="d1a90-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="d1a90-110">Po ustawieniu TTL domyślnie kolekcji lub na poziomie dokumentu, DB rozwiązania Cosmos automatycznie usunie dokumenty znajdujące się po upływie tego czasu w sekundach od ostatniej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="d1a90-111">Czas wygaśnięcia w bazie danych rozwiązania Cosmos używa przesunięcia względem datę ostatniej modyfikacji dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="d1a90-112">W tym używa `_ts` pola, które znajduje się na każdy dokument.</span><span class="sxs-lookup"><span data-stu-id="d1a90-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="d1a90-113">Pole _ts jest sygnatura czasowa typu unix epoki reprezentujący datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="d1a90-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="d1a90-114">`_ts` Pole jest aktualizowane za każdym razem, gdy dokument zostanie zmodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="d1a90-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="d1a90-115">Zachowanie TTL</span><span class="sxs-lookup"><span data-stu-id="d1a90-115">TTL behavior</span></span>
<span data-ttu-id="d1a90-116">Funkcja czas wygaśnięcia jest kontrolowana przez właściwości TTL na dwa poziomy - poziomem kolekcji i dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="d1a90-117">Wartości są ustawiane w sekundach i są traktowane jako różnicowej z `_ts` czy dokument został ostatnio zmodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="d1a90-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="d1a90-118">DefaultTTL dla kolekcji</span><span class="sxs-lookup"><span data-stu-id="d1a90-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="d1a90-119">Jeśli brakuje (lub ustawionej na wartość null), dokumenty nie są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="d1a90-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="d1a90-120">Jeśli obecny i wartość to "-1" = nieskończone — dokumenty nie wygasa domyślnie</span><span class="sxs-lookup"><span data-stu-id="d1a90-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="d1a90-121">Jeśli jest obecny i wartość jest niektórych numer ("n") — dokumenty wygasają "n" sekundach od ostatniej modyfikacji</span><span class="sxs-lookup"><span data-stu-id="d1a90-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="d1a90-122">Czas wygaśnięcia dokumentów:</span><span class="sxs-lookup"><span data-stu-id="d1a90-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="d1a90-123">Właściwość ma zastosowanie, tylko wtedy, gdy dla kolekcji nadrzędnej DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="d1a90-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="d1a90-124">Zastępuje wartość DefaultTTL dla kolekcji nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="d1a90-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="d1a90-125">Jak wygasł dokumentu (`ttl`  +  `_ts` > = bieżący czas serwera), dokument jest oznaczony jako "wygasł".</span><span class="sxs-lookup"><span data-stu-id="d1a90-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="d1a90-126">Żadna operacja będą dozwolone na tych dokumentów po upływie tego czasu i będzie można wykluczyć z wyników kwerendy wykonywane.</span><span class="sxs-lookup"><span data-stu-id="d1a90-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="d1a90-127">Dokumenty są fizycznie usunięte z systemu i są usuwane w tle używana w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="d1a90-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="d1a90-128">To nie zużywa żadnego [jednostek żądania (RUs)](request-units.md) z budżetu kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="d1a90-129">W poniższej tabeli można pokazać logiki powyżej:</span><span class="sxs-lookup"><span data-stu-id="d1a90-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="d1a90-130">DefaultTTL Brak nie ustawiać kolekcji</span><span class="sxs-lookup"><span data-stu-id="d1a90-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="d1a90-131">DefaultTTL = -1 w kolekcji</span><span class="sxs-lookup"><span data-stu-id="d1a90-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="d1a90-132">DefaultTTL = "n" w kolekcji</span><span class="sxs-lookup"><span data-stu-id="d1a90-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="d1a90-133">Brak TTL dokumentu</span><span class="sxs-lookup"><span data-stu-id="d1a90-133">TTL Missing on document</span></span> |<span data-ttu-id="d1a90-134">Nie można zastąpić na poziomie dokumentu, ponieważ dokumentu i kolekcji nie ma żadnych koncepcji TTL.</span><span class="sxs-lookup"><span data-stu-id="d1a90-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="d1a90-135">Wygaśnie żaden dokument w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="d1a90-136">Dokumenty w tej kolekcji wygaśnie po upływie interwału n.</span><span class="sxs-lookup"><span data-stu-id="d1a90-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="d1a90-137">Czas wygaśnięcia = -1 do dokumentu</span><span class="sxs-lookup"><span data-stu-id="d1a90-137">TTL = -1 on document</span></span> |<span data-ttu-id="d1a90-138">Nie można zastąpić na poziomie dokumentu od kolekcji nie zdefiniowano Właściwość DefaultTTL, którą można zastąpić dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="d1a90-139">Wartość TTL dokumentu jest nie interpretowany przez system.</span><span class="sxs-lookup"><span data-stu-id="d1a90-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="d1a90-140">Wygaśnie żaden dokument w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="d1a90-141">Nigdy nie wygasa dokument z = TTL-1 w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="d1a90-142">Wszystkie inne dokumenty wygaśnie po upływie interwału "n".</span><span class="sxs-lookup"><span data-stu-id="d1a90-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="d1a90-143">Czas wygaśnięcia = n dokumentu</span><span class="sxs-lookup"><span data-stu-id="d1a90-143">TTL = n on document</span></span> |<span data-ttu-id="d1a90-144">Nie można zastąpić na poziomie dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-144">Nothing to override at the document level.</span></span> <span data-ttu-id="d1a90-145">Wartość TTL dokumentu nie interpretowany przez system.</span><span class="sxs-lookup"><span data-stu-id="d1a90-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="d1a90-146">Dokument z TTL = n wygaśnie po n interwał, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="d1a90-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="d1a90-147">Inne dokumenty będą dziedziczyć interwał-1 i nigdy nie wygasa.</span><span class="sxs-lookup"><span data-stu-id="d1a90-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="d1a90-148">Dokument z TTL = n wygaśnie po n interwał, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="d1a90-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="d1a90-149">Inne dokumenty będzie dziedziczyć interwał "n" z kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="d1a90-150">Konfigurowanie TTL</span><span class="sxs-lookup"><span data-stu-id="d1a90-150">Configuring TTL</span></span>
<span data-ttu-id="d1a90-151">Domyślnie czas wygaśnięcia jest domyślnie wyłączona, we wszystkich zbiorach DB rozwiązania Cosmos i na wszystkich dokumentach.</span><span class="sxs-lookup"><span data-stu-id="d1a90-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="d1a90-152">Włączanie TTL</span><span class="sxs-lookup"><span data-stu-id="d1a90-152">Enabling TTL</span></span>
<span data-ttu-id="d1a90-153">Włącz TTL kolekcji lub dokumentów w kolekcji, należy ustawić właściwość DefaultTTL kolekcji -1 lub liczbą dodatnią inną niż zero.</span><span class="sxs-lookup"><span data-stu-id="d1a90-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="d1a90-154">Ustawienie DefaultTTL-1 oznacza domyślne wszystkich dokumentów w kolekcji, zawsze na żywo, ale usługa DB rozwiązania Cosmos monitorować tej kolekcji dokumentów, które zostały zastąpione to ustawienie domyślne.</span><span class="sxs-lookup"><span data-stu-id="d1a90-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="d1a90-155">Konfigurowanie domyślny czas wygaśnięcia w kolekcji</span><span class="sxs-lookup"><span data-stu-id="d1a90-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="d1a90-156">Jesteś w stanie skonfigurować domyślny czas wygaśnięcia na poziomie kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="d1a90-157">Aby ustawić czas wygaśnięcia w kolekcji, należy podać liczbą dodatnią niezerowa wskazuje okres, w sekundach, wygaśnie wszystkich dokumentów w kolekcji po jego ostatniej modyfikacji sygnatury czasowej dokumentu (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="d1a90-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="d1a90-158">Alternatywnie można ustawić wartość domyślna -1, co oznacza, że wszystkie dokumenty wstawione do kolekcji będzie domyślnie funkcjonować w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="d1a90-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="d1a90-159">Ustawienie TTL w dokumencie</span><span class="sxs-lookup"><span data-stu-id="d1a90-159">Setting TTL on a document</span></span>
<span data-ttu-id="d1a90-160">Poza ustawieniem domyślny czas wygaśnięcia w kolekcji można ustawić TTL określonych na poziomie dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="d1a90-161">W ten sposób zastępują domyślne w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="d1a90-162">Aby ustawić czas wygaśnięcia dokument, musisz podać liczbą dodatnią inną niż zero, co oznacza okres, w sekundach, wygaśnie dokumentu po jego ostatniej modyfikacji sygnatury czasowej dokumentu (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="d1a90-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="d1a90-163">Jeśli dokument nie zawiera TTL pola, domyślnej kolekcji zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="d1a90-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="d1a90-164">Jeśli czas wygaśnięcia jest wyłączona na poziomie kolekcji, pola TTL dokumentu zostanie zignorowany, aż do ponownego włączenia TTL w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="d1a90-165">Oto fragment przedstawiający sposób ustawiania wygaśnięcia TTL w dokumencie:</span><span class="sxs-lookup"><span data-stu-id="d1a90-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="d1a90-166">Rozszerzanie TTL na istniejącego dokumentu</span><span class="sxs-lookup"><span data-stu-id="d1a90-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="d1a90-167">Wartość TTL dokumentu można zresetować wykonując żadnej operacji zapisu w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="d1a90-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="d1a90-168">Spowoduje to ustawi `_ts` bieżący czas i odlicza czas do wygaśnięcia dokumentu, zgodnie z ustawieniami `ttl`, rozpocznie się ponownie.</span><span class="sxs-lookup"><span data-stu-id="d1a90-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="d1a90-169">Jeśli chcesz zmienić `ttl` dokumentu, można zaktualizować pola, jak mogą z innego pola można ustawić.</span><span class="sxs-lookup"><span data-stu-id="d1a90-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="d1a90-170">Usuwanie TTL z dokumentu</span><span class="sxs-lookup"><span data-stu-id="d1a90-170">Removing TTL from a document</span></span>
<span data-ttu-id="d1a90-171">Jeśli wartości TTL został ustawiony w dokumencie i nie ma już ten dokument wygasa, następnie można pobrać dokumentu, usuń pola TTL i zastąpić dokument na serwerze.</span><span class="sxs-lookup"><span data-stu-id="d1a90-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="d1a90-172">Pola TTL zostanie usunięty z dokumentu, zostaną zastosowane domyślne w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="d1a90-173">Aby zatrzymać dokumentu z wygasa i nie dziedziczy z kolekcji należy ustawić wartość TTL-1.</span><span class="sxs-lookup"><span data-stu-id="d1a90-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="d1a90-174">Wyłączanie TTL</span><span class="sxs-lookup"><span data-stu-id="d1a90-174">Disabling TTL</span></span>
<span data-ttu-id="d1a90-175">Wyłączenie TTL całkowicie w kolekcji i zatrzymać proces w tle z wyszukiwanie wygasłe dokumenty Właściwość DefaultTTL w kolekcji należy go usunąć.</span><span class="sxs-lookup"><span data-stu-id="d1a90-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="d1a90-176">Usunięcie tej właściwości jest inna niż ustawieniem dla niego wartość -1.</span><span class="sxs-lookup"><span data-stu-id="d1a90-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="d1a90-177">Ustawienie, aby nowe dokumenty-1 oznacza dodać do kolekcji, zawsze na żywo, ale można zmienić na określonych dokumentów w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a90-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="d1a90-178">Usunięcie tej właściwości całkowicie z kolekcji oznacza, że żaden dokument wygaśnie, nawet jeśli istnieją dokumenty, które zostały jawnie przesłonięte wcześniejszy domyślny.</span><span class="sxs-lookup"><span data-stu-id="d1a90-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="d1a90-179">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="d1a90-179">FAQ</span></span>
<span data-ttu-id="d1a90-180">**Co to jest czas wygaśnięcia koszt mnie?**</span><span class="sxs-lookup"><span data-stu-id="d1a90-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="d1a90-181">Nie ma żadnych dodatkowych kosztów do ustawiania wartości TTL w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="d1a90-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="d1a90-182">**Jak długo trwa usuwanie dokumentu po czas wygaśnięcia jest uruchomiony?**</span><span class="sxs-lookup"><span data-stu-id="d1a90-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="d1a90-183">Dokumenty są wygasł natychmiast po czas wygaśnięcia jest uruchomiony i nie będzie dostępny za pośrednictwem CRUD lub kwerendy interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="d1a90-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="d1a90-184">**Zostanie TTL w dokumencie miały wpływu na RU opłat**</span><span class="sxs-lookup"><span data-stu-id="d1a90-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="d1a90-185">Nie, nie będzie bez wpływu na RU opłat za usunięcia wygasłych dokumentów za pomocą TTL w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d1a90-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="d1a90-186">**Funkcja TTL tylko dotyczy całego dokumenty lub pojedynczy dokument wartości właściwości mogą wygaśnie?**</span><span class="sxs-lookup"><span data-stu-id="d1a90-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="d1a90-187">Czas wygaśnięcia ma zastosowanie do całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-187">TTL applies to the entire document.</span></span> <span data-ttu-id="d1a90-188">Jeśli chcesz tylko części dokumentu wygaśnie, następnie zalecane jest aby wyodrębnić część z głównego dokumentu w oddzielnych "połączony" dokument, a następnie użyć TTL na wyodrębnione dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d1a90-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="d1a90-189">**Funkcja TTL ma szczególne wymagania indeksowania?**</span><span class="sxs-lookup"><span data-stu-id="d1a90-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="d1a90-190">Tak.</span><span class="sxs-lookup"><span data-stu-id="d1a90-190">Yes.</span></span> <span data-ttu-id="d1a90-191">Kolekcja musi mieć [indeksowania zestawu zasad](indexing-policies.md) spójność lub opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="d1a90-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="d1a90-192">Ustawiany DefaultTTL w kolekcji z indeksowania zestaw None spowoduje błąd, podobnie jak w trakcie wyłączyć indeksowanie w kolekcji, której DefaultTTL został już ustawiony.</span><span class="sxs-lookup"><span data-stu-id="d1a90-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1a90-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1a90-193">Next steps</span></span>
<span data-ttu-id="d1a90-194">Aby dowiedzieć się więcej na temat bazy danych Azure rozwiązania Cosmos, zapoznaj się z usługą [ *dokumentacji* ](https://azure.microsoft.com/documentation/services/cosmos-db/) strony.</span><span class="sxs-lookup"><span data-stu-id="d1a90-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

