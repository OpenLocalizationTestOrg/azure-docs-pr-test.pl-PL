---
title: "Transakcje aaaOptimizing dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Najlepszych rozwiązań o pisaniu aktualizacje wydajne transakcji w magazynie danych SQL Azure"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Optymalizacja transakcji dla magazynu danych SQL
W tym artykule opisano, jak toooptimize hello wydajności kodu transakcyjnego przy jednoczesnym zmniejszeniu ryzyka dla długich cofnięcia.

## <a name="transactions-and-logging"></a>Rejestrowanie i transakcji
Transakcje są ważne składnika aparacie relacyjnej bazy danych. Usługa SQL Data Warehouse używa transakcji podczas modyfikacji danych. Te transakcje można jawnych ani niejawnych. Pojedynczy `INSERT`, `UPDATE` i `DELETE` instrukcje są wszystkie przykłady w transakcji niejawnej. Jawnych transakcji są zapisywane bezpośrednio przez dewelopera przy użyciu `BEGIN TRAN`, `COMMIT TRAN` lub `ROLLBACK TRAN` i są zazwyczaj używane do wielu instrukcji modyfikacji muszą toobe powiązane razem w jednym Atomowej jednostki. 

Usługa Azure SQL Data Warehouse zatwierdza przy użyciu dzienników transakcji toohello zmian w bazie danych. Rozkład każdy ma własny dziennik transakcji. Zapisy dziennika transakcji są automatyczne. Nie jest wymagana żadna konfiguracja. Jednak podczas tego procesu gwarantuje zapisu hello go wprowadzić obciążenia w systemie hello. Pisanie kodu transakcyjnie wydajne, można zminimalizować wpływ ten. Transakcyjnie efektywne zasadniczo mieszczą się na dwie kategorie.

* Korzystaj z konstrukcji minimalne rejestrowanie, jeśli jest to możliwe
* Przetwarzania danych przy użyciu pojedynczego tooavoid zakresie partie długotrwałe transakcje
* Przyjmuje partycji przełączania wzorca dla dużych modyfikacje tooa podane partycji

## <a name="minimal-vs-full-logging"></a>Minimalny a pełne rejestrowanie
W przeciwieństwie do pełni zarejestrowanych operacji, korzystających z hello transakcji dziennika tookeep Śledź każdy wiersz zmiany, minimalny zestaw zarejestrowanych operacji zachować informacje o zakresie alokacji i tylko zmiany metadanych. W związku z tym minimalne rejestrowanie obejmuje hello tylko te informacje, które są wymagane toorollback hello transakcji w przypadku hello awarii lub jawnego żądania rejestrowania (`ROLLBACK TRAN`). Jak znacznie mniej informacje są śledzone w dzienniku transakcji hello, minimalny zestaw zarejestrowanych operacji działa lepiej niż podobnie rozmiarze pełni zarejestrowanych operacji. Ponadto ponieważ zapisy mniejszą liczbę przejść hello dziennika transakcji, generowany jest znacznie mniejszą ilość danych dziennika, i dlatego jest efektywne więcej operacji We/Wy.

limity bezpieczeństwa transakcji Hello mają zastosowanie tylko operacje toofully rejestrowane.

> [!NOTE]
> Minimalny zestaw zarejestrowanych operacji mogą uczestniczyć w jawnych transakcji. Wszystkie zmiany w alokacji struktur są śledzone, jest możliwe tooroll wstecz minimalny rejestrowane operacji. Jest ważne, rejestrowana toounderstand, że zmiana hello jest "minimalny zestaw" nie jest, które nie zostały zarejestrowane.
> 
> 

## <a name="minimally-logged-operations"></a>Minimalny zestaw zarejestrowanych operacji
Hello są w stanie są rejestrowane następujące operacje:

* UTWÓRZ TABLE AS SELECT ([CTAS][CTAS])
* INSERT... WYBIERZ
* TWORZENIE INDEKSU
* ALTER INDEX REBUILD
* INDEKS
* OBCIĄĆ TABELI
* TABELĘ
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> Operacje przenoszenia danych wewnętrznych (takich jak `BROADCAST` i `SHUFFLE`) nie dotyczy limitu bezpieczeństwa transakcji hello.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Minimalne rejestrowanie z ładowanie zbiorcze
`CTAS`i `INSERT...SELECT` zarówno zbiorcze operacje obciążenia. Jednak zarówno wpływało definicji tabeli docelowej hello i zależą od scenariusza obciążenia hello. Poniżej znajduje się tabela, która wyjaśnia, jeśli operacji zbiorczej zostanie całkowicie lub minimalny zarejestrowane:  

| Podstawowy indeks | Scenariusz obciążenia | Tryb rejestrowania |
| --- | --- | --- |
| Sterty |Dowolne |**Minimalny** |
| Indeks klastrowany |Tabela docelowa pusty |**Minimalny** |
| Indeks klastrowany |Załadować wierszy nie pokrywają się z istniejących stron w lokalizacji docelowej |**Minimalny** |
| Indeks klastrowany |Nakładanie się załadować wierszy z istniejących stron w lokalizacji docelowej |Pełne |
| Klastrowany indeks magazynu kolumn |Rozmiar partii > = 102400 na partycji wyrównane dystrybucji |**Minimalny** |
| Klastrowany indeks magazynu kolumn |Rozmiar < 102400 na partycji wyrównane dystrybucji partii |Pełne |

Warto zauważyć, że wszystkie zapisy tooupdate dodatkowej lub nieklastrowanych indeksów zawsze będą pełni rejestrowane operacji.

