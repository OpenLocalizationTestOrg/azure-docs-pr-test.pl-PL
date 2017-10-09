---
title: "aaaUse mongoimport i mongorestore z hello interfejsu API Azure rozwiązania Cosmos bazy danych dla bazy danych MongoDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse mongoimport i mongorestore tooimport danych tooan interfejsu API dla konta bazy danych MongoDB"
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="cf61d-104">Platformy Azure rozwiązania Cosmos bazy danych: Danych MongoDB importu</span><span class="sxs-lookup"><span data-stu-id="cf61d-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="cf61d-105">toomigrate dane z bazy danych MongoDB tooan konta bazy danych Azure rozwiązania Cosmos do korzystania z interfejsu API hello bazy danych mongodb, należy:</span><span class="sxs-lookup"><span data-stu-id="cf61d-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="cf61d-106">Pobierz albo *mongoimport.exe* lub *mongorestore.exe* z hello [Centrum pobierania bazy danych MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="cf61d-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="cf61d-107">Pobierz z [interfejsu API dla parametrów połączenia bazy danych MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="cf61d-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="cf61d-108">Jeśli importujesz dane z bazy danych MongoDB i plan toouse go przy użyciu hello Azure DB rozwiązania Cosmos, należy użyć hello [narzędzia migracji danych](import-data.md) tooimport danych.</span><span class="sxs-lookup"><span data-stu-id="cf61d-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="cf61d-109">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="cf61d-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf61d-110">Podczas pobierania parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="cf61d-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="cf61d-111">Importowanie danych MongoDB przy użyciu mongoimport</span><span class="sxs-lookup"><span data-stu-id="cf61d-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="cf61d-112">Importowanie danych MongoDB przy użyciu mongorestore</span><span class="sxs-lookup"><span data-stu-id="cf61d-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf61d-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf61d-113">Prerequisites</span></span>

* <span data-ttu-id="cf61d-114">Zwiększyć przepływność: czas trwania hello migrację danych zależy od ilości hello przepływność dla kolekcji można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="cf61d-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="cf61d-115">Należy się, że przepływność hello tooincrease większych migracji danych.</span><span class="sxs-lookup"><span data-stu-id="cf61d-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="cf61d-116">Po zakończeniu migracji hello obniżyć hello przepływności toosave.</span><span class="sxs-lookup"><span data-stu-id="cf61d-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="cf61d-117">Aby uzyskać więcej informacji o zwiększenie przepływności w hello [portalu Azure](https://portal.azure.com), zobacz [poziomy wydajności i warstw cenowych w usłudze Azure DB rozwiązania Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="cf61d-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="cf61d-118">Włącz protokół SSL: Azure DB rozwiązania Cosmos ma wymogi ograniczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="cf61d-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="cf61d-119">Można się tooenable protokołu SSL podczas interakcji z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="cf61d-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="cf61d-120">procedury Hello w hello dalszej części artykułu hello obejmują jak tooenable SSL mongoimport i mongorestore.</span><span class="sxs-lookup"><span data-stu-id="cf61d-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="cf61d-121">Znajdź informacje ciągu połączenia (host, port, nazwę użytkownika i hasło)</span><span class="sxs-lookup"><span data-stu-id="cf61d-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="cf61d-122">W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, kliknij przycisk hello **bazy danych Azure rozwiązania Cosmos** wpisu.</span><span class="sxs-lookup"><span data-stu-id="cf61d-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="cf61d-123">W hello **subskrypcje** okienku, wybierz nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="cf61d-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="cf61d-124">W hello **ciąg połączenia** bloku, kliknij przycisk **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="cf61d-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="cf61d-125">Witaj w prawym okienku zawiera wszystkie informacje hello potrzebne toosuccessfully łączyć tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="cf61d-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Blok ciągu połączenia](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="cf61d-127">Importowanie danych toohello API bazy danych mongodb przy użyciu mongoimport</span><span class="sxs-lookup"><span data-stu-id="cf61d-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="cf61d-128">tooimport danych tooyour konta bazy danych rozwiązania Cosmos platformy Azure, użyj hello następującego szablonu.</span><span class="sxs-lookup"><span data-stu-id="cf61d-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="cf61d-129">Wypełnij *hosta*, *username*, i *hasło* wartościami hello są tooyour określonego konta.</span><span class="sxs-lookup"><span data-stu-id="cf61d-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="cf61d-130">Szablon:</span><span class="sxs-lookup"><span data-stu-id="cf61d-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="cf61d-131">Przykład:</span><span class="sxs-lookup"><span data-stu-id="cf61d-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="cf61d-132">Importowanie danych toohello API bazy danych mongodb przy użyciu mongorestore</span><span class="sxs-lookup"><span data-stu-id="cf61d-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="cf61d-133">toorestore interfejsu API tooyour danych dla bazy danych MongoDB konta, użyj powitania po importowania hello tooexecute szablonu.</span><span class="sxs-lookup"><span data-stu-id="cf61d-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="cf61d-134">Wypełnij *hosta*, *username*, i *hasło* wartościami hello są tooyour określonego konta.</span><span class="sxs-lookup"><span data-stu-id="cf61d-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="cf61d-135">Szablon:</span><span class="sxs-lookup"><span data-stu-id="cf61d-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="cf61d-136">Przykład:</span><span class="sxs-lookup"><span data-stu-id="cf61d-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="cf61d-137">Przewodnik po pomyślnej migracji</span><span class="sxs-lookup"><span data-stu-id="cf61d-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="cf61d-138">Wstępnie tworzyć i skalować kolekcji:</span><span class="sxs-lookup"><span data-stu-id="cf61d-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="cf61d-139">Domyślnie program Azure DB rozwiązania Cosmos inicjuje nową kolekcję bazy danych MongoDB z 1000 jednostek żądania (RUs).</span><span class="sxs-lookup"><span data-stu-id="cf61d-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="cf61d-140">Przed rozpoczęciem powitalne migracji za pomocą mongoimport, mongorestore lub mongomirror Utwórz wstępnie wszystkie kolekcje z hello [portalu Azure](https://portal.azure.com) lub z bazy danych MongoDB sterowników i narzędzi.</span><span class="sxs-lookup"><span data-stu-id="cf61d-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="cf61d-141">Jeśli kolekcji jest większa niż 10 GB, upewnij się, że toocreate [podzielonej/podzielona na partycje kolekcji](partition-data.md) przy użyciu klucza odpowiedni identyfikator niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="cf61d-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="cf61d-142">Z hello [portalu Azure](https://portal.azure.com), zwiększyć przepływność sieci kolekcje z 1000 RUs dla kolekcji jednej partycji i 2500 RUs dla podzielonej kolekcji tylko do migracji hello.</span><span class="sxs-lookup"><span data-stu-id="cf61d-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="cf61d-143">Z wyższej przepustowości hello można uniknąć, ograniczania i migracji w krótszym czasie.</span><span class="sxs-lookup"><span data-stu-id="cf61d-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="cf61d-144">Z rozliczeniami co godzinę w usłudze Azure DB rozwiązania Cosmos, można zmniejszyć przepustowość hello natychmiast po hello migracji toosave kosztów.</span><span class="sxs-lookup"><span data-stu-id="cf61d-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="cf61d-145">Oblicz hello przybliżonej RU opłat zapisu pojedynczego dokumentu:</span><span class="sxs-lookup"><span data-stu-id="cf61d-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="cf61d-146">a.</span><span class="sxs-lookup"><span data-stu-id="cf61d-146">a.</span></span> <span data-ttu-id="cf61d-147">Połączenia bazy danych Azure rozwiązania Cosmos bazy danych MongoDB tooyour z hello powłoki bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cf61d-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="cf61d-148">Instrukcje można znaleźć [połączenia bazy danych MongoDB aplikacji tooAzure DB rozwiązania Cosmos](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="cf61d-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="cf61d-149">b.</span><span class="sxs-lookup"><span data-stu-id="cf61d-149">b.</span></span> <span data-ttu-id="cf61d-150">Polecenie insert próbki za pomocą jednego z przykładowych dokumentów z hello powłoki bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="cf61d-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="cf61d-151">c.</span><span class="sxs-lookup"><span data-stu-id="cf61d-151">c.</span></span> <span data-ttu-id="cf61d-152">Uruchom ```db.runCommand({getLastRequestStatistics: 1})``` i otrzymasz odpowiedź podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="cf61d-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="cf61d-153">d.</span><span class="sxs-lookup"><span data-stu-id="cf61d-153">d.</span></span> <span data-ttu-id="cf61d-154">Zwróć uwagę hello żądań bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="cf61d-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="cf61d-155">Określ opóźnienie hello z toohello Twojego komputera usługa w chmurze Azure DB rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="cf61d-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="cf61d-156">a.</span><span class="sxs-lookup"><span data-stu-id="cf61d-156">a.</span></span> <span data-ttu-id="cf61d-157">Włącz pełne rejestrowanie z hello powłoki bazy danych MongoDB za pomocą tego polecenia:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="cf61d-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="cf61d-158">b.</span><span class="sxs-lookup"><span data-stu-id="cf61d-158">b.</span></span> <span data-ttu-id="cf61d-159">Uruchom proste zapytanie w bazie danych hello: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="cf61d-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="cf61d-160">Otrzymasz odpowiedź podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="cf61d-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="cf61d-161">Usuwanie dokumentu hello wstawiony przed hello migracji tooensure, że nie ma żadnych zduplikowanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="cf61d-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="cf61d-162">Należy usunąć dokumentów za pomocą tego polecenia:```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="cf61d-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="cf61d-163">Oblicz hello przybliżonej *batchSize* i *numInsertionWorkers* wartości:</span><span class="sxs-lookup"><span data-stu-id="cf61d-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="cf61d-164">Aby uzyskać *batchSize*, łącznie hello dzielenia elastycznie RUs przez RUs hello używane z Twojej zapisu pojedynczego dokumentu w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="cf61d-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="cf61d-165">Jeśli obliczana hello *batchSize* < = 24, użyj tego numeru jako sieci *batchSize* wartość.</span><span class="sxs-lookup"><span data-stu-id="cf61d-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="cf61d-166">Jeśli obliczana hello *batchSize* > 24, zestaw hello *batchSize* too24 wartość.</span><span class="sxs-lookup"><span data-stu-id="cf61d-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="cf61d-167">Dla *numInsertionWorkers*, użyj równanie: *numInsertionWorkers = (udostępnionej przepływności * czas oczekiwania w sekundach) / (rozmiar partii * używane dla pojedynczego zapisu RUs)*.</span><span class="sxs-lookup"><span data-stu-id="cf61d-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="cf61d-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cf61d-168">Property</span></span>|<span data-ttu-id="cf61d-169">Wartość</span><span class="sxs-lookup"><span data-stu-id="cf61d-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="cf61d-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="cf61d-170">batchSize</span></span>| <span data-ttu-id="cf61d-171">24</span><span class="sxs-lookup"><span data-stu-id="cf61d-171">24</span></span> |
    |<span data-ttu-id="cf61d-172">RUs udostępnione</span><span class="sxs-lookup"><span data-stu-id="cf61d-172">RUs provisioned</span></span> | <span data-ttu-id="cf61d-173">10 000</span><span class="sxs-lookup"><span data-stu-id="cf61d-173">10000</span></span> |
    |<span data-ttu-id="cf61d-174">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="cf61d-174">Latency</span></span> | <span data-ttu-id="cf61d-175">0.100 s</span><span class="sxs-lookup"><span data-stu-id="cf61d-175">0.100 s</span></span> |
    |<span data-ttu-id="cf61d-176">RU naliczona opłata za zapisu 1 doc</span><span class="sxs-lookup"><span data-stu-id="cf61d-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="cf61d-177">10 RUs</span><span class="sxs-lookup"><span data-stu-id="cf61d-177">10 RUs</span></span> |
    |<span data-ttu-id="cf61d-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="cf61d-178">numInsertionWorkers</span></span> | <span data-ttu-id="cf61d-179">?</span><span class="sxs-lookup"><span data-stu-id="cf61d-179">?</span></span> |
    
    <span data-ttu-id="cf61d-180">*numInsertionWorkers = (RUs 10000 x 0,1 s) / (RUs 24 x 10) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="cf61d-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="cf61d-181">Polecenie hello końcowego migracji:</span><span class="sxs-lookup"><span data-stu-id="cf61d-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="cf61d-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf61d-182">Next steps</span></span>

<span data-ttu-id="cf61d-183">Można kontynuować toohello następny samouczek i Dowiedz się, jak tooquery danych MongoDB przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cf61d-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="cf61d-184">Jak tooquery danych MongoDB?</span><span class="sxs-lookup"><span data-stu-id="cf61d-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
