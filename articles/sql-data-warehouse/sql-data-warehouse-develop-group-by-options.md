---
title: "aaaGroup opcje w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące implementowania grupy Opcje w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="ade08-103">Grupuj według opcje w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ade08-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="ade08-104">Witaj [GROUP BY] [ GROUP BY] jest używana klauzula tooaggregate danych tooa podsumowania zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="ade08-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="ade08-105">Ma również kilka opcji rozszerzające jego funkcjonalność tego toobe potrzeby działał wokół, ponieważ nie są bezpośrednio obsługiwane przez Magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ade08-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="ade08-106">Te opcje są</span><span class="sxs-lookup"><span data-stu-id="ade08-106">These options are</span></span>

* <span data-ttu-id="ade08-107">GROUP BY z pakietem ZBIORCZYM</span><span class="sxs-lookup"><span data-stu-id="ade08-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="ade08-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="ade08-108">GROUPING SETS</span></span>
* <span data-ttu-id="ade08-109">Klauzula GROUP BY modułu</span><span class="sxs-lookup"><span data-stu-id="ade08-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="ade08-110">Ustawia opcje ROLLUP i grouping</span><span class="sxs-lookup"><span data-stu-id="ade08-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="ade08-111">Witaj najprostsza opcja tutaj jest toouse `UNION ALL` zamiast tego pakiet zbiorczy hello tooperform zamiast polegania na hello jawnej składni.</span><span class="sxs-lookup"><span data-stu-id="ade08-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="ade08-112">wynik Hello jest hello dokładnie tego samego</span><span class="sxs-lookup"><span data-stu-id="ade08-112">hello result is exactly hello same</span></span>

<span data-ttu-id="ade08-113">Poniżej znajduje się przykład grupy przez instrukcję, używając hello `ROLLUP` opcji:</span><span class="sxs-lookup"><span data-stu-id="ade08-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="ade08-114">Za pomocą pakietu ZBIORCZEGO żądanych firma Microsoft hello po agregacji:</span><span class="sxs-lookup"><span data-stu-id="ade08-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="ade08-115">Kraj lub Region</span><span class="sxs-lookup"><span data-stu-id="ade08-115">Country and Region</span></span>
* <span data-ttu-id="ade08-116">Kraj</span><span class="sxs-lookup"><span data-stu-id="ade08-116">Country</span></span>
* <span data-ttu-id="ade08-117">Całkowita suma</span><span class="sxs-lookup"><span data-stu-id="ade08-117">Grand Total</span></span>

<span data-ttu-id="ade08-118">tooreplace to należy toouse `UNION ALL`; Określanie agregacji hello wymagane jawnie tooreturn hello takie same wyniki:</span><span class="sxs-lookup"><span data-stu-id="ade08-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="ade08-119">GROUPING SETS potrzebujemy toodo jest przyjąć hello sama główna, lecz tylko utworzyć sekcje UNION ALL dla hello poziomy agregacji chcemy toosee</span><span class="sxs-lookup"><span data-stu-id="ade08-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="ade08-120">Opcje modułu</span><span class="sxs-lookup"><span data-stu-id="ade08-120">Cube options</span></span>
<span data-ttu-id="ade08-121">Jest możliwe toocreate GROUP BY WITH CUBE hello podejście UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="ade08-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="ade08-122">Hello problem jest, że kod hello może szybko stać się skomplikowane i niewygodna.</span><span class="sxs-lookup"><span data-stu-id="ade08-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="ade08-123">toomitigate to możesz użyć tej funkcji bardziej zaawansowane metody.</span><span class="sxs-lookup"><span data-stu-id="ade08-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="ade08-124">Użyjmy przykład Witaj powyżej.</span><span class="sxs-lookup"><span data-stu-id="ade08-124">Let's use hello example above.</span></span>

<span data-ttu-id="ade08-125">pierwszym krokiem Hello jest hello toodefine modułu, który definiuje wszystkie poziomy hello agregacji, że chcemy toocreate.</span><span class="sxs-lookup"><span data-stu-id="ade08-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="ade08-126">Jest ważne tootake należy wziąć pod uwagę hello CROSS JOIN hello dwóch tabel pochodnych.</span><span class="sxs-lookup"><span data-stu-id="ade08-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="ade08-127">Spowoduje to wygenerowanie wszystkie poziomy hello firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ade08-127">This generates all hello levels for us.</span></span> <span data-ttu-id="ade08-128">rest Hello kodu hello jest naprawdę formatowania.</span><span class="sxs-lookup"><span data-stu-id="ade08-128">hello rest of hello code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="ade08-129">wyniki Hello hello CTAS są widoczne poniżej:</span><span class="sxs-lookup"><span data-stu-id="ade08-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="ade08-130">drugim krokiem Hello jest toospecify przejściowej toostore tabeli docelowej w wynikach:</span><span class="sxs-lookup"><span data-stu-id="ade08-130">hello second step is toospecify a target table toostore interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="ade08-131">trzeci krok Hello jest tooloop za pośrednictwem naszego modułu wykonywania agregacji hello kolumn.</span><span class="sxs-lookup"><span data-stu-id="ade08-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="ade08-132">Zapytanie Hello zostaną uruchomione jeden raz dla każdego wiersza w tabeli tymczasowej hello #Cube i przechowywać wyniki hello w tabeli tymczasowej hello #Results</span><span class="sxs-lookup"><span data-stu-id="ade08-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="ade08-133">Na koniec zostanie zwrócona wyniki hello odczytując po prostu z tabeli tymczasowej hello #Results</span><span class="sxs-lookup"><span data-stu-id="ade08-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="ade08-134">Przez podzielenie kodu hello sekcje i generowania pętli hello konstrukcji kodu staje się bardziej łatwe w zarządzaniu i łatwy w obsłudze.</span><span class="sxs-lookup"><span data-stu-id="ade08-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ade08-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ade08-135">Next steps</span></span>
<span data-ttu-id="ade08-136">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="ade08-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
