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
# <a name="get-started-with-hello-u-sql-catalog"></a>Rozpoczynanie pracy z hello katalogu U-SQL

## <a name="create-a-tvf"></a>Tworzenie funkcji TVF

W poprzednich skryptu U-SQL hello powtarzany hello stosowania tooread WYODRĘBNIANIA z hello tego samego pliku źródłowego. Z hello U-SQL funkcji zwracającej tabelę (TVF) umożliwiająca Hermetyzowanie hello danych w celu wykorzystania w przyszłości.  

Witaj poniższy skrypt tworzy funkcji TVF o nazwie `Searchlog()` hello domyślnej bazy danych i schematu:

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

Witaj następującego skryptu pokazuje, jak toouse hello funkcji TVF, która została zdefiniowana w skrypcie poprzedniej hello:

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

## <a name="create-views"></a>Tworzenie widoków

Jeśli masz wyrażenia jednego zapytania, zamiast funkcji TVF możesz użyć tooencapsulate U-SQL WIDOKU tego wyrażenia.

Witaj poniższy skrypt tworzy widok o nazwie `SearchlogView` hello domyślnej bazy danych i schematu:

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

Hello następującego skryptu przedstawiono użycie hello hello definicja widoku:

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

## <a name="create-tables"></a>Tworzenie tabel
Zgodnie z tabelami relacyjnej bazy danych z U-SQL można utworzyć tabelę z wstępnie zdefiniowanych schematów lub utworzyć tabelę, która wnioskuje schemat hello hello zapytania, które wypełnia tabelę hello (znanej także jako CREATE TABLE AS SELECT lub CTAS).

Utwórz bazę danych i tabel za pomocą hello następującego skryptu:

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

## <a name="query-tables"></a>Tabele kwerendy
Można zbadać tabelami, takie jak te utworzone w poprzednim skryptu hello w hello wykonywania zapytań hello danych plików tak samo. Zamiast tworzenia zestawu wierszy za pomocą WYODRĘBNIANIA, teraz można się odwołać toohello nazwy tabeli.

tooread z tabel hello zmodyfikować skrypt transformacji hello, wcześniej używany:

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
 >Obecnie nie można uruchomić SELECT w tabeli w hello sam skrypt jako jeden hello, w którym utworzono hello tabeli.

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
