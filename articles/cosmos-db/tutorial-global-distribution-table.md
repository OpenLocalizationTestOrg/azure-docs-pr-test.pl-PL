---
title: "Samouczek globalne dystrybucji DB rozwiązania Cosmos aaaAzure tabeli interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello tabeli interfejsu API."
services: cosmos-db
keywords: globalne dystrybucji, tabeli
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello tabeli interfejsu API

W tym artykule zostanie przedstawiony sposób toouse hello dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup portalu Azure, a następnie nawiąż połączenie przy użyciu hello tabeli interfejsu API (wersja zapoznawcza).

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure
> * Skonfiguruj globalne dystrybucji przy użyciu hello [tabeli interfejsu API](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Łączenie preferowanego regionu tooa przy użyciu hello tabeli interfejsu API

W kolejności tootake zaletą [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić hello uporządkowana lista preferencji toobe regionów używanych tooperform dokumentu operacji. Można to zrobić przez ustawienie hello `TablePreferredLocations` wartości konfiguracji w pliku konfiguracyjnym aplikacji hello podglądu hello zestawu SDK usługi Magazyn Azure. Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos hello bieżącej dostępności regionalnych i hello preferencji listy jest określony, powitalne większości optymalne punkt końcowy zostanie wybrany przez tooperform zestawu SDK usługi Magazyn Azure hello zapisu i operacji odczytu.

Witaj `TablePreferredLocations` powinien zawierać rozdzielaną przecinkami listę preferowanych lokalizacji (podłączonej do wielu sieci) dla operacji odczytu. Każde wystąpienie klienta można określić podzbiór tych regionów hello preferowane aby odczyty małe opóźnienia. regiony Hello muszą nosić przy użyciu ich [wyświetlane nazwy](https://msdn.microsoft.com/library/azure/gg441293.aspx), na przykład `West US`.

Wszystkie operacje odczytu zostaną wysłane jako pierwszy dostępny region toohello hello `TablePreferredLocations` listy. W przypadku niepowodzenia żądania hello powitania klienta się nie powieść w dół listy hello toohello następny region i tak dalej.

Hello SDK podejmie tylko tooread z określonych w regionów hello `TablePreferredLocations`. Tak, na przykład, jeśli hello konto bazy danych są dostępne w trzech regionów, ale powitania klienta określa tylko dwa hello regionów i do zapisu dla `TablePreferredLocations`, a następnie odczyty nie zostanie obsłużona poza region zapisu hello, nawet w przypadku hello pracy awaryjnej.

Witaj SDK będzie automatycznie wysyłać wszystkie zapisy toohello bieżącego zapisu regionu.

Jeśli hello `TablePreferredLocations` właściwość nie jest ustawiona, wszystkie żądania zostanie obsłużona z hello bieżący obszar zapisu.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
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
