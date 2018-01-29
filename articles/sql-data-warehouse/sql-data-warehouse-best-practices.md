---
title: "Najlepsze praktyki dotyczące usługi Azure SQL Data Warehouse | Microsoft Docs"
description: "Zalecenia i najlepsze praktyki, których stosowanie zaleca się podczas tworzenia rozwiązań dla usługi Azure SQL Data Warehouse. Dzięki nim łatwiej jest odnieść sukces."
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jenniehubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 12/06/2017
ms.author: barbkess
ms.openlocfilehash: 861c2c977fa9d0341125127852bc7747dfd6001a
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse
W tym artykule zebrano szereg najlepszych praktyk, które pomogą optymalnie wykorzystać możliwości usługi Azure SQL Data Warehouse.  Niektóre kwestie poruszane w tym artykule mają charakter podstawowy i są łatwe do wyjaśnienia. Inne są bardziej zaawansowane i zostaną tu omówione jedynie powierzchownie.  Celem tego artykułu jest dostarczenie podstawowych wskazówek oraz zwiększenie wiedzy w zakresie ważnych obszarów, na których należy skupić się, tworząc magazyn danych.  Każda sekcja wprowadza konkretną koncepcję i prowadzi do bardziej szczegółowych artykułów, w których dana koncepcja została omówiona bardziej szczegółowo.

Użytkownicy rozpoczynający korzystanie z usługi Azure SQL Data Warehouse nie powinni przerażać się bogactwem informacji zawartych w tym artykule.  Zasadniczo tematy zostały uporządkowane według ważności.  Na początek warto skupić się choćby na kilku pierwszych koncepcjach — pozwoli to uzyskać znaczne korzyści.  Wraz ze wzrostem umiejętności i wiedzy z zakresu usługi SQL Data Warehouse warto powracać do tego artykułu, aby poświęcić nieco uwagi kolejnym koncepcjom.  Wkrótce wszystko zacznie składać się w spójną całość.

Aby uzyskać wskazówki dotyczące ładowania, zobacz [Wskazówki dotyczące ładowania danych](guidance-for-loading-data.md).

## <a name="reduce-cost-with-pause-and-scale"></a>Obniżenie kosztów dzięki wstrzymaniu i skalowaniu
Kluczową cechą usługi SQL Data Warehouse jest możliwość jej wstrzymania w sytuacji, gdy nie jest ona używana. Pozwala to przerwać naliczanie opłat za zasoby obliczeniowe.  Inną niezwykle ważną cechą jest możliwość skalowania zasobów.  Wstrzymywanie i skalowanie można przeprowadzać w witrynie Azure Portal lub za pomocą poleceń programu PowerShell.  Należy zapoznać się z tymi funkcjami, ponieważ ich użycie pozwala znacznie obniżyć koszty magazynu danych w czasie, gdy nie jest on używany.  Jeśli magazyn danych ma być zawsze dostępny, zamiast go wstrzymywać, warto rozważyć skalowanie w dół do najmniejszego możliwego rozmiaru (DW100).

Zobacz też artykuły [Wstrzymywanie zasobów obliczeniowych][Pause compute resources], [Wznawianie zasobów obliczeniowych][Resume compute resources] i [Skalowanie zasobów obliczeniowych].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Opróżnianie transakcji przed wstrzymywaniem i skalowaniem
Gdy ma zostać przeprowadzona procedura wstrzymania lub skalowania usługi SQL Data Warehouse, po zainicjowaniu odpowiedniego żądania następuje anulowanie zapytań w tle.  Anulowanie prostego zapytania typu SELECT to szybka operacja, która nie ma prawie żadnego wpływu na czas wstrzymywania lub skalowania wystąpienia.  Może jednak nie być możliwe szybkie zatrzymanie zapytań transakcyjnych, które modyfikują dane lub ich strukturę.  **Zapytania transakcyjne należy z założenia wykonać w całości lub wycofać ich zmiany.**  Całkowite cofnięcie wyników działania zapytania transakcyjnego może trwać równie długo lub nawet dłużej niż pierwotna zmiana wprowadzona przez zapytanie.  Na przykład w przypadku anulowania zapytania, którego zadaniem było usunięcie wierszy i które było uruchomione przez godzinę, może upłynąć kolejna godzina, zanim system z powrotem wstawi wiersze, które zostały usunięte.  W przypadku uruchomienia procedury wstrzymywania lub skalowania w toku transakcji operacja wstrzymywania lub skalowania może zająć dużo czasu, ponieważ zanim będzie możliwe jej wykonanie, zmiany muszą zostać w pełni cofnięte.

