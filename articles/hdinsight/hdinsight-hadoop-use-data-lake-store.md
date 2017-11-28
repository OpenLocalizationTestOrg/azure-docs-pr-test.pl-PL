---
title: "Data Lake Store z platformą Hadoop w usłudze Azure HDInsight aaaUse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooquery danych z usługi Azure Data Lake Store i toostore wyniki analiz."
keywords: blob storage,hdfs,structured data,unstructured data, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="abaa6-104">Korzystanie z usługi Data Lake Store w połączeniu z klastrami usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="abaa6-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="abaa6-105">dane tooanalyze w klastrze usługi HDInsight, dane można przechowywać na powitania albo w [usługi Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), lub obie.</span><span class="sxs-lookup"><span data-stu-id="abaa6-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="abaa6-106">Obie te opcje magazynu Włącz toosafely usunąć klastrów usługi HDInsight używane do obliczeń bez utraty danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="abaa6-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="abaa6-107">W tym artykule omówiono współdziałanie usługi Data Lake Store z klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abaa6-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="abaa6-108">toolearn magazynu Azure współpracuje z klastrami HDInsight, zobacz [użycia usługi Azure Storage z usługą Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="abaa6-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="abaa6-109">Więcej informacji dotyczących tworzenia klastra usługi HDInsight można znaleźć w artykule [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów platformy Hadoop w usłudze HDInsight).</span><span class="sxs-lookup"><span data-stu-id="abaa6-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="abaa6-110">Usługa Data Lake Store jest dostępna wyłącznie przez zabezpieczony kanał, dlatego nazwa schematu systemu plików `adls` nie jest używana.</span><span class="sxs-lookup"><span data-stu-id="abaa6-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="abaa6-111">Zawsze używaj nazwy `adl`.</span><span class="sxs-lookup"><span data-stu-id="abaa6-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="abaa6-112">Dostępność klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="abaa6-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="abaa6-113">Platforma Hadoop obsługuje pojęcie domyślnego systemu plików hello.</span><span class="sxs-lookup"><span data-stu-id="abaa6-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="abaa6-114">system plików domyślne Hello wyznacza domyślny schemat i urząd.</span><span class="sxs-lookup"><span data-stu-id="abaa6-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="abaa6-115">Można także używane tooresolve ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="abaa6-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="abaa6-116">Podczas procesu tworzenia klastra usługi HDInsight hello, można określić kontenera obiektów blob w magazynie Azure jako hello domyślny system plików lub HDInsight 3.5 i nowszych wersji, można wybrać magazyn Azure lub usługi Azure Data Lake Store jako system plików domyślne hello z kilka wyjątków.</span><span class="sxs-lookup"><span data-stu-id="abaa6-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="abaa6-117">Klastry usługi HDInsight mogą używać usługi Data Lake Store na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="abaa6-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="abaa6-118">Jako hello domyślny magazyn</span><span class="sxs-lookup"><span data-stu-id="abaa6-118">As hello default storage</span></span>
* <span data-ttu-id="abaa6-119">Jako magazyn dodatkowy z rozszerzeniem Azure Storage Blob jako magazynem domyślnym</span><span class="sxs-lookup"><span data-stu-id="abaa6-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="abaa6-120">Od tej chwili tylko niektóre hello HDInsight klastra obsługi typów/wersji przy użyciu usługi Data Lake Store jako domyślnego magazynu i dodatkowych kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="abaa6-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="abaa6-121">Typ klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="abaa6-121">HDInsight cluster type</span></span> | <span data-ttu-id="abaa6-122">Usługa Data Lake Store jako magazyn domyślny</span><span class="sxs-lookup"><span data-stu-id="abaa6-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="abaa6-123">Usługa Data Lake Store jako magazyn dodatkowy</span><span class="sxs-lookup"><span data-stu-id="abaa6-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="abaa6-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="abaa6-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="abaa6-125">HDInsight w wersji 3.6</span><span class="sxs-lookup"><span data-stu-id="abaa6-125">HDInsight version 3.6</span></span> | <span data-ttu-id="abaa6-126">Tak</span><span class="sxs-lookup"><span data-stu-id="abaa6-126">Yes</span></span> | <span data-ttu-id="abaa6-127">Tak</span><span class="sxs-lookup"><span data-stu-id="abaa6-127">Yes</span></span> | |
| <span data-ttu-id="abaa6-128">HDInsight w wersji 3.5</span><span class="sxs-lookup"><span data-stu-id="abaa6-128">HDInsight version 3.5</span></span> | <span data-ttu-id="abaa6-129">Tak</span><span class="sxs-lookup"><span data-stu-id="abaa6-129">Yes</span></span> | <span data-ttu-id="abaa6-130">Tak</span><span class="sxs-lookup"><span data-stu-id="abaa6-130">Yes</span></span> | <span data-ttu-id="abaa6-131">Z wyjątkiem hello HBase</span><span class="sxs-lookup"><span data-stu-id="abaa6-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="abaa6-132">HDInsight w wersji 3.4</span><span class="sxs-lookup"><span data-stu-id="abaa6-132">HDInsight version 3.4</span></span> | <span data-ttu-id="abaa6-133">Nie</span><span class="sxs-lookup"><span data-stu-id="abaa6-133">No</span></span> | <span data-ttu-id="abaa6-134">Tak</span><span class="sxs-lookup"><span data-stu-id="abaa6-134">Yes</span></span> | |
| <span data-ttu-id="abaa6-135">HDInsight w wersji 3.3</span><span class="sxs-lookup"><span data-stu-id="abaa6-135">HDInsight version 3.3</span></span> | <span data-ttu-id="abaa6-136">Nie</span><span class="sxs-lookup"><span data-stu-id="abaa6-136">No</span></span> | <span data-ttu-id="abaa6-137">Nie</span><span class="sxs-lookup"><span data-stu-id="abaa6-137">No</span></span> | |
| <span data-ttu-id="abaa6-138">HDInsight w wersji 3.2</span><span class="sxs-lookup"><span data-stu-id="abaa6-138">HDInsight version 3.2</span></span> | <span data-ttu-id="abaa6-139">Nie</span><span class="sxs-lookup"><span data-stu-id="abaa6-139">No</span></span> | <span data-ttu-id="abaa6-140">Tak</span><span class="sxs-lookup"><span data-stu-id="abaa6-140">Yes</span></span> | |
| <span data-ttu-id="abaa6-141">HDInsight Premium (warstwa)</span><span class="sxs-lookup"><span data-stu-id="abaa6-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="abaa6-142">Nie</span><span class="sxs-lookup"><span data-stu-id="abaa6-142">No</span></span> | <span data-ttu-id="abaa6-143">Nie</span><span class="sxs-lookup"><span data-stu-id="abaa6-143">No</span></span> | |
| <span data-ttu-id="abaa6-144">Storm</span><span class="sxs-lookup"><span data-stu-id="abaa6-144">Storm</span></span> | | |<span data-ttu-id="abaa6-145">Data Lake Store toowrite danych można użyć od topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="abaa6-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="abaa6-146">Usługi Data Lake Store można również używać do obsługi danych referencyjnych, które następnie mogą być odczytywane przez topologię Storm.</span><span class="sxs-lookup"><span data-stu-id="abaa6-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="abaa6-147">Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpłynąć na wydajność lub tooread możliwości hello lub zapis tooAzure magazynu z klastra hello.</span><span class="sxs-lookup"><span data-stu-id="abaa6-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="abaa6-148">Używanie usługi Data Lake Store jako magazynu domyślnego</span><span class="sxs-lookup"><span data-stu-id="abaa6-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="abaa6-149">Po wdrożeniu usługi HDInsight z usługą Data Lake Store jako domyślny magazyn plików związanych z klastrem hello są przechowywane w usłudze Data Lake Store w hello w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="abaa6-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="abaa6-150">gdzie `<cluster_root_path>` jest nazwą hello folderu utworzyć w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="abaa6-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="abaa6-151">Określ ścieżkę katalogu głównego dla każdego klastra, można użyć hello tego samego konta usługi Data Lake Store dla więcej niż jednego klastra.</span><span class="sxs-lookup"><span data-stu-id="abaa6-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="abaa6-152">Dlatego jest możliwa następująca konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="abaa6-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="abaa6-153">Klaster1 można użyć ścieżki hello`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="abaa6-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="abaa6-154">Cluster2 można użyć ścieżki hello`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="abaa6-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="abaa6-155">Powiadomienie zarówno tekst hello Użyj klastrów hello same konta usługi Data Lake Store **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="abaa6-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="abaa6-156">Każdy klaster ma własny system plików głównego w usłudze Data Lake Store tooits dostępu.</span><span class="sxs-lookup"><span data-stu-id="abaa6-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="abaa6-157">Witaj środowisko wdrażania portalu Azure w szczególności monit toouse nazwę folderu takich jak **/clusters/\<clustername >** hello ścieżki katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="abaa6-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="abaa6-158">toobe stanie toouse usługi Data Lake Store jako domyślny magazyn, należy udzielić toohello główna dostępu usługi hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="abaa6-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="abaa6-159">Witaj głównego konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="abaa6-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="abaa6-160">na przykład: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="abaa6-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="abaa6-161">folder Hello wszystkie foldery klastra.</span><span class="sxs-lookup"><span data-stu-id="abaa6-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="abaa6-162">na przykład: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="abaa6-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="abaa6-163">folder Hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="abaa6-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="abaa6-164">na przykład: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="abaa6-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="abaa6-165">Aby uzyskać więcej informacji na temat tworzenia jednostki usługi i przyznawania dostępu, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="abaa6-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="abaa6-166">Używanie usługi Data Lake Store jako magazynu dodatkowego</span><span class="sxs-lookup"><span data-stu-id="abaa6-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="abaa6-167">Data Lake Store jako dodatkowego miejsca do magazynowania służy również hello klastra.</span><span class="sxs-lookup"><span data-stu-id="abaa6-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="abaa6-168">W takich przypadkach hello klastra domyślny magazyn może być obiektu Blob magazynu Azure lub konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="abaa6-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="abaa6-169">Jeśli używasz zadań HDInsight hello danych przechowywanych w usłudze Data Lake Store jako dodatkowego magazynu, należy użyć hello w pełni kwalifikowaną ścieżkę toohello plików.</span><span class="sxs-lookup"><span data-stu-id="abaa6-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="abaa6-170">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="abaa6-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="abaa6-171">Należy pamiętać, że ma nie **cluster_root_path** hello teraz adres URL.</span><span class="sxs-lookup"><span data-stu-id="abaa6-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="abaa6-172">Wynika usługi Data Lake Store nie jest magazynu domyślną w tym przypadku więc toodo wystarczy zapewnić hello ścieżki toohello pliki.</span><span class="sxs-lookup"><span data-stu-id="abaa6-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="abaa6-173">toobe stanie toouse usługi Data Lake Store jako dodatkowego magazynu, tylko potrzebne toogrant hello usługi głównej dostępu toohello ścieżki gdzie są przechowywane pliki.</span><span class="sxs-lookup"><span data-stu-id="abaa6-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="abaa6-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="abaa6-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="abaa6-175">Aby uzyskać więcej informacji na temat tworzenia jednostki usługi i przyznawania dostępu, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="abaa6-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="abaa6-176">Używanie wielu kont usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="abaa6-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="abaa6-177">Dodanie konta usługi Data Lake Store jako dodatkowego i dodanie więcej niż jednej usługi Data Lake Store konta są realizowane przez nadanie uprawnień klastra usługi HDInsight hello na danych w jednej lub więcej kont usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="abaa6-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="abaa6-178">Zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="abaa6-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="abaa6-179">Konfigurowanie dostępu do usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="abaa6-179">Configure Data Lake store access</span></span>

