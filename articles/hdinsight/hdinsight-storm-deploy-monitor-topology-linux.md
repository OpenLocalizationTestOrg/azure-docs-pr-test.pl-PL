---
title: "Wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrażanie, monitorowanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux przy użyciu pulpitu nawigacyjnego Storm. Narzędzia usługi Hadoop dla programu Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="77719-104">Wdrażanie i zarządzanie nimi topologii Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="77719-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="77719-105">W tym dokumencie przedstawiono podstawy zarządzania i monitorowania topologii Storm działających w Storm w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77719-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77719-106">Kroki opisane w tym artykule wymagają platformy Storm opartej na systemie Linux w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77719-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="77719-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="77719-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="77719-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="77719-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="77719-109">Aby uzyskać informacje dotyczące wdrażania i monitorowania topologii w usłudze HDInsight z systemu Windows, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="77719-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="77719-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77719-110">Prerequisites</span></span>

* <span data-ttu-id="77719-111">**Platformy Storm opartej na systemie Linux w klastrze usługi HDInsight**: zobacz [wprowadzenie do Apache Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) instrukcje dotyczące tworzenia klastra</span><span class="sxs-lookup"><span data-stu-id="77719-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="77719-112">(Opcjonalnie) **Znajomość protokołów SSH i SCP**: Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="77719-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="77719-113">(Opcjonalnie) **Programu visual Studio**: zestaw Azure SDK 2.5.1 lub nowszej i narzędzi Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77719-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="77719-114">Aby uzyskać więcej informacji, zobacz [rozpoczęcie pracy przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="77719-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="77719-115">Jedna z następujących wersji programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="77719-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="77719-116">Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="77719-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="77719-117">Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="77719-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="77719-118">Program Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="77719-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="77719-119">Visual Studio 2015 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="77719-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="77719-120">Visual Studio 2017 r (dowolna wersja).</span><span class="sxs-lookup"><span data-stu-id="77719-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="77719-121">Narzędzia Data Lake Tools dla programu Visual Studio 2017 są instalowane jako część obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="77719-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="77719-122">Przedstawia topologię: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77719-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="77719-123">Narzędzia HDInsight Tools może służyć do przesyłania C# i hybrydowych topologii do klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="77719-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="77719-124">Poniższe kroki użyć przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77719-124">The following steps use a sample application.</span></span> <span data-ttu-id="77719-125">Aby uzyskać informacji o tworzeniu własnych topologii za pomocą narzędzi HDInsight, zobacz [topologii opracowywania C# za pomocą narzędzi HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="77719-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="77719-126">Jeśli nie został już zainstalowany najnowszą wersję narzędzi Data Lake Tools dla programu Visual Studio, zobacz [rozpoczęcie pracy przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="77719-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="77719-127">Narzędzia Data Lake Tools dla programu Visual Studio były dawniej nazywane narzędzia HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77719-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="77719-128">Narzędzia Data Lake Tools dla programu Visual Studio znajdują się w __obciążenia Azure__ dla programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="77719-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="77719-129">Otwórz program Visual Studio, wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="77719-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="77719-130">W **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **szablony**, a następnie wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="77719-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="77719-131">Wybierz z listy szablonów **próbki Storm**.</span><span class="sxs-lookup"><span data-stu-id="77719-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="77719-132">W dolnej części okna dialogowego wpisz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77719-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![Obraz](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="77719-134">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="77719-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="77719-135">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77719-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="77719-136">Jeśli masz więcej niż jedną subskrypcję, zaloguj się za jedną, która zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77719-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="77719-137">Wybierz Storm w klastrze usługi HDInsight z **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="77719-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="77719-138">Można monitorować, czy przekazywania działa prawidłowo, używając **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="77719-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="77719-139">Przedstawia topologię: SSH, a polecenie Storm</span><span class="sxs-lookup"><span data-stu-id="77719-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="77719-140">Używanie protokołu SSH, aby połączyć się z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77719-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="77719-141">Zastąp **USERNAME** nazwę użytkownika logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="77719-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="77719-142">Zastąp **CLUSTERNAME** z nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77719-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="77719-143">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH do nawiązania połączenia z klastrem usługi HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="77719-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="77719-144">Użyj następującego polecenia, aby uruchomić przykładową topologię:</span><span class="sxs-lookup"><span data-stu-id="77719-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="77719-145">To polecenie uruchamia przykładową topologię WordCount w klastrze.</span><span class="sxs-lookup"><span data-stu-id="77719-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="77719-146">Ta topologia losowo wygenerowanie zdań i zliczenie wystąpień poszczególnych wyrazów w zdaniach.</span><span class="sxs-lookup"><span data-stu-id="77719-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="77719-147">Podczas przesyłania topologii do klastra przed użyciem polecenia `storm` należy skopiować plik JAR zawierający klaster.</span><span class="sxs-lookup"><span data-stu-id="77719-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="77719-148">Aby skopiować plik do klastra, można użyć `scp` polecenia.</span><span class="sxs-lookup"><span data-stu-id="77719-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="77719-149">Na przykład: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="77719-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="77719-150">Przykład WordCount i inne przykłady z projektu Storm Starter znajdują się już w klastrze w lokalizacji `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="77719-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="77719-151">Przedstawia topologię: programowe</span><span class="sxs-lookup"><span data-stu-id="77719-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="77719-152">Topologii Storm w usłudze HDInsight można programowo wdrożyć przez komunikacji z usługą Nimbus hostowanych w klastrze.</span><span class="sxs-lookup"><span data-stu-id="77719-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="77719-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-STORM-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) przykładowego aplikacji Java, która ilustruje sposób wdrażania i uruchamiania topologii za pośrednictwem usługi Nimbus.</span><span class="sxs-lookup"><span data-stu-id="77719-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="77719-154">Monitorowanie i zarządzanie nimi: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77719-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="77719-155">Gdy topologii zostało pomyślnie przesłane za pomocą programu Visual Studio, **topologii Storm** widoku pojawia się w klastrze.</span><span class="sxs-lookup"><span data-stu-id="77719-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="77719-156">Wybierz topologię z listy, aby wyświetlić informacje o uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-156">Select the topology from the list to view information about the running topology.</span></span>

![monitor programu Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="77719-158">Można również wyświetlić **topologii Storm** z **Eksploratora serwera** rozwijając **Azure** > **HDInsight**, a następnie prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierając **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="77719-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="77719-159">Wybierz kształt na elementach spout lub elementów bolt, aby wyświetlić informacje dotyczące tych składników.</span><span class="sxs-lookup"><span data-stu-id="77719-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="77719-160">Otwiera nowe okno dla każdego wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="77719-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="77719-161">Najpierw dezaktywować i ponowne uaktywnianie</span><span class="sxs-lookup"><span data-stu-id="77719-161">Deactivate and reactivate</span></span>

<span data-ttu-id="77719-162">Dezaktywowanie topologii wstrzymuje go dopóki zostanie przerwana lub ponownej aktywacji.</span><span class="sxs-lookup"><span data-stu-id="77719-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="77719-163">Aby wykonać te operacje, należy użyć __Dezaktywuj__ i __ponownie uaktywnić__ przycisków w górnej części __podsumowanie topologii__.</span><span class="sxs-lookup"><span data-stu-id="77719-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="77719-164">Ponownie Zrównoważ</span><span class="sxs-lookup"><span data-stu-id="77719-164">Rebalance</span></span>

<span data-ttu-id="77719-165">Ponowne równoważenie topologii umożliwi systemowi Popraw równoległości topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="77719-166">Na przykład jeśli zmieniono klastra, aby dodać więcej uwagi, ponowne równoważenie umożliwia topologii zobaczyć nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="77719-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="77719-167">Aby ponowne zrównoważenie topologii, użyj __Rebalance__ przycisk w górnej części __podsumowanie topologii__.</span><span class="sxs-lookup"><span data-stu-id="77719-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="77719-168">Ponowne równoważenie topologii najpierw dezaktywuje topologii, ponownie dystrybuuje pracowników równomiernie w ramach klastra, a następnie na koniec zwraca topologii do stanu sprzed ponowne równoważenie wystąpił.</span><span class="sxs-lookup"><span data-stu-id="77719-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="77719-169">Dlatego jeśli topologii był aktywny, staje się aktywny ponownie.</span><span class="sxs-lookup"><span data-stu-id="77719-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="77719-170">Jeśli została ona zdezaktywowana, pozostaje dezaktywowane.</span><span class="sxs-lookup"><span data-stu-id="77719-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="77719-171">Kasowanie topologii</span><span class="sxs-lookup"><span data-stu-id="77719-171">Kill a topology</span></span>

<span data-ttu-id="77719-172">Topologii STORM nadal działać do chwili zostały zatrzymane lub usunąć klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="77719-173">Aby zatrzymać topologii, użyj __Kill__ przycisk w górnej części __podsumowanie topologii__.</span><span class="sxs-lookup"><span data-stu-id="77719-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="77719-174">Monitorowanie i zarządzanie nimi: SSH, a polecenie Storm</span><span class="sxs-lookup"><span data-stu-id="77719-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="77719-175">`storm` Narzędzie umożliwia pracę z uruchomionymi topologiami z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="77719-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="77719-176">Użyj `storm -h` pełną listę poleceń.</span><span class="sxs-lookup"><span data-stu-id="77719-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="77719-177">Topologie listy</span><span class="sxs-lookup"><span data-stu-id="77719-177">List topologies</span></span>

<span data-ttu-id="77719-178">Użyj następującego polecenia, aby wyświetlić listę wszystkich uruchomionymi topologiami:</span><span class="sxs-lookup"><span data-stu-id="77719-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="77719-179">To polecenie zwraca informacje podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="77719-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="77719-180">Najpierw dezaktywować i ponowne uaktywnianie</span><span class="sxs-lookup"><span data-stu-id="77719-180">Deactivate and reactivate</span></span>

<span data-ttu-id="77719-181">Dezaktywowanie topologii wstrzymuje go dopóki zostanie przerwana lub ponownej aktywacji.</span><span class="sxs-lookup"><span data-stu-id="77719-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="77719-182">Aby zdezaktywować i ponownie uaktywnić, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="77719-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="77719-183">Kasowanie uruchomionej topologii</span><span class="sxs-lookup"><span data-stu-id="77719-183">Kill a running topology</span></span>

<span data-ttu-id="77719-184">STORM topologii po uruchomieniu, nadal uruchomione aż do zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="77719-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="77719-185">Aby zatrzymać topologii, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="77719-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="77719-186">Ponownie Zrównoważ</span><span class="sxs-lookup"><span data-stu-id="77719-186">Rebalance</span></span>

<span data-ttu-id="77719-187">Ponowne równoważenie topologii umożliwi systemowi Popraw równoległości topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="77719-188">Na przykład jeśli zmieniono klastra, aby dodać więcej uwagi, ponowne równoważenie umożliwia topologii zobaczyć nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="77719-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="77719-189">Ponowne równoważenie topologii najpierw dezaktywuje topologii, ponownie dystrybuuje pracowników równomiernie w ramach klastra, a następnie na koniec zwraca topologii do stanu sprzed ponowne równoważenie wystąpił.</span><span class="sxs-lookup"><span data-stu-id="77719-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="77719-190">Dlatego jeśli topologii był aktywny, staje się aktywny ponownie.</span><span class="sxs-lookup"><span data-stu-id="77719-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="77719-191">Jeśli została ona zdezaktywowana, pozostaje dezaktywowane.</span><span class="sxs-lookup"><span data-stu-id="77719-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="77719-192">Monitorowanie i zarządzanie nimi: Storm interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="77719-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="77719-193">Interfejs użytkownika platformy Storm udostępnia interfejs sieci Web do pracy z uruchomionymi topologiami i jest zawarty w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77719-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="77719-194">Aby wyświetlić interfejsu użytkownika platformy Storm, użyj przeglądarki sieci web, aby otworzyć **https://CLUSTERNAME.azurehdinsight.net/stormui**, gdzie **CLUSTERNAME** jest nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="77719-195">Jeśli zostanie wyświetlony monit o podanie nazwy użytkownika i hasła, wprowadź nazwę administratora klastra (admin) i hasło użyte podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="77719-196">Strona główna</span><span class="sxs-lookup"><span data-stu-id="77719-196">Main page</span></span>

<span data-ttu-id="77719-197">Strona główna interfejsu użytkownika Storm udostępnia następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="77719-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="77719-198">**Podsumowanie klastra**: podstawowe informacje dotyczące klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="77719-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="77719-199">**Topologia podsumowania**: Lista uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="77719-200">Użyj linków w tej sekcji, aby wyświetlić więcej informacji na temat określonych topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="77719-201">**Podsumowanie przełożonego**: informacje o przełożonego Storm.</span><span class="sxs-lookup"><span data-stu-id="77719-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="77719-202">**Konfiguracja nimbus**: Nimbus konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="77719-203">Topologia podsumowania</span><span class="sxs-lookup"><span data-stu-id="77719-203">Topology summary</span></span>

<span data-ttu-id="77719-204">Kliknąć łącze z **podsumowanie topologii** sekcja zawiera następujące informacje o topologii:</span><span class="sxs-lookup"><span data-stu-id="77719-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="77719-205">**Topologia podsumowania**: podstawowe informacje o topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="77719-206">**Akcje topologii**: Akcje zarządzania, które można wykonywać w topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="77719-207">**Aktywuj**: wznowienie przetwarzania dezaktywowanej topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="77719-208">**Dezaktywuj**: wstrzymanie uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="77719-209">**Rebalance**: dopasowanie równoległości topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="77719-210">Po zmianie liczby węzłów w klastrze należy przeprowadzić ponowne równoważenie uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="77719-211">Ta operacja pozwala topologii dostosować równoległość kompensacji zwiększenia lub zmniejszenia liczby węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="77719-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="77719-212">Aby uzyskać więcej informacji, zobacz temat <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Pojęcie równoległości w topologii Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="77719-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="77719-213">**Kasowanie**: kończy topologii Storm po określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="77719-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="77719-214">**Statystyka topologii**: Statystyka topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="77719-215">Aby ustawić zakres czasu dla pozostałe wpisy na stronie, użyj linków w **okna** kolumny.</span><span class="sxs-lookup"><span data-stu-id="77719-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="77719-216">**Spouts**: elementach spout, używany przez topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="77719-217">Użyj łącza w tej sekcji, aby wyświetlić więcej informacji o elementach spout określonych.</span><span class="sxs-lookup"><span data-stu-id="77719-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="77719-218">**Bolts**: elementów bolt, używany przez topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="77719-219">Użyj łącza w tej sekcji, aby wyświetlić więcej informacji na temat określonych elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="77719-220">**Topologia konfiguracji**: konfiguracji wybranego topologii.</span><span class="sxs-lookup"><span data-stu-id="77719-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="77719-221">Spout i Bolt — podsumowanie</span><span class="sxs-lookup"><span data-stu-id="77719-221">Spout and Bolt summary</span></span>

<span data-ttu-id="77719-222">Wybieranie spout z **Spouts** lub **Bolts** sekcje zawiera następujące informacje dotyczące wybranej pozycji:</span><span class="sxs-lookup"><span data-stu-id="77719-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="77719-223">**Składnik podsumowania**: podstawowe informacje o spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="77719-224">**Spout/Bolt stats**: Statystyka spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="77719-225">Aby ustawić zakres czasu dla pozostałe wpisy na stronie, użyj linków w **okna** kolumny.</span><span class="sxs-lookup"><span data-stu-id="77719-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="77719-226">**Wprowadź statystykę** (tylko dla elementów bolt): informacje o strumienie wejściowe, używane przez elementy bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="77719-227">**OUTPUT stats**: informacje o strumieni emitowane przez to spout ani dla elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="77719-228">**Modułów**: informacje na temat wystąpień spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="77719-229">Wybierz **portu** utworzony wpis dla określonego modułu wykonującego wyświetlić dziennik informacje diagnostyczne dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="77719-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="77719-230">**Błędy**: informacje o błędzie dla tego spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="77719-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="77719-231">Monitorowanie i zarządzanie nimi: interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="77719-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="77719-232">Interfejsu użytkownika platformy Storm jest oparty na interfejsie API REST, dlatego można wykonać podobne do zarządzania i monitorowania funkcji za pomocą interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="77719-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="77719-233">Można użyć interfejsu API REST do tworzenia niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="77719-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="77719-234">Aby uzyskać więcej informacji, zobacz [interfejsu API REST interfejsu użytkownika Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="77719-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="77719-235">Następujące informacje są specyficzne dla z systemu Apache Storm w usłudze HDInsight przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="77719-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77719-236">Interfejs API REST Storm nie jest publicznie dostępna przez internet i muszą być dostępne przy użyciu tunelu SSH do węzła głównego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77719-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="77719-237">Aby uzyskać informacje na temat tworzenia i używania tunelu SSH, zobacz [Użyj SSH Tunneling można uzyskać dostępu do interfejsu użytkownika sieci web Ambari, ResourceManager, JobHistory, NameNode, Oozie i innych sieci web UI](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="77719-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="77719-238">Podstawowy identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="77719-238">Base URI</span></span>

<span data-ttu-id="77719-239">Podstawowy identyfikator URI dla interfejsu API REST w klastrach HDInsight opartych na systemie Linux jest dostępna w węźle głównym na **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="77719-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="77719-240">Nazwa węzła głównego domeny jest generowany podczas tworzenia klastra i nie jest statyczne.</span><span class="sxs-lookup"><span data-stu-id="77719-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="77719-241">W pełni kwalifikowaną nazwę (FQDN) dla węzła głównego klastra można znaleźć na kilka różnych sposobów:</span><span class="sxs-lookup"><span data-stu-id="77719-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="77719-242">**W sesji SSH**: Użyj polecenia `headnode -f` w sesji SSH do klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="77719-243">**Z sieci Ambari Web**: Wybierz **usług** w górnej części strony, następnie wybierz **Storm**.</span><span class="sxs-lookup"><span data-stu-id="77719-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="77719-244">Z **Podsumowanie** wybierz opcję **serwera interfejsu użytkownika Storm**.</span><span class="sxs-lookup"><span data-stu-id="77719-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="77719-245">Nazwa FQDN węzła, który działa interfejsu użytkownika platformy Storm i interfejsu API REST jest w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="77719-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="77719-246">**Z interfejsu API REST Ambari**: Użyj polecenia `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` można pobrać informacji na temat interfejsu użytkownika platformy Storm i interfejsu API REST są uruchomione na węzeł.</span><span class="sxs-lookup"><span data-stu-id="77719-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="77719-247">Zastąp **hasło** o hasło administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="77719-248">Zastąp **CLUSTERNAME** z nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="77719-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="77719-249">W odpowiedzi wpis "host_name" zawiera nazwę FQDN węzła.</span><span class="sxs-lookup"><span data-stu-id="77719-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="77719-250">Authentication</span><span class="sxs-lookup"><span data-stu-id="77719-250">Authentication</span></span>

<span data-ttu-id="77719-251">Żądania do interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, aby użyć nazwy administratora klastra usługi HDInsight i hasło.</span><span class="sxs-lookup"><span data-stu-id="77719-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="77719-252">Ponieważ uwierzytelnianie podstawowe jest wysyłany przy użyciu zwykłego tekstu, należy **zawsze** zabezpieczenia komunikacji z klastrem przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="77719-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="77719-253">Wartości zwracane</span><span class="sxs-lookup"><span data-stu-id="77719-253">Return values</span></span>

<span data-ttu-id="77719-254">Można używać z wewnątrz klastra lub maszyn wirtualnych w tej samej sieci wirtualnej Azure, co klaster może być tylko informacje zwrócone z interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="77719-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="77719-255">Na przykład w pełni kwalifikowaną nazwę (FQDN) zwróciła dozorcy serwerów jest nie być dostępny z Internetu.</span><span class="sxs-lookup"><span data-stu-id="77719-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77719-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77719-256">Next Steps</span></span>

<span data-ttu-id="77719-257">Teraz, kiedy znasz już sposobu wdrażania i monitorowania topologii za pomocą pulpitu nawigacyjnego Storm, Dowiedz się, jak [topologie oparte na opracowanie Java za pomocą programu Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="77719-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="77719-258">Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="77719-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
