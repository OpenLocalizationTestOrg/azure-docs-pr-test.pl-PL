---
title: aaaWhat jest Azure SQL Data Warehouse? | Microsoft Docs
description: "Rozproszona baza danych klasy korporacyjnej, która może przetwarzać woluminy zawierające petabajty danych relacyjnych i nierelacyjnych. Jest branży hello pierwszy magazyn danych w chmurze Zwiększaj, zmniejszyć i wstrzymywać w sekundach."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Co to jest Azure SQL Data Warehouse?
Azure SQL Data Warehouse to oparta na chmurze i skalowalna w poziomie relacyjna baza danych masowego przetwarzania równoległego (MPP, Massively Parallel Processing), która może przetwarzać ogromne ilości danych. 

SQL Data Warehouse:

* Łączy relacyjnej bazy danych programu SQL Server hello z chmury Azure możliwości skalowania w poziomie. 
* Oddziela magazyn od zasobów obliczeniowych.
* Umożliwia zwiększanie, zmniejszanie, wstrzymywanie i wznawianie procesów obliczeniowych. 
* Integruje się między hello platformy Azure.
* Korzysta z programu SQL Server Transact-SQL (T-SQL) i narzędzi.
* Jest zgodna z różnymi wymaganiami dotyczącymi zabezpieczeń prawnych oraz biznesowych, takich jak SOC i ISO.

W tym artykule opisano najważniejsze funkcje hello usługi SQL Data Warehouse.

## <a name="massively-parallel-processing-architecture"></a>Architektura masowego przetwarzania równoległego
Usługa SQL Data Warehouse to system rozproszonych baz danych o architekturze masowego przetwarzana równoległego (MPP). Tle hello SQL Data Warehouse rozprzestrzenia dane w wielu nieudostępnianych jednostkach magazynowych i jednostkach przetwarzania. Witaj dane są przechowywane w warstwie Premium magazyn lokalnie nadmiarowy u góry, który dynamicznie połączony węzły obliczeniowe wykonywanie zapytań. Ładuje "dzielenia i o" toorunning podejście ma SQL Data Warehouse i złożonych zapytań. Żądania są odbierane przez węzeł kontrolny, zoptymalizowana pod kątem dystrybucji, a następnie przekazywane toodo węzłów tooCompute pracy równolegle.

Dzięki oddzieleniu magazynu od zasobów obliczeniowych usługa SQL Data Warehouse może wykonywać następujące zadania:

* Zwiększać i zmniejszać rozmiar magazynu niezależne od zasobów obliczeniowych.
* Zwiększać i zmniejszać moc obliczeniową bez przenoszenia danych.
* Wstrzymywać moc obliczeniową bez zmieniania danych, płacąc tylko za przestrzeń dyskową.
* Wznawiać moc obliczeniową w godzinach działania.

Witaj Poniższy diagram przedstawia architekturę hello bardziej szczegółowo.

![Architektura usługi SQL Data Warehouse][1]

**Węzeł kontrolny:** węzeł kontrolny hello zarządza i optymalizuje zapytania. Jest hello fronton współdziałający ze wszystkimi aplikacjami i połączeniami. W usłudze SQL Data Warehouse węzeł kontrolny hello jest obsługiwany przez usługę SQL Database i łączenie tooit wyszukuje i tak samo hello. W obszarze powierzchni hello hello węzeł kontrolny koordynuje w wszystkich hello przenoszenie i obliczanie danych wymagane toorun zapytania równoległe względem danych rozproszonych. Podczas przesyłania tooSQL zapytania T-SQL Data Warehouse hello węzeł kontrolny przekształca je w oddzielne zapytania, które są uruchamiane na każdy węzeł obliczeniowy równolegle.

**Węzły obliczeniowe:** węzły obliczeniowe hello służyć jako zasilania hello usługę SQL Data Warehouse. Są one bazami danych SQL, które przechowują dane i przetwarzają zapytania. Po dodaniu danych usługi SQL Data Warehouse dystrybuuje węzły obliczeniowe tooyour wierszy hello. węzły obliczeniowe Hello są hello pracowników, którzy uruchamiania zapytań równoległych hello na podstawie danych. Po zakończeniu przetwarzania przekazują węzeł kontrolny wstecz toohello wyniki hello. zapytania hello toofinish, hello węzeł kontrolny agreguje wyniki hello i zwraca hello wynik końcowy.

