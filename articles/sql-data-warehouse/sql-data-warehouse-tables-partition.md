---
title: "tabele aaaPartitioning w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: Wprowadzenie do partycjonowania tabeli w magazynie danych SQL Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Partycjonowanie tabel w usłudze SQL Data Warehouse
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

Partycjonowanie jest obsługiwana dla wszystkich typów tabeli SQL Data Warehouse; w tym klastrowanego magazynu kolumn, indeks klastrowany i stosu.  Partycjonowanie jest również obsługiwany na wszystkich typach dystrybucji, w tym zarówno skrótu lub działanie okrężne rozproszonych.  Partycjonowanie umożliwia toodivide, które dane na mniejsze grupy danych i w większości przypadków Partycjonowanie jest wykonywana na kolumnę dat.

## <a name="benefits-of-partitioning"></a>Korzyści wynikające z partycjonowania
Partycjonowanie mogą korzystać wydajność obsługi i zapytań danych.  Określa, czy przynosi korzyści zarówno lub jeden z nich jest zależna od jak załadować danych i czy hello tej samej kolumnie może służyć do obu celów, ponieważ Partycjonowanie jest możliwe tylko w jednej kolumnie.

### <a name="benefits-tooloads"></a>Tooloads korzyści
Hello główną zaletą partycjonowania w usłudze SQL Data Warehouse jest zwiększyć wydajność hello i wydajności podczas ładowania danych przy użyciu usunięcia partycji, przełączania i scalanie.  W większości przypadków, w których dane są podzielone na partycje w dniu kolumny, która jest ściśle powiązana sekwencji toohello danych hello jest załadowany toohello bazy danych.  Jedną z największych zalet hello przy użyciu danych toomaintain partycje go hello unikania rejestrowanie transakcji.  Po prostu Wstawianie, aktualizowanie lub usuwanie danych mogą być Najprostszym rozwiązaniem hello z niewielką ilością myśl i nakładu pracy, przy użyciu podziału na partycje podczas procesu obciążenia znacznie może poprawić wydajność.

Przełączanie partycji można używane tooquickly Usuń lub Zamień sekcji tabeli.  Na przykład tabela faktów sprzedaży może zawierać tylko dane dla hello ostatnich miesięcy 36.  Na końcu hello co miesiąc hello miesiąc najstarsze dane są usuwane z tabeli hello.  Można go usunąć te dane przy użyciu danych hello toodelete instrukcji delete dla hello najstarsze miesiąca.  Jednak usunięcie dużych ilości danych wiersz po wierszu z instrukcji delete może zająć bardzo dużo czasu, a także spowodować ryzyko hello duże transakcje przyjmujących toorollback dużo czasu, jeśli jakaś nieprawidłowość.  Więcej optymalne podejście jest toosimply upuszczania hello najstarsze partycji danych.  Gdzie usuwanie wierszy poszczególnych hello może zająć godziny, usunięcie całego partycji może potrwać sekund.

### <a name="benefits-tooqueries"></a>Tooqueries korzyści
Partycjonowanie może być również używane tooimprove wydajność zapytań.  Jeśli zapytanie zastosowanie filtru kolumny podzielone na partycje, może to ograniczyć hello tooonly skanowania hello kwalifikowanie partycje, które mogą być znacznie mniejszy podzbiór danych hello, unikając tabeli pełnego skanowania.  Z wprowadzeniem hello klastrowane indeksy magazynu kolumn zwiększenia wydajności predykatu eliminacji hello są mniej korzystne, ale w niektórych przypadkach może być tooqueries korzyści.  Na przykład jeśli tabela faktów sprzedaży hello jest podzielona na partycje do 36 miesięcy za pomocą pola Data sprzedaży hello, następnie zapytań, które odfiltrować Data sprzedaży hello można pominąć wyszukiwanie w partycji, które nie pasuje do filtru hello.

## <a name="partition-sizing-guidance"></a>Wskazówki dotyczące rozmiaru partycji
Podczas partycjonowania mogą być używane tooimprove wydajności niektórych scenariuszy tworzenia tabeli z **zbyt wiele** partycji może pogarszać wydajność w pewnych okolicznościach.  Te problemy są szczególnie istotne w przypadku tabel klastrowanego magazynu kolumn.  Partycjonowanie toobe pomocne, jest ważne toounderstand podczas toouse partycjonowania i hello liczba toocreate partycji.  Jest nie twardych reguły szybkiego jako toohow większej liczby partycji są zbyt wiele, zależy od danych i jak wiele partycji ładowania toosimultaneously.  Ale jako ogólne zasadą, traktować Dodawanie 10s too100s partycji, nie 1000s.

