---
title: "aaaBest wskazówki dotyczące usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Zalecenia i najlepsze praktyki, których stosowanie zaleca się podczas tworzenia rozwiązań dla usługi Azure SQL Data Warehouse. Dzięki nim łatwiej jest odnieść sukces."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse
W tym artykule jest kolekcją wiele najlepszych rozwiązań, które pomogą Ci tooachieve optymalnej wydajności z usługi Azure SQL Data Warehouse.  Niektóre z pojęć hello w tym artykule są tooexplain podstawowe i łatwe i innych koncepcji są bardziej zaawansowane powierzchni hello możemy scratch właśnie w tym artykule.  Celem tego artykułu Hello jest toogive niektóre podstawowe wskazówki i tooraise pogłębianie wiedzy na temat toofocus obszarów ważne podczas tworzenia magazynu danych.  Każda sekcja wprowadzono pojęcie tooa, a następnie punktu toomore szczegółowe artykuły, które obejmują koncepcji hello bardziej szczegółowo.

Użytkownicy rozpoczynający korzystanie z usługi Azure SQL Data Warehouse nie powinni przerażać się bogactwem informacji zawartych w tym artykule.  Hello sekwencji tematów hello jest przeważnie hello według ważności.  Możesz uruchomić koncentrujących się na powitania najpierw kilka pojęć, będziesz w dobrej kształtu.  Wraz ze wzrostem umiejętności i wiedzy z zakresu usługi SQL Data Warehouse warto powracać do tego artykułu, aby poświęcić nieco uwagi kolejnym koncepcjom.  Nie zostanie znaków dla wszystkich toomake znaczeniu.

## <a name="reduce-cost-with-pause-and-scale"></a>Obniżenie kosztów dzięki wstrzymaniu i skalowaniu
Kluczowych funkcji usługi SQL Data Warehouse jest toopause możliwości hello gdy nie używasz, co uniemożliwia rozliczeń hello zasobów obliczeniowych.  Inna funkcja klucza jest hello możliwości tooscale zasobów.  Wstrzymywanie i skalowanie mogą być przeprowadzane za pośrednictwem portalu Azure hello lub za pomocą poleceń programu PowerShell.  Zapoznanie się z tych funkcji zgodnie z ich znacznie zmniejszyć koszt hello magazynu danych, gdy nie jest używany.  Jeśli chcesz zawsze magazyn danych dostępny, można tooconsider zmniejszania toohello najmniejszy rozmiar, DW100 zamiast wstrzymanie.

Zobacz też artykuły [Wstrzymywanie zasobów obliczeniowych][Pause compute resources], [Wznawianie zasobów obliczeniowych][Resume compute resources] i [Skalowanie zasobów obliczeniowych].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Opróżnianie transakcji przed wstrzymywaniem i skalowaniem
Po wstrzymaniu lub skalowania SQL Data Warehouse tle hello, który zapytań są anulowane po zainicjowaniu hello wstrzymania lub skalować żądania.  Anulowanie prostego zapytania SELECT jest operacją szybki i prawie nie czasu toohello wpływu, jaki zajmuje toopause lub skalowanie wystąpienia.  Jednak transakcyjne zapytań, które zmodyfikować struktury danych lub hello hello danych, nie może być toostop mogli szybko.  **Zapytania transakcyjne należy z założenia wykonać w całości lub wycofać ich zmiany.**  Wycofywanie hello wykonania transakcyjne kwerendy może zająć, ponieważ długi, lub nawet dłuższy niż oryginalny zmiany hello hello zapytanie zostało stosowania.  Na przykład jeśli anulujesz kwerendę, która została usuwanie wierszy i zostało już uruchomione na godziny, może zająć systemu hello godzinę tooinsert wstecz hello wiersze, które zostały usunięte.  Po uruchomieniu pauzę lub skalowanie podczas transakcje są transmitowane, Twoje Wstrzymaj lub skalowanie może wydawać się tootake dużo czasu, ponieważ wstrzymywanie i skalowanie ma toowait dla toocomplete wycofywania hello przed jego rozpoczęciem.