**Magazyn:** Dane są przechowywane w usłudze Azure Blob Storage. Gdy węzły obliczeniowe współdziałają z danymi, zapisują i odczytują bezpośrednio tooand z magazynu obiektów blob. Ponieważ Magazyn Azure rozszerza przezroczyste i znacząco, Magazyn danych SQL można wykonać hello takie same. Ponieważ zasoby obliczeniowe i magazyn są niezależne od siebie, usługa SQL Data Warehouse może automatycznie skalować magazyn niezależnie od skalowania zasobów obliczeniowych i na odwrót. Magazynu obiektów Blob platformy Azure jest również całkowicie odporna na uszkodzenia oraz usprawnia hello kopii zapasowej i przywracanie procesu.

**Usługa przenoszenia danych:** usługi przenoszenia danych (DMS) przenosi dane między węzłami hello. Usługa DMS umożliwia toodata dostępu węzły obliczeniowe hello, które są im niezbędne do sprzęgania i agregacji. Usługa DMS nie jest usługą platformy Azure. Jest to usługa systemu Windows uruchamiana razem z usługą SQL Database na wszystkich węzłach hello. Usługa DMS to proces działający w tle, z którym nie jest możliwa bezpośrednia interakcja. Jednak można przyjrzeć się zapytania plany toosee gdy występują one operacje DMS, gdyż przenoszenie danych jest konieczne toorun każdego zapytania równolegle.

## <a name="optimized-for-data-warehouse-workloads"></a>Optymalizacja pod kątem obciążeń magazynu danych
Hello rozwiązanie MPP jest wspomagane przez kilka magazynowania optymalizacji wydajności zależnych, w tym danych:

* Optymalizator zapytań rozproszonych i zestaw złożonych statystyk obejmujących wszystkie dane. Przy użyciu informacji dotyczących rozmiaru i dystrybucji danych, usługa hello jest stanie toooptimize zapytania przez ocenę kosztów określonych operacji zapytań rozproszonych hello.
* Zaawansowane algorytmy i techniki zintegrowane danych hello przepływu procesu tooefficiently przenosi dane między zasobami obliczeniowymi niezbędne tooperform hello kwerendy. Te operacje przenoszenia danych są wbudowane, a wszystkie toohello optymalizacje usługi przenoszenia danych następują automatycznie.
* Domyślnie klastrowane indeksy **magazynu kolumn**. Za pomocą magazynu kolumn, Magazyn danych SQL pobiera średnio 5 x większe wzmocnienie kompresji w tradycyjnym zorientowanym magazynu i zapasowej too10x lub więcej większe wzmocnienie wydajności zapytań. Zapytania analityczne, które wymagają tooscan dużą liczbę wierszy lepiej współpracuje z indeksów magazynu kolumn.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Przewidywalna i skalowalna wydajność dzięki jednostkom magazynu danych
W usłudze SQL Data Warehouse są wykorzystywane podobne technologie co w usłudze SQL Database, dzięki czemu użytkownicy mogą oczekiwać spójnej i przewidywalnej wydajności zapytań analitycznych. Użytkownicy spodziewać skalowania wydajności toosee liniowo dodawania lub odejmowania węzłów obliczeniowych. Alokacja zasobów tooyour SQL Data Warehouse jest mierzony w jednostki magazynu danych (dwu). Jednostki dwu są miary źródłowej zasobów, takich jak Procesora, pamięci, IOPS, które są przydzielane tooyour SQL Data Warehouse. Witaj liczby jednostek dwu zwiększeniu zasobów i wydajności. Jednostki DWU pozwalają w szczególności zagwarantować, że:

* Jesteś tooscale stanie magazynu danych, nie martwiąc się o hello używanego sprzętu lub oprogramowania.
* Można przewidzieć zwiększenie wydajności dla poziomu wartości DWU przed zmianą hello obliczeniowe magazynu danych.
* Witaj odpowiedni sprzęt i oprogramowanie wystąpienia można zmienić lub przenieść bez wpływu na wydajność obciążenia.
* Microsoft może poprawić hello podstawowej architektury usługi hello bez wpływu na wydajność hello obciążenia.
* Microsoft można szybko poprawia wydajność magazynu danych SQL, w taki sposób, który jest skalowalny i równomiernie efekty hello systemu.

