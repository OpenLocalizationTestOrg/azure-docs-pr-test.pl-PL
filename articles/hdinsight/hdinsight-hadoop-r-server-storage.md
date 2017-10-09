---
title: "aaaAzure rozwiązań magazynów na potrzeby R Server w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toousers dostępne opcje magazynu innego hello z serwerem R w usłudze HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="da6f0-103">Azure rozwiązań magazynów na potrzeby R Server w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="da6f0-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="da6f0-104">Microsoft R Server w usłudze HDInsight zawiera różnych danych toopersist rozwiązań magazynu, kodu lub obiektów zawierających wyniki analizy.</span><span class="sxs-lookup"><span data-stu-id="da6f0-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="da6f0-105">Obejmują one hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="da6f0-105">These include hello following options:</span></span>

- [<span data-ttu-id="da6f0-106">Obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="da6f0-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="da6f0-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="da6f0-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="da6f0-108">Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="da6f0-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="da6f0-109">Istnieje również opcja hello uzyskiwania dostępu do wielu kont magazynu Azure lub kontenery z klastra HDI.</span><span class="sxs-lookup"><span data-stu-id="da6f0-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="da6f0-110">Magazyn plików Azure to wygodny danych opcji magazynu do użycia na powitania węzeł krawędzi, który pozwala toomount udziału plików magazynu Azure do, na przykład hello systemu plików systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="da6f0-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="da6f0-111">Jednak udziały plików platformy Azure można zainstalować i używane przez system z obsługiwane systemy operacyjne, takie jak Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="da6f0-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="da6f0-112">Podczas tworzenia klastra usługi Hadoop w usłudze HDInsight, należy określić albo **magazynu Azure** konta lub **Data Lake store**.</span><span class="sxs-lookup"><span data-stu-id="da6f0-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="da6f0-113">Z tego konta kontener magazynu określonych przechowuje hello systemu plików dla klastra hello utworzyć (na przykład hello rozproszonego systemu plików Hadoop).</span><span class="sxs-lookup"><span data-stu-id="da6f0-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="da6f0-114">Aby uzyskać więcej informacji i wskazówek zobacz:</span><span class="sxs-lookup"><span data-stu-id="da6f0-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="da6f0-115">Użyj magazynu platformy Azure z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="da6f0-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="da6f0-116">[Użyj Data Lake Store z usługą Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="da6f0-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="da6f0-117">Aby uzyskać więcej informacji na temat rozwiązań magazynu Azure hello, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da6f0-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="da6f0-118">Aby uzyskać wskazówki dotyczące wybierania hello najbardziej odpowiedni magazyn opcja toouse dla danego scenariusza, zobacz [Deciding podczas obiektów blob Azure toouse, pliki Azure lub dyski danych Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="da6f0-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="da6f0-119">Używanie kont magazynu obiektów Blob platformy Azure z serwerem R</span><span class="sxs-lookup"><span data-stu-id="da6f0-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="da6f0-120">W razie potrzeby mogą otwierać wiele kont magazynu Azure lub kontenery z klastra HDI.</span><span class="sxs-lookup"><span data-stu-id="da6f0-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="da6f0-121">toodo, należy więc toospecify hello dodatkowych kont magazynu w hello interfejsu użytkownika podczas tworzenia klastra hello, a następnie wykonaj te kroki toouse je z serwerem R.</span><span class="sxs-lookup"><span data-stu-id="da6f0-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="da6f0-122">Ze względów wydajnościowych klastra usługi HDInsight hello jest tworzony w hello sam centrum danych, co konto magazynu podstawowego hello, który określisz.</span><span class="sxs-lookup"><span data-stu-id="da6f0-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="da6f0-123">Używanie konta magazynu w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="da6f0-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="da6f0-124">Tworzenie klastra usługi HDInsight przy użyciu nazwy konta magazynu **storage1** i domyślny kontener o nazwie **container1**.</span><span class="sxs-lookup"><span data-stu-id="da6f0-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="da6f0-125">Określ konto dodatkowego magazynu o nazwie **storage2**.</span><span class="sxs-lookup"><span data-stu-id="da6f0-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="da6f0-126">Skopiuj hello mycsv.csv pliku toohello/share katalogu i przeprowadzania analizy dla tego pliku.</span><span class="sxs-lookup"><span data-stu-id="da6f0-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="da6f0-127">W kodzie języka R, ustawić hello nazwa węzła także**domyślnie** i ustaw tooprocess Twojego katalogu i pliku.</span><span class="sxs-lookup"><span data-stu-id="da6f0-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="da6f0-128">Witaj wszystkich katalogów i plików odwołuje się do konta magazynu toohello punktu wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="da6f0-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="da6f0-129">Jest to hello **domyślne konto magazynu** który jest skojarzony z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="da6f0-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="da6f0-130">Teraz załóżmy, że chcesz tooprocess pliku o nazwie mySpecial.csv, który znajduje się w hello /private katalog **container2** w **storage2**.</span><span class="sxs-lookup"><span data-stu-id="da6f0-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="da6f0-131">W kodzie języka R punkt hello nazwa węzła odniesienia toohello **storage2** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="da6f0-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="da6f0-132">Wszystkie hello katalogów i plików odwołań teraz toohello punktu konta magazynu wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="da6f0-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="da6f0-133">Jest to hello **nazwa węzła** , który został określony.</span><span class="sxs-lookup"><span data-stu-id="da6f0-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="da6f0-134">Masz tooconfigure hello/User/RevoShare/<SSH username> katalogu na **storage2** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da6f0-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="da6f0-135">Używanie usługi Azure Data Lake store z serwerem R</span><span class="sxs-lookup"><span data-stu-id="da6f0-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="da6f0-136">toouse Data Lake przechowuje z Twoim kontem usługi HDInsight, należy toogive sklepu usługi Azure Data Lake tooeach dostępu do klastra, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="da6f0-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="da6f0-137">Aby uzyskać instrukcje dotyczące sposobu toouse hello toocreate portalu Azure HDInsight dla klastra przy użyciu konta usługi Azure Data Lake Store jako hello domyślny magazyn lub jako dodatkowy magazyn, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store za pomocą portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="da6f0-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="da6f0-138">Następnie należy użyć magazynu hello w skrypcie R znacznie jak konto magazynu Azure dodatkowej zgodnie z opisem w poprzedniej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="da6f0-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="da6f0-139">Dodaj tooyour dostępu do klastra, który przechowuje usługi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="da6f0-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="da6f0-140">Data Lake store jest dostęp przy użyciu nazwy głównej usługi Azure Active Directory (Azure AD), który został skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da6f0-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="da6f0-141">tooadd nazwy głównej usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="da6f0-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="da6f0-142">Podczas tworzenia klastra usługi HDInsight, wybierz **tożsamość usługi AAD klastra** z hello **źródła danych** kartę.</span><span class="sxs-lookup"><span data-stu-id="da6f0-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="da6f0-143">W hello **tożsamość usługi AAD klastra** okna dialogowego, w obszarze **wybierz jednostkę usługi AD**, wybierz pozycję **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="da6f0-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="da6f0-144">Po nadaj nazwę hello nazwy głównej usługi i Utwórz hasło dla niego kliknij **zarządzać dostępem ADLS** hello tooassociate przechowuje nazwy głównej usługi z Twojej usługi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da6f0-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="da6f0-145">Możliwe jest również możliwe tooadd klastra dostępu tooone lub więcej usługi Data Lake przechowuje po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="da6f0-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="da6f0-146">Otwórz hello wpis portalu Azure Data Lake store i za Przejdź**Eksploratora danych > dostępu > Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="da6f0-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="da6f0-147">Jak tooaccess hello Data Lake store z serwera R</span><span class="sxs-lookup"><span data-stu-id="da6f0-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="da6f0-148">Po którym został przyznany dostęp tooa Data Lake store, można użyć magazynu hello w R Server w HDInsight hello sposób, w jaki konto magazynu Azure dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="da6f0-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="da6f0-149">Witaj tylko różnicą jest to, że prefiks hello **wasb: / /** zmiany zbyt**adl: / /** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da6f0-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="da6f0-150">Witaj następujące polecenia są hello tooconfigure używane konto usługi Data Lake magazynu z katalogu RevoShare hello i dodać hello przykładowy plik CSV z poprzedniego przykładu hello:</span><span class="sxs-lookup"><span data-stu-id="da6f0-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="da6f0-151">Użyj usługi Magazyn plików Azure z serwerem R</span><span class="sxs-lookup"><span data-stu-id="da6f0-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="da6f0-152">Istnieje również wygodne danych opcji magazynu do użycia na powitania krawędzi węzeł o nazwie — Azure plików ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="da6f0-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="da6f0-153">Umożliwia toomount toohello udziału pliku magazynu Azure systemu plików w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="da6f0-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="da6f0-154">Ta opcja może być przydatna do przechowywania plików danych, skrypty języka R i obiektów wynikowych, które mogą być wymagane później, szczególnie w przypadku ułatwia wykrywanie toouse hello macierzysty system plików na węzeł brzegowy hello zamiast systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="da6f0-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="da6f0-155">Główną zaletą usługi pliki Azure jest ten plik hello udziały mogą być zainstalowane i używane przez system z obsługiwane systemy operacyjne, takie jak Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="da6f0-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="da6f0-156">Na przykład można używany przez inny klaster usługi HDInsight, który użytkownik lub inna w zespole ma, maszyny Wirtualnej platformy Azure lub nawet przez system lokalny.</span><span class="sxs-lookup"><span data-stu-id="da6f0-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="da6f0-157">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="da6f0-157">For more information, see:</span></span>

- [<span data-ttu-id="da6f0-158">Jak toouse magazyn plików Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="da6f0-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="da6f0-159">Jak toouse magazyn plików Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="da6f0-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="da6f0-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da6f0-160">Next steps</span></span>

<span data-ttu-id="da6f0-161">Teraz, gdy opcje magazynu Azure hello zrozumiałe, użyj następujących hello łączy toodiscover sposobów uzyskiwania zadania nauki danych odbywa się za pomocą R Server w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da6f0-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="da6f0-162">Omówienie R Server w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="da6f0-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="da6f0-163">Rozpoczynanie pracy z serwerem R na platformie Hadoop</span><span class="sxs-lookup"><span data-stu-id="da6f0-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="da6f0-164">Dodaj serwer programu RStudio tooHDInsight (Jeśli nie dodano podczas tworzenia klastra)</span><span class="sxs-lookup"><span data-stu-id="da6f0-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* <span data-ttu-id="da6f0-165">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="da6f0-165">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)</span></span>

