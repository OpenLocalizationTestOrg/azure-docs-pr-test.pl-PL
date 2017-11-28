---
title: "Azure rozwiązań magazynów na potrzeby R Server w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat magazynu różne opcje dostępne dla użytkowników z serwerem R w usłudze HDInsight"
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="57bd9-103">Azure rozwiązań magazynów na potrzeby R Server w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="57bd9-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="57bd9-104">Microsoft R Server w usłudze HDInsight zawiera różnych rozwiązań magazynu do utrwalenia danych, kodu lub obiektów zawierających wyniki analizy.</span><span class="sxs-lookup"><span data-stu-id="57bd9-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="57bd9-105">Należą do nich następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="57bd9-105">These include the following options:</span></span>

- [<span data-ttu-id="57bd9-106">Obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="57bd9-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="57bd9-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="57bd9-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="57bd9-108">Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="57bd9-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="57bd9-109">Istnieje również możliwość uzyskiwania dostępu do wielu kont magazynu Azure lub kontenery z klastra HDI.</span><span class="sxs-lookup"><span data-stu-id="57bd9-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="57bd9-110">Magazyn plików Azure to wygodny danych opcji magazynu do użycia na węzeł krawędzi, który umożliwia zainstalowanie udziału plików magazynu Azure, na przykład system plików systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="57bd9-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="57bd9-111">Jednak udziały plików platformy Azure można zainstalować i używane przez system z obsługiwane systemy operacyjne, takie jak Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="57bd9-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="57bd9-112">Podczas tworzenia klastra usługi Hadoop w usłudze HDInsight, należy określić albo **magazynu Azure** konta lub **Data Lake store**.</span><span class="sxs-lookup"><span data-stu-id="57bd9-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="57bd9-113">Z tego konta kontener magazynu określonych przechowuje systemu plików dla klastra, który można utworzyć (na przykład rozproszonego systemu plików Hadoop).</span><span class="sxs-lookup"><span data-stu-id="57bd9-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="57bd9-114">Aby uzyskać więcej informacji i wskazówek zobacz:</span><span class="sxs-lookup"><span data-stu-id="57bd9-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="57bd9-115">Użyj magazynu platformy Azure z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="57bd9-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="57bd9-116">[Użyj Data Lake Store z usługą Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="57bd9-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="57bd9-117">Aby uzyskać więcej informacji na temat rozwiązań magazynu Azure, zobacz [wprowadzenie do usługi Microsoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57bd9-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="57bd9-118">Aby uzyskać wskazówki dotyczące wybierania najbardziej odpowiedniej opcji magazynu do użycia na potrzeby danego scenariusza, zobacz [decydowania, kiedy używać obiektów blob Azure, Azure pliki i dyski danych Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="57bd9-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="57bd9-119">Używanie kont magazynu obiektów Blob platformy Azure z serwerem R</span><span class="sxs-lookup"><span data-stu-id="57bd9-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="57bd9-120">W razie potrzeby mogą otwierać wiele kont magazynu Azure lub kontenery z klastra HDI.</span><span class="sxs-lookup"><span data-stu-id="57bd9-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="57bd9-121">Aby to zrobić, należy określić dodatkowe konta magazynu w interfejsie użytkownika, podczas tworzenia klastra, a następnie wykonaj następujące kroki, aby można było ich używać z serwerem R.</span><span class="sxs-lookup"><span data-stu-id="57bd9-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="57bd9-122">Ze względów wydajnościowych klastra usługi HDInsight jest tworzony w tym samym centrum danych, co konto magazynu podstawowego, który określisz.</span><span class="sxs-lookup"><span data-stu-id="57bd9-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="57bd9-123">Używanie konta magazynu w innej lokalizacji niż klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="57bd9-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="57bd9-124">Tworzenie klastra usługi HDInsight przy użyciu nazwy konta magazynu **storage1** i domyślny kontener o nazwie **container1**.</span><span class="sxs-lookup"><span data-stu-id="57bd9-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="57bd9-125">Określ konto dodatkowego magazynu o nazwie **storage2**.</span><span class="sxs-lookup"><span data-stu-id="57bd9-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="57bd9-126">Skopiuj plik mycsv.csv do katalogu/share i przeprowadzania analizy dla tego pliku.</span><span class="sxs-lookup"><span data-stu-id="57bd9-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="57bd9-127">W kodzie języka R ustawioną nazwę węzła **domyślnie** i Ustaw użytkownika katalogów i plików do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="57bd9-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="57bd9-128">Wszystkie odwołania katalogów i plików wskaż konta magazynu wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="57bd9-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="57bd9-129">Jest to **domyślne konto magazynu** który jest skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57bd9-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="57bd9-130">Załóżmy, że chcesz przetworzyć pliku o nazwie mySpecial.csv, który znajduje się w /private katalog **container2** w **storage2**.</span><span class="sxs-lookup"><span data-stu-id="57bd9-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="57bd9-131">W kodzie języka R punkt nazwa węzła odwołania do **storage2** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="57bd9-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="57bd9-132">Wszystkie odwołania do plików i katalogów wskazywać konto magazynu wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="57bd9-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="57bd9-133">Jest to **nazwa węzła** , który został określony.</span><span class="sxs-lookup"><span data-stu-id="57bd9-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="57bd9-134">Należy skonfigurować User/RevoShare/<SSH username> katalogu na **storage2** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="57bd9-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="57bd9-135">Używanie usługi Azure Data Lake store z serwerem R</span><span class="sxs-lookup"><span data-stu-id="57bd9-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="57bd9-136">W celu używania usługi Data Lake magazynów z Twoim kontem usługi HDInsight, należy zapewnić dostęp do sieci klastra do każdego Azure Data Lake store, którego chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="57bd9-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="57bd9-137">Aby uzyskać instrukcje dotyczące sposobu tworzenia klastra usługi HDInsight przy użyciu konta usługi Azure Data Lake Store jako domyślnego magazynu lub dodatkowego magazynu za pomocą portalu Azure, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store za pomocą portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="57bd9-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="57bd9-138">Następnie należy użyć magazynu w skrypcie R znacznie jak konto magazynu Azure dodatkowej zgodnie z opisem w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="57bd9-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="57bd9-139">Dodaj klaster dostęp do usługi Azure Data Lake sklepach</span><span class="sxs-lookup"><span data-stu-id="57bd9-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="57bd9-140">Data Lake store jest dostęp przy użyciu nazwy głównej usługi Azure Active Directory (Azure AD), który został skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57bd9-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="57bd9-141">Aby dodać nazwy głównej usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="57bd9-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="57bd9-142">Podczas tworzenia klastra usługi HDInsight, wybierz **tożsamość usługi AAD klastra** z **źródła danych** kartę.</span><span class="sxs-lookup"><span data-stu-id="57bd9-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="57bd9-143">W **tożsamość usługi AAD klastra** okna dialogowego, w obszarze **wybierz jednostkę usługi AD**, wybierz pozycję **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="57bd9-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="57bd9-144">Po nadaj nazwę główną usługi i Utwórz hasło dla niego kliknij **zarządzać dostępem ADLS** do skojarzenia z sklepach usługi Data Lake nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="57bd9-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="57bd9-145">Istnieje również możliwość można dodać jeden lub więcej sklepów usługi Data Lake po utworzeniu klastra dostępu do klastra.</span><span class="sxs-lookup"><span data-stu-id="57bd9-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="57bd9-146">Otwórz pozycję portalu Azure Data Lake store i przejdź do **Eksploratora danych > dostępu > Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="57bd9-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="57bd9-147">Jak uzyskać dostęp z serwera R Data Lake store</span><span class="sxs-lookup"><span data-stu-id="57bd9-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="57bd9-148">Po został przez Ciebie udzielony dostęp do magazynu usługi Data Lake, używając magazynu w R Server w usłudze HDInsight sposób, w jaki konto magazynu Azure dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="57bd9-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="57bd9-149">Jedyną różnicą jest to, że prefiks **wasb: / /** zmienia się na **adl: / /** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="57bd9-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="57bd9-150">Następujące polecenia są używane do konfigurowania konta usługi Data Lake magazynu z katalogiem RevoShare i dodać przykładowy plik CSV z poprzedniego przykładu:</span><span class="sxs-lookup"><span data-stu-id="57bd9-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="57bd9-151">Użyj usługi Magazyn plików Azure z serwerem R</span><span class="sxs-lookup"><span data-stu-id="57bd9-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="57bd9-152">Istnieje również wygodne danych opcji magazynu do użycia na węzeł krawędzi, o nazwie — Azure plików ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="57bd9-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="57bd9-153">Umożliwia instalowanie udziału plików magazynu Azure w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="57bd9-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="57bd9-154">Ta opcja może być przydatna do przechowywania plików danych, skrypty języka R i obiektów wynikowych, które mogą być wymagane później, szczególnie w przypadku warto system plików natywnych węzła krawędzi zamiast systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="57bd9-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="57bd9-155">Główną zaletą usługi pliki Azure jest udziały plików może być zainstalowane i używane przez system z obsługiwane systemy operacyjne, takie jak Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="57bd9-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="57bd9-156">Na przykład można używany przez inny klaster usługi HDInsight, który użytkownik lub inna w zespole ma, maszyny Wirtualnej platformy Azure lub nawet przez system lokalny.</span><span class="sxs-lookup"><span data-stu-id="57bd9-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="57bd9-157">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="57bd9-157">For more information, see:</span></span>

- [<span data-ttu-id="57bd9-158">Jak używać usługi Azure File Storage z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="57bd9-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="57bd9-159">Jak używać magazynu plików Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="57bd9-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="57bd9-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57bd9-160">Next steps</span></span>

<span data-ttu-id="57bd9-161">Po zapoznaniu się z opcji magazynu Azure, użyj następujących łączy odkrywanie sposobów uzyskiwania zadania nauki danych odbywa się za pomocą R Server w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57bd9-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="57bd9-162">Omówienie R Server w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="57bd9-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="57bd9-163">Rozpoczynanie pracy z serwerem R na platformie Hadoop</span><span class="sxs-lookup"><span data-stu-id="57bd9-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="57bd9-164">Dodaj serwer programu RStudio do HDInsight (Jeśli nie dodano podczas tworzenia klastra)</span><span class="sxs-lookup"><span data-stu-id="57bd9-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* <span data-ttu-id="57bd9-165">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="57bd9-165">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)</span></span>

