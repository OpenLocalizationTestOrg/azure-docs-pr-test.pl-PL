---
title: "Interfejs API tabeli DB aaaIntroduction tooAzure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używasz bazy danych Azure rozwiązania Cosmos toostore i bardzo dużych woluminów danych klucz wartość z niskim opóźnieniem przy użyciu zapytania hello popularnych interfejsów API bazy danych MongoDB OSS."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Wprowadzenie tooAzure DB rozwiązania Cosmos: Tabela interfejsu API

[Azure Cosmos DB](introduction.md) to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft do aplikacji o krytycznym znaczeniu. Udostępnia bazę danych systemu Azure rozwiązania Cosmos [dystrybucji globalne gotowe](distribute-data-globally.md), [elastyczne skalowanie przepływność i magazyn](partition-data.md) na całym świecie, jednocyfrowej milisekundy opóźnienia na powitania 99-ty percentyl [pięć dobrze zdefiniowane poziomy spójności](consistency-levels.md), zagwarantować wysokiej dostępności, wszystkie kopie przez [SLA branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB rozwiązania Cosmos [automatycznie indeksuje danych](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności toodeal z zarządzania schematu i indeksu. To usługa wielomodelowa, obsługująca modele dokumentowe, klucz-wartość, wykresy i kolumny. 

![Interfejs API magazynu tabel Azure (Azure Table Storage) i usługa Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Azure DB rozwiązania Cosmos zapewnia hello tabelę interfejsu API (wersja zapoznawcza) w przypadku aplikacji wymagających magazyn kluczy i wartości, elastyczne schematu, przewidywalną wydajność, globalne dystrybucji i wysokiej przepływności. Hello tabeli interfejs API udostępnia hello same funkcje co magazynu tabel Azure, ale wykorzystuje korzyści hello hello aparatu bazy danych Azure rozwiązania Cosmos. 

Można kontynuować toouse magazynu tabel Azure dla tabel z magazynu wysokiej i niższe wymagania przepływności. Azure DB rozwiązania Cosmos wprowadzi pomocy technicznej dla tabel zoptymalizowanych pod kątem pamięci masowej w przyszłej aktualizacji, a istniejące i nowe tabel Azure, konta magazynu nie zostaną uaktualnione tooAzure DB rozwiązania Cosmos.

## <a name="premium-and-standard-table-apis"></a>Interfejsy API tabel, premium i standardowe
Jeśli obecnie używasz magazynu tabel Azure, możesz zyskać następujące korzyści, przenosząc tooAzure rozwiązania Cosmos DB podglądu "premium tabeli" hello:

|  | Azure Table Storage | Usługa Azure Cosmos DB: magazyn tabel (wersja zapoznawcza) |
| --- | --- | --- |
| Opóźnienie | Niewielkie, ale brak górnych granic opóźnienia | Jednocyfrowej milisekundy opóźnienia dla odczyty i zapisy, kopie z < opóźnieniem 10 ms odczytuje i < zapisuje 15 ms, czas oczekiwania na powitania 99-ty percentyl, w dowolnej skali, w dowolnym miejscu Witaj świecie |
| Przepływność | Wysoka skalowalność, brak dedykowanego modelu przepływności. Tabele mają limit skalowalności 20 000 operacji/s | Wysoka skalowalność dzięki [dedykowanej zarezerwowanej przepływności na tabelę](request-units.md), wspieranej przez umowy SLA. Konta nie mają górnego limitu przepływności i obsługują >10 milionów operacji/s na tabelę |
| Dystrybucja globalna | Jeden region z jednym opcjonalnym dodatkowym regionem odczytu, co zapewnia wysoką dostępność. Nie można zainicjować trybu failover | [Globalne dystrybucji gotowe](distribute-data-globally.md) z jednego too30 + regionów, obsługę [automatycznej i ręcznej pracy awaryjnej](regional-failover.md) w dowolnym momencie, w dowolnym miejscu Witaj świecie |
| Indeksowanie | Tylko podstawowy indeks PartitionKey i RowKey. Brak dodatkowych indeksów | Automatyczne i kompletne indeksowanie wszystkich właściwości, brak zarządzania indeksem |
| Zapytanie | Wykonanie zapytania wykorzystuje indeks klucza podstawowego, a w przeciwnym przypadku skanuje. | Zapytania mogą korzystać z automatycznego indeksowania właściwości, co skraca czas odpowiedzi. Mechanizm bazy danych usługi Azure Cosmos DB obsługuje agregację, rozwiązania geoprzestrzenne i sortowanie. |
| Spójność | Na poziomie „strong” w regionie podstawowym, na poziomie „eventual” w regionie pomocniczym | [Pięć dobrze zdefiniowane poziomy spójności](consistency-levels.md) tootrade poza dostępności, czas oczekiwania, przepływności i spójności w oparciu wymagań aplikacji |
| Cennik | Optymalizacja pod kątem pamięci  | Optymalizacja pod kątem przepływności |
| Umowy SLA | Dostępność 99,9% | dostępność 99,99% w pojedynczym regionie i możliwości tooadd więcej regionów potrzeby wyższej dostępności. [Wiodące w branży, kompleksowe umowy SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) dotyczące ogólnej dostępności |

## <a name="how-tooget-started"></a>Sposób uruchamiania tooget

Tworzenie konta bazy danych Azure rozwiązania Cosmos w hello [portalu Azure](https://portal.azure.com)i rozpoczynanie pracy z naszych [szybkiego startu dla tabeli interfejsu API przy użyciu platformy .NET](create-table-dotnet.md). 

## <a name="next-steps"></a>Następne kroki

Poniżej przedstawiono kilka tooget wskaźniki rozpoczętej:
* [Tworzenie aplikacji platformy .NET przy użyciu hello tabeli interfejsu API](create-table-dotnet.md)
* [Opracowywania hello tabeli interfejs API .NET](tutorial-develop-table-dotnet.md)
* [Zapytanie tabeli danych przy użyciu hello tabeli interfejsu API](tutorial-query-table.md)
* [Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello tabeli interfejsu API](tutorial-global-distribution-table.md)
* [Zestaw SDK interfejsu API tabel usługi Azure Cosmos DB dla platformy .NET](table-sdk-dotnet.md)
