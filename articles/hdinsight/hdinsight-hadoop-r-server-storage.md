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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Azure rozwiązań magazynów na potrzeby R Server w usłudze HDInsight

Microsoft R Server w usłudze HDInsight zawiera różnych danych toopersist rozwiązań magazynu, kodu lub obiektów zawierających wyniki analizy. Obejmują one hello następujące opcje:

- [Obiektów Blob platformy Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/)
- [Magazyn plików Azure](https://azure.microsoft.com/services/storage/files/)

Istnieje również opcja hello uzyskiwania dostępu do wielu kont magazynu Azure lub kontenery z klastra HDI. Magazyn plików Azure to wygodny danych opcji magazynu do użycia na powitania węzeł krawędzi, który pozwala toomount udziału plików magazynu Azure do, na przykład hello systemu plików systemu Linux. Jednak udziały plików platformy Azure można zainstalować i używane przez system z obsługiwane systemy operacyjne, takie jak Windows lub Linux. 

Podczas tworzenia klastra usługi Hadoop w usłudze HDInsight, należy określić albo **magazynu Azure** konta lub **Data Lake store**. Z tego konta kontener magazynu określonych przechowuje hello systemu plików dla klastra hello utworzyć (na przykład hello rozproszonego systemu plików Hadoop). Aby uzyskać więcej informacji i wskazówek zobacz:

- [Użyj magazynu platformy Azure z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Użyj Data Lake Store z usługą Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md). 

Aby uzyskać więcej informacji na temat rozwiązań magazynu Azure hello, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md). 

Aby uzyskać wskazówki dotyczące wybierania hello najbardziej odpowiedni magazyn opcja toouse dla danego scenariusza, zobacz [Deciding podczas obiektów blob Azure toouse, pliki Azure lub dyski danych Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Używanie kont magazynu obiektów Blob platformy Azure z serwerem R

W razie potrzeby mogą otwierać wiele kont magazynu Azure lub kontenery z klastra HDI. toodo, należy więc toospecify hello dodatkowych kont magazynu w hello interfejsu użytkownika podczas tworzenia klastra hello, a następnie wykonaj te kroki toouse je z serwerem R.

> [!WARNING]
> Ze względów wydajnościowych klastra usługi HDInsight hello jest tworzony w hello sam centrum danych, co konto magazynu podstawowego hello, który określisz. Używanie konta magazynu w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.

1. Tworzenie klastra usługi HDInsight przy użyciu nazwy konta magazynu **storage1** i domyślny kontener o nazwie **container1**.
2. Określ konto dodatkowego magazynu o nazwie **storage2**.  
3. Skopiuj hello mycsv.csv pliku toohello/share katalogu i przeprowadzania analizy dla tego pliku.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. W kodzie języka R, ustawić hello nazwa węzła także**domyślnie** i ustaw tooprocess Twojego katalogu i pliku.  

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

Witaj wszystkich katalogów i plików odwołuje się do konta magazynu toohello punktu wasb://container1@storage1.blob.core.windows.net. Jest to hello **domyślne konto magazynu** który jest skojarzony z klastrem usługi HDInsight hello.

Teraz załóżmy, że chcesz tooprocess pliku o nazwie mySpecial.csv, który znajduje się w hello /private katalog **container2** w **storage2**.

W kodzie języka R punkt hello nazwa węzła odniesienia toohello **storage2** konta magazynu.


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

Wszystkie hello katalogów i plików odwołań teraz toohello punktu konta magazynu wasb://container2@storage2.blob.core.windows.net. Jest to hello **nazwa węzła** , który został określony.

Masz tooconfigure hello/User/RevoShare/<SSH username> katalogu na **storage2** w następujący sposób:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Używanie usługi Azure Data Lake store z serwerem R

toouse Data Lake przechowuje z Twoim kontem usługi HDInsight, należy toogive sklepu usługi Azure Data Lake tooeach dostępu do klastra, które mają toouse. Aby uzyskać instrukcje dotyczące sposobu toouse hello toocreate portalu Azure HDInsight dla klastra przy użyciu konta usługi Azure Data Lake Store jako hello domyślny magazyn lub jako dodatkowy magazyn, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store za pomocą portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Następnie należy użyć magazynu hello w skrypcie R znacznie jak konto magazynu Azure dodatkowej zgodnie z opisem w poprzedniej procedurze hello.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Dodaj tooyour dostępu do klastra, który przechowuje usługi Azure Data Lake
Data Lake store jest dostęp przy użyciu nazwy głównej usługi Azure Active Directory (Azure AD), który został skojarzony z klastrem usługi HDInsight.

tooadd nazwy głównej usługi Azure AD:

1. Podczas tworzenia klastra usługi HDInsight, wybierz **tożsamość usługi AAD klastra** z hello **źródła danych** kartę.

2. W hello **tożsamość usługi AAD klastra** okna dialogowego, w obszarze **wybierz jednostkę usługi AD**, wybierz pozycję **Utwórz nowy**.

Po nadaj nazwę hello nazwy głównej usługi i Utwórz hasło dla niego kliknij **zarządzać dostępem ADLS** hello tooassociate przechowuje nazwy głównej usługi z Twojej usługi Data Lake.

Możliwe jest również możliwe tooadd klastra dostępu tooone lub więcej usługi Data Lake przechowuje po utworzeniu klastra. Otwórz hello wpis portalu Azure Data Lake store i za Przejdź**Eksploratora danych > dostępu > Dodaj**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Jak tooaccess hello Data Lake store z serwera R

Po którym został przyznany dostęp tooa Data Lake store, można użyć magazynu hello w R Server w HDInsight hello sposób, w jaki konto magazynu Azure dodatkowej. Witaj tylko różnicą jest to, że prefiks hello **wasb: / /** zmiany zbyt**adl: / /** w następujący sposób:


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


Witaj następujące polecenia są hello tooconfigure używane konto usługi Data Lake magazynu z katalogu RevoShare hello i dodać hello przykładowy plik CSV z poprzedniego przykładu hello:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Użyj usługi Magazyn plików Azure z serwerem R

Istnieje również wygodne danych opcji magazynu do użycia na powitania krawędzi węzeł o nazwie — Azure plików ((https://azure.microsoft.com/services/storage/files/). Umożliwia toomount toohello udziału pliku magazynu Azure systemu plików w systemie Linux. Ta opcja może być przydatna do przechowywania plików danych, skrypty języka R i obiektów wynikowych, które mogą być wymagane później, szczególnie w przypadku ułatwia wykrywanie toouse hello macierzysty system plików na węzeł brzegowy hello zamiast systemu plików HDFS. 

Główną zaletą usługi pliki Azure jest ten plik hello udziały mogą być zainstalowane i używane przez system z obsługiwane systemy operacyjne, takie jak Windows lub Linux. Na przykład można używany przez inny klaster usługi HDInsight, który użytkownik lub inna w zespole ma, maszyny Wirtualnej platformy Azure lub nawet przez system lokalny. Aby uzyskać więcej informacji, zobacz:

- [Jak toouse magazyn plików Azure z systemem Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Jak toouse magazyn plików Azure w systemie Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Następne kroki

Teraz, gdy opcje magazynu Azure hello zrozumiałe, użyj następujących hello łączy toodiscover sposobów uzyskiwania zadania nauki danych odbywa się za pomocą R Server w usłudze HDInsight.

* [Omówienie R Server w usłudze HDInsight](hdinsight-hadoop-r-server-overview.md)
* [Rozpoczynanie pracy z serwerem R na platformie Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Dodaj serwer programu RStudio tooHDInsight (Jeśli nie dodano podczas tworzenia klastra)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)

