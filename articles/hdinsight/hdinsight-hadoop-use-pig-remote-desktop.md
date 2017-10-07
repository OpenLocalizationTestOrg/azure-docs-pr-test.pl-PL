---
title: "aaaUse Hadoop Pig przy użyciu pulpitu zdalnego w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Pig toorun Pig Latin instrukcje z klastra platformy Hadoop działającej w systemie Windows tooa połączenia pulpitu zdalnego w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="77b96-103">Uruchamianie zadań Pig połączenie pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="77b96-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="77b96-104">Ten dokument zawiera wskazówki dotyczące korzystania z hello Pig polecenia toorun Pig Latin instrukcji z klastra usługi HDInsight opartej na systemie Windows tooa połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="77b96-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="77b96-105">Pig Latin umożliwia aplikacji MapReduce toocreate przez opisywania przekształceń danych, a nie mapy i zmniejszyć funkcji.</span><span class="sxs-lookup"><span data-stu-id="77b96-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77b96-106">Pulpit zdalny jest dostępna tylko w klastrach HDInsight, które używają systemu Windows jako system operacyjny hello.</span><span class="sxs-lookup"><span data-stu-id="77b96-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="77b96-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="77b96-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="77b96-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="77b96-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="77b96-109">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [Use Pig HDInsight i SSH](hdinsight-hadoop-use-pig-ssh.md) informacji na temat interakcyjnego uruchamiania Pig zadania bezpośrednio na powitania klastra z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="77b96-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="77b96-110"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77b96-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="77b96-111">toocomplete hello kroki opisane w tym artykule, należy hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="77b96-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="77b96-112">Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="77b96-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="77b96-113">Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7</span><span class="sxs-lookup"><span data-stu-id="77b96-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="77b96-114"><a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="77b96-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="77b96-115">Włączenie pulpitu zdalnego dla klastra usługi HDInsight hello, a następnie połącz tooit, wykonując następujące instrukcje hello [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="77b96-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="77b96-116"><a id="pig"></a>Użyj polecenia Pig hello</span><span class="sxs-lookup"><span data-stu-id="77b96-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="77b96-117">Po utworzeniu połączenia pulpitu zdalnego, należy rozpocząć hello **wiersza polecenia platformy Hadoop** przy użyciu hello ikony na pulpicie hello.</span><span class="sxs-lookup"><span data-stu-id="77b96-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="77b96-118">Użyj następującego polecenia Pig hello toostart hello:</span><span class="sxs-lookup"><span data-stu-id="77b96-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="77b96-119">Użytkownik zobaczy `grunt>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="77b96-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="77b96-120">Wprowadź hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="77b96-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="77b96-121">To polecenie ładuje hello zawartość pliku sample.log hello do hello plików DZIENNIKÓW.</span><span class="sxs-lookup"><span data-stu-id="77b96-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="77b96-122">Witaj zawartość pliku hello można wyświetlić przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="77b96-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="77b96-123">Przekształć dane hello stosując poziom tooextract tylko hello rejestrowania wyrażenia regularnego z każdego rekordu:</span><span class="sxs-lookup"><span data-stu-id="77b96-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="77b96-124">Można użyć **zrzutu** tooview hello danych po przekształceniu hello.</span><span class="sxs-lookup"><span data-stu-id="77b96-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="77b96-125">W takim przypadku `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="77b96-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="77b96-126">Kontynuować stosowanie przekształceń przy użyciu hello następujące instrukcje.</span><span class="sxs-lookup"><span data-stu-id="77b96-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="77b96-127">Użyj `DUMP` tooview hello wynik transformacji powitania po każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="77b96-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="77b96-128">— Instrukcja</span><span class="sxs-lookup"><span data-stu-id="77b96-128">Statement</span></span></th><th><span data-ttu-id="77b96-129">Wyniki działania</span><span class="sxs-lookup"><span data-stu-id="77b96-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="77b96-130">FILTEREDLEVELS = poziomy filtru przez LOGLEVEL nie ma wartości null;</span><span class="sxs-lookup"><span data-stu-id="77b96-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="77b96-131">Usuwa wiersze, które zawierają wartość null dla poziomu dziennika hello i przechowuje wyniki hello do FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="77b96-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="77b96-132">GROUPEDLEVELS = FILTEREDLEVELS grupy przez LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="77b96-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="77b96-133">Hello grup wierszy przez poziom dziennika i przechowuje wyniki hello do GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="77b96-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="77b96-134">CZĘSTOTLIWOŚCI = foreach GROUPEDLEVELS Generowanie grupy jako LOGLEVEL, COUNT (FILTEREDLEVELS. LOGLEVEL) jako liczba;</span><span class="sxs-lookup"><span data-stu-id="77b96-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="77b96-135">Tworzy nowy zestaw danych zawierający każdego dziennika unikatową wartość poziomu i ile razy występuje.</span><span class="sxs-lookup"><span data-stu-id="77b96-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="77b96-136">To jest przechowywane w częstotliwości</span><span class="sxs-lookup"><span data-stu-id="77b96-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="77b96-137">WYNIK = kolejności częstotliwości przez liczbę desc;</span><span class="sxs-lookup"><span data-stu-id="77b96-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="77b96-138">Porządkuje hello poziomy dziennika według liczby (malejąco) i magazyny do wyniku</span><span class="sxs-lookup"><span data-stu-id="77b96-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="77b96-139">
6.Można także zapisać wyniki hello przekształcania za pomocą hello `STORE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="77b96-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="77b96-140">Na przykład następujące polecenie hello zapisuje hello `RESULT` toohello **/example/data/pigout** katalogu w hello domyślnego kontenera magazynu dla klastra:</span><span class="sxs-lookup"><span data-stu-id="77b96-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="77b96-141">Hello dane są przechowywane w katalogu określonym hello w plikach o nazwie **nnnnn części**.</span><span class="sxs-lookup"><span data-stu-id="77b96-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="77b96-142">Jeśli istnieje już katalog hello, otrzymasz komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="77b96-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="77b96-143">Witaj tooexit o tej grunt monit, wprowadź powitania po instrukcji.</span><span class="sxs-lookup"><span data-stu-id="77b96-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="77b96-144">Pig Latin pliki wsadowe</span><span class="sxs-lookup"><span data-stu-id="77b96-144">Pig Latin batch files</span></span>
<span data-ttu-id="77b96-145">Umożliwia także hello Pig polecenia toorun Pig Latin, który jest zawarty w pliku.</span><span class="sxs-lookup"><span data-stu-id="77b96-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="77b96-146">Po zakończeniu hello grunt wiersza, otwórz **Notatnik** i Utwórz nowy plik o nazwie **pigbatch.pig** w hello **PIG_HOME %** katalogu.</span><span class="sxs-lookup"><span data-stu-id="77b96-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="77b96-147">Wpisz lub Wklej hello następujące wiersze do hello **pigbatch.pig** pliku, a następnie zapisz go:</span><span class="sxs-lookup"><span data-stu-id="77b96-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="77b96-148">Użyj powitania po toorun hello **pigbatch.pig** pliku za pomocą polecenia pig hello.</span><span class="sxs-lookup"><span data-stu-id="77b96-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="77b96-149">Po zakończeniu wykonywania zadania wsadowego hello powinna zostać wyświetlona hello następujące dane wyjściowe, które powinny być hello sam jako gdy używane `DUMP RESULT;` w poprzednich krokach hello:</span><span class="sxs-lookup"><span data-stu-id="77b96-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="77b96-150"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="77b96-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="77b96-151">Jak widać, hello polecenia Pig umożliwia toointeractively uruchamiania operacji MapReduce lub uruchamianie zadań Pig Latin, które są przechowywane w pliku wsadowym.</span><span class="sxs-lookup"><span data-stu-id="77b96-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="77b96-152"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77b96-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="77b96-153">Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77b96-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="77b96-154">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="77b96-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="77b96-155">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77b96-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="77b96-156">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="77b96-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="77b96-157">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="77b96-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
