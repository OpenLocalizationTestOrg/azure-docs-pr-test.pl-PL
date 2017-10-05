---
title: Zainstaluj Presto w klastrach Azure HDInsight Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zainstalować Presto i Airpal w klastrach opartych na systemie Linux usługi HDInsight Hadoop za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="df3db-103">Zainstalować i używać Presto w klastrach HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="df3db-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="df3db-104">W tym temacie możesz dowiedzieć się, jak instalować Presto w klastrach HDInsight Hadoop za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="df3db-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="df3db-105">Możesz również informacje o instalowaniu Airpal w istniejącym klastrze Presto usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df3db-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df3db-106">Kroki w tym dokumencie wymagają **klastra usługi HDInsight Hadoop 3.5** używającą systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="df3db-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="df3db-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="df3db-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="df3db-108">Aby uzyskać więcej informacji, zobacz [wersji usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="df3db-109">Co to jest Presto?</span><span class="sxs-lookup"><span data-stu-id="df3db-109">What is Presto?</span></span>
<span data-ttu-id="df3db-110">[Presto](https://prestodb.io/overview.html) jest szybkie rozproszonej aparatu zapytań SQL dla danych big data.</span><span class="sxs-lookup"><span data-stu-id="df3db-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="df3db-111">Presto nadaje się do interaktywnego kwerend do poziomu petabajtów danych.</span><span class="sxs-lookup"><span data-stu-id="df3db-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="df3db-112">Aby uzyskać więcej informacji na składniki Presto i ich współpracę, zobacz [Presto pojęcia](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="df3db-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="df3db-113">Składniki dostarczony z klastrem usługi HDInsight są w pełni obsługiwane, a Microsoft Support pomoże w celu odizolowania i rozwiązać problemy związane z tych składników.</span><span class="sxs-lookup"><span data-stu-id="df3db-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="df3db-114">Niestandardowe składniki, takie jak Presto, otrzymywanie pomocy uzasadnione ekonomicznie ułatwiające aby dalej rozwiązywać ten problem.</span><span class="sxs-lookup"><span data-stu-id="df3db-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="df3db-115">Może to spowodować w rozwiązaniu problemu lub monitem o Uwzględnij dostępnych kanałów dla technologiach typu open source wykryto głębokie doświadczenia z tej technologii.</span><span class="sxs-lookup"><span data-stu-id="df3db-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="df3db-116">Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="df3db-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="df3db-117">Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="df3db-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="df3db-118">Zainstaluj Presto za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="df3db-118">Install Presto using script action</span></span>

<span data-ttu-id="df3db-119">Ta sekcja zawiera instrukcje dotyczące sposobu używania przykładowy skrypt, podczas tworzenia nowego klastra za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="df3db-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="df3db-120">Uruchom inicjowania obsługi klastra, wykonując kroki opisane w [klastrów usługi HDInsight opartych na systemie Linux należy](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="df3db-121">Upewnij się, że tworzenia klastra przy użyciu **niestandardowy** przepływu tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="df3db-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="df3db-122">Należy się upewnić, że klastra, którą utworzysz spełnia następujące wymagania.</span><span class="sxs-lookup"><span data-stu-id="df3db-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="df3db-123">a.</span><span class="sxs-lookup"><span data-stu-id="df3db-123">a.</span></span> <span data-ttu-id="df3db-124">Musi to być klastra usługi Hadoop z usługą HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="df3db-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="df3db-125">b.</span><span class="sxs-lookup"><span data-stu-id="df3db-125">b.</span></span> <span data-ttu-id="df3db-126">Należy użyć magazynu Azure do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="df3db-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="df3db-127">Używanie Presto w klastrze, który używa usługi Azure Data Lake Store jako opcji magazynu nie jest jeszcze obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="df3db-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![Tworzenie klastra usługi HDInsight przy użyciu niestandardowych opcji](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="df3db-129">Na **Zaawansowane ustawienia** bloku, wybierz opcję **akcji skryptu**i podaj poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="df3db-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="df3db-130">**Nazwa**: Wprowadź przyjazną nazwę dla akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="df3db-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="df3db-131">**Identyfikator URI skryptu powłoki systemowej**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="df3db-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="df3db-132">**HEAD**: Zaznaczenie tego pola wyboru</span><span class="sxs-lookup"><span data-stu-id="df3db-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="df3db-133">**Proces ROBOCZY**: Zaznaczenie tego pola wyboru</span><span class="sxs-lookup"><span data-stu-id="df3db-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="df3db-134">**DOZORCY**: wyczyść to pole wyboru</span><span class="sxs-lookup"><span data-stu-id="df3db-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="df3db-135">**Parametry**: pozostaw to pole puste</span><span class="sxs-lookup"><span data-stu-id="df3db-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="df3db-136">W dolnej części **akcji skryptu** bloku, kliknij przycisk **wybierz** przycisk, aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="df3db-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="df3db-137">Na koniec kliknij **wybierz** przycisk w dolnej części **Zaawansowane ustawienia** bloku, aby zapisać informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="df3db-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="df3db-138">Kontynuuj, inicjowania obsługi klastra, zgodnie z opisem w [klastrów usługi HDInsight opartych na systemie Linux należy](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="df3db-139">Program Azure PowerShell, interfejsu wiersza polecenia Azure, zestawu .NET SDK usługi HDInsight lub szablonów usługi Azure Resource Manager można również zastosować akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="df3db-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="df3db-140">Akcje skryptu można również dotyczą już działające klastry.</span><span class="sxs-lookup"><span data-stu-id="df3db-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="df3db-141">Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="df3db-142">Korzystanie z usługą HDInsight Presto</span><span class="sxs-lookup"><span data-stu-id="df3db-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="df3db-143">Wykonaj poniższe kroki, aby użyć Presto w klastrze HDInsight po zainstalowaniu go za pomocą kroków opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="df3db-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="df3db-144">Nawiąż połączenie z klastrem usługi HDInsight przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="df3db-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="df3db-145">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="df3db-146">Uruchom powłokę Presto przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="df3db-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="df3db-147">Uruchom zapytania w tabeli próbki **hivesampletable**, który jest dostępny na wszystkich klastrach HDInsight domyślnie.</span><span class="sxs-lookup"><span data-stu-id="df3db-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="df3db-148">Domyślnie [Hive](https://prestodb.io/docs/current/connector/hive.html) i [TPCH](https://prestodb.io/docs/current/connector/tpch.html) łączników dla Presto są już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="df3db-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="df3db-149">Gałąź łącznik jest skonfigurowany do używania domyślnie zainstalowaną instalacji Hive, dlatego wszystkie tabele z gałęzi będzie automatycznie wyświetlane w Presto.</span><span class="sxs-lookup"><span data-stu-id="df3db-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="df3db-150">Aby uzyskać szczegółowy opis używania Presto, zobacz [Presto dokumentacji](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="df3db-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="df3db-151">Airpal za pomocą Presto</span><span class="sxs-lookup"><span data-stu-id="df3db-151">Use Airpal with Presto</span></span>

<span data-ttu-id="df3db-152">[Airpal](https://github.com/airbnb/airpal#airpal) jest interfejsem open source opartych na sieci web zapytania dla Presto.</span><span class="sxs-lookup"><span data-stu-id="df3db-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="df3db-153">Aby uzyskać więcej informacji o Airpal, zobacz [dokumentacji Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="df3db-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="df3db-154">W tej sekcji opisano kroki, aby **zainstalować Airpal na edgenode** klastra usługi HDInsight Hadoop Presto już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="df3db-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="df3db-155">Dzięki temu, że Airpal zapytania interfejs jest dostępny za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="df3db-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="df3db-156">Przy użyciu protokołu SSH, podłącz do headnode Presto zainstalowanym klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="df3db-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="df3db-157">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="df3db-158">Po nawiązaniu połączenia, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="df3db-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="df3db-159">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="df3db-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="df3db-160">Z danych wyjściowych, zwróć uwagę na wartość dla **wartość** właściwości.</span><span class="sxs-lookup"><span data-stu-id="df3db-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="df3db-161">Będzie on potrzebny podczas instalowania Airpal na edgenode klastra.</span><span class="sxs-lookup"><span data-stu-id="df3db-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="df3db-162">W powyższych danych wyjściowych, wartość, która będzie potrzebny jest **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="df3db-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="df3db-163">Szablon  **[tutaj](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  do tworzenia edgenode klastra usługi HDInsight i podaj wartości, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="df3db-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![HDInsight instalacji Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="df3db-165">Kliknij pozycję **Kup**.</span><span class="sxs-lookup"><span data-stu-id="df3db-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="df3db-166">Po zmiany zostaną zastosowane do konfiguracji klastra, uzyskać dostęp do interfejsu sieci web Airpal, wykonując następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="df3db-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="df3db-167">a.</span><span class="sxs-lookup"><span data-stu-id="df3db-167">a.</span></span> <span data-ttu-id="df3db-168">W bloku klastra, kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="df3db-168">From the cluster blade, click **Applications**.</span></span>

    ![Uruchamianie usługi HDInsight Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="df3db-170">b.</span><span class="sxs-lookup"><span data-stu-id="df3db-170">b.</span></span> <span data-ttu-id="df3db-171">Z **zainstalowane aplikacje** bloku, kliknij przycisk **Portal** przed airpal.</span><span class="sxs-lookup"><span data-stu-id="df3db-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Uruchamianie usługi HDInsight Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="df3db-173">c.</span><span class="sxs-lookup"><span data-stu-id="df3db-173">c.</span></span> <span data-ttu-id="df3db-174">Po wyświetleniu monitu wprowadź poświadczenia administratora, które można określić podczas tworzenia klastra usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="df3db-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="df3db-175">Dostosowanie Presto instalacji w klastrze usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="df3db-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="df3db-176">Po zainstalowaniu Presto na klaster usługi HDInsight Hadoop, można dostosować instalacji, aby wprowadzić zmiany, takie jak zaktualizować ustawienia pamięci, zmienianie łączników, itp. W tym celu wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="df3db-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="df3db-177">Przy użyciu protokołu SSH, podłącz do headnode Presto zainstalowanym klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="df3db-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="df3db-178">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="df3db-179">Wprowadź zmiany w konfiguracji w pliku `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="df3db-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="df3db-180">Aby uzyskać więcej informacji na Presto konfiguracji, zobacz [Presto konfiguracji dla klastrów YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="df3db-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="df3db-181">Zatrzymaj i Zakończ bieżący uruchomione wystąpienie Presto.</span><span class="sxs-lookup"><span data-stu-id="df3db-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="df3db-182">Uruchom nowe wystąpienie klasy Presto do dostosowywania.</span><span class="sxs-lookup"><span data-stu-id="df3db-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="df3db-183">Poczekaj, aż gotowość i zanotuj adres presto koordynatora nowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="df3db-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="df3db-184">Generowanie wyników testów dla klastrów usługi HDInsight, które są uruchamiane Presto</span><span class="sxs-lookup"><span data-stu-id="df3db-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="df3db-185">TPC DS to branżowy standard do pomiaru wydajności wiele systemów wsparcia decyzji, w tym systemy danych big data.</span><span class="sxs-lookup"><span data-stu-id="df3db-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="df3db-186">Umożliwia Presto w klastrach HDInsight generowania danych i ocenić, jak są porównywane z własnych danych testowych HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df3db-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="df3db-187">Aby uzyskać więcej informacji, zobacz [tutaj](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="df3db-188">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="df3db-188">See also</span></span>
* <span data-ttu-id="df3db-189">[Zainstalować i używać Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="df3db-190">HUE jest interfejs użytkownika, który ułatwia tworzenie, uruchamianie i Zapisz zadań Pig i Hive, a także przeglądania magazynu domyślnego dla Twojej usługi HDInsight klastra w sieci web.</span><span class="sxs-lookup"><span data-stu-id="df3db-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="df3db-191">[Zainstaluj Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="df3db-192">Dostosowywanie klastra należy zainstalować Giraph w klastrach HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="df3db-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="df3db-193">Giraph umożliwia wykonywanie wykresu przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df3db-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="df3db-194">[Zainstaluj Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="df3db-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="df3db-195">Dostosowywanie klastra należy zainstalować Solr w klastrach HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="df3db-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="df3db-196">Solr umożliwia wykonywanie operacji wyszukiwania zaawansowanego w przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="df3db-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
