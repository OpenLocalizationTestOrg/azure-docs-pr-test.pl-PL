---
title: "Omówienie zapytania elastycznej bazy danych SQL aaaAzure | Dokumentacja firmy Microsoft"
description: "Omówienie funkcji elastycznej zapytania hello"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Omówienie usługi Azure zapytania elastycznej bazy danych SQL (wersja zapoznawcza)
Hello funkcji elastycznej zapytania (w wersji zapoznawczej) umożliwia toorun zapytania języka Transact-SQL, obejmującej wiele baz danych w bazie danych SQL Azure. Pozwala ona tooperform zapytań bazy danych między tooaccess zdalnych tabel i tooquery narzędzia (programu Excel, usługa Power BI, Tableau itp.) firmy Microsoft i innych firm tooconnect między warstwami danych z wielu baz danych. Za pomocą tej funkcji, można skalować w poziomie warstwy danych toolarge kwerendy w bazie danych SQL i wizualizacja wyników hello business intelligence (BI) raportów.


## <a name="why-use-elastic-queries"></a>Dlaczego warto używać elastycznej zapytania?

**Azure SQL Database**

Zapytanie dla baz danych Azure SQL całkowicie w T-SQL. Dzięki temu tylko do odczytu wysyłania zapytań do zdalnej bazy danych. Zapewnia to opcja dla bieżącej lokalnej aplikacji toomigrate klientów programu SQL Server przy użyciu trzech i czterech niepełnym nazw lub tooSQL połączonego serwera bazy danych.

**Dostępne w warstwie standardowa**

Elastyczne zapytania jest obsługiwana w warstwie standardowa wydajności hello w warstwę wydajności Premium toohello dodanie. Zobacz sekcję hello na ograniczenia wersji zapoznawczej poniżej na ograniczeń wydajności niższe poziomy wydajności.

**Wypychanie tooremote baz danych**

Elastyczne zapytania można teraz push parametry toohello zdalnej bazy danych SQL do wykonania.

**Wykonywanie procedury składowanej**

Wykonywanie wywołań zdalnej procedury składowanej lub funkcji zdalnego przy użyciu [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714).

**Elastyczność**

Tabele zewnętrzne z zapytaniem elastycznej teraz mogą odwoływać się tooremote tabel z innym schematem lub nazwę tabeli.

## <a name="elastic-query-scenarios"></a>Scenariusze elastycznej zapytania

Celem Hello jest toofacilitate zapytań scenariuszy, w którym wielu baz danych współtworzenia wierszy w jeden wynik ogólny. Zapytanie Hello może albo składać się przez użytkownika hello lub aplikacji bezpośrednio lub pośrednio za pomocą narzędzia, które są połączone toohello bazy danych. Jest to szczególnie przydatne podczas tworzenia raportów, za pomocą narzędzia integracji komercyjnego BI lub dane — lub dowolnej aplikacji, nie można jej zmienić. Zapytania o elastyczne umożliwia wysyłanie zapytań przez wiele baz danych, za pomocą hello znane rozwiązanie łączności serwera SQL w narzędzi, takich jak program Excel, usługa Power BI, Tableau lub Cognos.
Elastyczne zapytanie umożliwia łatwy dostęp tooan całą kolekcję baz danych za pomocą zapytań wystawiony przez program SQL Server Management Studio lub Visual Studio i ułatwia badanie między bazami danych z programu Entity Framework lub innych środowisk ORM. Rysunek 1 pokazuje scenariusz, w którym istniejące chmury aplikacji (hello, który używa [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)) warstwy oparte na danych skalowalnych w poziomie i elastyczny zapytania jest używana do raportowania między bazami danych.

**Rysunek 1** elastycznej Zapytanie używane w warstwie danych skalowalnych w poziomie

![Elastyczne Zapytanie używane w warstwie danych skalowalnych w poziomie][1]

Scenariusze klienta dla elastycznej zapytania charakteryzują się hello następujących topologii:

