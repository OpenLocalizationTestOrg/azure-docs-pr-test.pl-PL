---
title: "tabele aaaDistributing w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do korzystania z dystrybucji tabel w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Dystrybucja tabel w usłudze SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Typy danych][Data Types]
> * [Dystrybuuj][Distribute]
> * [Indeks][Index]
> * [Partycji][Partition]
> * [Statystyki][Statistics]
> * [Tymczasowe][Temporary]
>
>

Usługa SQL Data Warehouse to system rozproszonych baz danych o architekturze masowego przetwarzana równoległego (MPP).  Dzieląc dane i możliwości przetwarzania między wiele węzłów, usługa SQL Data Warehouse może zaoferować bardzo dużą skalowalność — znacznie większą niż w przypadku jakiegokolwiek pojedynczego systemu.  Przy wyborze sposobu toodistribute danych w magazynie danych SQL jest jedną z najważniejszych hello czynniki tooachieving optymalną wydajność.   wydajności klucza toooptimal Hello jest minimalizowania przenoszenia danych i z kolei przenoszenia danych klucza toominimizing hello jest wybranie hello strategii prawa dystrybucji.

## <a name="understanding-data-movement"></a>Opis przenoszenia danych
W systemie MPP hello danych z każdej tabeli jest dzielona między kilka podstawowej bazy danych.  Witaj najbardziej zoptymalizowanych pod kątem zapytań w systemie MPP po prostu mogą zostać przekazane za pośrednictwem tooexecute na powitania pojedyncze rozproszonej bazy danych bez interakcji między hello innych baz danych.  Załóżmy na przykład, że masz bazę danych danymi sprzedaży zawiera dwie tabele, sprzedaży i klientów.  Jeśli masz kwerendę, która wymaga toojoin tabeli klienta tooyour tabeli sprzedaży i dzielenia sprzedaży i tabele klienta się przez numer klienta umieszczanie każdego klienta w oddzielnej bazy danych, w ramach każdej można rozwiązać żadnych zapytań, które przyłączyć sprzedaży i klienta bazy danych z żadnej znajomości hello innych baz danych.  Z kolei danych sprzedaży rozdzielonych numer zamówienia i danych klienta przez numer klienta, następnie wszystkie danego bazy danych nie będzie zawierał hello odpowiednich danych dla każdego klienta, dlatego jeśli chce toojoin danych klienta tooyour danych sprzedaży, będzie potrzebny tooget hello danych dla każdego klienta z hello innych baz danych.  W drugim przykładzie przenoszenia danych musi toooccur toomove powitania klienta toohello sprzedaży danych, tak, aby Witaj dwie tabele mogą zostać sprzężone.  

Przenoszenie danych zawsze jest zły element, czasami jest konieczne toosolve zapytania.  Jednak podczas tego dodatkowego kroku można uniknąć, naturalny zapytanie będzie szybsze.  Przenoszenie danych powstaje najczęściej, gdy są połączone tabele lub agregacji są wykonywane.  Często konieczne toodo obu, gdy być może toooptimize jednym ze scenariuszy, takich jak sprzężenia, możesz nadal wymaga toohelp przepływu danych, które rozwiązywać dla hello innej sytuacji, takich jak agregacji.  Lewa Hello jest ustaleniem, czyli mniej pracy.  W większości przypadków dystrybucja tabele faktów dużych często dołączonego do kolumny jest hello najbardziej efektywną metodę zmniejszenie hello większości przenoszenia danych.  Dystrybucja danych na kolumn sprzężenia jest znacznie bardziej popularne przenoszenia danych tooreduce metody na niż dystrybucji danych kolumn uczestniczących w agregacji.

## <a name="select-distribution-method"></a>Wybieranie metody dystrybucji
Usługi SQL Data Warehouse tle hello dzieli dane 60 baz danych.  Każdej poszczególne bazy danych jest określony tooas **dystrybucji**.  Podczas ładowania danych w każdej tabeli, Magazyn danych SQL ma tooknow jak toodivide danych przez tych 60 dystrybucji.  

Metoda dystrybucji Hello jest zdefiniowana na poziomie tabeli hello i obecnie dostępne są dwie możliwości:

1. **Działanie okrężne** który równomiernie, ale losowo dystrybucji danych.
2. **Skrótów rozproszone** która dystrybuuje oparte na tworzenie skrótów wartości z jednej kolumny danych

Domyślnie, gdy metoda dystrybucji danych, nie zostaną zdefiniowane tabeli będą dystrybuowane za pomocą hello **działanie okrężne** metoda dystrybucji.  Jednak ponieważ staje się bardziej złożone w implementacji, można za pomocą tooconsider **rozpowszechniane skrót** tabele toominimize przenoszenia danych, który będzie z kolei optymalizacji wydajności zapytania.

