---
title: "Gałąź rejestru przy użyciu narzędzi Data Lake (Hadoop) dla programu Visual Studio - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie korzystania z narzędzi Data Lake dla programu Visual Studio do uruchamiania zapytań Apache Hive z platformą Apache Hadoop w usłudze Azure HDInsight."
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
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="bfa69-103">Uruchamianie zapytań Hive przy użyciu narzędzi Data Lake tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfa69-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="bfa69-104">Informacje o sposobie korzystania z narzędzi Data Lake dla programu Visual Studio do zapytania Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="bfa69-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="bfa69-105">Narzędzia Data Lake umożliwiają łatwe tworzenie, przesyłania i monitorowania zapytań programu Hive do platformy Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfa69-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="bfa69-106"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bfa69-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="bfa69-107">Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="bfa69-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="bfa69-108">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="bfa69-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bfa69-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="bfa69-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="bfa69-110">Visual Studio (jedna z następujących wersji):</span><span class="sxs-lookup"><span data-stu-id="bfa69-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="bfa69-111">Visual Studio 2013 Community/Professional/Premium/Ultimate z aktualizacją 4</span><span class="sxs-lookup"><span data-stu-id="bfa69-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="bfa69-112">Visual Studio 2015 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="bfa69-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="bfa69-113">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="bfa69-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="bfa69-114">Narzędzia HDInsight tools for Visual Studio lub usługi Azure Data Lake tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfa69-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="bfa69-115">Zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) informacji o instalowaniu i konfigurowaniu narzędzi.</span><span class="sxs-lookup"><span data-stu-id="bfa69-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="bfa69-116"><a id="run"></a>Uruchamianie zapytań Hive przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfa69-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="bfa69-117">Otwórz **programu Visual Studio** i wybierz **nowy** > **projektu** > **usługi Azure Data Lake** > **HIVE** > **aplikacji Hive**.</span><span class="sxs-lookup"><span data-stu-id="bfa69-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="bfa69-118">Podaj nazwę dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="bfa69-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="bfa69-119">Otwórz **Script.hql** pliku, który jest tworzony z tego projektu i wklej poniższe instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="bfa69-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="bfa69-120">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfa69-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="bfa69-121">`DROP TABLE`: Jeśli tabela istnieje, ta instrukcja usunięcia go.</span><span class="sxs-lookup"><span data-stu-id="bfa69-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="bfa69-122">`CREATE EXTERNAL TABLE`: Tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="bfa69-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="bfa69-123">Tabele zewnętrzne przechowywać tylko definicji tabeli w gałęzi (danych pozostaje w oryginalnej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="bfa69-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="bfa69-124">Jeśli oczekujesz zaktualizowania za pomocą zewnętrznego źródła danych, należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="bfa69-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="bfa69-125">Na przykład zadania MapReduce lub usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa69-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="bfa69-126">Usunięcie tabeli zewnętrznej jest **nie** Usuń dane, definicję tabeli.</span><span class="sxs-lookup"><span data-stu-id="bfa69-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="bfa69-127">`ROW FORMAT`: Nakazuje Hive sposób formatowania danych.</span><span class="sxs-lookup"><span data-stu-id="bfa69-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="bfa69-128">W takim przypadku pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="bfa69-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="bfa69-129">`STORED AS TEXTFILE LOCATION`: Nakazuje Hive przechowywania danych (katalog przykład/danych) i które są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="bfa69-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="bfa69-130">`SELECT`: Wybierz liczbę wszystkich wierszy gdzie kolumna `t4` zawiera wartość `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="bfa69-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="bfa69-131">Ta instrukcja zwraca wartość `3` ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="bfa69-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="bfa69-132">`INPUT__FILE__NAME LIKE '%.log'`-Informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika.</span><span class="sxs-lookup"><span data-stu-id="bfa69-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="bfa69-133">Klauzulę ogranicza wyszukiwanie do pliku sample.log, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="bfa69-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="bfa69-134">Na pasku narzędzi wybierz **klastra usługi HDInsight** , który ma być używany dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="bfa69-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="bfa69-135">Wybierz **przesyłania** do uruchamiania instrukcje jako zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="bfa69-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Przedstawia paska](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="bfa69-137">**Podsumowanie zadania Hive** pojawia się i wyświetla informacje o wykonywanym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="bfa69-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="bfa69-138">Użyj **Odśwież** łącze, aby odświeżyć informacje o zadaniu, dopóki **stan zadania** zmienia się na **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="bfa69-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![Podsumowanie zadania wyświetlania zadanie zostało ukończone](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="bfa69-140">Użyj **dane wyjściowe zadania** łącze, aby wyświetlić dane wyjściowe tego zadania.</span><span class="sxs-lookup"><span data-stu-id="bfa69-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="bfa69-141">Wyświetla `[ERROR] 3`, czyli wartość zwrócona przez tę kwerendę.</span><span class="sxs-lookup"><span data-stu-id="bfa69-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="bfa69-142">Można również uruchomić zapytań programu Hive, bez tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="bfa69-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="bfa69-143">Przy użyciu **Eksploratora serwera**, rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy serwera usługi HDInsight, a następnie wybierz **Napisz zapytanie Hive**.</span><span class="sxs-lookup"><span data-stu-id="bfa69-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="bfa69-144">W **temp.hql** dokumentu, która jest wyświetlana, Dodaj następujące instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="bfa69-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="bfa69-145">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfa69-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="bfa69-146">`CREATE TABLE IF NOT EXISTS`: Tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="bfa69-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="bfa69-147">Ponieważ `EXTERNAL` — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli.</span><span class="sxs-lookup"><span data-stu-id="bfa69-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="bfa69-148">Wewnętrzny tabele są przechowywane w magazynie danych programu Hive i są zarządzane przez Hive.</span><span class="sxs-lookup"><span data-stu-id="bfa69-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="bfa69-149">W odróżnieniu od `EXTERNAL` tabel, również porzucenie wewnętrznej tabeli powoduje usunięcie danych.</span><span class="sxs-lookup"><span data-stu-id="bfa69-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="bfa69-150">`STORED AS ORC`: Przechowuje dane w formacie (ORC) kolumnowym zoptymalizowane wiersza.</span><span class="sxs-lookup"><span data-stu-id="bfa69-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="bfa69-151">ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="bfa69-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="bfa69-152">`INSERT OVERWRITE ... SELECT`: Wybiera wiersze z `log4jLogs` tabeli, która zawiera `[ERROR]`, następnie wstawia dane do `errorLogs` tabeli.</span><span class="sxs-lookup"><span data-stu-id="bfa69-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="bfa69-153">Na pasku narzędzi wybierz **przesyłania** uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="bfa69-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="bfa69-154">Użyj **stan zadania** ustalenie, czy zadanie zostało zakończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="bfa69-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="bfa69-155">Aby sprawdzić, czy zadania utworzone tabeli, należy użyć **Eksploratora serwera** i rozwiń **Azure** > **HDInsight** > z klastrem usługi HDInsight > **bazy danych programu Hive** > **domyślne**.</span><span class="sxs-lookup"><span data-stu-id="bfa69-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="bfa69-156">**ErrorLogs** tabeli i **log4jLogs** tabeli są wymienione.</span><span class="sxs-lookup"><span data-stu-id="bfa69-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="bfa69-157"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bfa69-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="bfa69-158">Jak widać, narzędzia HDInsight tools for Visual Studio umożliwiają łatwe do pracy z zapytań programu Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bfa69-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="bfa69-159">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="bfa69-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="bfa69-160">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfa69-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="bfa69-161">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="bfa69-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="bfa69-162">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfa69-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="bfa69-163">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bfa69-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="bfa69-164">Aby uzyskać więcej informacji na temat narzędzia HDInsight tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bfa69-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="bfa69-165">Wprowadzenie do narzędzi HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfa69-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
