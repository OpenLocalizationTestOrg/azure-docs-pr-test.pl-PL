---
title: "Korzystanie z interfejsu użytkownika aplikacji Tez z usługą HDInsight opartych na systemie Windows - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i debugowanie aplikacji Tez zadania w usłudze HDInsight HDInsight dla komputerów z systemem Windows przy użyciu interfejsu użytkownika aplikacji Tez."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="a6d42-103">Debugowanie aplikacji Tez zadania w usłudze HDInsight z systemem Windows przy użyciu interfejsu użytkownika aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="a6d42-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="a6d42-104">Interfejs użytkownika aplikacji Tez jest strony sieci web, który może służyć do zrozumienia i debugowania zadania, które korzystają z aplikacji Tez jako aparat wykonywania w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="a6d42-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a6d42-105">Interfejs użytkownika aplikacji Tez umożliwia wizualizacji zadaniem w postaci wykresu połączonych elementów, przejdź do każdego elementu i pobrać statystyk i informacje o rejestrowaniu.</span><span class="sxs-lookup"><span data-stu-id="a6d42-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6d42-106">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="a6d42-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="a6d42-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="a6d42-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a6d42-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="a6d42-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6d42-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a6d42-109">Prerequisites</span></span>
* <span data-ttu-id="a6d42-110">Klaster usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="a6d42-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="a6d42-111">Aby uzyskać instrukcje dotyczące tworzenia nowego klastra, zobacz [rozpocząć korzystanie z usługi HDInsight opartej na systemie Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="a6d42-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a6d42-112">Interfejs użytkownika aplikacji Tez jest dostępna tylko w klastrach HDInsight opartych na systemie Windows utworzone po 8 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="a6d42-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="a6d42-113">Klient pulpitu zdalnego z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="a6d42-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="a6d42-114">Opis aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="a6d42-114">Understanding Tez</span></span>
<span data-ttu-id="a6d42-115">Tez jest rozszerzalną strukturą do przetwarzania danych w Hadoop, która zapewnia większe szybkości niż tradycyjne przetwarzania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a6d42-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="a6d42-116">W przypadku klastrów usługi HDInsight opartej na systemie Windows jest opcjonalny mechanizm, który można włączyć dla gałęzi przy użyciu następującego polecenia w ramach zapytania Hive:</span><span class="sxs-lookup"><span data-stu-id="a6d42-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="a6d42-117">Podczas pracy jest przesyłany do aplikacji Tez, tworzy skierowane acykliczne Graph (DAG) opisujący kolejność wykonywania czynności wymaganych przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="a6d42-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="a6d42-118">Poszczególne działania są nazywane wierzchołki i wykonaj część ogólnej zadania.</span><span class="sxs-lookup"><span data-stu-id="a6d42-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="a6d42-119">Rzeczywiste wykonywania pracy opisanego przez wierzchołek nosi nazwę zadania i mogą być rozproszone na wielu węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="a6d42-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="a6d42-120">Opis interfejsu użytkownika aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="a6d42-120">Understanding the Tez UI</span></span>
<span data-ttu-id="a6d42-121">Interfejs użytkownika aplikacji Tez jest strony sieci web zapewnia informacji na temat procesów, które są uruchomione lub mieć wcześniej został uruchomiony przy użyciu aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="a6d42-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="a6d42-122">Umożliwia wyświetlenie DAG wygenerowane w aplikacji Tez, liczniki jak dystrybuowana klastrów, takie jak pamięć używane przez zadania i wierzchołki i informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="a6d42-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="a6d42-123">Może on oferować informacje przydatne w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="a6d42-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="a6d42-124">Monitorowanie długotrwałe przetwarza, wyświetlanie postęp mapowania i zmniejszyć zadania.</span><span class="sxs-lookup"><span data-stu-id="a6d42-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="a6d42-125">Analizowanie danych historycznych dla procesów powiodły się czy nie dowiedzieć się, jak można poprawić przetwarzania lub przyczyny niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="a6d42-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="a6d42-126">Generowanie DAG</span><span class="sxs-lookup"><span data-stu-id="a6d42-126">Generate a DAG</span></span>
<span data-ttu-id="a6d42-127">Interfejs użytkownika aplikacji Tez będzie zawierać tylko dane, jeśli zadanie, które używa aparatu Tez jest obecnie uruchomiony lub został były uruchamiane w przeszłości.</span><span class="sxs-lookup"><span data-stu-id="a6d42-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="a6d42-128">Proste zapytań programu Hive można rozpoznawać zwykle bez korzystania z aplikacji Tez, jednak bardziej złożonych zapytań, które wykonaj filtrowanie, grupowanie, kolejność sprzężenia, itp. zwykle wymagają Tez.</span><span class="sxs-lookup"><span data-stu-id="a6d42-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="a6d42-129">Wykonaj następujące kroki, aby uruchomić zapytanie Hive, które będą wykonywane przy użyciu aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="a6d42-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="a6d42-130">W przeglądarce sieci web, przejdź do https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a6d42-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="a6d42-131">Wybierz z menu w górnej części strony **Edytor Hive**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="a6d42-132">Zostanie wyświetlona strona z następujące przykładowe zapytanie.</span><span class="sxs-lookup"><span data-stu-id="a6d42-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="a6d42-133">ERASE przykładowe zapytanie i zastąp go poniżej.</span><span class="sxs-lookup"><span data-stu-id="a6d42-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="a6d42-134">Wybierz **przesyłania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a6d42-134">Select the **Submit** button.</span></span> <span data-ttu-id="a6d42-135">**Sesji zadania** sekcji w dolnej części strony będzie wyświetlany stan zapytania.</span><span class="sxs-lookup"><span data-stu-id="a6d42-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="a6d42-136">Gdy stan zmienia się na **Ukończono**, wybierz pozycję **Wyświetl szczegóły** łącze, aby wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="a6d42-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="a6d42-137">**Dane wyjściowe zadania** powinien być podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="a6d42-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="a6d42-138">Korzystanie z interfejsu użytkownika aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="a6d42-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="a6d42-139">Interfejs użytkownika aplikacji Tez jest dostępna wyłącznie z pulpitu głównymi węzłami klastra, trzeba używać pulpitu zdalnego nawiązywania połączenia z węzłów głównych.</span><span class="sxs-lookup"><span data-stu-id="a6d42-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="a6d42-140">Z [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a6d42-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="a6d42-141">W górnej części bloku HDInsight, wybierz **pulpitu zdalnego** ikony.</span><span class="sxs-lookup"><span data-stu-id="a6d42-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="a6d42-142">Spowoduje to wyświetlenie bloku pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="a6d42-142">This will display the remote desktop blade</span></span>

    ![Ikony pulpitu zdalnego](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="a6d42-144">W bloku pulpitu zdalnego, wybierz **Connect** nawiązać połączenia z głównym węzłem klastra.</span><span class="sxs-lookup"><span data-stu-id="a6d42-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="a6d42-145">Po wyświetleniu monitu użyj nazwa użytkownika pulpitu zdalnego klastra i hasło do uwierzytelniania połączenia.</span><span class="sxs-lookup"><span data-stu-id="a6d42-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Ikona połączenia pulpitu zdalnego](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="a6d42-147">Jeśli połączenie pulpitu zdalnego nie jest włączone, wprowadź nazwę użytkownika, hasło oraz Data wygaśnięcia, a następnie wybierz **włączyć** można włączyć pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="a6d42-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="a6d42-148">Po jej włączeniu, skorzystaj z poprzednich kroków, aby połączyć.</span><span class="sxs-lookup"><span data-stu-id="a6d42-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="a6d42-149">Po nawiązaniu połączenia, Otwórz program Internet Explorer na pulpicie zdalnym, wybierz koło zębate ikonę w prawym górnym rogu przeglądarki, a następnie wybierz **ustawienia widoku zgodności**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="a6d42-150">W dolnej części **ustawienia widoku zgodności**, usuń zaznaczenie pola wyboru dla **wyświetlić witryn intranetowych w widoku zgodności** i **listy zgodności użycia Microsoft**, i następnie wybierz **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="a6d42-151">W programie Internet Explorer przejdź do http://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="a6d42-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="a6d42-152">Spowoduje to wyświetlenie interfejsu użytkownika aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="a6d42-152">This will display the Tez UI</span></span>

    ![Interfejs użytkownika aplikacji tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="a6d42-154">Podczas ładowania interfejsu użytkownika aplikacji Tez, pojawi się, że lista grupy DAG, które są aktualnie uruchomione lub zostały uruchomione w klastrze.</span><span class="sxs-lookup"><span data-stu-id="a6d42-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="a6d42-155">Domyślny widok zawiera nazwę grupy Dag, identyfikatora, osoba przesyłająca, stan, czas rozpoczęcia, godziny zakończenia, czas trwania, identyfikator aplikacji i kolejki.</span><span class="sxs-lookup"><span data-stu-id="a6d42-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="a6d42-156">Można dodać więcej kolumn, za pomocą ikony koło zębate po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="a6d42-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="a6d42-157">Jeśli masz tylko jeden wpis będzie zapytania uruchomionego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a6d42-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="a6d42-158">Jeśli masz wiele wpisów, możesz wyszukać, wpisując kryteria wyszukiwania w polach powyżej grupy DAG, a następnie kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="a6d42-159">Wybierz **Nazwa grupy Dag** najnowszych wpisu grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="a6d42-160">Spowoduje to wyświetlenie informacji o DAG, a także opcję Pobierz zip pliki w formacie JSON, które zawierają informacje dotyczące grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![Szczegóły grupy DAG.](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="a6d42-162">Powyżej **szczegóły DAG** są kilka łącza, które mogą służyć do wyświetlania informacji dotyczących grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="a6d42-163">**Liczniki DAG** Wyświetla liczniki informacje dla tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="a6d42-164">**Widok graficzny** Wyświetla graficzną reprezentację tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="a6d42-165">**Wszystkich wierzchołków** Wyświetla listę wierzchołków w tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="a6d42-166">**Wszystkie zadania** Wyświetla listę zadań dla wszystkich wierzchołków w tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="a6d42-167">**Wszystkie TaskAttempts** Wyświetla informacje o próby uruchomienia zadania dla tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a6d42-168">Wyświetl kolumny do wierzchołków, zadania i TaskAttempts podczas przewijania, zwróć uwagę, czy łącza, aby wyświetlić **liczniki** i **wyświetlić lub pobrać dzienniki** dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="a6d42-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="a6d42-169">Jeśli wystąpił błąd z zadaniem, stan Niepowodzenie, oraz linki do informacji dotyczących zadań zakończonych niepowodzeniem będą wyświetlane szczegóły grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="a6d42-170">Informacje diagnostyczne pojawi się poniżej szczegółów grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="a6d42-171">Wybierz **widoku graficznego**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-171">Select **Graphical View**.</span></span> <span data-ttu-id="a6d42-172">Spowoduje to wyświetlenie graficzną reprezentację DAG.</span><span class="sxs-lookup"><span data-stu-id="a6d42-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="a6d42-173">Można umieścić wskaźnik myszy przez każdy wierzchołek w widoku, aby wyświetlić informacje o nim.</span><span class="sxs-lookup"><span data-stu-id="a6d42-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Widok graficzny](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="a6d42-175">Kliknięcie wierzchołek załaduje **szczegóły wierzchołków** dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="a6d42-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="a6d42-176">Polecenie **1 mapy** wierzchołków, aby wyświetlić szczegóły dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="a6d42-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="a6d42-177">Wybierz **Potwierdź** o potwierdzenie w obszarze nawigacji.</span><span class="sxs-lookup"><span data-stu-id="a6d42-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Szczegóły wierzchołków](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="a6d42-179">Należy zauważyć, że możesz teraz łączy w górnej części strony, które są związane z wierzchołki i zadania.</span><span class="sxs-lookup"><span data-stu-id="a6d42-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6d42-180">Tej strony można również przyjeździe, przechodząc do **szczegółów grupy DAG**, wybierając żądane **szczegóły wierzchołków**, a następnie wybierając **1 mapy** wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="a6d42-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="a6d42-181">**Liczniki wierzchołków** Wyświetla informacje o liczniku tym wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="a6d42-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="a6d42-182">**Zadania** Wyświetla zadania dla tego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="a6d42-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="a6d42-183">**Zadanie prób** Wyświetla informacje dotyczące prób wykonania zadania dla tego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="a6d42-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="a6d42-184">**Źródłem & wychwytywanie** wyświetla źródła danych i sink tego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="a6d42-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a6d42-185">Jako mogą być przewijane Wyświetl kolumny do zadania, prób zadań i źródeł & Sinks__ wyświetlić łącza do dodatkowych informacji dla każdego elementu z poprzedniego menu.</span><span class="sxs-lookup"><span data-stu-id="a6d42-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="a6d42-186">Wybierz **zadania**, a następnie wybierz element o nazwie **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="a6d42-187">Spowoduje to wyświetlenie **szczegóły zadania** dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="a6d42-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="a6d42-188">Na tym ekranie można wyświetlić **liczniki zadań** i **zadań prób**.</span><span class="sxs-lookup"><span data-stu-id="a6d42-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Szczegóły zadania](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="a6d42-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6d42-190">Next Steps</span></span>
<span data-ttu-id="a6d42-191">Teraz, kiedy znasz sposobu korzystania z widoku aplikacji Tez, Dowiedz się więcej o [przy użyciu Hive w usłudze HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="a6d42-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="a6d42-192">Aby uzyskać szczegółowe informacje techniczne na temat aplikacji Tez, zobacz [Tez strony o Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="a6d42-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