Zobacz także artykuły [Omówienie transakcji][Understanding transactions] i [Optymalizowanie transakcji][Optimizing transactions]

## <a name="maintain-statistics"></a>Prowadzenie statystyk
W przeciwieństwie do programu SQL Server, który automatycznie wykrywa i tworzy lub aktualizuje statystyki kolumn, usługa SQL Data Warehouse wymaga ręcznego prowadzenia statystyk.  Gdy planujemy toochange to w przyszłych, dla teraz można toomaintain Twojego tooensure statystyk, który hello planów usługi SQL Data Warehouse hello są zoptymalizowane.  utworzone przez optymalizator hello planów Hello są tylko dobrą hello dostępne statystyki.  **Tworzenie statystyk próbki w każdej kolumnie jest tooget łatwy sposób pracy z statystyk.**  Równie jest tooupdate ważnych statystyk jako tooyour danych wprowadzenia znaczące zmiany.  Tradycyjne podejście może być tooupdate statystyk codziennie lub po każdej obciążenia.  Zawsze są kompromis między wydajnością i hello koszt toocreate i aktualizację statystyk. Jeśli okaże się, że trwa zbyt długo toomaintain wszystkich statystyk, możesz się, że toobe tootry więcej selektywnie, które kolumny mają statystyk lub kolumny, które wymagają częstego aktualizowania.  Na przykład można tooupdate kolumn dat, gdy nowe wartości może być dodany, codziennie. **Witaj będzie uzyskać największe korzyści, uzyskanie statystyki do kolumn uczestniczących w sprzężeniu, kolumn używanych w hello klauzuli i kolumny wykrytych GROUP BY.**