<span data-ttu-id="abaa6-180">tooconfigure Data Lake dostęp do sklepu z klastrem usługi HDInsight, musi mieć usługi Azure Active directory (Azure AD) nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="abaa6-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="abaa6-181">Tylko administrator usługi Azure AD może utworzyć jednostkę usługi.</span><span class="sxs-lookup"><span data-stu-id="abaa6-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="abaa6-182">nazwy głównej usługi Hello musi zostać utworzony przy użyciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="abaa6-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="abaa6-183">Aby uzyskać więcej informacji, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) i [Create service principal with self-signed-certificate (Tworzenie jednostki usługi przy użyciu certyfikatu z podpisem własnym)](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="abaa6-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="abaa6-184">Jeśli zamierzasz toouse Azure Data Lake Store jako dodatkowego magazynu dla klastra usługi HDInsight, zdecydowanie zaleca się to zrobić podczas tworzenia klastra hello zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="abaa6-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="abaa6-185">Dodawanie usługi Azure Data Lake Store jako dodatkowego magazynu tooan istniejącym klastrze usługi HDInsight to skomplikowany proces i tooerrors podatnych na błędy.</span><span class="sxs-lookup"><span data-stu-id="abaa6-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="abaa6-186">Uzyskiwanie dostępu do plików z hello klastra</span><span class="sxs-lookup"><span data-stu-id="abaa6-186">Access files from hello cluster</span></span>

