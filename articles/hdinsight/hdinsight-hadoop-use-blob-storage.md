---
title: "aaaQuery danych z systemu plików HDFS zgodnego magazynu Azure - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooquery danych z magazynu Azure i usługi Azure Data Lake Store toostore wyniki analiz."
keywords: blob storage,hdfs,structured data,unstructured data,data lake store,Hadoop input,Hadoop output, hadoop storage, hdfs input,hdfs output,hdfs storage,wasb azure
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Korzystanie z usługi Azure Storage w połączeniu z klastrami usługi Azure HDInsight

dane tooanalyze w klastrze usługi HDInsight, dane można przechowywać hello w usłudze Azure Storage i Azure Data Lake Store. Obie te opcje magazynu Włącz toosafely usunąć klastrów usługi HDInsight używane do obliczeń bez utraty danych użytkownika.

Platforma Hadoop obsługuje pojęcie domyślnego systemu plików hello. system plików domyślne Hello wyznacza domyślny schemat i urząd. Można także używane tooresolve ścieżek względnych. Podczas procesu tworzenia klastra usługi HDInsight hello można określić kontenera obiektów blob w magazynie Azure jako domyślny system plików hello, lub z HDInsight 3.5, można wybrać magazyn Azure lub usługi Azure Data Lake Store jako system plików domyślne hello kilka wyjątków. Aby hello możliwość wykorzystania usługi Data Lake Store jako domyślny hello i magazynu połączone, zobacz [dostępność dla klastra usługi HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

W tym artykule omówiono współdziałanie usługi Azure Storage z klastrami usługi HDInsight. toolearn Data Lake Store współpracuje z klastrami HDInsight, zobacz [użycia usługi Azure Data Lake Store z usługą Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md). Więcej informacji dotyczących tworzenia klastra usługi HDInsight można znaleźć w artykule [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów platformy Hadoop w usłudze HDInsight).

Usługa Azure Storage to niezawodne rozwiązanie ogólnego przeznaczenia, które bezproblemowo integruje się z usługą HDInsight. HDInsight można użyć kontenera obiektów blob w magazynie Azure jako hello domyślnego systemu plików dla klastra hello. Za pomocą interfejsu systemu (HDFS) DFS Hadoop hello pełny zestaw składników usługi HDInsight może operować bezpośrednio na danych strukturalnych lub bez struktury przechowywanych jako obiekty BLOB.

> [!WARNING]
> Podczas tworzenia konta usługi Azure Storage jest dostępnych kilka opcji. Witaj w poniższej tabeli podano informacje, na jakie opcje są obsługiwane z usługą HDInsight:
> 
> | Typ konta magazynu | Warstwa magazynu | Obsługiwane z usługą HDInsight |
> | ------- | ------- | ------- |
> | Konto magazynu ogólnego przeznaczenia | Standardowa | __Tak__ |
> | &nbsp; | Premium | Nie |
> | Konto magazynu obiektów blob | Gorąca | Nie |
> | &nbsp; | Chłodna | Nie |

Nie zaleca się użycie hello domyślnego kontenera obiektów blob do przechowywania danych biznesowych. Usunięcie domyślnego kontenera obiektów blob powitania po każdym tooreduce Użyj przestrzeni magazynowej jest dobrym rozwiązaniem. Uwaga kontenera domyślnego hello zawierającym węzły aplikacji i systemu dzienników. Upewnij się, że tooretrieve hello dzienniki przed usunięciem hello kontenera.

Udostępnianie jednego kontenera obiektów blob dla wielu klastrów nie jest obsługiwane.

## <a name="hdinsight-storage-architecture"></a>Architektura magazynu usługi HDInsight
powitania po diagram zawiera abstrakcyjny widok architektury magazynu usługi HDInsight przy użyciu usługi Azure Storage hello:

![Klastry Hadoop Użyj hello interfejsu API systemu plików HDFS tooaccess i przechowywania danych strukturalnych i bez struktury w magazynie obiektów Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Architektura magazynu usługi HDInsight")

Usługa HDInsight zapewnia dostęp do systemu plików toohello rozproszonych, który jest lokalnie dołączony toohello węzłów obliczeniowych. W tym systemie plików jest możliwy za pomocą hello w pełni kwalifikowana identyfikatora URI, na przykład:

    hdfs://<namenodehost>/<path>

Ponadto HDInsight umożliwia tooaccess danych przechowywanych w usłudze Azure Storage. Składnia Hello jest następująca:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

Poniżej przedstawiono kilka zagadnień dotyczących korzystania z konta usługi Azure Storage w połączeniu z klastrami usługi HDInsight.

* **Kontenery na kontach magazynu hello, które są połączone tooa klastra:** ponieważ hello nazwę konta i klucz są skojarzone z klastrem hello podczas tworzenia, masz pełny dostęp do toohello obiektów blob w tych kontenerach.

* **Publiczne kontenery lub publiczne obiekty BLOB na kontach magazynu, które nie są połączone klastra tooa:** masz uprawnienia tylko do odczytu toohello BLOB w kontenerach hello.
  
  > [!NOTE]
  > Kontenery publiczne pozwalają tooget listę wszystkich obiektów blob, które są dostępne w danym kontenerze oraz pobranie metadanych kontenera. Publiczne obiekty BLOB umożliwiają tooaccess hello blob jedynie osobom znającym dokładny adres URL hello. Aby uzyskać więcej informacji, zobacz <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">ograniczanie dostępu toocontainers i obiekty BLOB</a>.
  > 
  > 
* **Prywatne kontenery na kontach magazynu, które nie są połączone w klaster tooa:** nie masz dostępu do obiektów blob hello w kontenerach hello chyba że zdefiniujesz konto magazynu hello podczas przesyłania zadań WebHCat hello. Wyjaśnienie jest zawarte w dalszej części tego artykułu.

Witaj kontach magazynu, które są definiowane w procesie tworzenia hello i ich kluczy są przechowywane w %HADOOP_HOME%/conf/core-site.xml w węzłach klastra hello. domyślne zachowanie Hello HDInsight jest kont magazynu hello toouse zdefiniowanych w pliku core-site.xml hello. To ustawienie możesz zmodyfikować przy użyciu narzędzia [Ambari](./hdinsight-hadoop-manage-ambari.md)

Wiele zadań WebHCat, w tym Hive, MapReduce, przesyłanie strumieniowe Hadoop, a także Pig, może przenosić ze sobą opis kont magazynu i metadane. (W przypadku technologii Pig obecnie działa to z kontami magazynu, ale nie dla metadanych). Aby uzyskać więcej informacji, zobacz [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Używanie klastra usługi HDInsight z alternatywnymi kontami magazynu i magazynami metadanych).

Obiekty blob mogą być używane z danymi ze strukturą i bez niej. Kontenery obiektów blob przechowują dane jako pary klucz/wartość, bez hierarchii katalogów. Jednak hello znaku ukośnika (/) może być używana w hello toomake nazwa klucza wydaje się tak, jakby plik był przechowywany w ramach struktury katalogów. Na przykład klucz obiektu blob może mieć postać *input/log1.txt*. Nie rzeczywiste *wejściowych* katalog istnieje, ale powodu obecności toohello hello znaku ukośnika w nazwie klucza hello, ma wygląd hello ścieżki do pliku.

## <a id="benefits"></a>Korzyści z usługi Azure Storage
Witaj DOROZUMIANE skuteczność została osłabiona przez hello sposób tworzenia klastrów obliczeniowych hello zasobów konta magazynu zamknij toohello wewnątrz hello regionu Azure, w którym hello szybkie sieci zapewniają koszt wydajności nie wspólnie lokalizowania klastrów obliczeniowych i zasobów magazynowania efektywne dla węzłów obliczeniowych hello tooaccess hello danych wewnątrz magazynu Azure.

Istnieje kilka korzyści związanych z przechowywaniem danych hello w magazynie Azure zamiast systemu plików HDFS:

* **Udostępnianie i ponowne użycie danych:** hello dane w systemie plików HDFS znajdują się wewnątrz klastra obliczeniowego hello. Tylko aplikacji hello, które mają dostęp toohello obliczeń klaster może używać hello danych przy użyciu interfejsów API systemu plików HDFS. Witaj dane w magazynie Azure są dostępne za pośrednictwem interfejsów API systemu plików HDFS hello lub hello [interfejsów API REST magazynu obiektów Blob][blob-storage-restAPI]. W związku z tym większy zestaw narzędzi i aplikacji (w tym inne klastry HDInsight) można tooproduce używane i wykorzystują dane hello.
* **Archiwizacja danych:** przechowywanie danych w magazynie Azure umożliwia hello klastrów usługi HDInsight używane do obliczeń toobe bezpiecznie usunąć bez utraty danych użytkownika.
* **Koszt magazynowania danych:** przechowywania danych w systemie plików DFS długoterminowej hello jest droższe niż przechowywanie danych hello w magazynie Azure, ponieważ hello koszt klastra obliczeniowego jest wyższy niż koszt hello magazynu Azure. Ponadto ponieważ hello danych nie ma toobe ponownie załadowana każdej generacji klastra obliczeniowego, oszczędzamy również koszty ładowania danych.
* **Elastyczne skalowalnego w poziomie:** Chociaż system plików HDFS zapewnia system plików skalowalnych w poziomie, skala hello jest określany przez hello liczbę węzłów tworzonych dla klastra. Zmiana skali hello może stać się procesem bardziej skomplikowane niż polegania na elastyczne hello możliwościami skalowania, które można uzyskać automatycznie w magazynie Azure.
* **Replikacja geograficzna:** usługę Azure Storage można replikować geograficznie. Chociaż zapewnia to odzyskiwanie geograficzne i nadmiarowość danych, lokalizacji zreplikowanych geograficznie trybu failover toohello poważnie wpływa na wydajność i może pociągnąć za sobą dodatkowe koszty. Dlatego zalecamy toochoose hello — replikacja geograficzna rozsądny sposób i tylko wtedy, gdy wartość hello hello danych uzasadnia ponoszenie dodatkowych kosztów hello.

Niektóre zadania i pakiety MapReduce mogą tworzyć wyniki pośrednie, że nie naprawdę chcesz toostore w magazynie Azure. W tym przypadku można wybrać toostore hello danych w hello lokalnego systemu plików HDFS. W rzeczywistości HDInsight używa systemu plików DFS dla wielu wyników pośrednich w zadaniach Hive i innych procesach.

> [!NOTE]
> Większość poleceń systemu plików HDFS (na przykład <b>ls</b>, <b>copyFromLocal</b> i <b>mkdir</b>) nadal działa zgodnie z oczekiwaniami. Tylko hello poleceń, które są określone toohello natywnych implementacji systemu plików HDFS (czyli tooas określonego systemu plików DFS), takich jak <b>fschk</b> i <b>dfsadmin</b>, Pokaż inaczej w magazynie Azure.
> 
> 

## <a name="create-blob-containers"></a>Tworzenie kontenerów obiektów blob
toouse obiektów blob, należy najpierw utworzyć [konta magazynu Azure][azure-storage-create]. W ramach tego możesz określić region platformy Azure, gdzie hello konto magazynu jest tworzone. Witaj klaster i konto magazynu hello musi być obsługiwana przez hello tego samego regionu. Hello Hive potrzeby magazynu metadanych serwera SQL w bazie danych i Oozie potrzeby magazynu metadanych programu SQL Server, bazy danych, również muszą znajdować się w hello tego samego regionu.

Wszędzie tam, gdzie go umieszczono, każdy utworzony obiekt blob należy tooa kontenera na koncie magazynu Azure. Ten kontener może być istniejącym obiektem blob utworzonym poza usługą HDInsight lub może być kontenerem, który jest tworzony dla klastra usługi HDInsight.

Witaj domyślnego kontenera obiektów Blob przechowuje informacje specyficzne dla klastra, takie jak dzienniki i historię zadań. Nie należy współużytkować domyślnego kontenera obiektów blob dla wielu klastrów usługi HDInsight. Może to spowodować uszkodzenie historii zadań. Zalecane jest toouse innego kontenera dla każdego klastra i umieszczanie udostępnionych danych w połączonym koncie magazynu określonym we wdrożeniu wszystkich odpowiednich klastrów zamiast hello domyślne konto magazynu. Aby uzyskać więcej informacji na temat konfigurowania połączonych kont magazynu, zobacz artykuł [Tworzenie klastrów usługi HDInsight][hdinsight-creation]. Jednak po usunięciu oryginalnego klastra usługi HDInsight hello można ponownie użyć domyślnego kontenera magazynu. W przypadku klastrów HBase faktycznie można zachować schemat tabeli HBase hello i danych przez utworzenie nowego klastra HBase przy użyciu hello domyślnego kontenera obiektów blob używanego przez klaster HBase, który został usunięty.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Użyj hello portalu Azure
Podczas tworzenia klastra usługi HDInsight z hello portalu, masz szczegóły konta magazynu tooprovide hello hello opcje (jak pokazano poniżej). Można również określić, czy mają konta dodatkowego magazynu skojarzone z hello klastra i jeśli tak, wybierz z usługi Data Lake Store lub innego obiektu blob magazynu Azure jako hello dodatkowego magazynu.

![HDInsight, hadoop, tworzenie źródła danych](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> Przy użyciu konta, dodatkowe miejsce do magazynowania w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.


### <a name="use-azure-powershell"></a>Korzystanie z programu Azure PowerShell
Jeśli użytkownik [zainstalowaniu i skonfigurowaniu programu Azure PowerShell][powershell-install], można użyć poniższych z hello Azure PowerShell monitu toocreate konto magazynu i kontener hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Interfejs wiersza polecenia platformy Azure

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Jeśli masz [zainstalowany i skonfigurowany hello Azure CLI](../cli-install-nodejs.md), hello następujące polecenie, mogą być używane tooa konto magazynu i kontener.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Witaj `--type` parametr wskazuje sposób replikacji konta magazynu hello. Aby uzyskać więcej informacji, zobacz artykuł [Azure Storage Replication](../storage/storage-redundancy.md) (Replikacja usługi Azure Storage). Nie używaj magazynu strefowo nadmiarowego, ponieważ nie obsługuje on stronicowych obiektów blob, plików, tabel ani kolejek.
> 
> 

Jesteś toospecify zostanie wyświetlony monit o hello region geograficzny w utworzeniu konta magazynu hello. Należy utworzyć konta magazynu hello w hello tym samym regionie, w którym planujesz utworzenie klastra usługi HDInsight.

Po utworzeniu konta magazynu hello Użyj hello następujące klucze konta magazynu hello tooretrieve polecenia:

    azure storage account keys list <storageaccountname>

toocreate kontener hello Użyj następującego polecenia:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Adresowanie plików w usłudze Azure Storage
schemat identyfikatora URI Hello dla uzyskiwania dostępu do plików w magazynie Azure z usługi HDInsight to:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

Witaj schemat identyfikatora URI zapewnia nieszyfrowany dostęp (z hello *wasb:* prefiks) oraz szyfrowany dostęp SSL (z *wasbs*). Firma Microsoft zaleca używanie *wasbs* wszędzie tam, gdzie to możliwe, nawet wtedy, gdy podczas uzyskiwania dostępu do danych, które znajdują się wewnątrz hello tego samego regionu w systemie Azure.

Witaj &lt;BlobStorageContainerName&gt; identyfikuje nazwę hello hello kontenera obiektów blob w magazynie Azure.
Witaj &lt;StorageAccountName&gt; identyfikuje nazwę konta usługi Azure Storage hello. Wymagana jest w pełni kwalifikowana nazwa domeny (FQDN).

Jeśli żadna &lt;BlobStorageContainerName&gt; ani &lt;StorageAccountName&gt; został określony, domyślny system plików hello jest używany. Dla plików hello na powitania domyślnego systemu plików można użyć ścieżkę względną lub ścieżką bezwzględną. Na przykład Witaj *hadoop-mapreduce-examples.jar* dostarczanego z klastrami usługi HDInsight może być określony tooby przy użyciu jednej z następujących hello:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Nazwa pliku Hello jest <i>hadoop-examples.jar</i> w klastrach usługi HDInsight w wersji 2.1 i 1.6.
> 
> 

Witaj &lt;ścieżki&gt; jest hello pliku lub katalogu systemu plików HDFS nazwą ścieżki. Ponieważ kontenery w usłudze Azure Storage przechowują po prostu pary klucz-wartość, nie istnieje prawdziwy hierarchiczny system plików. Znak ukośnika (/) wewnątrz klucza obiektu blob jest interpretowany jako separator katalogu. Na przykład nazwą obiektu blob powitania dla *hadoop-mapreduce-examples.jar* jest:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Podczas pracy z obiektami blob poza usługą HDInsight, większość narzędzi nie rozpoznaje formatu WASB hello i zamiast tego oczekuje podstawowego formatu ścieżki, takie jak `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Dostęp do obiektów blob 


### <a name="access-blobs-using-azure-powershell"></a> Korzystanie z programu Azure PowerShell
> [!NOTE]
> Witaj polecenia w tej sekcji stanowią podstawowy przykład przy użyciu programu PowerShell tooaccess dane przechowywane w obiektach blob. Na przykład obszerniejszy dostosowany do pracy z usługą HDInsight, zobacz hello [narzędzi HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Użyj następującego polecenia cmdlet związanych z obiektami blob hello toolist hello:

    Get-Command *blob*

![Lista poleceń cmdlet programu PowerShell związanych z obiektami blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Przekazywanie plików
Zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Pobieranie plików
Witaj poniższy skrypt pobiera bloku folderu bieżącego toohello obiektu blob. Przed uruchamianie skryptu hello Zmień folder tooa katalogu hello, w którym masz uprawnienia do zapisu.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Jeśli nazwa grupy zasobów hello i nazwa klastra hello, można użyć hello następującego kodu:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Usuwanie plików
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Lista plików
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Uruchamianie zapytań Hive przy użyciu niezdefiniowanego konta magazynu
Ten przykład przedstawia, jak toolist folderu z konta magazynu, który nie jest zdefiniowany podczas hello procesu tworzenia.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Użyj powitania po toolist hello związanych z obiektami blob poleceń:

    azure storage blob

**Przykład użycia interfejsu wiersza polecenia Azure tooupload pliku**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Przykład użycia interfejsu wiersza polecenia Azure toodownload pliku**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Przykład użycia interfejsu wiersza polecenia Azure toodelete pliku**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Przykład użycia interfejsu wiersza polecenia Azure toolist plików**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Używanie dodatkowych kont magazynu

Podczas tworzenia klastra usługi HDInsight, możesz określić hello konto Azure Storage, które chcesz tooassociate z nim. Ponadto toothis konta magazynu, można dodać dodatkowe konta magazynu z hello sam subskrypcji platformy Azure lub różnych subskrypcji Azure, podczas procesu tworzenia hello lub po utworzeniu klastra. Aby uzyskać instrukcje dotyczące dodawania kolejnych kont magazynu, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> Przy użyciu konta, dodatkowe miejsce do magazynowania w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.

## <a name="next-steps"></a>Następne kroki
W tym artykule należy przedstawiono sposób toouse zgodnego systemem plików HDFS magazynu platformy Azure z usługą HDInsight. Dzięki temu można toobuild skalowalnych, długoterminowych, archiwizacji rozwiązań do pozyskiwania danych i użyj HDInsight toounlock hello informacji wewnątrz hello przechowywane strukturalnych i danych bez struktury.

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
