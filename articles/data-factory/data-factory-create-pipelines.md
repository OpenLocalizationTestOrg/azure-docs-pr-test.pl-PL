---
title: "Potoki aaaCreate/zaplanować, działania łańcucha w fabryce danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate danych potok w fabryce danych Azure toomove i przekształcania danych. Utwórz opartego na informacje o przepływie pracy tooproduce gotowe toouse danych."
keywords: "dane potoku, przepływów pracy opartych na danych"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Potoki i działań w fabryce danych Azure
Ten artykuł pomaga zrozumieć potoki i działań w fabryce danych Azure i używać ich tooconstruct end-to-end opartych na danych w przepływach pracy dla przenoszenia danych i scenariusze przetwarzania danych.  

> [!NOTE]
> W tym artykule przyjęto założenie, że przejściu [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md). Jeśli nie masz hands-na-doświadczenie w tworzeniu fabryki danych, pośrednictwa [samouczek przekształcania danych](data-factory-build-your-first-pipeline.md) i/lub [samouczek przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) można lepiej zrozumieć, w tym artykule.  

## <a name="overview"></a>Omówienie
Fabryka danych może obejmować jeden lub wiele potoków. Potoki to logiczne grupy działań, które wspólnie wykonują zadanie. Hello działań w potoku zdefiniuj akcje tooperform na podstawie danych. Na przykład może używać kopii działania toocopy danych z lokalnego programu SQL Server tooan magazynu obiektów Blob Azure. Następnie należy użyć działania Hive, które uruchamia skrypt Hive na usłudze Azure HDInsight klastra tooprocess/przekształcania danych z danych wyjściowych tooproduce hello obiektu blob magazynu. Na koniec należy użyć drugiej kopii działania toocopy hello danych wyjściowych danych tooan magazyn danych SQL Azure na podstawie których analizy biznesowej (BI) rozwiązań raportowych są tworzone. 

Dane działanie może — ale nie musi — korzystać z wejściowych [zestawów danych](data-factory-create-datasets.md) i generować co najmniej jeden wyjściowy [zestaw danych](data-factory-create-datasets.md). Witaj Poniższy diagram przedstawia hello relacji między potoku, działania i zestawu danych w fabryce danych: 

