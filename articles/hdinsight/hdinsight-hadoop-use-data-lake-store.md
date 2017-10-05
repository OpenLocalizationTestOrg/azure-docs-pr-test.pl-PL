---
title: "Używanie usługi Data Lake Store z platformą Hadoop w usłudze Azure HDInsight | Microsoft Docs"
description: "Dowiedz się, jak wykonywać zapytania o dane z usługi Azure Data Lake Store i zapisywać wyniki analiz."
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
ms.openlocfilehash: 28a836aff65636ef0031ac63f633d746436d7e4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="f3487-104">Korzystanie z usługi Data Lake Store w połączeniu z klastrami usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3487-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="f3487-105">Aby analizować dane w klastrze usługi HDInsight, możesz je zapisać w usłudze [Microsoft Azure Storage](../storage/common/storage-introduction.md) lub [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) albo obu tych usługach.</span><span class="sxs-lookup"><span data-stu-id="f3487-105">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="f3487-106">Obie opcje magazynowania pozwalają bezpiecznie usuwać klastry usługi HDInsight używane do obliczeń bez utraty danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3487-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="f3487-107">W tym artykule omówiono współdziałanie usługi Data Lake Store z klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f3487-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="f3487-108">Aby dowiedzieć się, jak usługa Microsoft Azure Storage współdziała z klastrami usługi HDInsight, zobacz [Use Azure Storage with Azure HDInsight clusters (Używanie usługi Microsoft Azure Storage z klastrami usługi Azure HDInsight)](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f3487-108">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="f3487-109">Więcej informacji dotyczących tworzenia klastra usługi HDInsight można znaleźć w temacie [Create Hadoop clusters in HDInsight (Tworzenie klastrów platformy Hadoop w usłudze HDInsight)](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f3487-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f3487-110">Usługa Data Lake Store jest dostępna wyłącznie przez zabezpieczony kanał, dlatego nazwa schematu systemu plików `adls` nie jest używana.</span><span class="sxs-lookup"><span data-stu-id="f3487-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="f3487-111">Zawsze używaj nazwy `adl`.</span><span class="sxs-lookup"><span data-stu-id="f3487-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="f3487-112">Dostępność klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3487-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="f3487-113">Platforma Hadoop obsługuje pojęcie domyślnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="f3487-113">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="f3487-114">Domyślny system plików wyznacza domyślny schemat i element authority.</span><span class="sxs-lookup"><span data-stu-id="f3487-114">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="f3487-115">Może również służyć do rozpoznawania ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="f3487-115">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="f3487-116">W trakcie procesu tworzenia klastra usługi HDInsight jako domyślny system plików można wskazać kontener obiektów blob w usłudze Azure Storage. W przypadku wersji 3.5 lub nowszych wersji usługi HDInsight jako domyślny system plików można wybrać usługę Microsoft Azure Storage lub Azure Data Lake Store (z nielicznymi wyjątkami).</span><span class="sxs-lookup"><span data-stu-id="f3487-116">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> 

<span data-ttu-id="f3487-117">Klastry usługi HDInsight mogą używać usługi Data Lake Store na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="f3487-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="f3487-118">Jako magazyn domyślny</span><span class="sxs-lookup"><span data-stu-id="f3487-118">As the default storage</span></span>
* <span data-ttu-id="f3487-119">Jako magazyn dodatkowy z rozszerzeniem Azure Storage Blob jako magazynem domyślnym</span><span class="sxs-lookup"><span data-stu-id="f3487-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="f3487-120">Aktualnie tylko niektóre typy/wersje klastra usługi HDInsight obsługują używanie kont usługi Data Lake Store jako magazynu domyślnego i magazynu dodatkowego:</span><span class="sxs-lookup"><span data-stu-id="f3487-120">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="f3487-121">Typ klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="f3487-121">HDInsight cluster type</span></span> | <span data-ttu-id="f3487-122">Usługa Data Lake Store jako magazyn domyślny</span><span class="sxs-lookup"><span data-stu-id="f3487-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="f3487-123">Usługa Data Lake Store jako magazyn dodatkowy</span><span class="sxs-lookup"><span data-stu-id="f3487-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="f3487-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f3487-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="f3487-125">HDInsight w wersji 3.6</span><span class="sxs-lookup"><span data-stu-id="f3487-125">HDInsight version 3.6</span></span> | <span data-ttu-id="f3487-126">Tak</span><span class="sxs-lookup"><span data-stu-id="f3487-126">Yes</span></span> | <span data-ttu-id="f3487-127">Tak</span><span class="sxs-lookup"><span data-stu-id="f3487-127">Yes</span></span> | |
| <span data-ttu-id="f3487-128">HDInsight w wersji 3.5</span><span class="sxs-lookup"><span data-stu-id="f3487-128">HDInsight version 3.5</span></span> | <span data-ttu-id="f3487-129">Tak</span><span class="sxs-lookup"><span data-stu-id="f3487-129">Yes</span></span> | <span data-ttu-id="f3487-130">Tak</span><span class="sxs-lookup"><span data-stu-id="f3487-130">Yes</span></span> | <span data-ttu-id="f3487-131">Z wyjątkiem bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="f3487-131">With the exception of HBase</span></span>|
| <span data-ttu-id="f3487-132">HDInsight w wersji 3.4</span><span class="sxs-lookup"><span data-stu-id="f3487-132">HDInsight version 3.4</span></span> | <span data-ttu-id="f3487-133">Nie</span><span class="sxs-lookup"><span data-stu-id="f3487-133">No</span></span> | <span data-ttu-id="f3487-134">Tak</span><span class="sxs-lookup"><span data-stu-id="f3487-134">Yes</span></span> | |
| <span data-ttu-id="f3487-135">HDInsight w wersji 3.3</span><span class="sxs-lookup"><span data-stu-id="f3487-135">HDInsight version 3.3</span></span> | <span data-ttu-id="f3487-136">Nie</span><span class="sxs-lookup"><span data-stu-id="f3487-136">No</span></span> | <span data-ttu-id="f3487-137">Nie</span><span class="sxs-lookup"><span data-stu-id="f3487-137">No</span></span> | |
| <span data-ttu-id="f3487-138">HDInsight w wersji 3.2</span><span class="sxs-lookup"><span data-stu-id="f3487-138">HDInsight version 3.2</span></span> | <span data-ttu-id="f3487-139">Nie</span><span class="sxs-lookup"><span data-stu-id="f3487-139">No</span></span> | <span data-ttu-id="f3487-140">Tak</span><span class="sxs-lookup"><span data-stu-id="f3487-140">Yes</span></span> | |
| <span data-ttu-id="f3487-141">HDInsight Premium (warstwa)</span><span class="sxs-lookup"><span data-stu-id="f3487-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="f3487-142">Nie</span><span class="sxs-lookup"><span data-stu-id="f3487-142">No</span></span> | <span data-ttu-id="f3487-143">Nie</span><span class="sxs-lookup"><span data-stu-id="f3487-143">No</span></span> | |
| <span data-ttu-id="f3487-144">Storm</span><span class="sxs-lookup"><span data-stu-id="f3487-144">Storm</span></span> | | |<span data-ttu-id="f3487-145">Usługa Data Lake Store umożliwia zapisanie danych pochodzących z topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="f3487-145">You can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="f3487-146">Usługi Data Lake Store można również używać do obsługi danych referencyjnych, które następnie mogą być odczytywane przez topologię Storm.</span><span class="sxs-lookup"><span data-stu-id="f3487-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="f3487-147">Używanie usługi Data Lake Store jako konta magazynu dodatkowego nie ma wpływu na wydajność ani możliwość odczytywania danych z klastra lub zapisywania ich w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f3487-147">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="f3487-148">Używanie usługi Data Lake Store jako magazynu domyślnego</span><span class="sxs-lookup"><span data-stu-id="f3487-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="f3487-149">Po wdrożeniu usługi HDInsight z usługą Data Lake Store jako magazynem domyślnym pliki klastra są zapisywane w usłudze Data Lake Store w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="f3487-149">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="f3487-150">gdzie `<cluster_root_path>` to nazwa folderu utworzonego w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3487-150">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="f3487-151">Określając ścieżkę główną dla każdego klastra, możesz użyć tego samego konta usługi Data Lake Store dla wielu klastrów.</span><span class="sxs-lookup"><span data-stu-id="f3487-151">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="f3487-152">Dlatego jest możliwa następująca konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="f3487-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="f3487-153">Klaster1 może używać ścieżki `adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="f3487-153">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="f3487-154">Klaster2 może używać ścieżki `adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="f3487-154">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="f3487-155">Zwróć uwagę, że oba klastry używają tego samego konta usługi Data Lake Store — **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="f3487-155">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="f3487-156">Każdy klaster ma dostęp do własnego głównego systemu plików w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3487-156">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="f3487-157">W środowisku wdrażania witryny Azure Portal zostanie wyświetlony monit o użycie nazwy folderu, takiej jak **/clusters/\<nazwa_klastra>**, dla ścieżki głównej.</span><span class="sxs-lookup"><span data-stu-id="f3487-157">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

<span data-ttu-id="f3487-158">Aby używanie usługi Data Lake Store jako magazynu domyślnego było możliwe, jednostka usługi musi mieć dostęp do następujących ścieżek:</span><span class="sxs-lookup"><span data-stu-id="f3487-158">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span></span>

- <span data-ttu-id="f3487-159">Katalog główny konta usługi Data Lake Store,</span><span class="sxs-lookup"><span data-stu-id="f3487-159">The Data Lake Store account root.</span></span>  <span data-ttu-id="f3487-160">na przykład: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="f3487-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="f3487-161">Folder zawierający wszystkie foldery klastra,</span><span class="sxs-lookup"><span data-stu-id="f3487-161">The folder for all cluster folders.</span></span>  <span data-ttu-id="f3487-162">na przykład: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="f3487-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="f3487-163">Folder klastra,</span><span class="sxs-lookup"><span data-stu-id="f3487-163">The folder for the cluster.</span></span>  <span data-ttu-id="f3487-164">na przykład: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="f3487-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="f3487-165">Aby uzyskać więcej informacji na temat tworzenia jednostki usługi i przyznawania dostępu, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="f3487-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="f3487-166">Używanie usługi Data Lake Store jako magazynu dodatkowego</span><span class="sxs-lookup"><span data-stu-id="f3487-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="f3487-167">Jako dodatkowego magazynu dla klastra można również użyć usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3487-167">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="f3487-168">Domyślnym magazynem klastra może wtedy być konto usługi Azure Storage Blob lub Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3487-168">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="f3487-169">Jeśli do obsługi danych przechowywanych w usłudze Data Lake Store jako magazynie dodatkowym używasz zadań usługi HDInsight, musisz podać w pełni kwalifikowaną ścieżkę do plików.</span><span class="sxs-lookup"><span data-stu-id="f3487-169">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="f3487-170">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f3487-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="f3487-171">Zwróć uwagę, że teraz w adresie URL nie ma elementu **cluster_root_path**.</span><span class="sxs-lookup"><span data-stu-id="f3487-171">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="f3487-172">Przyczyną jest to, że w tym przypadku usługa Data Lake Store nie jest magazynem domyślnym, więc należy tylko podać ścieżkę do plików.</span><span class="sxs-lookup"><span data-stu-id="f3487-172">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>

<span data-ttu-id="f3487-173">Aby używać usługi Data Lake Store jako magazynu dodatkowego, wystarczy przyznać jednostce usługi dostęp do ścieżek przechowywania plików.</span><span class="sxs-lookup"><span data-stu-id="f3487-173">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span></span>  <span data-ttu-id="f3487-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f3487-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="f3487-175">Aby uzyskać więcej informacji na temat tworzenia jednostki usługi i przyznawania dostępu, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="f3487-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="f3487-176">Używanie wielu kont usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3487-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="f3487-177">Aby dodać kilka kont usługi Data Lake Store, należy przyznać klastrowi usługi HDInsight uprawnienia do danych na kontach usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3487-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="f3487-178">Zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="f3487-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="f3487-179">Konfigurowanie dostępu do usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3487-179">Configure Data Lake store access</span></span>

<span data-ttu-id="f3487-180">Aby skonfigurować dostęp do usługi Data Lake Store z klastra usługi HDInsight, musisz mieć jednostkę usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3487-180">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="f3487-181">Tylko administrator usługi Azure AD może utworzyć jednostkę usługi.</span><span class="sxs-lookup"><span data-stu-id="f3487-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="f3487-182">Jednostkę usługi należy utworzyć przy użyciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f3487-182">The service principal must be created with a certificate.</span></span> <span data-ttu-id="f3487-183">Aby uzyskać więcej informacji, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) i [Create service principal with self-signed-certificate (Tworzenie jednostki usługi przy użyciu certyfikatu z podpisem własnym)](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="f3487-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="f3487-184">Jeśli zamierzasz używać usługi Azure Data Lake Store jako dodatkowego magazynu klastra usługi HDInsight, zdecydowanie zalecamy wykonanie tej czynności podczas tworzenia klastra zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f3487-184">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="f3487-185">Dodawanie usługi Azure Data Lake Store jako dodatkowego magazynu do istniejącego klastra usługi HDInsight jest skomplikowane i podatne na błędy.</span><span class="sxs-lookup"><span data-stu-id="f3487-185">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

## <a name="access-files-from-the-cluster"></a><span data-ttu-id="f3487-186">Dostęp do plików z klastra</span><span class="sxs-lookup"><span data-stu-id="f3487-186">Access files from the cluster</span></span>

<span data-ttu-id="f3487-187">Istnieją różne sposoby uzyskiwania dostępu do plików w usłudze Data Lake Store z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f3487-187">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="f3487-188">**Przy użyciu w pełni kwalifikowanej nazwy**.</span><span class="sxs-lookup"><span data-stu-id="f3487-188">**Using the fully qualified name**.</span></span> <span data-ttu-id="f3487-189">W przypadku tej metody należy podać pełną ścieżkę do pliku, do którego chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="f3487-189">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="f3487-190">**Przy użyciu skróconego formatu ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="f3487-190">**Using the shortened path format**.</span></span> <span data-ttu-id="f3487-191">W przypadku tej metody należy zastąpić ścieżkę do katalogu głównego klastra prefiksem adl:///.</span><span class="sxs-lookup"><span data-stu-id="f3487-191">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="f3487-192">W powyższym przykładzie można zastąpić ścieżkę `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` prefiksem `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="f3487-192">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="f3487-193">**Przy użyciu ścieżki względnej**.</span><span class="sxs-lookup"><span data-stu-id="f3487-193">**Using the relative path**.</span></span> <span data-ttu-id="f3487-194">W przypadku tej metody należy podać tylko względną ścieżkę do pliku, do którego chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="f3487-194">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="f3487-195">Na przykład jeśli pełna ścieżka do pliku to:</span><span class="sxs-lookup"><span data-stu-id="f3487-195">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="f3487-196">Dostęp do tego samego pliku sample.log można uzyskać zamiast tego za pomocą tej ścieżki względnej.</span><span class="sxs-lookup"><span data-stu-id="f3487-196">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="f3487-197">Tworzenie klastrów usługi HDInsight z dostępem do usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3487-197">Create HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="f3487-198">Poniższe linki pozwalają uzyskać szczegółowe instrukcje dotyczące tworzenia klastrów usługi HDInsight z dostępem do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f3487-198">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="f3487-199">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="f3487-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* <span data-ttu-id="f3487-200">[HDInsight with Data Lake Store as default storage - PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md) (Usługa HDInsight z usługą Data Lake Store jako magazynem domyślnym — PowerShell)</span><span class="sxs-lookup"><span data-stu-id="f3487-200">[Using PowerShell (with Data Lake Store as default storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)</span></span>
* <span data-ttu-id="f3487-201">[Using PowerShell (with Data Lake Store as additional storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md) (Korzystanie z programu PowerShell z usługą Data Lake Store jako magazynem dodatkowym)</span><span class="sxs-lookup"><span data-stu-id="f3487-201">[Using PowerShell (with Data Lake Store as additional storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)</span></span>
* [<span data-ttu-id="f3487-202">Korzystanie z szablonów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f3487-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="f3487-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3487-203">Next steps</span></span>
<span data-ttu-id="f3487-204">W tym artykule przedstawiono sposób korzystania z usługi Azure Data Lake Store zgodnej z systemem plików HDFS w połączeniu z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f3487-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="f3487-205">Podane tu informacje umożliwiają tworzenie skalowalnych, długoterminowych rozwiązań do pozyskiwania danych archiwalnych i używanie usługi HDInsight w celu efektywnego wykorzystywania informacji przechowywanych w postaci danych ze strukturą i bez niej.</span><span class="sxs-lookup"><span data-stu-id="f3487-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="f3487-206">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="f3487-206">For more information, see:</span></span>

* <span data-ttu-id="f3487-207">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f3487-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="f3487-208">Wprowadzenie do usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f3487-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="f3487-209">[Przekazywanie danych do usługi HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="f3487-209">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="f3487-210">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f3487-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f3487-211">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f3487-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f3487-212">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas] (Używanie sygnatur dostępu współdzielonego do usługi Azure Storage, aby ograniczyć dostęp do danych za pomocą usługi HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f3487-212">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
