---
title: Rozpoczynanie pracy z katalogu hello U-SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak hello toouse U-SQL w katalogu tooshare kodu i danych."
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
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="41c6a-103">Rozpoczynanie pracy z hello katalogu U-SQL</span><span class="sxs-lookup"><span data-stu-id="41c6a-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="41c6a-104">Tworzenie funkcji TVF</span><span class="sxs-lookup"><span data-stu-id="41c6a-104">Create a TVF</span></span>

<span data-ttu-id="41c6a-105">W poprzednich skryptu U-SQL hello powtarzany hello stosowania tooread WYODRĘBNIANIA z hello tego samego pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="41c6a-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="41c6a-106">Z hello U-SQL funkcji zwracającej tabelę (TVF) umożliwiająca Hermetyzowanie hello danych w celu wykorzystania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="41c6a-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="41c6a-107">Witaj poniższy skrypt tworzy funkcji TVF o nazwie `Searchlog()` hello domyślnej bazy danych i schematu:</span><span class="sxs-lookup"><span data-stu-id="41c6a-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="41c6a-108">Witaj następującego skryptu pokazuje, jak toouse hello funkcji TVF, która została zdefiniowana w skrypcie poprzedniej hello:</span><span class="sxs-lookup"><span data-stu-id="41c6a-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="41c6a-109">Tworzenie widoków</span><span class="sxs-lookup"><span data-stu-id="41c6a-109">Create views</span></span>

<span data-ttu-id="41c6a-110">Jeśli masz wyrażenia jednego zapytania, zamiast funkcji TVF możesz użyć tooencapsulate U-SQL WIDOKU tego wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="41c6a-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="41c6a-111">Witaj poniższy skrypt tworzy widok o nazwie `SearchlogView` hello domyślnej bazy danych i schematu:</span><span class="sxs-lookup"><span data-stu-id="41c6a-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="41c6a-112">Hello następującego skryptu przedstawiono użycie hello hello definicja widoku:</span><span class="sxs-lookup"><span data-stu-id="41c6a-112">hello following script demonstrates hello use of hello defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="41c6a-113">Tworzenie tabel</span><span class="sxs-lookup"><span data-stu-id="41c6a-113">Create tables</span></span>
<span data-ttu-id="41c6a-114">Zgodnie z tabelami relacyjnej bazy danych z U-SQL można utworzyć tabelę z wstępnie zdefiniowanych schematów lub utworzyć tabelę, która wnioskuje schemat hello hello zapytania, które wypełnia tabelę hello (znanej także jako CREATE TABLE AS SELECT lub CTAS).</span><span class="sxs-lookup"><span data-stu-id="41c6a-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="41c6a-115">Utwórz bazę danych i tabel za pomocą hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="41c6a-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="41c6a-116">Tabele kwerendy</span><span class="sxs-lookup"><span data-stu-id="41c6a-116">Query tables</span></span>
<span data-ttu-id="41c6a-117">Można zbadać tabelami, takie jak te utworzone w poprzednim skryptu hello w hello wykonywania zapytań hello danych plików tak samo.</span><span class="sxs-lookup"><span data-stu-id="41c6a-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="41c6a-118">Zamiast tworzenia zestawu wierszy za pomocą WYODRĘBNIANIA, teraz można się odwołać toohello nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="41c6a-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="41c6a-119">tooread z tabel hello zmodyfikować skrypt transformacji hello, wcześniej używany:</span><span class="sxs-lookup"><span data-stu-id="41c6a-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="41c6a-120">Obecnie nie można uruchomić SELECT w tabeli w hello sam skrypt jako jeden hello, w którym utworzono hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="41c6a-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41c6a-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41c6a-121">Next Steps</span></span>
* [<span data-ttu-id="41c6a-122">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="41c6a-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="41c6a-123">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="41c6a-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="41c6a-124">Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="41c6a-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
