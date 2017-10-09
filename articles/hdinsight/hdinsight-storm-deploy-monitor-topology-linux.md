---
title: "aaaDeploy i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy, monitorowanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux przy użyciu hello pulpit nawigacyjny Storm. Narzędzia usługi Hadoop dla programu Visual Studio."
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
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="6d3bd-104">Wdrażanie i zarządzanie nimi topologii Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d3bd-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="6d3bd-105">Dowiedz się hello podstawowe informacje dotyczące zarządzania i monitorowania topologii Storm działających w Storm w klastrach HDInsight, w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d3bd-106">Witaj kroki opisane w tym artykule wymagają platformy Storm opartej na systemie Linux w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="6d3bd-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d3bd-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="6d3bd-109">Aby uzyskać informacje dotyczące wdrażania i monitorowania topologii w usłudze HDInsight z systemu Windows, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="6d3bd-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6d3bd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6d3bd-110">Prerequisites</span></span>

* <span data-ttu-id="6d3bd-111">**Platformy Storm opartej na systemie Linux w klastrze usługi HDInsight**: zobacz [wprowadzenie do Apache Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) instrukcje dotyczące tworzenia klastra</span><span class="sxs-lookup"><span data-stu-id="6d3bd-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="6d3bd-112">(Opcjonalnie) **Znajomość protokołów SSH i SCP**: Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="6d3bd-113">(Opcjonalnie) **Programu visual Studio**: zestaw Azure SDK 2.5.1 lub nowszej i hello narzędzi Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="6d3bd-114">Aby uzyskać więcej informacji, zobacz [rozpoczęcie pracy przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="6d3bd-115">Jedna z hello następujące wersje programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="6d3bd-116">Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="6d3bd-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="6d3bd-117">Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="6d3bd-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="6d3bd-118">Program Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="6d3bd-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="6d3bd-119">Visual Studio 2015 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="6d3bd-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="6d3bd-120">Visual Studio 2017 r (dowolna wersja).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="6d3bd-121">Narzędzia Data Lake Tools dla programu Visual Studio 2017 są instalowane jako część hello Azure obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="6d3bd-122">Przedstawia topologię: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d3bd-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="6d3bd-123">Narzędzia HDInsight Hello mogą być używane toosubmit C# i hybrydowych topologii tooyour klaster Storm.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="6d3bd-124">Witaj, wykonaj czynności użyć przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-124">hello following steps use a sample application.</span></span> <span data-ttu-id="6d3bd-125">Informacji o tworzeniu własnych topologii za pomocą narzędzi HDInsight hello, zobacz [topologii opracowywania C# za pomocą hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="6d3bd-126">Jeśli hello najnowszą wersję narzędzia Data Lake hello nie jest już zainstalowany dla programu Visual Studio, zobacz [rozpoczęcie pracy przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="6d3bd-127">Hello narzędzi Data Lake Tools dla programu Visual Studio były dawniej nazywane hello HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="6d3bd-128">Narzędzia Data Lake Tools dla programu Visual Studio znajdują się w hello __obciążenia Azure__ dla programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="6d3bd-129">Otwórz program Visual Studio, wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="6d3bd-130">W hello **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **szablony**, a następnie wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="6d3bd-131">Wybierz z listy hello szablonów **próbki Storm**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="6d3bd-132">U dołu hello hello — okno dialogowe wpisz nazwę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Obraz](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="6d3bd-134">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d3bd-135">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="6d3bd-136">Jeśli masz więcej niż jedną subskrypcję, zaloguj się za toohello, który zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="6d3bd-137">Wybierz Storm w klastrze usługi HDInsight z hello **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="6d3bd-138">Można monitorować, czy przesyłanie hello działa prawidłowo, używając hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="6d3bd-139">Przedstawia topologię: SSH i hello Storm polecenia</span><span class="sxs-lookup"><span data-stu-id="6d3bd-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="6d3bd-140">Użyj klastra usługi HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="6d3bd-141">Zastąp **USERNAME** hello nazwa logowania użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="6d3bd-142">Zastąp **CLUSTERNAME** z nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="6d3bd-143">Aby uzyskać więcej informacji na temat używania SSH tooconnect tooyour HDInsight klastra, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6d3bd-144">Użyj następującego polecenia toostart przykładową topologię hello:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="6d3bd-145">To polecenie uruchamia hello przykładową topologię WordCount na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="6d3bd-146">Ta topologia losowego generowania zdań i hello liczby wystąpień poszczególnych wyrazów w zdaniach hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d3bd-147">Podczas przesyłania topologii toohello klastra, należy najpierw skopiować plik jar hello zawierający hello klastra przed użyciem hello `storm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="6d3bd-148">toocopy hello pliku toohello klastra, można użyć hello `scp` polecenia.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="6d3bd-149">Na przykład: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="6d3bd-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="6d3bd-150">przykład Witaj WordCount i inne przykłady storm starter, znajdują się już w klastrze na `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="6d3bd-151">Przedstawia topologię: programowe</span><span class="sxs-lookup"><span data-stu-id="6d3bd-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="6d3bd-152">TooStorm topologii, w usłudze HDInsight można wdrożyć programowo przy komunikacji z hello Nimbus usług hostowanych w klastrze.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="6d3bd-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-STORM-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) przykładowego aplikacji w języku Java pokazano, jak toodeploy i uruchomić topologii za pośrednictwem hello usługi Nimbus.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="6d3bd-154">Monitorowanie i zarządzanie nimi: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d3bd-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="6d3bd-155">Gdy topologii zostało pomyślnie przesłane za pomocą programu Visual Studio, hello **topologii Storm** widoku hello klastra jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="6d3bd-156">Wybierz topologię hello z hello listy tooview informacji na temat hello systemem topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![monitor programu Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="6d3bd-158">Można również wyświetlić **topologii Storm** z **Eksploratora serwera** rozwijając **Azure** > **HDInsight**, a następnie prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierając **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="6d3bd-159">Wybierz kształt hello hello spouts lub bolts tooview informacji dotyczących tych składników.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="6d3bd-160">Otwiera nowe okno dla każdego wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="6d3bd-161">Najpierw dezaktywować i ponowne uaktywnianie</span><span class="sxs-lookup"><span data-stu-id="6d3bd-161">Deactivate and reactivate</span></span>

<span data-ttu-id="6d3bd-162">Dezaktywowanie topologii wstrzymuje go dopóki zostanie przerwana lub ponownej aktywacji.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="6d3bd-163">tooperform te operacje, użyj hello __Dezaktywuj__ i __ponownie uaktywnić__ przyciski u góry hello hello __podsumowanie topologii__.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="6d3bd-164">Ponownie Zrównoważ</span><span class="sxs-lookup"><span data-stu-id="6d3bd-164">Rebalance</span></span>

<span data-ttu-id="6d3bd-165">Ponowne równoważenie topologii umożliwia hello systemu toorevise hello równoległość topologii hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="6d3bd-166">Na przykład jeśli ma zmieniony tooadd klastra hello dodatkowych notatek, ponowne równoważenie umożliwia topologii toosee hello nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="6d3bd-167">toorebalance topologii, użyj hello __Rebalance__ u góry hello hello __podsumowanie topologii__.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="6d3bd-168">Ponowne równoważenie topologii najpierw dezaktywuje topologii hello ponownie dystrybuuje pracowników równomiernie między hello klastra, a następnie finally zwraca hello topologii toohello stanu sprzed ponowne równoważenie wystąpił.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="6d3bd-169">Tak topologii hello był aktywny, staje się aktywny ponownie.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="6d3bd-170">Jeśli została ona zdezaktywowana, pozostaje dezaktywowane.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="6d3bd-171">Kasowanie topologii</span><span class="sxs-lookup"><span data-stu-id="6d3bd-171">Kill a topology</span></span>

<span data-ttu-id="6d3bd-172">Topologii STORM nadal działać do chwili zostały zatrzymane lub hello klastra zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="6d3bd-173">toostop topologii, użyj hello __Kill__ u góry hello hello __podsumowanie topologii__.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="6d3bd-174">Monitorowanie i zarządzanie nimi: SSH i hello Storm polecenia</span><span class="sxs-lookup"><span data-stu-id="6d3bd-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="6d3bd-175">Witaj `storm` narzędzie umożliwia toowork z uruchomionymi topologiami z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="6d3bd-176">Użyj `storm -h` pełną listę poleceń.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="6d3bd-177">Topologie listy</span><span class="sxs-lookup"><span data-stu-id="6d3bd-177">List topologies</span></span>

<span data-ttu-id="6d3bd-178">Użyj następującego polecenia toolist hello wszystkich uruchomionych topologii:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="6d3bd-179">To polecenie zwraca informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="6d3bd-180">Najpierw dezaktywować i ponowne uaktywnianie</span><span class="sxs-lookup"><span data-stu-id="6d3bd-180">Deactivate and reactivate</span></span>

<span data-ttu-id="6d3bd-181">Dezaktywowanie topologii wstrzymuje go dopóki zostanie przerwana lub ponownej aktywacji.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="6d3bd-182">Użyj następującego polecenia toodeactivate hello i Uaktywnij ponownie:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="6d3bd-183">Kasowanie uruchomionej topologii</span><span class="sxs-lookup"><span data-stu-id="6d3bd-183">Kill a running topology</span></span>

<span data-ttu-id="6d3bd-184">STORM topologii po uruchomieniu, nadal uruchomione aż do zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="6d3bd-185">toostop topologii, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="6d3bd-186">Ponownie Zrównoważ</span><span class="sxs-lookup"><span data-stu-id="6d3bd-186">Rebalance</span></span>

<span data-ttu-id="6d3bd-187">Ponowne równoważenie topologii umożliwia hello systemu toorevise hello równoległość topologii hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="6d3bd-188">Na przykład jeśli ma zmieniony tooadd klastra hello dodatkowych notatek, ponowne równoważenie umożliwia topologii toosee hello nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="6d3bd-189">Ponowne równoważenie topologii najpierw dezaktywuje topologii hello ponownie dystrybuuje pracowników równomiernie między hello klastra, a następnie finally zwraca hello topologii toohello stanu sprzed ponowne równoważenie wystąpił.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="6d3bd-190">Tak topologii hello był aktywny, staje się aktywny ponownie.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="6d3bd-191">Jeśli została ona zdezaktywowana, pozostaje dezaktywowane.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="6d3bd-192">Monitorowanie i zarządzanie nimi: Storm interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6d3bd-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="6d3bd-193">Hello interfejsu użytkownika platformy Storm udostępnia interfejs sieci web do pracy z uruchomionymi topologiami i znajduje się w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="6d3bd-194">Witaj tooview interfejsu użytkownika platformy Storm, użyj tooopen przeglądarki sieci web **https://CLUSTERNAME.azurehdinsight.net/stormui**, gdzie **CLUSTERNAME** jest hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6d3bd-195">Jeśli pojawi się monit tooprovide nazwy użytkownika i hasła, wprowadź hello administratora klastra (admin) i hasło użyte podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="6d3bd-196">Strona główna</span><span class="sxs-lookup"><span data-stu-id="6d3bd-196">Main page</span></span>

<span data-ttu-id="6d3bd-197">strony główne Hello hello interfejsu użytkownika platformy Storm udostępnia hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="6d3bd-198">**Podsumowanie klastra**: podstawowe informacje o hello klaster Storm.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="6d3bd-199">**Topologia podsumowania**: Lista uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="6d3bd-200">Użyj hello łącza w tej sekcji tooview więcej informacji o określonych topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="6d3bd-201">**Podsumowanie przełożonego**: informacje o przełożonego Storm hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="6d3bd-202">**Konfiguracja nimbus**: Konfiguracja Nimbus hello klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="6d3bd-203">Topologia podsumowania</span><span class="sxs-lookup"><span data-stu-id="6d3bd-203">Topology summary</span></span>

<span data-ttu-id="6d3bd-204">Wybieranie łącza z hello **podsumowanie topologii** sekcja wyświetla następujące informacje o topologii hello hello:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="6d3bd-205">**Topologia podsumowania**: podstawowe informacje o topologii hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="6d3bd-206">**Akcje topologii**: Akcje zarządzania, które można wykonywać w odniesieniu do topologii hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="6d3bd-207">**Aktywuj**: wznowienie przetwarzania dezaktywowanej topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="6d3bd-208">**Dezaktywuj**: wstrzymanie uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="6d3bd-209">**Rebalance**: można dostosować równoległość hello hello topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="6d3bd-210">Po zmianie hello liczby węzłów w klastrze hello, należy przeprowadzić ponowne równoważenie uruchomionych topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="6d3bd-211">Ta operacja pozwala hello topologii tooadjust równoległości toocompensate dla hello zwiększyć lub zmniejszyć liczbę węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="6d3bd-212">Aby uzyskać więcej informacji, zobacz <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">opis hello równoległości topologii Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="6d3bd-213">**Kasowanie**: kończy topologii Storm po hello określony limit czasu.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="6d3bd-214">**Statystyka topologii**: Statystyka topologii hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="6d3bd-215">tooset hello uzyskać hello pozostałe wpisy na stronie powitania, użyj łącza hello w hello **okna** kolumny.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="6d3bd-216">**Spouts**: hello elementach spout używane przez hello topologii.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="6d3bd-217">Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementach spout.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="6d3bd-218">**Bolts**: hello używane przez hello topologii elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="6d3bd-219">Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="6d3bd-220">**Topologia konfiguracji**: hello konfiguracji topologii hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="6d3bd-221">Spout i Bolt — podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6d3bd-221">Spout and Bolt summary</span></span>

<span data-ttu-id="6d3bd-222">Wybieranie spout z hello **Spouts** lub **Bolts** sekcje Wyświetla hello następujących informacji o elemencie hello wybrane:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="6d3bd-223">**Składnik podsumowania**: podstawowe informacje o hello spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="6d3bd-224">**Spout/Bolt stats**: Statystyka hello spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="6d3bd-225">tooset hello uzyskać hello pozostałe wpisy na stronie powitania, użyj łącza hello w hello **okna** kolumny.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="6d3bd-226">**Wprowadź statystykę** (tylko dla elementów bolt): informacje o hello strumienie używane przez hello bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="6d3bd-227">**OUTPUT stats**: informacje o strumieni hello emitowane przez to spout ani dla elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="6d3bd-228">**Modułów**: informacje na temat wystąpień hello hello spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="6d3bd-229">Wybierz hello **portu** wpis dla tooview określonego modułu wykonującego dziennika informacji diagnostycznych utworzone dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="6d3bd-230">**Błędy**: informacje o błędzie dla tego spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="6d3bd-231">Monitorowanie i zarządzanie nimi: interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="6d3bd-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="6d3bd-232">Hello interfejsu użytkownika platformy Storm jest oparty na powitania interfejsu API REST, więc można wykonać podobne do zarządzania i monitorowania funkcji przy użyciu hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="6d3bd-233">Można użyć interfejsu API REST hello toocreate niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="6d3bd-234">Aby uzyskać więcej informacji, zobacz [interfejsu API REST interfejsu użytkownika Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="6d3bd-235">Witaj następujące informacje są hello toousing określonego interfejsu API REST z systemu Apache Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d3bd-236">Witaj interfejsu API REST Storm nie jest publicznie dostępna przez hello internet i muszą być dostępne za pomocą protokołu SSH tunelu toohello HDInsight węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="6d3bd-237">Aby uzyskać informacje na temat tworzenia i używania tunelu SSH, zobacz [Użyj SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie i innych sieci web UI](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="6d3bd-238">Podstawowy identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="6d3bd-238">Base URI</span></span>

<span data-ttu-id="6d3bd-239">Witaj podstawowy identyfikator URI dla hello interfejsu API REST w klastrach HDInsight opartych na systemie Linux jest dostępna na powitania węzła głównego w **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="6d3bd-240">Nazwa domeny Hello węzła głównego hello jest generowany podczas tworzenia klastra i nie jest statyczne.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="6d3bd-241">Hello pełną nazwę domeny (FQDN) dla węzła głównego klastra hello znajduje się na kilka różnych sposobów:</span><span class="sxs-lookup"><span data-stu-id="6d3bd-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="6d3bd-242">**W sesji SSH**: Użyj polecenia hello `headnode -f` z klastra toohello sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="6d3bd-243">**Z sieci Ambari Web**: Wybierz **usług** od góry hello hello strony, następnie wybierz **Storm**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="6d3bd-244">Z hello **Podsumowanie** wybierz opcję **serwera interfejsu użytkownika Storm**.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="6d3bd-245">Witaj FQDN węzła hello, który działa hello interfejsu użytkownika platformy Storm i interfejsu API REST jest u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="6d3bd-246">**Z interfejsu API REST Ambari**: Użyj polecenia hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve informacji na temat hello węzła, który hello interfejsu użytkownika platformy Storm i interfejsu API REST są uruchomione na.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="6d3bd-247">Zastąp **hasło** o hasło administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="6d3bd-248">Zastąp **CLUSTERNAME** hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="6d3bd-249">W odpowiedzi hello wpis "host_name" hello zawiera hello FQDN węzła hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="6d3bd-250">Authentication</span><span class="sxs-lookup"><span data-stu-id="6d3bd-250">Authentication</span></span>

<span data-ttu-id="6d3bd-251">Toohello żądania interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, więc użyć hello HDInsight klastra nazwę i hasło administratora.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="6d3bd-252">Ponieważ uwierzytelnianie podstawowe jest wysyłany przy użyciu zwykłego tekstu, należy **zawsze** połączeń toosecure HTTPS za pomocą hello klastra.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="6d3bd-253">Wartości zwracane</span><span class="sxs-lookup"><span data-stu-id="6d3bd-253">Return values</span></span>

<span data-ttu-id="6d3bd-254">Informacje zwrócone z hello interfejsu API REST mogą być tylko można używać z wewnątrz klastra hello lub maszyn wirtualnych na hello tej samej sieci wirtualnej platformy Azure jako klaster hello.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="6d3bd-255">Na przykład nie jest dostępny z Internetu hello hello pełną nazwę domeny (FQDN) dla serwerów dozorcy zwracane.</span><span class="sxs-lookup"><span data-stu-id="6d3bd-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d3bd-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d3bd-256">Next Steps</span></span>

<span data-ttu-id="6d3bd-257">Teraz, kiedy znasz już jak topologie toodeploy i monitorować za pomocą hello pulpit nawigacyjny Storm, Dowiedz się, jak za[topologie oparte na opracowanie Java za pomocą programu Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="6d3bd-258">Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6d3bd-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
