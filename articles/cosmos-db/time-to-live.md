---
title: "aaaExpire danych w usłudze Azure DB rozwiązania Cosmos z czasem toolive | Dokumentacja firmy Microsoft"
description: "TTL bazy danych programu Microsoft Azure rozwiązania Cosmos zawiera dokumenty toohave możliwości hello automatycznie usunięte z systemu hello po upływie określonego czasu."
services: cosmos-db
documentationcenter: 
keywords: czas toolive
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
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="b79a0-104">Ważność danych w kolekcjach bazy danych rozwiązania Cosmos Azure automatycznie z czasem toolive</span><span class="sxs-lookup"><span data-stu-id="b79a0-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="b79a0-105">Aplikacje można tworzyć i przechowywania dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="b79a0-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="b79a0-106">Niektóre z tych danych, takich jak machine generowane zdarzenie danych, dzienników i użytkownika sesji informacji przydaje się tylko ograniczone okres czasu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="b79a0-107">Po hello danych staje się toohello nadmierne wymagania dotyczące aplikacji hello jest bezpieczne toopurge tych danych i zmniejszyć wymagania dotyczące magazynu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="b79a0-108">"Czas toolive" lub TTL bazy danych programu Microsoft Azure rozwiązania Cosmos zawiera dokumenty toohave możliwości hello automatycznie usunięte z bazy danych powitania po upływie określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="b79a0-109">Hello domyślny czas toolive można ustawić na poziomie kolekcji hello i zastąpiona na podstawie powiązany z dokumentem.</span><span class="sxs-lookup"><span data-stu-id="b79a0-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="b79a0-110">Po ustawieniu TTL domyślnie kolekcji lub na poziomie dokumentu, DB rozwiązania Cosmos automatycznie usunie dokumenty znajdujące się po upływie tego czasu w sekundach od ostatniej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="b79a0-111">Czas toolive w bazie danych rozwiązania Cosmos używa przesunięcia względem datę ostatniej modyfikacji hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="b79a0-112">toodo hello używa tego `_ts` pola, które znajduje się na każdy dokument.</span><span class="sxs-lookup"><span data-stu-id="b79a0-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="b79a0-113">Witaj _ts pole jest typu unix epoki sygnatury czasowej reprezentujące hello daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="b79a0-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="b79a0-114">Witaj `_ts` pole jest aktualizowane za każdym razem, gdy dokument zostanie zmodyfikowany.</span><span class="sxs-lookup"><span data-stu-id="b79a0-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="b79a0-115">Zachowanie TTL</span><span class="sxs-lookup"><span data-stu-id="b79a0-115">TTL behavior</span></span>
<span data-ttu-id="b79a0-116">Funkcja TTL Hello jest kontrolowana przez właściwości TTL na dwa poziomy - hello poziom kolekcji i dokumentu hello.</span><span class="sxs-lookup"><span data-stu-id="b79a0-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="b79a0-117">Witaj wartości są ustawiane w sekundach i są traktowane jako różnicowej z hello `_ts` w ostatniej modyfikacji tego dokumentu hello.</span><span class="sxs-lookup"><span data-stu-id="b79a0-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="b79a0-118">DefaultTTL hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="b79a0-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="b79a0-119">Jeśli brakuje (lub zestaw toonull) dokumenty nie są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="b79a0-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="b79a0-120">Jeśli jest obecny i -"1" jest wartość hello = nieskończone — dokumenty nie wygasa domyślnie</span><span class="sxs-lookup"><span data-stu-id="b79a0-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="b79a0-121">Jeśli jest obecny i wartość hello jest liczbą, niektóre ("n") — dokumenty wygasają "n" sekundach od ostatniej modyfikacji</span><span class="sxs-lookup"><span data-stu-id="b79a0-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="b79a0-122">Czas wygaśnięcia dokumentów hello:</span><span class="sxs-lookup"><span data-stu-id="b79a0-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="b79a0-123">Właściwość ma zastosowanie, tylko wtedy, gdy dla kolekcji nadrzędnej hello DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="b79a0-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="b79a0-124">Zastępuje wartość DefaultTTL hello hello kolekcji nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="b79a0-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="b79a0-125">Jak wygasł hello dokumentu (`ttl`  +  `_ts` > = bieżący czas serwera), dokument hello jest oznaczony jako "wygasł".</span><span class="sxs-lookup"><span data-stu-id="b79a0-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="b79a0-126">Żadna operacja będą dozwolone na tych dokumentów po upływie tego czasu i zostaną wykluczone z hello wyników kwerendy wykonywane.</span><span class="sxs-lookup"><span data-stu-id="b79a0-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="b79a0-127">dokumenty Hello są fizycznie usunięte w systemie hello i są usuwane w tle hello używana w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="b79a0-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="b79a0-128">To nie zużywa żadnego [jednostek żądania (RUs)](request-units.md) z hello kolekcji budżetu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="b79a0-129">Witaj powyżej logiki można pokazać na powitania po macierzy:</span><span class="sxs-lookup"><span data-stu-id="b79a0-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="b79a0-130">DefaultTTL Brak nie ustawiony na powitania kolekcji</span><span class="sxs-lookup"><span data-stu-id="b79a0-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="b79a0-131">DefaultTTL = -1 w kolekcji</span><span class="sxs-lookup"><span data-stu-id="b79a0-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="b79a0-132">DefaultTTL = "n" w kolekcji</span><span class="sxs-lookup"><span data-stu-id="b79a0-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="b79a0-133">Brak TTL dokumentu</span><span class="sxs-lookup"><span data-stu-id="b79a0-133">TTL Missing on document</span></span> |<span data-ttu-id="b79a0-134">Nic toooverride na poziomie dokumentu, ponieważ dokument hello programu i kolekcji mają nie koncepcji TTL.</span><span class="sxs-lookup"><span data-stu-id="b79a0-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="b79a0-135">Wygaśnie żaden dokument w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="b79a0-136">dokumenty Hello w tej kolekcji wygaśnie po upływie interwału n.</span><span class="sxs-lookup"><span data-stu-id="b79a0-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="b79a0-137">Czas wygaśnięcia = -1 do dokumentu</span><span class="sxs-lookup"><span data-stu-id="b79a0-137">TTL = -1 on document</span></span> |<span data-ttu-id="b79a0-138">Nic toooverride na poziomie dokumentu hello, ponieważ kolekcja hello nie definiuje hello DefaultTTL właściwość, którą można zastąpić dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="b79a0-139">Cofanie interpretowany przez hello system jest czas wygaśnięcia w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="b79a0-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="b79a0-140">Wygaśnie żaden dokument w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="b79a0-141">nigdy nie wygasa Hello dokument z = TTL-1 w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="b79a0-142">Wszystkie inne dokumenty wygaśnie po upływie interwału "n".</span><span class="sxs-lookup"><span data-stu-id="b79a0-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="b79a0-143">Czas wygaśnięcia = n dokumentu</span><span class="sxs-lookup"><span data-stu-id="b79a0-143">TTL = n on document</span></span> |<span data-ttu-id="b79a0-144">Nic toooverride na poziomie dokumentu hello.</span><span class="sxs-lookup"><span data-stu-id="b79a0-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="b79a0-145">Wartość TTL dokumentu nie interpretowany przez hello system.</span><span class="sxs-lookup"><span data-stu-id="b79a0-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="b79a0-146">dokument Hello TTL = n wygaśnie po n interwał, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="b79a0-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="b79a0-147">Inne dokumenty będą dziedziczyć interwał-1 i nigdy nie wygasa.</span><span class="sxs-lookup"><span data-stu-id="b79a0-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="b79a0-148">dokument Hello TTL = n wygaśnie po n interwał, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="b79a0-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="b79a0-149">Inne dokumenty będą dziedziczyć interwał "n" hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="b79a0-150">Konfigurowanie TTL</span><span class="sxs-lookup"><span data-stu-id="b79a0-150">Configuring TTL</span></span>
<span data-ttu-id="b79a0-151">Domyślnie czas toolive jest domyślnie wyłączona, we wszystkich zbiorach DB rozwiązania Cosmos i na wszystkich dokumentach.</span><span class="sxs-lookup"><span data-stu-id="b79a0-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="b79a0-152">Włączanie TTL</span><span class="sxs-lookup"><span data-stu-id="b79a0-152">Enabling TTL</span></span>
<span data-ttu-id="b79a0-153">tooenable TTL na kolekcję lub hello dokumentów w kolekcji należy tooset hello DefaultTTL właściwości kolekcji tooeither -1 lub liczbą dodatnią inną niż zero.</span><span class="sxs-lookup"><span data-stu-id="b79a0-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="b79a0-154">Ustawienie hello DefaultTTL zbyt-1 oznacza, że domyślnie wszystkie dokumenty w kolekcji hello będzie funkcjonować w nieskończoność, ale hello usługi rozwiązania Cosmos bazy danych należy monitorować tej kolekcji dokumentów, które zostały zastąpione to ustawienie domyślne.</span><span class="sxs-lookup"><span data-stu-id="b79a0-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="b79a0-155">Konfigurowanie domyślny czas wygaśnięcia w kolekcji</span><span class="sxs-lookup"><span data-stu-id="b79a0-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="b79a0-156">Jesteś tooconfigure stanie domyślny czas toolive na poziomie kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="b79a0-157">Witaj tooset TTL w kolekcji, należy tooprovide liczbą dodatnią niezerowa wskazuje w sekundach, tooexpire czasu hello wszystkich dokumentów w kolekcji powitania po hello ostatniej modyfikacji sygnatury czasowej hello dokumentu (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="b79a0-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="b79a0-158">Lub możesz ustawić hello domyślne zbyt-1, co oznacza, że wszystkie dokumenty wstawione w kolekcji toohello będzie funkcjonować nieskończoność domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b79a0-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="b79a0-159">Ustawienie TTL w dokumencie</span><span class="sxs-lookup"><span data-stu-id="b79a0-159">Setting TTL on a document</span></span>
<span data-ttu-id="b79a0-160">Ponadto toosetting domyślny czas wygaśnięcia w kolekcji można ustawić TTL określonych na poziomie dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="b79a0-161">W ten sposób zastępują domyślne hello hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="b79a0-162">Witaj tooset TTL na dokumentu, należy tooprovide liczbą dodatnią inną niż zero, co oznacza hello okres, w sekundach, tooexpire hello dokumentu po hello ostatniej modyfikacji sygnatury czasowej hello dokumentu (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="b79a0-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="b79a0-163">Jeśli dokument nie zawiera TTL pola, następnie hello domyślnej kolekcji hello zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="b79a0-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="b79a0-164">Jeśli czas wygaśnięcia jest wyłączona na poziomie zbioru hello, hello TTL pola w dokumencie hello zostanie zignorowany, aż do ponownego włączenia TTL na powitania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b79a0-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="b79a0-165">Oto fragment przedstawiający sposób tooset hello wygaśnięcia TTL w dokumencie:</span><span class="sxs-lookup"><span data-stu-id="b79a0-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="b79a0-166">Rozszerzanie TTL na istniejącego dokumentu</span><span class="sxs-lookup"><span data-stu-id="b79a0-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="b79a0-167">Wykonując dowolną operację zapisu na powitania dokumentu, można zresetować hello TTL w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="b79a0-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="b79a0-168">W ten sposób ustawi hello `_ts` toohello bieżący czas i toohello odliczania hello dokumentu ważności, zgodnie z ustawieniami hello `ttl`, rozpocznie się ponownie.</span><span class="sxs-lookup"><span data-stu-id="b79a0-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="b79a0-169">Jeśli chcesz, aby toochange hello `ttl` dokumentu, można zaktualizować pola hello, jak można zrobić za pomocą innego pola można ustawić.</span><span class="sxs-lookup"><span data-stu-id="b79a0-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="b79a0-170">Usuwanie TTL z dokumentu</span><span class="sxs-lookup"><span data-stu-id="b79a0-170">Removing TTL from a document</span></span>
<span data-ttu-id="b79a0-171">Jeśli wartości TTL został ustawiony w dokumencie i nie ma już tooexpire tego dokumentu, następnie można pobrać dokumentu hello, usuń pola TTL hello i zastąpić dokument hello na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="b79a0-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="b79a0-172">Po usunięciu hello TTL pole z dokumentu hello hello domyślnej kolekcji hello zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="b79a0-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="b79a0-173">toostop dokumentu z wygasa i nie dziedziczy z kolekcji hello, wówczas należy tooset hello TTL wartość zbyt-1.</span><span class="sxs-lookup"><span data-stu-id="b79a0-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="b79a0-174">Wyłączanie TTL</span><span class="sxs-lookup"><span data-stu-id="b79a0-174">Disabling TTL</span></span>
<span data-ttu-id="b79a0-175">toodisable TTL na kolekcji i tła hello Zatrzymaj przetwarzanie od wyszukiwanie wygasłe dokumenty hello DefaultTTL właściwości w kolekcji hello powinien zostać usunięty.</span><span class="sxs-lookup"><span data-stu-id="b79a0-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="b79a0-176">Usunięcie tej właściwości jest inna niż ustawienie zbyt-1.</span><span class="sxs-lookup"><span data-stu-id="b79a0-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="b79a0-177">Ustawienie zbyt-1 oznacza nowych dokumentów dodane kolekcji toohello będzie funkcjonować w nieskończoność, ale można zmienić na określonych dokumentów w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="b79a0-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="b79a0-178">Usunięcie tej właściwości całkowicie z kolekcji hello oznacza, że żaden dokument wygaśnie, nawet jeśli istnieją dokumenty, które zostały jawnie przesłonięte wcześniejszy domyślny.</span><span class="sxs-lookup"><span data-stu-id="b79a0-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="b79a0-179">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b79a0-179">FAQ</span></span>
<span data-ttu-id="b79a0-180">**Co to jest czas wygaśnięcia koszt mnie?**</span><span class="sxs-lookup"><span data-stu-id="b79a0-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="b79a0-181">Nie ma żadnych dodatkowych kosztów toosetting TTL w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="b79a0-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="b79a0-182">**Jak długo trwa toodelete dokumencie po hello TTL działa?**</span><span class="sxs-lookup"><span data-stu-id="b79a0-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="b79a0-183">dokumenty Hello wygasły natychmiast po hello TTL jest uruchomiony i nie będzie dostępny za pośrednictwem CRUD lub kwerendy interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="b79a0-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="b79a0-184">**Zostanie TTL w dokumencie miały wpływu na RU opłat**</span><span class="sxs-lookup"><span data-stu-id="b79a0-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="b79a0-185">Nie, nie będzie bez wpływu na RU opłat za usunięcia wygasłych dokumentów za pomocą TTL w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b79a0-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="b79a0-186">**Funkcja TTL hello tylko dotyczy tooentire dokumenty lub pojedynczy dokument wartości właściwości mogą wygaśnie?**</span><span class="sxs-lookup"><span data-stu-id="b79a0-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="b79a0-187">Czas wygaśnięcia stosuje toohello całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b79a0-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="b79a0-188">Jeśli chcesz tooexpire tylko części dokumentu, a następnie go zaleca się czy wyodrębniania hello części dokumentu głównego hello w oddzielnych "połączony" dokument tooa, a następnie użyć TTL na tym dokumencie wyodrębnione.</span><span class="sxs-lookup"><span data-stu-id="b79a0-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="b79a0-189">**Funkcja TTL hello ma szczególne wymagania indeksowania?**</span><span class="sxs-lookup"><span data-stu-id="b79a0-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="b79a0-190">Tak.</span><span class="sxs-lookup"><span data-stu-id="b79a0-190">Yes.</span></span> <span data-ttu-id="b79a0-191">Witaj, Kolekcja musi mieć [indeksowania zestawu zasad](indexing-policies.md) tooeither spójność lub opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="b79a0-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="b79a0-192">W trakcie tooset DefaultTTL na kolekcję z zestawu tooNone indeksowania spowoduje błąd, podobnie jak w trakcie tooturn poza indeksowania w kolekcji, której DefaultTTL został już ustawiony.</span><span class="sxs-lookup"><span data-stu-id="b79a0-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b79a0-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b79a0-193">Next steps</span></span>
<span data-ttu-id="b79a0-194">toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, można znaleźć usługi toohello [ *dokumentacji* ](https://azure.microsoft.com/documentation/services/cosmos-db/) strony.</span><span class="sxs-lookup"><span data-stu-id="b79a0-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

