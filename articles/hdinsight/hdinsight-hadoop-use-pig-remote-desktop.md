---
title: "Korzystanie z języka Pig Hadoop przy użyciu pulpitu zdalnego w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać polecenia Pig do uruchomienia instrukcji Pig Latin połączenie pulpitu zdalnego do klastra z systemem Windows Hadoop w usłudze HDInsight."
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="198c1-103">Uruchamianie zadań Pig połączenie pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="198c1-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="198c1-104">Ten dokument zawiera wskazówki dotyczące korzystania z polecenia Pig do uruchomienia instrukcji Pig Latin połączenie pulpitu zdalnego do klastra usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="198c1-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="198c1-105">Pig Latin umożliwia tworzenie aplikacji MapReduce przez opisywania przekształceń danych, a nie mapy i zmniejszyć funkcji.</span><span class="sxs-lookup"><span data-stu-id="198c1-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="198c1-106">Pulpit zdalny jest dostępna tylko w klastrach HDInsight, które używają systemu Windows jako system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="198c1-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="198c1-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="198c1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="198c1-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="198c1-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="198c1-109">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [Use Pig HDInsight i SSH](hdinsight-hadoop-use-pig-ssh.md) informacji na temat interakcyjnego uruchamiania zadań Pig bezpośrednio w klastrze z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="198c1-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="198c1-110"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="198c1-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="198c1-111">Aby wykonać kroki opisane w tym artykule, potrzebne następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="198c1-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="198c1-112">Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="198c1-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="198c1-113">Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7</span><span class="sxs-lookup"><span data-stu-id="198c1-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="198c1-114"><a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="198c1-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="198c1-115">Włączenie pulpitu zdalnego dla klastra usługi HDInsight, a następnie nawiązać zgodnie z instrukcjami w [Connect do klastrów usługi HDInsight za pomocą protokołu RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="198c1-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="198c1-116"><a id="pig"></a>Użyj polecenia Pig</span><span class="sxs-lookup"><span data-stu-id="198c1-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="198c1-117">Po utworzeniu połączenia pulpitu zdalnego rozpocząć **wiersza polecenia platformy Hadoop** przy użyciu ikony na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="198c1-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="198c1-118">Aby uruchomić polecenie Pig, skorzystaj z następujących:</span><span class="sxs-lookup"><span data-stu-id="198c1-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="198c1-119">Użytkownik zobaczy `grunt>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="198c1-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="198c1-120">Wprowadź następująca instrukcja:</span><span class="sxs-lookup"><span data-stu-id="198c1-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="198c1-121">To polecenie ładuje zawartość pliku sample.log do plików DZIENNIKÓW.</span><span class="sxs-lookup"><span data-stu-id="198c1-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="198c1-122">Można wyświetlić zawartość pliku za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="198c1-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="198c1-123">Przekształcanie danych za pomocą wyrażenia regularnego można wyodrębnić poziom rejestrowania z każdego rekordu:</span><span class="sxs-lookup"><span data-stu-id="198c1-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="198c1-124">Można użyć **zrzutu** do wyświetlania danych po przekształceniu.</span><span class="sxs-lookup"><span data-stu-id="198c1-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="198c1-125">W takim przypadku `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="198c1-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="198c1-126">Kontynuować stosowanie przekształceń za pomocą następujących instrukcji.</span><span class="sxs-lookup"><span data-stu-id="198c1-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="198c1-127">Użyj `DUMP` do wyświetlania wyniku transformacji po każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="198c1-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="198c1-128">— Instrukcja</span><span class="sxs-lookup"><span data-stu-id="198c1-128">Statement</span></span></th><th><span data-ttu-id="198c1-129">Wyniki działania</span><span class="sxs-lookup"><span data-stu-id="198c1-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="198c1-130">FILTEREDLEVELS = poziomy filtru przez LOGLEVEL nie ma wartości null;</span><span class="sxs-lookup"><span data-stu-id="198c1-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="198c1-131">Usuwa wiersze, które zawierają wartość null dla poziomu dziennika i przechowuje wyniki w FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="198c1-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="198c1-132">GROUPEDLEVELS = FILTEREDLEVELS grupy przez LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="198c1-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="198c1-133">Grupuje wiersze według poziom dziennika i przechowuje wyniki w GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="198c1-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="198c1-134">CZĘSTOTLIWOŚCI = foreach GROUPEDLEVELS Generowanie grupy jako LOGLEVEL, COUNT (FILTEREDLEVELS. LOGLEVEL) jako liczba;</span><span class="sxs-lookup"><span data-stu-id="198c1-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="198c1-135">Tworzy nowy zestaw danych zawierający każdego dziennika unikatową wartość poziomu i ile razy występuje.</span><span class="sxs-lookup"><span data-stu-id="198c1-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="198c1-136">To jest przechowywane w częstotliwości</span><span class="sxs-lookup"><span data-stu-id="198c1-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="198c1-137">WYNIK = kolejności częstotliwości przez liczbę desc;</span><span class="sxs-lookup"><span data-stu-id="198c1-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="198c1-138">Porządkuje poziomy dziennika według liczby (malejąco) i są przechowywane w wyniku</span><span class="sxs-lookup"><span data-stu-id="198c1-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="198c1-139">
6.Można także zapisać wyniki przekształcania za pomocą `STORE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="198c1-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="198c1-140">Na przykład następujące polecenie zapisuje `RESULT` do **/example/data/pigout** katalogu w domyślnego kontenera magazynu dla klastra:</span><span class="sxs-lookup"><span data-stu-id="198c1-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="198c1-141">Dane są przechowywane w katalogu określonym w plikach o nazwie **nnnnn części**.</span><span class="sxs-lookup"><span data-stu-id="198c1-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="198c1-142">Jeśli katalog już istnieje, zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="198c1-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="198c1-143">Aby zamknąć wiersz grunt, wprowadź następującą instrukcję.</span><span class="sxs-lookup"><span data-stu-id="198c1-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="198c1-144">Pig Latin pliki wsadowe</span><span class="sxs-lookup"><span data-stu-id="198c1-144">Pig Latin batch files</span></span>
<span data-ttu-id="198c1-145">Polecenie Pig umożliwia również uruchomić Pig Latin, który jest zawarty w pliku.</span><span class="sxs-lookup"><span data-stu-id="198c1-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="198c1-146">Po zakończeniu wiersza grunt, otwórz **Notatnik** i Utwórz nowy plik o nazwie **pigbatch.pig** w **PIG_HOME %** katalogu.</span><span class="sxs-lookup"><span data-stu-id="198c1-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="198c1-147">Wpisz lub wklej następujące wiersze do **pigbatch.pig** pliku, a następnie zapisz go:</span><span class="sxs-lookup"><span data-stu-id="198c1-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="198c1-148">Użyj następujących czynności, aby uruchomić **pigbatch.pig** plików za pomocą polecenia pig.</span><span class="sxs-lookup"><span data-stu-id="198c1-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="198c1-149">Po zakończeniu zadania wsadowego, powinny pojawić się następujące dane wyjściowe, która powinna być taka sama jak kiedy używany `DUMP RESULT;` w poprzednich krokach:</span><span class="sxs-lookup"><span data-stu-id="198c1-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="198c1-150"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="198c1-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="198c1-151">Jak widać, polecenie Pig umożliwia interakcyjnego uruchamiania operacji MapReduce lub uruchamianie zadań Pig Latin, które są przechowywane w pliku wsadowym.</span><span class="sxs-lookup"><span data-stu-id="198c1-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="198c1-152"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="198c1-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="198c1-153">Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="198c1-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="198c1-154">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="198c1-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="198c1-155">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="198c1-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="198c1-156">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="198c1-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="198c1-157">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="198c1-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
