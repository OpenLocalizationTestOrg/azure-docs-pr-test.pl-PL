---
title: "Wdrażanie i zarządzanie nimi topologii Apache Storm w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrażanie, monitorowanie i zarządzanie topologiami Apache Storm na HDInsight przy użyciu pulpitu nawigacyjnego Storm. Narzędzia usługi Hadoop dla programu Visual Studio."
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
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="e387d-104">Wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Windows</span><span class="sxs-lookup"><span data-stu-id="e387d-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="e387d-105">Pulpit nawigacyjny Storm umożliwia łatwe wdrażanie i uruchamianie topologii Apache Storm do klastra usługi HDInsight przy użyciu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="e387d-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="e387d-106">Można również pulpit nawigacyjny do monitorowania i zarządzania uruchomionymi topologiami.</span><span class="sxs-lookup"><span data-stu-id="e387d-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="e387d-107">Jeśli używasz programu Visual Studio, narzędzia HDInsight Tools for Visual Studio zapewniają podobne funkcje w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e387d-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="e387d-108">Pulpit nawigacyjny Storm i funkcje systemu Storm w narzędziach HDInsight korzystają z interfejsu API REST Storm, która może służyć do tworzenia własnych monitorowania i rozwiązań do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e387d-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e387d-109">Kroki opisane w tym dokumencie wymagają Storm w klastrze usługi HDInsight, z systemem Windows jako systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e387d-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="e387d-110">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="e387d-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e387d-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="e387d-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="e387d-112">Aby uzyskać informacje dotyczące wdrażania i zarządzania topologii Storm z klastrem usługi HDInsight, który używa systemu Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e387d-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e387d-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e387d-113">Prerequisites</span></span>

* <span data-ttu-id="e387d-114">**Apache Storm w usłudze HDInsight** — zobacz [wprowadzenie do Apache Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started.md) instrukcje dotyczące tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e387d-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="e387d-115">Aby uzyskać **pulpitu nawigacyjnego Storm**: przeglądarki nowoczesnych witryn sieci web, która obsługuje protokół HTML5.</span><span class="sxs-lookup"><span data-stu-id="e387d-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="e387d-116">Dla **programu Visual Studio** -zestawu Azure SDK 2.5.1 lub nowszej i narzędzi HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e387d-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="e387d-117">Zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) do instalowania i konfigurowania narzędzi HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e387d-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="e387d-118">Jedna z następujących wersji programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e387d-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="e387d-119">Program Visual Studio 2012 z aktualizacją 4</span><span class="sxs-lookup"><span data-stu-id="e387d-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="e387d-120">Visual Studio 2013 z aktualizacją 4 lub Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="e387d-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="e387d-121">Visual Studio 2015 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="e387d-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="e387d-122">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="e387d-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="e387d-123">Pulpit nawigacyjny STORM</span><span class="sxs-lookup"><span data-stu-id="e387d-123">Storm Dashboard</span></span>

<span data-ttu-id="e387d-124">Pulpit nawigacyjny Storm jest dostępne na klaster Storm strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="e387d-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="e387d-125">Adres URL jest **https://&lt;clustername >.azurehdinsight.net/**, gdzie **clustername** jest nazwą Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e387d-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="e387d-126">W górnej części pulpitu nawigacyjnego Storm, wybierz **przesyłania topologii**.</span><span class="sxs-lookup"><span data-stu-id="e387d-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="e387d-127">Postępuj zgodnie z instrukcjami na stronie Uruchom przykładowa topologia lub aby przekazać i uruchom topologii, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="e387d-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![na stronie topologia przesyłania][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="e387d-129">STORM interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="e387d-129">Storm UI</span></span>

<span data-ttu-id="e387d-130">Wybierz z pulpitu nawigacyjnego Storm **interfejsu użytkownika platformy Storm** łącza.</span><span class="sxs-lookup"><span data-stu-id="e387d-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="e387d-131">Zostaną wyświetlone informacje o klastrze, oprócz żadnych uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![Interfejs użytkownika platformy storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="e387d-133">W niektórych wersjach programu Internet Explorer może stwierdzić, interfejsu użytkownika platformy Storm nie powoduje odświeżenia po raz pierwszy odwiedzeniu go.</span><span class="sxs-lookup"><span data-stu-id="e387d-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="e387d-134">Na przykład może nie pokazywać nowe topologie przesłane lub mogą być wyświetlane topologii jako aktywny, gdy wcześniej dezaktywowana.</span><span class="sxs-lookup"><span data-stu-id="e387d-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="e387d-135">Firma Microsoft zna tego problemu i pracuje nad rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="e387d-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="e387d-136">Strona główna</span><span class="sxs-lookup"><span data-stu-id="e387d-136">Main page</span></span>