### <a name="round-robin-tables"></a>Działanie okrężne tabel
Przy użyciu hello okrężnego metoda dystrybucji danych jest znacznie, jak ich wymowy.  Jak Twoje dane są ładowane, każdy wiersz po prostu są wysyłane toohello dystrybucji dalej.  Ta metoda dystrybucji hello danych będzie zawsze losowo równomierne danych hello bardzo we wszystkich hello dystrybucji.  Oznacza to, że istnieje sortowania nie gotowe podczas hello round działania okrężnego procesu, który umieszcza dane.  Działanie okrężne dystrybucji jest niekiedy nazywany losowego wyznaczania wartości skrótu z tego powodu.  Z tabelą rozproszonej okrężnego nie ma żadnych danych hello toounderstand potrzeby.  Z tego powodu tabel okrężnego należy często dobrym ładowanie obiektów docelowych.

Domyślnie, jeśli wybrano opcję Brak metody dystrybucji, hello okrężnego dystrybucji zostanie użyta metoda.  Jednak działanie okrężne tabele są łatwe toouse, ponieważ danych jest rozłożona losowo systemu hello, oznacza to, że hello system nie może zagwarantować, które dystrybucji każdy wiersz jest na.  Wynik, czasami systemu hello potrzeb tooinvoke toobetter operacji przenoszenia danych organizowania danych przed może rozpoznać zapytania.  Ten krok dodatkowe może to spowolnić zapytań.

Rozważ użycie dystrybucji okrężnego dla tej tabeli w hello następujące scenariusze:

* Gdy wprowadzenie jako punktu wyjścia proste
* Jeśli oczywiste łącząca klucz nie istnieje
* Jeśli nie ma kolumny odpowiednimi kandydatami do wyznaczania wartości skrótu dystrybucji hello tabeli
* Jeśli hello tabeli nie udostępnia wspólny klucz sprzężenia z innych tabel
* Jeśli sprzężenia hello jest mniej istotna niż inne sprzężeń w zapytaniu hello
* Gdy tabeli hello jest tymczasowy tabeli przemieszczania

Oba te przykłady spowoduje utworzenie tabeli działanie okrężne:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Gdy jest działanie okrężne typem tabeli domyślnym hello jest jawne w kod DDL jest uważany za najlepszym rozwiązaniem, wyczyść tooothers aby zamiarach hello układu tabeli.
>
>

### <a name="hash-distributed-tables"></a>Rozproszone tabele hash
Przy użyciu **rozpowszechniane skrót** toodistribute algorytm tabel może poprawić wydajność w różnych scenariuszach ograniczając przenoszenie danych w czasie zapytania.  Tabele rozproszone są tabele, które są dzielone między hello skrótu rozproszonych baz danych przy użyciu algorytmu wyznaczania wartości skrótu w jednej kolumnie, która zostanie wybrana.  Kolumna dystrybucji Hello jest, co określa, jak dane hello jest dzielona między rozproszonych baz danych.  Funkcja wyznaczania wartości skrótu Hello używa hello dystrybucji kolumny tooassign wierszy toodistributions.  Witaj algorytmu wyznaczania wartości skrótu i wynikowy dystrybucji jest deterministyczna.  Oznacza to hello toohello ma tę samą wartość z tego samego typu danych będzie zawsze hello tego samego dystrybucji.    

W tym przykładzie utworzy rozproszone na identyfikator tabeli:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Wybierz kolumnę dystrybucji
Jeśli zdecydujesz się zbyt**skrótu dystrybucji** tabeli, konieczne będzie tooselect dystrybucji jednej kolumny.  Podczas wybierania kolumn dystrybucji, istnieją trzy główne czynniki tooconsider.  

Wybrać pojedynczą kolumnę, która będzie:

1. Nie można zaktualizować
2. Równomierne danych, unikając pochylenia danych
3. Minimalizowanie przepływu danych

### <a name="select-distribution-column-which-will-not-be-updated"></a>Wybierz kolumnę dystrybucji, które nie zostaną zaktualizowane
Kolumny dystrybucji nie są aktualizowalne, w związku z tym, wybierz kolumnę o wartości statyczne.  Jeśli kolumny, należy zaktualizować toobe, zwykle nie jest kandydatem dobrej.  W przypadku przypadek, w którym należy zaktualizować kolumn dystrybucji, można to zrobić przez najpierw usunięcie hello wiersza, a następnie wstawienia nowego wiersza.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Wybierz kolumnę dystrybucji, który będzie równomierne danych
Ponieważ rozproszony system przeprowadza tylko tak szybko, jak jego najwolniejsze dystrybucji, jest ważne toodivide hello pracy równomiernie między dystrybucje hello kolejność wykonywania tooachieve zrównoważonym między hello systemu.  sposób Hello pracy hello jest podzielona na Rozproszony system jest oparty na którym mieszka hello danych dla poszczególnych dystrybucji.  Dzięki temu tooselect bardzo ważne hello dystrybucji prawa kolumna dystrybucji hello danych tak, aby każdy dystrybucji ma taki sam pracy i będzie podjęcia hello tym samym czasie toocomplete część pracy hello.  Podczas pracy dobrze jest dzielona między hello systemu, danych hello jest równoważone między hello dystrybucji.  Gdy dane nie jest rozmieszczana równomiernie, nazywamy to **zegara danych**.  