<span data-ttu-id="abaa6-187">Istnieje kilka sposobów dostępne pliki hello w usłudze Data Lake Store z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abaa6-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="abaa6-188">**Przy użyciu w pełni kwalifikowana nazwa hello**.</span><span class="sxs-lookup"><span data-stu-id="abaa6-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="abaa6-189">Z tej metody, podaj hello pełną ścieżkę toohello plików, które mają tooaccess.</span><span class="sxs-lookup"><span data-stu-id="abaa6-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="abaa6-190">**Przy użyciu formatu ścieżki skróconą hello**.</span><span class="sxs-lookup"><span data-stu-id="abaa6-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="abaa6-191">Z tej metody można zastąpić ścieżki hello zapasowej głównego klastra toohello adl: / / /.</span><span class="sxs-lookup"><span data-stu-id="abaa6-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="abaa6-192">Dlatego w powyższym przykładzie hello, musisz zastąpić `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` z `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="abaa6-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="abaa6-193">**Za pomocą ścieżki względnej hello**.</span><span class="sxs-lookup"><span data-stu-id="abaa6-193">**Using hello relative path**.</span></span> <span data-ttu-id="abaa6-194">Z tej metody, tylko podać hello ścieżki względnej toohello plików, które mają tooaccess.</span><span class="sxs-lookup"><span data-stu-id="abaa6-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="abaa6-195">Na przykład, jeśli plik toohello pełną ścieżkę hello jest:</span><span class="sxs-lookup"><span data-stu-id="abaa6-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="abaa6-196">Dostęp można uzyskać hello przy użyciu tej ścieżki względnej zamiast tego samego pliku sample.log.</span><span class="sxs-lookup"><span data-stu-id="abaa6-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="abaa6-197">Tworzenie klastrów usługi HDInsight na uzyskiwanie dostępu do tooData Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="abaa6-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="abaa6-198">Użyj następującego łącza, aby uzyskać szczegółowe instrukcje na jak toocreate, który klastrów usługi HDInsight z dostępu do magazynu Lake tooData hello.</span><span class="sxs-lookup"><span data-stu-id="abaa6-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="abaa6-199">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="abaa6-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* <span data-ttu-id="abaa6-200">[HDInsight with Data Lake Store as default storage - PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md) (Usługa HDInsight z usługą Data Lake Store jako magazynem domyślnym — PowerShell)</span><span class="sxs-lookup"><span data-stu-id="abaa6-200">[Using PowerShell (with Data Lake Store as default storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)</span></span>
* <span data-ttu-id="abaa6-201">[Using PowerShell (with Data Lake Store as additional storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md) (Korzystanie z programu PowerShell z usługą Data Lake Store jako magazynem dodatkowym)</span><span class="sxs-lookup"><span data-stu-id="abaa6-201">[Using PowerShell (with Data Lake Store as additional storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)</span></span>
* [<span data-ttu-id="abaa6-202">Korzystanie z szablonów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="abaa6-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="abaa6-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abaa6-203">Next steps</span></span>
<span data-ttu-id="abaa6-204">W tym artykule należy przedstawiono sposób toouse zgodnego systemem plików HDFS Azure Data Lake Store z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abaa6-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="abaa6-205">Dzięki temu można toobuild skalowalnych, długoterminowych, archiwizacji rozwiązań do pozyskiwania danych i użyj HDInsight toounlock hello informacji wewnątrz hello przechowywane strukturalnych i danych bez struktury.</span><span class="sxs-lookup"><span data-stu-id="abaa6-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="abaa6-206">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="abaa6-206">For more information, see:</span></span>

* <span data-ttu-id="abaa6-207">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="abaa6-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="abaa6-208">Wprowadzenie do usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="abaa6-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="abaa6-209">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="abaa6-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="abaa6-210">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="abaa6-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="abaa6-211">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="abaa6-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="abaa6-212">[Korzystanie z usługą HDInsight toodata dostępu toorestrict sygnatury dostępu współdzielonego magazynu Azure][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="abaa6-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
