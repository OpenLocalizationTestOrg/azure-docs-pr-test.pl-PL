---
title: "aaaUse Hadoop Hive na powitania konsoli zapytania w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello opartych na sieci web konsoli zapytania toorun zapytań programu Hive w usłudze HDInsight Hadoop klastra z przeglądarki."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="f9568-103">Uruchamianie zapytań Hive przy użyciu hello konsoli zapytania</span><span class="sxs-lookup"><span data-stu-id="f9568-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="f9568-104">W tym artykule dowiesz się, jak toouse hello konsoli zapytania HDInsight toorun zapytań programu Hive w usłudze HDInsight Hadoop klastra z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f9568-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9568-105">Witaj HDInsight zapytania konsoli jest dostępna tylko w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="f9568-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="f9568-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f9568-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f9568-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="f9568-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="f9568-108">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [uruchamianie zapytań Hive w widoku Hive narzędzia Ambari](hdinsight-hadoop-use-hive-ambari-view.md) informacji na temat uruchamiania zapytań Hive z przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="f9568-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="f9568-109"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9568-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="f9568-110">toocomplete hello kroki opisane w tym artykule, należy hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="f9568-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="f9568-111">Klastra z systemem Windows usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="f9568-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="f9568-112">Nowoczesna przeglądarka sieci web</span><span class="sxs-lookup"><span data-stu-id="f9568-112">A modern web browser</span></span>

## <span data-ttu-id="f9568-113"><a id="run"></a>Uruchamianie zapytań Hive przy użyciu hello konsoli zapytania</span><span class="sxs-lookup"><span data-stu-id="f9568-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="f9568-114">Otwórz przeglądarkę sieci web i przejdź zbyt**https://CLUSTERNAME.azurehdinsight.net**, gdzie **CLUSTERNAME** jest nazwą hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9568-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="f9568-115">Jeśli zostanie wyświetlony monit, wprowadź hello nazwę użytkownika i hasło użyte podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f9568-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="f9568-116">Łącza hello u góry strony hello hello, zaznacz **Edytor Hive**.</span><span class="sxs-lookup"><span data-stu-id="f9568-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="f9568-117">Spowoduje to wyświetlenie formularza, który może być instrukcje HiveQL hello używane tooenter, które mają toorun hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9568-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![Edytor hive Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="f9568-119">Zastąp tekst hello `Select * from hivesampletable` z hello następujące instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="f9568-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="f9568-120">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="f9568-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f9568-121">**DROP TABLE**: usuwa tabeli hello i hello pliku danych, jeśli hello tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="f9568-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="f9568-122">**Tworzenie tabeli zewnętrznej**: tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="f9568-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="f9568-123">Tylko definicji tabeli hello są przechowywane w tabelach zewnętrznych w gałęzi; Hello danych pozostaje w hello oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f9568-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f9568-124">Tabele zewnętrzne należy używać oczekiwać hello podstawowych aktualizowane przez źródło zewnętrzne (na przykład procesu przekazywania danych) lub przez inną operację MapReduce toobe danych, ale zawsze mają toouse hello najnowsze dane zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="f9568-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="f9568-125">Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="f9568-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="f9568-126">**FORMAT wiersza**: informuje Hive sposób formatowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="f9568-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="f9568-127">W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="f9568-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="f9568-128">**PRZECHOWYWANE jako lokalizacji TEXTFILE**: informuje gałąź rejestru, których hello dane są przechowywane (katalog hello przykład/danych) i są przechowywane jako tekst</span><span class="sxs-lookup"><span data-stu-id="f9568-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="f9568-129">**Wybierz**: Wybierz liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartości hello **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="f9568-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="f9568-130">Powinny zostać zwrócone wartości **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="f9568-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="f9568-131">**INPUT__FILE__NAME takich jak "%.log"** -informuje, który mamy powinno zwrócić tylko danych z plików w gałęzi. dziennika.</span><span class="sxs-lookup"><span data-stu-id="f9568-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="f9568-132">To ogranicza hello wyszukiwania toohello sample.log pliku, który zawiera dane hello utrzymuje je z zwracać dane z innych przykładowe pliki danych, która nie pasuje do schematu hello zdefiniowanego.</span><span class="sxs-lookup"><span data-stu-id="f9568-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="f9568-133">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="f9568-133">Click **Submit**.</span></span> <span data-ttu-id="f9568-134">Witaj **sesji zadania** na powitania u dołu strony hello powinien być wyświetlany szczegóły dotyczące hello zadania.</span><span class="sxs-lookup"><span data-stu-id="f9568-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="f9568-135">Gdy hello **stan** pola zmiany zbyt**Ukończono**, wybierz pozycję **Wyświetl szczegóły** hello zadania.</span><span class="sxs-lookup"><span data-stu-id="f9568-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="f9568-136">Na stronie szczegółów hello hello **dane wyjściowe zadania** zawiera `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="f9568-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="f9568-137">Można użyć hello **Pobierz** przycisk pod tym toodownload pole plik zawierający dane wyjściowe hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="f9568-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="f9568-138"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f9568-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="f9568-139">Jak widać, powitalne Konsola zapytania zapewnia prosty sposób toorun zapytania Hive w programie klastra usługi HDInsight, monitorować stan zadania hello i pobrać dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="f9568-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="f9568-140">Wybierz toolearn więcej informacji na temat przy użyciu konsoli zapytania Hive toorun zadań Hive, **wprowadzenie** u góry hello hello konsoli zapytania, a następnie użyć hello przykłady, które są udostępniane.</span><span class="sxs-lookup"><span data-stu-id="f9568-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="f9568-141">Każda próbka przeprowadzi Cię przez proces hello przy użyciu danych tooanalyze gałęzi, w tym objaśnienia dotyczące instrukcje HiveQL hello używane w przykładowym hello.</span><span class="sxs-lookup"><span data-stu-id="f9568-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="f9568-142"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9568-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f9568-143">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f9568-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="f9568-144">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9568-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="f9568-145">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f9568-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f9568-146">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9568-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f9568-147">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9568-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f9568-148">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów dla informacji debugowania:</span><span class="sxs-lookup"><span data-stu-id="f9568-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="f9568-149">Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f9568-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="f9568-150">Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f9568-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
