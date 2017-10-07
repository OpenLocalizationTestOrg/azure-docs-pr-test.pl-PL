---
title: "aaaHive przy użyciu narzędzi Data Lake (Hadoop) dla programu Visual Studio - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak narzędzia hello toouse usługi Data Lake w dla programu Visual Studio toorun Apache Hive zapytania z platformy Apache Hadoop w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="0b56e-103">Uruchamianie zapytań Hive przy użyciu narzędzi Data Lake hello for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b56e-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="0b56e-104">Dowiedz się, jak toouse hello Data Lake tools dla Visual Studio tooquery Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="0b56e-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="0b56e-105">narzędzia Data Lake Hello pozwalają tooeasily tworzenia, przesyłania i monitorowania tooHadoop zapytań Hive w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b56e-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="0b56e-106"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0b56e-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="0b56e-107">Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="0b56e-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0b56e-108">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0b56e-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0b56e-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="0b56e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0b56e-110">Visual Studio (jedna hello następujące wersje):</span><span class="sxs-lookup"><span data-stu-id="0b56e-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="0b56e-111">Visual Studio 2013 Community/Professional/Premium/Ultimate z aktualizacją 4</span><span class="sxs-lookup"><span data-stu-id="0b56e-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="0b56e-112">Visual Studio 2015 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="0b56e-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="0b56e-113">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="0b56e-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="0b56e-114">Narzędzia HDInsight tools for Visual Studio lub usługi Azure Data Lake tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b56e-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="0b56e-115">Zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) informacji o instalowaniu i konfigurowaniu hello narzędzia.</span><span class="sxs-lookup"><span data-stu-id="0b56e-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="0b56e-116"><a id="run"></a>Uruchamianie zapytań Hive przy użyciu hello Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b56e-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="0b56e-117">Otwórz **programu Visual Studio** i wybierz **nowy** > **projektu** > **usługi Azure Data Lake** > **HIVE** > **aplikacji Hive**.</span><span class="sxs-lookup"><span data-stu-id="0b56e-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="0b56e-118">Podaj nazwę dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="0b56e-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="0b56e-119">Otwórz hello **Script.hql** pliku, który jest tworzony z tego projektu, a następnie wklej w hello następujące instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="0b56e-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="0b56e-120">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="0b56e-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="0b56e-121">`DROP TABLE`: Jeśli hello tabela istnieje, ta instrukcja usunięcia go.</span><span class="sxs-lookup"><span data-stu-id="0b56e-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="0b56e-122">`CREATE EXTERNAL TABLE`: Tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="0b56e-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="0b56e-123">Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi (powitalne pozostanie danych w oryginalnej lokalizacji hello).</span><span class="sxs-lookup"><span data-stu-id="0b56e-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="0b56e-124">Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="0b56e-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="0b56e-125">Na przykład zadania MapReduce lub usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="0b56e-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="0b56e-126">Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="0b56e-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="0b56e-127">`ROW FORMAT`: Określa, że sposób formatowania danych hello Hive.</span><span class="sxs-lookup"><span data-stu-id="0b56e-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="0b56e-128">W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="0b56e-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="0b56e-129">`STORED AS TEXTFILE LOCATION`: Nakazuje Hive gdzie hello są przechowywane dane (katalog hello przykład/danych) i które są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="0b56e-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="0b56e-130">`SELECT`: Wybierz liczbę wszystkich wierszy gdzie kolumna `t4` zawiera wartość hello `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="0b56e-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="0b56e-131">Ta instrukcja zwraca wartość `3` ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="0b56e-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="0b56e-132">`INPUT__FILE__NAME LIKE '%.log'`-Informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika.</span><span class="sxs-lookup"><span data-stu-id="0b56e-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="0b56e-133">Klauzulę ogranicza hello wyszukiwania toohello sample.log pliku, który zawiera dane hello.</span><span class="sxs-lookup"><span data-stu-id="0b56e-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="0b56e-134">Wybierz hello z narzędzi hello **klastra usługi HDInsight** mają toouse dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="0b56e-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="0b56e-135">Wybierz **przesyłania** instrukcje hello toorun jako zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="0b56e-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Przedstawia paska](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="0b56e-137">Witaj **Podsumowanie zadania Hive** pojawia się i wyświetla informacje o hello uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="0b56e-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="0b56e-138">Użyj hello **Odśwież** połączyć toorefresh hello zadania informacje do momentu hello **stan zadania** zmiany zbyt**Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="0b56e-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![Podsumowanie zadania wyświetlania zadanie zostało ukończone](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="0b56e-140">Użyj hello **dane wyjściowe zadania** link tooview hello dane wyjściowe tego zadania.</span><span class="sxs-lookup"><span data-stu-id="0b56e-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="0b56e-141">Wyświetla `[ERROR] 3`, która jest wartością hello zwracanych przez to zapytanie.</span><span class="sxs-lookup"><span data-stu-id="0b56e-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="0b56e-142">Można również uruchomić zapytań programu Hive, bez tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="0b56e-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="0b56e-143">Przy użyciu **Eksploratora serwera**, rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy serwera usługi HDInsight, a następnie wybierz **Napisz zapytanie Hive**.</span><span class="sxs-lookup"><span data-stu-id="0b56e-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="0b56e-144">W hello **temp.hql** dokumentu, która jest wyświetlana, Dodaj następujące instrukcje HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="0b56e-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="0b56e-145">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="0b56e-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="0b56e-146">`CREATE TABLE IF NOT EXISTS`: Tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0b56e-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="0b56e-147">Ponieważ hello `EXTERNAL` — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli.</span><span class="sxs-lookup"><span data-stu-id="0b56e-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="0b56e-148">Wewnętrzny tabele są przechowywane w magazynie danych hello Hive i są zarządzane przez Hive.</span><span class="sxs-lookup"><span data-stu-id="0b56e-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0b56e-149">W odróżnieniu od `EXTERNAL` tabel, również porzucenie wewnętrznej tabeli usuwa hello podstawowych danych.</span><span class="sxs-lookup"><span data-stu-id="0b56e-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="0b56e-150">`STORED AS ORC`: Magazyny hello dane w formacie (ORC) kolumnowym zoptymalizowane wiersza.</span><span class="sxs-lookup"><span data-stu-id="0b56e-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="0b56e-151">ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="0b56e-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="0b56e-152">`INSERT OVERWRITE ... SELECT`: Wybiera wiersze z hello `log4jLogs` tabeli, która zawiera `[ERROR]`, a następnie wstawia hello danych do hello `errorLogs` tabeli.</span><span class="sxs-lookup"><span data-stu-id="0b56e-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="0b56e-153">Z narzędzi hello wybierz **przesyłania** toorun hello zadania.</span><span class="sxs-lookup"><span data-stu-id="0b56e-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="0b56e-154">Użyj hello **stan zadania** toodetermine zadania hello została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="0b56e-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="0b56e-155">tooverify, który hello zadania utworzone hello tabeli, użyj **Eksploratora serwera** i rozwiń **Azure** > **HDInsight** > z klastrem usługi HDInsight > **Bazy danych programu hive** > **domyślne**.</span><span class="sxs-lookup"><span data-stu-id="0b56e-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="0b56e-156">Witaj **errorLogs** tabeli i hello **log4jLogs** tabeli są wymienione.</span><span class="sxs-lookup"><span data-stu-id="0b56e-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="0b56e-157"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b56e-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="0b56e-158">Jak widać, hello narzędzia HDInsight tools for Visual Studio zapewniają prosty sposób toowork z zapytań programu Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0b56e-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="0b56e-159">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0b56e-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="0b56e-160">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b56e-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0b56e-161">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0b56e-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="0b56e-162">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b56e-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="0b56e-163">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0b56e-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="0b56e-164">Aby uzyskać więcej informacji na temat hello HDInsight tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="0b56e-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="0b56e-165">Wprowadzenie do narzędzi HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b56e-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
