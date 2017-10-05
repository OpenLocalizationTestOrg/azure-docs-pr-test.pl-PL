---
title: "Korzystanie z programu Hadoop Hive w konsoli zapytania w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu konsoli zapytania oparte na sieci web do uruchamiania zapytań Hive w klastrze usługi HDInsight Hadoop w przeglądarce."
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
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="a7309-103">Uruchamianie zapytań Hive przy użyciu konsoli zapytania</span><span class="sxs-lookup"><span data-stu-id="a7309-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="a7309-104">W tym artykule dowiesz się, za pomocą konsoli zapytania HDInsight do uruchamiania zapytań Hive w klastrze usługi HDInsight Hadoop w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a7309-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7309-105">HDInsight konsoli zapytania jest dostępna tylko w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="a7309-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a7309-106">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="a7309-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a7309-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="a7309-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="a7309-108">Dla usługi HDInsight w wersji 3.4 lub większą, zobacz [uruchamianie zapytań Hive w widoku Hive narzędzia Ambari](hdinsight-hadoop-use-hive-ambari-view.md) informacji na temat uruchamiania zapytań Hive z przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="a7309-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="a7309-109"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a7309-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="a7309-110">Aby wykonać kroki opisane w tym artykule, potrzebne następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="a7309-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="a7309-111">Klastra z systemem Windows usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="a7309-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="a7309-112">Nowoczesna przeglądarka sieci web</span><span class="sxs-lookup"><span data-stu-id="a7309-112">A modern web browser</span></span>

## <span data-ttu-id="a7309-113"><a id="run"></a>Uruchamianie zapytań Hive przy użyciu konsoli zapytania</span><span class="sxs-lookup"><span data-stu-id="a7309-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="a7309-114">Otwórz przeglądarkę sieci web i przejdź do **https://CLUSTERNAME.azurehdinsight.net**, gdzie **CLUSTERNAME** jest nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7309-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="a7309-115">Jeśli zostanie wyświetlony monit, wprowadź nazwę użytkownika i hasło, które zostały użyte podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="a7309-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="a7309-116">Łącza w górnej części strony, zaznacz **Edytor Hive**.</span><span class="sxs-lookup"><span data-stu-id="a7309-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="a7309-117">Spowoduje to wyświetlenie formularza, który może służyć do wprowadzania instrukcje HiveQL, które mają być uruchamiane w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a7309-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![Edytor hive](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="a7309-119">Zamień tekst `Select * from hivesampletable` z poniższe instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="a7309-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="a7309-120">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a7309-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="a7309-121">**DROP TABLE**: usuwa tabeli i plik danych, jeśli tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="a7309-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="a7309-122">**Tworzenie tabeli zewnętrznej**: tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="a7309-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="a7309-123">Tabele zewnętrzne przechowywać tylko definicji tabeli w gałęzi; dane pozostaną w oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a7309-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a7309-124">Jeśli oczekujesz danych do zaktualizowania przez źródło zewnętrzne (na przykład procesu przekazywania danych) lub przez inną operację MapReduce, należy użyć tabel zewnętrznych, ale ma zawsze zapytań programu Hive za pomocą najnowszych danych.</span><span class="sxs-lookup"><span data-stu-id="a7309-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="a7309-125">Usunięcie tabeli zewnętrznej jest **nie** Usuń dane, definicję tabeli.</span><span class="sxs-lookup"><span data-stu-id="a7309-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="a7309-126">**FORMAT wiersza**: Określa, że Hive, jak dane są sformatowane.</span><span class="sxs-lookup"><span data-stu-id="a7309-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="a7309-127">W takim przypadku pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="a7309-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="a7309-128">**PRZECHOWYWANE jako lokalizacji TEXTFILE**: informuje gałąź rejestru, których dane są przechowywane (katalogu przykładzie/danych) i są przechowywane jako tekst</span><span class="sxs-lookup"><span data-stu-id="a7309-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="a7309-129">**Wybierz**: Wybierz liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="a7309-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="a7309-130">Powinny zostać zwrócone wartości **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="a7309-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="a7309-131">**INPUT__FILE__NAME takich jak "%.log"** -informuje, który mamy powinno zwrócić tylko danych z plików w gałęzi. dziennika.</span><span class="sxs-lookup"><span data-stu-id="a7309-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="a7309-132">To ogranicza wyszukiwanie do pliku sample.log, który zawiera dane, a następnie utrzymuje je z zwracać dane z innych przykładowe pliki danych, która nie pasuje do schematu, zdefiniowanego.</span><span class="sxs-lookup"><span data-stu-id="a7309-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="a7309-133">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="a7309-133">Click **Submit**.</span></span> <span data-ttu-id="a7309-134">**Sesji zadania** w dolnej części strony powinien być wyświetlany szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="a7309-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="a7309-135">Gdy **stan** pola zmienia się na **Ukończono**, wybierz pozycję **Wyświetl szczegóły** zadania.</span><span class="sxs-lookup"><span data-stu-id="a7309-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="a7309-136">Na stronie szczegółów **dane wyjściowe zadania** zawiera `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="a7309-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="a7309-137">Można użyć **Pobierz** przycisku w tym polu, aby pobrać plik, który zawiera dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="a7309-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="a7309-138"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a7309-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="a7309-139">Jak widać, konsoli zapytania zapewnia prosty sposób do uruchamiania zapytań Hive w klastra usługi HDInsight, monitorować stan zadania i pobrać dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a7309-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="a7309-140">Aby dowiedzieć się więcej na temat uruchamiania zadań Hive za pomocą konsoli zapytania Hive, wybierz **wprowadzenie** u góry konsoli zapytania, a następnie użyć przykłady, które zostały opublikowane.</span><span class="sxs-lookup"><span data-stu-id="a7309-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="a7309-141">Każda próbka przeprowadzi Cię przez proces za pomocą gałęzi do analizowania danych, w tym objaśnienia dotyczące instrukcje HiveQL użyty w próbce.</span><span class="sxs-lookup"><span data-stu-id="a7309-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="a7309-142"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7309-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a7309-143">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a7309-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="a7309-144">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7309-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="a7309-145">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a7309-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a7309-146">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7309-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a7309-147">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a7309-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="a7309-148">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz informacji o debugowaniu w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="a7309-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="a7309-149">Użyj interfejsu użytkownika aplikacji Tez w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a7309-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="a7309-150">Użyj widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="a7309-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
