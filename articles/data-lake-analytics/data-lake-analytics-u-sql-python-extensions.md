---
title: "Rozszerzanie skryptów U-SQL z języka Python w usłudze Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uruchomić kod w języku Python w skryptów U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d18ef1f747aee2fa01cef9891432d0461031ee4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="dcfbd-103">Samouczek: Rozpoczynanie pracy z rozszerzanie U-SQL z języka Python</span><span class="sxs-lookup"><span data-stu-id="dcfbd-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="dcfbd-104">Rozszerzenia języka Python dla U-SQL umożliwiają deweloperom wykonać równoległemu wykonywanie kodu języka Python.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="dcfbd-105">Poniższy przykład przedstawia podstawowe kroki:</span><span class="sxs-lookup"><span data-stu-id="dcfbd-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="dcfbd-106">Użyj `REFERENCE ASSEMBLY` instrukcji, aby włączyć rozszerzenia języka Python dla skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="dcfbd-106">Use the `REFERENCE ASSEMBLY` statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="dcfbd-107">Przy użyciu `REDUCE` operacji do partycjonowania danych wejściowych dla klucza</span><span class="sxs-lookup"><span data-stu-id="dcfbd-107">Using the `REDUCE` operation to partition the input data on a key</span></span>
* <span data-ttu-id="dcfbd-108">Rozszerzenia języka Python dla U-SQL to wbudowane reduktor (`Extension.Python.Reducer`) uruchomione na każdy wierzchołek przypisane do reduktor kodu języka Python</span><span class="sxs-lookup"><span data-stu-id="dcfbd-108">The Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="dcfbd-109">Skrypt U-SQL zawiera osadzony kod języka Python, który ma funkcji o nazwie `usqlml_main` akceptuje pandas DataFrame jako dane wejściowe i zwraca pandas DataFrame jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-109">The U-SQL script contains the embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="dcfbd-110">Jak Python integruje się z języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="dcfbd-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="dcfbd-111">Typy danych</span><span class="sxs-lookup"><span data-stu-id="dcfbd-111">Datatypes</span></span>

* <span data-ttu-id="dcfbd-112">Ciąg, jak i numeryczne kolumny z U-SQL są konwertowane na — między Pandas i języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="dcfbd-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="dcfbd-113">U-SQL wartości null są konwertowane do i z Pandas `NA` wartości</span><span class="sxs-lookup"><span data-stu-id="dcfbd-113">U-SQL Nulls are converted to and from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="dcfbd-114">Schematy</span><span class="sxs-lookup"><span data-stu-id="dcfbd-114">Schemas</span></span>

* <span data-ttu-id="dcfbd-115">Wektory indeksu w Pandas nie są obsługiwane w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="dcfbd-116">Wszystkie ramki danych wejściowych w funkcji języka Python zawsze ma 64-bitowych indeksu numerycznych od 0 do liczby wierszy pomniejszonej o 1.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="dcfbd-117">Zestaw danych skryptu U-SQL nie mogą mieć zduplikowanych nazw kolumn</span><span class="sxs-lookup"><span data-stu-id="dcfbd-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="dcfbd-118">U-SQL nazwy kolumn zestawów danych, które nie są ciągami.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="dcfbd-119">Wersji języka Python</span><span class="sxs-lookup"><span data-stu-id="dcfbd-119">Python Versions</span></span>
<span data-ttu-id="dcfbd-120">Obsługiwane jest tylko Python 3.5.1 (skompilowany dla systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="dcfbd-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="dcfbd-121">Standardowe moduły języka Python</span><span class="sxs-lookup"><span data-stu-id="dcfbd-121">Standard Python modules</span></span>
<span data-ttu-id="dcfbd-122">Uwzględniane są wszystkie standardowe moduły języka Python.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="dcfbd-123">Dodatkowe moduły języka Python</span><span class="sxs-lookup"><span data-stu-id="dcfbd-123">Additional Python modules</span></span>
<span data-ttu-id="dcfbd-124">Oprócz standardowych bibliotek języka Python uwzględniono kilka bibliotek często używane python:</span><span class="sxs-lookup"><span data-stu-id="dcfbd-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="dcfbd-125">Komunikaty o wyjątkach</span><span class="sxs-lookup"><span data-stu-id="dcfbd-125">Exception Messages</span></span>
<span data-ttu-id="dcfbd-126">Obecnie Wystąpił wyjątek w kodzie języka Python jest wyświetlany jako błąd rodzajowy wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="dcfbd-127">Komunikaty o błędach zadań U-SQL w przyszłości, wyświetli komunikat o wyjątku języka Python.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="dcfbd-128">Dane wejściowe i ograniczenia rozmiaru danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="dcfbd-128">Input and Output size limitations</span></span>
<span data-ttu-id="dcfbd-129">Każdy wierzchołek ma ograniczoną ilość pamięci przypisanej do niego.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="dcfbd-130">Obecnie ten limit jest 6 GB dla funkcji Aktualizacje automatyczne.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="dcfbd-131">Ponieważ DataFrames wejściowych i wyjściowych musi istnieć w pamięci w kodzie języka Python, wówczas łączny rozmiar danych wejściowych i wyjściowych nie może przekroczyć 6 GB.</span><span class="sxs-lookup"><span data-stu-id="dcfbd-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="dcfbd-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="dcfbd-132">See also</span></span>
* [<span data-ttu-id="dcfbd-133">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="dcfbd-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="dcfbd-134">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dcfbd-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="dcfbd-135">Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="dcfbd-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

