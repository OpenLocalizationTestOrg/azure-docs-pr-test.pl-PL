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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API usługi DocumentDB

W tym artykule zostanie przedstawiony sposób toouse hello Azure toosetup portalu Azure DB rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu hello interfejsu API usługi DocumentDB.

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure
> * Skonfiguruj globalne dystrybucji przy użyciu hello [interfejsów API usługi DocumentDB](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Łączenie preferowanego regionu tooa przy użyciu hello interfejsu API usługi DocumentDB

W kolejności tootake zaletą [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić hello uporządkowana lista preferencji toobe regionów używanych tooperform dokumentu operacji. Można to zrobić przez ustawienie hello zasad połączenia. Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos hello bieżącej dostępności regionalnych i listy preferencji hello określone, powitalne większości optymalne punkt końcowy zostanie wybrany przez hello tooperform zestawu SDK usługi DocumentDB zapisu i odczytu operacji.

Ta lista preferencji określono podczas inicjowania połączenia przy użyciu hello zestawów SDK usługi DocumentDB. Witaj zestawów SDK zaakceptować opcjonalny parametr "PreferredLocations" oznacza to uporządkowana lista regionów platformy Azure.

Witaj SDK będzie automatycznie wysyłać wszystkie zapisy toohello bieżącego zapisu regionu.

Wszystkie operacje odczytu zostaną wysłane jako pierwszy dostępny region toohello hello PreferredLocations listy. W przypadku niepowodzenia żądania hello powitania klienta się nie powieść w dół listy hello toohello następny region i tak dalej.

tylko tooread z określonych w PreferredLocations regionów hello zostanie podjęta próba Hello zestawów SDK. Tak na przykład, jeśli hello konto bazy danych jest dostępne w trzech regionów, ale powitania klienta tylko określa dwa regiony i do zapisu hello PreferredLocations, następnie odczyty nie zostanie obsłużona poza region zapisu hello, nawet w przypadku hello pracy awaryjnej.

aplikacji Hello można Sprawdź hello bieżący punkt końcowy zapisu i odczytu punktu końcowego wybierany przez hello zestawu SDK przez sprawdzanie, czy dwie właściwości WriteEndpoint i ReadEndpoint dostępne w wersji zestawu SDK 1.8 i powyżej.

Jeśli nie ustawiono właściwości PreferredLocations hello, wszystkie żądania będą udostępniane przez hello bieżący obszar zapisu.

## <a name="net-sdk"></a>Zestaw SDK .NET
Witaj zestawu SDK można bez wprowadzania żadnych zmian kodu. W takim przypadku hello zestawu SDK automatycznie kieruje zarówno odczytuje i zapisuje bieżący obszar zapisu toohello.

W wersji 1.8 i nowszej hello zestawu .NET SDK hello ConnectionPolicy parametr dla konstruktora DocumentClient hello ma właściwość o nazwie Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Ta właściwość jest typu kolekcji `<string>` i powinien zawierać listę nazw regionu. wartości ciągu Hello są sformatowane w kolumnie Nazwa regionu hello na powitania [regiony platformy Azure] [ regions] strony nie może zawierać spacji przed lub po hello pierwszy i ostatni znak odpowiednio.

punktów końcowych odczytu i zapisu bieżącego Hello są odpowiednio dostępne w DocumentClient.WriteEndpoint i DocumentClient.ReadEndpoint.

> [!NOTE]
> nie należy traktować jako długotrwałe stałe adresy URL Hello hello punktów końcowych. Usługa Hello może zaktualizować je w dowolnym momencie. Witaj SDK automatycznie obsługuje tę zmianę.
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

## <a name="nodejs-javascript-and-python-sdks"></a>NodeJS, JavaScript i zestawy SDK Python
Witaj zestawu SDK można bez wprowadzania żadnych zmian kodu. W takim przypadku powitalne SDK spowoduje automatyczne kierowanie zarówno odczytuje i zapisuje toohello bieżący obszar zapisu.

W wersji 1.8 i później każdego zestawu SDK, hello ConnectionPolicy parametr dla konstruktora DocumentClient hello nową właściwość o nazwie DocumentClient.ConnectionPolicy.PreferredLocations. Ten parametr jest tablicą ciągów przyjmuje listę nazw regionu. nazwy Hello są sformatowane na powitania kolumnę Nazwa regionu w hello [regiony platformy Azure] [ regions] strony. Umożliwia także stałe hello wstępnie zdefiniowane w obiekcie wygody hello AzureDocuments.Regions

punktów końcowych odczytu i zapisu bieżącego Hello są odpowiednio dostępne w DocumentClient.getWriteEndpoint i DocumentClient.getReadEndpoint.

> [!NOTE]
> nie należy traktować jako długotrwałe stałe adresy URL Hello hello punktów końcowych. Usługa Hello może zaktualizować je w dowolnym momencie. Witaj SDK zostanie automatycznie obsłużyć tej zmiany.
>
>

Poniżej podano przykładowy kod NodeJS/JavaScript. Python i Java zastosują hello tego samego wzorca.

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

## <a name="rest"></a>REST
Gdy konto bazy danych został udostępniony w wielu regionach, klienci mogą wykonywać kwerendę jego dostępność, wykonując na powitania następującego identyfikatora URI żądania GET.

    https://{databaseaccount}.documents.azure.com/

Usługa Hello zwróci listę regionów i ich odpowiednich bazy danych Azure rozwiązania Cosmos punktu końcowego identyfikatorów URI dla replik hello. bieżący obszar zapisu Hello zostanie wskazany w hello odpowiedzi. powitania klienta można wybrać odpowiednie punktu końcowego hello na wszystkie kolejne żądania interfejsu API REST w następujący sposób.

Przykład odpowiedzi

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


* Należy przejść do żądania PUT, POST i DELETE toohello wskazanych zapisu identyfikatora URI
* Pobiera wszystkie i inne żądania tylko do odczytu (na przykład kwerendy) może go punktu końcowego tooany wyboru powitania klienta

Zapis regionów tylko do tooread żądań zakończy się niepowodzeniem z kodem błędu HTTP 403 ("Dostęp zabroniony").

Jeśli region zapisu hello zmieni się po fazie początkowe wykrywanie powitania klienta, kolejne zapisuje toohello poprzedniego region zapisu zakończy się niepowodzeniem z kodem błędu HTTP 403 ("Dostęp zabroniony"). powitania klienta należy następnie UZYSKAĆ hello listę regionów ponownie tooget hello zaktualizowane zapisu regionu.

To wszystko, która kończy w tym samouczku. Dowiedz się jak toomanage hello spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md). I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure
> * Skonfiguruj globalne dystrybucji przy użyciu hello interfejsów API usługi DocumentDB

Można teraz kontynuować toohello następny samouczek toolearn jak toodevelop lokalnie za pomocą hello emulatora lokalnej bazy danych Azure rozwiązania Cosmos.

> [!div class="nextstepaction"]
> [Opracowywanie lokalnie emulatorze hello](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

