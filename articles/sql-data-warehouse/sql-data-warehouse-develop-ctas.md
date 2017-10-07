---
title: "aaaCreate tabeli jako wybierz (CTAS) w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące programowania z hello Utwórz tabelę jako select — instrukcja (CTAS) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Utwórz tabelę jako Select (CTAS) w magazynie danych SQL
Utwórz tabelę jako wybierz lub `CTAS` jest jednym z hello najważniejszych funkcjach T-SQL. Jest całkowicie zrównoleglone operacja, która tworzy nową tabelę oparte na danych wyjściowych hello instrukcji SELECT. `CTAS`jest toocreate najprostszym i najszybszym sposobem hello kopii tabeli. Ten dokument zawiera zarówno przykłady i najlepsze rozwiązania dotyczące `CTAS`.

## <a name="selectinto-vs-ctas"></a>WYBIERZ... W wersji programu vs. CTAS
Można rozważyć `CTAS` nadrzędne obciążona wersja `SELECT..INTO`.

Poniżej przedstawiono przykładowy prostą `SELECT..INTO` instrukcji:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

W powyższym przykładzie hello `[dbo].[FactInternetSales_new]` zostałyby utworzone ROUND_ROBIN rozproszonej tabeli z INDEKSEM magazynu kolumn w KLASTRZE na nim są one wartości domyślnych tabeli hello w usłudze Azure SQL Data Warehouse.

`SELECT..INTO`jednak nie pozwala toochange wpisz albo hello dystrybucji metody lub hello indeks jako część hello operacji. Jest to, gdy `CTAS` polega na.

tooconvert hello powyżej za`CTAS` jest dość proste:

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

Z `CTAS` są możliwe toochange zarówno hello dystrybucji hello tabeli danych, a także hello typ tabeli. 

> [!NOTE]
> Jeśli chcesz tylko toochange hello indeksu w Twojej `CTAS` operacji i hello tabela źródłowa jest rozpowszechniane skrót, a następnie z `CTAS` wykona operację najlepiej, jeśli hello tego samego typu kolumny i danych dystrybucji. Pozwoli to uniknąć cross przenoszenia danych dystrybucji podczas operacji hello, które jest bardziej wydajny.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>Przy użyciu toocopy CTAS tabeli
Możliwe, że jedną z najbardziej typowych hello korzysta z `CTAS` jest tworzenie kopii tabeli, dzięki czemu można zmienić hello DDL. Jeśli na przykład pierwotnie utworzona jako tabela `ROUND_ROBIN` a teraz chcesz je zmienić tabeli tooa od kolumny, `CTAS` się, jak można zmienić kolumny dystrybucji hello. `CTAS`można także toochange używane typy partycjonowania, indeksowania lub kolumny.

Załóżmy, że utworzono tej tabeli za pomocą typu dystrybucji domyślne hello `ROUND_ROBIN` rozproszonych, ponieważ kolumna nie dystrybucji została określona w hello `CREATE TABLE`.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

Teraz ma toocreate nową kopię tej tabeli z indeksem magazynu kolumn w klastrze tak, aby można było korzystać z wydajności hello tabel klastrowanego magazynu kolumn. Należy zawsze toodistribute tej tabeli po klucz produktu od są przewidywanie sprzężenia od tej kolumny, a ma tooavoid przenoszenia danych podczas sprzężenia na klucz produktu. Na koniec ma również tooadd partycjonowania na OrderDateKey, dzięki czemu można szybko usunąć stare dane przez usunięcie starego partycji. Oto hello CTAS instrukcja, która będzie skopiować starego tabeli do nowej tabeli.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

Na koniec można zmienić Twojego tooswap tabel w nowej tabeli, a następnie upuść starego tabeli.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.  W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello.  Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Przy użyciu toowork CTAS wokół nieobsługiwane funkcje
`CTAS`może być również używane toowork wokół szereg funkcji hello nieobsługiwany wymienionych poniżej. To może często udowodnić toobe sytuacji win/win nie tylko kodzie będą zgodne, ale będą często wykonywane szybciej na magazyn danych SQL. Jest to wyniku pełni zrównoleglone projekt. Scenariusze, które można pracować z CTAS wokół obejmują:

* SPRZĘŻENIA ANSI na aktualizacje
* Sprzężenia ANSI na usuwaniu
* MERGE — instrukcja

> [!NOTE]
> Spróbuj toothink "CTAS pierwszy". Jeśli uważasz, że uda się rozwiązać problem przy użyciu `CTAS` hello najlepsze sposób tooapproach zazwyczaj jest to go — nawet jeśli w związku z tym pisania większej ilości danych.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>ANSI zamienny sprzężenia dla instrukcji update
Może się okazać się, że masz złożonych aktualizacji, której jest przyłączany więcej niż dwie tabele ze sobą przy użyciu ANSI dołączenie hello tooperform składni UPDATE lub DELETE.

Załóżmy, że miała tooupdate tej tabeli:

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

oryginalne zapytanie Hello może sprawdzono podobny do następującego:

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

Ponieważ Magazyn danych SQL nie obsługuje ANSI sprzężenia w hello `FROM` klauzuli `UPDATE` instrukcji, nie można skopiować ten kod nad zmieniając nieco.

