---
title: "aaaMapReduce i połączenia SSH z usługą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SSH toorun MapReduce zadania przy użyciu platformy Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="b7bd1-103">Używanie MapReduce z usługą Hadoop w usłudze HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="b7bd1-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="b7bd1-104">Dowiedz się, jak zadania toosubmit MapReduce z tooHDInsight połączeń Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="b7bd1-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="b7bd1-105">Jeśli znasz już opartą na systemie Linux platformą Hadoop korzystanie z serwerów, ale nowe tooHDInsight, zobacz [porady HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="b7bd1-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="b7bd1-106"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b7bd1-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="b7bd1-107">Klaster opartych na systemie Linux usługą HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b7bd1-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b7bd1-108">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b7bd1-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="b7bd1-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b7bd1-110">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-110">An SSH client.</span></span> <span data-ttu-id="b7bd1-111">Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="b7bd1-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="b7bd1-112"><a id="ssh"></a>Połącz przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="b7bd1-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="b7bd1-113">Połącz toohello klastra przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="b7bd1-114">Na przykład następujące polecenie hello łączy tooa klastra o nazwie **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="b7bd1-115">**Jeśli używasz klucza certyfikatu dla uwierzytelniania SSH**, może być konieczne toospecify hello lokalizację klucza prywatnego hello w systemie klienta, na przykład:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="b7bd1-116">**Jeśli używasz hasła dla uwierzytelniania SSH**, potrzebne tooprovide hello hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="b7bd1-117">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b7bd1-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="b7bd1-118"><a id="hadoop"></a>Użyj poleceń usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="b7bd1-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="b7bd1-119">Po są połączone toohello klastra usługi HDInsight, użyj następujących hello polecenia toostart zadania MapReduce:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="b7bd1-120">To polecenie uruchamia hello `wordcount` klasy, która jest zawarta w hello `hadoop-mapreduce-examples.jar` pliku.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="b7bd1-121">Używa hello `/example/data/gutenberg/davinci.txt` dokumentu jako dane wejściowe i wyjściowe są przechowywane w `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7bd1-122">Aby uzyskać więcej informacji o tym MapReduce zadania i hello przykładowe dane, zobacz [MapReduce używany w Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="b7bd1-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="b7bd1-123">zadanie Hello emituje szczegóły przetwarzania i zwraca informacje toohello podobne następującego tekstu po zakończeniu zadania hello:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="b7bd1-124">Po zakończeniu zadania hello, użyj hello następujące pliki wyjściowe hello toolist polecenia:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="b7bd1-125">To polecenie wyświetla dwa pliki `_SUCCESS` i `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="b7bd1-126">Witaj `part-r-00000` plik zawiera dane wyjściowe powitania dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7bd1-127">Niektóre zadania MapReduce mogą podzielone hello wyniki w wielu **części r-###** plików.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="b7bd1-128">Jeśli tak, użyj hello ### sufiks tooindicate kolejność hello hello plików.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="b7bd1-129">dane wyjściowe hello tooview, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="b7bd1-130">To polecenie wyświetla listę hello wyrazy, które są zawarte w hello **wasb://example/data/gutenberg/davinci.txt** plików i hello liczba wystąpił każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="b7bd1-131">Witaj następujący tekst jest przykładem hello danych zawartych w pliku hello:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="b7bd1-132"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b7bd1-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="b7bd1-133">Jak widać, polecenia Hadoop zapewniają prosty sposób toorun zadań MapReduce w klastrze usługi HDInsight, a następnie dane wyjściowe zadania hello widoku.</span><span class="sxs-lookup"><span data-stu-id="b7bd1-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="b7bd1-134"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7bd1-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="b7bd1-135">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="b7bd1-136">Korzystać z usługi MapReduce na HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="b7bd1-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="b7bd1-137">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b7bd1-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b7bd1-138">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7bd1-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b7bd1-139">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7bd1-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
