---
title: "aaaDeploy i zarządzanie topologiami Apache Storm na HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy, monitorować i zarządzać nimi za pomocą hello pulpit nawigacyjny Storm w usłudze HDInsight topologii Apache Storm. Narzędzia usługi Hadoop dla programu Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="d5f18-104">Wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Windows</span><span class="sxs-lookup"><span data-stu-id="d5f18-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="d5f18-105">pulpit nawigacyjny Storm Hello umożliwia tooeasily wdrażanie i uruchamianie klastra usługi HDInsight tooyour topologii Apache Storm za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="d5f18-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="d5f18-106">Można również użyć hello toomonitor pulpitu nawigacyjnego i zarządzania uruchomionymi topologiami.</span><span class="sxs-lookup"><span data-stu-id="d5f18-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="d5f18-107">Jeśli używasz programu Visual Studio hello narzędzia HDInsight Tools for Visual Studio zapewniają podobne funkcje w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5f18-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="d5f18-108">Hello pulpit nawigacyjny Storm i funkcje Storm hello hello narzędzi HDInsight Tools korzystają z interfejsu API REST Storm, które mogą być używane toocreate hello własnych rozwiązań do zarządzania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="d5f18-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5f18-109">kroki Hello w tym dokumencie wymagają Storm w klastrze usługi HDInsight, z systemem Windows jako hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d5f18-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="d5f18-110">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d5f18-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d5f18-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="d5f18-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="d5f18-112">Aby uzyskać informacje dotyczące wdrażania i zarządzania topologii Storm z klastrem usługi HDInsight, który używa systemu Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="d5f18-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5f18-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d5f18-113">Prerequisites</span></span>

* <span data-ttu-id="d5f18-114">**Apache Storm w usłudze HDInsight** — zobacz [wprowadzenie do Apache Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started.md) instrukcje dotyczące tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d5f18-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="d5f18-115">Dla hello **pulpitu nawigacyjnego Storm**: przeglądarki nowoczesnych witryn sieci web, która obsługuje protokół HTML5.</span><span class="sxs-lookup"><span data-stu-id="d5f18-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="d5f18-116">Dla **programu Visual Studio** -zestawu Azure SDK 2.5.1 lub nowszej i hello narzędzi HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5f18-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="d5f18-117">Zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall i skonfigurować hello HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5f18-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="d5f18-118">Jedna z hello następujące wersje programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d5f18-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="d5f18-119">Program Visual Studio 2012 z aktualizacją 4</span><span class="sxs-lookup"><span data-stu-id="d5f18-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="d5f18-120">Visual Studio 2013 z aktualizacją 4 lub Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="d5f18-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="d5f18-121">Visual Studio 2015 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="d5f18-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="d5f18-122">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="d5f18-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="d5f18-123">Pulpit nawigacyjny STORM</span><span class="sxs-lookup"><span data-stu-id="d5f18-123">Storm Dashboard</span></span>

