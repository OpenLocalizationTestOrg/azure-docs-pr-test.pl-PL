---
title: "Użyj usługi Hadoop Hive i pulpitu zdalnego w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nawiązywania połączenia z klastrem usługi Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego, a następnie uruchom zapytań programu Hive za pomocą interfejsu wiersza polecenia Hive."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="bad75-103">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="bad75-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="bad75-104">W tym artykule będzie Dowiedz się, jak nawiązać połączenia z klastrem usługi HDInsight przy użyciu pulpitu zdalnego, a następnie uruchom zapytań Hive przy użyciu Hive interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="bad75-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bad75-105">Pulpit zdalny jest dostępna tylko w klastrach HDInsight, które używają systemu Windows jako system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="bad75-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="bad75-106">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="bad75-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bad75-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="bad75-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="bad75-108">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [używanie Hive z HDInsight i Beeline](hdinsight-hadoop-use-hive-beeline.md) informacji na temat uruchamiania zapytań Hive bezpośrednio w klastrze z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="bad75-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="bad75-109"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bad75-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="bad75-110">Aby wykonać kroki opisane w tym artykule, będą potrzebne następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bad75-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="bad75-111">Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="bad75-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="bad75-112">Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7</span><span class="sxs-lookup"><span data-stu-id="bad75-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="bad75-113"><a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="bad75-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="bad75-114">Włączenie pulpitu zdalnego dla klastra usługi HDInsight, a następnie nawiązać zgodnie z instrukcjami w [Connect do klastrów usługi HDInsight za pomocą protokołu RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="bad75-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="bad75-115"><a id="hive"></a>Użyj polecenia gałęzi</span><span class="sxs-lookup"><span data-stu-id="bad75-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="bad75-116">Po podłączeniu do pulpitu dla klastra usługi HDInsight, wykonaj następujące kroki pracy z gałęzi:</span><span class="sxs-lookup"><span data-stu-id="bad75-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="bad75-117">Z poziomu pulpitu HDInsight start **wiersza polecenia usługi Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="bad75-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="bad75-118">Wprowadź następujące polecenie, aby uruchomić interfejs wiersza polecenia Hive:</span><span class="sxs-lookup"><span data-stu-id="bad75-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="bad75-119">Rozpoczęto interfejsu wiersza polecenia, można zobaczyć w wierszu polecenia programu Hive interfejsu wiersza polecenia: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="bad75-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="bad75-120">Przy użyciu interfejsu wiersza polecenia, wpisz poniższe instrukcje, aby utworzyć nową tabelę o nazwie **log4jLogs** przy użyciu przykładowych danych:</span><span class="sxs-lookup"><span data-stu-id="bad75-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="bad75-121">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bad75-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="bad75-122">**DROP TABLE**: usuwa tabeli i plik danych, jeśli tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="bad75-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="bad75-123">**Tworzenie tabeli zewnętrznej**: tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="bad75-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="bad75-124">Tabele zewnętrzne przechowywać tylko definicji tabeli w gałęzi rejestru (danych pozostaje w oryginalnej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="bad75-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="bad75-125">Jeśli oczekujesz danych do zaktualizowania przez źródło zewnętrzne (na przykład procesu przekazywania danych) lub przez inną operację MapReduce, należy użyć tabel zewnętrznych, ale ma zawsze zapytań programu Hive za pomocą najnowszych danych.</span><span class="sxs-lookup"><span data-stu-id="bad75-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="bad75-126">Usunięcie tabeli zewnętrznej jest **nie** Usuń dane, definicję tabeli.</span><span class="sxs-lookup"><span data-stu-id="bad75-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="bad75-127">**FORMAT wiersza**: Określa, że Hive, jak dane są sformatowane.</span><span class="sxs-lookup"><span data-stu-id="bad75-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="bad75-128">W takim przypadku pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="bad75-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="bad75-129">**PRZECHOWYWANE jako lokalizacji TEXTFILE**: informuje gałąź rejestru, których dane są przechowywane (katalogu przykładzie/danych) i są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="bad75-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="bad75-130">**Wybierz**: wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="bad75-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="bad75-131">Powinny zostać zwrócone wartości **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="bad75-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="bad75-132">**INPUT__FILE__NAME takich jak "%.log"** -informuje, który mamy powinno zwrócić tylko danych z plików w gałęzi. dziennika.</span><span class="sxs-lookup"><span data-stu-id="bad75-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="bad75-133">To ogranicza wyszukiwanie do pliku sample.log, który zawiera dane, a następnie utrzymuje je z zwracać dane z innych przykładowe pliki danych, która nie pasuje do schematu, zdefiniowanego.</span><span class="sxs-lookup"><span data-stu-id="bad75-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="bad75-134">Poniższe instrukcje umożliwiają utworzenie nowej tabeli "internal" o nazwie **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="bad75-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="bad75-135">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bad75-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="bad75-136">**Utwórz Tabela Jeśli nie ISTNIEJE**: tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="bad75-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="bad75-137">Ponieważ **zewnętrznych** — słowo kluczowe nie jest używany, to wewnętrznej tabeli, która jest przechowywana w magazynie danych programu Hive i zarządza całkowicie Hive.</span><span class="sxs-lookup"><span data-stu-id="bad75-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="bad75-138">W odróżnieniu od **zewnętrznych** tabel, również porzucenie wewnętrznej tabeli powoduje usunięcie danych.</span><span class="sxs-lookup"><span data-stu-id="bad75-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="bad75-139">**ORC AS PRZECHOWYWANE**: przechowuje dane w formacie (ORC) kolumnowym zoptymalizowane wiersza.</span><span class="sxs-lookup"><span data-stu-id="bad75-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="bad75-140">Jest to wysoce zoptymalizowane i wydajne format do przechowywania danych Hive.</span><span class="sxs-lookup"><span data-stu-id="bad75-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="bad75-141">**ZASTĄP INSERT... Wybierz**: wybiera wiersze z **log4jLogs** tabeli, która zawiera **[Błąd]**, następnie wstawia dane do **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="bad75-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="bad75-142">Aby zweryfikować, że tylko wiersze zawierające **[Błąd]** w kolumnie były przechowywane t4 **errorLogs** tabeli, użyj poniższych instrukcji, aby zwracanie wszystkich wierszy z **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="bad75-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="bad75-143">Wybierz * z errorLogs;</span><span class="sxs-lookup"><span data-stu-id="bad75-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="bad75-144">Trzy wiersze danych ma zostać zwrócony, zawierający wszystkie **[Błąd]** w t4 kolumny.</span><span class="sxs-lookup"><span data-stu-id="bad75-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="bad75-145"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="bad75-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="bad75-146">Jak widać, polecenie gałęzi udostępnia prostą metodą interakcyjnego uruchamianie zapytań Hive w klastrze usługi HDInsight, monitorować stan zadania i pobrać dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="bad75-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="bad75-147"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bad75-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="bad75-148">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="bad75-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="bad75-149">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bad75-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="bad75-150">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="bad75-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="bad75-151">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bad75-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="bad75-152">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bad75-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="bad75-153">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz informacji o debugowaniu w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="bad75-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="bad75-154">Użyj interfejsu użytkownika aplikacji Tez w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bad75-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="bad75-155">Użyj widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="bad75-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