Zobacz też artykuły [Zarządzanie statystykami tabel][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS] i [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>Grupowanie instrukcji INSERT w partie
Jednorazowe obciążenia tooa małą tabelę z instrukcji INSERT lub nawet okresowe Załaduj odnośników może wykonywać świetnie dla potrzeb z instrukcją, takich jak `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Jednak tooload tysiące lub miliony wierszy w ciągu dnia hello należy może się okazać, że pojedyncza WSTAWIA właśnie nie może przechowywać.  Zamiast tego należy utworzyć procesów, aby zapisują tooa pliku, a inny proces okresowo pochodzi i ładuje tego pliku.

Zobacz też artykuł poświęcony instrukcji [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>Szybko Użyj programu PolyBase tooload i eksportowanie danych
Usługa SQL Data Warehouse obsługuje ładowanie i eksportowanie danych za pośrednictwem kilku narzędzi, w tym Azure Data Factory, PolyBase i BCP.  W przypadku małych ilości danych, gdy wydajność nie ma decydującego znaczenia, można zastosować dowolne narzędzie.  Podczas ładowania lub eksportowania dużych ilości danych lub jest wymagana duża wydajność, PolyBase jest jednak najlepszym wyborem hello.  PolyBase to architektura MPP (Massively Parallel Processing) hello zaprojektowanego tooleverage usługi SQL Data Warehouse, a także w związku z tym obciążenia i wyeksportować wielkości dane szybciej niż przy użyciu innych narzędzi.  Obciążenia funkcji PolyBase można uruchomić za pomocą instrukcji CTAS lub INSERT INTO.  **Przy użyciu CTAS zostanie zminimalizowane rejestrowania transakcji i hello najszybszy sposób tooload danych.**  Usługa Azure Data Factory obsługuje również obciążenia funkcji PolyBase.  Funkcja PolyBase obsługuje wiele formatów plików, w tym pliki Gzip.  **Przepływność toomaximize, gdy przy użyciu gzip pliki tekstowe, pliki podziału do 60 lub więcej plików toomaximize równoległości obciążenia.**  W celu uzyskania szybszej całkowitej przepływności warto rozważyć równoległe ładowania danych.

Zobacz też [Ładowanie danych][Load data], [Przewodnik po funkcji PolyBase][Guide for using PolyBase], [Wzorce i strategie ładowania danych w usłudze Azure SQL Data Warehouse][Azure SQL Data Warehouse loading patterns and strategies], [Ładowanie danych za pomocą usługi Azure Data Factory][Load Data with Azure Data Factory], [Przenoszenie danych za pomocą usługi Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] i [Tworzenie tabeli przy użyciu instrukcji Select (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Ładowanie i przesyłanie zapytań dotyczących tabel zewnętrznych
Polybase, znanej także jako tabele zewnętrzne mogą być hello najszybszy sposób tooload danych, nie jest optymalna dla zapytania. Obecnie tabele funkcji Polybase w usłudze SQL Data Warehouse obsługują tylko pliki obiektów blob platformy Azure. Te pliki nie mają żadnych zasobów obliczeniowych stanowiących ich zaplecze.  W związku z tym SQL Data Warehouse nie może odciążyć tę pracę i w związku z tym musi odczytać całego pliku hello przez załadowanie go tootempdb w kolejności tooread hello danych.  W związku z tym jeśli masz kilka zapytań, które będą badania tych danych jest lepsze tooload te dane raz i mieć zapytania tabeli lokalne powitania.

Zobacz także artykuł [Przewodnik po funkcji PolyBase][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Dystrybucja dużych tabel z użyciem skrótów
Domyślnym sposobem dystrybucji tabel jest działanie okrężne.  Ułatwia to tworzenie tabel bez konieczności toodecide rozkład ich tabel tooget użytkowników.  Tabele wykorzystujące działanie okrężne mogą zapewniać wydajność wystarczającą dla niektórych obciążeń, ale w większości przypadków wybór kolumny dystrybucji sprawdzi się znacznie lepiej.  Hello najczęściej przykładem po dystrybuowane za pomocą kolumny tabeli do tej pory przewyższyć tabeli działanie okrężne jest dwie tabele faktów dużych są połączone.  Na przykład jeśli masz tabeli zamówienia, które jest udostępniane przez ZAM_ID, i tabeli transakcji rozpowszechniane przez ZAM_ID, po dołączeniu do tabeli transakcji tooyour tabeli zamówienia na ZAM_ID, to zapytanie staje się zapytania przekazującego, co oznacza Firma Microsoft wyeliminować operacje przenoszenia danych.  Mniej kroków to szybsze kwerendy.  Mniejsza konieczność przenoszenia danych wpływa także na skrócenie czasu działania kwerend.  Wyjaśnienie to po prostu zadrapania hello powierzchni. Podczas ładowania tabeli rozproszonych, pamiętaj, że przychodzących danych nie jest sortowana na powitania dystrybucji kluczy, w to spowolni obciążenia sieci.  Zobacz poniższe hello łączy dla znacznie więcej informacji na temat sposobu wybranie kolumny dystrybucji może poprawić wydajność oraz toodefine rozproszonej tabeli w klauzuli WITH hello instrukcji tworzenia tabel.

Zobacz także [Omówienie tabel][Table overview], [Dystrybucja tabel][Table distribution], [Wybór dystrybucji tabel][Selecting table distribution], [CREATE TABLE][CREATE TABLE] i [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Unikanie nadmiernego partycjonowania
O ile partycjonowanie danych może stanowić bardzo skuteczny sposób na obsługę danych poprzez przełączanie partycji lub optymalizowanie skanowań z eliminacją partycji, o tyle użycie zbyt dużej liczby partycji może spowolnić wykonywanie zapytań.  Strategie zakładające zastosowanie wysokiego stopnia szczegółowości partycjonowania danych, które mogą działać poprawnie w programie SQL Server, mogą nie działać dobrze w usłudze SQL Data Warehouse.  Zbyt wiele partycji mających pomaga również zmniejszyć skuteczność hello klastrowane indeksy magazynu kolumn, gdy każda partycja zawiera mniej niż 1 milion wierszy.  Należy pamiętać, że tle hello SQL Data Warehouse partycje danych dla Ciebie do 60 baz danych, więc jeśli utworzysz tabelę z partycjami 100 faktycznie w efekcie 6000 partycji.  Poszczególnych obciążeń różni się więc porady najlepsze hello jest tooexperiment z partycjonowania toosee co najlepiej będzie działać dla obciążenia.  Warto rozważyć stopień szczegółowości niższy od pomyślnie zastosowanego w programie SQL Server.  Można na przykład rozważyć wykorzystanie partycji cotygodniowych lub comiesięcznych zamiast partycji codziennych.

Zobacz też artykuł [Partycjonowanie tabel][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Minimalizowanie rozmiarów transakcji
Instrukcje INSERT, UPDATE i DELETE działają w obrębie transakcji i muszą zostać wycofane, jeśli zakończą się niepowodzeniem.  hello toominimize możliwość wycofywania długie, zminimalizować rozmiary transakcji, jeśli to możliwe.  Można to zrobić poprzez podział instrukcji INSERT, UPDATE i DELETE na części.  Na przykład jeśli masz WSTAWIENIEM, w którym oczekujesz tootake 1 godziny, jeśli to możliwe, podzielić hello WSTAWIANIA do 4 części, które zostaną każdego uruchomione w ciągu 15 minut.  Korzystaj z szczególnych przypadkach minimalnego rejestrowania, takich jak CTAS, TRUNCATE, DROP TABLE lub wstawianie tooempty tabel, tooreduce wycofywania ryzyka.  Inny sposób tooeliminate wycofań jest toouse metadane tylko operacje takie jak partycja przełączania w celu zarządzania danymi.  Na przykład raczej nie zostanie wykonane toodelete instrukcji DELETE wszystkie wiersze w tabeli, w którym hello order_date było października 2001, możesz można partycje danych co miesiąc i następnie do przełączania z partycji hello z pustym partycji z innej tabeli (patrz ALTER Przykłady tabeli).  W przypadku tabel podzielony na partycje należy wziąć pod uwagę przy użyciu danych hello toowrite CTAS ma tookeep w tabeli, a nie używanie opcji usuwania.  Jeśli CTAS przyjmuje hello czasie, jest znacznie bezpieczniejsze toorun operacji, ponieważ ma minimalne transakcji rejestrowania i mogą zostać anulowane szybkiego, w razie potrzeby.

Zobacz także artykuły [Omówienie transakcji][Understanding transactions], [Optymalizowanie transakcji][Optimizing transactions], [Partycjonowanie tabel][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE] i [Tworzenie tabeli przy użyciu instrukcji Select (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Użyj hello najmniejsze możliwe kolumny
Podczas definiowania kod DDL, przy użyciu hello najmniejszą typ danych, który będzie obsługiwać danych umożliwi zwiększenie wydajności zapytania.  Jest to szczególnie ważne w przypadku kolumn CHAR i VARCHAR.  Jeśli hello najdłuższym wartość w kolumnie 25 znaków, Zdefiniuj kolumny jako VARCHAR(25).  Unikaj definiowania wszystkich kolumn tooa domyślne dużych znaków.  Ponadto należy unikać stosowania kolumn NVARCHAR, jeśli zastosowanie typu VARCHAR spełni wymagania danego zastosowania.

Zobacz także artykuły [Omówienie tabel][Table overview], [Typy danych w tabelach][Table data types] i [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Korzystanie z tymczasowych tabel stosów dla danych przejściowych
Gdy dane są tymczasowo kierowanych na SQL Data Warehouse, może się okazać, że przy użyciu tabeli sterty dokona szybciej hello całego procesu.  Przypadku ładowania danych toostage tylko przed uruchomieniem więcej przekształcenia, ładowanie hello tooheap tabeli będzie znacznie szybsze niż ładowania tooa danych hello klastrowanego magazynu kolumn tabeli.  Ponadto podczas ładowania danych tooa tabeli tymczasowej również załaduje znacznie szybciej niż ładowania magazynu toopermanent tabeli.  Tabele tymczasowe rozpoczynać się od znaku "#" i są dostępne jedynie przez sesję hello, w której został utworzony, więc może obowiązywało tylko w scenariuszach ograniczone.   Tabele sterty są definiowane w klauzuli WITH hello CREATE TABLE.  Jeśli używasz tabeli tymczasowej, za Pamiętaj toocreate statystyki dotyczące tej tabeli tymczasowej.

Zobacz także artykuły [Tabele tymczasowe][Temporary tables], [CREATE TABLE][CREATE TABLE] i [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Optymalizowanie tabel klastrowanego magazynu kolumn
Klastrowane indeksy magazynu kolumn są hello sposoby najbardziej efektywne, można przechowywać dane w magazynie danych SQL Azure.  Domyślnie tabele w usłudze SQL Data Warehouse są tworzone jako tabele Clustered ColumnStore, czyli tabele klastrowanego magazynu kolumn.  ważne jest tooget hello najlepszą wydajność kwerend w tabelach magazynu kolumn, najwyższą jakość dobrej segmentu.  Jeśli wiersze są zapisywane tabel toocolumnstore wykorzystanie pamięci, może to spowodować obniżenie jakości segmentu magazynu kolumn.  Jakość segmentu określa się na podstawie liczby wierszy w skompresowanej grupie wierszy.  Zobacz hello [przyczyny niskiej magazynu kolumn indeksu jakości] [ Causes of poor columnstore index quality] w hello [indeksów tabeli] [ Table indexes] artykuł instrukcje krok po kroku na wykrywanie i poprawy jakości segmentu dla tabel klastrowanego magazynu kolumn.  Wysokiej jakości segmentów magazynu kolumn jest ważne, dlatego jest identyfikatorów użytkowników toouse dobrym rozwiązaniem, które należą do klasy zasobu średnich i dużych hello ładowania danych.  Witaj mniejszej liczby jednostek dwu używasz, hello większych hello klasy zasobów można tooyour tooassign ładowania użytkownika.

Ponieważ magazynu kolumn tabel zazwyczaj nie wypychanie danych do segmentu skompresowany magazynu kolumn dopóki istnieje więcej niż 1 milion wierszy w tabeli i każdej tabeli SQL Data Warehouse jest podzielona na partycje w tabelach 60 jako zasadą, tabele magazynu kolumn nie będzie korzystna zapytania Jeśli tabela hello ma więcej niż 60 mln wierszy.  Dla tabeli z mniej niż 60 mln wierszy może nie mieć żadnych toohave znaczeniu indeksu magazynu kolumn.  Jego użycie nie przyniesie też jednak niekorzystnych skutków.  Ponadto jeśli partycji danych, następnie można tooconsider każda partycja musi toohave 1 milion wierszy toobenefit z klastrowanego indeksu magazynu kolumn.  Jeśli tabela ma partycje 100, a następnie konieczne będzie toohave co najmniej 6 miliard wierszy toobenefit z magazynu klastrowanego kolumn (60 dystrybucje * partycje 100 * 1 milion wierszy).  Jeśli tabela nie ma 6 miliardy wierszy w tym przykładzie, Zmniejsz liczbę hello partycji lub tabeli sterty zamiast tego Rozważ użycie.  Również może być warto eksperymentowanie toosee Jeśli lepszą wydajność można uzyskać z tabeli sterty z indeksów pomocniczych zamiast tabeli magazynu kolumn.  Tabele magazynu kolumn nie obsługują jeszcze indeksów pomocniczych.

Podczas wykonywania zapytania w tabeli magazynu kolumn, zapytania będzie szybsze w przypadku wybrania tylko kolumny hello potrzebne.  

Zobacz także artykuły [Indeksy tabel][Table indexes], [Przewodnik po indeksach magazynu kolumn][Columnstore indexes guide] i [Ponowne tworzenie indeksów magazynu kolumn][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Użyj większą wydajność zapytań tooimprove klasy zasobu
Usługi SQL Data Warehouse korzysta z grup zasobów jako tooqueries pamięci tooallocate sposób.  Fabrycznej hello wszyscy użytkownicy są przypisywane toohello małych zasobów klasy, która udziela 100 MB pamięci dla dystrybucji.  Ponieważ są zawsze 60 dystrybucji, a każdy dystrybucji znajduje się co najmniej 100 MB, system hello szerokości całkowitej ilości pamięci alokacji jest 6000 MB lub po prostu mniej niż 6 GB.  Niektóre kwerendy, takich jak sprzężenia dużych lub obciążeń tooclustered magazynu kolumn tabel, będą korzystać z większej alokacji pamięci.  W przypadku innych kwerend, takich jak czyste skanowanie, korzyść z ich zastosowania będzie niezauważalna.  Na stronie Przerzucanie hello przy użyciu klasy zasobów o większych ma wpływ na współbieżności, więc można tootake to pod uwagę przed przeniesieniem wszystkie klasy zasobu dużych tooa użytkowników.

Zobacz także artykuł [Współbieżność i zarządzanie obciążeniami][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Użyj mniejszych klasy zasobów tooIncrease współbieżności
Jeśli są powiadamiania, że zapytania użytkownika prawdopodobnie toohave długim opóźnieniu, możliwe, że użytkownicy są uruchomione w większych klasy zasobów i zużywa bardzo dużo miejsc współbieżności powoduje tooqueue innych zapytań się.  toosee kwerend użytkowników są umieszczane w kolejce, uruchom `SELECT * FROM sys.dm_pdw_waits` toosee, jeśli nie zostały zwrócone żadne wiersze.

Zobacz także artykuł [Współbieżność i zarządzanie obciążeniami][Concurrency and workload management] i [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Przy użyciu widoków DMV toomonitor a optymalizacji zapytań
Magazyn danych SQL ma kilka widoków DMV, które mogą być używane toomonitor wykonywania zapytania.  Hello monitorowania poniżej artykuł przeprowadzi Cię przez instrukcje krok po kroku w sposób toolook na powitania szczegóły wykonywania zapytania.  zapytania wyszukiwania tooquickly w tych widoków DMV, przy użyciu opcji etykiety hello z zapytań może pomóc.

Zobacz także artykuły [Monitorowanie obciążenia przy użyciu widoków DMV][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Inne zasoby
Zobacz artykuł [Rozwiązywanie problemów][Troubleshooting], w którym omówiono typowe problemy i ich rozwiązania.

Jeśli nie udało się znaleźć, czego szukasz w tym artykule, spróbuj użyć hello "Szukaj docs" hello lewej strony z tej strony toosearch wszystkie hello Azure SQL Data Warehouse dokumentów.  Witaj [Forum MSDN magazynu danych SQL Azure] [ Azure SQL Data Warehouse MSDN Forum] został utworzyć jako miejsca możesz tooask pytania użytkowników tooother i toohello grupę produktu magazynu danych SQL.  Firma Microsoft aktywne monitorowanie tego tooensure forum, że Twoje odpowiedzi na pytania przez innego użytkownika lub jedną z nami.  Jeśli wolisz tooask pytania w witrynie Stack Overflow, będziemy również mieć [Azure SQL Data magazynu stosu przepełnienie Forum][Azure SQL Data Warehouse Stack Overflow Forum].

Na koniec użyj hello [opinii magazynu danych SQL Azure] [ Azure SQL Data Warehouse Feedback] toomake funkcji żądań strony.  Dodawanie konkretnych propozycji lub głosowanie na już zgłoszone sugestie bardzo pomaga nam określać priorytety funkcji.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Skalowanie zasobów obliczeniowych]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
