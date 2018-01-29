---
title: "Optymalizacja transakcji dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Optymalizacja transakcji dla magazynu danych SQL
W tym artykule wyjaśniono, jak zoptymalizować wydajność kodu transakcyjnego przy jednoczesnym zmniejszeniu ryzyka dla długich wycofań.

## <a name="transactions-and-logging"></a>Rejestrowanie i transakcji
Transakcje są ważne składnika aparacie relacyjnej bazy danych. Usługa SQL Data Warehouse używa transakcji podczas modyfikacji danych. Te transakcje można jawnych ani niejawnych. Pojedynczy `INSERT`, `UPDATE` i `DELETE` instrukcje są wszystkie przykłady w transakcji niejawnej. Jawnych transakcji są zapisywane bezpośrednio przez dewelopera przy użyciu `BEGIN TRAN`, `COMMIT TRAN` lub `ROLLBACK TRAN` i są zwykle używane, jeśli wiele instrukcji modyfikacji muszą być powiązane razem w jednym Atomowej jednostki. 

Usługa Azure SQL Data Warehouse zatwierdza zmiany w bazie danych przy użyciu dzienników transakcji. Rozkład każdy ma własny dziennik transakcji. Zapisy dziennika transakcji są automatyczne. Nie jest wymagana żadna konfiguracja. Jednak podczas tego procesu gwarantuje zapisu on wprowadzić obciążenia w systemie. Pisanie kodu transakcyjnie wydajne, można zminimalizować wpływ ten. Transakcyjnie efektywne zasadniczo mieszczą się na dwie kategorie.

* Korzystaj z konstrukcji minimalne rejestrowanie, jeśli jest to możliwe
* Przetwarzania danych przy użyciu zakres partie, aby uniknąć pojedynczej długotrwałej transakcji
* Przyjmuje partycji przełączania wzorca dla dużych modyfikacje w danej partycji

## <a name="minimal-vs-full-logging"></a>Minimalny a pełne rejestrowanie
W przeciwieństwie do pełni zarejestrowanych operacji, które korzystania z dziennika transakcji do śledzenia każdej zmiany wiersza, minimalny zestaw zarejestrowanych operacji zachować informacje o zakresie alokacji i tylko zmiany metadanych. W związku z tym minimalne rejestrowanie obejmuje tylko informacje wymagane do wycofania transakcji w przypadku awarii lub jawne żądanie logowania (`ROLLBACK TRAN`). Jak znacznie mniej informacje są śledzone w dzienniku transakcji, minimalny zestaw zarejestrowanych operacji działa lepiej niż podobnie rozmiarze pełni zarejestrowanych operacji. Ponadto ponieważ zapisy mniejszą liczbę przejść dziennika transakcji, generowany jest znacznie mniejszą ilość danych dziennika, i dlatego jest efektywne więcej operacji We/Wy.

Limity bezpieczeństwa transakcji dotyczą tylko pełni zarejestrowanych operacji.

> [!NOTE]
> Minimalny zestaw zarejestrowanych operacji mogą uczestniczyć w jawnych transakcji. Jak są śledzone wszystkie zmiany w strukturach alokacji, jest to możliwe wycofać migrację zarejestrowanych operacji. Ważne jest, aby zrozumieć, że zmiana jest rejestrowane "minimalnie" nie jest które nie zostały zarejestrowane.
> 
> 

## <a name="minimally-logged-operations"></a>Minimalny zestaw zarejestrowanych operacji
Stanie są rejestrowane są następujące operacje:

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
> Operacje przenoszenia danych wewnętrznych (takich jak `BROADCAST` i `SHUFFLE`) nie dotyczy limitu bezpieczeństwa transakcji.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Minimalne rejestrowanie z ładowanie zbiorcze
`CTAS`i `INSERT...SELECT` zarówno zbiorcze operacje obciążenia. Jednak zarówno wpływało definicji tabeli docelowej i zależą od scenariusza obciążenia. Poniżej znajduje się tabela, która wyjaśnia, jeśli operacji zbiorczej zostanie całkowicie lub minimalny zarejestrowane:  

| Podstawowy indeks | Scenariusz obciążenia | Tryb rejestrowania |
| --- | --- | --- |
| Sterty |Dowolne |**Minimalny** |
| Indeks klastrowany |Tabela docelowa pusty |**Minimalny** |
| Indeks klastrowany |Załadować wierszy nie pokrywają się z istniejących stron w lokalizacji docelowej |**Minimalny** |
| Indeks klastrowany |Nakładanie się załadować wierszy z istniejących stron w lokalizacji docelowej |Pełne |
| Klastrowany indeks magazynu kolumn |Rozmiar partii > = 102400 na partycji wyrównane dystrybucji |**Minimalny** |
| Klastrowany indeks magazynu kolumn |Rozmiar < 102400 na partycji wyrównane dystrybucji partii |Pełne |

Warto zauważyć, że żadnych zapisów w celu aktualizacji dodatkowej lub nieklastrowanych indeksów będzie zawsze pełni zarejestrowanych operacji.

> [!IMPORTANT]
> Magazyn danych SQL ma 60 dystrybucji. W związku z tym zakładając, że wszystkie wiersze są równomiernie i kierowanych do jednej partycji, z partii musi zawierać 6,144,000 wierszy lub większy minimalny było rejestrowane podczas zapisywania do klastrowanego indeksu magazynu kolumn. Jeśli tabela jest podzielona na partycje i wiersze wstawiane span granice partycji, będzie konieczne 6,144,000 wierszy na granicy partycji przy założeniu nawet danych dystrybucji. Każdej partycji w każdej dystrybucji niezależnie może przekroczyć próg 102 400 wiersza wstawiania minimalny zalogowania się do dystrybucji.
> 
> 

