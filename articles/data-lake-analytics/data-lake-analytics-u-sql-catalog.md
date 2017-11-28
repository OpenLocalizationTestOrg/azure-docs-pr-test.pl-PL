---
title: Rozpoczynanie pracy z katalogu U-SQL | Dokumentacja firmy Microsoft
description: "Informacje o sposobie korzystania z katalogu U-SQL do udostępniania kodu i danych."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="e8458-103">Rozpoczynanie pracy z katalogu U-SQL</span><span class="sxs-lookup"><span data-stu-id="e8458-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="e8458-104">Tworzenie funkcji TVF</span><span class="sxs-lookup"><span data-stu-id="e8458-104">Create a TVF</span></span>

<span data-ttu-id="e8458-105">W poprzednich skryptu U-SQL powtarza się użycie WYODRĘBNIANIA do odczytu z tego samego pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="e8458-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="e8458-106">Funkcją U-SQL zwracającej tabelę (TVF) umożliwiająca Hermetyzowanie danych w celu wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="e8458-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="e8458-107">Poniższy skrypt tworzy funkcji TVF o nazwie `Searchlog()` w domyślnej bazy danych i schemat:</span><span class="sxs-lookup"><span data-stu-id="e8458-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

<span data-ttu-id="e8458-108">Poniższy skrypt pokazuje, jak używać funkcji TVF zdefiniowanego w poprzedniej skryptu:</span><span class="sxs-lookup"><span data-stu-id="e8458-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="e8458-109">Tworzenie widoków</span><span class="sxs-lookup"><span data-stu-id="e8458-109">Create views</span></span>

<span data-ttu-id="e8458-110">Jeśli masz wyrażenia jednego zapytania, zamiast funkcji TVF możesz użyć WIDOKU U-SQL hermetyzacji tego wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="e8458-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="e8458-111">Poniższy skrypt tworzy widok o nazwie `SearchlogView` w domyślnej bazy danych i schemat:</span><span class="sxs-lookup"><span data-stu-id="e8458-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="e8458-112">Poniższy skrypt pokazuje użycie zdefiniowano widoku:</span><span class="sxs-lookup"><span data-stu-id="e8458-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="e8458-113">Tworzenie tabel</span><span class="sxs-lookup"><span data-stu-id="e8458-113">Create tables</span></span>
<span data-ttu-id="e8458-114">Zgodnie z tabelami relacyjnej bazy danych z U-SQL można utworzyć tabelę z wstępnie zdefiniowanych schematów lub utworzyć tabelę, która wnioskuje schemat z kwerendy, który wypełnia tabeli (znanej także jako CREATE TABLE AS SELECT lub CTAS).</span><span class="sxs-lookup"><span data-stu-id="e8458-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="e8458-115">Utwórz bazę danych i tabel za pomocą następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="e8458-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="e8458-116">Tabele kwerendy</span><span class="sxs-lookup"><span data-stu-id="e8458-116">Query tables</span></span>
<span data-ttu-id="e8458-117">Umożliwia wysyłanie zapytań tabel, takich jak te utworzone w poprzednim skryptu w taki sam sposób wykonywania zapytań plików danych.</span><span class="sxs-lookup"><span data-stu-id="e8458-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="e8458-118">Zamiast tworzenia zestawu wierszy za pomocą WYODRĘBNIANIA, możesz teraz mogą odwoływać się do nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="e8458-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="e8458-119">Aby odczytać z tabel, zmodyfikuj skrypt transformacji wcześniej używany:</span><span class="sxs-lookup"><span data-stu-id="e8458-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="e8458-120">Obecnie nie można uruchomić SELECT w tabeli w tym samym skrypcie, której utworzono tabelę.</span><span class="sxs-lookup"><span data-stu-id="e8458-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8458-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8458-121">Next Steps</span></span>
* [<span data-ttu-id="e8458-122">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e8458-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="e8458-123">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8458-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="e8458-124">Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e8458-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
