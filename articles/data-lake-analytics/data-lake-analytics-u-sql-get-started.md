---
title: "Wprowadzenie do języka U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawy hello języka U-SQL."
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>Wprowadzenie do języka U-SQL
U-SQL jest językiem, który łączy deklaratywne SQL z natury C# toolet przetwarzania danych w dowolnej skali. Za pomocą hello skalowalnych, rozproszonych zapytania możliwości U-SQL można efektywne analizowanie danych w sklepach relacyjne, takie jak bazy danych SQL Azure. Języku U-SQL może przetwarzać danych niestrukturalnych przy zastosowaniu schematu na odczyt i wstawianie niestandardowej logiki i funkcji UDF. Ponadto U-SQL obejmuje rozszerzalności, który zapewnia precyzyjną kontrolę nad jak tooexecute na dużą skalę. 

## <a name="learning-resources"></a>Materiałów szkoleniowych

* Witaj [samouczek U-SQL](http://aka.ms/usqltutorial) zawiera przewodnik krok po kroku większości języka hello U-SQL. Ten dokument jest zalecane odczytu dla wszystkich deweloperów pożądane toolearn U-SQL.
* Aby uzyskać szczegółowe informacje o hello **składni języka U-SQL**, zobacz hello [dokumentację języka U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* Witaj toounderstand **zasady projektowania klas U-SQL**, zobacz Visual Studio blogu hello [wprowadzenie do języka U-SQL — A język, który ułatwia Big przetwarzania danych](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Wymagania wstępne

Przed przejściem przez przykłady hello U-SQL w tym dokumencie, odczytu i wykonania [samouczek: skrypty opracowanie U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Ten samouczek wyjaśnia sposób mechanika hello przy użyciu języka U-SQL z usługi Azure Data Lake Tools dla programu Visual Studio.

## <a name="your-first-u-sql-script"></a>Pierwszy skrypt U-SQL

Witaj następującego skryptu U-SQL jest prosta i ułatwiają badanie wiele aspektów hello U-SQL języka.

```
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

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

Ten skrypt nie ma żadnych kroków transformacji. Odczytuje z pliku źródłowego hello o nazwie `SearchLog.tsv`schematizes go i ponownie zapisuje hello wierszy w pliku o nazwie SearchLog pierwszej u-sql.csv.

Zwróć uwagę, hello znaku zapytania dalej toohello typ danych w hello `Duration` pola. Oznacza to, że hello `Duration` pole może mieć wartości null.

### <a name="key-concepts"></a>Kluczowe pojęcia
* **Zestaw wierszy zmiennych**: każde wyrażenie zapytania, który spowoduje utworzenie zestawu wierszy można przypisać zmiennej tooa. U-SQL następuje hello T-SQL variable — wzorzec nazewnictwa (`@searchlog`, na przykład) w skrypcie hello.
* Witaj **WYODRĘBNIĆ** — słowo kluczowe odczytywać dane z pliku i definiuje schemat hello na odczyt. `Extractors.Tsv`jest wbudowane ekstraktor U-SQL dla plików kartę wartości rozdzielanych przecinkami. Można tworzyć niestandardowe ekstraktory.
* Witaj **dane wyjściowe** zapisuje dane z pliku tooa zestawu wierszy. `Outputters.Csv()`jest to plik przecinkami wartości rozdzielanych przecinkami wbudowanych toocreate outputter U-SQL. Można tworzyć niestandardowe outputters.

### <a name="file-paths"></a>Ścieżki do plików

Hello WYODRĘBNIANIA i danych wyjściowych instrukcji należy użyć ścieżki do pliku. Ścieżki plików może być bezwzględny lub względny:

Plik tooa w usłudze Data Lake Store o nazwie odwołuje się ten następująca ścieżka bezwzględna do pliku `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

Rozpoczyna się od tego następująca ścieżka pliku `"/"`. Odwołuje się plik tooa w hello domyślnego konta usługi Data Lake Store:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Użyj zmienne skalara

Można używać skalarne zmiennych jako dobrze toomake Twojego skryptu konserwacji łatwiejsze. poprzedni skrypt U-SQL Hello również może być zapisany jako:

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>Przekształć zestawy wierszy

Użyj **wybierz** tootransform zestawów wierszy:

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

Witaj, używa klauzuli WHERE [C# logicznego wyrażenia](https://msdn.microsoft.com/library/6a71f45d.aspx). Witaj C# wyrażenia języka toodo można użyć własnych wyrażeń i funkcji. Można nawet wykonywać bardziej złożone filtrowanie łącząc je z spójników logiczne (i) i disjunctions (ORs).

Witaj poniższy skrypt używa metody DateTime.Parse() hello i połączeniu.

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >wynik hello hello pierwszy zestaw wierszy, który tworzy dwa filtry złożone hello działające Hello drugiego zapytania. Można również użyć ponownie nazwę zmiennej, a nazwy hello lexically ograniczone.

## <a name="aggregate-rowsets"></a>Łączny zestawy wierszy
U-SQL umożliwia hello znanych ORDER BY, GROUP BY i agregacji.

Hello następujące zapytanie znajdzie hello całkowity czas trwania na region, a następnie wyświetla hello top pięciu wartości czasu trwania w kolejności.

Zestawy wierszy U-SQL nie zachowuj ich kolejność hello dalej zapytania. W związku z tym tooorder jako dane wyjściowe, należy tooadd ORDER BY toohello danych wyjściowych instrukcji:

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

klauzuli U-SQL ORDER BY Hello wymaga przy użyciu klauzuli FETCH hello w wyrażeniu SELECT.

Klauzula o języku U-SQL Hello może być używane toorestrict hello dane wyjściowe toogroups, które spełniają warunek HAVING hello:

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Scenariusze zaawansowane agregacji, można znaleźć w dokumentacji odwołanie hello U-SQL hello [agregacji, analitycznych i referencyjne funkcji](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
