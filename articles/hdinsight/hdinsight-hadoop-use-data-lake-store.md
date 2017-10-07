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
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Korzystanie z usługi Data Lake Store w połączeniu z klastrami usługi Azure HDInsight

dane tooanalyze w klastrze usługi HDInsight, dane można przechowywać na powitania albo w [usługi Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), lub obie. Obie te opcje magazynu Włącz toosafely usunąć klastrów usługi HDInsight używane do obliczeń bez utraty danych użytkownika.

W tym artykule omówiono współdziałanie usługi Data Lake Store z klastrami usługi HDInsight. toolearn magazynu Azure współpracuje z klastrami HDInsight, zobacz [użycia usługi Azure Storage z usługą Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md). Więcej informacji dotyczących tworzenia klastra usługi HDInsight można znaleźć w artykule [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów platformy Hadoop w usłudze HDInsight).

> [!NOTE]
> Usługa Data Lake Store jest dostępna wyłącznie przez zabezpieczony kanał, dlatego nazwa schematu systemu plików `adls` nie jest używana. Zawsze używaj nazwy `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Dostępność klastrów usługi HDInsight

Platforma Hadoop obsługuje pojęcie domyślnego systemu plików hello. system plików domyślne Hello wyznacza domyślny schemat i urząd. Można także używane tooresolve ścieżek względnych. Podczas procesu tworzenia klastra usługi HDInsight hello, można określić kontenera obiektów blob w magazynie Azure jako hello domyślny system plików lub HDInsight 3.5 i nowszych wersji, można wybrać magazyn Azure lub usługi Azure Data Lake Store jako system plików domyślne hello z kilka wyjątków. 

Klastry usługi HDInsight mogą używać usługi Data Lake Store na dwa sposoby:

* Jako hello domyślny magazyn
* Jako magazyn dodatkowy z rozszerzeniem Azure Storage Blob jako magazynem domyślnym

Od tej chwili tylko niektóre hello HDInsight klastra obsługi typów/wersji przy użyciu usługi Data Lake Store jako domyślnego magazynu i dodatkowych kont magazynu:

| Typ klastra usługi HDInsight | Usługa Data Lake Store jako magazyn domyślny | Usługa Data Lake Store jako magazyn dodatkowy| Uwagi |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight w wersji 3.6 | Tak | Tak | |
| HDInsight w wersji 3.5 | Tak | Tak | Z wyjątkiem hello HBase|
| HDInsight w wersji 3.4 | Nie | Tak | |
| HDInsight w wersji 3.3 | Nie | Nie | |
| HDInsight w wersji 3.2 | Nie | Tak | |
| HDInsight Premium (warstwa)| Nie | Nie | |
| Storm | | |Data Lake Store toowrite danych można użyć od topologii Storm. Usługi Data Lake Store można również używać do obsługi danych referencyjnych, które następnie mogą być odczytywane przez topologię Storm.|

Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpłynąć na wydajność lub tooread możliwości hello lub zapis tooAzure magazynu z klastra hello.


## <a name="use-data-lake-store-as-default-storage"></a>Używanie usługi Data Lake Store jako magazynu domyślnego

Po wdrożeniu usługi HDInsight z usługą Data Lake Store jako domyślny magazyn plików związanych z klastrem hello są przechowywane w usłudze Data Lake Store w hello w następującej lokalizacji:

    adl://mydatalakestore/<cluster_root_path>/

gdzie `<cluster_root_path>` jest nazwą hello folderu utworzyć w usłudze Data Lake Store. Określ ścieżkę katalogu głównego dla każdego klastra, można użyć hello tego samego konta usługi Data Lake Store dla więcej niż jednego klastra. Dlatego jest możliwa następująca konfiguracja:

* Klaster1 można użyć ścieżki hello`adl://mydatalakestore/cluster1storage`
* Cluster2 można użyć ścieżki hello`adl://mydatalakestore/cluster2storage`

Powiadomienie zarówno tekst hello Użyj klastrów hello same konta usługi Data Lake Store **mydatalakestore**. Każdy klaster ma własny system plików głównego w usłudze Data Lake Store tooits dostępu. Witaj środowisko wdrażania portalu Azure w szczególności monit toouse nazwę folderu takich jak **/clusters/\<clustername >** hello ścieżki katalogu głównego.

toobe stanie toouse usługi Data Lake Store jako domyślny magazyn, należy udzielić toohello główna dostępu usługi hello następującej ścieżki:

- Witaj głównego konta usługi Data Lake Store.  na przykład: adl://mydatalakestore/.
- folder Hello wszystkie foldery klastra.  na przykład: adl://mydatalakestore/clusters.
- folder Hello hello klastra.  na przykład: adl://mydatalakestore/clusters/cluster1storage.

Aby uzyskać więcej informacji na temat tworzenia jednostki usługi i przyznawania dostępu, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Używanie usługi Data Lake Store jako magazynu dodatkowego

