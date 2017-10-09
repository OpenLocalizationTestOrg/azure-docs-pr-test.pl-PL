---
title: "aaaUse Hadoop Pig przy użyciu protokołu SSH w klastrze usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć tooa opartych na systemie Linux klastra usługi Hadoop przy użyciu protokołu SSH, a następnie hello Pig polecenia toorun Pig Latin instrukcji interakcyjnego lub jako partii zadań."
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
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="14fd7-103">Uruchamianie zadań Pig na opartych na systemie Linux klaster o hello polecenia Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="14fd7-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="14fd7-104">Dowiedz się, jak toointeractively uruchamiania zadań Pig z klastra usługi HDInsight tooyour połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="14fd7-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="14fd7-105">Witaj język programowania Pig Latin umożliwia toodescribe transformacje, których są stosowane toohello wejściowych danych tooproduce hello potrzebne w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="14fd7-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14fd7-106">Witaj czynności w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="14fd7-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="14fd7-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="14fd7-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="14fd7-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="14fd7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="14fd7-109"><a id="ssh"></a>Połącz przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="14fd7-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="14fd7-110">Użyj klastra usługi HDInsight tooyour tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="14fd7-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="14fd7-111">Witaj poniższy przykład łączy tooa klastra o nazwie **myhdinsight** jako hello konta o nazwie **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="14fd7-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="14fd7-112">**Jeśli podano klucz certyfikatu dla uwierzytelniania SSH** podczas tworzenia klastra usługi HDInsight hello może być konieczne lokalizacji hello toospecify hello klucza prywatnego na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="14fd7-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="14fd7-113">**Jeśli podano hasło dla uwierzytelniania SSH** podczas tworzenia klastra usługi HDInsight hello hello hasło po wyświetleniu monitu podaj.</span><span class="sxs-lookup"><span data-stu-id="14fd7-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="14fd7-114">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="14fd7-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="14fd7-115"><a id="pig"></a>Użyj polecenia Pig hello</span><span class="sxs-lookup"><span data-stu-id="14fd7-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="14fd7-116">Po nawiązaniu połączenia, należy uruchomić hello Pig wiersza polecenia (CLI) przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="14fd7-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="14fd7-117">Po chwili powinna zostać wyświetlona `grunt>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="14fd7-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="14fd7-118">Wprowadź hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="14fd7-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="14fd7-119">To polecenie ładuje hello zawartość pliku sample.log hello w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="14fd7-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="14fd7-120">Witaj zawartość pliku hello można wyświetlić przy użyciu hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="14fd7-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="14fd7-121">Następnie przekształcania danych hello stosując poziom tooextract tylko hello rejestrowania wyrażenia regularnego z każdego rekordu przy użyciu hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="14fd7-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="14fd7-122">Można użyć **zrzutu** tooview hello danych po przekształceniu hello.</span><span class="sxs-lookup"><span data-stu-id="14fd7-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="14fd7-123">W takim przypadku należy użyć `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="14fd7-124">Kontynuować stosowanie przekształceń za pomocą instrukcji hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="14fd7-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="14fd7-125">Pig Latin — instrukcja</span><span class="sxs-lookup"><span data-stu-id="14fd7-125">Pig Latin statement</span></span> | <span data-ttu-id="14fd7-126">Jakie instrukcji hello jest</span><span class="sxs-lookup"><span data-stu-id="14fd7-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="14fd7-127">Usuwa wiersze, które zawierają wartość null dla poziomu dziennika hello i przechowuje wyniki hello do `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="14fd7-128">Hello grup wierszy przez poziom dziennika i przechowuje wyniki hello do `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="14fd7-129">Tworzy zestaw danych zawierający każdego dziennika unikatową wartość poziomu i ile razy występuje.</span><span class="sxs-lookup"><span data-stu-id="14fd7-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="14fd7-130">zestaw danych Hello jest przechowywany w `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="14fd7-131">Porządkuje poziomy dziennika hello według liczby (malejąco) i są przechowywane w `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="14fd7-132">Użyj `DUMP` tooview hello wynik transformacji powitania po każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="14fd7-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="14fd7-133">Można także zapisać wyniki hello przekształcania za pomocą hello `STORE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="14fd7-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="14fd7-134">Na przykład po instrukcji hello zapisuje hello `RESULT` toohello `/example/data/pigout` katalogu na powitania domyślny magazyn dla klastra:</span><span class="sxs-lookup"><span data-stu-id="14fd7-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="14fd7-135">Hello dane są przechowywane w katalogu określonym hello w plikach o nazwie `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="14fd7-136">Jeśli hello katalog już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="14fd7-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="14fd7-137">Witaj tooexit o tej grunt monit, wprowadź hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="14fd7-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="14fd7-138">Pig Latin pliki wsadowe</span><span class="sxs-lookup"><span data-stu-id="14fd7-138">Pig Latin batch files</span></span>

<span data-ttu-id="14fd7-139">Umożliwia także hello Pig polecenia toorun Pig Latin zawarte w pliku.</span><span class="sxs-lookup"><span data-stu-id="14fd7-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="14fd7-140">Po zakończeniu hello grunt wiersza, użyj hello następujące polecenie toopipe STDIN do pliku o nazwie `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="14fd7-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="14fd7-141">Ten plik jest tworzony w katalogu macierzystym hello hello konta użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="14fd7-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="14fd7-142">Wpisz lub Wklej hello następujące wiersze, a następnie użyj klawiszy Ctrl + D po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="14fd7-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="14fd7-143">Użyj hello następujące polecenie toorun hello `pigbatch.pig` pliku za pomocą polecenia Pig hello.</span><span class="sxs-lookup"><span data-stu-id="14fd7-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="14fd7-144">Po zakończeniu zadania wsadowego hello, zapoznaj się hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="14fd7-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="14fd7-145"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14fd7-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="14fd7-146">Ogólne informacje na temat Pig w usłudze HDInsight zobacz następujące dokumentu hello:</span><span class="sxs-lookup"><span data-stu-id="14fd7-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="14fd7-147">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="14fd7-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="14fd7-148">Aby uzyskać więcej informacji na inne sposoby toowork z platformą Hadoop w usłudze HDInsight Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="14fd7-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="14fd7-149">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="14fd7-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="14fd7-150">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="14fd7-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
