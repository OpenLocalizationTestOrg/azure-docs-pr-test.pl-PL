---
title: "aaaUse interfejsu użytkownika aplikacji Tez z usługą HDInsight opartych na systemie Windows - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse toodebug interfejsu użytkownika aplikacji Tez Tez zadania w usłudze HDInsight HDInsight dla systemu Windows."
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="637c4-103">Użyj hello interfejsu użytkownika aplikacji Tez toodebug Tez zadania w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="637c4-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="637c4-104">Witaj Tez interfejsu użytkownika jest strony sieci web, które mogą być używane toounderstand i debugowanie zadań, korzystających z aplikacji Tez jako aparat wykonywania hello w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="637c4-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="637c4-105">Hello interfejsu użytkownika aplikacji Tez umożliwia toovisualize hello zadania jako wykres połączonych elementów, przejdź do każdego elementu, a następnie pobrać statystyk i informacje o rejestrowaniu.</span><span class="sxs-lookup"><span data-stu-id="637c4-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="637c4-106">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="637c4-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="637c4-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="637c4-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="637c4-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="637c4-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="637c4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="637c4-109">Prerequisites</span></span>
* <span data-ttu-id="637c4-110">Klaster usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="637c4-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="637c4-111">Aby uzyskać instrukcje dotyczące tworzenia nowego klastra, zobacz [rozpocząć korzystanie z usługi HDInsight opartej na systemie Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="637c4-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="637c4-112">Hello Tez interfejsu użytkownika jest dostępna tylko w klastrach HDInsight opartych na systemie Windows utworzone po 8 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="637c4-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="637c4-113">Klient pulpitu zdalnego z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="637c4-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="637c4-114">Opis aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="637c4-114">Understanding Tez</span></span>
<span data-ttu-id="637c4-115">Tez jest rozszerzalną strukturą do przetwarzania danych w Hadoop, która zapewnia większe szybkości niż tradycyjne przetwarzania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="637c4-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="637c4-116">W przypadku klastrów usługi HDInsight opartej na systemie Windows jest opcjonalny mechanizm, który można włączyć dla gałęzi przy użyciu następującego polecenia w ramach zapytania Hive hello:</span><span class="sxs-lookup"><span data-stu-id="637c4-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="637c4-117">Podczas pracy jest tooTez przesłane, tworzy skierowane acykliczne Graph (DAG) opisujący hello kolejność wykonywania działań hello wymagane przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="637c4-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="637c4-118">Poszczególne działania są nazywane wierzchołki i wykonać fragment hello ogólną zadania.</span><span class="sxs-lookup"><span data-stu-id="637c4-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="637c4-119">Hello rzeczywistego wykonania pracy hello opisanego przez wierzchołek nosi nazwę zadania i mogą być rozproszone na wielu węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="637c4-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="637c4-120">Opis hello Tez interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="637c4-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="637c4-121">strony sieci web zapewnia informacji na temat procesów, które są uruchomione lub mieć wcześniej został uruchomiony przy użyciu aplikacji Tez jest Hello Tez interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="637c4-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="637c4-122">Umożliwia hello tooview DAG wygenerowane w aplikacji Tez, liczniki jak dystrybuowana klastrów, takie jak pamięć używane przez zadania i wierzchołki i informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="637c4-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="637c4-123">Może on oferować przydatnych informacji w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="637c4-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="637c4-124">Monitorowanie procesy długotrwałe, wyświetlanie hello postęp mapowania i zmniejszyć zadania.</span><span class="sxs-lookup"><span data-stu-id="637c4-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="637c4-125">Analizowanie dane historyczne dotyczące toolearn procesów powiodły się czy nie, jak można poprawić przetwarzania lub przyczyny niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="637c4-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="637c4-126">Generowanie DAG</span><span class="sxs-lookup"><span data-stu-id="637c4-126">Generate a DAG</span></span>
<span data-ttu-id="637c4-127">Jeśli zadanie, które używa hello Tez aparat jest aktualnie uruchomione lub zostało uruchomione w ostatnich hello Hello interfejsu użytkownika aplikacji Tez tylko zawierają dane.</span><span class="sxs-lookup"><span data-stu-id="637c4-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="637c4-128">Proste zapytań programu Hive można rozpoznawać zwykle bez korzystania z aplikacji Tez, jednak bardziej złożonych zapytań, które wykonaj filtrowanie, grupowanie, kolejność sprzężenia, itp. zwykle wymagają Tez.</span><span class="sxs-lookup"><span data-stu-id="637c4-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="637c4-129">Użyj hello następujące kroki toorun zapytań programu Hive, które będą wykonywane przy użyciu aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="637c4-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="637c4-130">W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="637c4-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="637c4-131">Witaj menu u góry hello hello strony i wybierz polecenie hello **Edytor Hive**.</span><span class="sxs-lookup"><span data-stu-id="637c4-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="637c4-132">Spowoduje to wyświetlenie strony z hello następujące przykładowe zapytanie.</span><span class="sxs-lookup"><span data-stu-id="637c4-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="637c4-133">ERASE hello przykładowe zapytanie i zastąp go hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="637c4-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="637c4-134">Wybierz hello **przesyłania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="637c4-134">Select hello **Submit** button.</span></span> <span data-ttu-id="637c4-135">Witaj **sesji zadania** sekcji u dołu strony hello hello jest wyświetlany stan hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="637c4-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="637c4-136">Raz zbyt hello zmiany stanu**Ukończono**, wybierz pozycję hello **Wyświetl szczegóły** link tooview hello wyników.</span><span class="sxs-lookup"><span data-stu-id="637c4-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="637c4-137">Witaj **dane wyjściowe zadania** powinny być podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="637c4-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="637c4-138">Użyj hello Tez interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="637c4-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="637c4-139">Hello Tez interfejsu użytkownika jest dostępna wyłącznie z pulpitem hello hello głównymi węzłami klastra, trzeba używać węzłów głównych toohello tooconnect pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="637c4-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="637c4-140">Z hello [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="637c4-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="637c4-141">Z góry hello hello HDInsight bloku, wybierz hello **pulpitu zdalnego** ikony.</span><span class="sxs-lookup"><span data-stu-id="637c4-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="637c4-142">Spowoduje to wyświetlenie bloku pulpitu zdalnego hello</span><span class="sxs-lookup"><span data-stu-id="637c4-142">This will display hello remote desktop blade</span></span>

    ![Ikony pulpitu zdalnego](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="637c4-144">W bloku pulpitu zdalnego hello, wybierz **Connect** węzła głównego klastra toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="637c4-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="637c4-145">Po wyświetleniu monitu użyj hello klastra Podłączanie pulpitu zdalnego użytkownika nazwę i hasło tooauthenticate hello.</span><span class="sxs-lookup"><span data-stu-id="637c4-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Ikona połączenia pulpitu zdalnego](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="637c4-147">Jeśli połączenie pulpitu zdalnego nie jest włączone, wprowadź nazwę użytkownika, hasło oraz Data wygaśnięcia, a następnie wybierz **włączyć** tooenable pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="637c4-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="637c4-148">Po jej włączeniu, użyj hello poprzednich kroków tooconnect.</span><span class="sxs-lookup"><span data-stu-id="637c4-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="637c4-149">Po nawiązaniu połączenia, Otwórz program Internet Explorer na powitania pulpitu zdalnego, wybierz hello koło zębate ikonę w hello górnym rogu przeglądarki hello, a następnie wybierz **ustawienia widoku zgodności**.</span><span class="sxs-lookup"><span data-stu-id="637c4-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="637c4-150">Od dołu hello **ustawienia widoku zgodności**, wyczyść pola wyboru hello **wyświetlić witryn intranetowych w widoku zgodności** i **listy zgodności użycia programu Microsoft**, a następnie wybierz **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="637c4-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="637c4-151">W programie Internet Explorer przejdź toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="637c4-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="637c4-152">Spowoduje to wyświetlenie hello Tez interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="637c4-152">This will display hello Tez UI</span></span>

    ![Interfejs użytkownika aplikacji tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="637c4-154">Po załadowaniu hello Tez interfejsu użytkownika, pojawi się, że listy grupy DAG, które są aktualnie uruchomione lub zostały uruchomione na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="637c4-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="637c4-155">Widok domyślny Hello obejmuje hello Nazwa grupy Dag, identyfikator przesyłający, stan, czas rozpoczęcia, godziny zakończenia, czas trwania, identyfikator aplikacji i kolejki.</span><span class="sxs-lookup"><span data-stu-id="637c4-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="637c4-156">Przy użyciu hello koło zębate ikonę na powitania po prawej strony hello można dodać więcej kolumn.</span><span class="sxs-lookup"><span data-stu-id="637c4-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="637c4-157">Jeśli masz tylko jeden wpis będzie dla zapytania hello, uruchomionego w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="637c4-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="637c4-158">Jeśli masz wiele wpisów, można wyszukać, wpisując kryteria wyszukiwania w polach hello powyżej hello grupy DAG, a następnie kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="637c4-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="637c4-159">Wybierz hello **Nazwa grupy Dag** hello najnowszych DAG wpisu.</span><span class="sxs-lookup"><span data-stu-id="637c4-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="637c4-160">Spowoduje to wyświetlenie informacji o hello DAG, a także toodownload opcji hello zip pliki w formacie JSON, które zawierają informacje dotyczące hello DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Szczegóły grupy DAG.](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="637c4-162">Powyżej hello **szczegóły DAG** są kilka łącza, które mogą być używane toodisplay informacji na temat hello grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="637c4-163">**Liczniki DAG** Wyświetla liczniki informacje dla tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="637c4-164">**Widok graficzny** Wyświetla graficzną reprezentację tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="637c4-165">**Wszystkich wierzchołków** zostanie wyświetlona lista hello wierzchołków w tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="637c4-166">**Wszystkie zadania** zostanie wyświetlona lista hello zadania dla wszystkich wierzchołków w tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="637c4-167">**Wszystkie TaskAttempts** Wyświetla informacje o hello prób toorun zadań dla tej grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="637c4-168">Podczas przewijania hello kolumny wyświetlanej wierzchołków, zadania i TaskAttempts, zwróć uwagę, że istnieją łączy tooview **liczniki** i **wyświetlić lub pobrać dzienniki** dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="637c4-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="637c4-169">Jeśli wystąpił błąd z zadaniem hello, hello DAG szczegółów będzie wyświetlany stan nie powiodła się, wraz z tooinformation łącza o hello zadania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="637c4-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="637c4-170">Informacje diagnostyczne pojawi się poniżej szczegóły hello grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="637c4-171">Wybierz **widoku graficznego**.</span><span class="sxs-lookup"><span data-stu-id="637c4-171">Select **Graphical View**.</span></span> <span data-ttu-id="637c4-172">Spowoduje to wyświetlenie graficzną reprezentację hello grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="637c4-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="637c4-173">Można umieścić hello myszy przez każdy wierzchołek hello widoku toodisplay informacje o nim.</span><span class="sxs-lookup"><span data-stu-id="637c4-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Widok graficzny](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="637c4-175">Kliknięcie wierzchołek załaduje hello **szczegóły wierzchołków** dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="637c4-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="637c4-176">Polecenie hello **1 mapy** wierzchołków toodisplay szczegóły dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="637c4-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="637c4-177">Wybierz **Potwierdź** tooconfirm hello nawigacji.</span><span class="sxs-lookup"><span data-stu-id="637c4-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Szczegóły wierzchołków](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="637c4-179">Należy zauważyć, że możesz teraz łącza u góry hello hello strony, które są powiązane toovertices i zadania.</span><span class="sxs-lookup"><span data-stu-id="637c4-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="637c4-180">Tej strony można również przyjeździe, przechodząc zbyt**szczegóły DAG**, wybierając żądane **szczegóły wierzchołków**i wybierając hello **1 mapy** wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="637c4-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="637c4-181">**Liczniki wierzchołków** Wyświetla informacje o liczniku tym wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="637c4-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="637c4-182">**Zadania** Wyświetla zadania dla tego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="637c4-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="637c4-183">**Zadanie prób** Wyświetla informacje o zadaniach toorun prób dla tego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="637c4-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="637c4-184">**Źródłem & wychwytywanie** wyświetla źródła danych i sink tego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="637c4-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="637c4-185">Z menu poprzedniej hello podczas przewijania hello kolumny wyświetlanej dla zadań, toodisplay prób zadań i źródeł & Sinks__ łączy toomore informacje dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="637c4-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="637c4-186">Wybierz **zadania**, a następnie wybierz hello elementu o nazwie **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="637c4-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="637c4-187">Spowoduje to wyświetlenie **szczegóły zadania** dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="637c4-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="637c4-188">Na tym ekranie można wyświetlić **liczniki zadań** i **zadań prób**.</span><span class="sxs-lookup"><span data-stu-id="637c4-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Szczegóły zadania](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="637c4-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="637c4-190">Next Steps</span></span>
<span data-ttu-id="637c4-191">Teraz, gdy wiesz już, jak wyświetlić toouse hello Tez, Dowiedz się więcej o [przy użyciu Hive w usłudze HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="637c4-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="637c4-192">Aby uzyskać szczegółowe informacje techniczne na temat aplikacji Tez, zobacz hello [Tez strony o Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="637c4-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