<span data-ttu-id="d5f18-124">Hello pulpit nawigacyjny Storm jest dostępne na klaster Storm strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="d5f18-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="d5f18-125">adres URL Hello jest **https://&lt;clustername >.azurehdinsight.net/**, gdzie **clustername** jest nazwą hello Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5f18-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="d5f18-126">Z góry hello hello pulpit nawigacyjny Storm, wybierz **przesyłania topologii**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="d5f18-127">Postępuj zgodnie z instrukcjami hello na powitania strony toorun przykładowa topologia lub tooupload i uruchom topologii, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="d5f18-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Witaj przesyłania topologii strony][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="d5f18-129">STORM interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d5f18-129">Storm UI</span></span>

<span data-ttu-id="d5f18-130">Hello pulpit nawigacyjny Storm, zaznacz hello **interfejsu użytkownika platformy Storm** łącza.</span><span class="sxs-lookup"><span data-stu-id="d5f18-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="d5f18-131">Informacje o klastrze hello, spowoduje to wyświetlenie w tooany dodanie uruchomionymi topologiami.</span><span class="sxs-lookup"><span data-stu-id="d5f18-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![Witaj interfejsu użytkownika platformy storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="d5f18-133">W niektórych wersjach programu Internet Explorer może stwierdzić, że powitalne interfejsu użytkownika platformy Storm nie powoduje odświeżenia po raz pierwszy odwiedzeniu go.</span><span class="sxs-lookup"><span data-stu-id="d5f18-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="d5f18-134">Na przykład może nie pokazywać topologii nowy hello przesłane lub mogą być wyświetlane topologii jako aktywny, gdy wcześniej dezaktywowana.</span><span class="sxs-lookup"><span data-stu-id="d5f18-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="d5f18-135">Firma Microsoft zna tego problemu i pracuje nad rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="d5f18-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="d5f18-136">Strona główna</span><span class="sxs-lookup"><span data-stu-id="d5f18-136">Main page</span></span>

<span data-ttu-id="d5f18-137">strony główne Hello hello interfejsu użytkownika platformy Storm udostępnia hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="d5f18-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="d5f18-138">**Podsumowanie klastra**: podstawowe informacje o hello klaster Storm.</span><span class="sxs-lookup"><span data-stu-id="d5f18-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="d5f18-139">**Topologia podsumowania**: Lista uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="d5f18-140">Użyj hello łącza w tej sekcji tooview więcej informacji o określonych topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="d5f18-141">**Podsumowanie przełożonego**: informacje o przełożonego Storm hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="d5f18-142">**Konfiguracja nimbus**: Konfiguracja Nimbus hello klastra.</span><span class="sxs-lookup"><span data-stu-id="d5f18-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="d5f18-143">Topologia podsumowania</span><span class="sxs-lookup"><span data-stu-id="d5f18-143">Topology summary</span></span>

<span data-ttu-id="d5f18-144">Wybieranie łącza z hello **podsumowanie topologii** sekcja wyświetla następujące informacje o topologii hello hello:</span><span class="sxs-lookup"><span data-stu-id="d5f18-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="d5f18-145">**Topologia podsumowania**: podstawowe informacje o topologii hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="d5f18-146">**Akcje topologii**: Akcje zarządzania, które można wykonywać w odniesieniu do topologii hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="d5f18-147">**Aktywuj**: wznowienie przetwarzania dezaktywowanej topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="d5f18-148">**Dezaktywuj**: wstrzymanie uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="d5f18-149">**Rebalance**: można dostosować równoległość hello hello topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="d5f18-150">Po zmianie hello liczby węzłów w klastrze hello, należy przeprowadzić ponowne równoważenie uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="d5f18-151">Dzięki temu hello topologii tooadjust równoległości toocompensate dla hello zwiększyć lub zmniejszyć liczbę węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="d5f18-152">Aby uzyskać więcej informacji, zobacz [opis hello równoległości topologii Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="d5f18-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="d5f18-153">**Kasowanie**: kończy topologii Storm po hello określony limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d5f18-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="d5f18-154">**Statystyka topologii**: Statystyka topologii hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="d5f18-155">Użyj łączy hello w hello **okna** kolumny tooset hello ramy czasowe hello pozostałe wpisy na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d5f18-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="d5f18-156">**Spouts**: hello elementach spout używane przez hello topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="d5f18-157">Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementach spout.</span><span class="sxs-lookup"><span data-stu-id="d5f18-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="d5f18-158">**Bolts**: hello używane przez hello topologii elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="d5f18-159">Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="d5f18-160">**Topologia konfiguracji**: hello konfiguracji topologii hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="d5f18-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="d5f18-161">Spout i Bolt — podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d5f18-161">Spout and Bolt summary</span></span>

<span data-ttu-id="d5f18-162">Wybieranie spout z hello **Spouts** lub **Bolts** sekcje Wyświetla hello następujących informacji o elemencie hello wybrane:</span><span class="sxs-lookup"><span data-stu-id="d5f18-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="d5f18-163">**Składnik podsumowania**: podstawowe informacje o hello spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="d5f18-164">**Spout/Bolt stats**: Statystyka hello spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="d5f18-165">Użyj łączy hello w hello **okna** kolumny tooset hello ramy czasowe hello pozostałe wpisy na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d5f18-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="d5f18-166">**Wprowadź statystykę** (tylko dla elementów bolt): informacje o hello strumienie używane przez hello bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="d5f18-167">**OUTPUT stats**: informacje o strumieni hello emitowane przez to spout ani dla elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="d5f18-168">**Modułów**: informacje na temat wystąpień hello hello spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="d5f18-169">Wybierz hello **portu** wpis dla tooview określonego modułu wykonującego dziennika informacji diagnostycznych utworzone dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="d5f18-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="d5f18-170">**Błędy**: informacje o błędzie dla tego spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="d5f18-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="d5f18-171">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5f18-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="d5f18-172">Narzędzia HDInsight Hello mogą być używane toosubmit C# i hybrydowych topologii tooyour klaster Storm.</span><span class="sxs-lookup"><span data-stu-id="d5f18-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="d5f18-173">Witaj, wykonaj czynności użyć przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5f18-173">hello following steps use a sample application.</span></span> <span data-ttu-id="d5f18-174">Informacji o tworzeniu własnych topologii za pomocą narzędzi HDInsight hello, zobacz [topologii opracowywania C# za pomocą hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d5f18-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="d5f18-175">Użyj następujących hello kroki toodeploy tooyour próbki Storm w klastrze usługi HDInsight, a następnie Wyświetl i Zarządzaj hello topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="d5f18-176">Jeśli nie został już zainstalowany hello najnowszą wersję hello narzędzi HDInsight Tools for Visual Studio, zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5f18-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="d5f18-177">Otwórz program Visual Studio, wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="d5f18-178">W hello **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **szablony**, a następnie wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="d5f18-179">Wybierz z listy hello szablonów **próbki Storm**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="d5f18-180">U dołu hello hello — okno dialogowe wpisz nazwę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Obraz](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="d5f18-182">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5f18-183">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5f18-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="d5f18-184">Jeśli masz więcej niż jedną subskrypcję, zaloguj się za toohello, który zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5f18-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="d5f18-185">Wybierz Storm w klastrze usługi HDInsight z hello **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="d5f18-186">Można monitorować, czy przesyłanie hello działa prawidłowo, używając hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="d5f18-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="d5f18-187">Gdy topologia hello został pomyślnie przesłany, hello **topologii Storm** dla klastra hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="d5f18-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="d5f18-188">Wybierz topologię hello z hello listy tooview informacji na temat hello systemem topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![monitor programu Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="d5f18-190">Można również wyświetlić **topologii Storm** z **Eksploratora serwera** rozwijając **Azure** > **HDInsight**, a następnie prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierając **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="d5f18-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="d5f18-191">Wybierz kształt hello hello spouts lub bolts tooview informacji dotyczących tych składników.</span><span class="sxs-lookup"><span data-stu-id="d5f18-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="d5f18-192">Otwiera nowe okno dla każdego wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="d5f18-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5f18-193">Nazwa Hello topologii hello jest nazwą klasy hello topologii hello (w tym przypadku `HelloWord`,) z sygnaturą czasową dołączane.</span><span class="sxs-lookup"><span data-stu-id="d5f18-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="d5f18-194">Z hello **podsumowanie topologii** widok, wybierz opcję **Kill** toostop hello topologii.</span><span class="sxs-lookup"><span data-stu-id="d5f18-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5f18-195">Topologii STORM nadal działać do chwili zostały zatrzymane lub hello klastra zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="d5f18-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="d5f18-196">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d5f18-196">REST API</span></span>

<span data-ttu-id="d5f18-197">Hello interfejsu użytkownika platformy Storm jest oparty na powitania interfejsu API REST, więc można wykonać podobne do zarządzania i monitorowania funkcji przy użyciu hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="d5f18-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="d5f18-198">Można użyć interfejsu API REST hello toocreate niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="d5f18-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="d5f18-199">Aby uzyskać więcej informacji, zobacz [interfejsu API REST interfejsu użytkownika Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="d5f18-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="d5f18-200">Witaj następujące informacje są hello toousing określonego interfejsu API REST z systemu Apache Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5f18-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="d5f18-201">Podstawowy identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="d5f18-201">Base URI</span></span>

<span data-ttu-id="d5f18-202">Hello jest podstawowy identyfikator URI dla hello interfejsu API REST w klastrach HDInsight **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, gdzie **clustername** jest nazwą hello Storm na Klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5f18-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="d5f18-203">Authentication</span><span class="sxs-lookup"><span data-stu-id="d5f18-203">Authentication</span></span>

<span data-ttu-id="d5f18-204">Toohello żądania interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, więc użyć hello HDInsight klastra nazwę i hasło administratora.</span><span class="sxs-lookup"><span data-stu-id="d5f18-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="d5f18-205">Ponieważ uwierzytelnianie podstawowe jest wysyłany przy użyciu zwykłego tekstu, należy **zawsze** połączeń toosecure HTTPS za pomocą hello klastra.</span><span class="sxs-lookup"><span data-stu-id="d5f18-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5f18-206">Wartości zwracane</span><span class="sxs-lookup"><span data-stu-id="d5f18-206">Return values</span></span>

<span data-ttu-id="d5f18-207">Informacje zwrócone z hello interfejsu API REST mogą być tylko można używać z wewnątrz klastra hello lub maszyn wirtualnych na hello tej samej sieci wirtualnej platformy Azure jako klaster hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="d5f18-208">Na przykład hello pełną nazwę domeny (FQDN) dla serwerów dozorcy zwracane są nie być dostępny z Internetu hello.</span><span class="sxs-lookup"><span data-stu-id="d5f18-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5f18-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5f18-209">Next Steps</span></span>

<span data-ttu-id="d5f18-210">Teraz, kiedy znasz już jak topologie toodeploy i monitorować za pomocą hello pulpit nawigacyjny Storm, Dowiedz się jak:</span><span class="sxs-lookup"><span data-stu-id="d5f18-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="d5f18-211">Opracowywanie topologii C# za pomocą hello HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5f18-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="d5f18-212">Opracowywanie topologii opartych na języku Java za pomocą programu Maven</span><span class="sxs-lookup"><span data-stu-id="d5f18-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="d5f18-213">Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d5f18-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
