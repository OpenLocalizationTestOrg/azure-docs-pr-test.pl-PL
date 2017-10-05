---
title: "MapReduce i SSH połączenia z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać SSH do uruchomienia zadań MapReduce przy użyciu platformy Hadoop w usłudze HDInsight."
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
ms.openlocfilehash: eaf6278f97cd5ddd7e049ff4745181f39d7949a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="86aa4-103">Używanie MapReduce z usługą Hadoop w usłudze HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="86aa4-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="86aa4-104">Dowiedz się, jak można przesłać zadania MapReduce z połączenia protokołu Secure Shell (SSH) do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86aa4-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="86aa4-105">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale jesteś nowym użytkownikiem usługi HDInsight, zobacz [porady HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="86aa4-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="86aa4-106"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86aa4-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="86aa4-107">Klaster opartych na systemie Linux usługą HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="86aa4-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="86aa4-108">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="86aa4-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="86aa4-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="86aa4-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="86aa4-110">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="86aa4-110">An SSH client.</span></span> <span data-ttu-id="86aa4-111">Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="86aa4-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="86aa4-112"><a id="ssh"></a>Połącz przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="86aa4-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="86aa4-113">Połącz z klastrem przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="86aa4-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="86aa4-114">Na przykład następujące polecenie nawiązuje połączenie z klastra o nazwie **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="86aa4-114">For example, the following command connects to a cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="86aa4-115">**Jeśli używasz klucza certyfikatu dla uwierzytelniania SSH**, może być konieczne na przykład określ lokalizację klucza prywatnego w systemie klienta:</span><span class="sxs-lookup"><span data-stu-id="86aa4-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="86aa4-116">**Jeśli używasz hasła dla uwierzytelniania SSH**, musisz podać hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="86aa4-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="86aa4-117">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="86aa4-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="86aa4-118"><a id="hadoop"></a>Użyj poleceń usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="86aa4-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="86aa4-119">Po połączeniu się z klastrem usługi HDInsight, użyj następującego polecenia, można uruchomić zadania MapReduce:</span><span class="sxs-lookup"><span data-stu-id="86aa4-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="86aa4-120">To polecenie uruchamia `wordcount` klasy, która jest zawarta w `hadoop-mapreduce-examples.jar` pliku.</span><span class="sxs-lookup"><span data-stu-id="86aa4-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="86aa4-121">Używa `/example/data/gutenberg/davinci.txt` dokumentu jako dane wejściowe i wyjściowe są przechowywane w `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="86aa4-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86aa4-122">Aby uzyskać więcej informacji dotyczących tego zadania MapReduce i przykładowe dane, zobacz [MapReduce używany w Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="86aa4-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="86aa4-123">Zadanie emituje szczegóły przetwarzania i zwraca informacje podobne do następującego po zakończeniu zadania:</span><span class="sxs-lookup"><span data-stu-id="86aa4-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="86aa4-124">Po zakończeniu zadania, użyj następującego polecenia, aby wyświetlić listę plików wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="86aa4-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="86aa4-125">To polecenie wyświetla dwa pliki `_SUCCESS` i `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="86aa4-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="86aa4-126">`part-r-00000` Plik zawiera dane wyjściowe dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="86aa4-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86aa4-127">Niektóre zadania MapReduce mogą podzielone wyniki w wielu **części r-###** plików.</span><span class="sxs-lookup"><span data-stu-id="86aa4-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="86aa4-128">Jeśli tak, użyj ### przyrostka, aby wskazać kolejność plików.</span><span class="sxs-lookup"><span data-stu-id="86aa4-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="86aa4-129">Aby wyświetlić dane wyjściowe, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="86aa4-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="86aa4-130">To polecenie wyświetla listę słów, które są zawarte w **wasb://example/data/gutenberg/davinci.txt** plików i liczba wystąpił każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="86aa4-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="86aa4-131">Przykładem danych, który jest zawarty w pliku jest następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="86aa4-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="86aa4-132"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="86aa4-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="86aa4-133">Jak widać, polecenia Hadoop umożliwiają łatwe do uruchomienia zadań MapReduce w klastrze usługi HDInsight, a następnie Wyświetl dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="86aa4-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="86aa4-134"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86aa4-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="86aa4-135">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="86aa4-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="86aa4-136">Korzystać z usługi MapReduce na HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="86aa4-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="86aa4-137">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="86aa4-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="86aa4-138">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="86aa4-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="86aa4-139">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="86aa4-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