<span data-ttu-id="e387d-137">Strona główna interfejsu użytkownika Storm udostępnia następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="e387d-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="e387d-138">**Podsumowanie klastra**: podstawowe informacje dotyczące klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="e387d-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="e387d-139">**Topologia podsumowania**: Lista uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="e387d-140">Użyj linków w tej sekcji, aby wyświetlić więcej informacji na temat określonych topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="e387d-141">**Podsumowanie przełożonego**: informacje o przełożonego Storm.</span><span class="sxs-lookup"><span data-stu-id="e387d-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="e387d-142">**Konfiguracja nimbus**: Nimbus konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="e387d-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="e387d-143">Topologia podsumowania</span><span class="sxs-lookup"><span data-stu-id="e387d-143">Topology summary</span></span>

<span data-ttu-id="e387d-144">Kliknąć łącze z **podsumowanie topologii** sekcja zawiera następujące informacje o topologii:</span><span class="sxs-lookup"><span data-stu-id="e387d-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="e387d-145">**Topologia podsumowania**: podstawowe informacje o topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="e387d-146">**Akcje topologii**: Akcje zarządzania, które można wykonywać w topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="e387d-147">**Aktywuj**: wznowienie przetwarzania dezaktywowanej topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="e387d-148">**Dezaktywuj**: wstrzymanie uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="e387d-149">**Rebalance**: dopasowanie równoległości topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="e387d-150">Po zmianie liczby węzłów w klastrze należy przeprowadzić ponowne równoważenie uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="e387d-151">Dzięki temu topologii dostosować równoległość kompensacji zwiększenia lub zmniejszenia liczby węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e387d-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="e387d-152">Aby uzyskać więcej informacji, zobacz [pojęcie równoległości w topologii Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="e387d-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="e387d-153">**Kasowanie**: kończy topologii Storm po określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="e387d-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="e387d-154">**Statystyka topologii**: Statystyka topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="e387d-155">Użyj linków w **okna** kolumnę, aby ustawić zakres czasu dla pozostałe wpisy na stronie.</span><span class="sxs-lookup"><span data-stu-id="e387d-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="e387d-156">**Spouts**: elementach spout, używany przez topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="e387d-157">Użyj łącza w tej sekcji, aby wyświetlić więcej informacji o elementach spout określonych.</span><span class="sxs-lookup"><span data-stu-id="e387d-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="e387d-158">**Bolts**: elementów bolt, używany przez topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="e387d-159">Użyj łącza w tej sekcji, aby wyświetlić więcej informacji na temat określonych elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="e387d-160">**Topologia konfiguracji**: konfiguracji wybranego topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="e387d-161">Spout i Bolt — podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e387d-161">Spout and Bolt summary</span></span>

