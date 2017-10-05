---
title: "Utwórz tabelę jako wybierz (CTAS) w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące programowania z Utwórz tabelę jako instrukcji select (CTAS) w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
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
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="1427d-103">Utwórz tabelę jako Select (CTAS) w magazynie danych SQL</span><span class="sxs-lookup"><span data-stu-id="1427d-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="1427d-104">Utwórz tabelę jako wybierz lub `CTAS` jest jedną z najważniejszych funkcji T-SQL jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="1427d-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="1427d-105">Jest całkowicie zrównoleglone operacja, która tworzy nową tabelę oparte na danych wyjściowych instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="1427d-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="1427d-106">`CTAS`jest najprostszym i najszybszym sposobem tworzenia kopii tabeli.</span><span class="sxs-lookup"><span data-stu-id="1427d-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="1427d-107">Ten dokument zawiera zarówno przykłady i najlepsze rozwiązania dotyczące `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="1427d-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="1427d-108">WYBIERZ... W wersji programu vs. CTAS</span><span class="sxs-lookup"><span data-stu-id="1427d-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="1427d-109">Można rozważyć `CTAS` nadrzędne obciążona wersja `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="1427d-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="1427d-110">Poniżej przedstawiono przykładowy prostą `SELECT..INTO` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1427d-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="1427d-111">W powyższym przykładzie `[dbo].[FactInternetSales_new]` zostałyby utworzone ROUND_ROBIN rozproszonej tabeli z INDEKSEM magazynu kolumn w KLASTRZE na nim są one wartości domyślnych tabeli w magazynie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1427d-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="1427d-112">`SELECT..INTO`jednak nie umożliwiają zmianę metody dystrybucji lub typ indeksu jako część operacji.</span><span class="sxs-lookup"><span data-stu-id="1427d-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="1427d-113">Jest to, gdy `CTAS` polega na.</span><span class="sxs-lookup"><span data-stu-id="1427d-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="1427d-114">Aby przekonwertować powyżej, aby `CTAS` jest dość proste:</span><span class="sxs-lookup"><span data-stu-id="1427d-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="1427d-115">Z `CTAS` można zmienić dystrybucji dane w tabeli, a także z typem tabeli.</span><span class="sxs-lookup"><span data-stu-id="1427d-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="1427d-116">Jeśli tylko chcesz zmienić indeks w Twojej `CTAS` operacji i tabeli źródłowej są rozpowszechniane skrót, a następnie z `CTAS` operacji będzie wykonywać najlepiej, jeśli obsługa tego samego typu kolumny i danych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="1427d-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="1427d-117">Pozwoli to uniknąć cross przenoszenia danych dystrybucji podczas operacji, które jest bardziej wydajny.</span><span class="sxs-lookup"><span data-stu-id="1427d-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="1427d-118">Aby skopiować tabelę przy użyciu CTAS</span><span class="sxs-lookup"><span data-stu-id="1427d-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="1427d-119">Możliwe, że jedną z najbardziej typowych zastosowań `CTAS` jest tworzenie kopii tabeli, dzięki czemu można zmienić kod DDL.</span><span class="sxs-lookup"><span data-stu-id="1427d-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="1427d-120">Jeśli na przykład pierwotnie utworzona jako tabela `ROUND_ROBIN` , a teraz chcesz zmienić rozproszonych od kolumny, tabeli `CTAS` jest sposób należy zmienić kolumny dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="1427d-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="1427d-121">`CTAS`można również zmienić typy partycjonowania, indeksowania lub kolumny.</span><span class="sxs-lookup"><span data-stu-id="1427d-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="1427d-122">Załóżmy, że utworzono tej tabeli przy użyciu domyślnego typu dystrybucji `ROUND_ROBIN` rozproszonych, ponieważ kolumna nie dystrybucji została określona w `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="1427d-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="1427d-123">Teraz chcesz utworzyć nową kopię tej tabeli z indeksem magazynu kolumn w klastrze, tak, aby można było korzystać z wydajności tabel klastrowanego magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="1427d-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="1427d-124">Również dystrybuowania tej tabeli po klucz produktu, ponieważ są przewidywanie sprzężenia od tej kolumny i aby uniknąć przenoszenia danych podczas sprzężenia na klucz produktu.</span><span class="sxs-lookup"><span data-stu-id="1427d-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="1427d-125">Na koniec również chcesz dodać partycjonowania na OrderDateKey, dzięki czemu można szybko usunąć stare dane przez usunięcie starego partycji.</span><span class="sxs-lookup"><span data-stu-id="1427d-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="1427d-126">Oto instrukcji CTAS, które będzie skopiować starego tabeli do nowej tabeli.</span><span class="sxs-lookup"><span data-stu-id="1427d-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="1427d-127">Na koniec można zmienić nazwy tabel do wymiany w nowej tabeli, a następnie upuść starego tabeli.</span><span class="sxs-lookup"><span data-stu-id="1427d-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="1427d-128">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="1427d-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="1427d-129">W celu uzyskania najlepszej wydajności zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu danych, a następnie po każdej istotnej zmianie.</span><span class="sxs-lookup"><span data-stu-id="1427d-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="1427d-130">Szczegółowy opis statystyk znajduje się w temacie [Statystyki][Statistics] w grupie artykułów dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1427d-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="1427d-131">Aby obejść nieobsługiwanych funkcji przy użyciu CTAS</span><span class="sxs-lookup"><span data-stu-id="1427d-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="1427d-132">`CTAS`można również obejść liczba nieobsługiwanych funkcji wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="1427d-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="1427d-133">Można to często okazać się sytuacji win/win nie tylko kodzie będą zgodne, ale będą często wykonywane szybciej na magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="1427d-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="1427d-134">Jest to wyniku pełni zrównoleglone projekt.</span><span class="sxs-lookup"><span data-stu-id="1427d-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="1427d-135">Scenariusze, które można pracować z CTAS wokół obejmują:</span><span class="sxs-lookup"><span data-stu-id="1427d-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="1427d-136">SPRZĘŻENIA ANSI na aktualizacje</span><span class="sxs-lookup"><span data-stu-id="1427d-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="1427d-137">Sprzężenia ANSI na usuwaniu</span><span class="sxs-lookup"><span data-stu-id="1427d-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="1427d-138">MERGE — instrukcja</span><span class="sxs-lookup"><span data-stu-id="1427d-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="1427d-139">Pomyśl "CTAS pierwszy".</span><span class="sxs-lookup"><span data-stu-id="1427d-139">Try to think "CTAS first".</span></span> <span data-ttu-id="1427d-140">Jeśli uważasz, że uda się rozwiązać problem przy użyciu `CTAS` następnie jest zwykle najlepszym sposobem zbliżających się — nawet wtedy, gdy w związku z tym pisania większej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="1427d-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="1427d-141">ANSI zamienny sprzężenia dla instrukcji update</span><span class="sxs-lookup"><span data-stu-id="1427d-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="1427d-142">Może się okazać się, że masz złożonych aktualizacji, w której jest przyłączany więcej niż dwie tabele ze sobą przy użyciu ANSI dołączenie składni przeprowadzić UPDATE lub DELETE.</span><span class="sxs-lookup"><span data-stu-id="1427d-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="1427d-143">Załóżmy, że wymagał zaktualizowania tej tabeli:</span><span class="sxs-lookup"><span data-stu-id="1427d-143">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="1427d-144">Oryginalne zapytanie może sprawdzono podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="1427d-144">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="1427d-145">Ponieważ Magazyn danych SQL nie obsługuje ANSI sprzężenia w `FROM` klauzuli `UPDATE` instrukcji, nie można skopiować ten kod nad zmieniając nieco.</span><span class="sxs-lookup"><span data-stu-id="1427d-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="1427d-146">Można użyć kombinacji `CTAS` i niejawne sprzężenia, aby zastąpić ten kod:</span><span class="sxs-lookup"><span data-stu-id="1427d-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="1427d-147">Zastępuje sprzężenia ANSI usunąć — instrukcje</span><span class="sxs-lookup"><span data-stu-id="1427d-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="1427d-148">Czasami najlepszym rozwiązaniem związanych z usuwaniem danych jest użycie `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="1427d-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="1427d-149">Zamiast usuwania danych, po prostu zaznacz dane, które chcesz zachować.</span><span class="sxs-lookup"><span data-stu-id="1427d-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="1427d-150">To szczególnie istotne dla `DELETE` instrukcji używających ansi łącząca składni, ponieważ usługa SQL Data Warehouse nie obsługuje ANSI sprzężenia w `FROM` klauzuli `DELETE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="1427d-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="1427d-151">Przykład przekonwertowanego instrukcji DELETE jest dostępny poniżej:</span><span class="sxs-lookup"><span data-stu-id="1427d-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="1427d-152">Zastąp instrukcjach merge</span><span class="sxs-lookup"><span data-stu-id="1427d-152">Replace merge statements</span></span>
<span data-ttu-id="1427d-153">Instrukcje scalania można zastąpić, co najmniej w części, za pomocą `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="1427d-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="1427d-154">Można skonsolidować `INSERT` i `UPDATE` w jednej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="1427d-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="1427d-155">Rekordy usunięte musi być zamknięte w drugim instrukcji.</span><span class="sxs-lookup"><span data-stu-id="1427d-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="1427d-156">Przykład `UPSERT` znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="1427d-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="1427d-157">Zalecenie CTAS: jawnie określać typ danych i dopuszczanie wartości null dla danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="1427d-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="1427d-158">Podczas migrowania kod może się okazać, czy uruchomione przez ten typ kodowania wzorca:</span><span class="sxs-lookup"><span data-stu-id="1427d-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="1427d-159">Instynktownie może traktować, należy zainstalować ten kod CTAS, a użytkownik będzie poprawna.</span><span class="sxs-lookup"><span data-stu-id="1427d-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="1427d-160">Istnieje jednak jest ukrytym problem.</span><span class="sxs-lookup"><span data-stu-id="1427d-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="1427d-161">Następujący kod nie uzyskanie takiego samego wyniku:</span><span class="sxs-lookup"><span data-stu-id="1427d-161">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="1427d-162">Zwróć uwagę, kolumna "wynik" przenosi do przodu danych typu i dopuszczanie wartości null wartości wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="1427d-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="1427d-163">Może to prowadzić do niewielkie różnice w wartości, jeśli nie są dokładne.</span><span class="sxs-lookup"><span data-stu-id="1427d-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="1427d-164">Spróbuj wykonać następujące czynności, na przykład:</span><span class="sxs-lookup"><span data-stu-id="1427d-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="1427d-165">Wartość przechowywana dla wyniku jest inny.</span><span class="sxs-lookup"><span data-stu-id="1427d-165">The value stored for result is different.</span></span> <span data-ttu-id="1427d-166">Zgodnie z utrwalonego wartości w kolumnie wyników jest używana w innych wyrażeniach błąd staje się jeszcze bardziej znaczące.</span><span class="sxs-lookup"><span data-stu-id="1427d-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="1427d-167">Jest to szczególnie ważne w przypadku migracji danych.</span><span class="sxs-lookup"><span data-stu-id="1427d-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="1427d-168">Mimo że drugiego zapytania jest raczej dokładniejsze występuje problem.</span><span class="sxs-lookup"><span data-stu-id="1427d-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="1427d-169">Dane będą różne w porównaniu z systemem źródłowym i powodująca pytania integralności w procesie migracji.</span><span class="sxs-lookup"><span data-stu-id="1427d-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="1427d-170">Jest to jeden z tych rzadkich przypadkach, gdy "nieprawidłowe" odpowiedzi jest rzeczywiście właściwy!</span><span class="sxs-lookup"><span data-stu-id="1427d-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="1427d-171">Z powodu widzimy tej różnicy między dwoma wynikami jest do rzutowania typu niejawnego.</span><span class="sxs-lookup"><span data-stu-id="1427d-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="1427d-172">W pierwszym przykładzie tabela definiuje definicji kolumny.</span><span class="sxs-lookup"><span data-stu-id="1427d-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="1427d-173">Gdy zostanie wstawiona występuje niejawna konwersja typu.</span><span class="sxs-lookup"><span data-stu-id="1427d-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="1427d-174">W drugim przykładzie nie jest typu niejawna konwersja jako wyrażenie definiuje typ danych kolumny.</span><span class="sxs-lookup"><span data-stu-id="1427d-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="1427d-175">Należy zauważyć, że kolumny w drugim przykładzie została zdefiniowana jako kolumny wartości null należy w pierwszym przykładzie nie.</span><span class="sxs-lookup"><span data-stu-id="1427d-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="1427d-176">Podczas tworzenia tabeli w pierwszym dopuszczania wartości Null kolumny przykład został jawnie zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="1427d-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="1427d-177">W drugim przykładzie, który został właśnie pozostawiany wyrażeniu i domyślnie to spowoduje definicji wartości NULL.</span><span class="sxs-lookup"><span data-stu-id="1427d-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="1427d-178">Aby rozwiązać te problemy należy jawnie ustawić konwersji typu i dopuszczanie wartości null w `SELECT` część `CTAS` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="1427d-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="1427d-179">Te właściwości nie można ustawić w części Tworzenie tabeli.</span><span class="sxs-lookup"><span data-stu-id="1427d-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="1427d-180">W poniższym przykładzie pokazano, jak poprawić kod:</span><span class="sxs-lookup"><span data-stu-id="1427d-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="1427d-181">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="1427d-181">Note the following:</span></span>

* <span data-ttu-id="1427d-182">CAST lub CONVERT może zostały już użyte</span><span class="sxs-lookup"><span data-stu-id="1427d-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="1427d-183">Można wymusić dopuszczania wartości null nie ŁĄCZONEJ ISNULL</span><span class="sxs-lookup"><span data-stu-id="1427d-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="1427d-184">ISNULL jest najbardziej zewnętrzną funkcję</span><span class="sxs-lookup"><span data-stu-id="1427d-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="1427d-185">Druga część ISNULL jest stałą tj. 0</span><span class="sxs-lookup"><span data-stu-id="1427d-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="1427d-186">Dla dopuszczania wartości null poprawnie można ustawić jest niezbędne do używania `ISNULL` i nie `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="1427d-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="1427d-187">`COALESCE`nie jest deterministyczna funkcji i dlatego wynikiem wyrażenia zawsze będzie NULLable.</span><span class="sxs-lookup"><span data-stu-id="1427d-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="1427d-188">`ISNULL`różni się.</span><span class="sxs-lookup"><span data-stu-id="1427d-188">`ISNULL` is different.</span></span> <span data-ttu-id="1427d-189">Jest ona deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="1427d-189">It is deterministic.</span></span> <span data-ttu-id="1427d-190">W związku z tym po drugiej części `ISNULL` funkcja jest stałą lub literałem, a następnie będzie wynikowej wartości NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="1427d-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="1427d-191">Tej porady nie jest przydatne tylko w celu zapewnienia integralności obliczeń.</span><span class="sxs-lookup"><span data-stu-id="1427d-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="1427d-192">Należy również do przełączenia partycji tabeli.</span><span class="sxs-lookup"><span data-stu-id="1427d-192">It is also important for table partition switching.</span></span> <span data-ttu-id="1427d-193">Załóżmy, że w tej tabeli zdefiniowany jako Twoje fakt:</span><span class="sxs-lookup"><span data-stu-id="1427d-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="1427d-194">Jednak w polu wartość jest wyrażenie obliczeniowej nie jest on częścią źródła danych.</span><span class="sxs-lookup"><span data-stu-id="1427d-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="1427d-195">Aby utworzyć partycjonowanej zestawu danych może być w tym celu:</span><span class="sxs-lookup"><span data-stu-id="1427d-195">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="1427d-196">Zapytanie może działać dokładnie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="1427d-196">The query would run perfectly fine.</span></span> <span data-ttu-id="1427d-197">Problem jest dostarczany podczas próby wykonania przełącznik partycji.</span><span class="sxs-lookup"><span data-stu-id="1427d-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="1427d-198">Definicje tabel są zgodne.</span><span class="sxs-lookup"><span data-stu-id="1427d-198">The table definitions do not match.</span></span> <span data-ttu-id="1427d-199">Aby definicji tabeli, zgodna CTAS ma zostać zmodyfikowana.</span><span class="sxs-lookup"><span data-stu-id="1427d-199">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="1427d-200">Widać w związku z tym, że typ spójności i utrzymywanie właściwości dopuszczania wartości null na CTAS dobrej engineering najlepszym rozwiązaniem jest.</span><span class="sxs-lookup"><span data-stu-id="1427d-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="1427d-201">Umożliwia zachowanie spójności w obliczeniach, a także zapewnia, że możliwe jest przełączanie partycji.</span><span class="sxs-lookup"><span data-stu-id="1427d-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="1427d-202">Zapoznaj się z subskrypcją MSDN, aby uzyskać więcej informacji na temat używania [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="1427d-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="1427d-203">Jest jednym z najważniejszych instrukcje w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1427d-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1427d-204">Upewnij się, że rozumiesz dokładnie.</span><span class="sxs-lookup"><span data-stu-id="1427d-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1427d-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1427d-205">Next steps</span></span>
<span data-ttu-id="1427d-206">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="1427d-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
