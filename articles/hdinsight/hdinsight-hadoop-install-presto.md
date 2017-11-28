---
title: "aaaInstall Presto w usłudze Azure HDInsight w systemie Linux klastrów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Presto i Airpal na platformie Hadoop, HDInsight opartych na systemie Linux klastrów za pomocą akcji skryptu."
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
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="cedef-103">Zainstalować i używać Presto w klastrach HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="cedef-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="cedef-104">W tym temacie dowiesz się, jak tooinstall Presto na platformie Hadoop w HDInsight clusters za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="cedef-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="cedef-105">Możesz także dowiedzieć się, jak tooinstall Airpal w istniejącym klastrze Presto usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cedef-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cedef-106">Witaj kroki w tym dokumencie wymagają **klastra usługi HDInsight Hadoop 3.5** używającą systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="cedef-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="cedef-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cedef-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cedef-108">Aby uzyskać więcej informacji, zobacz [wersji usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="cedef-109">Co to jest Presto?</span><span class="sxs-lookup"><span data-stu-id="cedef-109">What is Presto?</span></span>
<span data-ttu-id="cedef-110">[Presto](https://prestodb.io/overview.html) jest szybkie rozproszonej aparatu zapytań SQL dla danych big data.</span><span class="sxs-lookup"><span data-stu-id="cedef-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="cedef-111">Presto nadaje się do interaktywnego kwerend do poziomu petabajtów danych.</span><span class="sxs-lookup"><span data-stu-id="cedef-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="cedef-112">Aby uzyskać więcej informacji na składniki hello Presto i jak one współdziałają, zobacz [Presto pojęcia](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="cedef-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="cedef-113">Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane i Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.</span><span class="sxs-lookup"><span data-stu-id="cedef-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="cedef-114">Niestandardowe składniki, takie jak Presto, odbierania toohelp uzasadnione ekonomicznie Obsługa toofurther należy rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="cedef-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="cedef-115">Może to spowodować nad rozwiązaniem problemu hello lub proszenia tooengage dostępnych kanałów dla hello otwarty technologii źródła wykryto głębokie doświadczenia z tej technologii.</span><span class="sxs-lookup"><span data-stu-id="cedef-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="cedef-116">Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="cedef-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="cedef-117">Zainstaluj Presto za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="cedef-117">Install Presto using script action</span></span>

<span data-ttu-id="cedef-118">Ta sekcja zawiera instrukcje jak toouse hello przykładowy skrypt podczas tworzenia nowego klastra za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cedef-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="cedef-119">Uruchom inicjowania obsługi klastra za pomocą kroków hello w [klastrów usługi HDInsight opartych na systemie Linux należy](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="cedef-120">Upewnij się, że tworzenie klastra hello przy użyciu hello **niestandardowy** przepływu tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="cedef-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="cedef-121">Należy się upewnić się, że tworzenia klastra hello spełnia następujące wymagania hello.</span><span class="sxs-lookup"><span data-stu-id="cedef-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="cedef-122">a.</span><span class="sxs-lookup"><span data-stu-id="cedef-122">a.</span></span> <span data-ttu-id="cedef-123">Musi to być klastra usługi Hadoop z usługą HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="cedef-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="cedef-124">b.</span><span class="sxs-lookup"><span data-stu-id="cedef-124">b.</span></span> <span data-ttu-id="cedef-125">Należy użyć usługi Azure Storage hello przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="cedef-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="cedef-126">Używanie Presto w klastrze, który używa usługi Azure Data Lake Store jako opcji magazynu hello nie jest jeszcze obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cedef-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Tworzenie klastra usługi HDInsight przy użyciu niestandardowych opcji](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="cedef-128">Na powitania **Zaawansowane ustawienia** bloku, wybierz opcję **akcji skryptu**i podaj poniższe informacje hello:</span><span class="sxs-lookup"><span data-stu-id="cedef-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="cedef-129">**Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="cedef-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="cedef-130">**Identyfikator URI skryptu powłoki systemowej**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="cedef-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="cedef-131">**HEAD**: Zaznaczenie tego pola wyboru</span><span class="sxs-lookup"><span data-stu-id="cedef-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="cedef-132">**Proces ROBOCZY**: Zaznaczenie tego pola wyboru</span><span class="sxs-lookup"><span data-stu-id="cedef-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="cedef-133">**DOZORCY**: wyczyść to pole wyboru</span><span class="sxs-lookup"><span data-stu-id="cedef-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="cedef-134">**Parametry**: pozostaw to pole puste</span><span class="sxs-lookup"><span data-stu-id="cedef-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="cedef-135">U dołu hello hello **akcji skryptu** bloku, kliknij przycisk hello **wybierz** przycisk toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cedef-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="cedef-136">Na koniec kliknij hello **wybierz** u dołu hello hello **Zaawansowane ustawienia** bloku toosave hello — informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cedef-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="cedef-137">Kontynuuj, inicjowania obsługi klastra hello zgodnie z opisem w [klastrów usługi HDInsight opartych na systemie Linux należy](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="cedef-138">Program Azure PowerShell, hello Azure CLI, hello zestawu .NET SDK usługi HDInsight lub szablonów usługi Azure Resource Manager może być również używane tooapply akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="cedef-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="cedef-139">Można także zastosować tooalready akcji skryptu działające klastry.</span><span class="sxs-lookup"><span data-stu-id="cedef-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="cedef-140">Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="cedef-141">Korzystanie z usługą HDInsight Presto</span><span class="sxs-lookup"><span data-stu-id="cedef-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="cedef-142">Wykonaj następujące kroki toouse Presto w klastrze usługi HDInsight, po zainstalowaniu go za pomocą hello opisane powyżej hello.</span><span class="sxs-lookup"><span data-stu-id="cedef-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="cedef-143">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="cedef-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="cedef-144">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="cedef-145">Uruchom powłokę Presto hello przy użyciu następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="cedef-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="cedef-146">Uruchom zapytania w tabeli próbki **hivesampletable**, który jest dostępny na wszystkich klastrach HDInsight domyślnie.</span><span class="sxs-lookup"><span data-stu-id="cedef-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="cedef-147">Domyślnie [Hive](https://prestodb.io/docs/current/connector/hive.html) i [TPCH](https://prestodb.io/docs/current/connector/tpch.html) łączników dla Presto są już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="cedef-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="cedef-148">Łącznik hive jest skonfigurowany toouse hello domyślnie zainstalowaną Hive instalacji dlatego wszystkie tabele hello Hive będzie automatycznie wyświetlane w Presto.</span><span class="sxs-lookup"><span data-stu-id="cedef-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="cedef-149">Aby uzyskać szczegółowy opis używania Presto, zobacz [Presto dokumentacji](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="cedef-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="cedef-150">Airpal za pomocą Presto</span><span class="sxs-lookup"><span data-stu-id="cedef-150">Use Airpal with Presto</span></span>

<span data-ttu-id="cedef-151">[Airpal](https://github.com/airbnb/airpal#airpal) jest interfejsem open source opartych na sieci web zapytania dla Presto.</span><span class="sxs-lookup"><span data-stu-id="cedef-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="cedef-152">Aby uzyskać więcej informacji o Airpal, zobacz [dokumentacji Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="cedef-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="cedef-153">W tej sekcji opisano kroki hello zbyt**zainstalować Airpal na powitania edgenode** klastra usługi HDInsight Hadoop Presto już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="cedef-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="cedef-154">Dzięki temu interfejsu zapytania hello Airpal sieci web jest dostępna za pośrednictwem hello Internet.</span><span class="sxs-lookup"><span data-stu-id="cedef-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="cedef-155">Przy użyciu protokołu SSH, połączenie headnode toohello klastra usługi HDInsight hello, który zainstalował Presto:</span><span class="sxs-lookup"><span data-stu-id="cedef-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="cedef-156">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cedef-157">Po nawiązaniu połączenia uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="cedef-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="cedef-158">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="cedef-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="cedef-159">Z danych wyjściowych hello, zanotuj wartość hello na powitania **wartość** właściwości.</span><span class="sxs-lookup"><span data-stu-id="cedef-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="cedef-160">Będzie on potrzebny podczas instalowania Airpal na powitania edgenode klastra.</span><span class="sxs-lookup"><span data-stu-id="cedef-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="cedef-161">Z danych wyjściowych hello powyżej wartości hello, który będzie potrzebny jest **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="cedef-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="cedef-162">Użyj szablonu hello  **[tutaj](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate HDInsight klastra edgenode i podaj wartości hello, jak pokazano w hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="cedef-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![HDInsight instalacji Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="cedef-164">Kliknij pozycję **Kup**.</span><span class="sxs-lookup"><span data-stu-id="cedef-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="cedef-165">Po zatwierdzeniu zmian hello zastosowane toohello konfiguracji klastra, mogą korzystać interfejs sieci web Airpal hello za pomocą hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="cedef-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="cedef-166">a.</span><span class="sxs-lookup"><span data-stu-id="cedef-166">a.</span></span> <span data-ttu-id="cedef-167">W bloku klastra powitania kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cedef-167">From hello cluster blade, click **Applications**.</span></span>

    ![Uruchamianie usługi HDInsight Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="cedef-169">b.</span><span class="sxs-lookup"><span data-stu-id="cedef-169">b.</span></span> <span data-ttu-id="cedef-170">Z hello **zainstalowane aplikacje** bloku, kliknij przycisk **Portal** przed airpal.</span><span class="sxs-lookup"><span data-stu-id="cedef-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![Uruchamianie usługi HDInsight Airpal w klastrze Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="cedef-172">c.</span><span class="sxs-lookup"><span data-stu-id="cedef-172">c.</span></span> <span data-ttu-id="cedef-173">Po wyświetleniu monitu wprowadź poświadczenia administratora hello, które określono podczas tworzenia klastra usługi HDInsight Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="cedef-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="cedef-174">Dostosowanie Presto instalacji w klastrze usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="cedef-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="cedef-175">Po zainstalowaniu Presto w klastrze usługi HDInsight Hadoop, można dostosować hello instalacji toomake zmiany, takie jak ustawienia pamięci aktualizacji, zmień łączniki, itp. Wykonaj hello, więc po toodo czynności.</span><span class="sxs-lookup"><span data-stu-id="cedef-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="cedef-176">Przy użyciu protokołu SSH, połączenie headnode toohello klastra usługi HDInsight hello, który zainstalował Presto:</span><span class="sxs-lookup"><span data-stu-id="cedef-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="cedef-177">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cedef-178">Wprowadź zmiany w konfiguracji w pliku hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="cedef-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="cedef-179">Aby uzyskać więcej informacji na Presto konfiguracji, zobacz [Presto konfiguracji dla klastrów YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="cedef-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="cedef-180">Zatrzymaj i kasowanie hello bieżącego uruchomione wystąpienie Presto.</span><span class="sxs-lookup"><span data-stu-id="cedef-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="cedef-181">Nowe wystąpienie klasy Presto rozpoczynać się hello dostosowania.</span><span class="sxs-lookup"><span data-stu-id="cedef-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="cedef-182">Poczekaj, aż hello nowego wystąpienia toobe gotowy i zanotuj adres presto koordynatora.</span><span class="sxs-lookup"><span data-stu-id="cedef-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="cedef-183">Generowanie wyników testów dla klastrów usługi HDInsight, które są uruchamiane Presto</span><span class="sxs-lookup"><span data-stu-id="cedef-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="cedef-184">TPC DS jest hello branżowy standard do pomiaru wydajności hello wiele systemów wsparcia decyzji, w tym systemy danych big data.</span><span class="sxs-lookup"><span data-stu-id="cedef-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="cedef-185">Można użyć Presto danych toogenerate klastrów usługi HDInsight i ocenić, jak są porównywane z własnych danych testowych HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cedef-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="cedef-186">Aby uzyskać więcej informacji, zobacz [tutaj](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="cedef-187">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cedef-187">See also</span></span>
* <span data-ttu-id="cedef-188">[Zainstalować i używać Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="cedef-189">Odcienia, który jest interfejs użytkownika, który umożliwia łatwe toocreate, uruchom w sieci web i Zapisz zadań Pig i Hive, jak również jako Przeglądaj hello domyślny magazyn dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cedef-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="cedef-190">[Zainstaluj Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="cedef-191">Użyj tooinstall dostosowywania klastra, który Giraph na platformie Hadoop w HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="cedef-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="cedef-192">Giraph pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cedef-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="cedef-193">[Zainstaluj Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cedef-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="cedef-194">Użyj tooinstall dostosowywania klastra, który Solr na platformie Hadoop w HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="cedef-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="cedef-195">Solr umożliwia operacji wyszukiwania zaawansowanego tooperform na przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="cedef-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
