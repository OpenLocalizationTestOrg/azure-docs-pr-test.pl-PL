---
title: "aaaExtend U-SQL skrypty języka Python w usłudze Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kod toorun Python skryptów U-SQL"
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
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="3a48e-103">Samouczek: Rozpoczynanie pracy z rozszerzanie U-SQL z języka Python</span><span class="sxs-lookup"><span data-stu-id="3a48e-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="3a48e-104">Rozszerzenia języka Python dla U-SQL Włącz deweloperzy tooperform równoległemu wykonywanie kodu języka Python.</span><span class="sxs-lookup"><span data-stu-id="3a48e-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="3a48e-105">Witaj poniższy przykład przedstawia hello podstawowe kroki:</span><span class="sxs-lookup"><span data-stu-id="3a48e-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="3a48e-106">Użyj hello `REFERENCE ASSEMBLY` rozszerzenia języka Python tooenable instrukcji hello skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="3a48e-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="3a48e-107">Przy użyciu hello `REDUCE` operacji toopartition hello wprowadzić dane dla klucza</span><span class="sxs-lookup"><span data-stu-id="3a48e-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="3a48e-108">Hello rozszerzenia języka Python dla U-SQL zawierają wbudowane reduktor (`Extension.Python.Reducer`) uruchomione na każdy wierzchołek przypisane toohello reduktor kodu języka Python</span><span class="sxs-lookup"><span data-stu-id="3a48e-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="3a48e-109">Hello skryptu U-SQL zawiera osadzone hello Python kod, który ma funkcji o nazwie `usqlml_main` akceptuje pandas DataFrame jako dane wejściowe i zwraca pandas DataFrame jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3a48e-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

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
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="3a48e-110">Jak Python integruje się z języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="3a48e-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="3a48e-111">Typy danych</span><span class="sxs-lookup"><span data-stu-id="3a48e-111">Datatypes</span></span>

* <span data-ttu-id="3a48e-112">Ciąg, jak i numeryczne kolumny z U-SQL są konwertowane na — między Pandas i języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="3a48e-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="3a48e-113">U-SQL wartości null są tooand przekonwertowany z Pandas `NA` wartości</span><span class="sxs-lookup"><span data-stu-id="3a48e-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="3a48e-114">Schematy</span><span class="sxs-lookup"><span data-stu-id="3a48e-114">Schemas</span></span>

* <span data-ttu-id="3a48e-115">Wektory indeksu w Pandas nie są obsługiwane w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3a48e-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="3a48e-116">Wszystkie ramki danych wejściowych w funkcji Python hello zawsze ma 64-bitowych indeksu numerycznych od 0 do hello liczbę wierszy pomniejszonej o 1.</span><span class="sxs-lookup"><span data-stu-id="3a48e-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="3a48e-117">Zestaw danych skryptu U-SQL nie mogą mieć zduplikowanych nazw kolumn</span><span class="sxs-lookup"><span data-stu-id="3a48e-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="3a48e-118">U-SQL nazwy kolumn zestawów danych, które nie są ciągami.</span><span class="sxs-lookup"><span data-stu-id="3a48e-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="3a48e-119">Wersji języka Python</span><span class="sxs-lookup"><span data-stu-id="3a48e-119">Python Versions</span></span>
<span data-ttu-id="3a48e-120">Obsługiwane jest tylko Python 3.5.1 (skompilowany dla systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="3a48e-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="3a48e-121">Standardowe moduły języka Python</span><span class="sxs-lookup"><span data-stu-id="3a48e-121">Standard Python modules</span></span>
<span data-ttu-id="3a48e-122">Uwzględniane są wszystkie moduły hello standard języka Python.</span><span class="sxs-lookup"><span data-stu-id="3a48e-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="3a48e-123">Dodatkowe moduły języka Python</span><span class="sxs-lookup"><span data-stu-id="3a48e-123">Additional Python modules</span></span>
<span data-ttu-id="3a48e-124">Oprócz hello standardowych bibliotek języka Python, uwzględniono kilka bibliotek często używane python:</span><span class="sxs-lookup"><span data-stu-id="3a48e-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="3a48e-125">Komunikaty o wyjątkach</span><span class="sxs-lookup"><span data-stu-id="3a48e-125">Exception Messages</span></span>
<span data-ttu-id="3a48e-126">Obecnie Wystąpił wyjątek w kodzie języka Python jest wyświetlany jako błąd rodzajowy wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="3a48e-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="3a48e-127">W przyszłości hello komunikaty o błędach zadań U-SQL hello wyświetli komunikat o wyjątku hello Python.</span><span class="sxs-lookup"><span data-stu-id="3a48e-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="3a48e-128">Dane wejściowe i ograniczenia rozmiaru danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="3a48e-128">Input and Output size limitations</span></span>
<span data-ttu-id="3a48e-129">Każdy wierzchołek ma ograniczoną ilość pamięci przypisana tooit.</span><span class="sxs-lookup"><span data-stu-id="3a48e-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="3a48e-130">Obecnie ten limit jest 6 GB dla funkcji Aktualizacje automatyczne.</span><span class="sxs-lookup"><span data-stu-id="3a48e-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="3a48e-131">Ponieważ hello DataFrames wejściowych i wyjściowych musi istnieć w pamięci w kodzie języka Python hello, łączny rozmiar hello hello danych wejściowych i wyjściowych nie może przekroczyć 6 GB.</span><span class="sxs-lookup"><span data-stu-id="3a48e-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="3a48e-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3a48e-132">See also</span></span>
* [<span data-ttu-id="3a48e-133">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3a48e-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3a48e-134">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a48e-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="3a48e-135">Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="3a48e-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

