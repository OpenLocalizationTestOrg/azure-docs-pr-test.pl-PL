---
title: "aaaAzure Toolkit for IntelliJ — aplikacje debugowania zdalnego na Spark w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą narzędzi HDInsight w zestawie narzędzi Azure dla aplikacji debugowania tooremotely IntelliJ uruchamianych w klastrach HDInsight Spark za pośrednictwem sieci vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="0e299-103">Użyj zestawu narzędzi platformy Azure dla aplikacji toodebug IntelliJ zdalnie w HDInsight Spark za pośrednictwem sieci VPN</span><span class="sxs-lookup"><span data-stu-id="0e299-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="0e299-104">Firma Microsoft zaleca sposób hello debugowania applicaltion spark zdalnie za pomocą ssh.</span><span class="sxs-lookup"><span data-stu-id="0e299-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="0e299-105">Aby uzyskać instrukcje, zobacz [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="0e299-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="0e299-106">Ten artykuł zawiera wskazówki krok po kroku, jak toouse hello narzędzi HDInsight Tools w zestawie narzędzi Azure dla toosubmit IntelliJ zadania Spark w klastrze Spark w usłudze HDInsight i następnie Debuguj go zdalnie z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="0e299-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="0e299-107">toodo tak, należy wykonać następujące kroki wysokiego poziomu hello:</span><span class="sxs-lookup"><span data-stu-id="0e299-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="0e299-108">Tworzenie sieci wirtualnej platformy Azure do lokacji lub punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="0e299-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="0e299-109">kroki Hello w tym dokumencie Załóżmy, że sieć lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="0e299-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="0e299-110">Tworzenie klastra Spark w usłudze Azure HDInsight, który jest częścią hello lokacja lokacja sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e299-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="0e299-111">Sprawdź łączność hello między hello headnode klastra i pulpitu.</span><span class="sxs-lookup"><span data-stu-id="0e299-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="0e299-112">Tworzenie aplikacji Scala w IntelliJ IDEA i skonfigurować go na potrzeby debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="0e299-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="0e299-113">Uruchom i debugowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e299-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0e299-114">Prerequisites</span></span>
* <span data-ttu-id="0e299-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e299-115">An Azure subscription.</span></span> <span data-ttu-id="0e299-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0e299-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0e299-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0e299-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0e299-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0e299-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="0e299-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="0e299-119">Oracle Java Development kit.</span></span> <span data-ttu-id="0e299-120">Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="0e299-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="0e299-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="0e299-121">IntelliJ IDEA.</span></span> <span data-ttu-id="0e299-122">W tym artykule używa wersji 2017.1.</span><span class="sxs-lookup"><span data-stu-id="0e299-122">This article uses version 2017.1.</span></span> <span data-ttu-id="0e299-123">Możesz zainstalować ją z [tutaj](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="0e299-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="0e299-124">Narzędzia HDInsight Tools w Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0e299-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0e299-125">Narzędzia HDInsight tools for IntelliJ są dostępne jako część hello Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0e299-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0e299-126">Aby uzyskać instrukcje dotyczące sposobu tooinstall hello Azure zestawu narzędzi, zobacz [hello Instalowanie narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="0e299-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="0e299-127">Zaloguj się do Twojej subskrypcji platformy Azure z rozwiązaniem IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="0e299-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="0e299-128">Postępuj zgodnie z instrukcjami hello [tutaj](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="0e299-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="0e299-129">Podczas uruchamiania aplikacji Spark Scala do zdalnego debugowania na komputerze z systemem Windows, może spowodować wyjątek, zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) występuje powodu Brak tooa WinUtils.exe w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="0e299-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="0e299-130">toowork uniknąć tego błędu, należy najpierw [Pobierz hello pliku wykonywalnego w tym miejscu](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa lokalizacji, takich jak **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="0e299-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="0e299-131">Następnie należy dodać zmienną środowiskową **HADOOP_HOME** i ustaw wartość hello zmiennej hello zbyt**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="0e299-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="0e299-132">Krok 1: Tworzenie sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e299-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="0e299-133">Wykonaj instrukcje hello z hello poniżej toocreate łącza sieci wirtualnej platformy Azure, a następnie sprawdź łączność hello hello pulpitu i sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e299-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="0e299-134">Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0e299-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="0e299-135">Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e299-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="0e299-136">Skonfiguruj połączenie punkt lokacja tooa sieć wirtualną przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e299-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="0e299-137">Krok 2: Tworzenie klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="0e299-138">Należy również utworzyć klaster Apache Spark w usłudze Azure HDInsight jest częścią hello Azure Virtual Network, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="0e299-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="0e299-139">Użyj hello informacji dostępnych w [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0e299-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="0e299-140">W ramach konfiguracji opcjonalnej wybierz hello Azure Virtual Network, utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="0e299-141">Krok 3: Sprawdź łączność hello między hello headnode klastra i pulpitu</span><span class="sxs-lookup"><span data-stu-id="0e299-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="0e299-142">Pobierz adres IP hello hello headnode.</span><span class="sxs-lookup"><span data-stu-id="0e299-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="0e299-143">Otwórz interfejs użytkownika narzędzia Ambari hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0e299-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="0e299-144">W bloku klastra powitania kliknij **pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="0e299-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="0e299-146">Hello interfejsu użytkownika narzędzia Ambari, z hello prawym górnym rogu kliknij **hostów**.</span><span class="sxs-lookup"><span data-stu-id="0e299-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="0e299-148">Należy wyświetlić listę headnodes węzłów procesu roboczego i węzły dozorcy.</span><span class="sxs-lookup"><span data-stu-id="0e299-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="0e299-149">Witaj headnodes ma hello **hn*** prefiks.</span><span class="sxs-lookup"><span data-stu-id="0e299-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="0e299-150">Kliknij pierwszy headnode hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-150">Click hello first headnode.</span></span>

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="0e299-152">U dołu strony hello, który zostanie otwarty z hello hello **Podsumowanie** polu adres IP hello kopiowania hello headnode i hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="0e299-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="0e299-154">Obejmują hello adresu IP i nazwy hosta hello hello headnode toohello **hostów** pliku na komputerze hello, z którym chcesz toorun i zdalne debugowanie zadań Spark hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="0e299-155">Pozwoli to toocommunicate z headnode hello przy użyciu hello adresu IP, a także hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="0e299-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="0e299-156">Otwórz program Notatnik z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="0e299-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="0e299-157">W menu Plik powitania kliknij **Otwórz** , a następnie przejdź toohello lokalizację pliku hosts hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="0e299-158">Na komputerze z systemem Windows jest `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="0e299-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="0e299-159">Dodaj następujące toohello hello **hostów** pliku.</span><span class="sxs-lookup"><span data-stu-id="0e299-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="0e299-160">Z komputera hello, który połączony toohello sieci wirtualnej platformy Azure, używanego przez klaster usługi HDInsight hello Sprawdź, czy można wykonać polecenie ping zarówno headnodes hello przy użyciu hello adresu IP, a także hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="0e299-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="0e299-161">SSH do hello headnode klastra przy użyciu instrukcji hello na [klastra usługi HDInsight tooan Połącz przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0e299-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="0e299-162">Z headnode klastra hello Zbadaj hello adres IP komputera stacjonarnego hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="0e299-163">Należy przetestować połączenie tooboth hello adresy IP przypisane toohello komputer, dla połączenia sieciowego hello i hello innych dla hello sieci wirtualnej platformy Azure, która hello komputer jest połączony.</span><span class="sxs-lookup"><span data-stu-id="0e299-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="0e299-164">Powtórz kroki od hello na powitania również inne headnode.</span><span class="sxs-lookup"><span data-stu-id="0e299-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="0e299-165">Krok 4: Tworzenie aplikacji Spark Scala przy użyciu narzędzi HDInsight hello w zestawie narzędzi Azure for IntelliJ i skonfiguruj ją do zdalnego debugowania</span><span class="sxs-lookup"><span data-stu-id="0e299-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="0e299-166">Uruchom IntelliJ IDEA i Utwórz nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="0e299-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="0e299-167">W powitalne okno dialogowe Nowy projekt, wprowadź hello następujące opcje, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0e299-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Tworzenie aplikacji Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="0e299-169">W okienku po lewej stronie powitania, wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0e299-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="0e299-170">W okienku po prawej stronie powitania, wybierz **Spark w usłudze HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="0e299-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="0e299-171">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="0e299-171">Click **Next**.</span></span>
2. <span data-ttu-id="0e299-172">W następnym oknie hello, podaj poniższe informacje projektu hello, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="0e299-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="0e299-173">Podaj nazwę projektu i lokalizacja projektu.</span><span class="sxs-lookup"><span data-stu-id="0e299-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="0e299-174">Dla **SDK projektu**, użyj języka Java 1.8 Java 1.7 spark 1.x klastra spark 2.x klastra.</span><span class="sxs-lookup"><span data-stu-id="0e299-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="0e299-175">Aby uzyskać **wersji Spark**, Kreator tworzenia projektu Scala integruje poprawnej wersji dla platformy Spark zestawy SDK i Scala.</span><span class="sxs-lookup"><span data-stu-id="0e299-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="0e299-176">Jeśli hello klastra spark w wersji 2.0 niższe, wybierz spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="0e299-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="0e299-177">W przeciwnym razie należy wybrać spark2.x.</span><span class="sxs-lookup"><span data-stu-id="0e299-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="0e299-178">W tym przykładzie użyto Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="0e299-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="0e299-179">![Tworzenie aplikacji Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="0e299-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="0e299-180">Projekt Spark Hello automatycznie utworzy artefaktu.</span><span class="sxs-lookup"><span data-stu-id="0e299-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="0e299-181">toosee hello artefaktu, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="0e299-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="0e299-182">Z hello **pliku** menu, kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="0e299-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="0e299-183">W hello **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** toosee hello domyślne artefaktu, który jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="0e299-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="0e299-184">![Utwórz JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="0e299-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="0e299-185">Można również tworzyć własne artefaktu bly kliknięcie hello  **+**  ikona wyróżnione powyższy obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="0e299-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="0e299-186">Dodaj projekt tooyour biblioteki.</span><span class="sxs-lookup"><span data-stu-id="0e299-186">Add libraries tooyour project.</span></span> <span data-ttu-id="0e299-187">tooadd biblioteki, kliknij prawym przyciskiem myszy nazwę projektu hello w drzewie projektu hello, a następnie kliknij przycisk **Otwórz ustawienia modułu**.</span><span class="sxs-lookup"><span data-stu-id="0e299-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="0e299-188">W hello **struktury projektu** okno dialogowe, w okienku po lewej stronie powitania kliknij **biblioteki**, kliknij symbol hello (+), a następnie kliknij przycisk **z Maven**.</span><span class="sxs-lookup"><span data-stu-id="0e299-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Dodaj bibliotekę](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="0e299-190">W hello **pobrania biblioteki z repozytorium Maven** okna dialogowego, wyszukiwanie i dodać hello następujące biblioteki.</span><span class="sxs-lookup"><span data-stu-id="0e299-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="0e299-191">Kopiuj `yarn-site.xml` i `core-site.xml` z hello headnode klastra, a następnie dodaj go toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="0e299-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="0e299-192">Użyj hello następujące pliki hello toocopy poleceń.</span><span class="sxs-lookup"><span data-stu-id="0e299-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="0e299-193">Można użyć [programów Cygwin](https://cygwin.com/install.html) toorun hello następujące `scp` polecenia toocopy hello plików z hello headnodes klastra.</span><span class="sxs-lookup"><span data-stu-id="0e299-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="0e299-194">Ponieważ dodano już hello klastra headnode IP adres i nazwy hostów fo hello pliku hosts na pulpicie hello, możemy użyć hello **scp** poleceń w powitania po sposób.</span><span class="sxs-lookup"><span data-stu-id="0e299-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="0e299-195">Dodaj projekt tooyour te pliki, kopiując je w obszarze hello **/src** folderu w drzewie z projektu, na przykład `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="0e299-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="0e299-196">Aktualizacja hello `core-site.xml` hello toomake następujące zmiany.</span><span class="sxs-lookup"><span data-stu-id="0e299-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="0e299-197">`core-site.xml`zawiera konta magazynu kluczy toohello hello szyfrowane skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="0e299-198">W hello `core-site.xml` dodania toohello projektu, Zastąp hello zaszyfrowanego klucza z kluczem przechowywania hello skojarzone z hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="0e299-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="0e299-199">Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0e299-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="0e299-200">Usuń następujące wpisy z hello hello `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="0e299-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="0e299-201">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-201">Save hello file.</span></span>
7. <span data-ttu-id="0e299-202">Dodawanie klasy głównym hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e299-202">Add hello Main class for your application.</span></span> <span data-ttu-id="0e299-203">Z hello **Eksplorator projektów**, kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie kliknij przycisk **klasy Scala**.</span><span class="sxs-lookup"><span data-stu-id="0e299-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Dodaj kod źródłowy](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="0e299-205">W hello **Utwórz nową klasę Scala** okna dialogowego podaj nazwę, dla **rodzaj** wybierz **obiektu**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e299-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Dodaj kod źródłowy](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="0e299-207">W hello `MyClusterAppMain.scala` plików, Wklej hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="0e299-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="0e299-208">Ten kod tworzy hello Spark kontekstu i uruchamia `executeJob` metody z hello `SparkSample` obiektu.</span><span class="sxs-lookup"><span data-stu-id="0e299-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="0e299-209">Powtórz kroki od 8 do 9 powyżej tooadd nowy obiekt Scala o nazwie `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="0e299-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="0e299-210">Klasa toothis Dodaj hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="0e299-210">toothis class add hello following code.</span></span> <span data-ttu-id="0e299-211">Ten kod odczytuje dane hello z hello HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera hello wiersze z tylko jedną cyfrę w kolumnie siódmego hello hello CSV i zapisuje dane wyjściowe hello zbyt**/HVACOut** w obszarze hello domyślne kontener magazynu hello klaster.</span><span class="sxs-lookup"><span data-stu-id="0e299-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="0e299-212">Powtórz kroki od 8 do 9 powyżej tooadd nową klasę o nazwie `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="0e299-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="0e299-213">Ta klasa implementuje hello struktury testowej Spark, która jest używana do debugowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e299-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="0e299-214">Dodaj hello następującego kodu toohello `RemoteClusterDebugging` klasy.</span><span class="sxs-lookup"><span data-stu-id="0e299-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="0e299-215">Kilka ważnych rzeczy toonote tutaj:</span><span class="sxs-lookup"><span data-stu-id="0e299-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="0e299-216">Aby uzyskać `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, upewnij się, że hello zestawu Spark JAR jest dostępna w magazynie klastra hello w określonej ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="0e299-217">Aby uzyskać `setJars`, określ lokalizację hello, w której zostanie utworzona jar artefaktu hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="0e299-218">Zazwyczaj jest `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="0e299-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="0e299-219">W hello `RemoteClusterDebugging` klasy, kliknij prawym przyciskiem myszy hello `test` — słowo kluczowe i wybierz **Tworzenie konfiguracji RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="0e299-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Tworzenie konfiguracji zdalnej](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="0e299-221">Okno dialogowe hello, podaj nazwę dla konfiguracji hello, a następnie wybierz hello **Test rodzaj** jako **nazwa testu**.</span><span class="sxs-lookup"><span data-stu-id="0e299-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="0e299-222">Pozostaw pozostałe wartości domyślne, kliknij przycisk **Zastosuj**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e299-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Tworzenie konfiguracji zdalnej](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="0e299-224">Powinien zostać wyświetlony **zdalnego uruchom** konfiguracji listy rozwijanej na pasku menu hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Tworzenie konfiguracji zdalnej](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="0e299-226">Krok 5: Uruchamianie aplikacji hello w trybie debugowania</span><span class="sxs-lookup"><span data-stu-id="0e299-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="0e299-227">Otwórz w projekcie IntelliJ IDEA `SparkSample.scala` i Utwórz rdd1 too'val z następnego punktu przerwania ".</span><span class="sxs-lookup"><span data-stu-id="0e299-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="0e299-228">W menu podręczne hello tworzenia punkt przerwania, wybierz **wiersz w funkcji executeJob**.</span><span class="sxs-lookup"><span data-stu-id="0e299-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Dodawanie punktu przerwania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="0e299-230">Kliknij hello **debugowania Uruchom** przycisku Dalej toohello **zdalnego uruchom** uruchomiona aplikacja hello toostart listy rozwijanej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0e299-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="0e299-232">Podczas wykonywania programu hello osiągnie punkt przerwania hello, powinny być widoczne **debugera** w hello dolnym okienku.</span><span class="sxs-lookup"><span data-stu-id="0e299-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="0e299-234">Kliknij przycisk hello (**+**) tooadd ikona czujki, jak pokazano w poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="0e299-236">Tutaj, ponieważ aplikacja hello spowodowało przerwanie przed zmiennej hello `rdd1` został utworzony przy użyciu tego czujki możemy stwierdzić, jakie są hello 5 pierwszych wierszy w zmiennej hello `rdd`.</span><span class="sxs-lookup"><span data-stu-id="0e299-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="0e299-237">Naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="0e299-237">Press **ENTER**.</span></span>

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="0e299-239">Zobacz w powyższy obraz powitania jest, że w czasie wykonywania, można zbadać terrabytes danych i debugowania sposób realizowany Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e299-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="0e299-240">Na przykład w danych wyjściowych hello pokazano powyższy obraz powitania widać tego hello pierwszy wiersz danych wyjściowych hello jest nagłówkiem.</span><span class="sxs-lookup"><span data-stu-id="0e299-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="0e299-241">Na podstawie tych, można zmodyfikować wiersz kodu nagłówka hello tooskip Twojej aplikacji w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0e299-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="0e299-242">Możesz teraz kliknąć hello **Program Wznów** tooproceed ikonę z aplikacją, uruchom.</span><span class="sxs-lookup"><span data-stu-id="0e299-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="0e299-244">Jeśli aplikacja hello zakończy się pomyślnie, powinny pojawić się dane wyjściowe podobne do następujących hello.</span><span class="sxs-lookup"><span data-stu-id="0e299-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="0e299-246"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0e299-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0e299-247">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="0e299-248">Demonstracja</span><span class="sxs-lookup"><span data-stu-id="0e299-248">Demo</span></span>
* <span data-ttu-id="0e299-249">Utwórz projekt Scala (klip wideo): [tworzenie aplikacji Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0e299-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="0e299-250">Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0e299-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="0e299-251">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="0e299-251">Scenarios</span></span>
* [<span data-ttu-id="0e299-252">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="0e299-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0e299-253">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="0e299-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0e299-254">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0e299-255">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="0e299-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0e299-256">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0e299-257">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0e299-257">Create and run applications</span></span>
* [<span data-ttu-id="0e299-258">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="0e299-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0e299-259">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="0e299-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0e299-260">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="0e299-260">Tools and extensions</span></span>
* [<span data-ttu-id="0e299-261">Użycie narzędzi HDInsight w zestawie narzędzi Azure IntelliJ toocreate i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="0e299-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0e299-262">Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem SSH</span><span class="sxs-lookup"><span data-stu-id="0e299-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="0e299-263">Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="0e299-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="0e299-264">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji</span><span class="sxs-lookup"><span data-stu-id="0e299-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="0e299-265">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0e299-266">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0e299-267">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="0e299-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0e299-268">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0e299-269">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="0e299-269">Manage resources</span></span>
* [<span data-ttu-id="0e299-270">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0e299-271">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e299-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
