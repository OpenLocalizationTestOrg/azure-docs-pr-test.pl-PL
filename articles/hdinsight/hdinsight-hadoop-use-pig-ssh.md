---
title: "Korzystanie z języka Hadoop Pig przy użyciu protokołu SSH w klastrze usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak łączyć się z SSH, a następnie użyć polecenia Pig do uruchomienia instrukcji Pig Latin interakcyjnego lub w trybie wsadowym klastra opartą na systemie Linux platformą Hadoop."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="a56b8-103">Uruchamianie zadań Pig na klastrze opartych na systemie Linux przy użyciu polecenia Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="a56b8-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="a56b8-104">Dowiedz się, jak interakcyjnego uruchamiania zadań Pig z połączenia SSH do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a56b8-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="a56b8-105">Język programowania Pig Latin służy do opisywania przekształceń, które są stosowane do danych wejściowych w celu utworzenia żądanego wyniku.</span><span class="sxs-lookup"><span data-stu-id="a56b8-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a56b8-106">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a56b8-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a56b8-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="a56b8-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a56b8-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="a56b8-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a56b8-109"><a id="ssh"></a>Połącz przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="a56b8-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="a56b8-110">Używanie protokołu SSH, aby nawiązać połączenie z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a56b8-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="a56b8-111">Poniższy przykład łączy do klastra o nazwie **myhdinsight** jako konta o nazwie **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="a56b8-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="a56b8-112">**Jeśli podano klucz certyfikatu dla uwierzytelniania SSH** podczas tworzenia klastra usługi HDInsight, konieczne może być Określ lokalizację klucza prywatnego na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="a56b8-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="a56b8-113">**Jeśli podano hasło dla uwierzytelniania SSH** podczas tworzenia klastra usługi HDInsight, podaj hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="a56b8-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="a56b8-114">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a56b8-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="a56b8-115"><a id="pig"></a>Użyj polecenia Pig</span><span class="sxs-lookup"><span data-stu-id="a56b8-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="a56b8-116">Po nawiązaniu połączenia, należy uruchomić Pig interfejsu wiersza polecenia (CLI) za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a56b8-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="a56b8-117">Po chwili powinna zostać wyświetlona `grunt>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="a56b8-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="a56b8-118">Wprowadź następująca instrukcja:</span><span class="sxs-lookup"><span data-stu-id="a56b8-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="a56b8-119">To polecenie ładuje zawartość pliku sample.log do DZIENNIKÓW.</span><span class="sxs-lookup"><span data-stu-id="a56b8-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="a56b8-120">Można wyświetlić zawartość pliku za pomocą następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="a56b8-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="a56b8-121">Następnie przekształcać dane za pomocą wyrażenia regularnego można wyodrębnić poziom rejestrowania z każdego rekordu przy użyciu następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="a56b8-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="a56b8-122">Można użyć **zrzutu** do wyświetlania danych po przekształceniu.</span><span class="sxs-lookup"><span data-stu-id="a56b8-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="a56b8-123">W takim przypadku należy użyć `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="a56b8-124">Kontynuować stosowanie przekształceń przy użyciu instrukcje w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="a56b8-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="a56b8-125">Pig Latin — instrukcja</span><span class="sxs-lookup"><span data-stu-id="a56b8-125">Pig Latin statement</span></span> | <span data-ttu-id="a56b8-126">Jaki jest instrukcji</span><span class="sxs-lookup"><span data-stu-id="a56b8-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="a56b8-127">Usuwa wiersze, które zawierają wartość null dla poziomu dziennika i przechowuje wyniki w `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="a56b8-128">Grupuje wiersze według poziom dziennika i przechowuje wyniki w `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="a56b8-129">Tworzy zestaw danych zawierający każdego dziennika unikatową wartość poziomu i ile razy występuje.</span><span class="sxs-lookup"><span data-stu-id="a56b8-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="a56b8-130">Zestaw danych jest przechowywany w `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="a56b8-131">Porządkuje poziomy dziennika według liczby (malejąco) i są przechowywane w `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="a56b8-132">Użyj `DUMP` do wyświetlania wyniku transformacji po każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="a56b8-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="a56b8-133">Można także zapisać wyniki przekształcania za pomocą `STORE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="a56b8-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="a56b8-134">Na przykład następująca instrukcja zapisuje `RESULT` do `/example/data/pigout` katalogu na domyślny magazyn dla klastra:</span><span class="sxs-lookup"><span data-stu-id="a56b8-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="a56b8-135">Dane są przechowywane w katalogu określonym w plikach o nazwie `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="a56b8-136">Jeśli katalog już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="a56b8-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="a56b8-137">Aby zamknąć wiersz grunt, wprowadź następującą instrukcję:</span><span class="sxs-lookup"><span data-stu-id="a56b8-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="a56b8-138">Pig Latin pliki wsadowe</span><span class="sxs-lookup"><span data-stu-id="a56b8-138">Pig Latin batch files</span></span>

<span data-ttu-id="a56b8-139">Polecenie Pig umożliwia również uruchomić Pig Latin zawarte w pliku.</span><span class="sxs-lookup"><span data-stu-id="a56b8-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="a56b8-140">Po zakończeniu wiersza grunt, użyj następującego polecenia do potoku STDIN do pliku o nazwie `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="a56b8-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="a56b8-141">Ten plik jest tworzony w katalogu macierzystego dla konta użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="a56b8-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="a56b8-142">Wpisz lub wklej poniższe wiersze, a następnie użyj klawiszy Ctrl + D po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="a56b8-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="a56b8-143">Użyj następującego polecenia do uruchomienia `pigbatch.pig` pliku za pomocą polecenia Pig.</span><span class="sxs-lookup"><span data-stu-id="a56b8-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="a56b8-144">Po zakończeniu zadania wsadowego, zapoznaj się następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a56b8-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="a56b8-145"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a56b8-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a56b8-146">Ogólne informacje na temat Pig w usłudze HDInsight zobacz następujący dokument:</span><span class="sxs-lookup"><span data-stu-id="a56b8-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="a56b8-147">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a56b8-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="a56b8-148">Aby uzyskać więcej informacji na inne sposoby pracy z platformą Hadoop w usłudze HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="a56b8-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="a56b8-149">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a56b8-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a56b8-150">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a56b8-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