dane toodivide równomiernie i uniknąć pochylenia danych, należy wziąć pod uwagę następujące powitania po wybraniu kolumny dystrybucji:

1. Wybierz kolumny, która zawiera znaczące liczbę unikatowych wartości.
2. Unikaj dystrybucji danych w kolumnach z kilku odrębnych wartości.
3. Unikaj dystrybucji danych dla kolumn o wysokiej częstotliwości zawiera wartości null.
4. Unikaj dystrybucji danych na kolumny daty.

Ponieważ każda wartość skrótu too1 60 dystrybucji, nawet dystrybucji tooachieve można tooselect kolumny, która jest wysoce unikatowy i zawiera więcej niż 60 unikatowe wartości.  tooillustrate, należy wziąć pod uwagę w przypadku, gdy kolumna zawiera tylko 40 unikatowe wartości.  Jeśli ta kolumna została wybrana jako klucza dystrybucji hello, hello danych dla tej tabeli spowoduje grunt na 40 dystrybucje co najwyżej pozostawienie 20 dystrybucji żadnych danych i nie toodo przetwarzania.  Z drugiej strony hello innych 40 dystrybucji mają więcej toodo pracy, że jeśli hello danych został równomierny dystrybucje ponad 60.  Ten scenariusz jest przykładem danych pochylenia.

W systemie MPP każdego kroku zapytania czeka na wszystkich toocomplete dystrybucje udziału hello pracy.  Jeśli jeden dystrybucji jest więcej pracy niż hello innych użytkowników, a następnie hello zasobów hello innych dystrybucji są zasadniczo niewykorzystana właśnie trwa oczekiwanie na powitania dystrybucji zajęty.  Podczas pracy nie jest równomiernie umieszczonych na wszystkie dystrybucje, nazywamy to **przetwarzania pochylenia**.  Przetwarzanie zegara spowoduje wolniej niż Jeśli hello obciążenie może być równomierny dla wszystkich dystrybucje hello toorun zapytania.  Pochylenie danych doprowadzi tooprocessing pochylenia.

Nie udostępniaj wysokiej wartości Null kolumny jako wartości null hello wszystkie przeniesie na powitania sam dystrybucji. Dystrybucja na kolumnę dat może również spowodować przetwarzania pochylenia ponieważ wszystkie dane dla określonej daty przeniesie na powitania sam dystrybucji. W przypadku kilku użytkowników jest wykonywanie zapytań wszystkie filtrowania na powitania sama data, następnie tylko 1 dystrybucje 60 hello będzie realizacji wszystkich prac powitania od podanej daty będą tylko w jednej dystrybucji. W tym scenariuszu zapytania hello prawdopodobnie zostanie uruchomiony 60 razy mniejsza niż Jeśli hello danych zostały jednakowo rozprzestrzeniać się wszystkie hello dystrybucji.

Jeśli istnieją żadnych kolumn odpowiednimi kandydatami, należy rozważyć hello metoda dystrybucji przy użyciu okrężnego.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Wybierz kolumny dystrybucji, która zostanie zminimalizowane przepływu danych
Minimalizując przenoszenia danych, wybierając kolumnę prawo dystrybucji hello jest jednym z najważniejszych strategii hello optymalizacji wydajności magazynu danych SQL.  Przenoszenie danych powstaje najczęściej, gdy są połączone tabele lub agregacji są wykonywane.  Kolumn używanych w `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` i `HAVING` klauzule wszystkie ułatwiają **dobrej** skrótów kandydatów dystrybucji.

Witaj w drugiej kolumny w hello `WHERE` klauzuli **nie** wprowadzić kandydatów kolumny dobrej skrótu ponieważ ich ograniczenia, które dystrybucje uczestniczyć w zapytaniu hello, co powoduje przetwarzania pochylenia.  Dobrym przykładem kolumny, która może być kuszące toodistribute na, ale często powodują tego pochylenia przetwarzania jest kolumny daty.

Ogólnie rzecz biorąc Jeśli masz dwie tabele faktów dużych często zaangażowane w sprzężeniu, będzie uzyskasz hello większości wydajności przez dystrybucję obu tabel w jednym z hello kolumn sprzężenia.  Jeśli masz tabelę, która nie jest nigdy tooanother dołączonego do tabeli faktów dużych Szukaj toocolumns, które są często stosowane w hello `GROUP BY` klauzuli.