* **Partycjonowanie pionowe - zapytań bazy danych między** (topologia 1): hello danych jest podzielona na partycje w pionie między wiele baz danych w warstwie danych. Zazwyczaj różne zestawy tabel znajdują się na różnych baz danych. Oznacza to, że schemat hello różni się w różnych baz danych. Na przykład wszystkie tabele spisu są na jedną bazę danych, gdy wszystkie tabele powiązane ewidencjonowania aktywności znajdują się w drugiej bazy danych. Typowe przypadki użycia z tą topologią wymagają jednego tooquery między lub raporty toocompile między tabelami w kilku baz danych.
* **Partycjonowanie poziome - dzielenia na fragmenty** (topologia 2): danych jest podzielona na partycje w poziomie warstwy wierszy toodistribute przez skalowany danych. Z tej metody schemat hello jest takie same na wszystkich uczestniczących baz danych. Takie podejście jest również nazywany "dzielenia na fragmenty". Dzielenia na fragmenty mogą być wykonywane i zarządzane przy użyciu bibliotek narzędzi elastycznej bazy danych (1) hello lub (2) samoobsługowego-dzielenia na fragmenty. Elastyczne zapytanie jest używane raporty tooquery lub kompilacji w wielu fragmentów.

> [!NOTE]
> Elastyczne zapytania najlepiej pasuje do okazjonalne scenariuszy raportowania, gdzie można wykonać większość przetwarzania hello na powitania warstwy danych. Obciążenia wymagające raportowania lub magazynowania scenariuszy z bardziej złożonych kwerend danych, również należy rozważyć użycie [magazyn danych SQL Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Partycjonowanie pionowe - między bazami danych zapytań

toobegin kodowania, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).

Elastycznej zapytania mogą być używane toomake danych znajdujących się w bazy danych SQL tooother dostępne bazy danych SQL. Dzięki temu zapytania z jednej bazy danych toorefer tootables żadnych innych zdalnej bazy danych SQL. pierwszym krokiem Hello jest toodefine zewnętrznego źródła danych dla każdej zdalnej bazy danych. Witaj zewnętrzne źródło danych jest zdefiniowany w lokalnej bazie danych hello z którego mają zostać tootables dostępu toogain znajdujących się na powitania zdalnej bazy danych. Żadne zmiany nie jest niezbędna w hello zdalnej bazy danych. Dla typowy pionowy partycjonowania scenariusz, w której różnych baz danych mają różne schematów elastyczne zapytania można tooimplement używane typowe przypadki użycia, takich jak dane tooreference dostępu i między bazami danych zapytań.

> [!IMPORTANT]
> Musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych. To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE. Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.
>

**Danych referencyjnych**: topologii hello jest używany w celu zarządzania danymi odwołania. W poniższym rysunku hello dwie tabele (T1 a T2) w przypadku danych referencyjnych są przechowywane na dedykowany bazy danych. Przy użyciu elastycznej kwerendy, teraz są dostępne tabele T1 a T2 zdalnie innych baz danych, jak pokazano na rysunku hello. Użyj topologii 1 w przypadku tabel odwołań małych lub zdalnego zapytań do tabeli referencyjnej ma selektywnego predykatów.

**Rysunek 2** partycjonowanie pionowe — przy użyciu danych referencyjnych tooquery elastycznej zapytania

![Partycjonowanie pionowe — przy użyciu danych referencyjnych tooquery elastycznej zapytania][3]

**Zapytanie bazy danych między**: elastyczna odpytuje przypadki użycia Włącz wymagających wykonywanie zapytań w kilku baz danych. Rysunek 3 przedstawia czterech różnych baz danych: CRM, spisu i HR produktów. Zapytania wykonywane w jednej z baz danych hello również muszą mieć dostęp do tooone lub hello wszystkich innych baz danych. Przy użyciu elastycznej kwerendy, można skonfigurować bazy danych dla tego przypadku uruchamiając kilka prostych instrukcji DDL w każdym hello cztery bazy danych. Po tym jednorazowej konfiguracji tabeli zdalnej tooa dostępu jest tak proste, jak przywołuje tooa lokalnej tabeli z zapytania T-SQL lub narzędzi do analizy Biznesowej. Takie podejście jest zalecane, jeśli hello zapytań zdalnych nie zwracają dużych wyników.