Podczas tworzenia partycji na **klastrowanego magazynu kolumn** tabel, jest ważne tooconsider, ile wierszy nastąpi przejście do każdej partycji.  Optymalne kompresji i wydajności tabel klastrowanego magazynu kolumn co najmniej 1 milion wierszy na dystrybucji i partycja na potrzeby.  Przed utworzeniem partycji usługi SQL Data Warehouse już dzieli każdej tabeli 60 rozproszonej bazy danych.  Partycjonowania tabeli tooa dodany jest ponadto dystrybucje toohello utworzone w tle hello.  Jeśli tabela faktów sprzedaży hello zawarte 36 miesięczne partycji i biorąc pod uwagę, że magazyn danych SQL ma 60 dystrybucje hello sprzedaży fakt, że tabela musi zawierać 60 mln wierszy na miesiąc lub 2.1 miliardy wierszy, gdy wszystkie miesiące są wypełniane przy użyciu tego przykładu.  Jeśli tabela zawiera znacznie mniej wierszy niż hello Zalecana minimalna liczba wierszy przypadających na partycję, rozważ użycie mniejszej liczby partycji w kolejności toomake wzrost hello liczba wierszy przypadających na partycję.  Zobacz też hello [indeksowanie] [ Index] artykułu, który obejmuje zapytania uruchamiane na SQL Data Warehouse tooassess hello jakości klastra indeksy magazynu kolumn.

## <a name="syntax-difference-from-sql-server"></a>Różnica składni z programu SQL Server
Usługa SQL Data Warehouse wprowadza uproszczony definicję partycji, która różni się nieznacznie z programu SQL Server.  Partycjonowania funkcje i schematy nie są używane w usłudze SQL Data Warehouse, ponieważ są one w programie SQL Server.  Zamiast tego toodo wystarczy zidentyfikować partycjonowanej kolumny i hello granic punkty.  Składnia hello partycjonowania może być nieco inne niż SQL Server, podstawowe koncepcje hello są hello tego samego.  SQL Server i SQL Data Warehouse obsługuje jedna kolumna partycji w tabeli, które mogą być ranged partycji.  toolearn więcej informacji na temat partycjonowania, zobacz [partycjonowane tabele i indeksy][Partitioned Tables and Indexes].

Witaj w poniższym przykładzie usługi SQL Data Warehouse na partycje [CREATE TABLE] [ CREATE TABLE] instrukcji, partycje tabela FactInternetSales hello w kolumnie OrderDateKey hello:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a>Migrowanie partycjonowania z programu SQL Server
toomigrate programu SQL Server po prostu partycji tooSQL definicje magazynu danych:

* Eliminowanie hello programu SQL Server [schemat partycji][partition scheme].
* Dodaj hello [funkcja partycji] [ partition function] tooyour definicji tworzenia tabeli.

W przypadku migracji tabeli partycjonowanej z hello wystąpienia programu SQL Server, poniżej SQL może pomóc toointerrogate hello liczbę wierszy, które znajdują się w każdej partycji.  Należy pamiętać, że jeśli hello samej szczegółowości partycjonowania jest używany na SQL Data Warehouse, hello liczba wierszy przypadających na partycję zmniejszy się o 60.  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a>Zarządzanie obciążeniami
Jest jeden toofactor uwagę ostatni element w decyzji partycji tabeli toohello [zarządzania obciążenia][workload management].  Zarządzanie obciążenia w usłudze SQL Data Warehouse jest głównie hello zarządzania pamięci i współbieżność.  W hello SQL Data Warehouse maksymalna ilość pamięci przydzielona tooeach dystrybucji podczas wykonywania zapytania jest klasy zasobów o której działalność.  W idealnym przypadku będzie o rozmiarze partycji, biorąc pod uwagę innych czynników, takich jak wymagania dotyczące pamięci hello tworzenia klastrowane indeksy magazynu kolumn.  Klastrowane korzyści indeksy magazynu kolumn znacznie, gdy są przydzielone więcej pamięci.  W związku z tym można się, że tooensure, który odbudować indeksu partycji nie jest zagłodzone pamięci. Zwiększenie hello ilość pamięci dostępna tooyour zapytania można osiągnąć przełączyć hello domyślnej roli, smallrc, tooone z hello innych ról, takich jak largerc.