Można użyć kombinacji `CTAS` i niejawne join tooreplace ten kod:

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a>Zastępuje sprzężenia ANSI usunąć — instrukcje
Czasami najlepszym podejściem hello związanych z usuwaniem danych jest toouse `CTAS`. Zamiast usuwania danych powitania po prostu wybierz hello dane, które mają tookeep. To szczególnie istotne dla `DELETE` instrukcji używających ansi dołączenie składni, ponieważ usługa SQL Data Warehouse nie obsługuje sprzężeń ANSI w hello `FROM` klauzuli `DELETE` instrukcji.

Przykład przekonwertowanego instrukcji DELETE jest dostępny poniżej:

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a>Zastąp instrukcjach merge
Instrukcje scalania można zastąpić, co najmniej w części, za pomocą `CTAS`. Można skonsolidować hello `INSERT` i hello `UPDATE` w jednej instrukcji. Rekordy usunięte potrzebny toobe zamknięte w drugim instrukcji.

Przykład `UPSERT` znajduje się poniżej:

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Zalecenie CTAS: jawnie określać typ danych i dopuszczanie wartości null dla danych wyjściowych
Podczas migrowania kod może się okazać, czy uruchomione przez ten typ kodowania wzorca:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instynktownie może traktować ten kod tooa CTAS należy zmigrować, a użytkownik będzie poprawna. Istnieje jednak jest ukrytym problem.

Witaj następujący kod nie uzyskanie takiego samego wyniku hello:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Zwróć uwagę, hello kolumny "wynik" przenosi do przodu hello wartości typu i dopuszczanie wartości null danych hello wyrażenia. Może to prowadzić odchylenia toosubtle wartości, jeśli nie są dokładne.

Spróbuj następujących hello na przykład:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

wartość Hello przechowywane dla wyniku różni się. Jak hello utrwalonego wartości w kolumnie wyników hello jest używany w innych wyrażenia hello błąd staje się jeszcze bardziej znaczące.

![][1]

Jest to szczególnie ważne w przypadku migracji danych. Mimo że hello drugiego zapytania jest raczej dokładniejsze występuje problem. Hello dane byłyby różnych toohello porównaniu systemu źródłowego i powodująca tooquestions integralności w hello migracji. Jest to jedna z rzadkich przypadkach gdy odpowiedzi "nieprawidłowe" hello jest rzeczywiście hello prawo jeden!

Witaj Przyczyna widzimy tej różnicy między wyniki hello dwa działa tooimplicit typu rzutowania. Witaj pierwszej tabeli hello przykład definiuje hello definicji kolumny. Po wstawieniu wiersza hello występuje niejawna konwersja typu. W drugim przykładzie hello nie ma żadnych niejawna konwersja typu jako wyrażenie hello definiuje typ danych kolumny hello. Zwróć uwagę, również tej kolumny hello w drugim przykładzie hello została zdefiniowana jako kolumny wartości null należy w pierwszym przykładzie hello nie. Podczas tworzenia tabeli hello w hello pierwszym przykładzie kolumny opcjami dopuszczania wartości null został jawnie zdefiniowany. W drugim przykładzie hello został właśnie opuściła wyrażenie toohello i domyślnie spowodowałoby to w definicji wartości NULL.  

tooresolve tych problemów, które należy jawnie ustawić konwersji typu hello i dopuszczanie wartości null hello `SELECT` część hello `CTAS` instrukcji. Nie można ustawić te właściwości w hello tworzenie części tabeli.

Witaj w poniższym przykładzie pokazano, jak toofix hello kodu:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Należy uwzględnić następujące hello:

* CAST lub CONVERT może zostały już użyte
* ISNULL jest używane tooforce dopuszczania wartości null nie ŁĄCZONEJ
* ISNULL jest najbardziej zewnętrzną funkcję hello
* druga część hello ISNULL Hello jest stałą tj. 0

> [!NOTE]
> Dla poprawnie ustawić hello toobe dopuszczania wartości null jest istotne toouse `ISNULL` i nie `COALESCE`. `COALESCE`nie jest deterministyczna funkcji i dlatego hello wynik hello wyrażenia zawsze będzie NULLable. `ISNULL`różni się. Jest ona deterministyczna. W związku z tym jeśli hello drugiej części hello `ISNULL` funkcja jest stałą lub literałem, a następnie zostanie użyta wartość wynikową hello NOT NULL.
> 
> 

Tej porady nie jest po prostu przydatne w przypadku zapewnienia integralności hello obliczeń. Należy również do przełączenia partycji tabeli. Załóżmy, że w tej tabeli zdefiniowany jako Twoje fakt:

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

Pole wartości hello jest jednak wyrażenie obliczeniowej nie jest częścią hello źródła danych.

toocreate partycjonowanej zestawu danych toodo może być to:

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

Zapytanie Hello może działać dokładnie poprawnie. Hello problem jest dostarczany podczas próby tooperform hello partycji przełącznika. definicje tabel Hello są niezgodne. definicje tabel hello toomake odpowiada hello CTAS musi toobe zmodyfikowane.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

Widać w związku z tym, że typ spójności i utrzymywanie właściwości dopuszczania wartości null na CTAS dobrej engineering najlepszym rozwiązaniem jest. Pomaga integralności toomaintain w obliczeniach ono oraz gwarantuje również, że możliwe jest przełączanie partycji.

Przeczytaj tooMSDN, aby uzyskać więcej informacji na temat używania [CTAS][CTAS]. Jest jednym z najważniejszych instrukcje hello w usłudze Azure SQL Data Warehouse. Upewnij się, że rozumiesz dokładnie.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
