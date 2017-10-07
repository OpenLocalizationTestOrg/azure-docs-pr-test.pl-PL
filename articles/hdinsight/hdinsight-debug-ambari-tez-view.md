---
title: "aaaUse Ambari Tez widoku z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse Ambari Tez wyświetlić toodebug Tez zadania w usłudze HDInsight."
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
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="64bbd-103">Użyj widoków Ambari toodebug Tez zadania w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="64bbd-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="64bbd-104">Witaj Interfejsu sieci Web Ambari dla usługi HDInsight zawiera widok Tez, które mogą być używane toounderstand i debugowania zadania, które korzystają z aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="64bbd-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="64bbd-105">Widok Tez Hello umożliwia toovisualize hello zadania jako wykres połączonych elementów, przejdź do każdego elementu, a następnie pobrać statystyk i informacje o rejestrowaniu.</span><span class="sxs-lookup"><span data-stu-id="64bbd-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64bbd-106">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="64bbd-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="64bbd-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="64bbd-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="64bbd-108">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="64bbd-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64bbd-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64bbd-109">Prerequisites</span></span>

* <span data-ttu-id="64bbd-110">Klaster usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="64bbd-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="64bbd-111">Aby uzyskać instrukcje dotyczące tworzenia klastra, zobacz [rozpocząć korzystanie z usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64bbd-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="64bbd-112">Nowoczesna przeglądarka sieci Web, obsługująca język HTML5.</span><span class="sxs-lookup"><span data-stu-id="64bbd-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="64bbd-113">Opis aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="64bbd-113">Understanding Tez</span></span>

<span data-ttu-id="64bbd-114">Tez jest rozszerzalną strukturą do przetwarzania danych w Hadoop, która zapewnia większe szybkości niż tradycyjne przetwarzania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="64bbd-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="64bbd-115">W przypadku klastrów usługi HDInsight opartej na systemie Linux jest hello domyślny aparat gałęzi.</span><span class="sxs-lookup"><span data-stu-id="64bbd-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="64bbd-116">Tez tworzy skierowane acykliczne wykresu (DAG) opisujący hello kolejność akcji wymaganych przez zadania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="64bbd-117">Poszczególne działania są nazywane wierzchołki i wykonać fragment hello ogólną zadania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="64bbd-118">Hello rzeczywistego wykonania pracy hello opisanego przez wierzchołek nosi nazwę zadania i mogą być rozproszone na wielu węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="64bbd-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="64bbd-119">Opis hello widoku aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="64bbd-119">Understanding hello Tez view</span></span>

<span data-ttu-id="64bbd-120">Witaj Tez widok zawiera zarówno historyczne informacje i po procesów, które są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="64bbd-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="64bbd-121">Te informacje pokazują, jak zadanie jest dystrybuowana do klastrów.</span><span class="sxs-lookup"><span data-stu-id="64bbd-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="64bbd-122">Wyświetlane są również używane przez zadania i wierzchołków liczników i toohello zadania powiązane informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="64bbd-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="64bbd-123">Może on oferować przydatnych informacji w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="64bbd-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="64bbd-124">Monitorowanie procesy długotrwałe, wyświetlanie hello postęp mapowania i zmniejszyć zadania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="64bbd-125">Analizowanie dane historyczne dotyczące toolearn procesów powiodły się czy nie, jak można poprawić przetwarzania lub przyczyny niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="64bbd-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="64bbd-126">Generowanie DAG</span><span class="sxs-lookup"><span data-stu-id="64bbd-126">Generate a DAG</span></span>

<span data-ttu-id="64bbd-127">Hello Tez widok zawiera dane tylko jeśli zadanie, które używa hello Tez aparat jest obecnie uruchomiony lub wcześniej uruchomione.</span><span class="sxs-lookup"><span data-stu-id="64bbd-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="64bbd-128">Proste zapytań programu Hive można rozpoznawać bez korzystania z aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="64bbd-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="64bbd-129">Bardziej złożone kwerendy tego czy filtrowanie, grupowanie, kolejność, sprzężenia, itp.</span><span class="sxs-lookup"><span data-stu-id="64bbd-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="64bbd-130">Użyj hello Tez aparatu.</span><span class="sxs-lookup"><span data-stu-id="64bbd-130">use hello Tez engine.</span></span>

