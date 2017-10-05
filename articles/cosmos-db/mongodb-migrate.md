---
title: "Korzystania z interfejsu API Azure rozwiązania Cosmos bazy danych dla bazy danych MongoDB mongoimport i mongorestore | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać mongoimport i mongorestore do importowania danych do interfejsu API dla konta bazy danych MongoDB"
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
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="5fa64-104">Platformy Azure rozwiązania Cosmos bazy danych: Danych MongoDB importu</span><span class="sxs-lookup"><span data-stu-id="5fa64-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="5fa64-105">Do migracji danych z bazy danych MongoDB do bazy danych Azure rozwiązania Cosmos konta do użycia przy użyciu interfejsu API dla bazy danych MongoDB, należy:</span><span class="sxs-lookup"><span data-stu-id="5fa64-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="5fa64-106">Pobierz albo *mongoimport.exe* lub *mongorestore.exe* z [Centrum pobierania bazy danych MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="5fa64-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="5fa64-107">Pobierz z [interfejsu API dla parametrów połączenia bazy danych MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="5fa64-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="5fa64-108">Jeśli dane są importowane z bazy danych MongoDB i planowane jest używanie go z bazy danych rozwiązania Cosmos platformy Azure, należy użyć [narzędzia migracji danych](import-data.md) do importowania danych.</span><span class="sxs-lookup"><span data-stu-id="5fa64-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="5fa64-109">Ten samouczek obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="5fa64-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5fa64-110">Podczas pobierania parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="5fa64-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="5fa64-111">Importowanie danych MongoDB przy użyciu mongoimport</span><span class="sxs-lookup"><span data-stu-id="5fa64-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="5fa64-112">Importowanie danych MongoDB przy użyciu mongorestore</span><span class="sxs-lookup"><span data-stu-id="5fa64-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fa64-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5fa64-113">Prerequisites</span></span>

* <span data-ttu-id="5fa64-114">Zwiększyć przepływność: czas trwania migracji danych zależy od ilości przepływność dla kolekcji można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="5fa64-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="5fa64-115">Pamiętaj zwiększyć przepływność większych migracji danych.</span><span class="sxs-lookup"><span data-stu-id="5fa64-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="5fa64-116">Po zakończeniu migracji należy zmniejszyć przepustowość w celu ograniczenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="5fa64-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="5fa64-117">Aby uzyskać więcej informacji o zwiększenie przepływności w [portalu Azure](https://portal.azure.com), zobacz [poziomy wydajności i warstw cenowych w usłudze Azure DB rozwiązania Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5fa64-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="5fa64-118">Włącz protokół SSL: Azure DB rozwiązania Cosmos ma wymogi ograniczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5fa64-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="5fa64-119">Pamiętaj włączyć protokół SSL w przypadku interakcji z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="5fa64-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="5fa64-120">Procedury w pozostałej części tego artykułu obejmują włączania protokołu SSL dla mongoimport i mongorestore.</span><span class="sxs-lookup"><span data-stu-id="5fa64-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="5fa64-121">Znajdź informacje ciągu połączenia (host, port, nazwę użytkownika i hasło)</span><span class="sxs-lookup"><span data-stu-id="5fa64-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="5fa64-122">W [portalu Azure](https://portal.azure.com), w okienku po lewej stronie kliknij **bazy danych Azure rozwiązania Cosmos** wpisu.</span><span class="sxs-lookup"><span data-stu-id="5fa64-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="5fa64-123">W **subskrypcje** okienku, wybierz nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="5fa64-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="5fa64-124">W **ciąg połączenia** bloku, kliknij przycisk **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="5fa64-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="5fa64-125">Prawe okienko zawiera wszystkie informacje potrzebne do pomyślnego połączenia z kontem.</span><span class="sxs-lookup"><span data-stu-id="5fa64-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![Blok ciągu połączenia](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="5fa64-127">Importowanie danych do interfejsu API dla bazy danych MongoDB przy użyciu mongoimport</span><span class="sxs-lookup"><span data-stu-id="5fa64-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="5fa64-128">Aby zaimportować dane do swojego konta bazy danych Azure rozwiązania Cosmos, szablon.</span><span class="sxs-lookup"><span data-stu-id="5fa64-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="5fa64-129">Wypełnij *hosta*, *username*, i *hasło* z wartościami, które są specyficzne dla swojego konta.</span><span class="sxs-lookup"><span data-stu-id="5fa64-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="5fa64-130">Szablon:</span><span class="sxs-lookup"><span data-stu-id="5fa64-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="5fa64-131">Przykład:</span><span class="sxs-lookup"><span data-stu-id="5fa64-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="5fa64-132">Importowanie danych do interfejsu API dla bazy danych MongoDB przy użyciu mongorestore</span><span class="sxs-lookup"><span data-stu-id="5fa64-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="5fa64-133">Aby przywrócić dane do interfejsu API dla konta bazy danych MongoDB, należy użyć następującego szablonu można wykonać importu.</span><span class="sxs-lookup"><span data-stu-id="5fa64-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="5fa64-134">Wypełnij *hosta*, *username*, i *hasło* z wartościami, które są specyficzne dla swojego konta.</span><span class="sxs-lookup"><span data-stu-id="5fa64-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="5fa64-135">Szablon:</span><span class="sxs-lookup"><span data-stu-id="5fa64-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="5fa64-136">Przykład:</span><span class="sxs-lookup"><span data-stu-id="5fa64-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="5fa64-137">Przewodnik po pomyślnej migracji</span><span class="sxs-lookup"><span data-stu-id="5fa64-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="5fa64-138">Wstępnie tworzyć i skalować kolekcji:</span><span class="sxs-lookup"><span data-stu-id="5fa64-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="5fa64-139">Domyślnie program Azure DB rozwiązania Cosmos inicjuje nową kolekcję bazy danych MongoDB z 1000 jednostek żądania (RUs).</span><span class="sxs-lookup"><span data-stu-id="5fa64-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="5fa64-140">Przed rozpoczęciem migracji za pomocą mongoimport, mongorestore lub mongomirror wstępnego tworzenia Twojej kolekcji z [portalu Azure](https://portal.azure.com) lub z bazy danych MongoDB sterowników i narzędzi.</span><span class="sxs-lookup"><span data-stu-id="5fa64-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="5fa64-141">Jeśli kolekcja jest większa niż 10 GB, upewnij się utworzyć [podzielonej/podzielona na partycje kolekcji](partition-data.md) przy użyciu klucza odpowiedni identyfikator niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5fa64-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="5fa64-142">Z [portalu Azure](https://portal.azure.com), zwiększyć przepływność sieci kolekcje z 1000 RUs dla kolekcji jednej partycji i 2500 RUs dla podzielonej kolekcji tylko do migracji.</span><span class="sxs-lookup"><span data-stu-id="5fa64-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="5fa64-143">Z wyższej przepustowości można uniknąć, ograniczania i migracji w krótszym czasie.</span><span class="sxs-lookup"><span data-stu-id="5fa64-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="5fa64-144">Dzięki co godzinę rozliczeń w usłudze Azure DB rozwiązania Cosmos, można ograniczyć przepustowość natychmiast po migracji, w celu ograniczenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="5fa64-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="5fa64-145">Obliczania przybliżonej opłaty RU do zapisu pojedynczego dokumentu:</span><span class="sxs-lookup"><span data-stu-id="5fa64-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="5fa64-146">a.</span><span class="sxs-lookup"><span data-stu-id="5fa64-146">a.</span></span> <span data-ttu-id="5fa64-147">Połączenia z bazą danych Azure rozwiązania Cosmos bazy danych MongoDB z poziomu powłoki bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5fa64-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="5fa64-148">Instrukcje można znaleźć [połączyć aplikację bazy danych MongoDB do bazy danych Azure rozwiązania Cosmos](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="5fa64-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="5fa64-149">b.</span><span class="sxs-lookup"><span data-stu-id="5fa64-149">b.</span></span> <span data-ttu-id="5fa64-150">Polecenie insert próbki za pomocą jednego z przykładowych dokumentów z poziomu powłoki bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="5fa64-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="5fa64-151">c.</span><span class="sxs-lookup"><span data-stu-id="5fa64-151">c.</span></span> <span data-ttu-id="5fa64-152">Uruchom ```db.runCommand({getLastRequestStatistics: 1})``` i otrzymasz odpowiedź podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="5fa64-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="5fa64-153">d.</span><span class="sxs-lookup"><span data-stu-id="5fa64-153">d.</span></span> <span data-ttu-id="5fa64-154">Zanotuj opłata żądania.</span><span class="sxs-lookup"><span data-stu-id="5fa64-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="5fa64-155">Określ opóźnienie z komputera do usługi w chmurze Azure DB rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="5fa64-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="5fa64-156">a.</span><span class="sxs-lookup"><span data-stu-id="5fa64-156">a.</span></span> <span data-ttu-id="5fa64-157">Włącz pełne rejestrowanie z poziomu powłoki bazy danych MongoDB za pomocą tego polecenia:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="5fa64-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="5fa64-158">b.</span><span class="sxs-lookup"><span data-stu-id="5fa64-158">b.</span></span> <span data-ttu-id="5fa64-159">Uruchom proste zapytanie w bazie danych: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="5fa64-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="5fa64-160">Otrzymasz odpowiedź podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="5fa64-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="5fa64-161">Usuń wstawianego dokumentu przed migracją, aby upewnić się, że nie ma żadnych zduplikowanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="5fa64-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="5fa64-162">Należy usunąć dokumentów za pomocą tego polecenia:```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="5fa64-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="5fa64-163">Oblicz przybliżonej *batchSize* i *numInsertionWorkers* wartości:</span><span class="sxs-lookup"><span data-stu-id="5fa64-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="5fa64-164">Aby uzyskać *batchSize*, dzielenie łączną elastycznie RUs przez RUs używane z Twojej zapisu pojedynczego dokumentu w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="5fa64-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="5fa64-165">Jeśli obliczane *batchSize* < = 24, użyj tego numeru jako sieci *batchSize* wartość.</span><span class="sxs-lookup"><span data-stu-id="5fa64-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="5fa64-166">Jeśli obliczane *batchSize* > 24, ustaw *batchSize* wartość do 24.</span><span class="sxs-lookup"><span data-stu-id="5fa64-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="5fa64-167">Dla *numInsertionWorkers*, użyj równanie: *numInsertionWorkers = (udostępnionej przepływności * czas oczekiwania w sekundach) / (rozmiar partii * używane dla pojedynczego zapisu RUs)*.</span><span class="sxs-lookup"><span data-stu-id="5fa64-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="5fa64-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5fa64-168">Property</span></span>|<span data-ttu-id="5fa64-169">Wartość</span><span class="sxs-lookup"><span data-stu-id="5fa64-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="5fa64-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="5fa64-170">batchSize</span></span>| <span data-ttu-id="5fa64-171">24</span><span class="sxs-lookup"><span data-stu-id="5fa64-171">24</span></span> |
    |<span data-ttu-id="5fa64-172">RUs udostępnione</span><span class="sxs-lookup"><span data-stu-id="5fa64-172">RUs provisioned</span></span> | <span data-ttu-id="5fa64-173">10 000</span><span class="sxs-lookup"><span data-stu-id="5fa64-173">10000</span></span> |
    |<span data-ttu-id="5fa64-174">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="5fa64-174">Latency</span></span> | <span data-ttu-id="5fa64-175">0.100 s</span><span class="sxs-lookup"><span data-stu-id="5fa64-175">0.100 s</span></span> |
    |<span data-ttu-id="5fa64-176">RU naliczona opłata za zapisu 1 doc</span><span class="sxs-lookup"><span data-stu-id="5fa64-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="5fa64-177">10 RUs</span><span class="sxs-lookup"><span data-stu-id="5fa64-177">10 RUs</span></span> |
    |<span data-ttu-id="5fa64-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="5fa64-178">numInsertionWorkers</span></span> | <span data-ttu-id="5fa64-179">?</span><span class="sxs-lookup"><span data-stu-id="5fa64-179">?</span></span> |
    
    <span data-ttu-id="5fa64-180">*numInsertionWorkers = (RUs 10000 x 0,1 s) / (RUs 24 x 10) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="5fa64-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="5fa64-181">Uruchom polecenie końcowego migracji:</span><span class="sxs-lookup"><span data-stu-id="5fa64-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="5fa64-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fa64-182">Next steps</span></span>

<span data-ttu-id="5fa64-183">Możesz przejść do następnego samouczek i Dowiedz się, jak wykonać zapytanie dotyczące bazy danych MongoDB danych przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5fa64-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="5fa64-184">Jak wykonać zapytanie dotyczące bazy danych MongoDB danych?</span><span class="sxs-lookup"><span data-stu-id="5fa64-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