Istnieje kilka klucza kryteriów, które musi być niespełnienia tooavoid przenoszenia danych podczas sprzężenia:

1. Hello tabel, których dotyczy hello sprzężenia musi być rozproszone na skrót **jeden** hello kolumn uczestniczących w hello sprzężenia.
2. typy danych kolumn sprzężenia hello Hello musi odpowiadać między obu tabel.
3. Witaj kolumn muszą być przyłączone z operatorem równości.
4. Witaj typ sprzężenia mogą nie być `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Rozwiązywanie problemów z danych pochylenia
Dane tabeli są przesyłane przy użyciu metody dystrybucji skrótu hello jest ryzyko, że będzie niektórych dystrybucji niesymetryczna toohave nieproporcjonalnie więcej danych niż inne. Pochylenia nadmiernej ilości danych może wpłynąć na wydajność zapytań, ponieważ hello końcowego wyniku zapytania rozproszonego musi czekać na hello najdłuższym uruchomionych dystrybucji toofinish. W zależności od stopnia hello danych hello pochylenia, może być konieczne tooaddress go.

### <a name="identifying-skew"></a>Identyfikowanie zegara
Prosty sposób tooidentify tabelę niesymetryczna jest toouse `DBCC PDW_SHOWSPACEUSED`.  Jest to bardzo szybki i prosty sposób toosee hello liczba wierszy tabeli, które są przechowywane w każdym dystrybucje hello 60 bazy danych.  Należy pamiętać, że wydajności hello najbardziej zrównoważonym hello wierszy w tabeli rozproszonej należy można rozmieszczone równomiernie w obrębie wszystkie dystrybucje hello.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Jednak w przypadku zapytania hello Azure SQL Data Warehouse dynamicznych widoków zarządzania (DMV) można przeprowadzić bardziej szczegółowej analizy.  toostart, Utwórz widok hello [dbo.vTableSizes] [ dbo.vTableSizes] wyświetlić przy użyciu hello SQL z [omówienie tabeli] [ Overview] artykułu.  Po utworzeniu widoku hello Uruchom ten tooidentify zapytania tabel, które mają więcej niż 10% danych zegara.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Rozpoznawanie pochylenia danych
Nie wszystkie pochylenia jest za mało toowarrant poprawkę.  W niektórych przypadkach wydajności hello tabeli niektórych kwerend może przeważają hello uszkodzenie danych pochylenia.  pochylanie toodecide Jeśli danych powinien być rozpoznawany w tabeli, należy się dowiedzieć, jak to możliwe hello woluminów danych i zapytania w obciążenie.   Kroki hello toouse hello jest jednokierunkowej toolook na powitania wpływ zegara [monitorowania zapytania] [ Query Monitoring] artykuł toomonitor hello skutki pochylenia wzdłuż wydajność zapytań, a w szczególności hello wpływ toohow długich zapytań zająć toocomplete hello poszczególnych dystrybucji.

Dystrybucji danych polega na znajdowaniu hello kompromisu między minimalizując zegara danych i minimalizując przenoszenia danych. Te można przeciwne cele i czasem można danych tookeep pochylenia podczas przenoszenia danych tooreduce kolejności. Na przykład gdy kolumna dystrybucji hello jest często hello udostępnionego kolumną sprzęgania i agregacji, można będzie można minimalizację przenoszenia danych. Witaj o konieczności przenoszenia danych minimalnego hello może przeważają wpływ hello pochylanie danych.

Typowym sposobem Hello tooresolve danych zegara wynosi toore — Utwórz hello tabelę z kolumną różnych dystrybucji. Ponieważ nie istnieje sposób toochange hello dystrybucji kolumny w istniejącej tabeli hello sposób toochange hello dystrybucji tabeli go toorecreate za pomocą [] [CTAS].  Poniżej przedstawiono dwa przykłady tego, jak rozpoznać pochylenia danych:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Przykład 1: Ponownie utwórz tabelę hello z nową kolumnę dystrybucji
W tym przykładzie użyto toore [] [CTAS]-tworzy tabelę z kolumną dystrybucji różnych wyznaczania wartości skrótu.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Przykład 2: Ponownie utwórz tabeli hello przy użyciu rozkładu okrężnego
W tym przykładzie użyto toore [] [CTAS]-tworzy tabelę z okrężnego zamiast dystrybucji wyznaczania wartości skrótu. Ta zmiana spowoduje dystrybucji danych nawet kosztem hello przepływu danych.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji o projektowaniu tabel, zobacz hello [dystrybucji][Distribute], [indeksu][Index], [partycji] [ Partition], [Typy danych][Data Types], [statystyki] [ Statistics] i [tabel tymczasowych] [ Temporary] artykułów.

Omówienie najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
