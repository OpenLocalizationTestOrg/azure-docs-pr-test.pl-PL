---
title: "Grupuj według opcje w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="74f34-103">Grupuj według opcje w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="74f34-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="74f34-104">[GROUP BY] [ GROUP BY] jest używana do agregowania danych podsumowania zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="74f34-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="74f34-105">Ma również kilka opcji, które rozszerzają jego funkcjonalność konieczne działał wokół, ponieważ nie są bezpośrednio obsługiwane przez Magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="74f34-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="74f34-106">Te opcje są</span><span class="sxs-lookup"><span data-stu-id="74f34-106">These options are</span></span>

* <span data-ttu-id="74f34-107">GROUP BY z pakietem ZBIORCZYM</span><span class="sxs-lookup"><span data-stu-id="74f34-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="74f34-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="74f34-108">GROUPING SETS</span></span>
* <span data-ttu-id="74f34-109">Klauzula GROUP BY modułu</span><span class="sxs-lookup"><span data-stu-id="74f34-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="74f34-110">Ustawia opcje ROLLUP i grouping</span><span class="sxs-lookup"><span data-stu-id="74f34-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="74f34-111">Jest to najprostsza opcja używania `UNION ALL` zamiast tego przeprowadzić pakiet zbiorczy zamiast polegania na jawnej składni.</span><span class="sxs-lookup"><span data-stu-id="74f34-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="74f34-112">Wynik jest dokładnie taka sama</span><span class="sxs-lookup"><span data-stu-id="74f34-112">The result is exactly the same</span></span>

<span data-ttu-id="74f34-113">Poniżej znajduje się przykład grupy za pomocą instrukcji `ROLLUP` opcji:</span><span class="sxs-lookup"><span data-stu-id="74f34-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

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

<span data-ttu-id="74f34-114">Za pomocą pakietu ZBIORCZEGO możemy żądanych agregacji następujące:</span><span class="sxs-lookup"><span data-stu-id="74f34-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="74f34-115">Kraj lub Region</span><span class="sxs-lookup"><span data-stu-id="74f34-115">Country and Region</span></span>
* <span data-ttu-id="74f34-116">Kraj</span><span class="sxs-lookup"><span data-stu-id="74f34-116">Country</span></span>
* <span data-ttu-id="74f34-117">Całkowita suma</span><span class="sxs-lookup"><span data-stu-id="74f34-117">Grand Total</span></span>

<span data-ttu-id="74f34-118">Aby zamienić to będą musieli używać `UNION ALL`; Określanie agregacji jawnie muszą zwracać takie same wyniki:</span><span class="sxs-lookup"><span data-stu-id="74f34-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

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

<span data-ttu-id="74f34-119">GROUPING SETS wszystkie konieczne jest przyjąć tej samej nazwy głównej, ale tylko utworzyć UNION ALL sekcjach poziomów agregacji, które chcesz zobaczyć</span><span class="sxs-lookup"><span data-stu-id="74f34-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="74f34-120">Opcje modułu</span><span class="sxs-lookup"><span data-stu-id="74f34-120">Cube options</span></span>
<span data-ttu-id="74f34-121">Istnieje możliwość utworzenia grupy przez z modułu przy użyciu podejścia UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="74f34-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="74f34-122">Problem polega na tym, że kod może szybko stać się skomplikowane i niewygodna.</span><span class="sxs-lookup"><span data-stu-id="74f34-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="74f34-123">Aby temu zaradzić możesz użyć tego bardziej zaawansowane metody.</span><span class="sxs-lookup"><span data-stu-id="74f34-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="74f34-124">Użyjmy w powyższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="74f34-124">Let's use the example above.</span></span>

<span data-ttu-id="74f34-125">Pierwszym krokiem jest określenie "module" definiujący wszystkie poziomy agregacji, jeśli chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="74f34-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="74f34-126">Należy pamiętać o CROSS JOIN dwóch tabel pochodnych.</span><span class="sxs-lookup"><span data-stu-id="74f34-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="74f34-127">Spowoduje to wygenerowanie wszystkie poziomy firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74f34-127">This generates all the levels for us.</span></span> <span data-ttu-id="74f34-128">Pozostała część kodu jest naprawdę formatowania.</span><span class="sxs-lookup"><span data-stu-id="74f34-128">The rest of the code is really there for formatting.</span></span>

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

<span data-ttu-id="74f34-129">Wyniki CTAS są widoczne poniżej:</span><span class="sxs-lookup"><span data-stu-id="74f34-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="74f34-130">Drugim krokiem jest określenie tabeli docelowej do przechowywania wyników pośrednich:</span><span class="sxs-lookup"><span data-stu-id="74f34-130">The second step is to specify a target table to store interim results:</span></span>

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

<span data-ttu-id="74f34-131">Trzeci krok ma pętlę naszych modułu wykonywania agregacji kolumn.</span><span class="sxs-lookup"><span data-stu-id="74f34-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="74f34-132">Zapytanie zostanie uruchomione jeden raz dla każdego wiersza w tabeli tymczasowej #Cube i zapisać wyniki w tabeli tymczasowej #Results</span><span class="sxs-lookup"><span data-stu-id="74f34-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

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

<span data-ttu-id="74f34-133">Na koniec zostanie zwrócona po prostu przeczytaj z tabeli tymczasowej #Results wyników</span><span class="sxs-lookup"><span data-stu-id="74f34-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="74f34-134">Przez podzielenie kod na sekcje i generowanie konstrukcji pętli kodu staje się bardziej łatwe w zarządzaniu i łatwy w obsłudze.</span><span class="sxs-lookup"><span data-stu-id="74f34-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74f34-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74f34-135">Next steps</span></span>
<span data-ttu-id="74f34-136">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="74f34-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
