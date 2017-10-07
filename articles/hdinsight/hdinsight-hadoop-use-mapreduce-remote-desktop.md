---
title: "aaaMapReduce i zdalny pulpit z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse pulpitu zdalnego tooconnect tooHadoop w usłudze HDInsight i uruchamiania zadań MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="31600-103">Korzystać z usługi MapReduce w Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="31600-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="31600-104">W tym artykule będzie Dowiedz się, jak tooa tooconnect Hadoop w usłudze HDInsight klastra przy użyciu pulpitu zdalnego i za pomocą polecenia Hadoop hello i uruchom zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="31600-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31600-105">Pulpit zdalny jest dostępna tylko w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="31600-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="31600-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="31600-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="31600-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="31600-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="31600-108">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [MapReduce Użyj przy użyciu protokołu SSH](hdinsight-hadoop-use-mapreduce-ssh.md) informacji na temat łączenia toohello klastra usługi HDInsight i uruchamiania zadań MapReduce.</span><span class="sxs-lookup"><span data-stu-id="31600-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="31600-109"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="31600-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="31600-110">toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="31600-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="31600-111">Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="31600-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="31600-112">Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7</span><span class="sxs-lookup"><span data-stu-id="31600-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="31600-113"><a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="31600-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="31600-114">Włączenie pulpitu zdalnego dla klastra usługi HDInsight hello, a następnie połącz tooit, wykonując następujące instrukcje hello [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="31600-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="31600-115"><a id="hadoop"></a>Użyj polecenia Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="31600-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="31600-116">Po zakończeniu pulpitu toohello podłączonego do klastra usługi HDInsight hello, za pomocą hello następujące kroki toorun zadania MapReduce za pomocą polecenia Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="31600-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="31600-117">Na pulpicie HDInsight hello start hello **wiersza polecenia usługi Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="31600-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="31600-118">Zostanie otwarty nowy wiersz polecenia w hello **c:\apps\dist\hadoop-&lt;numer wersji >** katalogu.</span><span class="sxs-lookup"><span data-stu-id="31600-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31600-119">numer wersji Hello zmieni Hadoop jest aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="31600-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="31600-120">Witaj **HADOOP_HOME** zmiennej środowiskowej może być używane toofind hello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="31600-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="31600-121">Na przykład `cd %HADOOP_HOME%` zmiany katalogów toohello katalogu Hadoop, bez konieczności wprowadzania numer wersji hello tooknow.</span><span class="sxs-lookup"><span data-stu-id="31600-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="31600-122">Witaj toouse **Hadoop** polecenia toorun przykład zadania MapReduce, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="31600-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="31600-123">Spowoduje to uruchomienie hello **wordcount** klasy, która jest zawarta w hello **hadoop-mapreduce-examples.jar** plik w bieżącym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="31600-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="31600-124">Jako dane wejściowe, używa hello **wasb://example/data/gutenberg/davinci.txt** dokumentu, a dane wyjściowe są przechowywane w: **wasb: / / / przykład/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="31600-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31600-125">Aby uzyskać więcej informacji o tym MapReduce zadania i hello przykładowe dane, zobacz <a href="hdinsight-use-mapreduce.md">MapReduce użycia w usłudze HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="31600-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="31600-126">zadanie Hello emituje szczegóły, jak są przetwarzane i zwraca informacje o podobnych toohello następujące po zakończeniu zadania hello:</span><span class="sxs-lookup"><span data-stu-id="31600-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="31600-127">Po zakończeniu zadania hello Użyj hello następujące polecenia toolist hello dane wyjściowe pliki przechowywane w **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="31600-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="31600-128">To powinien być wyświetlany dwa pliki **_SUCCESS** i **części r-00000**.</span><span class="sxs-lookup"><span data-stu-id="31600-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="31600-129">Witaj **części r-00000** plik zawiera dane wyjściowe powitania dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="31600-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31600-130">Niektóre zadania MapReduce mogą podzielone hello wyniki w wielu **części r-###** plików.</span><span class="sxs-lookup"><span data-stu-id="31600-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="31600-131">Jeśli tak, użyj hello ### sufiks tooindicate kolejność hello hello plików.</span><span class="sxs-lookup"><span data-stu-id="31600-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="31600-132">dane wyjściowe hello tooview, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="31600-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="31600-133">Spowoduje to wyświetlenie listy hello wyrazy, które są zawarte w hello **wasb://example/data/gutenberg/davinci.txt** pliku hello liczba wystąpił każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="31600-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="31600-134">Witaj, poniżej przedstawiono przykładowy hello danych, które zostaną uwzględnione w pliku hello:</span><span class="sxs-lookup"><span data-stu-id="31600-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="31600-135"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="31600-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="31600-136">Jak widać, hello polecenia Hadoop zapewnia toorun łatwy sposób na klastra usługi HDInsight, a następnie dane wyjściowe zadania hello widoku zadań MapReduce.</span><span class="sxs-lookup"><span data-stu-id="31600-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="31600-137"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31600-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="31600-138">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31600-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="31600-139">Korzystać z usługi MapReduce na HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="31600-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="31600-140">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31600-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="31600-141">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="31600-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="31600-142">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="31600-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
