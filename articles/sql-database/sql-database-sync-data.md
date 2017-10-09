---
title: aaaSync danych (wersja zapoznawcza) | Dokumentacja firmy Microsoft
description: "W tym omówieniu przedstawiono synchronizacji danych SQL Azure (wersja zapoznawcza)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>Synchronizowanie danych między wieloma bazami danych chmury i lokalnych z opcją synchronizacji danych SQL

Synchronizacja danych SQL to usługa oparta na bazie danych SQL Azure, która umożliwia synchronizowanie danych hello wybierz dwukierunkowo przez wiele baz danych i wystąpień programu SQL Server.

Synchronizacja danych opiera się wokół koncepcji hello grupy synchronizacji. Grupy synchronizacji jest grupą baz danych, które mają toosynchronize.

Grupy synchronizacji ma hello następujące właściwości:

-   Witaj **schematu synchronizacji** w tym artykule opisano, które dane są synchronizowane.

-   Witaj **kierunek synchronizacji** może być dwukierunkowe lub mogą przepływać tylko w jednym kierunku. Oznacza to, że hello kierunek synchronizacji mogą być *tooMember Centrum* lub *tooHub elementu członkowskiego*, lub obie.

-   Witaj **interwał synchronizacji** jest częstotliwość synchronizacji.

-   Witaj **zasady rozpoznawania konfliktu** poziomu zasad grupy, które mogą być *wins Centrum* lub *wins elementu członkowskiego*.

Synchronizacja danych używa danych toosynchronize topologii gwiazdy. Do definiowania jednej z baz danych hello hello grupy jako hello Centrum bazy danych. rest Hello hello baz danych to element członkowski bazy danych. Synchronizacja występuje tylko między hello koncentratora i indywidualnych elementów członkowskich.
-   Witaj **bazy danych Centrum** musi być bazy danych SQL Azure.
-   Witaj **baz danych elementu członkowskiego** może być bazy danych SQL, lokalnych baz danych programu SQL Server lub wystąpień programu SQL Server na maszynach wirtualnych Azure.
-   Witaj **bazy danych usługi synchronizacji** zawiera hello metadanych i dziennika hello synchronizacji danych. Baza danych usługi synchronizacji ma toobe bazy danych SQL Azure znajduje się w hello tego samego regionu hello Centrum bazy danych. Hello bazy danych usługi synchronizacji jest utworzyć klienta i należące do klientów.