**Rysunek 3** partycjonowanie pionowe — przy użyciu elastycznej zapytania tooquery między różnymi bazami danych

![Partycjonowanie pionowe — przy użyciu elastycznej zapytania tooquery między różnymi bazami danych][4]

Hello następujące kroki konfigurowania zapytania elastycznej bazy danych dla pionowego partycjonowania scenariuszy, które wymagają dostępu do tabeli tooa znajduje się na zdalnej bazy danych SQL z hello sam schemat:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [Utwórz i UPUŚĆ zewnętrzne źródło danych](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource typu **RDBMS**
* [Utwórz i UPUŚĆ tabeli zewnętrznej](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Po uruchomieniu instrukcji DDL hello, tak, jakby była lokalnej tabeli można uzyskać dostępu do tabeli zdalnej hello "mytable". Baza danych SQL Azure automatycznie otwiera połączenia toohello zdalnej bazy danych, przetwarza żądania na powitania zdalnej bazy danych i zwraca wyniki hello.

## <a name="horizontal-partitioning---sharding"></a>Poziomy partycjonowania - dzielenia na fragmenty
Przy użyciu elastycznej zapytania tooperform zadania raportowania za pośrednictwem podzielonej, tj., poziomo podzielona na partycje, wymaga warstwy danych [mapy niezależnego fragmentu elastycznej bazy danych](sql-database-elastic-scale-shard-map-management.md) baz danych hello toorepresent hello warstwy danych. Zazwyczaj mapy jednego niezależnego fragmentu jest używany w tym scenariuszu, a dedykowany bazy danych z zapytania elastyczne możliwości (węzła głównego) służy jako punkt wejścia hello raportowania zapytań. Tylko ten dedykowany bazy danych musi Mapa niezależnego fragmentu toohello dostępu. Rysunek 4 przedstawia tej topologii i jego konfiguracja z hello zapytania elastycznej bazy danych i niezależnych mapy. bazy danych Hello w warstwie danych hello może mieć wersji lub wersji bazy danych SQL Azure. Aby uzyskać więcej informacji na temat biblioteki klienta elastycznej bazy danych hello i tworzenie map niezależnego fragmentu, zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).

**Rysunek 4** poziome partycjonowania — przy użyciu elastycznej zapytania dla raportowania za pośrednictwem warstw podzielonej danych

![Poziomy partycjonowania — przy użyciu elastycznej zapytania dla raportowania za pośrednictwem warstw podzielonej danych][5]

> [!NOTE]
> Elastyczne zapytanie do bazy danych (węzła głównego) może być oddzielnej bazy danych lub może być hello sama baza danych tej mapy niezależnego fragmentu hello hostów. Upewnij się, że niezależnie od konfiguracji, możesz wybrać tej warstwy usług i wydajności tej bazy danych jest wystarczająco duża toohandle hello oczekiwana ilość żądań logowania/zapytań.

Hello poniższe kroki należy skonfigurować elastycznej bazy danych zapytań dotyczących poziome partycjonowania scenariusze, które wymagają dostępu do zestawu tooa tabeli znajdujące się na (zwykle) kilka zdalnej bazy danych SQL:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* Utwórz [mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) reprezentujące warstwę danych przy użyciu biblioteki klienta elastycznej bazy danych hello.   
* [Utwórz i UPUŚĆ zewnętrzne źródło danych](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource typu **SHARD_MAP_MANAGER**
* [Utwórz i UPUŚĆ tabeli zewnętrznej](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Po wykonaniu tych czynności możesz uzyskać dostęp hello poziomie partycjonowanej tabeli "mytable" tak, jakby była lokalnej tabeli. Baza danych SQL Azure automatycznie otwiera wielu równoległych połączeń toohello zdalnymi bazami danych fizycznie przechowywania hello tabel, przetwarza żądania hello na powitania zdalnych baz danych i zwraca wyniki hello.
Więcej informacji na temat kroków hello wymagane dla hello poziome partycjonowania scenariusza można znaleźć w [elastycznej zapytania poziome partycjonowania](sql-database-elastic-query-horizontal-partitioning.md).

toobegin kodowania, zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>Wykonywanie zapytania T-SQL
Po zdefiniowaniu z zewnętrznych źródeł danych i tabel zewnętrznych można użyć regularne połączenia ciągów tooconnect toohello baz danych serwera SQL gdzie są zdefiniowane z tabel zewnętrznych. Następnie możesz uruchomić instrukcje T-SQL w tabelach zewnętrznych dla tego połączenia z ograniczeniami hello opisane poniżej. Dodatkowe informacje i przykłady zapytania T-SQL można znaleźć w tematach dokumentacji hello dla [poziomych partycji](sql-database-elastic-query-horizontal-partitioning.md) i [partycjonowanie pionowe](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Połączenie narzędzi
Regularne tooconnect ciągów połączenia programu SQL Server można użyć aplikacji i danych lub BI toodatabases narzędzi integracji, mające tabel zewnętrznych. Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi. Po nawiązaniu połączenia można znaleźć toohello zapytania elastycznej bazy danych i hello tabel zewnętrznych w tej bazie danych, tak samo, jak należy z przykładowej bazy danych programu SQL Server połączyć toowith własnych narzędzi.

> [!IMPORTANT]
> Uwierzytelnianie przy użyciu usługi Azure Active Directory z zapytaniami elastyczne nie jest obecnie obsługiwane.
> 
> 

## <a name="cost"></a>Koszty
Elastyczne zapytania jest uwzględniony w koszt hello baz danych, baza danych SQL Azure. Należy pamiętać, że są obsługiwane topologie, gdzie zdalnej bazy danych znajdują się w centrum danych niż hello elastycznej zapytania punktu końcowego, ale wyjście danych ze zdalnych baz danych są naliczane regular [Azure stawki](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Ograniczenia wersji zapoznawczej
* Uruchamianie pierwszej kwerendy elastycznej może potrwać nawet tooa kilka minut w warstwie standardowa wydajności hello. Ten czas jest niezbędne tooload hello elastycznej zapytania funkcjonalności. Ładowanie wydajności poprawia z warstwy wyższej wydajności.
* Obsługa skryptów z zewnętrznych źródeł danych lub tabel zewnętrznych z SSMS lub program SSDT nie jest jeszcze obsługiwana.
* Narzędzie importu/eksportu dla bazy danych serwera SQL nie obsługuje jeszcze zewnętrznych źródeł danych i tabel zewnętrznych. Toouse importu/eksportu, należy usunąć przed wyeksportowaniem te obiekty, a następnie ponownie utwórz je po zaimportowaniu.
* Elastyczne zapytania aktualnie obsługuje tylko tabele tooexternal dostęp tylko do odczytu. Jednak można używać pełnej funkcjonalności T-SQL w bazie danych hello której zdefiniowano hello tabeli zewnętrznej. Może to być przydatne do, np. utrwalenia tymczasowych wyników za pomocą, np. Wybierz < column_list > w < local_table > lub toodefine procedur składowanych na powitania elastycznej zapytanie do bazy danych, który można znaleźć tooexternal tabel.
* Z wyjątkiem nvarchar(max) typy obiektów LOB nie są obsługiwane w definicji tabeli zewnętrznej. Jako obejście można utworzyć widoku na powitania zdalnej bazy danych, który rzutuje typu LOB hello do nvarchar(max), zdefiniuj tabeli zewnętrznej za pośrednictwem widoku hello zamiast hello tabeli podstawowej i rzutować go wrócić do oryginalnego typu LOB hello zapytania.
* Kolumna statystyki dotyczące tabel zewnętrznych nie są obecnie obsługiwane. Tabele statystyki są obsługiwane, ale należy toobe utworzone ręcznie.

## <a name="feedback"></a>Opinia
Udostępnij opinii na temat korzystania z zapytaniami elastycznej z nami Disqus poniżej, fora MSDN hello, lub w witrynie Stackoverflow. Firma Microsoft interesuje wszelkiego rodzaju opinię na temat usługi hello (wady, niedociągnięcia luki funkcji).

## <a name="next-steps"></a>Następne kroki

* Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).
* Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)
* Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).
* Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)
* Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