<span data-ttu-id="64bbd-131">Użyj hello następujące kroki toorun zapytań programu Hive, która używa Tez:</span><span class="sxs-lookup"><span data-stu-id="64bbd-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="64bbd-132">W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64bbd-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="64bbd-133">Witaj menu u góry hello hello strony i wybierz polecenie hello **widoków** ikony.</span><span class="sxs-lookup"><span data-stu-id="64bbd-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="64bbd-134">Ta ikona wygląda jak seria kwadratów.</span><span class="sxs-lookup"><span data-stu-id="64bbd-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="64bbd-135">Hello listy rozwijanej, która jest wyświetlana, wybierz **Hive widoku**.</span><span class="sxs-lookup"><span data-stu-id="64bbd-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Wybranie widoku Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="64bbd-137">Witaj widoku Hive załadowanie, Wklej hello następujące zapytanie w hello edytora zapytań, a następnie kliknij **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="64bbd-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="64bbd-138">Po zakończeniu zadania hello powinny być widoczne dane wyjściowe hello wyświetlane w hello **wyniki przetwarzania zapytania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="64bbd-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="64bbd-139">Witaj wyniki powinny być podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="64bbd-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="64bbd-140">Wybierz hello **dziennika** kartę. Zostaną wyświetlone informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="64bbd-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="64bbd-141">Zapisz hello **identyfikator aplikacji** wartość, jak ta wartość jest używana w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="64bbd-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="64bbd-142">Użyj hello widoku aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="64bbd-142">Use hello Tez View</span></span>

1. <span data-ttu-id="64bbd-143">Witaj menu u góry hello hello strony i wybierz polecenie hello **widoków** ikony.</span><span class="sxs-lookup"><span data-stu-id="64bbd-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="64bbd-144">Hello listy rozwijanej, która jest wyświetlana, wybierz **widoku Tez**.</span><span class="sxs-lookup"><span data-stu-id="64bbd-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Wybranie widoku aplikacji Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="64bbd-146">Podczas ładowania hello widoku Tez widać listę zapytań hive, które są aktualnie uruchomione lub zostały uruchomione w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="64bbd-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Wszystkie grupy DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="64bbd-148">Jeśli masz tylko jeden wpis dotyczy zapytanie hello, uruchomionego w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="64bbd-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="64bbd-149">Jeśli masz wiele wpisów można wyszukiwać za pomocą pola hello u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="64bbd-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="64bbd-150">Wybierz hello **identyfikator zapytania** dla zapytania programu Hive.</span><span class="sxs-lookup"><span data-stu-id="64bbd-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="64bbd-151">Informacje o kwerendzie hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="64bbd-151">Information about hello query is displayed.</span></span>

    ![Szczegóły grupy DAG.](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="64bbd-153">karty Hello na tej stronie umożliwiają hello tooview następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="64bbd-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="64bbd-154">**Zapytanie szczegóły**: szczegółowe informacje o hello zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="64bbd-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="64bbd-155">**Oś czasu**: dowiedzieć się, jak długo trwało każdego etapu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="64bbd-156">**Konfiguracje**: hello konfiguracji używane dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="64bbd-157">Z __szczegóły kwerendy__ można użyć hello łącza toofind informacji na temat hello __aplikacji__ lub hello __DAG__ dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="64bbd-158">Witaj __aplikacji__ łącze Wyświetla informacje o hello YARN aplikacji dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="64bbd-159">W tym miejscu można uzyskać dostępu do dzienników aplikacji hello YARN.</span><span class="sxs-lookup"><span data-stu-id="64bbd-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="64bbd-160">Witaj __DAG__ łącze Wyświetla informacje o hello ukierunkowanego wykresu acyklicznego. dla tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="64bbd-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="64bbd-161">W tym miejscu można wyświetlić graficzną reprezentację hello grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="64bbd-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="64bbd-162">Można również znaleźć informacji o hello wierzchołków w hello grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="64bbd-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64bbd-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64bbd-163">Next Steps</span></span>

<span data-ttu-id="64bbd-164">Teraz, gdy wiesz już, jak wyświetlić toouse hello Tez, Dowiedz się więcej o [przy użyciu Hive w usłudze HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="64bbd-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="64bbd-165">Aby uzyskać szczegółowe informacje techniczne na temat aplikacji Tez, zobacz hello [Tez strony o Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="64bbd-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="64bbd-166">Aby uzyskać więcej informacji na temat używania narzędzia Ambari z usługą HDInsight, zobacz [Zarządzanie klastrów usługi HDInsight przy użyciu hello Interfejsu sieci Web Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="64bbd-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