![Relacja między potoku, działania i zestawu danych](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Potok pozwala toomanage działania jako zestaw zamiast nich osobno. Na przykład można wdrożyć, zaplanować, wstrzymać i wznowić potoku, zamiast dotyczących działań w potoku hello niezależnie.

Usługa Data Factory obsługuje dwa typy działań — w zakresie przekształcania oraz przenoszenia danych. Każde działanie może mieć zero lub więcej danych wejściowych [zestawów danych](data-factory-create-datasets.md) i tworzące co najmniej jeden wyjściowy zestaw danych.

Zestaw danych wejściowych reprezentuje hello dane wejściowe dla działania w potoku hello a hello wyjściowy dla działania hello wyjściowy zestaw danych. Zestawy danych identyfikują dane w różnych magazynach danych, takich jak tabele, pliki, foldery i dokumenty. Po utworzeniu zestawu danych można go użyć z działaniami w potoku. Na przykład zestaw danych może być zestawem danych wejściowych/wyjściowych działania kopiowania lub działania HDInsightHive. Aby uzyskać więcej informacji na temat zestawów danych, zobacz artykuł [Datasets in Azure Data Factory](data-factory-create-datasets.md) (Zestawy danych w usłudze Azure Data Factory).

### <a name="data-movement-activities"></a>Działania dotyczące przenoszenia danych
Działanie kopiowania w fabryce danych kopiuje dane z magazynu danych źródła danych magazynu tooa ujścia. Fabryka danych obsługuje powitania po magazynów danych. Obiekt sink tooany można zapisać danych z dowolnego źródła. Kliknij przycisk toolearn magazynu danych, jak toocopy tooand danych z tego magazynu.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Przechowuje dane z * można lokalnie lub na platformie Azure IaaS i wymaga tooinstall [brama zarządzania danymi](data-factory-data-management-gateway.md) na maszynie IaaS na lokalnym/Azure.

Aby uzyskać więcej informacji, zobacz artykuł [Działania dotyczące przenoszenia danych](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Działania dotyczące przekształcania danych
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Aby uzyskać więcej informacji, zobacz artykuł [Działania dotyczące przekształcania danych](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Niestandardowe działania programu .NET 
Jeśli potrzebujesz toomove danych do/z danych sklepu, która hello aktywność kopiowania nie obsługuje, lub Przekształcanie danych za pomocą własną logikę, Utwórz **działania niestandardowego .NET**. Aby uzyskać szczegółowe informacje na temat tworzenia i używania niestandardowego działania, zobacz artykuł [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) (Korzystanie z niestandardowych działań w potoku usługi Azure Data Factory).

## <a name="schedule-pipelines"></a>Potoki harmonogramu
Potok jest aktywna tylko między jego **start** czasu i **zakończenia** czasu. Nie jest wykonywany przed godziną rozpoczęcia hello lub po godzinie zakończenia hello. Jeśli potoku hello jest wstrzymana, nie zostanie wykonana niezależnie od jego czas rozpoczęcia i zakończenia. Dla toorun potoku jego powinien nie można wstrzymać. Zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) toounderstand działania planowania i wykonywania w fabryce danych Azure.

## <a name="pipeline-json"></a>Format JSON potoku
Przyjrzyjmy się bliżej definicji potoku w formacie JSON. Struktura ogólna powitania dla potoku wygląda następująco:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Tag | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa potoku hello. Określ nazwę, która reprezentuje akcję hello hello potoku wykonuje. <br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Tak |
| description | Określ tekst hello opisujący, jakie potoku hello jest używany dla. |Tak |
| activities | Witaj **działania** sekcji może mieć co najmniej jednego działania zdefiniowane w nim. Zobacz następną sekcję hello, aby uzyskać szczegółowe informacje o elemencie JSON działania hello. | Tak |  
| rozpoczynanie | Data i godzina rozpoczęcia dla potoku hello. Musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Na przykład: `2016-10-14T16:32:41Z`. <br/><br/>Jest możliwe toospecify czasu lokalnego, na przykład czas EST. Oto przykład: `2016-02-27T06:00:00-05:00`", która jest szacowana AM 6<br/><br/>Witaj właściwości początkową i końcową razem Określ okres aktywności potoku hello. Wycinki danych wyjściowych tylko są tworzone z aktywny okres. |Nie<br/><br/>Jeśli określono wartość dla właściwości końca hello, musisz określić wartość dla właściwości rozpoczęcia hello.<br/><br/>Witaj godziny rozpoczęcia i zakończenia zarówno można pusty toocreate potoku. Należy określić zarówno wartości tooset jako aktywny okres hello toorun potoku. Jeśli nie określono godziny rozpoczęcia i zakończenia podczas tworzenia potoku, można ustawić ich później za pomocą polecenia cmdlet hello AzureRmDataFactoryPipelineActivePeriod zestawu. |
| Koniec | Data czas zakończenia dla potoku hello. Jeśli zostanie określona, musi być w formacie ISO. Na przykład: `2016-10-14T17:32:41Z` <br/><br/>Jest możliwe toospecify czasu lokalnego, na przykład czas EST. Oto przykład: `2016-02-27T06:00:00-05:00`, która jest szacowana AM 6<br/><br/>potok hello toorun przez czas nieokreślony, określ 9999-09-09 jako wartość właściwości końca hello hello. <br/><br/> Potok jest aktywna tylko między jego czas rozpoczęcia i godzina zakończenia. Nie jest wykonywany przed godziną rozpoczęcia hello lub po godzinie zakończenia hello. Jeśli potoku hello jest wstrzymana, nie zostanie wykonana niezależnie od jego czas rozpoczęcia i zakończenia. Dla toorun potoku jego powinien nie można wstrzymać. Zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) toounderstand działania planowania i wykonywania w fabryce danych Azure. |Nie <br/><br/>Jeśli określono wartość dla właściwości rozpoczęcia hello, musisz określić wartość dla właściwości końca hello.<br/><br/>Zobacz uwagi dla hello **start** właściwości. |
| isPaused | Jeśli zestaw tootrue, hello potoku nie działa. W hello wstrzymał jego stan. Wartość domyślna = false. Można użyć tej właściwości tooenable lub wyłączyć potoku. |Nie |
| pipelineMode | Metoda Hello planowania trwający hello potoku. Dozwolone wartości to: (domyślnie), zaplanowane jednorazowe.<br/><br/>"Zaplanowana" oznacza, że tego potoku hello jest uruchamiane w określonych odstępach czasu zgodnie z tooits aktywny okres (czas rozpoczęcia i zakończenia). "Jednorazowe" oznacza, że tego potoku hello jest wykonywane tylko raz. Potoki jednorazowe utworzonej nie może być zmodyfikowany zaktualizowane obecnie. Zobacz [potoku Onetime](#onetime-pipeline) szczegółowe informacje o ustawienie jednorazowe. |Nie |
| expirationTime | Czas trwania po utworzeniu dla których hello [potoku jednorazowego](#onetime-pipeline) jest prawidłowa i powinny być zainicjowana. Jeśli nie ma żadnych aktywnych nie powiodło się, lub do czasu działa, potoku hello jest automatycznie usunięte po dotarciu hello czas wygaśnięcia. Wartość domyślna Hello:`"expirationTime": "3.00:00:00"`|Nie |
| Zbiory danych |Lista toobe zestawy danych używane przez działania zdefiniowane w potoku hello. Ta właściwość może być zestawów danych używanych toodefine, które są określone toothis potoku i nie jest zdefiniowany w fabryce danych hello. Zestaw danych zdefiniowany w ramach tego potoku można używać tylko w ramach tego potoku i nie może zostać udostępniony. Zobacz [zakres zestawów danych](data-factory-create-datasets.md#scoped-datasets) szczegółowe informacje. |Nie |

## <a name="activity-json"></a>Format JSON działania
Witaj **działania** sekcji może mieć co najmniej jednego działania zdefiniowane w nim. Każde działanie ma hello następujące struktury najwyższego poziomu:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    },
    "scheduler":
    {
    }
}
```

Poniższa tabela zawiera opis właściwości w działaniu hello JSON definicji:

| Tag | Opis | Wymagane |
| --- | --- | --- |
| name | Nazwa działania hello. Określ nazwę, która reprezentuje akcję hello, który wykonuje działania hello. <br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Tak |
| description | Tekst opisujący co hello działania lub służy do |Tak |
| type | Typ działania hello. Zobacz hello [działań przepływu danych](#data-movement-activities) i [działań przekształcania danych](#data-transformation-activities) sekcje dla różnych typów działań. |Tak |
| Dane wejściowe |Tabele wejściowe używane przez działanie hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Tak |
| dane wyjściowe |Tabele wyjściowe używany w działaniu hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Tak |
| linkedServiceName |Nazwa hello połączonej usługi używana na powitania działania. <br/><br/>Działanie może wymagać określenia hello połączone usługi, która łączy toohello środowiska obliczeniowego wymagane. |Tak w przypadku działania usługi HDInsight i Azure Machine Learning działanie wsadowego oceniania <br/><br/>Nie dla wszystkich innych |
| typeProperties |Właściwości w hello **typeProperties** sekcji są zależne od typu hello działania. właściwości typu toosee dla działania, kliknij działanie toohello łącza w poprzedniej sekcji hello. | Nie |
| policy |Zasady, które mają wpływ na zachowanie środowiska wykonawczego hello hello działania. Jeśli nie zostanie określona, używane są zasady domyślne. |Nie |
| Harmonogram | Właściwość "harmonogramu" jest używana toodefine potrzeby planowania dla działania hello. Właściwości podrzędnych są takie same jak te w hello hello hello [właściwości availability w zestawie danych](data-factory-create-datasets.md#dataset-availability). |Nie |


### <a name="policies"></a>Zasady
Zasady wpływają na zachowanie środowiska wykonawczego hello działania, w szczególności, podczas przetwarzania wycinka hello tabeli. w poniższej tabeli Hello zawiera szczegóły hello.

| Właściwość | Dozwolone wartości | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| Współbieżność |Liczba całkowita <br/><br/>Wartość maksymalna: 10 |1 |Liczba równoczesnych wykonaniami hello działania.<br/><br/>Określa hello Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków. Na przykład jeśli działanie wymaga toogo za pośrednictwem duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza hello przetwarzania danych. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Określa kolejność hello wycinki danych, które są przetwarzane.<br/><br/>Na przykład jeśli masz wycinków 2 (w toku co 4 godziny, a innym godzinie 5), a oba oczekują na wykonanie. Jeśli ustawisz hello executionPriorityOrder toobe NewestFirst wycinka hello godzinie 5 jest przetwarzana najpierw. Podobnie jeśli ustawisz hello executionPriorityORder toobe OldestFIrst wycinka hello godzinie 4 jest przetwarzany. |
| retry |Liczba całkowita<br/><br/>Maksymalna wartość może być 10 |0 |Liczba ponownych prób przed hello przetwarzania danych dla wycinka hello jest oznaczona jako niepowodzenie. Wykonania działania dla wycinka danych próba zostanie ponowiona się toohello określona liczba ponownych prób. Ponów próbę Hello odbywa się jak najszybciej po awarii hello. |
| timeout |Zakres czasu |00:00:00 |Limit czasu dla działania hello. Przykład: 00:10:00 (oznacza limitu 10 minut)<br/><br/>Jeśli wartość nie została określona lub jest równa 0, limit czasu hello jest nieograniczony.<br/><br/>Jeśli czas przetwarzania danych hello na wycinek przekracza wartość limitu czasu hello, anulowaniu i hello system próbuje tooretry hello przetwarzania. Witaj liczby ponownych prób zależy od hello ponawiania właściwości. W przypadku przekroczenia limitu czasu hello stan jest ustawiany tooTimedOut. |
| Opóźnienie |Zakres czasu |00:00:00 |Określ opóźnienie hello przed rozpoczęciem przetwarzania danych powoduje uruchomienie wycinek hello.<br/><br/>Hello wykonywania działań dotyczących wycinek danych jest uruchamiany po hello opóźnienie jest hello oczekiwany czas wykonywania.<br/><br/>Przykład: 00:10:00 (oznacza opóźnienia w ciągu 10 minut) |
| Parametr longRetry |Liczba całkowita<br/><br/>Wartość maksymalna: 10 |1 |Witaj liczbę długi ponownych prób przed hello wycinek wykonanie nie powiodło się.<br/><br/>Parametr longRetry prób uzyskają przez longRetryInterval. Dlatego toospecify czas między ponownymi próbami, należy użyć longRetry. Jeśli został określony zarówno longRetry, jak i ponów próbę, każdej próbie longRetry zawiera ponownych prób i hello maksymalną liczbę prób ponawiania * longRetry.<br/><br/>Na przykład, jeśli mamy hello następujące ustawienia zasad działania hello:<br/>Spróbuj ponownie: 3<br/>Parametr longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Załóżmy istnieje tylko jeden wycinek tooexecute (oczekiwanie stanu) i wykonania działania hello zawsze kończy się niepowodzeniem. Początkowo może być 3 wykonywanie kolejnych prób. Po każdej próbie stanu wycinka hello byłoby ponów próbę. Po pierwsze 3 prób się za pośrednictwem stanu wycinka hello będą LongRetry.<br/><br/>Po upływie godziny (to znaczy wartość longRetryInteval w) będzie inny zestaw 3 wykonywanie kolejnych prób. Po utworzeniu tego stanu wycinka hello będzie można i będą podejmowane próby. Dlatego całkowity 6 podejmowano.<br/><br/>Jeśli wykonanie żadnych zakończy się powodzeniem, stan wycinek hello będzie gotowy i są podjęto próby.<br/><br/>Parametr longRetry mogą być używane w sytuacji, w których danych zależnych dociera deterministyczna razy lub hello ogólnej środowiska jest niestabilnym, w których przetwarzania danych. W takich przypadkach podczas ponownych prób po kolei nie mogą pomóc w i w ten sposób po upływie interwału czasu powoduje hello potrzebne dane wyjściowe.<br/><br/>Word Przestroga: nie należy ustawiać wysokiej wartości longRetry lub longRetryInterval. Zazwyczaj wyższej wartości oznacza innych kwestii systemowych. |
| longRetryInterval |Zakres czasu |00:00:00 |Witaj opóźnienie między próbami czas ponów |

## <a name="sample-copy-pipeline"></a>Przykładowy potok kopiowania
Następujące przykładowe potoku hello, ma jedno działanie typu **kopiowania** w hello **działania** sekcji. W tym przykładzie hello [aktywności kopiowania](data-factory-data-movement-activities.md) kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów Blob platformy Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Należy zwrócić uwagę hello następujące punkty:

* W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.
* Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**. Definiowanie zestawów danych w formacie JSON opisano w artykule [Zestawy danych](data-factory-create-datasets.md). 
* W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello. W hello [działań przepływu danych](#data-movement-activities) kliknij hello magazynu danych, które mają toouse jako źródło lub toolearn zbiornika więcej informacji na temat przenoszenia danych z tego magazynu danych. 

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Przykładowy potok przekształcania
Następujące przykładowe potoku hello, ma jedno działanie typu **HDInsightHive** w hello **działania** sekcji. W tym przykładzie hello [działania HDInsight Hive](data-factory-hive-activity.md) przekształcenia danych z magazynu obiektów Blob platformy Azure, uruchamiając plik skryptu Hive w klastrze usługi Azure HDInsight Hadoop. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Należy zwrócić uwagę hello następujące punkty: 

* W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**HDInsightHive**.
* plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **AzureStorageLinkedService**) i w ** skrypt** folderu w kontenerze hello **adfgetstarted**.
* Witaj `defines` sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałąź (np. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Witaj **typeProperties** sekcja jest różne dla każdego działania transformacji. toolearn informacje o właściwościach typu obsługiwane dla działania przekształcania, kliknij działanie przekształcania hello w hello [działań przekształcania danych](#data-transformation-activities) tabeli. 

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: Tworzenie pierwszego potoku dane tooprocess przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Wiele działań w potoku
Hello poprzednie dwie próby potoki zawierać tylko jedno działanie w nich. Potok może obejmować więcej niż jedno działanie.  

Jeśli masz wiele działań w potoku, dane wyjściowe działania nie jest wejściem innej aktywności hello działania mogą działać równolegle, jeśli wycinki danych wejściowych dla działań hello jest gotowe. 

Dwa działania można łańcucha dzięki użyciu hello wyjściowy zestaw danych z jednego działania jako hello wejściowego zestawu danych hello innych działań. działanie drugi Hello wykonuje tylko wtedy, gdy hello najpierw jeden zakończy się pomyślnie.

![Tworzenie łańcuchów działań w hello sam potoku](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

W tym przykładzie potoku hello ma dwa działania: działania Activity1 i Activity2. Witaj działania Activity1 przyjmuje Dataset1 jako dane wejściowe i generuje dane wyjściowe Dataset2. Witaj działanie ma Dataset2 jako dane wejściowe i generuje dane wyjściowe Dataset3. Ponieważ dane wyjściowe działania Activity1 hello (Dataset2) jest wprowadzanie hello Activity2, hello Activity2 działa tylko po hello działanie zakończy się pomyślnie i tworzy hello Dataset2 wycinka. Jeśli hello działania Activity1 jakiegoś powodu nie powiedzie się i nie tworzy wycinek hello Dataset2, hello 2 działania nie zostanie uruchomiony dla tego wycinka (na przykład: 9 AM too10 m). 

Można również łańcucha działań, które znajdują się w różnych potoków.

![Tworzenie łańcuchów działań w dwóch potoki](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

W tym przykładzie Pipeline1 ma tylko jedno działanie, która przyjmuje Dataset1 jako dane wejściowe i tworzy Dataset2 jako dane wyjściowe. Witaj Pipeline2 ma również tylko jedno działanie, który pobiera Dataset2 jako dane wejściowe i Dataset3 jako dane wyjściowe. 

Aby uzyskać więcej informacji, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Tworzenie i monitorowanie potoki
Potoki można utworzyć przy użyciu jednej z tych narzędzi lub zestawów SDK. 

- Kreator kopiowania. 
- Azure Portal
- Visual Studio
- Azure PowerShell
- Szablon usługi Azure Resource Manager
- Interfejs API REST
- Interfejs API .NET

Zobacz hello następujące samouczki instrukcje krok po kroku dotyczące tworzenia potoki przy użyciu jednej z tych narzędzi lub zestawów SDK.
 
- [Tworzenie potoku z działaniem przekształcania danych](data-factory-build-your-first-pipeline.md)
- [Tworzenie potoku z działaniem przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Po potoku jest utworzony wdrożone, można zarządzać i monitorować Twoje potoki przy użyciu hello Azure bloki portalu lub Monitor i zarządzania aplikacjami. Zobacz następujące tematy, aby uzyskać instrukcje krok po kroku hello. 

- [Monitorowanie i zarządzanie nimi potoki przy użyciu bloków portalu Azure](data-factory-monitor-manage-pipelines.md).
- [Monitorowanie i zarządzanie nimi potoki za pomocą monitora i zarządzanie aplikacjami](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Jednorazowe potoku
Możesz utworzyć i zaplanować toorun potoku okresowo (na przykład: co godzinę lub codziennie) czasy, określ w definicji potoku hello w hello rozpoczęcia i zakończenia. Zobacz [planowania wykonania](#scheduling-and-execution) szczegółowe informacje. Można również utworzyć potok, który jest uruchamiany tylko raz. toodo tak, ustaw hello **pipelineMode** właściwości w hello potoku definicji zbyt**jednorazowe** pokazane na powitania następującego przykładowego kodu JSON. Witaj domyślna wartość tej właściwości to **zaplanowane**.

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Należy uwzględnić następujące hello:

* **Uruchom** i **zakończenia** razy dla potoku hello nie zostały określone.
* **Dostępność** danych wejściowych i wyjściowych zestawów danych jest określony (**częstotliwość** i **interwał**), nawet jeśli fabryki danych nie używa hello wartości.  
* Widok diagramu jednorazowe potoki nie są wyświetlane. To zachowanie jest celowe.
* Nie można zaktualizować jednorazowe potoków. Można sklonować potoku jednorazowego, zmień jego nazwę, właściwości aktualizacji i wdróż je toocreate kolejnego.


## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat zestawów danych, zobacz [utworzyć zestawy danych](data-factory-create-datasets.md) artykułu. 
- Aby uzyskać więcej informacji o sposobie planowania i wykonywania potoków, zobacz [planowania i wykonywania w fabryce danych Azure](data-factory-scheduling-and-execution.md) artykułu. 
  

