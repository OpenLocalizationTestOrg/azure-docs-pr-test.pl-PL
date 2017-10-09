---
title: "środowiskach aaaCompute obsługiwanych przez usługi fabryka danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat środowiska obliczeniowego, w których można używać w danych tootransform lub proces potoki (np. Azure HDInsight) fabryki danych Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Obliczenia bazy danych środowiskach obsługiwanych przez usługi fabryka danych Azure
W tym artykule opisano obliczeń różnych środowiskach można użyć tooprocess lub przekształcania danych. Udostępnia szczegóły o różnych konfiguracjach (na żądanie i użycie własnego) obsługiwany przez fabrykę danych podczas konfigurowania usług połączonych łączenia tych fabryki danych Azure tooan środowisk obliczeniowych.

Witaj Poniższa tabela zawiera listę środowiska obliczeniowe obsługiwane przez fabrykę danych oraz hello działania, które można uruchomić na nich. 

| Środowisko obliczeniowe | activities |
| --- | --- |
| [Klaster usługi HDInsight na żądanie](#azure-hdinsight-on-demand-linked-service) lub [klastrem usługi HDInsight](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md) |
| [Partia zadań Azure](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Działania usługi Machine Learning: wykonywanie wsadowe i aktualizacja zasobów](data-factory-azure-ml-batch-execution-activity.md) |
| [Usługi Azure Data Lake Analytics](#azure-data-lake-analytics-linked-service) |[Język U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [magazyn danych Azure SQL](#azure-sql-data-warehouse-linked-service), [programu SQL Server](#sql-server-linked-service) |[Procedura składowana](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Obsługiwane wersje usługi HDInsight w fabryce danych Azure
Usługa Azure HDInsight obsługuje wielu wersjach klastra Hadoop, które można wdrożyć w dowolnym momencie. Każdy wybór wersji tworzy określoną wersję hello dystrybucji Hortonworks Data Platform (HDP) i zestaw składników, które są zawarte w tej dystrybucji. Microsoft zachowuje aktualizowania hello listę obsługiwanych wersji usługi HDInsight tooprovide najnowsze składniki ekosystemu Hadoop i poprawki. Witaj HDInsight 3.2 jest przestarzałe na 1 kwietnia 2017 r. Aby uzyskać szczegółowe informacje, zobacz [obsługiwane wersje HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Ma to wpływ na istniejące fabryki danych Azure działań uruchamiania klastrów usługi HDInsight w wersji 3.2. Firma Microsoft zaleca się, że użytkownicy toofollow hello wytyczne w następujących sekcji tooupdate hello hello ryzyko fabryki danych:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Dla połączonych usług wskazanie tooyour własnych klastrów usługi HDInsight
* **Połączone usługi HDInsight wskazuje tooyour właścicielem HDInsight 3.2 lub poniżej klastrów:**

  Fabryka danych Azure obsługuje przesyłanie tooyour zadań HDInsight własnych klastrów z HDI 3.1 zbyt[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). Jednak możesz nie można już tworzyć klastra usługi HDInsight w wersji 3.2 po 1 kwietnia 2017 na podstawie hello amortyzacja zasad udokumentowane w [obsługiwane wersje HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Zalecenia:** 
  * Wykonywać testy zgodności hello tooensure hello działania odwołujące się do tej usługi połączonej za[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) z informacjami w [dostępne składniki platformy Hadoop różne wersje HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) i [Hortonworks wersji skojarzony z wersji usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Zbyt uaktualnienia klastra usługi HDInsight w wersji 3.2[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello najnowsze składniki ekosystemu Hadoop i poprawki. 

* **Połączone usługi HDInsight wskazuje tooyour właścicielem HDInsight 3.3 lub powyżej klastrów:**

  Fabryka danych Azure obsługuje przesyłanie tooyour zadań HDInsight własnych klastrów z HDI 3.1 zbyt[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Zalecenia:** 
  * Nie jest wymagane z punktu widzenia fabryki danych żadna akcja. Jednak jeśli pracujesz w starszej wersji usługi HDInsight, nadal zaleca się uaktualnienie zbyt[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello najnowsze składniki ekosystemu Hadoop i poprawki.

### <a name="for-hdinsight-on-demand-linked-services"></a>Dla usługi HDInsight na żądanie połączone usługi
* **W wersji 3.2 lub poniżej jest określona w definicji połączonego JSON usługi HDInsight na żądanie:**
  
  Fabryka danych Azure będzie obsługiwać tworzenie klastrów usługi HDInsight na żądanie wersji 3.3 lub więcej z **2017-05/15** i jego nowszych wersjach. I hello koniec obsługi istniejącego 3.2 HDInsight na żądanie usługi połączonej jest rozszerzona za**2017-07/15**.  

  **Zalecenia:** 
  * Wykonywać testy zgodności hello tooensure hello działania odwołujące się do tej usługi połączonej za [hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) z informacjami w [dostępne składniki platformy Hadoop różne wersje HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) i [Hortonworks wersji skojarzony z wersji usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Przed **2017-07/15**, zaktualizuj właściwość wersji hello w definicji JSON usługi połączonej HDI na żądanie za[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello najnowsze składniki ekosystemu Hadoop i poprawki. Szczegółowe definicji JSON, można znaleźć w temacie toohello [próbki połączonej usługi Azure HDInsight na żądanie](#azure-hdinsight-on-demand-linked-service). 

* **Nie określono wersję w połączonej usługi HDInsight na żądanie:**
  
  Fabryka danych Azure będzie obsługiwać tworzenie klastrów usługi HDInsight na żądanie wersji 3.3 lub więcej z **2017-05/15** i jego nowszych wersjach. I hello koniec usług połączonych 3.2 HDInsight na żądanie tooexisting pomocy technicznej jest rozszerzona za**2017-07/15**. 

  Przed **2017-07/15**, jeśli pole pozostanie puste, wartości domyślne hello wersji i właściwości osType są: 

  | Właściwość | Wartość domyślna | Wymagane |
  | --- | --- | --- |
  Wersja   | HDI 3.1 dla klastra systemu Windows i 3.2 HDI dla klastra z systemem Linux.| Nie
  osType | domyślne Hello jest systemu Windows | Nie

  Po **2017-07/15**, jeśli pole pozostanie puste, wartości domyślne hello wersji i właściwości osType są:

  | Właściwość | Wartość domyślna | Wymagane |
  | --- | --- | --- |
  Wersja   | 3.3 HDI dla klastra systemu Windows i 3.5 dla klastra z systemem Linux.    | Nie
  osType | Domyślnie Hello jest systemu Linux   | Nie

  **Zalecenia:** 
  * Przed **2017-07/15**, wykonać testy zgodności hello tooensure hello działania odwołujące się do tej połączonej usługi zbyt[hello najnowsza wersja obsługiwana wersja usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) informacje opisane w [Hadoop składników dostępnych w różnych wersjach HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) i [Hortonworks wersji skojarzony z wersji usługi HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Po **2017-07/15**, upewnij się, że zostaną jawnie określone wartości osType i wersji, jeśli chcesz toooverride hello domyślnych ustawień. 

>[!Note]
>Fabryka danych Azure nie obsługuje obecnie klastrów usługi HDInsight przy użyciu usługi Azure Data Lake Store jako podstawowy magazynu. Użyj magazynu Azure jako podstawowy magazynu dla klastrów usługi HDInsight. 
>  
>  

## <a name="on-demand-compute-environment"></a>Środowiska obliczeniowe na żądanie
W tym typie konfiguracji środowiska komputerowego hello pełni zarządza hello usługi fabryka danych Azure. Jest automatycznie tworzony przez hello usługi fabryka danych przed zadanie jest tooprocess przesłanych danych i usunięta po zakończeniu zadania hello. Można utworzyć połączonej usługi hello obliczeń na żądanie środowiska, jest skonfigurowana i sterowanie ustawieniami szczegółowego do wykonywania zadań zarządzania klastrem i uruchamianie akcji.

> [!NOTE]
> Konfiguracja na żądanie Hello jest obecnie obsługiwane tylko w przypadku klastrów usługi HDInsight Azure.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure HDInsight na żądanie połączona usługa
Witaj usługi fabryka danych Azure może automatycznie tworzyć opartych na systemie Windows/Linux na żądanie HDInsight klastra tooprocess danych. klaster Hello jest tworzony w tym samym regionie co konto magazynu hello (właściwość linkedServiceName w hello JSON) skojarzone z klastrem hello hello. Konto magazynu Hello musi być kontem magazynu ogólnego przeznaczenia Azure standard. 

Należy zwrócić uwagę następujące hello **ważne** punktów o HDInsight na żądanie połączonej usługi:

* Nie ma hello na żądanie klastra usługi HDInsight utworzone w ramach subskrypcji platformy Azure. Witaj usługi fabryka danych Azure zarządza hello klastra usługi HDInsight na żądanie w Twoim imieniu.
* Witaj dzienniki dla zadania, które są uruchamiane na HDInsight na żądanie z klastra są kopiowane toohello konta magazynu skojarzone z klastrem usługi HDInsight hello. Te dzienniki można korzystać z portalu Azure w hello hello **szczegóły uruchomienia działania** bloku. Zobacz [monitorować i zarządzać potoki](data-factory-monitor-manage-pipelines.md) artykułu, aby uzyskać szczegółowe informacje.
* Naliczane są opłaty tylko w przypadku hello godzinę klastra usługi HDInsight hello się i uruchomionych zadań.

> [!IMPORTANT]
> Zwykle trwa **20 minut** lub więcej tooprovision Azure HDInsight klastra na żądanie.
> 
> 

### <a name="example"></a>Przykład
powitania po JSON definiuje opartych na systemie Linux usługi HDInsight połączony na żądanie. Witaj usługi fabryka danych automatycznie tworzy **opartych na systemie Linux** klastra usługi HDInsight podczas przetwarzania wycinka danych. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

toouse klastra usługi HDInsight opartej na systemie Windows, ustaw **osType** za**windows** albo nie używaj właściwości hello jest wartość domyślna hello: systemu windows.  

> [!IMPORTANT]
> Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. Z usługą HDInsight połączony na żądanie, klastra usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello. 
> 
> Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.
> 
> 

### <a name="properties"></a>Właściwości
| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |właściwości typu Hello należy ustawić wartość zbyt**HDInsightOnDemand**. |Tak |
| Wartość ClusterSize |Liczba węzłów procesu roboczego/danych w klastrze hello. klaster usługi HDInsight Hello jest tworzony z głównymi węzłami 2 oraz hello liczba węzłów procesu roboczego, które określisz dla tej właściwości. węzły Hello mają rozmiar Standard_D3, który ma 4 rdzenie, więc klastra z węzłem procesu roboczego 4 przyjmuje 24 rdzenie (4\*4 = 16 rdzenie dla węzłów procesu roboczego, a także 2\*rdzenie 4 = 8 dla węzłów głównych). Zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) szczegółowe informacje o hello Standard_D3 warstwy. |Tak |
| wartość TimeToLive |Witaj dozwolony czas bezczynności klastra usługi HDInsight na żądanie hello. Określa, jak długo klastra usługi HDInsight na żądanie hello pozostaje aktywne po zakończeniu działania uruchamiania, jeśli w klastrze hello nie ma żadnych aktywnych działań.<br/><br/>Na przykład, jeśli działanie Uruchom przyjmuje 6 minut i timetolive jest too5 minut, pozostaje klastra hello aktywności 5 minut po hello 6 minut przetwarzania uruchamiania działania hello. Jeśli inny uruchamiania działania jest wykonywane z okna 6 minut hello, jednak jest przetwarzany przez hello tego samego klastra.<br/><br/>Tworzenie klastra usługi HDInsight na żądanie jest kosztowna operacja (może to potrwać pewien czas), więc użyć tego ustawienia jako wydajności wymagane tooimprove fabryki danych przez ponowne użycie klastra usługi HDInsight na żądanie.<br/><br/>Jeśli ustawisz too0 wartość timetolive klaster hello jest usunięty zaraz po zakończeniu działania hello Uruchom. Natomiast jeśli ustawisz wysokiej wartości hello klastra może pozostać bezczynny, co niepotrzebnie wysokich kosztów. Dlatego jest ważne, aby ustawić odpowiednią wartość hello na podstawie Twoich potrzeb.<br/><br/>Jeśli skonfigurowana wartość właściwości timetolive hello wielu potoki można udostępniać wystąpienia klastra usługi HDInsight na żądanie hello hello.  |Tak |
| Wersja |Wersja klastra usługi HDInsight hello. Wartość domyślna Hello jest 3.1 dla klastra systemu Windows i 3.2 dla systemu Linux klastra. |Nie |
| linkedServiceName | Usługa Azure Storage połączone toobe usługi używane przez klaster na żądanie hello do przechowywania i przetwarzania danych. Witaj klastra usługi HDInsight jest tworzony w hello sam regionu co konto magazynu Azure.<p>Obecnie nie można utworzyć klastra usługi HDInsight na żądanie, korzystającą z usługi Azure Data Lake Store jako hello magazynu. Jeśli chcesz toostore hello dane z usługi HDInsight przetwarzania w usłudze Azure Data Lake Store, użyj danych hello toocopy działanie kopiowania z toohello magazynu obiektów Blob Azure hello Azure Data Lake Store. </p>  | Tak |
| additionalLinkedServiceNames |Określa, że dodatkowe konta magazynu dla hello HDInsight połączonej usługi, dzięki czemu usługi fabryka danych hello można zarejestrować je w Twoim imieniu. Te konta magazynu musi być w hello tego samego regionu hello HDInsight klastra, który jest tworzony w hello sam regionu co konto magazynu hello określony przez linkedServiceName. |Nie |
| osType |Typ systemu operacyjnego. Dozwolone wartości to: (domyślnie) systemu Windows i Linux |Nie |
| hcatalogLinkedServiceName |Nazwa Hello Azure SQL połączone usługi bazy danych HCatalog toohello punktu. klaster usługi HDInsight na żądanie Hello jest tworzona przy użyciu bazy danych Azure SQL hello jako hello potrzeby magazynu metadanych. |Nie |

#### <a name="additionallinkedservicenames-json-example"></a>przykład JSON additionalLinkedServiceNames

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Zaawansowane właściwości
Można również określić następujące właściwości hello szczegółową konfigurację klastra usługi HDInsight na żądanie hello hello.

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| coreConfiguration |Określa parametry konfiguracji podstawowej hello (jak core-site.xml) toobe klastra usługi HDInsight hello utworzony. |Nie |
| hBaseConfiguration |Określa parametry konfiguracji bazy danych HBase hello (hbase-site.xml) do klastra usługi HDInsight hello. |Nie |
| hdfsConfiguration |Określa parametry konfiguracji systemu plików HDFS hello (systemu plików hdfs-site.xml) do klastra usługi HDInsight hello. |Nie |
| hiveConfiguration |Określa parametry konfiguracji hive hello (gałąź site.xml) dla klastra usługi HDInsight hello. |Nie |
| mapReduceConfiguration |Określa parametry konfiguracji MapReduce hello (mapred-site.xml) do klastra usługi HDInsight hello. |Nie |
| oozieConfiguration |Określa parametry konfiguracji Oozie hello (oozie-site.xml) do klastra usługi HDInsight hello. |Nie |
| stormConfiguration |Określa parametry konfiguracji Storm hello (storm-site.xml) do klastra usługi HDInsight hello. |Nie |
| yarnConfiguration |Określa parametry konfiguracji Yarn hello (yarn-site.xml) do klastra usługi HDInsight hello. |Nie |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Przykład — konfiguracji klastra usługi HDInsight na żądanie z właściwości zaawansowane

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Rozmiary węzła
Można określić rozmiary hello węzłów head, danych i dozorcy przy użyciu hello następujące właściwości: 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| headNodeSize |Określa rozmiar hello hello węzła głównego. Witaj, wartość domyślna to: Standard_D3. Zobacz hello **określania rozmiarów węzła** sekcji, aby uzyskać szczegółowe informacje. |Nie |
| dataNodeSize |Określa rozmiar hello hello danych węzła. Witaj, wartość domyślna to: Standard_D3. |Nie |
| zookeeperNodeSize |Określa rozmiar hello hello dozorca Zoo węzła. Witaj, wartość domyślna to: Standard_D3. |Nie |

#### <a name="specifying-node-sizes"></a>Określanie rozmiary węzła
Zobacz hello [rozmiary maszyn wirtualnych](../virtual-machines/linux/sizes.md) artykule potrzebne toospecify dla właściwości hello wymienionych w poprzedniej sekcji hello wartości ciągu. wartości Hello muszą tooconform toohello **poleceń cmdlet i interfejsów API** przywoływany w artykule hello. Jak widać w artykule hello hello węzeł danych o rozmiarze duży (ustawienie domyślne) zawiera 7 GB pamięci, która nie może być dobrym dla danego scenariusza. 

Jeśli toocreate D4 o rozmiarze węzłów głównych i węzłów procesu roboczego, należy określić **Standard_D4** jako wartość właściwości headNodeSize i dataNodeSize hello. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Określono nieprawidłową wartość dla tych właściwości, może zostać wyświetlony następujący hello **błąd:** klastra toocreate nie powiodło się. Wyjątek: Operacja tworzenia toocomplete hello klastra. Operacja zakończona niepowodzeniem z kodem „400”. Końcowy stan klastra: „Błąd”. Komunikat o błędzie: "PreClusterCreationValidationFailure". Gdy zostanie wyświetlony ten błąd, upewnij się, że używasz hello **polecenia CMDLET i interfejsów API** nazwa z tabeli hello w hello [rozmiary maszyn wirtualnych](../virtual-machines/linux/sizes.md) artykułu.  

## <a name="bring-your-own-compute-environment"></a>Przełącz środowiska obliczeniowe
W tym typie konfiguracji użytkownicy mogą zarejestrować już istniejącego środowiska komputerowego jako połączonej usługi z fabryki danych. środowiska komputerowego Hello jest zarządzana przez użytkownika hello i hello usługi fabryka danych używa tooexecute hello działań.

Ten typ konfiguracji jest obsługiwane dla następujących hello obliczeniowe środowiskach:

* Usługa Azure HDInsight
* Azure Batch
* Azure Machine Learning
* Azure Data Lake Analytics
* Bazy danych Azure SQL, magazynu danych Azure SQL, programu SQL Server

## <a name="azure-hdinsight-linked-service"></a>Usługa Azure HDInsight połączona usługa
Klaster usługi HDInsight można utworzyć tooregister usługi Azure HDInsight połączone z fabryką danych.

### <a name="example"></a>Przykład

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Właściwości
| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |właściwości typu Hello należy ustawić wartość zbyt**HDInsight**. |Tak |
| clusterUri |Witaj URI hello klastra usługi HDInsight. |Tak |
| nazwa użytkownika |Określ nazwę hello toobe użytkownika hello używanych tooconnect tooan istniejącym klastrze usługi HDInsight. |Tak |
| hasło |Określ hasło dla konta użytkownika hello. |Tak |
| linkedServiceName | Nazwa hello połączoną usługą magazynu Azure odwołujące się do magazynu obiektów blob Azure toohello używana przez hello klastra usługi HDInsight. <p>Obecnie nie można określić, czy usługa Azure Data Lake Store połączonej usługi dla tej właściwości. Jeśli klaster usługi HDInsight hello toohello dostępu do usługi Data Lake Store, ze skryptów usługi Pig/gałęzi może dostęp do danych w hello Azure Data Lake Store. </p>  |Tak |

## <a name="azure-batch-linked-service"></a>Partia zadań Azure połączona usługa
Tooregister usługi połączone partii zadań Azure można utworzyć puli partii fabryki danych tooa maszynach wirtualnych (VM). Możesz uruchomić niestandardowych działań platformy .NET przy użyciu partii zadań Azure lub usługi Azure HDInsight.

Zobacz następujące tematy, jeśli są nowe usługi partia zadań tooAzure:

* [Podstawy usługi partia zadań Azure](../batch/batch-technical-overview.md) omówienie hello usługi partia zadań Azure.
* [Nowy AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) toocreate polecenia cmdlet konto partii zadań Azure (lub) [portalu Azure](../batch/batch-account-create-portal.md) konto partii zadań Azure hello toocreate za pomocą portalu Azure. Zobacz [toomanage przy użyciu programu PowerShell konta usługi partia zadań Azure](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) tematu, aby uzyskać szczegółowe instrukcje na temat używania polecenia cmdlet hello.
* [Nowy AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) toocreate polecenia cmdlet puli partii zadań Azure.

### <a name="example"></a>Przykład

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Dołącz "**.\< Nazwa regionu\>**"toohello nazwę konta wsadowego hello **accountName** właściwości. Przykład:

```json
"accountName": "mybatchaccount.eastus"
```

Innym rozwiązaniem jest tooprovide hello batchUri endpoint, jak pokazano w hello następujące przykładowe:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Właściwości
| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |właściwości typu Hello należy ustawić wartość zbyt**AzureBatch**. |Tak |
| Nazwa konta |Nazwa konta usługi partia zadań Azure hello. |Tak |
| accessKey |Klucz dostępu dla konta usługi partia zadań Azure hello. |Tak |
| poolName |Nazwa puli hello maszyn wirtualnych. |Tak |
| linkedServiceName |Nazwa hello połączoną usługą magazynu Azure skojarzony z tą usługą partii zadań Azure połączone. Tej połączonej usługi jest używany na potrzeby przemieszczania plików wymagane działania hello toorun i przechowywanie dzienniki wykonywania hello działania. |Tak |

## <a name="azure-machine-learning-linked-service"></a>Uczenie maszynowe Azure połączona usługa
Możesz utworzyć tooregister usługi Azure Machine Learning połączone fabryki danych tooa punktu końcowego oceniania partii uczenia maszynowego.

### <a name="example"></a>Przykład

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Właściwości
| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Typ |powinien mieć ustawioną właściwość type Hello: **uczenie maszynowe Azure**. |Tak |
| mlEndpoint |Witaj URL wsadowego oceniania. |Tak |
| apiKey |Witaj opublikowane interfejs API modelu obszaru roboczego. |Tak |

## <a name="azure-data-lake-analytics-linked-service"></a>Usługi Azure Data Lake Analytics połączona usługa
Możesz utworzyć **Azure Data Lake Analytics** połączone toolink usługi fabryki danych Azure tooan usługi Azure Data Lake Analytics obliczeń. Data Lake Analytics U-SQL działania w potoku hello Hello odwołuje się toothis połączone usługi. 

Witaj Poniższa tabela zawiera opisy hello ogólne właściwości używane w hello definicji JSON. Dodatkowo można wybrać nazwy głównej usługi i uwierzytelnianie poświadczeń użytkownika.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| **Typ** |powinien mieć ustawioną właściwość type Hello: **AzureDataLakeAnalytics**. |Tak |
| **Nazwa konta** |Nazwa konta usługi Azure Data Lake Analytics. |Tak |
| **Element dataLakeAnalyticsUri** |Identyfikator URI, usługi Azure Data Lake Analytics. |Nie |
| **Identyfikator subskrypcji** |Identyfikator subskrypcji platformy Azure |Nie (Jeśli nie określono subskrypcji hello jest używana fabryka danych). |
| **grupy zasobów o nazwie** |Nazwa grupy zasobów platformy Azure |Nie (Jeśli nie określono grupy zasobów hello jest używana fabryka danych). |

### <a name="service-principal-authentication-recommended"></a>Uwierzytelnianie główna usługi (zalecane)
główne uwierzytelnianie usługi toouse rejestru jednostki aplikacji w usłudze Azure Active Directory (Azure AD) i udziel go hello dostępu tooData Lake Store. Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Zwróć uwagę na powitania następujące wartości, których używasz toodefine hello połączonej usługi:
* Identyfikator aplikacji
* Klucz aplikacji 
* Identyfikator dzierżawy

Uwierzytelnianie usługi głównej określając hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **servicePrincipalId** | Określ identyfikator aplikacji hello klienta. | Tak |
| **servicePrincipalKey** | Określ klucz aplikacji hello. | Tak |
| **dzierżawy** | Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja. Można go pobrać aktywowania hello myszy w prawym górnym narożniku hello hello portalu Azure. | Tak |

**Przykład: Usługa podmiotu zabezpieczeń uwierzytelniania**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Uwierzytelnianie poświadczeń użytkownika
Alternatywnie można uwierzytelnienia poświadczeń użytkownika dla usługi Data Lake Analytics, określając hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **autoryzacji** | Kliknij przycisk hello **autoryzacji** przycisku na powitania Edytor fabryki danych i wprowadź Twoje poświadczenia przypisującej właściwość toothis hello wygenerowana automatycznie autoryzacji URL. | Tak |
| **Identyfikator sesji** | Identyfikator sesji OAuth z sesji autoryzacji OAuth hello. Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz. To ustawienie jest automatycznie generowany, gdy używasz hello Edytor fabryki danych. | Tak |

**Przykład: Użytkownik poświadczeń uwierzytelniania**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Witaj kod autoryzacji wygenerowanych przy użyciu hello **autoryzacji** przycisk wygaśnie po upływie pewnego czasu. Zobacz hello na powitania czas wygaśnięcia dla różnych typów kont użytkowników w poniższej tabeli. Może zostać wyświetlony następujący komunikat o błędzie hello hello podczas uwierzytelniania **wygaśnięcia tokenu**: poświadczeń błąd operacji: invalid_grant - AADSTS70002: błąd podczas sprawdzania poprawności poświadczeń. AADSTS70008: hello podać Udziel dostępu jest wygasnąć lub zostać odwołane. Identyfikator śledzenia: Identyfikator korelacji d18629e8-af88-43c5-88e3-d8419eb1fca1: sygnatura czasowa fac30a0c-6be6-4e02-8d69-a776d2ffefd7: 2015-12-15 21:09:31Z

| Typ użytkownika | Wygasa po |
|:--- |:--- |
| Konta użytkowników, które nie są zarządzane przez usługę Azure Active Directory (@hotmail.com, @live.comitp.) |12 godzin |
| Konta użytkowników zarządzanych przez usługi Azure Active Directory (AAD) |Uruchom 14 dni od ostatniego wycinek hello. <br/><br/>90 dni, jeśli wycinek oparte na podstawie OAuth połączonej usługi jest uruchamiana co najmniej raz na 14 dni. |

tooavoid/Rozwiąż ten błąd, ponownie autoryzować przy użyciu hello **autoryzacji** przycisku hello **wygaśnięcia tokenu** i wdrożenie usługi hello połączone. Można również tworzyć wartości **sessionId** i **autoryzacji** właściwości programowo przy użyciu kodu w następujący sposób:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Zobacz [klasy AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [klasy AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), i [klasy AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tematy, aby uzyskać więcej informacji informacje o klasach fabryki danych hello używane w kodzie hello. Dodaj odwołanie do: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll dla hello WindowsFormsWebAuthenticationDialog klasy. 

## <a name="azure-sql-linked-service"></a>Azure SQL połączona usługa
Tworzenie usługi SQL Azure połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych. Zobacz [Łącznik usług SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) artykułu, aby uzyskać szczegółowe informacje o tej połączonej usługi.

## <a name="azure-sql-data-warehouse-linked-service"></a>Połączona usługa Magazyn danych Azure SQL
Tworzenie usługi Azure SQL Data Warehouse połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych. Zobacz [łącznika magazynu danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu, aby uzyskać szczegółowe informacje o tej połączonej usługi.

## <a name="sql-server-linked-service"></a>Program SQL Server połączona usługa
Tworzenie usługi SQL Server połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych. Zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu, aby uzyskać szczegółowe informacje o tej połączonej usługi.

