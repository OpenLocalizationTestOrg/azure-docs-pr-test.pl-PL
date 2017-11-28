---
title: "aaaCopy tooand danych z WASB do usługi Data Lake Store za pomocą narzędzia Distcp | Dokumentacja firmy Microsoft"
description: "Użyj narzędzia Distcp narzędzie toocopy danych tooand z Azure magazynu obiektów blob tooData Lake — Magazyn"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="2fe5a-103">Użyj narzędzia Distcp toocopy danych między obiektach blob magazynu Azure i usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2fe5a-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2fe5a-104">Korzystanie z narzędzia DistCp</span><span class="sxs-lookup"><span data-stu-id="2fe5a-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="2fe5a-105">Korzystanie z narzędzia AdlCopy</span><span class="sxs-lookup"><span data-stu-id="2fe5a-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="2fe5a-106">Po utworzeniu klastra usługi HDInsight, który ma konto usługi Data Lake Store tooa dostępu, można użyć narzędzia ekosystemu Hadoop, takie jak dane toocopy narzędzia Distcp **tooand z** magazynu klastra usługi HDInsight (WASB) do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="2fe5a-107">Ten artykuł zawiera instrukcje na temat tooachieve to.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fe5a-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2fe5a-108">Prerequisites</span></span>
<span data-ttu-id="2fe5a-109">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2fe5a-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="2fe5a-110">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-110">**An Azure subscription**.</span></span> <span data-ttu-id="2fe5a-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2fe5a-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2fe5a-112">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2fe5a-113">Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2fe5a-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="2fe5a-114">**Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="2fe5a-115">Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2fe5a-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="2fe5a-116">Upewnij się, że włączenie pulpitu zdalnego dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="2fe5a-117">Czy dzięki filmom szybko się uczysz?</span><span class="sxs-lookup"><span data-stu-id="2fe5a-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="2fe5a-118">[Obejrzyj ten film](https://mix.office.com/watch/1liuojvdx6sie) na temat danych toocopy między obiektach blob magazynu Azure i usługi Data Lake Store za pomocą narzędzia DistCp.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="2fe5a-119">Za pomocą narzędzia Distcp z klastra usługi HDInsight w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="2fe5a-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="2fe5a-120">Klaster usługi HDInsight jest dostarczany z hello narzędzia Distcp narzędzia, które mogą być używane toocopy danych z różnych źródeł do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="2fe5a-121">Jeśli skonfigurowano hello HDInsight klastra toouse Data Lake Store jako dodatkowego magazynu, hello narzędzia Distcp narzędzie może być używane poza pole toocopy tooand danych z na koncie usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="2fe5a-122">W tej sekcji opisano, jak toouse hello narzędzia Distcp narzędzia.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="2fe5a-123">Z pulpitu Użyj klastra toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="2fe5a-124">Zobacz [Connect tooa opartych na systemie Linux klaster usługi HDInsight](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2fe5a-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="2fe5a-125">Uruchom polecenia hello z hello SSH wiersza.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="2fe5a-126">Sprawdź, czy można uzyskać dostęp do hello Azure blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="2fe5a-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="2fe5a-127">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2fe5a-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="2fe5a-128">To powinien zawierać listę zawartości obiektu blob magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="2fe5a-129">Podobnie należy sprawdzić, czy mają dostęp do konta usługi Data Lake Store hello z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="2fe5a-130">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2fe5a-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="2fe5a-131">To powinien zawierać listę plików/folderów w hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="2fe5a-132">Użyj narzędzia Distcp toocopy danych z tooa WASB konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="2fe5a-133">Spowoduje to skopiowanie zawartości hello hello **/przykład/data/gutenberg/** folderu w WASB zbyt**/myfolder** w hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="2fe5a-134">Podobnie Użyj narzędzia Distcp toocopy danych z tooWASB konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="2fe5a-135">Spowoduje to skopiowanie zawartości hello **/myfolder** w hello usługi Data Lake Store za konta**/przykład/data/gutenberg/** folderu w WASB.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="2fe5a-136">Zagadnienia dotyczące wydajności podczas korzystania z narzędzia DistCp</span><span class="sxs-lookup"><span data-stu-id="2fe5a-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="2fe5a-137">Ponieważ narzędzia DistCp obiektu najniższy poziom szczegółowości pojedynczy plik, najważniejszych toooptimize parametru hello jest ustawienie hello maksymalną liczbę jednoczesnych kopii go przed usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="2fe5a-138">Jest to kontrolowane przez ustawienie hello liczby mapowań ('M ') parametr hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="2fe5a-139">Ten parametr określa maksymalną liczbę mapowań, które będą używane toocopy danych hello.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="2fe5a-140">Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-140">Default value is 20.</span></span>

<span data-ttu-id="2fe5a-141">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="2fe5a-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="2fe5a-142">Jak ustalić liczbę hello toouse mapowań?</span><span class="sxs-lookup"><span data-stu-id="2fe5a-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="2fe5a-143">Oto kilka użytecznych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="2fe5a-144">**Krok 1: Określanie pamięć YARN** -hello pierwszym krokiem jest gdy zostanie uruchomione zadanie narzędzia DistCp hello toodetermine hello YARN pamięci toohello dostępności klastra.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="2fe5a-145">Te informacje są dostępne w portalu Ambari hello skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="2fe5a-146">Nawigacja tooYARN i wyświetlanie hello Configs kartę toosee hello YARN pamięci.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="2fe5a-147">tooget hello YARN pamięć, mnożenie hello YARN ilość pamięci na węzeł z hello liczba węzłów się, że masz w klastrze.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="2fe5a-148">**Krok 2: Obliczanie hello liczby mapowań** — Witaj wartość **m** jest równy toohello iloraz pamięć YARN rozdzielonych hello YARN kontenera rozmiar.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="2fe5a-149">Hello YARN informacje o rozmiarze kontenera jest dostępna w hello Ambari również portalu.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="2fe5a-150">Przejdź tooYARN i widoku hello Configs kartę hello rozmiaru kontenera YARN jest wyświetlany w tym oknie.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="2fe5a-151">Witaj tooarrive równości hello liczby mapowań (**m**) jest</span><span class="sxs-lookup"><span data-stu-id="2fe5a-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="2fe5a-152">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="2fe5a-152">**Example**</span></span>

<span data-ttu-id="2fe5a-153">Załóżmy, że masz 4 węzły D14v2s hello klastra oraz chcesz tootransfer 10TB danych z różnych folderach 10.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="2fe5a-154">Zawiera foldery hello różnych ilości danych różni się od hello rozmiary plików w ramach każdego folderu.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="2fe5a-155">Łączna pamięć YARN — z hello portalu Ambari okaże się, że hello YARN pamięci jest 96GB dla węzła D14.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="2fe5a-156">Tak całkowita pamięć YARN 4 węzła klastra jest:</span><span class="sxs-lookup"><span data-stu-id="2fe5a-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="2fe5a-157">Liczba mapowań — od hello portalu Ambari, można określić tego rozmiaru kontenera YARN hello jest 3072 D14 węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="2fe5a-158">Tak liczba mapowań to:</span><span class="sxs-lookup"><span data-stu-id="2fe5a-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="2fe5a-159">Jeśli inne aplikacje korzystają z pamięci, następnie możesz wybrać Użyj tooonly część klastra YARN pamięci narzędzia DistCp.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="2fe5a-160">Kopiowanie dużych zestawów danych</span><span class="sxs-lookup"><span data-stu-id="2fe5a-160">Copying large datasets</span></span>

<span data-ttu-id="2fe5a-161">Po przeniesieniu hello rozmiar hello toobe zestawu danych jest bardzo duże (np. > 1TB) lub jeśli masz wiele różnych folderach, należy rozważyć użycie wielu zadań narzędzia DistCp.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="2fe5a-162">Nie jest prawdopodobnie nie są bardziej wydajne, ale będzie rozkładu limit hello zadania, aby w przypadku niepowodzenia wszystkie zadania wystarczy toorestart tego określonego zadania, a nie całego zadania hello.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="2fe5a-163">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="2fe5a-163">Limitations</span></span>

* <span data-ttu-id="2fe5a-164">Narzędzia DistCp próbuje mapowań toocreate, podobne rozmiar toooptimize wydajności.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="2fe5a-165">Zwiększenie liczby hello mapowań może nie zawsze zwiększyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="2fe5a-166">Narzędzia DistCp jest ograniczona tooonly jeden mapowania na plik.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="2fe5a-167">W związku z tym nie powinna mieć mapowań więcej niż liczba kupionych plików.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="2fe5a-168">Ponieważ narzędzia DistCp można przypisać tylko jednego mapowania tooa pliku, ogranicza ilość hello współbieżności, które mogą być używane toocopy dużych plików.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="2fe5a-169">Jeśli masz niewielką liczbę dużych plików, a następnie należy rozdzielić je do 256MB pliku fragmentów toogive możesz więcej potencjalnych współbieżności.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="2fe5a-170">Jeśli kopiujesz z konta magazynu obiektów Blob Azure, zadanie kopiowania może ograniczony po stronie magazynu obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="2fe5a-171">To spowoduje zmniejszenie wydajności hello zadania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2fe5a-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="2fe5a-172">toolearn więcej informacji na temat limitów hello magazynu obiektów Blob Azure, zobacz limity magazynu Azure w [subskrypcji platformy Azure i ograniczenia usługi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2fe5a-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2fe5a-173">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2fe5a-173">See also</span></span>
* [<span data-ttu-id="2fe5a-174">Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="2fe5a-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="2fe5a-175">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2fe5a-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2fe5a-176">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2fe5a-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2fe5a-177">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2fe5a-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
