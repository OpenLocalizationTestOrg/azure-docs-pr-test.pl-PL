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
# <a name="get-started-with-u-sql"></a><span data-ttu-id="4326a-103">Wprowadzenie do języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="4326a-103">Get started with U-SQL</span></span>
<span data-ttu-id="4326a-104">U-SQL jest językiem, który łączy deklaratywne SQL z natury C# toolet przetwarzania danych w dowolnej skali.</span><span class="sxs-lookup"><span data-stu-id="4326a-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="4326a-105">Za pomocą hello skalowalnych, rozproszonych zapytania możliwości U-SQL można efektywne analizowanie danych w sklepach relacyjne, takie jak bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4326a-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="4326a-106">Języku U-SQL może przetwarzać danych niestrukturalnych przy zastosowaniu schematu na odczyt i wstawianie niestandardowej logiki i funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="4326a-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="4326a-107">Ponadto U-SQL obejmuje rozszerzalności, który zapewnia precyzyjną kontrolę nad jak tooexecute na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="4326a-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="4326a-108">Materiałów szkoleniowych</span><span class="sxs-lookup"><span data-stu-id="4326a-108">Learning resources</span></span>

* <span data-ttu-id="4326a-109">Witaj [samouczek U-SQL](http://aka.ms/usqltutorial) zawiera przewodnik krok po kroku większości języka hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4326a-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="4326a-110">Ten dokument jest zalecane odczytu dla wszystkich deweloperów pożądane toolearn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4326a-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="4326a-111">Aby uzyskać szczegółowe informacje o hello **składni języka U-SQL**, zobacz hello [dokumentację języka U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="4326a-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="4326a-112">Witaj toounderstand **zasady projektowania klas U-SQL**, zobacz Visual Studio blogu hello [wprowadzenie do języka U-SQL — A język, który ułatwia Big przetwarzania danych](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="4326a-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4326a-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4326a-113">Prerequisites</span></span>

<span data-ttu-id="4326a-114">Przed przejściem przez przykłady hello U-SQL w tym dokumencie, odczytu i wykonania [samouczek: skrypty opracowanie U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4326a-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="4326a-115">Ten samouczek wyjaśnia sposób mechanika hello przy użyciu języka U-SQL z usługi Azure Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4326a-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="4326a-116">Pierwszy skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="4326a-116">Your first U-SQL script</span></span>

<span data-ttu-id="4326a-117">Witaj następującego skryptu U-SQL jest prosta i ułatwiają badanie wiele aspektów hello U-SQL języka.</span><span class="sxs-lookup"><span data-stu-id="4326a-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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

<span data-ttu-id="4326a-118">Ten skrypt nie ma żadnych kroków transformacji.</span><span class="sxs-lookup"><span data-stu-id="4326a-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="4326a-119">Odczytuje z pliku źródłowego hello o nazwie `SearchLog.tsv`schematizes go i ponownie zapisuje hello wierszy w pliku o nazwie SearchLog pierwszej u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="4326a-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="4326a-120">Zwróć uwagę, hello znaku zapytania dalej toohello typ danych w hello `Duration` pola.</span><span class="sxs-lookup"><span data-stu-id="4326a-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="4326a-121">Oznacza to, że hello `Duration` pole może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="4326a-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="4326a-122">Kluczowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="4326a-122">Key concepts</span></span>
* <span data-ttu-id="4326a-123">**Zestaw wierszy zmiennych**: każde wyrażenie zapytania, który spowoduje utworzenie zestawu wierszy można przypisać zmiennej tooa.</span><span class="sxs-lookup"><span data-stu-id="4326a-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="4326a-124">U-SQL następuje hello T-SQL variable — wzorzec nazewnictwa (`@searchlog`, na przykład) w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="4326a-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="4326a-125">Witaj **WYODRĘBNIĆ** — słowo kluczowe odczytywać dane z pliku i definiuje schemat hello na odczyt.</span><span class="sxs-lookup"><span data-stu-id="4326a-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="4326a-126">`Extractors.Tsv`jest wbudowane ekstraktor U-SQL dla plików kartę wartości rozdzielanych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="4326a-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="4326a-127">Można tworzyć niestandardowe ekstraktory.</span><span class="sxs-lookup"><span data-stu-id="4326a-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="4326a-128">Witaj **dane wyjściowe** zapisuje dane z pliku tooa zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="4326a-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="4326a-129">`Outputters.Csv()`jest to plik przecinkami wartości rozdzielanych przecinkami wbudowanych toocreate outputter U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4326a-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="4326a-130">Można tworzyć niestandardowe outputters.</span><span class="sxs-lookup"><span data-stu-id="4326a-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="4326a-131">Ścieżki do plików</span><span class="sxs-lookup"><span data-stu-id="4326a-131">File paths</span></span>

<span data-ttu-id="4326a-132">Hello WYODRĘBNIANIA i danych wyjściowych instrukcji należy użyć ścieżki do pliku.</span><span class="sxs-lookup"><span data-stu-id="4326a-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="4326a-133">Ścieżki plików może być bezwzględny lub względny:</span><span class="sxs-lookup"><span data-stu-id="4326a-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="4326a-134">Plik tooa w usłudze Data Lake Store o nazwie odwołuje się ten następująca ścieżka bezwzględna do pliku `mystore`:</span><span class="sxs-lookup"><span data-stu-id="4326a-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="4326a-135">Rozpoczyna się od tego następująca ścieżka pliku `"/"`.</span><span class="sxs-lookup"><span data-stu-id="4326a-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="4326a-136">Odwołuje się plik tooa w hello domyślnego konta usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="4326a-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="4326a-137">Użyj zmienne skalara</span><span class="sxs-lookup"><span data-stu-id="4326a-137">Use scalar variables</span></span>

<span data-ttu-id="4326a-138">Można używać skalarne zmiennych jako dobrze toomake Twojego skryptu konserwacji łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="4326a-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="4326a-139">poprzedni skrypt U-SQL Hello również może być zapisany jako:</span><span class="sxs-lookup"><span data-stu-id="4326a-139">hello previous U-SQL script can also be written as:</span></span>

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

## <a name="transform-rowsets"></a><span data-ttu-id="4326a-140">Przekształć zestawy wierszy</span><span class="sxs-lookup"><span data-stu-id="4326a-140">Transform rowsets</span></span>

<span data-ttu-id="4326a-141">Użyj **wybierz** tootransform zestawów wierszy:</span><span class="sxs-lookup"><span data-stu-id="4326a-141">Use **SELECT** tootransform rowsets:</span></span>

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

<span data-ttu-id="4326a-142">Witaj, używa klauzuli WHERE [C# logicznego wyrażenia](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="4326a-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="4326a-143">Witaj C# wyrażenia języka toodo można użyć własnych wyrażeń i funkcji.</span><span class="sxs-lookup"><span data-stu-id="4326a-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="4326a-144">Można nawet wykonywać bardziej złożone filtrowanie łącząc je z spójników logiczne (i) i disjunctions (ORs).</span><span class="sxs-lookup"><span data-stu-id="4326a-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="4326a-145">Witaj poniższy skrypt używa metody DateTime.Parse() hello i połączeniu.</span><span class="sxs-lookup"><span data-stu-id="4326a-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
 ><span data-ttu-id="4326a-146">wynik hello hello pierwszy zestaw wierszy, który tworzy dwa filtry złożone hello działające Hello drugiego zapytania.</span><span class="sxs-lookup"><span data-stu-id="4326a-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="4326a-147">Można również użyć ponownie nazwę zmiennej, a nazwy hello lexically ograniczone.</span><span class="sxs-lookup"><span data-stu-id="4326a-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="4326a-148">Łączny zestawy wierszy</span><span class="sxs-lookup"><span data-stu-id="4326a-148">Aggregate rowsets</span></span>
<span data-ttu-id="4326a-149">U-SQL umożliwia hello znanych ORDER BY, GROUP BY i agregacji.</span><span class="sxs-lookup"><span data-stu-id="4326a-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="4326a-150">Hello następujące zapytanie znajdzie hello całkowity czas trwania na region, a następnie wyświetla hello top pięciu wartości czasu trwania w kolejności.</span><span class="sxs-lookup"><span data-stu-id="4326a-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="4326a-151">Zestawy wierszy U-SQL nie zachowuj ich kolejność hello dalej zapytania.</span><span class="sxs-lookup"><span data-stu-id="4326a-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="4326a-152">W związku z tym tooorder jako dane wyjściowe, należy tooadd ORDER BY toohello danych wyjściowych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="4326a-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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

<span data-ttu-id="4326a-153">klauzuli U-SQL ORDER BY Hello wymaga przy użyciu klauzuli FETCH hello w wyrażeniu SELECT.</span><span class="sxs-lookup"><span data-stu-id="4326a-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="4326a-154">Klauzula o języku U-SQL Hello może być używane toorestrict hello dane wyjściowe toogroups, które spełniają warunek HAVING hello:</span><span class="sxs-lookup"><span data-stu-id="4326a-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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

<span data-ttu-id="4326a-155">Scenariusze zaawansowane agregacji, można znaleźć w dokumentacji odwołanie hello U-SQL hello [agregacji, analitycznych i referencyjne funkcji](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="4326a-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4326a-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4326a-156">Next steps</span></span>
* [<span data-ttu-id="4326a-157">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4326a-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4326a-158">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4326a-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