Informacje dotyczące hello alokacji pamięci dla dystrybucji są dostępne, badając hello zasobów zarządcy dynamicznych widoków zarządzania. W rzeczywistości Twojej przydział pamięci jest mniejsza niż poniższe rysunki hello. Zapewnia to jednak poziom wskazówki, które można używać podczas określania rozmiaru partycji dla danych operacji zarządzania.  Spróbuj tooavoid zmiany rozmiaru partycji przekracza przydział pamięci hello podał hello klasy zasobów bardzo duża. Jeśli partycji rosnąć poza tym rysunku uruchomieniem hello ryzyko wykorzystania pamięci, co z kolei prowadzi tooless optymalnej kompresji.

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a>Przełączanie partycji
Magazyn danych SQL obsługuje partycji dzielenia, łączenia i przełączania. Każda z tych funkcji jest excuted przy użyciu hello [instrukcji ALTER TABLE] [ ALTER TABLE] instrukcji.

partycje tooswitch między dwiema tabelami Pamiętaj, że partycje hello są wyrównane na ich odpowiednich granice a hello definicje tabel są takie same. Jako ograniczenia sprawdzania nie są dostępne wartości w tabeli źródłowej tabeli hello tooenforce hello zakresu musi zawierać hello sam partycji granice jako hello tabeli docelowej. Jeśli nie jest to hello, przełącznik partycji hello wystąpi błąd, ponieważ metadane partycji hello nie będą synchronizowane.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Jak toosplit partycji, która zawiera dane
Witaj najbardziej efektywny metody toosplit partycji, która zawiera już dane jest toouse `CTAS` instrukcji. Tabeli partycjonowanej hello jest klastrowanego magazynu kolumn następnie hello partycji tabeli może być puste przed mogą być dzielone.

Poniżej znajdują się magazynu kolumn partycjonowane przykładową tabelę zawierającą po jednym wierszu w każdej partycji:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> Tworzenie obiektu Statystyka hello możemy upewnij się, że tych metadanych tabeli jest bardziej dokładne. Jeśli firma Microsoft pominąć tworzenie statystyk, SQL Data Warehouse użyje wartości domyślnych. Dla Przejrzyj szczegóły dotyczące statystyk [statystyki][statistics].
> 
> 

Firma Microsoft może następnie wyszukiwać hello liczba wierszy za pomocą hello `sys.partitions` widoku katalogu:

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

Jeśli ta tabela spróbujemy toosplit uzyskujemy błąd:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346, 15 poziom, stan 1, wiersz 44 PODZIELONY klauzula instrukcji ALTER PARTITION nie powiodło się, ponieważ partycja hello nie jest pusty.  Gdy istnieje indeks magazynu kolumn w tabeli hello można podzielić tylko puste partycje w. Rozważ wyłączenie indeksu magazynu kolumn hello przed wykonaniem instrukcji ALTER PARTITION hello, a następnie odbudowanie indeksu magazynu kolumn powitania po ukończeniu operacji ALTER PARTITION.

Jednak używamy `CTAS` toocreate nowe toohold tabeli danych.

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

Jak hello granice partycji są wyrównane przełącznik jest dozwolone. Spowoduje to pozostawienie tabeli źródłowej hello z pustą partycję, który następnie możemy podzielić.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Pozostało toodo jest tooalign toohello naszych danych partycji nowych granic przy użyciu `CTAS` i przejdź wstecz w tabeli głównej toohello naszych danych

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

Po zakończeniu hello przepływu danych hello jest dobrym rozwiązaniem toorefresh hello statystyk na powitania docelowej tabeli tooensure hello dystrybucji nowych danych hello w ich odpowiednich partycji dokładnie odzwierciedlał:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Tabela partycjonowania kontroli źródła
tooavoid Twojego definicji tabeli z **uszkodzona** w systemie kontroli źródła może być hello tooconsider następujące podejście:

1. Utwórz hello tabeli partycjonowanej tabeli, ale bez wartości partycji

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. `SPLIT`Tabela Hello jako część procesu wdrażania hello:

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

Z tego podejścia hello pozostaje statyczna kodu w kontroli źródła i partycjonowania wartości granicznych hello mogą toobe dynamiczne; zmieniających się z magazynem hello wraz z upływem czasu.

## <a name="next-steps"></a>Następne kroki
toolearn więcej, zobacz artykuły hello na [omówienie tabeli][Overview], [typy danych tabeli][Data Types], [Dystrybucja tabeli] [ Distribute], [Indeksowania tabeli][Index], [utrzymania statystyk tabeli] [ Statistics] i [ Tabele tymczasowe][Temporary].  Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
