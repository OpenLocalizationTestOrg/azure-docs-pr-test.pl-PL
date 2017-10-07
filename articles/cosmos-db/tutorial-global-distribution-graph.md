---
title: "aaaAzure rozwiązania Cosmos bazy danych dystrybucji globalne samouczek dotyczący interfejsu API programu Graph | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API programu Graph."
services: cosmos-db
keywords: globalne dystrybucji, wykres, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API programu Graph

W tym artykule zostanie przedstawiony sposób toouse hello dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup portalu Azure, a następnie nawiąż połączenie przy użyciu hello interfejsu API programu Graph (wersja zapoznawcza).

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure
> * Skonfiguruj globalne dystrybucji przy użyciu hello [API Graph](graph-introduction.md) (wersja zapoznawcza)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Łączenie tooa przy użyciu interfejsu API programu Graph hello przy użyciu zestawu .NET SDK hello preferowanego regionu.

Interfejs API programu Graph Hello jest ujawniona jako biblioteki rozszerzenia na powitania zestawu SDK usługi DocumentDB.

W kolejności tootake zaletą [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić hello uporządkowana lista preferencji toobe regionów używanych tooperform dokumentu operacji. Można to zrobić przez ustawienie hello zasad połączenia. Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos hello bieżącej dostępności regionalnych i hello preferencji listy określone, hello większości optymalne punktu końcowego zostanie wybrany przez hello SDK tooperform zapisu i operacje odczytu.

Ta lista preferencji został określony podczas inicjowania połączenia przy użyciu hello zestawów SDK. Witaj zestawów SDK zaakceptować opcjonalny parametr "PreferredLocations" oznacza to uporządkowana lista regionów platformy Azure.

* **Zapisuje**: hello SDK będzie automatycznie wysyłać wszystkie zapisuje toohello bieżący obszar zapisu.
* **Odczytuje**: wszystkie operacje odczytu zostaną wysłane jako pierwszy dostępny region toohello hello PreferredLocations listy. W przypadku niepowodzenia żądania hello powitania klienta się nie powieść w dół listy hello toohello następny region i tak dalej. tylko tooread z określonych w PreferredLocations regionów hello zostanie podjęta próba Hello zestawów SDK. Tak na przykład, jeśli hello konto rozwiązania Cosmos bazy danych jest dostępne w trzech regionów, ale powitania klienta tylko określa dwa regiony i do zapisu hello PreferredLocations, następnie odczyty nie zostanie obsłużona poza region zapisu hello, nawet w przypadku hello pracy awaryjnej.

aplikacji Hello można Sprawdź hello bieżący punkt końcowy zapisu i odczytu punktu końcowego wybierany przez hello zestawu SDK przez sprawdzanie, czy dwie właściwości WriteEndpoint i ReadEndpoint dostępne w wersji zestawu SDK 1.8 i powyżej. Jeśli nie ustawiono właściwości PreferredLocations hello, wszystkie żądania będą udostępniane przez hello bieżący obszar zapisu.

### <a name="using-hello-sdk"></a>Przy użyciu hello zestawu SDK

Na przykład w hello zestawu .NET SDK hello `ConnectionPolicy` parametr hello `DocumentClient` Konstruktor ma właściwość o nazwie `PreferredLocations`. Tej właściwości można ustawić tooa lista obszaru nazw. Nazwa wyświetlana Hello [regiony platformy Azure] [ regions] może być określona jako część `PreferredLocations`.

> [!NOTE]
> nie należy traktować jako długotrwałe stałe adresy URL Hello hello punktów końcowych. Usługa Hello może zaktualizować je w dowolnym momencie. Witaj SDK automatycznie obsługuje tę zmianę.
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

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

