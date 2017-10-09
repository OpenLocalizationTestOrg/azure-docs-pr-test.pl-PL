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
# <a name="group-by-options-in-sql-data-warehouse"></a>Grupuj według opcje w usłudze SQL Data Warehouse
Witaj [GROUP BY] [ GROUP BY] jest używana klauzula tooaggregate danych tooa podsumowania zestawu wierszy. Ma również kilka opcji rozszerzające jego funkcjonalność tego toobe potrzeby działał wokół, ponieważ nie są bezpośrednio obsługiwane przez Magazyn danych SQL Azure.

Te opcje są

* GROUP BY z pakietem ZBIORCZYM
* GROUPING SETS
* Klauzula GROUP BY modułu

## <a name="rollup-and-grouping-sets-options"></a>Ustawia opcje ROLLUP i grouping
Witaj najprostsza opcja tutaj jest toouse `UNION ALL` zamiast tego pakiet zbiorczy hello tooperform zamiast polegania na hello jawnej składni. wynik Hello jest hello dokładnie tego samego

Poniżej znajduje się przykład grupy przez instrukcję, używając hello `ROLLUP` opcji:

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

Za pomocą pakietu ZBIORCZEGO żądanych firma Microsoft hello po agregacji:

* Kraj lub Region
* Kraj
* Całkowita suma

tooreplace to należy toouse `UNION ALL`; Określanie agregacji hello wymagane jawnie tooreturn hello takie same wyniki:

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

GROUPING SETS potrzebujemy toodo jest przyjąć hello sama główna, lecz tylko utworzyć sekcje UNION ALL dla hello poziomy agregacji chcemy toosee

## <a name="cube-options"></a>Opcje modułu
Jest możliwe toocreate GROUP BY WITH CUBE hello podejście UNION ALL. Hello problem jest, że kod hello może szybko stać się skomplikowane i niewygodna. toomitigate to możesz użyć tej funkcji bardziej zaawansowane metody.

Użyjmy przykład Witaj powyżej.

pierwszym krokiem Hello jest hello toodefine modułu, który definiuje wszystkie poziomy hello agregacji, że chcemy toocreate. Jest ważne tootake należy wziąć pod uwagę hello CROSS JOIN hello dwóch tabel pochodnych. Spowoduje to wygenerowanie wszystkie poziomy hello firmie Microsoft. rest Hello kodu hello jest naprawdę formatowania.

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

wyniki Hello hello CTAS są widoczne poniżej:

![][1]

drugim krokiem Hello jest toospecify przejściowej toostore tabeli docelowej w wynikach:

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

trzeci krok Hello jest tooloop za pośrednictwem naszego modułu wykonywania agregacji hello kolumn. Zapytanie Hello zostaną uruchomione jeden raz dla każdego wiersza w tabeli tymczasowej hello #Cube i przechowywać wyniki hello w tabeli tymczasowej hello #Results

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

Na koniec zostanie zwrócona wyniki hello odczytując po prostu z tabeli tymczasowej hello #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Przez podzielenie kodu hello sekcje i generowania pętli hello konstrukcji kodu staje się bardziej łatwe w zarządzaniu i łatwy w obsłudze.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
