---
title: "aaaUse Hadoop Pig w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse wieprzowe z platformą Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="58f89-103">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58f89-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="58f89-104">Dowiedz się, jak toouse [Apache Pig](http://pig.apache.org/) z usługą HDInsight...</span><span class="sxs-lookup"><span data-stu-id="58f89-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="58f89-105">Pig to platforma do tworzenia programów dla platformy Hadoop przy użyciu języka procedurach znany jako *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="58f89-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="58f89-106">Pig jest alternatywnych tooJava tworzenia *MapReduce* rozwiązania który znajduje się w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58f89-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="58f89-107">Użyj powitania po tabeli toodiscover hello różne sposoby, że Pig mogą być używane z usługą HDInsight:</span><span class="sxs-lookup"><span data-stu-id="58f89-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="58f89-108">**Użyj tej** Jeśli chcesz...</span><span class="sxs-lookup"><span data-stu-id="58f89-108">**Use this** if you want...</span></span> | <span data-ttu-id="58f89-109">.. .an **interakcyjne** powłoki</span><span class="sxs-lookup"><span data-stu-id="58f89-109">...an **interactive** shell</span></span> | <span data-ttu-id="58f89-110">... **partii** przetwarzania</span><span class="sxs-lookup"><span data-stu-id="58f89-110">...**batch** processing</span></span> | <span data-ttu-id="58f89-111">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="58f89-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="58f89-112">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="58f89-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="58f89-113">SSH</span><span class="sxs-lookup"><span data-stu-id="58f89-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="58f89-114">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-114">✔</span></span> |<span data-ttu-id="58f89-115">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-115">✔</span></span> |<span data-ttu-id="58f89-116">Linux</span><span class="sxs-lookup"><span data-stu-id="58f89-116">Linux</span></span> |<span data-ttu-id="58f89-117">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="58f89-118">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="58f89-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="58f89-119">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-119">✔</span></span> |<span data-ttu-id="58f89-120">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-120">Linux or Windows</span></span> |<span data-ttu-id="58f89-121">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="58f89-122">Zestaw SDK dla platformy .NET usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="58f89-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="58f89-123">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-123">✔</span></span> |<span data-ttu-id="58f89-124">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-124">Linux or Windows</span></span> |<span data-ttu-id="58f89-125">Systemu Windows (na razie)</span><span class="sxs-lookup"><span data-stu-id="58f89-125">Windows (for now)</span></span> |
| [<span data-ttu-id="58f89-126">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="58f89-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="58f89-127">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-127">✔</span></span> |<span data-ttu-id="58f89-128">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-128">Linux or Windows</span></span> |<span data-ttu-id="58f89-129">Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-129">Windows</span></span> |
| <span data-ttu-id="58f89-130">[Pulpit zdalny](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 i 3.3)</span><span class="sxs-lookup"><span data-stu-id="58f89-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="58f89-131">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-131">✔</span></span> |<span data-ttu-id="58f89-132">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-132">✔</span></span> |<span data-ttu-id="58f89-133">Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-133">Windows</span></span> |<span data-ttu-id="58f89-134">Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="58f89-135">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="58f89-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="58f89-136">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="58f89-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="58f89-137"><a id="why"></a>Dlaczego warto korzystać z języka Pig</span><span class="sxs-lookup"><span data-stu-id="58f89-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="58f89-138">Jednym z wyzwań hello przetwarzania danych przy użyciu MapReduce w Hadoop przy użyciu tylko mapy i funkcja Zmniejsz implementuje logika przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="58f89-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="58f89-139">Do złożonych obliczeń, często mają toobreak przetwarzania na wiele operacji MapReduce, które są połączone tooachieve hello żądanego wyniku.</span><span class="sxs-lookup"><span data-stu-id="58f89-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="58f89-140">Pig umożliwia toodefine przetwarzania jako serię transformacje, których hello przepływów danych za pośrednictwem tooproduce hello potrzebne w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="58f89-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="58f89-141">język Pig Latin Hello pozwala możesz toodescribe hello przepływu danych z nieprzetworzone dane wejściowe, przez co najmniej jeden przekształcenia, dane wyjściowe hello potrzeby tooproduce.</span><span class="sxs-lookup"><span data-stu-id="58f89-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="58f89-142">Programy pig Latin wykonaj tego wzorca ogólne:</span><span class="sxs-lookup"><span data-stu-id="58f89-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="58f89-143">**Obciążenia**: odczytu danych toobe modyfikowany w zakresie od hello systemu plików</span><span class="sxs-lookup"><span data-stu-id="58f89-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="58f89-144">**Przekształć**: manipulować danymi hello</span><span class="sxs-lookup"><span data-stu-id="58f89-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="58f89-145">**Zrzut lub przechowywać**: ekran toohello danych wyjściowych lub zapisać go do przetworzenia</span><span class="sxs-lookup"><span data-stu-id="58f89-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="58f89-146">Funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="58f89-146">User-defined functions</span></span>

<span data-ttu-id="58f89-147">Pig Latin obsługuje również funkcje zdefiniowane przez użytkownika (UDF), dzięki czemu można tooinvoke składników zewnętrznych, które implementują logikę, która jest trudne toomodel w Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="58f89-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="58f89-148">Aby uzyskać więcej informacji na temat Pig Latin, zobacz [1 Ręczne odwołanie Pig Latin](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) i [2 ręczne odwołanie Pig Latin](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="58f89-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="58f89-149">Przykład przy użyciu funkcji UDF z Pig Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="58f89-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="58f89-150">[DataFu za pomocą Pig w usłudze HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu jest kolekcją przydatne funkcje UDF obsługiwanego przez Apache</span><span class="sxs-lookup"><span data-stu-id="58f89-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="58f89-151">Używanie języka Python za pomocą Pig i Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58f89-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="58f89-152">Używanie języka C# z Hive i Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58f89-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="58f89-153"><a id="data"></a>Przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="58f89-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="58f89-154">Usługa HDInsight zapewnia różne przykład zestawów danych, które są przechowywane w hello `/example/data` i `/HdiSamples` katalogów.</span><span class="sxs-lookup"><span data-stu-id="58f89-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="58f89-155">Te katalogi są hello domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="58f89-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="58f89-156">przykład Witaj Pig w tym dokumencie używa hello *log4j* plik `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="58f89-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="58f89-157">Każdy dziennik wewnątrz pliku hello składa się z pól wiersz, który zawiera `[LOG LEVEL]` pola tooshow hello typu i hello ważność, na przykład:</span><span class="sxs-lookup"><span data-stu-id="58f89-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="58f89-158">W poprzednim przykładzie hello poziom dziennika hello jest błąd.</span><span class="sxs-lookup"><span data-stu-id="58f89-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="58f89-159">Można także wygenerować plik log4j przy użyciu hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) narzędzia rejestrowania, a następnie przekaż tego obiektu blob tooyour pliku.</span><span class="sxs-lookup"><span data-stu-id="58f89-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="58f89-160">Zobacz [tooHDInsight przekazywanie danych](hdinsight-upload-data.md) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="58f89-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="58f89-161">Aby uzyskać więcej informacji o używaniu obiekty BLOB w magazynie Azure z usługą HDInsight, zobacz [Użyj magazynu obiektów Blob Azure z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="58f89-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="58f89-162"><a id="job"></a>Przykładowe zadania</span><span class="sxs-lookup"><span data-stu-id="58f89-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="58f89-163">Witaj zadanie Pig Latin ładuje hello `sample.log` plik z hello domyślnego magazynu dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58f89-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="58f89-164">Następnie wykonuje szereg przekształcenia prowadzących liczbę jak wiele razy każdego danych wejściowych hello wystąpił poziomu dziennika.</span><span class="sxs-lookup"><span data-stu-id="58f89-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="58f89-165">wyniki Hello są zapisywane tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="58f89-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="58f89-166">Witaj poniższej ilustracji przedstawiono podsumowanie jakie każdego transformacji jest toohello danych.</span><span class="sxs-lookup"><span data-stu-id="58f89-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Graficzna reprezentacja hello przekształcenia][image-hdi-pig-data-transformation]

## <span data-ttu-id="58f89-168"><a id="run"></a>Uruchom zadanie Pig Latin hello</span><span class="sxs-lookup"><span data-stu-id="58f89-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="58f89-169">HDInsight można uruchamiać zadania Pig Latin przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="58f89-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="58f89-170">Użyj powitania po toodecide tabeli, która metoda jest odpowiednie dla Ciebie, a następnie wykonaj hello łącze, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="58f89-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="58f89-171">**Użyj tej** Jeśli chcesz...</span><span class="sxs-lookup"><span data-stu-id="58f89-171">**Use this** if you want...</span></span> | <span data-ttu-id="58f89-172">.. .an **interakcyjne** powłoki</span><span class="sxs-lookup"><span data-stu-id="58f89-172">...an **interactive** shell</span></span> | <span data-ttu-id="58f89-173">... **partii** przetwarzania</span><span class="sxs-lookup"><span data-stu-id="58f89-173">...**batch** processing</span></span> | <span data-ttu-id="58f89-174">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="58f89-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="58f89-175">.. .from to **klienta**</span><span class="sxs-lookup"><span data-stu-id="58f89-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="58f89-176">SSH</span><span class="sxs-lookup"><span data-stu-id="58f89-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="58f89-177">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-177">✔</span></span> |<span data-ttu-id="58f89-178">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-178">✔</span></span> |<span data-ttu-id="58f89-179">Linux</span><span class="sxs-lookup"><span data-stu-id="58f89-179">Linux</span></span> |<span data-ttu-id="58f89-180">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="58f89-181">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="58f89-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="58f89-182">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-182">✔</span></span> |<span data-ttu-id="58f89-183">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-183">Linux or Windows</span></span> |<span data-ttu-id="58f89-184">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="58f89-185">Zestaw SDK dla platformy .NET usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="58f89-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="58f89-186">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-186">✔</span></span> |<span data-ttu-id="58f89-187">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-187">Linux or Windows</span></span> |<span data-ttu-id="58f89-188">Systemu Windows (na razie)</span><span class="sxs-lookup"><span data-stu-id="58f89-188">Windows (for now)</span></span> |
| [<span data-ttu-id="58f89-189">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="58f89-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="58f89-190">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-190">✔</span></span> |<span data-ttu-id="58f89-191">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-191">Linux or Windows</span></span> |<span data-ttu-id="58f89-192">Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-192">Windows</span></span> |
| <span data-ttu-id="58f89-193">[Pulpit zdalny](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 i 3.3)</span><span class="sxs-lookup"><span data-stu-id="58f89-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="58f89-194">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-194">✔</span></span> |<span data-ttu-id="58f89-195">✔</span><span class="sxs-lookup"><span data-stu-id="58f89-195">✔</span></span> |<span data-ttu-id="58f89-196">Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-196">Windows</span></span> |<span data-ttu-id="58f89-197">Windows</span><span class="sxs-lookup"><span data-stu-id="58f89-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="58f89-198">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="58f89-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="58f89-199">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="58f89-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="58f89-200">Pig i SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="58f89-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="58f89-201">Możesz użyć programu SQL Server Integration Services (SSIS) toorun zadania programu Pig.</span><span class="sxs-lookup"><span data-stu-id="58f89-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="58f89-202">Hello Azure Feature Pack do SSIS zapewnia hello następujące składniki, które współpracują z zadań Pig w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58f89-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="58f89-203">[Zadaniem Azure HDInsight Pig][pigtask]</span><span class="sxs-lookup"><span data-stu-id="58f89-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="58f89-204">[Menedżer połączeń subskrypcji platformy Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="58f89-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="58f89-205">Dowiedz się więcej o hello Azure Feature Pack SSIS [tutaj][ssispack].</span><span class="sxs-lookup"><span data-stu-id="58f89-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="58f89-206"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58f89-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="58f89-207">Teraz, kiedy znasz już jak toouse Pig z usługą HDInsight, hello Użyj następujących łączy tooexplore toowork inne sposoby z usługą Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58f89-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="58f89-208">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="58f89-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="58f89-209">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="58f89-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="58f89-210">Korzystanie z usługą HDInsight Sqoop</span><span class="sxs-lookup"><span data-stu-id="58f89-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="58f89-211">Korzystanie z Oozie z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="58f89-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="58f89-212">[Korzystanie z zadań MapReduce z usługą HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="58f89-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
