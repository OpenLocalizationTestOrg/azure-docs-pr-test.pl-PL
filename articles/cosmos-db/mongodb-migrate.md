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
# <a name="azure-cosmos-db-import-mongodb-data"></a>Platformy Azure rozwiązania Cosmos bazy danych: Danych MongoDB importu 

toomigrate dane z bazy danych MongoDB tooan konta bazy danych Azure rozwiązania Cosmos do korzystania z interfejsu API hello bazy danych mongodb, należy:

* Pobierz albo *mongoimport.exe* lub *mongorestore.exe* z hello [Centrum pobierania bazy danych MongoDB](https://www.mongodb.com/download-center).
* Pobierz z [interfejsu API dla parametrów połączenia bazy danych MongoDB](connect-mongodb-account.md).

Jeśli importujesz dane z bazy danych MongoDB i plan toouse go przy użyciu hello Azure DB rozwiązania Cosmos, należy użyć hello [narzędzia migracji danych](import-data.md) tooimport danych.

Ten samouczek obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Podczas pobierania parametrów połączenia
> * Importowanie danych MongoDB przy użyciu mongoimport
> * Importowanie danych MongoDB przy użyciu mongorestore

## <a name="prerequisites"></a>Wymagania wstępne

* Zwiększyć przepływność: czas trwania hello migrację danych zależy od ilości hello przepływność dla kolekcji można skonfigurować. Należy się, że przepływność hello tooincrease większych migracji danych. Po zakończeniu migracji hello obniżyć hello przepływności toosave. Aby uzyskać więcej informacji o zwiększenie przepływności w hello [portalu Azure](https://portal.azure.com), zobacz [poziomy wydajności i warstw cenowych w usłudze Azure DB rozwiązania Cosmos](performance-levels.md).

* Włącz protokół SSL: Azure DB rozwiązania Cosmos ma wymogi ograniczeniami zabezpieczeń. Można się tooenable protokołu SSL podczas interakcji z Twoim kontem. procedury Hello w hello dalszej części artykułu hello obejmują jak tooenable SSL mongoimport i mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Znajdź informacje ciągu połączenia (host, port, nazwę użytkownika i hasło)

1. W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, kliknij przycisk hello **bazy danych Azure rozwiązania Cosmos** wpisu.
2. W hello **subskrypcje** okienku, wybierz nazwę konta.
3. W hello **ciąg połączenia** bloku, kliknij przycisk **ciąg połączenia**.  
Witaj w prawym okienku zawiera wszystkie informacje hello potrzebne toosuccessfully łączyć tooyour konta.

    ![Blok ciągu połączenia](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Importowanie danych toohello API bazy danych mongodb przy użyciu mongoimport

tooimport danych tooyour konta bazy danych rozwiązania Cosmos platformy Azure, użyj hello następującego szablonu. Wypełnij *hosta*, *username*, i *hasło* wartościami hello są tooyour określonego konta.  

Szablon:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Przykład:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Importowanie danych toohello API bazy danych mongodb przy użyciu mongorestore

toorestore interfejsu API tooyour danych dla bazy danych MongoDB konta, użyj powitania po importowania hello tooexecute szablonu. Wypełnij *hosta*, *username*, i *hasło* wartościami hello są tooyour określonego konta.

Szablon:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Przykład:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Przewodnik po pomyślnej migracji

1. Wstępnie tworzyć i skalować kolekcji:
        
    * Domyślnie program Azure DB rozwiązania Cosmos inicjuje nową kolekcję bazy danych MongoDB z 1000 jednostek żądania (RUs). Przed rozpoczęciem powitalne migracji za pomocą mongoimport, mongorestore lub mongomirror Utwórz wstępnie wszystkie kolekcje z hello [portalu Azure](https://portal.azure.com) lub z bazy danych MongoDB sterowników i narzędzi. Jeśli kolekcji jest większa niż 10 GB, upewnij się, że toocreate [podzielonej/podzielona na partycje kolekcji](partition-data.md) przy użyciu klucza odpowiedni identyfikator niezależnego fragmentu.

    * Z hello [portalu Azure](https://portal.azure.com), zwiększyć przepływność sieci kolekcje z 1000 RUs dla kolekcji jednej partycji i 2500 RUs dla podzielonej kolekcji tylko do migracji hello. Z wyższej przepustowości hello można uniknąć, ograniczania i migracji w krótszym czasie. Z rozliczeniami co godzinę w usłudze Azure DB rozwiązania Cosmos, można zmniejszyć przepustowość hello natychmiast po hello migracji toosave kosztów.

2. Oblicz hello przybliżonej RU opłat zapisu pojedynczego dokumentu:

    a. Połączenia bazy danych Azure rozwiązania Cosmos bazy danych MongoDB tooyour z hello powłoki bazy danych MongoDB. Instrukcje można znaleźć [połączenia bazy danych MongoDB aplikacji tooAzure DB rozwiązania Cosmos](connect-mongodb-account.md).
    
    b. Polecenie insert próbki za pomocą jednego z przykładowych dokumentów z hello powłoki bazy danych MongoDB:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Uruchom ```db.runCommand({getLastRequestStatistics: 1})``` i otrzymasz odpowiedź podobne do następującego:
     
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
        
    d. Zwróć uwagę hello żądań bezpłatnie.
    
3. Określ opóźnienie hello z toohello Twojego komputera usługa w chmurze Azure DB rozwiązania Cosmos:
    
    a. Włącz pełne rejestrowanie z hello powłoki bazy danych MongoDB za pomocą tego polecenia:```setVerboseShell(true)```
    
    b. Uruchom proste zapytanie w bazie danych hello: ```db.coll.find().limit(1)```. Otrzymasz odpowiedź podobne do następującego:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Usuwanie dokumentu hello wstawiony przed hello migracji tooensure, że nie ma żadnych zduplikowanych dokumentów. Należy usunąć dokumentów za pomocą tego polecenia:```db.coll.remove({})```

5. Oblicz hello przybliżonej *batchSize* i *numInsertionWorkers* wartości:

    * Aby uzyskać *batchSize*, łącznie hello dzielenia elastycznie RUs przez RUs hello używane z Twojej zapisu pojedynczego dokumentu w kroku 3.
    
    * Jeśli obliczana hello *batchSize* < = 24, użyj tego numeru jako sieci *batchSize* wartość.
    
    * Jeśli obliczana hello *batchSize* > 24, zestaw hello *batchSize* too24 wartość.
    
    * Dla *numInsertionWorkers*, użyj równanie: *numInsertionWorkers = (udostępnionej przepływności * czas oczekiwania w sekundach) / (rozmiar partii * używane dla pojedynczego zapisu RUs)*.
        
    |Właściwość|Wartość|
    |--------|-----|
    |batchSize| 24 |
    |RUs udostępnione | 10 000 |
    |Opóźnienie | 0.100 s |
    |RU naliczona opłata za zapisu 1 doc | 10 RUs |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (RUs 10000 x 0,1 s) / (RUs 24 x 10) = 4.1666*

6. Polecenie hello końcowego migracji:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Następne kroki

Można kontynuować toohello następny samouczek i Dowiedz się, jak tooquery danych MongoDB przy użyciu bazy danych Azure rozwiązania Cosmos. 

> [!div class="nextstepaction"]
>[Jak tooquery danych MongoDB?](../cosmos-db/tutorial-query-mongodb.md)
