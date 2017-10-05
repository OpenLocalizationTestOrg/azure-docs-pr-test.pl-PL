---
title: "Użyj widoku Tez Ambari z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skorzystać z widoku Ambari Tez do debugowania aplikacji Tez zadania w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="fee38-103">Debugowanie aplikacji Tez zadania w usłudze HDInsight przy użyciu widoków Ambari</span><span class="sxs-lookup"><span data-stu-id="fee38-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="fee38-104">Interfejs użytkownika sieci Web Ambari HDInsight zawiera widok Tez, który może służyć do zrozumienia i debugowanie zadań, które używają aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="fee38-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="fee38-105">Widok Tez umożliwia wizualizacji zadaniem w postaci wykresu połączonych elementów, przejdź do każdego elementu i pobrać statystyk i informacje o rejestrowaniu.</span><span class="sxs-lookup"><span data-stu-id="fee38-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fee38-106">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fee38-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="fee38-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="fee38-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fee38-108">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fee38-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fee38-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fee38-109">Prerequisites</span></span>

* <span data-ttu-id="fee38-110">Klaster usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="fee38-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="fee38-111">Aby uzyskać instrukcje dotyczące tworzenia klastra, zobacz [rozpocząć korzystanie z usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fee38-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="fee38-112">Nowoczesna przeglądarka sieci Web, obsługująca język HTML5.</span><span class="sxs-lookup"><span data-stu-id="fee38-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="fee38-113">Opis aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="fee38-113">Understanding Tez</span></span>

<span data-ttu-id="fee38-114">Tez jest rozszerzalną strukturą do przetwarzania danych w Hadoop, która zapewnia większe szybkości niż tradycyjne przetwarzania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="fee38-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="fee38-115">W przypadku klastrów usługi HDInsight opartej na systemie Linux jest domyślny aparat gałęzi.</span><span class="sxs-lookup"><span data-stu-id="fee38-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="fee38-116">Tez tworzy skierowane acykliczne wykresu (DAG) opisujący kolejność akcji wymaganych przez zadania.</span><span class="sxs-lookup"><span data-stu-id="fee38-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="fee38-117">Poszczególne działania są nazywane wierzchołki i wykonaj część ogólnej zadania.</span><span class="sxs-lookup"><span data-stu-id="fee38-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="fee38-118">Rzeczywiste wykonywania pracy opisanego przez wierzchołek nosi nazwę zadania i mogą być rozproszone na wielu węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="fee38-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="fee38-119">Opis widoku aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="fee38-119">Understanding the Tez view</span></span>

<span data-ttu-id="fee38-120">Widok Tez zawiera zarówno informacje historyczne i po procesów, które są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="fee38-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="fee38-121">Te informacje pokazują, jak zadanie jest dystrybuowana do klastrów.</span><span class="sxs-lookup"><span data-stu-id="fee38-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="fee38-122">Wyświetla również liczniki używane przez zadania i wierzchołki i powiązany z zadaniem informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="fee38-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="fee38-123">Może on oferować informacje przydatne w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="fee38-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="fee38-124">Monitorowanie długotrwałe przetwarza, wyświetlanie postęp mapowania i zmniejszyć zadania.</span><span class="sxs-lookup"><span data-stu-id="fee38-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="fee38-125">Analizowanie danych historycznych dla procesów powiodły się czy nie dowiedzieć się, jak można poprawić przetwarzania lub przyczyny niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="fee38-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="fee38-126">Generowanie DAG</span><span class="sxs-lookup"><span data-stu-id="fee38-126">Generate a DAG</span></span>

<span data-ttu-id="fee38-127">Widok Tez zawiera dane tylko jeśli używa aparatu Tez jest obecnie uruchomiony lub został wcześniej uruchomione zadanie.</span><span class="sxs-lookup"><span data-stu-id="fee38-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="fee38-128">Proste zapytań programu Hive można rozpoznawać bez korzystania z aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="fee38-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="fee38-129">Bardziej złożone kwerendy tego czy filtrowanie, grupowanie, kolejność, sprzężenia, itp.</span><span class="sxs-lookup"><span data-stu-id="fee38-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="fee38-130">Użyj aparatu Tez.</span><span class="sxs-lookup"><span data-stu-id="fee38-130">use the Tez engine.</span></span>