> [!IMPORTANT]
> Magazyn danych SQL ma 60 dystrybucji. W związku z tym zakładając, że wszystkie wiersze są równomiernie, a kierowanych do jednej partycji, Twoje partii musi toocontain 6,144,000 wierszy lub większy toobe minimalny rejestrowane podczas zapisywania tooa klastrowany indeks magazynu kolumn. Jeśli hello tabela jest podzielona na partycje i wierszy hello wstawiane span granice partycji, wymagana będzie 6,144,000 wierszy na granicy partycji przy założeniu nawet danych dystrybucji. Każdej partycji w każdej dystrybucji niezależnie przekraczać hello 102 400 wiersza próg toobe insert hello rejestrowane w hello dystrybucji.
> 
> 

Ładowanie danych do niepustej tabeli z indeksem klastrowanym często może zawierać mieszaninę pełni zarejestrowane i zarejestrowane minimalny zestaw wierszy. Indeks klastrowany jest drzewo zrównoważony (b drzewa) stron. Jeśli strona hello zapisywana tooalready zawiera wiersze z innej transakcji, następnie zapisuje te będą pełni rejestrowane. Jednak jeśli strona hello jest pusty następnie hello zapisu toothat strona zostanie minimalny zarejestrowane.

## <a name="optimizing-deletes"></a>Optymalizacja usuwa
`DELETE`jest całkowicie zarejestrowanych operacji.  Jeśli potrzebujesz toodelete dużej ilości danych w tabeli lub partycję, często warto więcej zbyt`SELECT` hello danych mają tookeep, które mogą być uruchamiane jako minimalny zestaw zarejestrowanych operacji.  tooaccomplish, Utwórz nową tabelę z [CTAS][CTAS].  Po utworzeniu, użyj [zmienić] [ RENAME] tooswap limit starego tabeli z tabelą hello nowo utworzona.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a>Optymalizacja aktualizacji
`UPDATE`jest całkowicie zarejestrowanych operacji.  Jeśli potrzebujesz tooupdate dużą liczbę wierszy w tabeli lub partycję często jest znacznie bardziej wydajne toouse minimalny zestaw zarejestrowanych operacji takich jak [CTAS] [ CTAS] toodo tak.

W hello przykładzie poniżej aktualizacji pełnej tabeli został przekonwertowany tooa `CTAS` , dzięki czemu możliwe jest minimalnym rejestrowania.

W takim przypadku retrospektywnie dodajemy sprzedaży toohello dyskontowa kwota w tabeli hello:

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Ponowne tworzenie dużych tabel mogą korzystać z funkcji zarządzania obciążenie SQL Data Warehouse. Dla bardziej szczegółowe informacje można znaleźć w sekcji Zarządzanie obciążenia toohello w hello [współbieżności] [ concurrency] artykułu.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Optymalizacja przełączania partycji
W przypadku zastosowania zmian dużą skalę w [tabeli partycji][table partition], partycji przełączania wzorca tworzy wiele znaczeniu. Jeśli hello modyfikacji danych jest znacząca i obejmuje wiele partycji, po prostu Iterowanie za pośrednictwem partycje hello osiąga hello takiego samego wyniku.

tooperform kroki Hello przełącznik partycji są następujące:

1. Utwórz pustą z partycji
2. Przeprowadź aktualizację"hello" CTAS
3. Przełącz się hello istniejących danych toohello limit tabeli
4. Przełącz hello nowe dane.
5. Czyszczenie danych hello

Jednak toohelp zidentyfikować tooswitch partycje hello zostanie najpierw musimy toobuild procedury pomocnika, takich jak hello jedną poniżej. 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

Ta procedura maksymalizuje ponownego użycia kodu i przechowuje przełączania przykład mniejszych hello partycji.

Poniższy kod Hello pokazuje, że hello pięć kroków wymienionych powyżej tooachieve pełne partycji przełączania procedury.

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Minimalizowanie rejestrowanie z małych partii
W przypadku operacji modyfikacji dużej ilości danych może dokonać znaczeniu toodivide hello operacji na fragmenty lub partie jednostki hello tooscope pracy.

Poniżej znajduje się przykład pracy. rozmiar partii Hello ustawiono tooa trivial numer toohighlight hello technik. W rzeczywistości rozmiar partii hello jest znacznie większe. 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a>Wstrzymywanie i skalowanie wskazówki
Usługa Azure SQL Data Warehouse pozwala wstrzymać, wznowić i skalowanie magazynu danych na żądanie. Po wstrzymaniu lub skalować magazyn danych SQL jest ważne toounderstand wszystkich transakcji locie kończą natychmiast; powoduje toobe wszystkie otwarte transakcje wycofana. Jeśli obciążenie wystawił długotrwałe i modyfikacji niepełne dane przed Wstrzymaj toohello lub operacji skalowania, a następnie tej pracy należy toobe cofnięta. Może to mieć wpływ na powitania czas toopause lub skalowania bazy danych magazynu danych SQL Azure. 

> [!IMPORTANT]
> Zarówno `UPDATE` i `DELETE` są całkowicie zarejestrowanych operacji i dlatego te Cofnij/ponów operacji może potrwać znacznie dłużej, niż równoważne rejestrowane operacji. 
> 
> 

najlepszym scenariuszu Hello jest toolet transmitowane danych modyfikacji transakcji ukończone przed toopausing lub skalowania SQL Data Warehouse. Jednak to może nie zawsze być praktyczne. ryzyka hello toomitigate wycofania długie, weź pod uwagę jedną z hello następujące opcje:

* Napisz ponownie przy użyciu długotrwałe operacje [CTAS][CTAS]
* Operacja hello podziału na fragmenty o różnych; korzysta z podzbioru hello wierszy

## <a name="next-steps"></a>Następne kroki
Zobacz [transakcje w usłudze SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn więcej informacji na temat poziomów izolacji i limity transakcyjnych.  Omówienie innych najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

