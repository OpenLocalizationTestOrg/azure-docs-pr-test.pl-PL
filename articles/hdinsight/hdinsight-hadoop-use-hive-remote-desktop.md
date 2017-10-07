---
title: "aaaUse Hadoop Hive i pulpitu zdalnego w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooHadoop klastra w usłudze HDInsight przy użyciu pulpitu zdalnego, a następnie uruchom zapytań programu Hive za pomocą hello Hive interfejsu wiersza polecenia."
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
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="f8d19-103">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="f8d19-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="f8d19-104">W tym artykule dowiesz się, jak tooan tooconnect HDInsight klastra przy użyciu pulpitu zdalnego, a następnie uruchom Hive zapytania przy użyciu hello Hive interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="f8d19-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8d19-105">Pulpit zdalny jest dostępna tylko w klastrach HDInsight, które używają systemu Windows jako system operacyjny hello.</span><span class="sxs-lookup"><span data-stu-id="f8d19-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="f8d19-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f8d19-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f8d19-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="f8d19-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="f8d19-108">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [używanie Hive z HDInsight i Beeline](hdinsight-hadoop-use-hive-beeline.md) informacji na temat uruchamiania zapytań Hive bezpośrednio w klastrze hello z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f8d19-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="f8d19-109"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f8d19-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="f8d19-110">toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f8d19-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="f8d19-111">Klastra z systemem Windows HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f8d19-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="f8d19-112">Komputer kliencki z systemem Windows 10, Windows 8 lub Windows 7</span><span class="sxs-lookup"><span data-stu-id="f8d19-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="f8d19-113"><a id="connect"></a>Uzyskuj dostęp do usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="f8d19-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="f8d19-114">Włączenie pulpitu zdalnego dla klastra usługi HDInsight hello, a następnie połącz tooit, wykonując następujące instrukcje hello [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="f8d19-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="f8d19-115"><a id="hive"></a>Polecenie gałęzi hello</span><span class="sxs-lookup"><span data-stu-id="f8d19-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="f8d19-116">Po podłączeniu pulpitu toohello dla klastra usługi HDInsight hello za pomocą hello następujące kroki toowork z gałęzi:</span><span class="sxs-lookup"><span data-stu-id="f8d19-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="f8d19-117">Na pulpicie HDInsight hello start hello **wiersza polecenia usługi Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="f8d19-118">Wprowadź hello następujące polecenia toostart hello Hive interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="f8d19-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="f8d19-119">Rozpoczęto hello interfejsu wiersza polecenia, można zobaczyć w wierszu Hive CLI hello: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="f8d19-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="f8d19-120">Używając hello interfejsu wiersza polecenia, wprowadź następujące instrukcje toocreate nowej tabeli o nazwie hello **log4jLogs** przy użyciu przykładowych danych:</span><span class="sxs-lookup"><span data-stu-id="f8d19-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="f8d19-121">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="f8d19-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f8d19-122">**DROP TABLE**: usuwa tabeli hello i hello pliku danych, jeśli hello tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="f8d19-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="f8d19-123">**Tworzenie tabeli zewnętrznej**: tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="f8d19-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="f8d19-124">Tabele zewnętrzne przechowywać tylko definicji tabeli hello w gałęzi (powitalne pozostanie danych w oryginalnej lokalizacji hello).</span><span class="sxs-lookup"><span data-stu-id="f8d19-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="f8d19-125">Tabele zewnętrzne należy używać oczekiwać hello podstawowych aktualizowane przez źródło zewnętrzne (na przykład procesu przekazywania danych) lub przez inną operację MapReduce toobe danych, ale zawsze mają toouse hello najnowsze dane zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="f8d19-126">Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="f8d19-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="f8d19-127">**FORMAT wiersza**: informuje Hive sposób formatowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="f8d19-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="f8d19-128">W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="f8d19-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="f8d19-129">**PRZECHOWYWANE jako lokalizacji TEXTFILE**: informuje gałąź rejestru, których hello dane są przechowywane (katalog hello przykład/danych) i są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="f8d19-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="f8d19-130">**Wybierz**: wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość hello **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="f8d19-131">Powinny zostać zwrócone wartości **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="f8d19-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="f8d19-132">**INPUT__FILE__NAME takich jak "%.log"** -informuje, który mamy powinno zwrócić tylko danych z plików w gałęzi. dziennika.</span><span class="sxs-lookup"><span data-stu-id="f8d19-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="f8d19-133">To ogranicza hello wyszukiwania toohello sample.log pliku, który zawiera dane hello utrzymuje je z zwracać dane z innych przykładowe pliki danych, która nie pasuje do schematu hello zdefiniowanego.</span><span class="sxs-lookup"><span data-stu-id="f8d19-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="f8d19-134">Użyj hello następujące instrukcje toocreate nową tabelę "internal" o nazwie **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="f8d19-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="f8d19-135">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="f8d19-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f8d19-136">**Utwórz Tabela Jeśli nie ISTNIEJE**: tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f8d19-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="f8d19-137">Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używany, to wewnętrznej tabeli, który jest przechowywany w magazynie danych Hive hello i zarządza całkowicie Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f8d19-138">W odróżnieniu od **zewnętrznych** tabel, również porzucenie wewnętrznej tabeli usuwa hello podstawowych danych.</span><span class="sxs-lookup"><span data-stu-id="f8d19-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="f8d19-139">**ORC AS PRZECHOWYWANE**: hello ilość danych przechowywana w zoptymalizowaną wiersza tabelarycznego (ORC).</span><span class="sxs-lookup"><span data-stu-id="f8d19-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="f8d19-140">Jest to wysoce zoptymalizowane i wydajne format do przechowywania danych Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="f8d19-141">**ZASTĄP INSERT... Wybierz**: wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie wstawia hello danych do hello **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="f8d19-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="f8d19-142">tooverify, który tylko wiersze, które zawierają **[Błąd]** w t4 kolumnie były przechowywane toohello **errorLogs** tabeli, należy użyć powitania po instrukcji tooreturn hello wszystkie wiersze z **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="f8d19-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="f8d19-143">Wybierz * z errorLogs;</span><span class="sxs-lookup"><span data-stu-id="f8d19-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="f8d19-144">Trzy wiersze danych ma zostać zwrócony, zawierający wszystkie **[Błąd]** w t4 kolumny.</span><span class="sxs-lookup"><span data-stu-id="f8d19-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="f8d19-145"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f8d19-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="f8d19-146">Jak widać, hello hello polecenie gałęzi zawiera toointeractively łatwe uruchamianie zapytań Hive w klastrze usługi HDInsight, monitor hello stan zadania i pobrać dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="f8d19-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="f8d19-147"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8d19-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f8d19-148">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f8d19-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="f8d19-149">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="f8d19-150">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f8d19-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f8d19-151">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f8d19-152">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f8d19-153">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów dla informacji debugowania:</span><span class="sxs-lookup"><span data-stu-id="f8d19-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="f8d19-154">Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f8d19-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="f8d19-155">Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f8d19-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