<span data-ttu-id="fee38-131">Uruchamianie zapytań programu Hive, która używa Tez, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fee38-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="fee38-132">W przeglądarce sieci web, przejdź do https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fee38-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="fee38-133">Wybierz z menu w górnej części strony **widoków** ikony.</span><span class="sxs-lookup"><span data-stu-id="fee38-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="fee38-134">Ta ikona wygląda jak seria kwadratów.</span><span class="sxs-lookup"><span data-stu-id="fee38-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="fee38-135">W wyświetlonym menu rozwijanego wybierz **Hive widoku**.</span><span class="sxs-lookup"><span data-stu-id="fee38-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Wybranie widoku Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="fee38-137">Załadowanie widoku Hive, wklej poniższe zapytanie w edytorze zapytań, a następnie kliknij przycisk **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="fee38-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="fee38-138">Po ukończeniu zadania powinien zostać wyświetlony wyświetlany w danych wyjściowych **wyniki przetwarzania zapytania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="fee38-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="fee38-139">Wyniki powinny być podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="fee38-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="fee38-140">Wybierz **dziennika** kartę.</span><span class="sxs-lookup"><span data-stu-id="fee38-140">Select the **Log** tab.</span></span> <span data-ttu-id="fee38-141">Zostaną wyświetlone informacje podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="fee38-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="fee38-142">Zapisz **identyfikator aplikacji** wartość, jak ta wartość jest używana w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fee38-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="fee38-143">Użyj widoku aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="fee38-143">Use the Tez View</span></span>

1. <span data-ttu-id="fee38-144">Wybierz z menu w górnej części strony **widoków** ikony.</span><span class="sxs-lookup"><span data-stu-id="fee38-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="fee38-145">W wyświetlonym menu rozwijanego wybierz **widoku Tez**.</span><span class="sxs-lookup"><span data-stu-id="fee38-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Wybranie widoku aplikacji Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="fee38-147">Po załadowaniu widoku aplikacji Tez, można znaleźć listę zapytań hive, które są aktualnie uruchomione lub były uruchomione w klastrze.</span><span class="sxs-lookup"><span data-stu-id="fee38-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Wszystkie grupy DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="fee38-149">Jeśli masz tylko jeden wpis jest zapytania uruchomionego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fee38-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="fee38-150">Jeśli masz wiele wpisów można wyszukiwać za pomocą pola w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="fee38-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="fee38-151">Wybierz **identyfikator zapytania** dla zapytania programu Hive.</span><span class="sxs-lookup"><span data-stu-id="fee38-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="fee38-152">Zostaną wyświetlone informacje o kwerendzie.</span><span class="sxs-lookup"><span data-stu-id="fee38-152">Information about the query is displayed.</span></span>

    ![Szczegóły grupy DAG.](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="fee38-154">Karty na tej stronie umożliwiają wyświetlić następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="fee38-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="fee38-155">**Zapytanie szczegóły**: szczegóły dotyczące zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="fee38-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="fee38-156">**Oś czasu**: dowiedzieć się, jak długo trwało każdego etapu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="fee38-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="fee38-157">**Konfiguracje**: Konfiguracja użyta dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="fee38-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="fee38-158">Z __szczegóły kwerendy__ można użyć linków, aby uzyskać informacje na temat __aplikacji__ lub __DAG__ dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="fee38-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="fee38-159">__Aplikacji__ link Wyświetla informacje o aplikacji YARN dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="fee38-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="fee38-160">W tym miejscu można uzyskać dostępu do dzienników YARN aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fee38-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="fee38-161">__DAG__ łącze Wyświetla informacje o ukierunkowanego wykresu acyklicznego. dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="fee38-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="fee38-162">W tym miejscu można wyświetlić graficzną reprezentację DAG.</span><span class="sxs-lookup"><span data-stu-id="fee38-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="fee38-163">Można również znaleźć informacji o wierzchołków w obrębie grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="fee38-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fee38-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fee38-164">Next Steps</span></span>

<span data-ttu-id="fee38-165">Teraz, kiedy znasz sposobu korzystania z widoku aplikacji Tez, Dowiedz się więcej o [przy użyciu Hive w usłudze HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="fee38-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="fee38-166">Aby uzyskać szczegółowe informacje techniczne na temat aplikacji Tez, zobacz [Tez strony o Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="fee38-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="fee38-167">Aby uzyskać więcej informacji na temat używania narzędzia Ambari z usługą HDInsight, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="fee38-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