Jednostki magazynu danych udostępniają trzy metryki, które są ściśle powiązane z wydajnością przetwarzania obciążenia wynikającego z magazynowania danych. następujące Hello klucza obciążenia metryki skalowania liniowo z jednostkami dwu hello.

**Skanowanie/agregacja:** standardowe zapytanie magazynowania danych, które skanuje dużą liczbę wierszy, a następnie wykonuje złożoną agregację. Jest to operacja intensywnie korzystająca z operacji we/wy i procesora CPU.

**Obciążenia:** hello możliwości tooingest danych do usługi hello. Obciążenia są obsługiwane z największą wydajnością za pomocą programu PolyBase z obiektów blob usługi Azure Storage lub z usługi Azure Data Lake. Ta metryka jest zaprojektowana toostress sieci i procesora CPU aspektów hello usługi.

**Utwórz tabelę jako Select (CTAS):** mierzy hello możliwości toocopy tabeli. Obejmuje to odczytywanie danych z magazynu, dystrybucję w węzłach hello hello urządzenia i zapisywanie toostorage ponownie. Jest to operacja intensywnie korzystająca z procesora CPU, we/wy i sieci.

## <a name="built-on-sql-server"></a>Oparta na programie SQL Server
Usługa SQL Data Warehouse jest oparta na aparacie relacyjnej bazy danych programu SQL Server hello i zawiera wiele funkcji hello, których można się spodziewać po magazynie danych przedsiębiorstwa. Jeśli znasz już T-SQL, jest łatwe tootransfer Twojego tooSQL wiedzy hurtowni danych. Określa, czy jesteś użytkownikiem zaawansowanym, czy dopiero zaczynasz, przykłady hello między hello dokumentacji ułatwią rozpoczęcie pracy. Ogólnie należy zwrócić uwagę sposób hello, w jaki tworzymy elementy językowe hello SQL Data Warehouse w następujący sposób:

* Usługa SQL Data Warehouse używa składni języka T-SQL do wykonywania wielu operacji. Obsługuje także szeroką gamę tradycyjnych struktur SQL, takich jak procedury składowane, funkcje zdefiniowane przez użytkownika, partycjonowanie tabel, indeksy i sortowanie.
* Usługa SQL Data Warehouse zawiera także różne nowsze funkcje programu SQL Server, takie jak klastrowane indeksy **magazynu kolumn**, integracja programu PolyBase oraz inspekcja danych (wraz z oceną zagrożenia).
* Niektóre elementy języka T-SQL, które są mniej typowe dla obciążeń magazynowania danych, lub nowszej tooSQL serwera, nie może być aktualnie dostępna. Aby uzyskać więcej informacji, zobacz hello [dokumentacja dotycząca migracji][Migration documentation].

Hello języka Transact-SQL i współdzielone funkcji programu SQL Server, SQL Data Warehouse, bazy danych SQL i Analytics Platform System można opracować rozwiązanie, które odpowiada potrzebom użytkownika danych. Można zdecydować, gdzie tookeep danych, na podstawie wydajności, zabezpieczeń i wymagań skali, a następnie transfer danych w razie potrzeby między różnymi systemami.

