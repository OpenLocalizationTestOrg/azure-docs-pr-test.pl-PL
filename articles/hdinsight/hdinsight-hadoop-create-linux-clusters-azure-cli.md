---
title: "klastry Hadoop aaaCreate przy użyciu wiersza polecenia - hello Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate klastrów usługi HDInsight przy użyciu hello 1.0 interfejsu wiersza polecenia platformy Azure i platform."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="e5fce-103">Tworzenie klastrów usługi HDInsight przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5fce-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e5fce-104">Witaj czynnościach w ramach tego przewodnika dokumentu tworzenia klastra usługi HDInsight 3.5 przy użyciu hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="e5fce-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5fce-105">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e5fce-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e5fce-106">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="e5fce-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e5fce-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e5fce-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="e5fce-108">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="e5fce-108">**An Azure subscription**.</span></span> <span data-ttu-id="e5fce-109">Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e5fce-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="e5fce-110">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="e5fce-110">**Azure CLI**.</span></span> <span data-ttu-id="e5fce-111">z wiersza polecenia platformy Azure w wersji 0.10.14 ostatnio przetestowane Hello kroków w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="e5fce-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5fce-112">kroki Hello w tym dokumencie nie współpracujesz z 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fce-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="e5fce-113">Azure CLI 2.0 nie obsługuje tworzenia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5fce-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="e5fce-114">Zaloguj się za tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5fce-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="e5fce-115">Wykonaj kroki hello udokumentowane w [połączyć tooan subskrypcji platformy Azure z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)](../xplat-cli-connect.md) i nawiąż połączenie przy użyciu hello subskrypcji tooyour **logowania** — metoda.</span><span class="sxs-lookup"><span data-stu-id="e5fce-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="e5fce-116">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="e5fce-116">Create a cluster</span></span>