Zobacz także artykuły [Omówienie transakcji][Understanding transactions] i [Optymalizowanie transakcji][Optimizing transactions]

## <a name="maintain-statistics"></a>Prowadzenie statystyk
W przeciwieństwie do programu SQL Server, który automatycznie wykrywa i tworzy lub aktualizuje statystyki kolumn, usługa SQL Data Warehouse wymaga ręcznego prowadzenia statystyk.  Planujemy zmienić to w przyszłości, ale obecnie warto prowadzić statystyki, aby mieć pewność, że plany usługi SQL Data Warehouse są zoptymalizowane.  Rzeczywista wartość planów tworzonych przez optymalizator zależy od jakości dostępnych statystyk.  **Utworzenie próbkowanych statystyk dla każdej z kolumn to prosty sposób na rozpoczęcie pracy ze statystykami.**  Równie ważne jest aktualizowanie statystyk w miarę pojawiania się kolejnych znaczących zmian w danych.  Zachowawcze podejście nakazywałoby aktualizowanie statystyk codziennie lub po każdym obciążeniu.  Zawsze istnieje możliwość wypracowania kompromisu pomiędzy wydajnością a kosztami tworzenia i aktualizowania statystyk. Jeśli okaże się, że utrzymywanie wszystkich statystyk trwa zbyt długo, można spróbować wybrać tylko niektóre kolumny, dla których mają być prowadzone statystyki, lub wybrać kolumny, które wymagają częstego aktualizowania.  Można na przykład aktualizować kolumny danych, w których codziennie mogą być dodawane nowe wartości. **Największe korzyści można osiągnąć, prowadząc statystyki dla kolumn uczestniczących w sprzężeniach, kolumn używanych w ramach klauzuli WHERE i kolumn z klauzuli GROUP BY.**