## <a name="data-protection"></a>Ochrona danych
Usługa SQL Data Warehouse przechowuje wszystkie dane w lokalnie nadmiarowym magazynie platformy Azure w warstwie Premium. Wiele synchronicznych kopii danych hello są obsługiwane w hello dane lokalne centrum tooguarantee przezroczystą ochronę danych przed zlokalizowanych awarii. Ponadto usługa SQL Data Warehouse automatycznie tworzy kopie zapasowe aktywnych (niewstrzymanych) baz danych w regularnych odstępach czasu przy użyciu programu Azure Storage Snapshots. toolearn więcej informacji na temat kopii zapasowej i przywracanie działa, zobacz hello [Omówienie kopii zapasowych i przywracania][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Integracja z narzędziami firmy Microsoft
Usługi SQL Data Warehouse integruje się również wiele narzędzi hello program SQL Server użytkownicy mogą znać. Do tych narzędzi należą:

**Tradycyjne narzędzia programu SQL Server:** Usługa SQL Data Warehouse jest w pełni zintegrowana z usługami SQL Server Analysis Services, Integration Services i Reporting Services.

**Narzędzia oparte na chmurze:** Usługę SQL Data Warehouse można zintegrować z różnymi usługami na platformie Azure, takimi jak Data Factory, Stream Analytics, Machine Learning oraz z usługą Power BI. Bardziej kompletny wykaz znajdziesz w artykule [Integrated tools overview][Integrated tools overview] (Przegląd zintegrowanych narzędzi).

**Narzędzia innych firm:** Wiele innych firm dostarczających narzędzia ma certyfikat integracji swoich narzędzi z usługą SQL Data Warehouse. Pełną listę znajdziesz w artykule [SQL Data Warehouse solution partners][SQL Data Warehouse solution partners] (Partnerzy rozwiązania SQL Data Warehouse).

## <a name="hybrid-data-sources-scenarios"></a>Hybrydowe scenariusze źródeł danych
Program Polybase pozwala tooleverage danych z różnych źródeł przy użyciu znanych poleceń T-SQL. Program Polybase pozwala tooquery danych nierelacyjnych przechowywanych w magazynie obiektów Blob platformy Azure, traktując go jak zwykłą tabelę. Użyj programu Polybase tooquery danych nierelacyjnych lub tooimport danych nierelacyjnych do usługi SQL Data Warehouse.

* Program PolyBase używa tabel zewnętrznych tooaccess nierelacyjnymi danymi. definicje tabel Hello są przechowywane w usłudze SQL Data Warehouse i będą dostępne przy użyciu języka SQL i narzędzi, takich jak użytkownik będzie dostęp do zwykłych danych relacyjnych.
* Program PolyBase jest niewymagający pod względem integracji. Go ujawnia hello te same funkcje i funkcjonalność tooall hello obsługiwanego źródła. dane Hello odczytywane w programie Polybase mogą być w różnych formatach plików rozdzielanych lub plików ORC.
* Program PolyBase mogą być używane tooaccess magazynu obiektów blob, który jest również używany jako magazyn dla klastra usługi HDInsight. Dzięki temu dostęp toohello samych danych za pomocą narzędzi relacyjnych i nierelacyjnych.

## <a name="sla"></a>Umowa SLA
Usługa SQL Data Warehouse oferuje na poziomie produktu umowę dotyczącą poziomu usług (SLA) w ramach umowy SLA usług Microsoft Online Services. Aby uzyskać więcej informacji, zobacz [SLA for SQL Data Warehouse][SLA for SQL Data Warehouse] (Usługa SQL Data Warehouse — umowa SLA). Umowa SLA informacji o innych produktach mogą odwiedzać hello [umowy dotyczące poziomu usług] Azure strony lub pobrać je na powitania [licencjonowania zbiorowego] [ Volume Licensing] strony. 

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz nieco SQL Data Warehouse, Dowiedz się jak tooquickly [Tworzenie usługi SQL Data Warehouse] [ create a SQL Data Warehouse] i [załadować przykładowe dane][load sample data]. W przypadku nowych tooAzure może się okazać hello [Azure słownik] [ Azure glossary] przydatne jako wystąpią terminologii nowe. Możesz też zwrócić uwagę na inne zasoby dotyczące usługi SQL Data Warehouse.  

* [Historie sukcesu klientów]
* [Blogi]
* [Żądania funkcji]
* [Filmy wideo]
* [Blogi zespołu doradczego klientów]
* [Tworzenie biletu pomocy technicznej]
* [Forum MSDN]
* [Forum Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Tworzenie biletu pomocy technicznej]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Historie sukcesu klientów]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogi]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogi zespołu doradczego klientów]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Żądania funkcji]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Forum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Filmy wideo]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[umowy dotyczące poziomu usług]: https://azure.microsoft.com/en-us/support/legal/sla/