Ładowanie danych do niepustej tabeli z indeksem klastrowanym często może zawierać mieszaninę pełni zarejestrowane i zarejestrowane minimalny zestaw wierszy. Indeks klastrowany jest drzewo zrównoważony (b drzewa) stron. Jeśli strona zapisywana już zawiera wiersze z innej transakcji, następnie zapisuje te będą pełni rejestrowane. Jednak jeśli strona jest pusta następnie zapisu na tej stronie będą minimalny rejestrowane.

## <a name="optimizing-deletes"></a>Optymalizacja usuwa
`DELETE`jest całkowicie zarejestrowanych operacji.  Jeśli musisz usunąć dużej ilości danych w tabeli lub partycję, często dobrym rozwiązaniem `SELECT` dane chcesz zachować, które mogą być uruchamiane jako minimalny zestaw zarejestrowanych operacji.  W tym celu utwórz nową tabelę z [CTAS][CTAS].  Po utworzeniu, użyj [zmienić] [ RENAME] wymienić starego tabeli z nowo utworzonej tabeli.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
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

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a>Optymalizacja aktualizacji
`UPDATE`jest całkowicie zarejestrowanych operacji.  Jeśli musisz zaktualizować dużą liczbę wierszy w tabeli lub partycję często jest znacznie bardziej wydajne używać minimalny zestaw zarejestrowanych operacji, takich jak [CTAS] [ CTAS] Aby to zrobić.

W przykładzie poniżej tabeli pełnej aktualizacji został przekonwertowany na `CTAS` , dzięki czemu możliwe jest minimalnym rejestrowania.

W takim przypadku retrospektywnie dodajemy kwota rabatu sprzedaży w tabeli:

```sql
--Step 01. Create a new table containing the "Update". 
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

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Ponowne tworzenie dużych tabel mogą korzystać z funkcji zarządzania obciążenie SQL Data Warehouse. Dla więcej szczegółowych informacji można znaleźć w sekcji zarządzania obciążenia [współbieżności] [ concurrency] artykułu.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Optymalizacja przełączania partycji
W przypadku zastosowania zmian dużą skalę w [tabeli partycji][table partition], partycji przełączania wzorca tworzy wiele znaczeniu. Jeśli modyfikacji danych jest znacząca i obejmuje wiele partycji, następnie po prostu Iterowanie po partycje osiąga ten sam rezultat.

Czynności do wykonania przełącznik partycji są następujące:

1. Utwórz pustą z partycji
2. Przeprowadź aktualizację CTAS
3. Przełącz się istniejące dane do tabeli poza
4. Przełączanie w nowych danych
5. Czyszczenie danych

Jednak aby ułatwić identyfikację partycje do przełącznika najpierw musimy kompilacji procedury pomocnika, takie jak poniżej. 

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

Ta procedura maksymalizuje ponownego użycia kodu i przechowuje przełączania przykład mniejszych partycji.

Poniższy kod pokazuje pięć kroków wymienionych powyżej, aby osiągnąć pełną partycji przełączania procedury.

```sql
--Create a partitioned aligned empty table to switch out the data 
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

--Create a partitioned aligned table and update the data in the select portion of the CTAS
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

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Minimalizowanie rejestrowanie z małych partii
Dla operacji modyfikacji dużej ilości danych na jego może być uzasadniona do dzielenia operacji na fragmenty lub partie, aby ustawić zakres jednostka pracy.

Poniżej znajduje się przykład pracy. Rozmiar partii ustawiono trivial numer aby wyróżnić techniki. W rzeczywistości rozmiar partii jest znacznie większe. 

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
Usługa Azure SQL Data Warehouse pozwala wstrzymać, wznowić i skalowanie magazynu danych na żądanie. Po wstrzymaniu lub skalować magazyn danych SQL ważne jest, aby zrozumieć wszystkich transakcji locie kończą natychmiast; co spowoduje cofnięcie transakcji otwartych. Jeśli obciążenie wystawił długo uruchomione i nieukończone modyfikacji danych przed operację wstrzymywania lub skalę, następnie tej pracy należy można cofnąć. Może to mieć wpływ na czas wymagany do wstrzymania lub skalowania bazy danych magazynu danych SQL Azure. 

> [!IMPORTANT]
> Zarówno `UPDATE` i `DELETE` są całkowicie zarejestrowanych operacji i dlatego te Cofnij/ponów operacji może potrwać znacznie dłużej, niż równoważne rejestrowane operacji. 
> 
> 

Najlepszym scenariuszu jest umożliwienie w transakcji modyfikacji dane transmitowane ukończone przed wstrzymaniem lub skalowania SQL Data Warehouse. Jednak to może nie zawsze być praktyczne. Aby ograniczyć ryzyko długi wycofywania, należy wziąć pod uwagę jedną z następujących opcji:

* Napisz ponownie przy użyciu długotrwałe operacje [CTAS][CTAS]
* Operacja podziału na fragmenty o różnych; korzysta z podzbioru wierszy

## <a name="next-steps"></a>Następne kroki
Zobacz [transakcje w usłudze SQL Data Warehouse] [ Transactions in SQL Data Warehouse] Aby dowiedzieć się więcej o poziomie izolacji i limity transakcyjnych.  Omówienie innych najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

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