Zobacz też artykuły [Zarządzanie statystykami tabel][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS] i [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>Grupowanie instrukcji INSERT w partie
Jednorazowe załadowanie do małej tabeli za pomocą instrukcji INSERT lub nawet okresowe przeładowanie wyszukiwania to strategie, które mogą sprawdzić się w przypadku instrukcji takich jak `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Jeśli jednak wymagane jest ładowanie tysięcy lub milionów wierszy na dzień, może okazać się, że same instrukcje INSERT zwyczajnie nie nadążą z działaniem.  Zamiast tego należy opracować procesy w taki sposób, aby zapisywały dane do pliku, po czym będzie następować okresowe uruchamianie innego procesu, który będzie ładować wspomniany plik.

Zobacz też artykuł poświęcony instrukcji [INSERT][INSERT]

## <a name="use-polybase-to-load-and-export-data-quickly"></a>Korzystanie z funkcji PolyBase do szybkiego ładowania i eksportowania danych
Usługa SQL Data Warehouse obsługuje ładowanie i eksportowanie danych za pośrednictwem kilku narzędzi, w tym Azure Data Factory, PolyBase i BCP.  W przypadku małych ilości danych, gdy wydajność nie ma decydującego znaczenia, można zastosować dowolne narzędzie.  Jednak podczas ładowania lub eksportowania dużych ilości danych lub w przypadku, gdy wymagana jest wysoka wydajność, najlepszym wyborem jest funkcja PolyBase.  Funkcja PolyBase wykorzystuje architekturę MPP (Massively Parallel Processing) usługi SQL Data Warehouse, w związku z czym ładuje i eksportuje znaczne ilości danych szybciej niż inne narzędzia.  Obciążenia funkcji PolyBase można uruchomić za pomocą instrukcji CTAS lub INSERT INTO.  **Użycie instrukcji CTAS minimalizuje rejestrowanie transakcji i stanowi najszybszy sposób ładowania danych.**  Usługa Azure Data Factory obsługuje również obciążenia funkcji PolyBase.  Funkcja PolyBase obsługuje wiele formatów plików, w tym pliki Gzip.  **Aby zmaksymalizować przepływność, korzystając z plików tekstowych gzip, należy podzielić pliki na 60 lub więcej plików w celu maksymalizacji równoległości obciążenia.**  W celu uzyskania szybszej całkowitej przepływności warto rozważyć równoległe ładowania danych.

Zobacz też [Ładowanie danych][Load data], [Przewodnik po funkcji PolyBase][Guide for using PolyBase], [Wzorce i strategie ładowania danych w usłudze Azure SQL Data Warehouse][Azure SQL Data Warehouse loading patterns and strategies], [Ładowanie danych za pomocą usługi Azure Data Factory][Load Data with Azure Data Factory], [Przenoszenie danych za pomocą usługi Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] i [Tworzenie tabeli przy użyciu instrukcji Select (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Ładowanie i przesyłanie zapytań dotyczących tabel zewnętrznych
O ile funkcja Polybase (nazywana też tabelami zewnętrznymi) może być najszybszym sposobem załadowania danych, nie jest to narzędzie zoptymalizowane pod kątem zapytań. Obecnie tabele funkcji Polybase w usłudze SQL Data Warehouse obsługują tylko pliki obiektów blob platformy Azure i magazyn usługi Azure Data Lake. Te pliki nie mają żadnych zasobów obliczeniowych stanowiących ich zaplecze.  W związku z tym usługa SQL Data Warehouse nie może odciążać tych zadań i, co za tym idzie, musi odczytać cały plik poprzez załadowanie go do bazy danych tempdb w celu odczytu danych.  W związku z tym mając kilka kwerend, które będą wykonywać zapytania dotyczące tych danych, lepiej jest załadować te dane jeden raz i zapewnić możliwość obejmowania zapytaniem lokalnej tabeli.

Zobacz także artykuł [Przewodnik po funkcji PolyBase][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Dystrybucja dużych tabel z użyciem skrótów
Domyślnym sposobem dystrybucji tabel jest działanie okrężne.  Dzięki temu użytkownicy mogą z łatwością rozpocząć tworzenie tabel bez konieczności podejmowania decyzji o tym, jak będzie przebiegać dystrybucja tabel.  Tabele wykorzystujące działanie okrężne mogą zapewniać wydajność wystarczającą dla niektórych obciążeń, ale w większości przypadków wybór kolumny dystrybucji sprawdzi się znacznie lepiej.  Najbardziej typowym przykładem sytuacji, w której zastosowanie dla tabeli dystrybucji według kolumny przyniesie znacznie lepsze wyniki niż zastosowanie tabeli z działaniem okrężnym, jest połączenie dwóch dużych tabel faktów.  Na przykład w przypadku tabeli z zamówieniami, która jest rozłożona według wartości id_zamowienia, oraz tabeli z transakcjami, która także jest rozłożona według wartości id_zamowienia, po połączeniu tabeli z zamówieniami z tabelą z transakcjami poprzez pola id_zamowienia, to zapytanie staje się kwerendą przekazującą, co oznacza, że zostają wyeliminowane operacje przenoszenia danych.  Mniej kroków to szybsze kwerendy.  Mniejsza konieczność przenoszenia danych wpływa także na skrócenie czasu działania kwerend.  To wyjaśnienie jest bardzo uproszczone. Podczas ładowania dystrybuowanej tabeli należy upewnić się, że dane przychodzące nie są sortowane według klucza dystrybucji, ponieważ mogłoby to spowolnić ładowanie.  Poniższe linki zawierają znacznie więcej szczegółowych informacji na temat tego, w jaki sposób wybór kolumny dystrybucji może zwiększyć wydajność oraz jak zdefiniować tabelę z dystrybucją w klauzuli WITH instrukcji CREATE TABLES.

Zobacz także [Omówienie tabel][Table overview], [Dystrybucja tabel][Table distribution], [Wybór dystrybucji tabel][Selecting table distribution], [CREATE TABLE][CREATE TABLE] i [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Unikanie nadmiernego partycjonowania
O ile partycjonowanie danych może stanowić bardzo skuteczny sposób na obsługę danych poprzez przełączanie partycji lub optymalizowanie skanowań z eliminacją partycji, o tyle użycie zbyt dużej liczby partycji może spowolnić wykonywanie zapytań.  Strategie zakładające zastosowanie wysokiego stopnia szczegółowości partycjonowania danych, które mogą działać poprawnie w programie SQL Server, mogą nie działać dobrze w usłudze SQL Data Warehouse.  Zbyt duża liczba partycji danych może także zmniejszyć skuteczność indeksów klastrowanego magazynu kolumn, jeśli każda partycja ma mniej niż milion wierszy.  Należy pamiętać, że usługa SQL Data Warehouse dzieli dane w tle na 60 baz danych, dlatego też w przypadku utworzenia tabeli ze 100 partycjami w istocie powstaje 6000 partycji.  Każde obciążenie jest inne, więc warto eksperymentować z podziałem na partycje — w ten sposób można przekonać się, jakie rozwiązanie sprawdzi się najlepiej w przypadku danego obciążenia.  Warto rozważyć stopień szczegółowości niższy od pomyślnie zastosowanego w programie SQL Server.  Można na przykład rozważyć wykorzystanie partycji cotygodniowych lub comiesięcznych zamiast partycji codziennych.

Zobacz też artykuł [Partycjonowanie tabel][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Minimalizowanie rozmiarów transakcji
Instrukcje INSERT, UPDATE i DELETE działają w obrębie transakcji i muszą zostać wycofane, jeśli zakończą się niepowodzeniem.  Aby zminimalizować ryzyko długiego czasu wycofywania, warto minimalizować rozmiary transakcji, gdy tylko jest to możliwe.  Można to zrobić poprzez podział instrukcji INSERT, UPDATE i DELETE na części.  Jeśli korzystasz na przykład z instrukcji INSERT, której przewidywany czas działania to 1 godzina, jeśli to możliwe, podziel ją na cztery części, z których każda będzie działać 15 minut.  Stosuj szczególne przypadki minimalnego rejestrowania, takie jak CTAS, TRUNCATE, DROP TABLE lub INSERT, do opróżniania tabel, aby zmniejszyć ryzyko wycofywania.  Innym sposobem na eliminację procesu wycofywania zmian jest korzystanie z operacji z właściwościami Tylko metadane, takich jak przełączanie partycji pod kątem zarządzania danymi.  Na przykład zamiast wykonywać instrukcję DELETE w celu usunięcia z tabeli wszystkich wierszy, dla których wartość data_zamowienia to październik 2001, można rozdzielić dane na miesiące, aby następnie przełączyć wybraną partycję na pustą partycję z innej tabeli (zobacz przykłady instrukcji ALTER TABLE).  W przypadku tabel niepartycjonowanych zamiast korzystać z instrukcji DELETE, należy rozważyć użycie instrukcji CTAS do zapisu danych, które mają zostać zachowane w tabeli.  Jeśli wykonanie instrukcji CTAS trwa tyle samo czasu, to na jej korzyść nadal przemawia znacznie większe bezpieczeństwo. Jej uruchomienie wiąże się z minimalnym rejestrowaniem, przez co operacja może w razie potrzeby zostać szybko anulowana.

Zobacz także artykuły [Omówienie transakcji][Understanding transactions], [Optymalizowanie transakcji][Optimizing transactions], [Partycjonowanie tabel][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE] i [Tworzenie tabeli przy użyciu instrukcji Select (CTAS)][Create table as select (CTAS)]

## <a name="use-the-smallest-possible-column-size"></a>Użycie możliwie najmniejszego rozmiaru kolumny
Użycie podczas definiowania kwerendy DDL najmniejszego typu danych, który umożliwi obsługę danych, zwiększy wydajność kwerendy.  Jest to szczególnie ważne w przypadku kolumn CHAR i VARCHAR.  Jeśli najdłuższa wartość w kolumnie ma 25 znaków, należy zdefiniować typ kolumny jako VARCHAR(25).  Należy unikać domyślnego definiowania wszystkich kolumn znaków jako kolumn długich wartości.  Ponadto należy unikać stosowania kolumn NVARCHAR, jeśli zastosowanie typu VARCHAR spełni wymagania danego zastosowania.

Zobacz także artykuły [Omówienie tabel][Table overview], [Typy danych w tabelach][Table data types] i [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Korzystanie z tymczasowych tabel stosów dla danych przejściowych
W przypadku tymczasowego kierowania danych do usługi SQL Data Warehouse może okazać się, że użycie tabeli stosu przyśpieszy cały proces.  Jeśli dane są ładowane tylko pod kątem przygotowania do uruchomienia kolejnych przekształceń, załadowanie tabeli do stosu będzie znacznie szybsze niż załadowanie danych do tabeli klastrowanego magazynu kolumn.  Ponadto załadowanie danych do tabeli tymczasowej będzie także znacznie szybsze niż załadowanie tabeli do pamięci trwałej.  Tabele tymczasowe zaczynają się od znaku „#” i są dostępne jedynie w ramach sesji, podczas której zostały utworzone. Sprawdzają się więc jedynie w ograniczonych scenariuszach.   Tabele stosu definiuje się przy użyciu klauzuli WITH instrukcji CREATE TABLE.  W przypadku użycia tabeli tymczasowej należy pamiętać o utworzeniu dla niej statystyk.

Zobacz także artykuły [Tabele tymczasowe][Temporary tables], [CREATE TABLE][CREATE TABLE] i [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Optymalizowanie tabel klastrowanego magazynu kolumn
Indeksy klastrowanego magazynu kolumn to jeden z najefektywniejszych sposobów na przechowywanie danych w usłudze SQL Data Warehouse.  Domyślnie tabele w usłudze SQL Data Warehouse są tworzone jako tabele Clustered ColumnStore, czyli tabele klastrowanego magazynu kolumn.  Dla uzyskania najlepszej wydajności kwerend w odniesieniu do tabel magazynu kolumn ważne jest zapewnienie dobrej jakości segmentów.  Jeśli wiersze są zapisywane w tabelach magazynu kolumn przy dużym wykorzystaniu pamięci, może to spowodować obniżenie jakości segmentów w magazynie kolumn.  Jakość segmentu określa się na podstawie liczby wierszy w skompresowanej grupie wierszy.  Zobacz sekcję [Przyczyny niskiej jakości indeksu magazynu kolumn][Causes of poor columnstore index quality] w artykule [Indeksy tabel][Table indexes], aby uzyskać instrukcje krok po kroku dotyczące sprawdzania i poprawiania jakości segmentu tabel klastrowanego magazynu kolumn.  Ze względu na znaczenie wysokiej jakości segmentów magazynu kolumn na potrzeby ładowania danych warto użyć identyfikatorów użytkowników, które należą do średniej lub dużej klasy zasobów. Użycie niższych [poziomów usług](performance-tiers.md#service-levels) oznacza, że chcesz do użytkownika ładującego przypisać większą klasę zasobów.

Jako że tabele magazynu kolumn zazwyczaj nie wypychają danych do skompresowanego segmentu magazynu kolumn aż do czasu, gdy liczba wierszy przekroczy milion na tabelę i gdy każda tabela w usłudze SQL Data Warehouse zostanie poddana partycjonowaniu na 60 tabel, jako ogólną regułę można przyjąć, że w przypadku tabel magazynu kolumn kwerendy nie przynoszą korzyści, o ile tabele te nie mają więcej niż 60 milionów wierszy.  Stosowanie indeksu magazynu kolumn może nie mieć sensu w przypadku tabel z mniej niż 60 milionami wierszy.  Jego użycie nie przyniesie też jednak niekorzystnych skutków.  Ponadto w przypadku partycjonowania danych warto wziąć pod uwagę, że każda partycja będzie musiała mieć milion wierszy, aby można było odnieść korzyść z zastosowania klastrowanego indeksu magazynu kolumn.  Jeśli tabela ma 100 partycji, będzie musiała mieć co najmniej 6 miliardów wierszy, aby skorzystanie z klastrowanego magazynu kolumn przyniosło korzyść (60 dystrybucji * 100 partycji * 1 milion wierszy).  Jeśli tabela w tym przykładzie nie ma 6 miliardów wierszy, zmniejsz liczbę partycji lub rozważ zastąpienie jej tabelą stosu.  Ponadto warto poeksperymentować, aby sprawdzić, czy lepszą wydajność można uzyskać, korzystając z tabeli stosu z indeksami pomocniczymi zamiast z tabeli magazynu kolumn.

Podczas wykonywania zapytania odnoszącego się do tabeli magazynu kolumn kwerendy będą uruchamiane szybciej, jeśli wybrane zostaną tylko niezbędne kolumny.  

Zobacz także artykuły [Indeksy tabel][Table indexes], [Przewodnik po indeksach magazynu kolumn][Columnstore indexes guide] i [Ponowne tworzenie indeksów magazynu kolumn][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-to-improve-query-performance"></a>Użycie większej klasy zasobów w celu poprawy wydajność przesyłania zapytań
Usługa SQL Data Warehouse korzysta z grup zasobów w celu przydzielania pamięci zapytaniom.  Każdemu z użytkowników zostaje natychmiastowo przypisana mała klasa zasobów, w ramach której zostaje przyznane 100 MB pamięci na dystrybucję.  Jako że zawsze jest 60 dystrybucji i każda z nich ma przydzielone co najmniej 100 MB, całkowita alokacji pamięci w systemie wynosi 6000 MB lub nieco poniżej 6 GB.  Stosowanie wybranych kwerend, takich jak duże sprzężenia lub obciążenia odnoszące się do klastrowanych tabel magazynu kolumn, pozwolą korzystać z większych alokacji pamięci.  W przypadku innych kwerend, takich jak czyste skanowanie, korzyść z ich zastosowania będzie niezauważalna.  Z drugiej strony, użycie większych klas zasobów ma wpływ na współbieżność, co należy wziąć pod uwagę przed przeniesieniem wszystkich użytkowników do większej klasy zasobów.

Zobacz także artykuł [Współbieżność i zarządzanie obciążeniami][Concurrency and workload management]

## <a name="use-smaller-resource-class-to-increase-concurrency"></a>Użycie mniejszej klasy zasobów w celu zwiększenia współbieżności
Jeśli wykonywanie kwerend użytkowników wiąże się z dużymi opóźnieniami, być może użytkownicy działają w większych klasach zasobów i wykorzystują dużo gniazd współbieżności, co z kolei powoduje, że inne kwerendy nawarstwiają się, tworząc kolejki.  Uruchom polecenie `SELECT * FROM sys.dm_pdw_waits`, aby to sprawdzić i zobaczyć, czy żadne wiersze nie są zwracane.

Zobacz także artykuł [Współbieżność i zarządzanie obciążeniami][Concurrency and workload management] i [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-to-monitor-and-optimize-your-queries"></a>Korzystanie z widoków DMV do monitorowania i optymalizowania zapytań
Usługa SQL Data Warehouse oferuje kilka widoków DMV, których można używać do monitorowania wykonywanych zapytań.  W poniższym artykule o monitorowaniu podano instrukcje krok po kroku na temat przeglądania szczegółowych informacji dotyczących wykonywanych zapytań.  Aby szybko wyszukać zapytania w tych widokach DMV, z zapytaniami można użyć opcji LABEL.

Zobacz także artykuły [Monitorowanie obciążenia przy użyciu widoków DMV][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Inne zasoby
Zobacz artykuł [Rozwiązywanie problemów][Troubleshooting], w którym omówiono typowe problemy i ich rozwiązania.

Jeśli nie możesz znaleźć tego, czego szukasz, użyj opcji „Wyszukaj dokumenty” po lewej stronie, aby wyszukać wszystkie dokumenty poświęcone usłudze Azure SQL Data Warehouse.  [Forum MSDN usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse MSDN Forum] to miejsce, w którym można zadawać pytania innym użytkownikom oraz zespołowi ds. grupy produktów SQL Data Warehouse.  Firma Microsoft aktywnie monitoruje to forum, aby mieć pewność, że użytkownicy uzyskują odpowiedzi od innych użytkowników lub pracowników firmy Microsoft.  Jeśli wolisz zadać pytanie w witrynie Stack Overflow, możesz także skorzystać z [tego forum usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse Stack Overflow Forum].

Zachęcamy do korzystania ze strony [opinii na temat usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse Feedback] i zgłaszania propozycji dotyczących funkcji.  Dodawanie konkretnych propozycji lub głosowanie na już zgłoszone sugestie bardzo pomaga nam określać priorytety funkcji.

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
[Guide for using PolyBase]: ./guidance-for-loading-data.md
[Load data]: ./design-elt-data-loading.md
[Move data with Azure Data Factory]: ../data-factory/transform-data-using-machine-learning.md
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
[Azure SQL Data Warehouse loading patterns and strategies]: http://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/