<span data-ttu-id="e5fce-117">Witaj, wykonaj czynności należy wykonać z poziomu wiersza polecenia, takich jak programu PowerShell lub Bash.</span><span class="sxs-lookup"><span data-stu-id="e5fce-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="e5fce-118">Witaj Użyj następującego polecenia tooauthenticate tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="e5fce-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="e5fce-119">Możesz się zostanie wyświetlony monit o tooprovide swoją nazwę i hasło.</span><span class="sxs-lookup"><span data-stu-id="e5fce-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="e5fce-120">Jeśli masz wiele subskrypcji Azure, użyj `azure account set <subscriptionname>` użyj polecenia tooset hello subskrypcji, która hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fce-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="e5fce-121">Przełącz tryb usługi Resource Manager tooAzure przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5fce-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="e5fce-122">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="e5fce-122">Create a resource group.</span></span> <span data-ttu-id="e5fce-123">Ta grupa zasobów zawiera hello klastra usługi HDInsight i skojarzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5fce-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="e5fce-124">Zastąp `groupname` o unikatowej nazwie hello grupy.</span><span class="sxs-lookup"><span data-stu-id="e5fce-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="e5fce-125">Zastąp `location` z hello region geograficzny, który ma być toocreate hello grupy.</span><span class="sxs-lookup"><span data-stu-id="e5fce-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="e5fce-126">Aby uzyskać listę prawidłowych lokalizacji, użyj hello `azure location list` polecenia, a następnie użyj jednej z lokalizacji hello z hello `Name` kolumny.</span><span class="sxs-lookup"><span data-stu-id="e5fce-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="e5fce-127">Utwórz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5fce-127">Create a storage account.</span></span> <span data-ttu-id="e5fce-128">To konto magazynu jest używany jako hello domyślny magazyn dla klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="e5fce-129">Zastąp `groupname` o nazwie hello hello grupy utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="e5fce-130">Zastąp `location` z tej samej lokalizacji używany w poprzednim kroku hello hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="e5fce-131">Zastąp `storagename` o unikatowej nazwie hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5fce-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e5fce-132">Aby uzyskać więcej informacji o parametrach hello używane w tym poleceniu można używać `azure storage account create -h` tooview pomocy dla tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5fce-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="e5fce-133">Pobieranie hello klucz używany konta magazynu hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e5fce-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="e5fce-134">Zastąp `groupname` z nazwy grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="e5fce-135">Zastąp `storagename` o nazwie hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5fce-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="e5fce-136">Witaj zwrócone dane, Zapisz hello `key` wartość `key1`.</span><span class="sxs-lookup"><span data-stu-id="e5fce-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="e5fce-137">Tworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5fce-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="e5fce-138">Zastąp `groupname` z nazwy grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="e5fce-139">Zastąp `Hadoop` typu klastra hello, że chcesz toocreate.</span><span class="sxs-lookup"><span data-stu-id="e5fce-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="e5fce-140">Na przykład `Hadoop`, `HBase`, `Kafka`, `Spark`, lub `Storm`.</span><span class="sxs-lookup"><span data-stu-id="e5fce-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="e5fce-141">HDInsight klastry są dostępne w różnych typów, które odpowiadają toohello obciążenia lub technologii, która hello klastra dostosowana pod kątem.</span><span class="sxs-lookup"><span data-stu-id="e5fce-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="e5fce-142">Brak toocreate nie obsługiwaną metodą klastra, który łączy wiele typów, takie jak Storm i bazy danych HBase w jednym klastrze.</span><span class="sxs-lookup"><span data-stu-id="e5fce-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="e5fce-143">Zastąp `location` z hello tej samej lokalizacji używane w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="e5fce-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="e5fce-144">Zastąp `storagename` nazwy konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="e5fce-145">Zastąp `storagekey` kluczem hello uzyskanych w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="e5fce-146">Dla hello `--defaultStorageContainer` parametru, użyj hello sama nazwa jak używasz hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e5fce-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="e5fce-147">Zastąp `admin` i `httppassword` hello nazwę i hasło mają toouse podczas uzyskiwania dostępu do klastra hello za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e5fce-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="e5fce-148">Zastąp `sshuser` i `sshuserpassword` hello nazwy użytkownika i hasło mają toouse podczas uzyskiwania dostępu do klastra hello przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="e5fce-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5fce-149">W tym przykładzie jest tworzony klaster z dwoma notes procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e5fce-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="e5fce-150">Po utworzeniu klastra można również zmienić hello liczba węzłów procesu roboczego przez wykonanie operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="e5fce-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="e5fce-151">Jeśli planujesz używanie więcej niż 32 węzłami procesów roboczych, następnie należy wybrać rozmiar węzła głównego z co najmniej 8 rdzeni i 14 GB pamięci RAM.</span><span class="sxs-lookup"><span data-stu-id="e5fce-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="e5fce-152">Można ustawić rozmiaru węzła głównego hello przy użyciu hello `--headNodeSize` parametru podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e5fce-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="e5fce-153">Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e5fce-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="e5fce-154">Może upłynąć kilka minut toofinish procesu tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e5fce-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="e5fce-155">Zazwyczaj około 15.</span><span class="sxs-lookup"><span data-stu-id="e5fce-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="e5fce-156">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e5fce-156">Troubleshoot</span></span>

<span data-ttu-id="e5fce-157">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="e5fce-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5fce-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5fce-158">Next steps</span></span>

<span data-ttu-id="e5fce-159">Po pomyślnym utworzeniu klastra usługi HDInsight przy użyciu hello Azure CLI, za pomocą powitania po toolearn jak toowork z klastrem:</span><span class="sxs-lookup"><span data-stu-id="e5fce-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="e5fce-160">Klastry Hadoop</span><span class="sxs-lookup"><span data-stu-id="e5fce-160">Hadoop clusters</span></span>

* [<span data-ttu-id="e5fce-161">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e5fce-162">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e5fce-163">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="e5fce-164">Klastrów HBase</span><span class="sxs-lookup"><span data-stu-id="e5fce-164">HBase clusters</span></span>

* [<span data-ttu-id="e5fce-165">Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="e5fce-166">Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="e5fce-167">Klastry STORM</span><span class="sxs-lookup"><span data-stu-id="e5fce-167">Storm clusters</span></span>

* [<span data-ttu-id="e5fce-168">Tworzenie topologii Java dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="e5fce-169">Użyj składników języka Python w Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="e5fce-170">Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5fce-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