> [!NOTE]
> Jeśli używasz bazy danych na lokalnym jest zbyt[Konfigurowanie lokalnego agenta.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Synchronizowanie danych między bazami danych](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Podczas synchronizacji danych toouse

Synchronizacja danych jest przydatne w sytuacjach, gdy dane musi toobe przechowywać przez okres toodate przez wiele baz danych SQL Azure lub baz danych programu SQL Server. Poniżej przedstawiono hello przypadki użycia główne synchronizacji danych:

-   **Synchronizacja danych hybrydowego:** z opcją synchronizacji danych można przechowywać dane synchronizowane między lokalnych baz danych i baz danych SQL Azure tooenable hybrydowych aplikacji. Ta funkcja może odwołać toocustomers, który rozważa przenoszenie chmury toohello i chcesz tooput niektórych aplikacji na platformie Azure.

-   **Aplikacje rozproszone:** w wielu przypadkach jest korzystne tooseparate różnych obciążeń w różnych baz danych. Na przykład jeśli masz dużą produkcyjnej bazy danych, ale należy również toorun raportowania lub analityka obciążenie te dane, jest przydatne toohave drugiej bazy danych dla tego dodatkowe obciążenie. Takie podejście minimalizuje wpływ na wydajność hello na obciążenie produkcji. Można użyć tych dwóch baz danych synchronizowane tookeep synchronizacji danych.

-   **Globalny aplikacji rozproszonych:** wiele firm span kilka regionów i nawet kilka krajów. toominimize opóźnienia sieci, jest najlepszym toohave zamknąć dane w regionie tooyou. Z opcją synchronizacji danych można pracować z baz danych w regionach wokół Witaj świecie zsynchronizowane.

Nie zaleca się synchronizacji danych dla hello następujące scenariusze:

-   Odzyskiwanie po awarii

-   Przeczytaj skali

-   ETL (OLTP tooOLAP)

-   Migracja z lokalnego programu SQL Server tooAzure bazy danych SQL

## <a name="how-does-data-sync-work"></a>Jak działa synchronizacji danych? 

-   **Śledzenie zmian danych:** synchronizacji danych śledzi zmiany przy użyciu wstawiania, aktualizacji i usuwania wyzwalaczy. zmiany Hello są rejestrowane w tabeli po stronie powitania bazy danych użytkowników.

-   **Synchronizowanie danych:** synchronizacji danych zaprojektowano w model gwiazdy. Witaj Centrum przeprowadza synchronizację z każdym elemencie członkowskim pojedynczo. Zmiany z hello koncentratora są elementami członkowskimi toohello pobrany, a następnie zmiany z elementu członkowskiego hello zostaną przekazane toohello koncentratora.

-   **Rozwiązywanie konfliktów:** synchronizacji danych są dostępne dwie opcje do rozwiązywania konfliktów *wins Centrum* lub *wins elementu członkowskiego*.
    -   W przypadku wybrania *wins Centrum*, hello zmiany w Centrum hello zawsze zastąpienie zmian w elemencie członkowskim hello.
    -   W przypadku wybrania *wins elementu członkowskiego*, zmiany w hello zmian Zastąp elementów członkowskich w Centrum hello hello. Jeśli istnieje więcej niż jeden element członkowski, końcowa wartość hello zależy który element członkowski jest najpierw zsynchronizowane.

## <a name="limitations-and-considerations"></a>Ograniczenia i zagadnienia

### <a name="performance-impact"></a>Wpływ na wydajność
Używa synchronizacji danych wstawiania, aktualizowania i usuwania wyzwalaczy tootrack zmiany. Tworzy tabele w bazie danych użytkownika hello śledzenie zmian. Te działania śledzenia zmiany mają wpływ na obciążenie bazy danych. Ocenia warstwę usługi i uaktualnienia, jeśli to konieczne.

### <a name="eventual-consistency"></a>Spójność ostateczna
Ponieważ synchronizacji danych na podstawie wyzwalacza, nie gwarantuje spójności transakcyjnej. Microsoft gwarantuje wprowadzone po pewnym czasie wszystkie zmiany i synchronizacji danych nie powoduje utraty danych.

### <a name="unsupported-data-types"></a>Nieobsługiwane typy danych

-   FileStream

-   UDT SQL/CLR

-   Kolekcji XMLSchemaCollection (XML obsługiwane)

-   Kursor, Timestamp, Hierarchyid

### <a name="requirements"></a>Wymagania

-   Każda tabela musi mieć klucz podstawowy.

-   Tabela nie może mieć kolumnę tożsamości, która nie jest kluczem podstawowym hello.

-   Hello nazwy obiektów (baz danych, tabel i kolumn) nie może zawierać hello drukowalne znaki kropki (.), lewego nawiasu kwadratowego ([]), lub prawo kwadratowa nawiasu (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Ograniczenia dotyczące wymiarów usługi i bazy danych

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Wymiary**                                                      | **Limit**              | **Obejście problemu**              |
| Maksymalna liczba grup synchronizacji wszystkie bazy danych może należeć do.       | 5                      |                             |
| Maksymalna liczba punktów końcowych w grupie jednej synchronizacji              | 30                     | Utwórz wiele grup synchronizacji |
| Maksymalna liczba punktów końcowych lokalnie w jednej synchronizacji grupy. | 5                      | Utwórz wiele grup synchronizacji |
| Nazwy bazy danych, tabel, schematów i kolumn                       | 50 znaków według nazwy |                             |
| Tabele w grupie synchronizacji                                          | 500                    | Utwórz wiele grup synchronizacji |
| Kolumn w tabeli w grupie synchronizacji                              | 1000                   |                             |
| Rozmiar wiersza danych w tabeli                                        | 24 mb                  |                             |
| Interwał synchronizacji minimalna                                           | 5 minut              |                             |

## <a name="common-questions"></a>Często zadawane pytania

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>Częstotliwość synchronizacji danych można synchronizować dane? 
Minimalna częstotliwość Hello jest co pięć minut.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>Można użyć toosync synchronizacji danych między lokalnymi baz danych serwera SQL tylko? 
Nie bezpośrednio. Można zsynchronizować między bazami danych programu SQL Server lokalne pośrednio, jednak tworzenia Centrum bazy danych na platformie Azure, a następnie dodając hello lokalnych baz danych toohello synchronizacji grupy.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>Można użyć danych tooseed synchronizacji danych z mojej produkcji tooan pusta baza danych i następnie były synchronizowane? 
Tak. Schemat hello ręcznie utworzyć hello nowej bazy danych za pomocą skryptu go z oryginalnego hello. Po utworzeniu hello schemat, dodać dane hello toocopy hello tabel tooa synchronizacji grupy i przechowywać zsynchronizowane.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>Dlaczego widzę tabel, które I nie może utworzyć?  
Synchronizacja danych tworzy tabele w bazie danych śledzenia zmian. Nie należy usuwać je lub synchronizacji danych przestanie działać.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>Otrzymano komunikat o błędzie, który powiedział "nie można wstawić hello wartości NULL w kolumnie hello \<kolumny\>. Kolumna nie dopuszcza wartości null." Co to znaczy i jak można naprawić błąd hello? 
Ten komunikat o błędzie wskazuje jeden Witaj dwie następujące problemy:
1.  Może istnieć bez klucza podstawowego tabeli. toofix ten problem, Dodaj tabele hello tooall klucza podstawowego w przypadku synchronizacji.
2.  Może być klauzuli WHERE w instrukcji CREATE INDEX. Synchronizacja nie obsługuje tego warunku. toofix ten problem, Usuń hello klauzuli WHERE lub ręcznie wprowadzić zmiany hello tooall baz danych. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>Jak synchronizacja danych obsługuje odwołania cykliczne? Oznacza to, kiedy hello te same dane jest zsynchronizowany w wielu grupach synchronizacji i śledzi zmiany w związku z tym?
Synchronizacja danych nie obsługuje odwołań cyklicznych. Tooavoid się, że można je. 

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat synchronizacji danych SQL zobacz:

-   [Wprowadzenie do synchronizacji danych SQL](sql-database-get-started-sql-data-sync.md)

-   Zakończenie przykłady z programu PowerShell, które zawierają sposobu synchronizacji danych SQL tooconfigure:
    -   [Użyj programu PowerShell toosync między wiele baz danych Azure SQL](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Użyj programu PowerShell toosync między bazą danych SQL Azure i lokalnej bazy danych programu SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Pobierz pełną dokumentację techniczną hello synchronizacji danych SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Pobierz hello dokumentacji interfejsu API REST synchronizacji danych SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Aby uzyskać więcej informacji na temat bazy danych SQL zobacz:

-   [Omówienie bazy danych SQL](sql-database-technical-overview.md)

-   [Zarządzanie cyklem życia bazy danych](https://msdn.microsoft.com/library/jj907294.aspx)