<span data-ttu-id="e387d-162">Wybieranie spout z **Spouts** lub **Bolts** sekcje zawiera następujące informacje dotyczące wybranej pozycji:</span><span class="sxs-lookup"><span data-stu-id="e387d-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="e387d-163">**Składnik podsumowania**: podstawowe informacje o spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="e387d-164">**Spout/Bolt stats**: Statystyka spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="e387d-165">Użyj linków w **okna** kolumnę, aby ustawić zakres czasu dla pozostałe wpisy na stronie.</span><span class="sxs-lookup"><span data-stu-id="e387d-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="e387d-166">**Wprowadź statystykę** (tylko dla elementów bolt): informacje o strumienie wejściowe, używane przez elementy bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="e387d-167">**OUTPUT stats**: informacje o strumieni emitowane przez to spout ani dla elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="e387d-168">**Modułów**: informacje na temat wystąpień spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="e387d-169">Wybierz **portu** utworzony wpis dla określonego modułu wykonującego wyświetlić dziennik informacje diagnostyczne dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e387d-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="e387d-170">**Błędy**: informacje o błędzie dla tego spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="e387d-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="e387d-171">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e387d-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="e387d-172">Narzędzia HDInsight Tools może służyć do przesyłania C# i hybrydowych topologii do klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="e387d-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="e387d-173">Poniższe kroki użyć przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e387d-173">The following steps use a sample application.</span></span> <span data-ttu-id="e387d-174">Aby uzyskać informacji o tworzeniu własnych topologii za pomocą narzędzi HDInsight, zobacz [topologii opracowywania C# za pomocą narzędzi HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e387d-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="e387d-175">Wykonaj następujące kroki, aby wdrożyć przykładowe Storm w klastrze usługi HDInsight, a następnie Wyświetl i zarządzaj nimi topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="e387d-176">Jeśli nie został jeszcze zainstalowany najnowszej wersji narzędzia HDInsight Tools for Visual Studio, zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e387d-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="e387d-177">Otwórz program Visual Studio, wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="e387d-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="e387d-178">W **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **szablony**, a następnie wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e387d-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="e387d-179">Wybierz z listy szablonów **próbki Storm**.</span><span class="sxs-lookup"><span data-stu-id="e387d-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="e387d-180">W dolnej części okna dialogowego wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e387d-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![Obraz](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="e387d-182">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e387d-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e387d-183">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e387d-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="e387d-184">Jeśli masz więcej niż jedną subskrypcję, zaloguj się za jedną, która zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e387d-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="e387d-185">Wybierz Storm w klastrze usługi HDInsight z **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="e387d-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="e387d-186">Można monitorować, czy przekazywania działa prawidłowo, używając **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="e387d-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="e387d-187">Gdy topologia zostało pomyślnie przesłane, **topologii Storm** dla klastra powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="e387d-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="e387d-188">Wybierz topologię z listy, aby wyświetlić informacje o uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-188">Select the topology from the list to view information about the running topology.</span></span>

    ![monitor programu Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="e387d-190">Można również wyświetlić **topologii Storm** z **Eksploratora serwera** rozwijając **Azure** > **HDInsight**, a następnie prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierając **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="e387d-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="e387d-191">Wybierz kształt na elementach spout lub elementów bolt, aby wyświetlić informacje dotyczące tych składników.</span><span class="sxs-lookup"><span data-stu-id="e387d-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="e387d-192">Otwiera nowe okno dla każdego wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="e387d-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e387d-193">Nazwa topologii jest nazwą klasy topologii (w tym przypadku `HelloWord`,) z sygnaturą czasową dołączane.</span><span class="sxs-lookup"><span data-stu-id="e387d-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="e387d-194">Z **podsumowanie topologii** widok, wybierz opcję **Kill** przestanie topologii.</span><span class="sxs-lookup"><span data-stu-id="e387d-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e387d-195">Topologii STORM nadal działać do chwili zostały zatrzymane lub usunąć klastra.</span><span class="sxs-lookup"><span data-stu-id="e387d-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="e387d-196">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="e387d-196">REST API</span></span>

<span data-ttu-id="e387d-197">Interfejsu użytkownika platformy Storm jest oparty na interfejsie API REST, dlatego można wykonać podobne do zarządzania i monitorowania funkcji za pomocą interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="e387d-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="e387d-198">Można użyć interfejsu API REST do tworzenia niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="e387d-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="e387d-199">Aby uzyskać więcej informacji, zobacz [interfejsu API REST interfejsu użytkownika Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="e387d-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="e387d-200">Następujące informacje są specyficzne dla z systemu Apache Storm w usłudze HDInsight przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="e387d-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="e387d-201">Podstawowy identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="e387d-201">Base URI</span></span>

<span data-ttu-id="e387d-202">Podstawowy identyfikator URI dla interfejsu API REST w klastrach HDInsight jest **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, gdzie **clustername** jest nazwą Storm w usłudze HDInsight klaster.</span><span class="sxs-lookup"><span data-stu-id="e387d-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="e387d-203">Authentication</span><span class="sxs-lookup"><span data-stu-id="e387d-203">Authentication</span></span>

<span data-ttu-id="e387d-204">Żądania do interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, aby użyć nazwy administratora klastra usługi HDInsight i hasło.</span><span class="sxs-lookup"><span data-stu-id="e387d-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="e387d-205">Ponieważ uwierzytelnianie podstawowe jest wysyłany przy użyciu zwykłego tekstu, należy **zawsze** zabezpieczenia komunikacji z klastrem przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e387d-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="e387d-206">Wartości zwracane</span><span class="sxs-lookup"><span data-stu-id="e387d-206">Return values</span></span>

<span data-ttu-id="e387d-207">Można używać z wewnątrz klastra lub maszyn wirtualnych w tej samej sieci wirtualnej Azure, co klaster może być tylko informacje zwrócone z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="e387d-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="e387d-208">Na przykład w pełni kwalifikowaną nazwę (FQDN) zwróciła dozorcy serwery są nie być dostępny z Internetu.</span><span class="sxs-lookup"><span data-stu-id="e387d-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e387d-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e387d-209">Next Steps</span></span>

<span data-ttu-id="e387d-210">Teraz, kiedy znasz już sposobu wdrażania i monitorowania topologii za pomocą pulpitu nawigacyjnego Storm, Dowiedz się, jak:</span><span class="sxs-lookup"><span data-stu-id="e387d-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="e387d-211">Opracowywanie topologii C# za pomocą narzędzi HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e387d-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="e387d-212">Opracowywanie topologii opartych na języku Java za pomocą programu Maven</span><span class="sxs-lookup"><span data-stu-id="e387d-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="e387d-213">Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e387d-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