Data Lake Store jako dodatkowego miejsca do magazynowania służy również hello klastra. W takich przypadkach hello klastra domyślny magazyn może być obiektu Blob magazynu Azure lub konto usługi Data Lake Store. Jeśli używasz zadań HDInsight hello danych przechowywanych w usłudze Data Lake Store jako dodatkowego magazynu, należy użyć hello w pełni kwalifikowaną ścieżkę toohello plików. Na przykład:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Należy pamiętać, że ma nie **cluster_root_path** hello teraz adres URL. Wynika usługi Data Lake Store nie jest magazynu domyślną w tym przypadku więc toodo wystarczy zapewnić hello ścieżki toohello pliki.

toobe stanie toouse usługi Data Lake Store jako dodatkowego magazynu, tylko potrzebne toogrant hello usługi głównej dostępu toohello ścieżki gdzie są przechowywane pliki.  Na przykład:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Aby uzyskać więcej informacji na temat tworzenia jednostki usługi i przyznawania dostępu, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Używanie wielu kont usługi Data Lake Store

Dodanie konta usługi Data Lake Store jako dodatkowego i dodanie więcej niż jednej usługi Data Lake Store konta są realizowane przez nadanie uprawnień klastra usługi HDInsight hello na danych w jednej lub więcej kont usługi Data Lake Store. Zobacz [Konfigurowanie dostępu do usługi Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Konfigurowanie dostępu do usługi Data Lake Store

tooconfigure Data Lake dostęp do sklepu z klastrem usługi HDInsight, musi mieć usługi Azure Active directory (Azure AD) nazwy głównej usługi. Tylko administrator usługi Azure AD może utworzyć jednostkę usługi. nazwy głównej usługi Hello musi zostać utworzony przy użyciu certyfikatu. Aby uzyskać więcej informacji, zobacz [Konfigurowanie dostępu do usługi Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) i [Create service principal with self-signed-certificate (Tworzenie jednostki usługi przy użyciu certyfikatu z podpisem własnym)](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Jeśli zamierzasz toouse Azure Data Lake Store jako dodatkowego magazynu dla klastra usługi HDInsight, zdecydowanie zaleca się to zrobić podczas tworzenia klastra hello zgodnie z opisem w tym artykule. Dodawanie usługi Azure Data Lake Store jako dodatkowego magazynu tooan istniejącym klastrze usługi HDInsight to skomplikowany proces i tooerrors podatnych na błędy.
>

## <a name="access-files-from-hello-cluster"></a>Uzyskiwanie dostępu do plików z hello klastra

Istnieje kilka sposobów dostępne pliki hello w usłudze Data Lake Store z klastra usługi HDInsight.

* **Przy użyciu w pełni kwalifikowana nazwa hello**. Z tej metody, podaj hello pełną ścieżkę toohello plików, które mają tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Przy użyciu formatu ścieżki skróconą hello**. Z tej metody można zastąpić ścieżki hello zapasowej głównego klastra toohello adl: / / /. Dlatego w powyższym przykładzie hello, musisz zastąpić `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` z `adl:///`.

        adl:///<file path>

* **Za pomocą ścieżki względnej hello**. Z tej metody, tylko podać hello ścieżki względnej toohello plików, które mają tooaccess. Na przykład, jeśli plik toohello pełną ścieżkę hello jest:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Dostęp można uzyskać hello przy użyciu tej ścieżki względnej zamiast tego samego pliku sample.log.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Tworzenie klastrów usługi HDInsight na uzyskiwanie dostępu do tooData Lake — Magazyn

Użyj następującego łącza, aby uzyskać szczegółowe instrukcje na jak toocreate, który klastrów usługi HDInsight z dostępu do magazynu Lake tooData hello.

* [Korzystanie z portalu](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [HDInsight with Data Lake Store as default storage - PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md) (Usługa HDInsight z usługą Data Lake Store jako magazynem domyślnym — PowerShell)
* [Using PowerShell (with Data Lake Store as additional storage)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md) (Korzystanie z programu PowerShell z usługą Data Lake Store jako magazynem dodatkowym)
* [Korzystanie z szablonów platformy Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Następne kroki
W tym artykule należy przedstawiono sposób toouse zgodnego systemem plików HDFS Azure Data Lake Store z usługą HDInsight. Dzięki temu można toobuild skalowalnych, długoterminowych, archiwizacji rozwiązań do pozyskiwania danych i użyj HDInsight toounlock hello informacji wewnątrz hello przechowywane strukturalnych i danych bez struktury.

Aby uzyskać więcej informacji, zobacz:

* [Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]
* [Wprowadzenie do usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Korzystanie z usługą HDInsight toodata dostępu toorestrict sygnatury dostępu współdzielonego magazynu Azure][hdinsight-use-sas]

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
