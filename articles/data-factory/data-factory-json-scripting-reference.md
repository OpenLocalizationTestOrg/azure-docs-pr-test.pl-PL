---
title: "aaaAzure fabryki danych - odwołanie skryptów JSON | Dokumentacja firmy Microsoft"
description: "Udostępnia schematów JSON dla jednostek fabryki danych."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Fabryki danych Azure - JSON skryptów odwołania
Ten artykuł zawiera przykłady i schematów JSON do definiowania jednostek fabryki danych Azure (potoku, działania, zestawu danych i połączonej usługi).  

## <a name="pipeline"></a>Potok 
Struktura wysokiego poziomu Hello definicji potoku jest następujący: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Poniższa tabela zawiera opis właściwości hello w potoku hello definicji JSON:

| Właściwość | Opis | Wymagane
-------- | ----------- | --------
| name | Nazwa potoku hello. Określ nazwę, która reprezentuje akcję hello hello działania lub potoku jest skonfigurowany toodo<br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Tak |
| description |Tekst opisujący, jakie działania hello lub potoku jest używana | Nie |
| activities | Zawiera listę działań. | Tak |
| rozpoczynanie |Data i godzina rozpoczęcia dla potoku hello. Musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Na przykład: 2014-10-14T16:32:41. <br/><br/>Jest możliwe toospecify czasu lokalnego, na przykład czas EST. Oto przykład: `2016-02-27T06:00:00**-05:00`, która jest szacowana AM 6<br/><br/>Witaj właściwości początkową i końcową razem Określ okres aktywności potoku hello. Wycinki danych wyjściowych tylko są tworzone z aktywny okres. |Nie<br/><br/>Jeśli określono wartość dla właściwości końca hello, musisz określić wartość dla właściwości rozpoczęcia hello.<br/><br/>Witaj godziny rozpoczęcia i zakończenia zarówno można pusty toocreate potoku. Należy określić zarówno wartości tooset jako aktywny okres hello toorun potoku. Jeśli nie określono godziny rozpoczęcia i zakończenia podczas tworzenia potoku, można ustawić ich później za pomocą polecenia cmdlet hello AzureRmDataFactoryPipelineActivePeriod zestawu. |
| Koniec |Data czas zakończenia dla potoku hello. Jeśli zostanie określona, musi być w formacie ISO. Na przykład: 2014-10-14T17:32:41 <br/><br/>Jest możliwe toospecify czasu lokalnego, na przykład czas EST. Oto przykład: `2016-02-27T06:00:00**-05:00`, która jest szacowana AM 6<br/><br/>potok hello toorun przez czas nieokreślony, określ 9999-09-09 jako wartość właściwości końca hello hello. |Nie <br/><br/>Jeśli określono wartość dla właściwości rozpoczęcia hello, musisz określić wartość dla właściwości końca hello.<br/><br/>Zobacz uwagi dla hello **start** właściwości. |
| isPaused |Jeśli zestaw tootrue hello potoku nie działa. Wartość domyślna = false. Można użyć tej właściwości tooenable lub wyłączyć. |Nie |
| pipelineMode |Metoda Hello planowania trwający hello potoku. Dozwolone wartości to: (domyślnie), zaplanowane jednorazowe.<br/><br/>"Zaplanowana" oznacza, że tego potoku hello jest uruchamiane w określonych odstępach czasu zgodnie z tooits aktywny okres (czas rozpoczęcia i zakończenia). "Jednorazowe" oznacza, że tego potoku hello jest wykonywane tylko raz. Potoki jednorazowe utworzonej nie może być zmodyfikowany zaktualizowane obecnie. Zobacz [potoku Onetime](data-factory-create-pipelines.md#onetime-pipeline) szczegółowe informacje o ustawienie jednorazowe. |Nie |
| expirationTime |Czas po utworzeniu, dla których hello potoku jest prawidłowa i powinny być zainicjowana. Jeśli nie ma żadnych aktywnych nie powiodło się, lub oczekujące działa, potoku hello zostanie usunięta automatycznie po osiągnięciu hello czas wygaśnięcia. |Nie |


## <a name="activity"></a>Działanie 
Hello struktury wysokiego poziomu do działania w potoku definicji (element działania), jest następujący:

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
    }
    "scheduler":
    {
    }
}
```

Następujące tabeli opisano właściwości hello w ramach działania hello definicji JSON:

| Tag | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa działania hello. Określ nazwę, która reprezentuje hello akcję, która jest działanie hello skonfigurować toodo<br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Tak |
| description |Tekst opisujący, jakie działanie hello jest używany dla. |Tak |
| type |Określa typ hello hello działania. Zobacz hello [MAGAZYNY danych](#data-stores) i [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) sekcje dla różnych typów działań. |Tak |
| Dane wejściowe |Tabele wejściowe używane przez działanie hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Tak |
| dane wyjściowe |Tabele wyjściowe używany w działaniu hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Tak |
| linkedServiceName |Nazwa hello połączonej usługi używana na powitania działania. <br/><br/>Działanie może wymagać określenia hello połączone usługi, która łączy toohello środowiska obliczeniowego wymagane. |Tak, aby HDInsight działań, działania usługi Azure Machine Learning i działania dotyczącego procedury składowanej. <br/><br/>Nie dla wszystkich innych |
| typeProperties |Właściwości w sekcji typeProperties hello są zależne od typu hello działania. |Nie |
| policy |Zasady, które mają wpływ na zachowanie środowiska wykonawczego hello hello działania. Jeśli nie zostanie określona, używane są zasady domyślne. |Nie |
| Harmonogram |Właściwość "harmonogramu" jest używana toodefine potrzeby planowania dla działania hello. Właściwości podrzędnych są takie same jak te w hello hello hello [właściwości availability w zestawie danych](data-factory-create-datasets.md#dataset-availability). |Nie |

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

### <a name="typeproperties-section"></a>sekcja typeProperties
sekcja typeProperties Hello jest różne dla każdego działania. Transformacja działania mają tylko hello typu właściwości. Zobacz [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) w tym artykule, aby uzyskać przykłady JSON, które definiują czynności do przekształcenia w potoku. 

**Aktywność kopiowania** zawiera dwa podpunkty w sekcji typeProperties hello: **źródła** i **zbiornika**. Zobacz [MAGAZYNY danych](#data-stores) sekcji w niniejszym artykule dla JSON przykłady przedstawiające sposób przechowywania toouse danych jako źródła i/lub ujścia. 

### <a name="sample-copy-pipeline"></a>Przykładowy potok kopiowania
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
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Należy zwrócić uwagę hello następujące punkty:

* W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.
* Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**.
* W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello.

Zobacz [MAGAZYNY danych](#data-stores) sekcji w niniejszym artykule dla JSON przykłady przedstawiające sposób przechowywania toouse danych jako źródła i/lub ujścia.    

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Przykładowy potok przekształcania
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
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Należy zwrócić uwagę hello następujące punkty: 

* W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**HDInsightHive**.
* plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **AzureStorageLinkedService**) i w  **skrypt** folderu w kontenerze hello **adfgetstarted**.
* Witaj **definiuje** sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałąź (np. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Zobacz [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) w tym artykule, aby uzyskać przykłady JSON, które definiują czynności do przekształcenia w potoku.

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: Tworzenie pierwszego potoku dane tooprocess przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Połączona usługa
Hello struktury wysokiego poziomu dla definicji usługi połączonej następująco:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Następujące tabeli opisano właściwości hello w ramach działania hello definicji JSON:

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- | 
| name | Nazwa hello połączonej usługi. | Tak | 
| właściwości — Typ | Typ hello połączonej usługi. Na przykład: Usługa Azure Storage, baza danych SQL Azure. |
| typeProperties | sekcja typeProperties Hello zawiera elementy, które są różne dla każdego magazynu danych lub środowiska obliczeniowe. Zobacz [magazyny danych](#datastores) sekcji przypadku wszystkie dane hello sklepu usług połączonych i [obliczeniowe środowisk](#compute-environments) dla wszystkich hello obliczeniowe połączone usługi |   

## <a name="dataset"></a>Zestaw danych 
Zestaw danych z fabryki danych Azure jest zdefiniowane w następujący sposób:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Witaj w poniższej tabeli opisano właściwości w hello powyżej JSON:   

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| name | Nazwa zestawu danych hello. Zobacz [fabryki danych Azure - reguły nazewnictwa](data-factory-naming-rules.md) dla reguły nazewnictwa. |Tak |Nie dotyczy |
| type | Typ hello zestawu danych. Określ jeden z typów hello obsługiwane przez usługi fabryka danych Azure (na przykład: AzureBlob, AzureSqlTable). Zobacz [MAGAZYNY danych](#data-stores) sekcji dla wszystkich hello magazynów danych i typy danych obsługiwane przez fabryki danych. | 
| Struktura | Schemat hello zestawu danych. Zawiera kolumny, jak ich typy, itp. | Nie |Nie dotyczy |
| typeProperties | Właściwości odpowiadającego toohello wybranego typu. Zobacz [MAGAZYNY danych](#data-stores) sekcji dla obsługiwanych typów i ich właściwości. |Tak |Nie dotyczy |
| external | Wartość logiczna Flaga toospecify, czy zestaw danych jawnie jest generowany przez potok fabryki danych lub nie. |Nie |wartość false |
| availability | Definiuje hello przetwarzania okna lub hello fragmentowania modelu hello zestawu danych produkcyjnych. Aby uzyskać szczegółowe informacje w zestawie danych hello fragmentowania modelu, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu. |Tak |Nie dotyczy |
| policy |Definiuje kryteria hello lub hello warunek, który należy spełnić hello wycinków zestaw danych. <br/><br/>Aby uzyskać więcej informacji, zobacz [zestawie danych zasad](#Policy) sekcji. |Nie |Nie dotyczy |

Każda kolumna hello **struktury** sekcja zawiera hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa kolumny hello. |Tak |
| type |Typ danych kolumny hello.  |Nie |
| Kultury |.NET na podstawie toobe kultura używana, gdy typ jest określona i jest typ architektury .NET `Datetime` lub `Datetimeoffset`. Domyślnie jest `en-us`. |Nie |
| Format |Format ciągu toobe używany, gdy typ jest określona i jest typ architektury .NET `Datetime` lub `Datetimeoffset`. |Nie |

W hello poniższy przykład, hello dataset zawiera trzy kolumny `slicetimestamp`, `projectname`, i `pageviews` i są typu: String, typ String i dziesiętnych odpowiednio.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Witaj poniższej tabeli opisano właściwości można używać w hello **dostępności** sekcji:

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| frequency |Określa jednostkę czasu hello w środowisku produkcyjnym wycinek zestawu danych.<br/><br/><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca |Tak |Nie dotyczy |
| interval |Określa mnożnik częstotliwości<br/><br/>"Interwał częstotliwości x" Określa, jak często hello wycinek jest generowany.<br/><br/>Należy hello podzielona na godzinę toobe zestawu danych, należy ustawić <b>częstotliwość</b> za<b>godzina</b>, i <b>interwał</b> za<b>1</b>.<br/><br/><b>Uwaga</b>: Jeśli określisz częstotliwość co minutę, firma Microsoft zaleca ustawienie hello interwał toono mniej niż 15 |Tak |Nie dotyczy |
| Styl |Określa, czy wycinek hello powinien zostać utworzony w hello rozpoczęcia/zakończenia hello interwału.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Jeśli częstotliwość ustawiono tooMonth i styl jest ustawiony tooEndOfInterval, wycinek hello jest realizowane na powitania ostatni dzień miesiąca. Jeśli hello styl jest ustawiony tooStartOfInterval, wycinek hello jest realizowane na powitania pierwszego dnia miesiąca.<br/><br/>Jeśli częstotliwość ustawiono tooDay i styl jest ustawiony tooEndOfInterval, wycinek hello jest tworzona w hello ostatniej godziny hello dnia.<br/><br/>Jeśli częstotliwość ustawiono tooHour i styl jest ustawiony tooEndOfInterval, wycinek hello jest generowany na końcu hello hello godzinę. Na przykład dla wycinka okres 13: 00 – 14: 00, wycinek hello jest generowany na 14: 00. |Nie |EndOfInterval |
| anchorDateTime |Definiuje położenie bezwzględne hello w czasie używana przez granice wycinek dataset toocompute harmonogramu. <br/><br/><b>Uwaga</b>: hello AnchorDateTime ma części daty, które są bardziej szczegółowego niż częstotliwość hello następnie hello części bardziej szczegółowego są ignorowane. <br/><br/>Na przykład, jeśli hello <b>interwał</b> jest <b>co godzinę</b> (częstotliwość: godzinę i interwał: 1) i hello <b>AnchorDateTime</b> zawiera <b>minut i sekund</b>następnie hello <b>minut i sekund</b> części hello AnchorDateTime są ignorowane. |Nie |01/01/0001 |
| Przesunięcie |Zakres czasu, przez który hello przesunięte początku i końcu wszystkie fragmenty zestawu danych. <br/><br/><b>Uwaga</b>: Jeśli jest określony zarówno anchorDateTime, jak i przesunięcie wynik hello jest shift hello połączone. |Nie |Nie dotyczy |

Określa powitania po sekcji dostępności tego zestawu danych wyjściowych hello jest utworzonych co godzinę (lub) danych wejściowych co godzinę zestaw danych jest dostępne:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Witaj **zasad** sekcja w definicji zestawu danych definiuje kryteria hello lub konieczne jest spełnienie warunku hello hello wycinków zestaw danych.

| Nazwa zasad | Opis | Stosowane za| Wymagane | Domyślne |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Sprawdza poprawność danych hello w **obiektów blob platformy Azure** spełnia hello wymagań minimalny rozmiar (w MB). |Obiekt bob Azure |Nie |Nie dotyczy |
| minimumRows |Sprawdza poprawność danych hello w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera hello minimalną liczbę wierszy. |<ul><li>Usługa Azure SQL Database</li><li>Tabeli platformy Azure</li></ul> |Nie |Nie dotyczy |

**Przykład:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

Jeśli zestaw danych jest tworzonym przez fabryki danych Azure, powinien być oznaczony jako **zewnętrznych**. To ustawienie dotyczy wejść toohello pierwszy aktywności w potoku, chyba że działania lub łańcucha potoku jest używany.

| Nazwa | Opis | Wymagane | Wartość domyślna |
| --- | --- | --- | --- |
| dataDelay |Sprawdzenie hello toodelay czasu dostępności hello hello danych zewnętrznych dla hello podane wycinka. Na przykład jeśli hello są dostępne dane co godzinę, dane zewnętrzne hello toosee wyboru hello jest dostępny i hello odpowiedniego wycinek jest gotowy można opóźnić przy użyciu dataDelay.<br/><br/>Ma zastosowanie tylko toohello obecny czas.  Na przykład jeśli 1:00 PM od razu i ta wartość to 10 minut, weryfikacji hello rozpoczyna się od 1:22:00.<br/><br/>To ustawienie nie ma wpływu na wycinki hello ostatnich (wycinków z godzina zakończenia wycinek + dataDelay < teraz) są przetwarzane bez opóźnień.<br/><br/>Czasu większą niż 23:59 godziny wymagają toospecified przy użyciu hello `day.hours:minutes:seconds` format. Na przykład toospecify 24 godziny, nie używaj 24:00:00; Zamiast tego należy użyć 1.00:00:00. Jeśli używasz 24:00:00, będzie traktowane jako 24 dni (24.00:00:00). 1 dzień i 4 godziny Określ 1:04:00:00. |Nie |0 |
| retryInterval |czas oczekiwania Hello między błędu i hello dalej ponowienia próby. W przypadku niepowodzenia spróbuj następnej próbie hello jest po retryInterval. <br/><br/>Jeśli jest 1:00 PM od razu, możemy rozpocząć hello pierwszej próby. W przypadku 1 minutę i nie można wykonać operacji hello hello czas trwania toocomplete hello pierwsze sprawdzanie poprawności hello Następna ponowna próba nastąpi na 1:00 1 min (czas trwania) + 1 min (interwał ponawiania) = 13:02:00. <br/><br/>Wycinki w przeszłości hello nie ma żadnego opóźnienia. Ponów próbę Hello odbywa się natychmiast. |Nie |00:01:00 (1 minuta) |
| retryTimeout |Witaj limitu czasu dla każdego ponowienia próby.<br/><br/>Jeśli ta właściwość jest ustawiona minut too10 hello toobe potrzeb Weryfikacja zakończona w ciągu 10 minut. Jeśli trwa dłużej niż 10 minut tooperform hello weryfikacji, hello ponów limit.<br/><br/>Jeśli upłynie limit czasu wszystkie próby dla weryfikacji hello, wycinek hello jest oznaczona jako upłynął limit czasu. |Nie |00:10:00 (10 minut) |
| maximumRetry |Liczba toocheck dostępności hello hello danych zewnętrznych. Witaj dozwolone, wartość maksymalna to 10. |Nie |3 |


## <a name="data-stores"></a>MAGAZYNY DANYCH
Witaj [połączona usługa](#linked-service) opisy sekcji określone dla elementów JSON, które są typowe tooall typów połączonych usług. Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są określone tooeach magazynu danych.

Witaj [Dataset](#dataset) opisy sekcji określone dla elementów JSON, które są najczęściej spotykane typy tooall zestawów danych. Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są określone tooeach magazynu danych.

Witaj [działania](#activity) opisy sekcji określone dla elementów JSON, które są tooall typowych działań. Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są określone tooeach magazynu danych, gdy jest używany jako źródło/ujście w działaniu kopiowania.  

Kliknij łącze hello magazynu hello interesuje schematów JSON hello toosee dla połączonej usługi, zestaw danych i hello źródło/ujście dla aktywności kopiowania hello.

| Kategoria | Magazyn danych 
|:--- |:--- |
| **Azure** |[Azure Blob Storage](#azure-blob-storage) |
| &nbsp; |[Azure Data Lake Store](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Database](#azure-sql-database) |
| &nbsp; |[Magazyn danych SQL Azure](#azure-sql-data-warehouse) |
| &nbsp; |[Azure Search](#azure-search) |
| &nbsp; |[Azure Table storage](#azure-table-storage) |
| **Bazy danych** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **Plik** |[Amazon S3](#amazon-s3) |
| &nbsp; |[System plików](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Inne** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Tabela sieci Web](#web-table) |

## <a name="azure-blob-storage"></a>Azure Blob Storage

### <a name="linked-service"></a>Połączona usługa
Istnieją dwa typy połączonych usług: połączonej usługi magazynu Azure i połączonej usługi magazynu Azure sygnatury dostępu Współdzielonego.

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu hello **klucz konta**, Utwórz połączoną usługą magazynu Azure. toodefine usługi Azure Storage połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureStorage**. Następnie można określić następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| Parametry połączenia |Określ informacje niezbędne tooconnect tooAzure magazynu dla właściwości connectionString hello. |Tak |

##### <a name="example"></a>Przykład  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Połączonej usługi magazynu Azure SAS
Hello SAS magazynu Azure połączone usługi umożliwia toolink fabryki danych Azure tooan konta magazynu Azure za pomocą udostępnionego podpis dostępu (SAS). Zapewnia fabryki danych hello dostęp ograniczony/czas-powiązane z określonego/tooall zasobów (kontener/obiektów blob) w magazynie hello. toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu sygnatura dostępu współdzielonego, Utwórz usługę połączone SAS magazynu Azure. toodefine SAS magazynu Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**element AzureStorageSas**. Następnie można określić następujące właściwości w hello **typeProperties** sekcji:   

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| sasUri |Określ zasoby usługi Azure Storage toohello udostępnionych URI sygnatury dostępu obiektu blob, kontenera lub tabeli. |Tak |

##### <a name="example"></a>Przykład

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika usługi Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych obiektów Blob platformy Azure, zestawu hello **typu** hello DataSet za**AzureBlob**. Następnie określ następujące właściwości specyficzne dla obiektów Blob platformy Azure w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Ścieżka toohello kontenera i folderu w magazynie obiektów blob hello. Przykład: myblobcontainer\myblobfolder\ |Tak |
| fileName |Nazwa obiektu blob hello. Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.<br/><br/>Jeśli określono nazwę pliku, hello działania (takie jak kopiowanie) działa na hello konkretnego obiektu Blob.<br/><br/>Jeśli nie określono nazwy pliku, kopiowania obejmuje wszystkie obiekty BLOB w hello folderPath dla zestawu danych wejściowych.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: danych. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| partitionedBy |partitionedBy jest opcjonalna właściwość. Umożliwia toospecify folderPath dynamiczne i nazwę pliku dla czasu serii danych. Na przykład folderPath mogą nadać parametry dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) artykułu.

### <a name="blobsource-in-copy-activity"></a>BlobSource w przypadku działania kopiowania
Jeśli dane są kopiowane z magazynu obiektów Blob platformy Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**BlobSource**i określ następujące właściwości w hello ** źródła ** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |TRUE, False (wartość domyślna) |Nie |

#### <a name="example-blobsource"></a>Przykład: BlobSource **
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink w przypadku działania kopiowania
Jeśli kopiujesz tooan danych magazynu obiektów Blob Azure, należy ustawić hello **typu sink** hello skopiować działania za**BlobSink**i określ następujące właściwości w hello **zbiornika** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| copyBehavior |Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików. |<b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello. Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.<br/><br/><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello znajdują się w hello najpierw poziomu folderu docelowego. pliki docelowe Hello ma automatycznie wygeneruje nazwę. <br/><br/><b>MergeFiles (domyślnie):</b> scala wszystkie pliki z pliku tooone folderu źródłowego hello. Jeśli określono hello nazwa pliku/obiektu Blob, nazwa pliku scalonych hello będzie hello określoną nazwą; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie. |Nie |

#### <a name="example-blobsink"></a>Przykład: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Blob](data-factory-azure-blob-connector.md#copy-activity-properties) artykułu. 

## <a name="azure-data-lake-store"></a>Azure Data Lake Store

### <a name="linked-service"></a>Połączona usługa
toodefine usługi Azure Data Lake Store połączony zestaw typu hello hello połączona usługa zbyt**AzureDataLakeStore**, a następnie określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type | musi mieć ustawioną właściwość type Hello: **AzureDataLakeStore** | Tak |
| dataLakeStoreUri | Określ informacje o hello konta usługi Azure Data Lake Store. Jest on zgodny z formatem hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` lub `adl://[accountname].azuredatalakestore.net/`. | Tak |
| subscriptionId | Należy subskrypcji platformy Azure toowhich identyfikator usługi Data Lake Store. | Wymagany dla odbiorcy |
| Grupy zasobów o nazwie | Należy toowhich Nazwa grupy zasobów platformy Azure Data Lake Store. | Wymagany dla odbiorcy |
| servicePrincipalId | Określ identyfikator aplikacji hello klienta. | Tak (dla uwierzytelniania głównej usługi) |
| servicePrincipalKey | Określ klucz aplikacji hello. | Tak (dla uwierzytelniania głównej usługi) |
| Dzierżawy | Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja. Można go pobrać aktywowania myszy hello w hello prawym górnym rogu hello portalu Azure. | Tak (dla uwierzytelniania głównej usługi) |
| Autoryzacji | Kliknij przycisk **autoryzacji** przycisku na powitania **Edytor fabryki danych** , a następnie wprowadź Twoje poświadczenia przypisującej hello automatycznie generowanej autoryzacji adresu URL toothis właściwości. | Tak (do uwierzytelniania poświadczeń użytkownika)|
| Identyfikator sesji | Identyfikator sesji OAuth z sesji autoryzacji OAuth hello. Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz. To ustawienie jest generowane automatycznie, gdy używasz Edytor fabryki danych. | Tak (do uwierzytelniania poświadczeń użytkownika) |

#### <a name="example-using-service-principal-authentication"></a>Przykład: przy użyciu uwierzytelniania głównej usługi
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Przykład: przy użyciu uwierzytelniania poświadczeń użytkownika
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych usługi Azure Data Lake Store hello zestaw **typu** hello DataSet za**AzureDataLakeStore**i określ następujące właściwości w hello hello **typeProperties**sekcji: 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| folderPath |Ścieżka toohello kontenera i folderu w hello Azure Data Lake magazynu. |Tak |
| fileName |Nazwa pliku hello w hello Azure Data Lake store. Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter. <br/><br/>Jeśli określono nazwę pliku, hello działania (w tym kopiowania) działa na powitania określonego pliku.<br/><br/>Jeśli nie określono nazwy pliku, kopia zawiera wszystkie pliki w hello folderPath dla zestawu danych wejściowych.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: danych. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| partitionedBy |partitionedBy jest opcjonalna właściwość. Umożliwia toospecify folderPath dynamiczne i nazwę pliku dla czasu serii danych. Na przykład folderPath mogą nadać parametry dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

#### <a name="example"></a>Przykład
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties) artykułu. 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Źródło usługi Azure Data Lake Store w przypadku działania kopiowania
Jeśli dane są kopiowane z usługi Azure Data Lake Store, ustaw hello **typ źródła** hello skopiować działania zbyt**AzureDataLakeStoreSource**i określ następujące właściwości w hello **źródła**  sekcji:

**AzureDataLakeStoreSource** obsługuje następujące właściwości hello **typeProperties** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |TRUE, False (wartość domyślna) |Nie |

#### <a name="example-azuredatalakestoresource"></a>Przykład: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties) artykułu.

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Obiekt Sink usługi Azure Data Lake Store w przypadku działania kopiowania
Kopiowania danych tooan Azure Data Lake Store, ustaw hello **typu sink** hello skopiować działania zbyt**AzureDataLakeStoreSink**i określ następujące właściwości w hello **zbiornika**sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| copyBehavior |Określa zachowanie kopii hello. |<b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello. Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.<br/><br/><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom folderu docelowego. pliki docelowe Hello są tworzone z nazwą automatycznie generowane.<br/><br/><b>MergeFiles</b>: scala wszystkie pliki z pliku tooone folderu źródłowego hello. Jeśli określono hello nazwa pliku/obiektu Blob, nazwa pliku scalonych hello będzie hello określoną nazwą; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie. |Nie |

#### <a name="example-azuredatalakestoresink"></a>Przykład: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties) artykułu. 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Połączona usługa
toodefine bazy danych Azure rozwiązania Cosmos połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**DocumentDb**i określ następujące właściwości w hello **typeProperties** sekcja:  

| **Właściwość** | **Opis** | **Wymagane** |
| --- | --- | --- |
| Parametry połączenia |Określ informacje niezbędne tooconnect tooAzure DB rozwiązania Cosmos w bazie danych. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych bazy danych Azure rozwiązania Cosmos hello zestaw **typu** hello DataSet za**DocumentDbCollection**i określ następujące właściwości w hello hello **typeProperties** sekcja: 

| **Właściwość** | **Opis** | **Wymagane** |
| --- | --- | --- |
| CollectionName |Nazwa hello Azure DB rozwiązania Cosmos kolekcji. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#dataset-properties) artykułu.

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Źródło kolekcji Azure rozwiązania Cosmos bazy danych w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych Azure rozwiązania Cosmos, ustaw hello **typ źródła** hello skopiować działania zbyt**DocumentDbCollectionSource**i określ następujące właściwości w hello **źródła** sekcji:


| **Właściwość** | **Opis** | **Dozwolone wartości** | **Wymagane** |
| --- | --- | --- | --- |
| query |Określ hello zapytania tooread dane. |Wyślij zapytanie do ciągu obsługuje bazy danych Azure rozwiązania Cosmos. <br/><br/>Przykład:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Nie <br/><br/>Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Tooindicate znak specjalny, który hello dokumentu jest zagnieżdżony. |Dowolny znak. <br/><br/>Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone. Fabryka danych Azure umożliwia hierarchii toodenote użytkownika za pośrednictwem nestingSeparator, czyli "." w hello powyżej przykłady. Z separatorem hello działanie kopiowania hello wygeneruje obiektu "Name" hello z trzech elementów podrzędnych elementów pierwszy, środkowy i ostatnich, zgodnie z too"Name.First", "Name.Middle" i "Name.Last" w hello definicja tabeli. |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Obiekt Sink kolekcji bazy danych Azure rozwiązania Cosmos w przypadku działania kopiowania
Jeśli kopiujesz tooAzure danych DB rozwiązania Cosmos ustawić hello **typu sink** hello skopiować działania zbyt**DocumentDbCollectionSink**i określ następujące właściwości w hello **zbiornika**sekcji:

| **Właściwość** | **Opis** | **Dozwolone wartości** | **Wymagane** |
| --- | --- | --- | --- |
| nestingSeparator |Wymagany jest znak specjalny w tooindicate nazwa kolumny źródła hello, który zagnieżdżone dokumentu. <br/><br/>Na przykład powyżej: `Name.First` w danych wyjściowych hello tabeli tworzy hello następującej strukturze JSON w dokumencie DB rozwiązania Cosmos hello:<br/><br/>"Nazwa": {<br/>    "Pierwszy": "Jan"<br/>}, |Znak, który jest używany tooseparate poziomów zagnieżdżenia.<br/><br/>Wartość domyślna to `.` (kropką). |Znak, który jest używany tooseparate poziomów zagnieżdżenia. <br/><br/>Wartość domyślna to `.` (kropką). |
| writeBatchSize |Liczba równoległe żądań tooAzure DB rozwiązania Cosmos usługi toocreate dokumentów.<br/><br/>Aby precyzyjnie zdefiniować hello wydajności podczas kopiowania danych z bazy danych rozwiązania Cosmos Azure przy użyciu tej właściwości. Wraz ze zwiększeniem writeBatchSize, ponieważ więcej żądań równoległych tooAzure rozwiązania Cosmos bazy danych są wysyłane, może spodziewać się lepszą wydajność. Jednak potrzebny tooavoid ograniczania przepustowości, który może zgłaszać komunikat o błędzie hello: "jest duża szybkość żądania".<br/><br/>Ograniczanie zadecyduje o wiele czynników, w tym rozmiar dokumentów, liczbę dokumentów, indeksowania zasady kolekcji docelowej, itd. Operacje kopiowania, można użyć lepsze hello toohave kolekcji (na przykład S3) większości dostępna przepustowość (2500 żądań jednostek na sekundę). |Liczba całkowita |Nie (domyślne: 5) |
| writeBatchTimeout |Czas toocomplete operacji hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#copy-activity-properties) artykułu.

## <a name="azure-sql-database"></a>Usługa Azure SQL Database

### <a name="linked-service"></a>Połączona usługa
toodefine bazy danych SQL Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDatabase**i określ następujące właściwości w hello **typeProperties**sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Parametry połączenia |Określ informacje niezbędne wystąpienie bazy danych SQL Azure toohello tooconnect hello właściwości connectionString. |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych usługi Azure SQL Database hello zestaw **typu** hello DataSet za**AzureSqlTable**i określ następujące właściwości w hello hello **typeProperties** sekcja: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Azure hello, która jest połączona usługa odnosi się do. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) artykułu. 

### <a name="sql-source-in-copy-activity"></a>Źródło SQL w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych SQL Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**SqlSource**i określ następujące właściwości w hello **źródła** sekcja:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Przykład: `select * from MyTable`. |Nie |
| sqlReaderStoredProcedureName |Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties) artykułu. 

### <a name="sql-sink-in-copy-activity"></a>Obiekt Sink SQL w przypadku działania kopiowania
Jeśli kopiujesz tooAzure danych bazy danych SQL, ustaw hello **typu sink** hello skopiować działania zbyt**SqlSink**i określ następujące właściwości w hello **zbiornika** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. |Instrukcja zapytania. |Nie |
| sliceIdentifierColumnName |Określ nazwę kolumny dla działania kopiowania toofill o identyfikatorze wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia. |Nazwa kolumny kolumnę o typie danych binary(32). |Nie |
| sqlWriterStoredProcedureName |Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |
| sqlWriterTableType |Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane. Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli. Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi. |Nazwa typu tabeli. |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties) artykułu. 

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse

### <a name="linked-service"></a>Połączona usługa
toodefine Azure SQL Data Warehouse połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDW**i określ następujące właściwości w hello **typeProperties**sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Parametry połączenia |Określ informacje potrzebne wystąpienia usługi Azure SQL Data Warehouse toohello tooconnect hello właściwości connectionString. |Tak |



#### <a name="example"></a>Przykład

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych usługi Azure SQL Data Warehouse hello zestaw **typu** hello DataSet za**AzureSqlDWTable**i określ następujące właściwości w hello hello **typeProperties**sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa hello tabeli lub widoku w bazie danych Azure SQL Data Warehouse hello, który hello połączonej usługi odwołuje się do. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) artykułu. 

### <a name="sql-dw-source-in-copy-activity"></a>Źródła magazynu danych SQL w przypadku działania kopiowania
Jeśli dane są kopiowane z magazynu danych SQL Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**SqlDWSource**i określ następujące właściwości w hello **źródła**sekcji:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. |Nie |
| sqlReaderStoredProcedureName |Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artykułu. 

### <a name="sql-dw-sink-in-copy-activity"></a>Ujścia magazynu danych SQL w przypadku działania kopiowania
Jeśli kopiujesz tooAzure danych magazynu danych SQL, ustaw hello **typu sink** hello skopiować działania zbyt**SqlDWSink**i określ następujące właściwości w hello **ujścia** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. |Instrukcja zapytania. |Nie |
| allowPolyBase |Wskazuje, czy toouse PolyBase (jeśli jest to wymagane) zamiast BULKINSERT mechanizmu. <br/><br/> **Przy użyciu programu PolyBase jest hello zalecany sposób tooload danych do usługi SQL Data Warehouse.** |True <br/>Wartość FAŁSZ (ustawienie domyślne) |Nie |
| Usługi |Grupa właściwości, które można określić podczas hello **allowPolybase** właściwość jest ustawiona zbyt**true**. |&nbsp; |Nie |
| rejectValue |Określa numer hello lub procent wierszy, które można odrzucić przed hello działanie nie powiodło się. <br/><br/>Dowiedz się więcej na temat hello PolyBase Odrzuć opcje w hello **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu. |0 (domyślnie), 1, 2... |Nie |
| dla właściwości rejectType |Określa, czy opcja rejectValue hello jest określona jako wartość literału lub wartość procentowa. |Wartość (ustawienie domyślne), wartość procentowa |Nie |
| rejectSampleValue |Określa liczbę hello tooretrieve wierszy przed hello PolyBase ponownie oblicza hello procent odrzuconych wierszy. |1, 2, … |Tak, jeśli **dla właściwości rejectType** jest **procent** |
| useTypeDefault |Określa, jak toohandle brakujących wartości w rozdzielane pliki tekstowe po programie PolyBase pobiera dane z pliku tekstowego hello.<br/><br/>Dowiedz się więcej o tej właściwości z sekcji argumenty hello w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |Wartość true, False (ustawienie domyślne) |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artykułu. 

## <a name="azure-search"></a>Azure Search

### <a name="linked-service"></a>Połączona usługa
toodefine usługi Azure Search połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSearch**i określ następujące właściwości w hello **typeProperties** sekcja:  

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| adres URL | Adres URL hello usługi Azure Search. | Tak |
| key | Klucz administratora dla hello usługi Azure Search. | Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych usługi Azure Search hello zestaw **typu** hello DataSet za**AzureSearchIndex**i określ następujące właściwości w hello hello **typeProperties** sekcji : 

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| type | zbyt należy ustawić właściwość typu Hello**AzureSearchIndex**.| Tak |
| indexName | Nazwa indeksu usługi Azure Search hello. Fabryki danych nie powoduje utworzenia hello indeksu. Indeks Hello musi istnieć w usłudze Azure Search. | Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#dataset-properties) artykułu.

### <a name="azure-search-index-sink-in-copy-activity"></a>Obiekt Sink indeksu usługi Azure Search w przypadku działania kopiowania
Jeśli kopiujesz indeksu usługi Azure Search tooan danych, ustaw hello **typu sink** hello skopiować działania zbyt**AzureSearchIndexSink**i określ następujące właściwości w hello **zbiornika**sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Określa, czy toomerge lub Zastąp, gdy dokument już istnieje w indeksie hello. | Merge (ustawienie domyślne)<br/>Upload| Nie |
| writeBatchSize | Przekazywanie danych do indeksu usługi Azure Search hello, gdy osiągnie rozmiar buforu hello writeBatchSize. | 1 too1 000. Wartość domyślna to 1000. | Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#copy-activity-properties) artykułu.

## <a name="azure-table-storage"></a>Azure Table Storage

### <a name="linked-service"></a>Połączona usługa
Istnieją dwa typy połączonych usług: połączonej usługi magazynu Azure i połączonej usługi magazynu Azure sygnatury dostępu Współdzielonego.

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu hello **klucz konta**, Utwórz połączoną usługą magazynu Azure. toodefine usługi Azure Storage połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureStorage**. Następnie można określić następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |musi mieć ustawioną właściwość type Hello: **AzureStorage** |Tak |
| Parametry połączenia |Określ informacje niezbędne tooconnect tooAzure magazynu dla właściwości connectionString hello. |Tak |

**Przykład:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Połączonej usługi magazynu Azure SAS
Hello SAS magazynu Azure połączone usługi umożliwia toolink fabryki danych Azure tooan konta magazynu Azure za pomocą udostępnionego podpis dostępu (SAS). Zapewnia fabryki danych hello dostęp ograniczony/czas-powiązane z określonego/tooall zasobów (kontener/obiektów blob) w magazynie hello. toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu sygnatura dostępu współdzielonego, Utwórz usługę połączone SAS magazynu Azure. toodefine SAS magazynu Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**element AzureStorageSas**. Następnie można określić następujące właściwości w hello **typeProperties** sekcji:   

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |musi mieć ustawioną właściwość type Hello: **element AzureStorageSas** |Tak |
| sasUri |Określ zasoby usługi Azure Storage toohello udostępnionych URI sygnatury dostępu obiektu blob, kontenera lub tabeli. |Tak |

**Przykład:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestaw tabel Azure hello zestaw **typu** hello DataSet za**AzureTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w wystąpieniu bazy danych tabeli Azure hello, która jest połączona usługa odnosi się do. |Tak. TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego. Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego. |

#### <a name="example"></a>Przykład

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#dataset-properties) artykułu. 

### <a name="azure-table-source-in-copy-activity"></a>Źródło tabeli platformy Azure w przypadku działania kopiowania
Jeśli dane są kopiowane z magazynu tabel Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**AzureTableSource**i określ następujące właściwości w hello **źródła**sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| azureTableSourceQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania tabeli platformy Azure. Przykłady w następnej sekcji hello. |Nie. TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego. Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego. |
| azureTableSourceIgnoreTableNotFound |Wskazuje, czy wyjątek hello swallow tabeli nie istnieją. |WARTOŚĆ TRUE<br/>WARTOŚĆ FALSE |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties) artykułu. 

### <a name="azure-table-sink-in-copy-activity"></a>Obiekt Sink tabeli platformy Azure w przypadku działania kopiowania
Jeśli kopiujesz tooAzure danych magazynu tabel, ustaw hello **typu sink** hello skopiować działania zbyt**AzureTableSink**i określ następujące właściwości w hello **ujścia** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Domyślna wartość klucza partycji, które mogą być używane przez obiekt sink hello. |Wartość ciągu. |Nie |
| azureTablePartitionKeyName |Określ nazwę kolumny hello, których wartości są używane jako klucze partycji. Jeśli nie zostanie określony, AzureTableDefaultPartitionKeyValue jest używana jako klucza partycji hello. |Nazwa kolumny. |Nie |
| azureTableRowKeyName |Określ nazwę kolumny hello, w których wartości kolumn używanych jako klucz wiersza. Jeśli nie zostanie określony, użyj identyfikatora GUID dla każdego wiersza. |Nazwa kolumny. |Nie |
| azureTableInsertType |Tryb Hello tooinsert dane w tabeli platformy Azure.<br/><br/>Ta właściwość określa, czy wartości zastąpienia lub scalić zostać istniejących wierszy w tabeli wyników hello ze zgodnymi kluczami partycji i wiersza. <br/><br/>toolearn informacji na temat tych ustawień (scalania i Zastąp) działania, zobacz [wstawienia lub scalania jednostki](https://msdn.microsoft.com/library/azure/hh452241.aspx) i [wstawienia lub Zastąp jednostki](https://msdn.microsoft.com/library/azure/hh452242.aspx) tematów. <br/><br> To ustawienie jest stosowane na poziomie wiersza hello, nie poziomu tabeli hello i żadna z tych opcji usuwa wiersze w tabeli wyników hello, które nie istnieją w danych wejściowych hello. |Merge (ustawienie domyślne)<br/>Zamień |Nie |
| writeBatchSize |Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| writeBatchTimeout |Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout |Zakres czasu<br/><br/>Przykład: "00:20:00" (20 minut) |Nie (domyślna toostorage klienta domyślny limit czasu operacji wartość 90 s) |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties) artykułu. 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>Połączona usługa
toodefine Redshift Amazon połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AmazonRedshift**i określ następujące właściwości w hello **typeProperties**sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Adres IP lub hosta nazwę hello Amazon Redshift serwera. |Tak |
| port |Witaj liczbę hello port TCP, którego hello Amazon Redshift serwer używa toolisten dla połączeń klienta. |Nie, wartość domyślna: 5439 |
| Bazy danych |Nazwa bazy danych usługi Amazon Redshift hello. |Tak |
| nazwa użytkownika |Nazwa użytkownika, który ma toohello dostępu do bazy danych. |Tak |
| hasło |Hasło dla konta użytkownika hello. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych usługi Amazon Redshift hello zestaw **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcja: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w bazie danych usługi Amazon Redshift hello, których połączonej usługi odwołuje się do. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |


#### <a name="example"></a>Przykład

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties) artykułu.

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania 
Jeśli dane są kopiowane z Amazon Redshift, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. |Nie (Jeśli **tableName** z **dataset** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties) artykułu.

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Połączona usługa
toodefine IBM DB2 połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesDB2**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Nazwa serwera hello bazy danych DB2. |Tak |
| Bazy danych |Nazwa bazy danych hello DB2. |Tak |
| Schemat |Nazwa schematu hello hello bazy danych. Nazwa schematu Hello jest rozróżniana wielkość liter. |Nie |
| Typ authenticationType |Typ uwierzytelniania używany toohello tooconnect bazy danych DB2. Możliwe wartości to: anonimowe, podstawowe i systemu Windows. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych DB2. |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine bazy danych DB2 zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w wystąpieniu bazy danych DB2 hello, która jest połączona usługa odnosi się do. Witaj tableName jest rozróżniana wielkość liter. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) 

#### <a name="example"></a>Przykład
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties) artykułu.

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z IBM DB2, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcji:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `"query": "select * from "MySchema"."MyTable""`. |Nie (Jeśli **tableName** z **dataset** jest określona) |

#### <a name="example"></a>Przykład
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties) artykułu.

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Połączona usługa
toodefine MySQL połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesMySql**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Nazwa serwera MySQL hello. |Tak |
| Bazy danych |Nazwa bazy danych MySQL hello. |Tak |
| Schemat |Nazwa schematu hello hello bazy danych. |Nie |
| Typ authenticationType |Typ uwierzytelniania używany toohello tooconnect baza danych MySQL. Możliwe wartości to: `Basic`. |Tak |
| nazwa użytkownika |Określ bazy danych MySQL toohello tooconnect nazwy użytkownika. |Tak |
| hasło |Określ hasło dla konta użytkownika hello określona. |Tak |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych MySQL. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych MySQL, zestaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w hello wystąpienie bazy danych MySQL, odnoszący się do połączonej usługi. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#dataset-properties) artykułu. 

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych MySQL, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. |Nie (Jeśli **tableName** z **dataset** jest określona) |


#### <a name="example"></a>Przykład
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties) artykułu. 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Połączona usługa
toodefine Oracle połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesOracle**i określ następujące właściwości w hello **typeProperties** sekcja:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| driverType | Określ, które sterownik toouse toocopy dane z / tooOracle bazy danych. Dozwolone wartości to **Microsoft** lub **ODP** (ustawienie domyślne). Zobacz [obsługiwanych wersji i instalacji](#supported-versions-and-installation) sekcji Szczegóły sterownika. | Nie |
| Parametry połączenia | Określ informacje niezbędne wystąpienie bazy danych Oracle toohello tooconnect hello właściwości connectionString. | Tak |
| gatewayName | Nazwa bramy hello, że jest używana tooconnect toohello lokalnego serwera Oracle |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych Oracle hello zestaw **typu** hello DataSet za**OracleTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Oznacza nazwę tabeli hello na powitania hello połączonej usługi bazy danych programu Oracle. |Nie (Jeśli **oracleReaderQuery** z **OracleSource** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#dataset-properties) artykułu.

### <a name="oracle-source-in-copy-activity"></a>Oracle źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych Oracle, ustaw hello **typ źródła** hello skopiować działania zbyt**OracleSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| oracleReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable` <br/><br/>Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana:`select * from MyTable` |Nie (Jeśli **tableName** z **dataset** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties) artykułu.

### <a name="oracle-sink-in-copy-activity"></a>Obiekt Sink Oracle w przypadku działania kopiowania
Kopiowania bazy danych Oracle tooam danych, ustaw hello **typu sink** hello skopiować działania zbyt**OracleSink**i określ następujące właściwości w hello **zbiornika** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: 00:30:00 (30 minut). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 100) |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. |Instrukcja zapytania. |Nie |
| sliceIdentifierColumnName |Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia. |Nazwa kolumny kolumnę o typie danych binary(32). |Nie |

#### <a name="example"></a>Przykład
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties) artykułu.

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Połączona usługa
toodefine PostgreSQL połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesPostgreSql**i określ następujące właściwości w hello **typeProperties**sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Nazwa serwera PostgreSQL hello. |Tak |
| Bazy danych |Nazwa bazy danych PostgreSQL hello. |Tak |
| Schemat |Nazwa schematu hello hello bazy danych. Nazwa schematu Hello jest rozróżniana wielkość liter. |Nie |
| Typ authenticationType |Typ uwierzytelniania używany tooconnect toohello PostgreSQL w bazie danych. Możliwe wartości to: anonimowe, podstawowe i systemu Windows. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych PostgreSQL. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine PostgreSQL zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w hello wystąpienie bazy danych PostgreSQL, odnoszący się do połączonej usługi. Witaj tableName jest rozróżniana wielkość liter. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |

#### <a name="example"></a>Przykład
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties) artykułu.

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych programu PostgreSQL, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: "zapytania": "Wybierz * z \"MySchema\".\" MyTable\"". |Nie (Jeśli **tableName** z **dataset** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties) artykułu.

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Połączona usługa
toodefine SAP Business magazynu (BW) połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**SapBw**i określ następujące właściwości w hello **typeProperties**sekcji:  

Właściwość | Opis | Dozwolone wartości | Wymagane
-------- | ----------- | -------------- | --------
serwer | Nazwa serwera hello, na które hello programu SAP BW znajduje się wystąpienie. | Ciąg | Tak
systemNumber | Numer systemu hello systemu SAP BW. | Liczba dziesiętna dwucyfrowe reprezentowany jako ciąg. | Tak
clientId | Identyfikator klienta na powitania klienta w hello systemu SAP W. | Trzycyfrowa liczba dziesiętna reprezentowany jako ciąg. | Tak
nazwa użytkownika | Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera | Ciąg | Tak
hasło | Hasło dla użytkownika hello. | Ciąg | Tak
gatewayName | Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego programu SAP BW wystąpienia. | Ciąg | Tak
encryptedCredential | Witaj zaszyfrowanego ciągu poświadczeń. | Ciąg | Nie

#### <a name="example"></a>Przykład

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine programu SAP BW zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**. Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych z programu SAP BW hello typu **RelationalTable**.  

#### <a name="example"></a>Przykład

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties) artykułu. 

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z SAP Business Warehouse, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query | Określa dane tooread zapytania MDX hello z wystąpienia programu SAP BW hello. | Zapytania MDX. | Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) artykułu. 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Połączona usługa
toodefine SAP HANA połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**SapHana**i określ następujące właściwości w hello **typeProperties** sekcji:  

Właściwość | Opis | Dozwolone wartości | Wymagane
-------- | ----------- | -------------- | --------
serwer | Nazwa serwera hello, na które hello SAP HANA znajduje się wystąpienie. Jeśli serwer używa portu dostosowane, określ `server:port`. | Ciąg | Tak
Typ authenticationType | Typ uwierzytelniania. | Ciąg. "Basic" lub "Windows" | Tak 
nazwa użytkownika | Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera | Ciąg | Tak
hasło | Hasło dla użytkownika hello. | Ciąg | Tak
gatewayName | Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego SAP HANA wystąpienia. | Ciąg | Tak
encryptedCredential | Witaj zaszyfrowanego ciągu poświadczeń. | Ciąg | Nie

#### <a name="example"></a>Przykład

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties) artykułu.
 
### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych SAP HANA, zestaw hello **typu** hello DataSet za**RelationalTable**. Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP HANA hello typu **RelationalTable**. 

#### <a name="example"></a>Przykład

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#dataset-properties) artykułu. 

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z magazynu danych SAP HANA, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query | Określa hello SQL tooread dane z wystąpieniem SAP HANA hello. | Zapytanie SQL. | Tak |


#### <a name="example"></a>Przykład


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties) artykułu.


## <a name="sql-server"></a>Oprogramowanie SQL Server

### <a name="linked-service"></a>Połączona usługa
Tworzenie połączonej usługi typu **OnPremisesSqlServer** toolink fabrykę danych tooa bazy danych programu SQL Server lokalne. Hello w poniższej tabeli przedstawiono opis dla usługi programu SQL Server połączone określonych lokalnych tooon elementy JSON.

Witaj w poniższej tabeli przedstawiono opis dla określonych tooSQL elementów JSON usługi Serwer połączony.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |powinien mieć ustawioną właściwość type Hello: **OnPremisesSqlServer**. |Tak |
| Parametry połączenia |Określ informacje connectionString potrzebne tooconnect toohello lokalnej bazy danych SQL Server przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows. |Tak |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu SQL Server. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows. Przykład: **domainname\\username**. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |

Można szyfrować poświadczeń przy użyciu hello **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia hello, jak pokazano w hello poniższy przykład (**EncryptedCredential** właściwość):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Przykład: JSON dla przy użyciu uwierzytelniania programu SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Przykład: JSON dla przy użyciu uwierzytelniania systemu Windows

Jeśli podano nazwę użytkownika i hasło, brama używa ich tooimpersonate hello określonego tooconnect toohello lokalnego programu SQL Server bazy danych kont użytkowników. W przeciwnym razie nawiązanie połączenia bramy toohello programu SQL Server bezpośrednio z kontekstu zabezpieczeń hello bramy (jego konta uruchamiania).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych programu SQL Server, zestaw hello **typu** hello DataSet za**SqlServerTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Server hello, która jest połączona usługa odnosi się do. |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#dataset-properties) artykułu. 

### <a name="sql-source-in-copy-activity"></a>Źródło SQL w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych programu SQL Server, należy ustawić hello **typ źródła** hello skopiować działania zbyt**SqlSource**i określ następujące właściwości w hello **źródła** sekcja:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| sqlReaderQuery |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. Może odwoływać się wiele tabel z bazy danych hello odwołuje się hello wejściowy zestaw danych. Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana: Wybierz z MyTable. |Nie |
| sqlReaderStoredProcedureName |Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |

Jeśli hello **sqlReaderQuery** określono hello SqlSource, hello odbywa się działanie kopii tego zapytania hello bazy danych SQL Server źródła tooget hello danych.

Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

> [!NOTE]
> Jeśli używasz **sqlReaderStoredProcedureName**, należy nadal toospecify wartość dla hello **tableName** właściwości w elemencie dataset hello JSON. Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.


#### <a name="example"></a>Przykład
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

W tym przykładzie **sqlReaderQuery** dla hello SqlSource został określony. Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello danych hello tooget źródła danych programu SQL Server. Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry). Hello sqlReaderQuery można odwoływać się wiele tabel w bazie danych hello odwołuje się hello wejściowy zestaw danych. Nie jest tabelą hello ograniczone tooonly ustawione jako hello typeProperty tableName zestawu danych.

Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server. Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.

Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) artykułu. 

### <a name="sql-sink-in-copy-activity"></a>Obiekt Sink SQL w przypadku działania kopiowania
Kopiowania bazy danych programu SQL Server tooa danych, ustaw hello **typu sink** hello skopiować działania zbyt**SqlSink**i określ następujące właściwości w hello **zbiornika** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| writeBatchTimeout |Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu. |Zakres czasu<br/><br/> Przykład: "00: 30:00" (30 minut). |Nie |
| writeBatchSize |Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize. |Liczba całkowita (liczba wierszy) |Nie (domyślne: 10000) |
| sqlWriterCleanupScript |Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone. Aby uzyskać więcej informacji, zobacz [powtarzalności](#repeatability-during-copy) sekcji. |Instrukcja zapytania. |Nie |
| sliceIdentifierColumnName |Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia. Aby uzyskać więcej informacji, zobacz [powtarzalności](#repeatability-during-copy) sekcji. |Nazwa kolumny kolumnę o typie danych binary(32). |Nie |
| sqlWriterStoredProcedureName |Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello. |Nazwa hello procedury składowanej. |Nie |
| storedProcedureParameters |Parametry hello procedury składowanej. |Par nazwa/wartość. Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter. |Nie |
| sqlWriterTableType |Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane. Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli. Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi. |Nazwa typu tabeli. |Nie |

#### <a name="example"></a>Przykład
potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę. W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) artykułu. 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Połączona usługa
toodefine Sybase połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesSybase**i określ następujące właściwości w hello **typeProperties** sekcja:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Nazwa serwera programu Sybase hello. |Tak |
| Bazy danych |Nazwa bazy danych programu Sybase hello. |Tak |
| Schemat |Nazwa schematu hello hello bazy danych. |Nie |
| Typ authenticationType |Typ uwierzytelniania używany toohello tooconnect baz danych programu Sybase. Możliwe wartości to: anonimowe, podstawowe i systemu Windows. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu Sybase. |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych programu Sybase, zestaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w hello wystąpienie bazy danych programu Sybase, odnoszący się do połączonej usługi. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#dataset-properties) artykułu. 

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych programu Sybase, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. |Nie (Jeśli **tableName** z **dataset** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties) artykułu.

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Połączona usługa
toodefine Teradata połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesTeradata**i określ następujące właściwości w hello **typeProperties** sekcja:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Nazwa serwera programu Teradata hello. |Tak |
| Typ authenticationType |Typ uwierzytelniania używany toohello tooconnect bazą danych programu Teradata. Możliwe wartości to: anonimowe, podstawowe i systemu Windows. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu Teradata. |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych obiektów Teradata Blob, zestaw hello **typu** hello DataSet za**RelationalTable**. Obecnie nie ma żadnych właściwości typu, obsługiwane dla zestawu danych programu Teradata hello. 

#### <a name="example"></a>Przykład
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#dataset-properties) artykułu.

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych programu Teradata, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties) artykułu.

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Połączona usługa
toodefine Cassandra połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesCassandra**i określ następujące właściwości w hello **typeProperties** sekcja:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Host |Jeden lub więcej adresów IP lub nazw hostów serwerów Cassandra.<br/><br/>Określ rozdzielaną przecinkami listę adresów IP lub serwerów tooall tooconnect nazwy hosta jednocześnie. |Tak |
| port |Hello port TCP, którego hello Cassandra serwer używa toolisten dla połączeń klienta. |Nie, wartość domyślna: 9042 |
| Typ authenticationType |Podstawowa lub anonimowe |Tak |
| nazwa użytkownika |Określ nazwę użytkownika dla konta użytkownika hello. |Tak, jeśli authenticationType ustawiono tooBasic. |
| hasło |Określ hasło dla konta użytkownika hello. |Tak, jeśli authenticationType ustawiono tooBasic. |
| gatewayName |Nazwa Hello hello bramy, która jest używana tooconnect toohello lokalnymi Cassandra w bazie danych. |Tak |
| encryptedCredential |Poświadczenie szyfrowane przez bramę hello. |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine Cassandra zestawu danych, ustaw hello **typu** hello DataSet za**CassandraTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| przestrzeni kluczy |Nazwa schematu bazy danych Cassandra lub hello przestrzeni kluczy. |Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana). |
| tableName |Nazwa tabeli hello Cassandra bazy danych. |Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana). |

#### <a name="example"></a>Przykład

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties) artykułu. 

### <a name="cassandra-source-in-copy-activity"></a>Źródło Cassandra w przypadku działania kopiowania
Jeśli dane są kopiowane z Cassandra, ustaw hello **typ źródła** hello skopiować działania zbyt**CassandraSource**i określ następujące właściwości w hello **źródła** sekcji :

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Zapytania SQL 92 lub CQL zapytania. Zobacz [odwołania CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Korzystając z zapytania SQL, określ **nazwa name.table przestrzeni kluczy** toorepresent hello tabelę, która ma tooquery. |Nie (jeśli są zdefiniowane tableName oraz przestrzeni kluczy w zestawie danych). |
| consistencyLevel |poziomu spójności Hello Określa, ile replik musi odpowiadać żądanie odczytu tooa przed zwróceniem aplikacji klienckiej toohello danych. Sprawdzanie Cassandra hello określonej liczby replik dla żądania odczytu hello toosatisfy danych. |JEDNĄ, DWIE, TRZY, KWORUM, WSZYSTKIE, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE. Zobacz [Konfigurowanie spójność danych](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegółowe informacje. |Nie. Domyślna wartość to jeden. |

#### <a name="example"></a>Przykład
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties) artykułu.

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Połączona usługa
toodefine MongoDB połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesMongoDB**i określ następujące właściwości w hello **typeProperties** sekcja:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| serwer |Adres IP lub hosta nazwę serwera bazy danych MongoDB hello. |Tak |
| port |Port TCP, którego hello serwera bazy danych MongoDB używa toolisten dla połączeń klienta. |Opcjonalne, wartość domyślna: 27017 |
| Typ authenticationType |Podstawowy, lub anonimowe. |Tak |
| nazwa użytkownika |Tooaccess konta użytkownika bazy danych MongoDB. |Tak (jeśli jest używane uwierzytelnianie podstawowe). |
| hasło |Hasło dla użytkownika hello. |Tak (jeśli jest używane uwierzytelnianie podstawowe). |
| authSource |Nazwa bazy danych MongoDB hello czy chcesz toouse toocheck swoje poświadczenia dla uwierzytelniania. |Opcjonalnie (jeśli jest używane uwierzytelnianie podstawowe). domyślne: używa konta administratora hello i hello bazy danych określona za pomocą właściwości databaseName. |
| DatabaseName |Nazwa bazy danych MongoDB hello, które mają tooaccess. |Tak |
| gatewayName |Nazwa bramy hello, który uzyskuje dostęp do magazynu danych hello. |Tak |
| encryptedCredential |Poświadczenie szyfrowane przez bramę. |Optional (Opcjonalność) |

#### <a name="example"></a>Przykład

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties)

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych MongoDB, zestaw hello **typu** hello DataSet za**MongoDbCollection**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| CollectionName |Nazwa kolekcji hello w bazie danych MongoDB. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties)

#### <a name="mongodb-source-in-copy-activity"></a>Źródłowej bazy danych MongoDB w przypadku działania kopiowania
Jeśli dane są kopiowane z bazy danych MongoDB, ustaw hello **typ źródła** hello skopiować działania zbyt**MongoDbSource**i określ następujące właściwości w hello **źródła** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL 92. Na przykład: `select * from MyTable`. |Nie (Jeśli **collectionName** z **dataset** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Połączona usługa
toodefine Amazon S3 połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AwsAccessKey**i określ następujące właściwości w hello **typeProperties** sekcji :  

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| accessKeyID |Identyfikator klucza tajnego dostępu hello. |Ciąg |Tak |
| secretAccessKey |klucz tajny dostępu Hello samej siebie. |Zaszyfrowanego ciągu tajny |Tak |

#### <a name="example"></a>Przykład
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Zestaw danych
toodefine Amazon S3 zestawu danych, ustaw hello **typu** hello DataSet za**AmazonS3**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| bucketName |Nazwa pakietu Hello S3. |Ciąg |Tak |
| key |Klucz obiektu Hello S3. |Ciąg |Nie |
| Prefiks |Prefiks hello S3 obiektu klucza. Wybrano obiektów, w której klucze uruchomienia z tym prefiksem. Ma zastosowanie tylko wtedy, gdy klucz jest pusty. |Ciąg |Nie |
| Wersja |Wersja Hello obiektu S3, jeśli włączono S3 przechowywania wersji. |Ciąg |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie | |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Witaj obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie | |


> [!NOTE]
> bucketName + klawisz Określa lokalizację hello obiektu hello S3, gdzie zasobnika jest hello nadrzędny kontener dla obiektów S3, a klucz hello pełną ścieżkę tooS3 obiektu.

#### <a name="example-sample-dataset-with-prefix"></a>Przykład: Przykładowego zestawu danych z prefiksem

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>Przykład: Zestaw danych przykładowych (wersją)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>Przykład: Dynamiczne ścieżki S3
W przykładowym hello używamy stałe wartości dla właściwości klucza i bucketName w zestawie danych hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

Program może obliczyć klucza hello i bucketName dynamicznie w czasie wykonywania za pomocą zmiennych systemowych, takich jak SliceStart fabryki danych.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Możesz zrobić hello takie same dla właściwości prefiks hello Amazon S3 zestawu danych. Zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md) listę obsługiwanych funkcjach i zmiennych.

Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Źródło systemu plików w przypadku działania kopiowania
Jeśli dane są kopiowane z Amazon S3, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcji :


| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Określa, czy lista toorecursively S3 obiekty w katalogu hello. |wartość true, false |Nie |


#### <a name="example"></a>Przykład


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>System plików


### <a name="linked-service"></a>Połączona usługa
Możesz połączyć fabrykę danych Azure lokalnego pliku system tooan z hello **na lokalnym serwerze plików** połączonej usługi. Witaj w poniższej tabeli przedstawiono opis elementów JSON, które są określone toohello połączony serwer plików lokalnej usługi.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |Sprawdź, czy właściwość type hello jest ustawiony za**OnPremisesFileServer**. |Tak |
| Host |Określa ścieżkę katalogu głównego hello folderu hello, które mają toocopy. Użyj znaku ucieczki hello ' \ ' znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady. |Tak |
| Nazwa użytkownika |Określ identyfikator hello hello użytkownik, który ma dostęp do serwera toohello. |Nie (Jeśli wybierzesz encryptedCredential) |
| hasło |Określ hasło hello hello użytkownika (nazwa użytkownika). |Nie (Jeśli wybierzesz encryptedCredential |
| encryptedCredential |Określ poświadczenia hello zaszyfrowane, które można uzyskać, uruchamiając polecenie cmdlet hello AzureRmDataFactoryEncryptValue nowy. |Nie (Jeśli wybierzesz toospecify identyfikatora użytkownika i hasła w postaci zwykłego tekstu) |
| gatewayName |Określa nazwę hello hello bramy, że fabryka danych powinien używać serwera plików lokalnych toohello tooconnect. |Tak |

#### <a name="sample-folder-path-definitions"></a>Ścieżka folderu definicje 
| Scenariusz | Host w definicji usługi połączonej | folderPath w definicji zestawu danych |
| --- | --- | --- |
| Folder lokalny na komputerze bramy zarządzania danymi: <br/><br/>Przykłady: D:\\ \* lub D:\folder\subfolder\\* |D:\\ \\ (dla danych zarządzania bramy 2.0 i nowsze wersje) <br/><br/> localhost (dla starszych niż 2.0 bramy zarządzania danych) |. \\ \\ lub folderu\\\\podfolder (dla danych zarządzania bramy 2.0 i nowsze wersje) <br/><br/>D:\\ \\ lub D:\\\\folderu\\\\podfolder (dla wersji bramy poniżej 2.0) |
| Zdalny folder udostępniony: <br/><br/>Przykłady: \\ \\MójSerwer\\udostępnianie\\ \* lub \\ \\MójSerwer\\udostępnianie\\folderu\\podfolderu\\* |\\\\\\\\MójSerwer\\\\udziału |. \\ \\ lub folderu\\\\podfolderu |


#### <a name="example-using-username-and-password-in-plain-text"></a>Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Przykład: Użycie encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Zestaw danych
toodefine System plików zestawu danych, ustaw hello **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Określa folder toohello podrzędną hello. Użyj znaku ucieczki hello ' \' znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwa hello hello wygenerowany plik jest zgodny z formatem hello: <br/><br/>`Data.<Guid>.txt`(Przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Nie |
| obiektu fileFilter |Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików. <br/><br/>Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).<br/><br/>Przykład 1: "obiektu"fileFilter: "* .log"<br/>Przykład 2: "obiektu"fileFilter: 2016 - 1-?. txt"<br/><br/>Należy pamiętać, że tego obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików. |Nie |
| partitionedBy |Toospecify partitionedBy dynamiczne folderPath/fileName służącego do dane szeregów czasowych. Przykładem jest folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**; i są obsługiwane poziomy: **optymalna** i **najszybciej**. zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

> [!NOTE]
> Nie można użyć nazwy pliku i obiektu fileFilter jednocześnie.

#### <a name="example"></a>Przykład

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Źródło systemu plików w przypadku działania kopiowania
Jeśli dane są kopiowane z systemu plików, należy ustawić hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>W przypadku działania kopiowania obiektu Sink systemu plików
Kopiowania danych tooFile systemu, ustaw hello **typu sink** hello skopiować działania zbyt**FileSystemSink**i określ następujące właściwości w hello **zbiornika** sekcji:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| copyBehavior |Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików. |**PreserveHierarchy:** zachowuje hello hierarchii plików w folderze docelowym hello. Oznacza to, że hello względnej ścieżki folderu źródłowego toohello pliku źródłowego hello jest hello taka sama jak ścieżka względna hello hello docelowego pliku toohello docelowy folderu.<br/><br/>**FlattenHierarchy:** wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom folderu docelowego. pliki docelowe Hello są tworzone z automatycznie generowaną nazwą.<br/><br/>**MergeFiles:** scala wszystkie pliki z pliku tooone folderu źródłowego hello. Jeśli określono hello pliku nazwy/nazwa obiektu blob, hello scalony plik nazwa jest hello określonej nazwy. W przeciwnym razie jest nazwa pliku wygenerowana automatycznie. |Nie |
Auto-

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Połączona usługa
toodefine FTP połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**SerwerFTP**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane | Domyślne |
| --- | --- | --- | --- |
| Host |Nazwa lub adres IP powitania serwera FTP |Tak |&nbsp; |
| Typ authenticationType |Określ typ uwierzytelniania |Tak |Basic anonimowe |
| nazwa użytkownika |Użytkownik, który ma dostęp do serwera FTP toohello |Nie |&nbsp; |
| hasło |Hasło dla użytkownika hello (nazwa_użytkownika) |Nie |&nbsp; |
| encryptedCredential |Serwer FTP hello tooaccess zaszyfrowane poświadczenia |Nie |&nbsp; |
| gatewayName |Nazwa hello brama zarządzania danymi bramy tooconnect tooan lokalnego serwera FTP |Nie |&nbsp; |
| port |Port, na którym hello FTP nasłuchuje serwer |Nie |21 |
| enableSsl |Określ, czy toouse FTP za pośrednictwem kanału SSL/TLS |Nie |Wartość true |
| enableServerCertificateValidation |Określ, czy tooenable serwera SSL przy użyciu protokołu FTP za pośrednictwem kanału SSL/TLS, certyfikat weryfikacji |Nie |Wartość true |

#### <a name="example-using-anonymous-authentication"></a>Przykład: Przy użyciu uwierzytelniania anonimowego

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu dla uwierzytelniania podstawowego

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Przykład: Przy użyciu portu, enableSsl, enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Przykład: Użycie encryptedCredential uwierzytelniania i bramy

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine FTP zestawu danych, ustaw hello **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Folder toohello ścieżki Sub. Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak 
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: <br/><br/>Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| obiektu fileFilter |Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.<br/><br/>Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).<br/><br/>Przykład 1:`"fileFilter": "*.log"`<br/>Przykład 2:`"fileFilter": 2016-1-?.txt"`<br/><br/> obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików. Ta właściwość nie jest obsługiwana z systemu plików HDFS. |Nie |
| partitionedBy |partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych. Na przykład folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**; i są obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |
| useBinaryTransfer |Określ, czy używany tryb transferu binarnego. Wartość true dla trybie binarnym i wartość false ASCII. Wartość domyślna: wartość True. Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP. |Nie |

> [!NOTE]
> Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.

#### <a name="example"></a>Przykład

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#dataset-properties) artykułu.

### <a name="file-system-source-in-copy-activity"></a>Źródło systemu plików w przypadku działania kopiowania
Jeśli dane są kopiowane z serwera FTP, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#copy-activity-properties) artykułu.


## <a name="hdfs"></a>SYSTEM PLIKÓW HDFS

### <a name="linked-service"></a>Połączona usługa
toodefine HDFS połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**systemu plików Hdfs**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |musi mieć ustawioną właściwość type Hello: **Hdfs** |Tak |
| Url |Adres URL toohello systemu plików HDFS |Tak |
| Typ authenticationType |Anonimowe lub Windows. <br><br> toouse **uwierzytelnianie Kerberos** łącznika systemu plików HDFS, można znaleźć zbyt[w tej sekcji](#use-kerberos-authentication-for-hdfs-connector) tooset się w lokalnym środowisku odpowiednio. |Tak |
| Nazwa użytkownika |Uwierzytelnianie nazwy użytkownika dla systemu Windows. |Tak (w przypadku uwierzytelniania systemu Windows) |
| hasło |Hasło dla uwierzytelniania systemu Windows. |Tak (w przypadku uwierzytelniania systemu Windows) |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać toohello tooconnect systemu plików HDFS. |Tak |
| encryptedCredential |[Nowy AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello poświadczeń dostępu do danych wyjściowych. |Nie |

#### <a name="example-using-anonymous-authentication"></a>Przykład: Przy użyciu uwierzytelniania anonimowego

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Przykład: Przy użyciu uwierzytelniania systemu Windows

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine systemu plików HDFS zestawu danych, ustaw hello **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Ścieżka folderu toohello. Przykład:`myfolder`<br/><br/>Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello. Na przykład: folder\subfolder, określ folder\\\\podfolderów i dla d:\samplefolder, określ d:\\\\folder_przykładowy.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: <br/><br/>Dane. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| partitionedBy |partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych. Przykład: folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

> [!NOTE]
> Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.

#### <a name="example"></a>Przykład

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#dataset-properties) artykułu. 

### <a name="file-system-source-in-copy-activity"></a>Źródło systemu plików w przypadku działania kopiowania
Jeśli dane są kopiowane z systemu plików HDFS, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcji:

**FileSystemSource** obsługuje hello następujące właściwości:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#copy-activity-properties) artykułu.

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Połączona usługa
toodefine SFTP połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**Sftp**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- | --- |
| Host | Nazwa lub adres IP serwera SFTP hello. |Tak |
| port |Port, na którym hello SFTP serwer nasłuchuje. Witaj, wartość domyślna to: 21 |Nie |
| Typ authenticationType |Określ typ uwierzytelniania. Dozwolone wartości: **podstawowe**, **parametry SshPublicKey**. <br><br> Odwołuje się zbyt[używanie uwierzytelniania podstawowego](#using-basic-authentication) i [przy użyciu publicznego klucza uwierzytelniania SSH](#using-ssh-public-key-authentication) odpowiednio sekcje więcej właściwości i przykłady JSON. |Tak |
| skipHostKeyValidation | Określ, czy tooskip hosta klucza weryfikacji. | Nie. Witaj wartość domyślna: false |
| hostKeyFingerprint | Podaj odcisk palca hello hello klucza hosta. | Tak, jeśli hello `skipHostKeyValidation` ustawiono toofalse.  |
| gatewayName |Nazwa tooan tooconnect brama zarządzania danymi hello SFTP serwerem lokalnym. | Tak, jeśli kopiowanie danych z lokalnego serwera SFTP. |
| encryptedCredential | Serwer protokołu SFTP hello tooaccess zaszyfrowane poświadczenia. Wygenerowany automatycznie po określeniu opcji Uwierzytelnianie podstawowe (nazwy użytkownika i hasła) lub uwierzytelniania parametry SshPublicKey (nazwy użytkownika i ścieżki do klucza prywatnego lub zawartości) kopiowania kreatora lub hello ClickOnce podręcznego okna dialogowego. | Nie. Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP. |

#### <a name="example-using-basic-authentication"></a>Przykład: Przy użyciu uwierzytelniania podstawowego

Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `Basic`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- | --- |
| nazwa użytkownika | Użytkownik, który ma dostęp toohello SFTP serwera. |Tak |
| hasło | Hasło dla użytkownika hello (nazwa_użytkownika). | Tak |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Przykład: Uwierzytelnianie podstawowe z zaszyfrowanych poświadczeń **

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Przy użyciu uwierzytelniania klucza publicznego SSH: **

Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `SshPublicKey`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- | --- |
| nazwa użytkownika |Użytkownik, który ma dostęp toohello SFTP serwera |Tak |
| privateKeyPath | Określ ścieżkę bezwzględną toohello pliku klucza prywatnego może dostęp do tej bramy. | Określ albo hello `privateKeyPath` lub `privateKeyContent`. <br><br> Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP. |
| privateKeyContent | Zserializowany ciąg hello prywatnego klucza zawartości. Witaj kreatora kopiowania może odczytywać hello pliku klucza prywatnego i Wyodrębnij zawartość klucza prywatnego hello automatycznie. Jeśli używane są wszystkie inne narzędzie/pakiet SDK, należy użyć właściwości privateKeyPath hello. | Określ albo hello `privateKeyPath` lub `privateKeyContent`. |
| Hasło | Określ hello przebiegu frazy/hasło toodecrypt hello prywatny klucz, jeśli plik klucza hello jest chroniony przez hasło. | Tak, czy plik klucza prywatnego hello jest chroniony przez hasło. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Przykład: Parametry SshPublicKey uwierzytelniania za pomocą prywatnego klucza zawartości **

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych SFTP hello zestaw **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| folderPath |Folder toohello ścieżki Sub. Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello. Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.<br/><br/>Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka. |Tak |
| fileName |Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello. Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.<br/><br/>Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: <br/><br/>Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Nie |
| obiektu fileFilter |Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.<br/><br/>Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).<br/><br/>Przykład 1:`"fileFilter": "*.log"`<br/>Przykład 2:`"fileFilter": 2016-1-?.txt"`<br/><br/> obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików. Ta właściwość nie jest obsługiwana z systemu plików HDFS. |Nie |
| partitionedBy |partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych. Na przykład folderPath sparametryzowana dla każdej godziny danych. |Nie |
| Format | obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Zestaw hello **typu** właściwości w formacie tooone tych wartości. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. <br><br> Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |
| useBinaryTransfer |Określ, czy używany tryb transferu binarnego. Wartość true dla trybie binarnym i wartość false ASCII. Wartość domyślna: wartość True. Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP. |Nie |

> [!NOTE]
> Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.

#### <a name="example"></a>Przykład

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#dataset-properties) artykułu. 

### <a name="file-system-source-in-copy-activity"></a>Źródło systemu plików w przypadku działania kopiowania
Jeśli dane są kopiowane z użyciem protokołu SFTP źródła, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| Cykliczne |Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu. |Wartość true, False (ustawienie domyślne) |Nie |



#### <a name="example"></a>Przykład

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#copy-activity-properties) artykułu.


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Połączona usługa
toodefine HTTP połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**Http**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| adres URL | Podstawowa toohello adres URL serwera sieci Web | Tak |
| Typ authenticationType | Określa typ uwierzytelniania hello. Dozwolone wartości to: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, **ClientCertificate**. <br><br> Dotyczą odpowiednio toosections pod tą tabelą więcej właściwości i przykłady JSON dla tych typów uwierzytelniania. | Tak |
| enableServerCertificateValidation | Określ, czy tooenable serwera SSL certyfikatu weryfikacji, jeśli źródło jest serwer sieci Web protokołu HTTPS | Nie, domyślna to true |
| gatewayName | Nazwa tooan tooconnect brama zarządzania danymi hello lokalnego źródła HTTP. | Tak, jeśli kopiowanie danych z lokalnego źródła HTTP. |
| encryptedCredential | Zaszyfrowane poświadczenia tooaccess hello punkt końcowy HTTP. Wygenerowany automatycznie podczas konfigurowania hello informacje o uwierzytelnianiu w kopii kreatora lub hello ClickOnce podręcznego okna dialogowego. | Nie. Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera HTTP. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Przykład: Uwierzytelnianie podstawowe, szyfrowane lub systemu Windows
Ustaw `authenticationType` jako `Basic`, `Digest`, lub `Windows`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| nazwa użytkownika | Nazwa użytkownika tooaccess hello punkt końcowy HTTP. | Tak |
| hasło | Hasło dla użytkownika hello (nazwa_użytkownika). | Tak |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Przykład: Przy użyciu uwierzytelniania ClientCertificate

Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `ClientCertificate`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| embeddedCertData | zawartość algorytmem Base64 Hello danych binarnych hello pliku wymiany informacji osobistych (PFX). | Określ albo hello `embeddedCertData` lub `certThumbprint`. |
| certThumbprint | Witaj odcisk palca certyfikatu hello, który został zainstalowany na komputerze bramy magazynu certyfikatów. Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego źródła HTTP. | Określ albo hello `embeddedCertData` lub `certThumbprint`. |
| hasło | Hasło skojarzone z certyfikatem hello. | Nie |

Jeśli używasz `certThumbprint` dla certyfikatu uwierzytelniania i hello jest zainstalowany w magazynie osobistym hello hello komputera lokalnego, należy Usługa bramy toohello toogrant hello uprawnienia do odczytu:

1. Uruchom program Microsoft Management Console (MMC). Dodaj hello **certyfikaty** tego hello cele przystawki **komputera lokalnego**.
2. Rozwiń węzeł **certyfikaty**, **osobistych**i kliknij przycisk **certyfikaty**.
3. Kliknij prawym przyciskiem myszy hello certyfikatu z magazynu osobistego hello, a następnie wybierz **wszystkie zadania**->**Zarządzaj kluczami prywatnymi...**
3. Na powitania **zabezpieczeń** , Dodaj konto użytkownika hello, pod którą jest uruchomiona usługa hosta bramy zarządzania danymi w certyfikatem toohello hello dostęp do odczytu.  

**Przykład: przy użyciu certyfikatu klienta:** to połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web. Używa certyfikatu klienta, który jest zainstalowany na komputerze hello z zainstalowana brama zarządzania danymi.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Przykład: przy użyciu certyfikatu klienta w pliku
To połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web. Za pomocą pliku certyfikatu klienta na powitania maszyny i zainstalować bramę zarządzania danymi.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine HTTP zestawu danych, ustaw hello **typu** hello DataSet za**Http**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| relativeUrl | Względny adres URL toohello zasób zawierający dane hello. Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany. <br><br> tooconstruct dynamicznego adresu URL, można użyć [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md), przykład: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | Nie |
| requestMethod | Metoda HTTP. Dozwolone wartości to **UZYSKAĆ** lub **POST**. | Nie. Domyślnie jest `GET`. |
| additionalHeaders | Dodatkowych nagłówków żądania HTTP. | Nie |
| requestBody | Treść żądania HTTP. | Nie |
| Format | Jeśli chcesz, aby toosimply **pobrać hello danych z punktu końcowego HTTP jako — jest** bez podczas analizowania, Pomiń ten ustawienia formatu. <br><br> Należy odpowiedzi hello HTTP tooparse zawartości podczas kopiowania są obsługiwane następujące typy format hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje. |Nie |
| Kompresja | Określ typ hello i poziom kompresji danych hello. Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**. Obsługiwane poziomy: **optymalna** i **najszybciej**. Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Nie |

#### <a name="example-using-hello-get-default-method"></a>Przykład: hello metoda GET (ustawienie domyślne)

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Przykład: przy użyciu metody POST hello

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#dataset-properties) artykułu.

### <a name="http-source-in-copy-activity"></a>Źródła HTTP w przypadku działania kopiowania
Jeśli dane są kopiowane ze źródła HTTP, ustaw hello **typ źródła** hello skopiować działania zbyt**HttpSource**i określ następujące właściwości w hello **źródła** sekcji:

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| httpRequestTimeout | Witaj limitu czasu (TimeSpan) dla tooget żądania HTTP hello odpowiedzi. Jest tooget hello limitu czasu odpowiedzi, hello limitu czasu tooread odpowiedzi danych. | Nie. Wartość domyślna: 00:01:40 |


#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#copy-activity-properties) artykułu.

## <a name="odata"></a>OData

### <a name="linked-service"></a>Połączona usługa
toodefine OData połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OData**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| adres URL |Adres URL usługi OData hello. |Tak |
| Typ authenticationType |Typ uwierzytelniania używany źródło OData toohello tooconnect. <br/><br/> Chmury OData możliwe wartości to anonimowe, podstawowe i OAuth (Uwaga obecnie tylko pomocy technicznej usługi fabryka danych Azure OAuth opartej na usłudze Azure Active Directory). <br/><br/> Dla protokołu OData lokalnymi możliwe wartości to anonimowe, podstawowe i systemu Windows. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego. |Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego) |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego) |
| authorizedCredential |Jeśli używasz uwierzytelniania OAuth, kliknij przycisk **autoryzacji** przycisku na powitania Kreatora kopiowania fabryki danych lub edytorze, a następnie wprowadź Twoje poświadczenia hello wartość tej właściwości będzie wygenerowany automatycznie. |Tak (tylko wtedy, gdy używasz uwierzytelniania OAuth) |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać usługi OData lokalnymi toohello tooconnect. Określ tylko, jeśli dane są kopiowane z lokalnego źródła OData. |Nie |

#### <a name="example---using-basic-authentication"></a>Przykład — przy użyciu uwierzytelniania podstawowego
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Przykład — przy użyciu uwierzytelniania anonimowego

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Przykład — Windows przy użyciu uwierzytelniania dostępu do lokalnego źródła OData

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Przykład — przy użyciu uwierzytelniania OAuth, uzyskiwanie dostępu do chmury źródło OData
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#linked-service-properties) artykułu.

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych OData hello zestaw **typu** hello DataSet za**ODataResource**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Ścieżka |Toohello ścieżki OData zasobów |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#dataset-properties) artykułu.

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane ze źródła danych OData, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Przykład | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |"? $select = nazwa, opis i $top = 5" |Nie |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#copy-activity-properties) artykułu.


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Połączona usługa
toodefine ODBC połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesOdbc**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Parametry połączenia |poświadczenie zaszyfrowana Hello poświadczeń innych niż dostępu część hello ciąg połączenia i opcjonalne. Przykłady w hello następujące sekcje. |Tak |
| poświadczenia |Hello dostępu do poświadczeń część hello parametrów połączenia określonego w formacie wartość właściwości sterownika. Przykład: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ". |Nie |
| Typ authenticationType |Typ uwierzytelniania używany Magazyn danych ODBC toohello tooconnect. Możliwe wartości to: anonimowych, jak i podstawowych. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać magazynu danych ODBC toohello tooconnect. |Tak |

#### <a name="example---using-basic-authentication"></a>Przykład — przy użyciu uwierzytelniania podstawowego

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Przykład — użyciu zaszyfrowane poświadczenia uwierzytelniania podstawowego
Można szyfrować poświadczeń hello przy użyciu hello [AzureRMDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet (w wersji 1.0 programu Azure PowerShell) lub [AzureDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 lub starszej wersji hello Program Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Przykład: Przy użyciu uwierzytelniania anonimowego

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawem danych ODBC hello zestaw **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w magazynie danych ODBC hello. |Tak |


#### <a name="example"></a>Przykład

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#dataset-properties) artykułu. 

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z magazynu danych ODBC, należy ustawić hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Ciąg zapytania SQL. Na przykład: `select * from MyTable`. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#copy-activity-properties) artykułu.

## <a name="salesforce"></a>SalesForce


### <a name="linked-service"></a>Połączona usługa
toodefine Salesforce połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**Salesforce**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| environmentUrl | Określ wystąpienie adres URL usługi Salesforce hello. <br><br> -Domyślna to "https://login.salesforce.com". <br> -toocopy danych z piaskownicy, określ "https://test.salesforce.com". <br> -toocopy dane z domeny niestandardowej, określić, na przykład "https://[domain].my.salesforce.com". |Nie |
| nazwa użytkownika |Określ nazwę użytkownika dla konta użytkownika hello. |Tak |
| hasło |Określ hasło dla konta użytkownika hello. |Tak |
| securityToken |Określ tokenu zabezpieczającego dla konta użytkownika hello. Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje na temat tooreset/get tokenu zabezpieczającego. Ogólnie rzecz biorąc, zobacz toolearn o tokeny zabezpieczające [zabezpieczeń i hello interfejsu API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine Salesforce zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| tableName |Nazwa tabeli hello w usłudze Salesforce. |Nie (Jeśli **zapytania** z **RelationalSource** jest określona) |

#### <a name="example"></a>Przykład

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#dataset-properties) artykułu. 

### <a name="relational-source-in-copy-activity"></a>Relacyjnego źródła w przypadku działania kopiowania
Jeśli dane są kopiowane z usług Salesforce, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:

| Właściwość | Opis | Dozwolone wartości | Wymagane |
| --- | --- | --- | --- |
| query |Użyj hello zapytanie niestandardowe tooread danych. |Zapytania SQL 92 lub [Salesforce obiektu Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) zapytania. Przykład: `select * from MyTable__c`. |Nie (jeśli hello **tableName** z hello **dataset** jest określona) |

#### <a name="example"></a>Przykład  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.

Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#copy-activity-properties) artykułu. 

## <a name="web-data"></a>Dane sieci Web 

### <a name="linked-service"></a>Połączona usługa
toodefine sieci Web połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**sieci Web**i określ następujące właściwości w hello **typeProperties** sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Url |Adres URL źródła toohello w sieci Web |Tak |
| Typ authenticationType |Anonimowe. |Tak |
 

#### <a name="example"></a>Przykład


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#linked-service-properties) artykułu. 

### <a name="dataset"></a>Zestaw danych
toodefine zestawu danych w sieci Web, zestaw hello **typu** hello DataSet za**tabeli WebTable**i określ następujące właściwości w hello hello **typeProperties** sekcji: 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |Typ hello zestawu danych. musi być ustawiona zbyt**tabeli WebTable** |Tak |
| Ścieżka |Względny adres URL toohello zasób zawiera tabelę hello. |Nie. Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany. |
| Indeks |Indeks Hello hello tabeli w zasobie hello. Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji kroki toogetting indeksu tabeli na stronie HTML. |Tak |

#### <a name="example"></a>Przykład

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#dataset-properties) artykułu. 

### <a name="web-source-in-copy-activity"></a>Źródło w sieci Web w przypadku działania kopiowania
Jeśli dane są kopiowane z tabeli sieci web, należy ustawić hello **typ źródła** hello skopiować działania zbyt**WebSource**. Obecnie, gdy hello źródła w przypadku działania kopiowania jest typu **WebSource**, są obsługiwane żadne dodatkowe właściwości.

#### <a name="example"></a>Przykład

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#copy-activity-properties) artykułu. 

## <a name="compute-environments"></a>ŚRODOWISKA OBLICZENIOWE
Witaj poniższej tabeli wymieniono hello środowiska obliczeniowe obsługiwane przez fabrykę danych oraz hello działania przekształcania, które można uruchomić na nich. Kliknij łącze hello hello obliczania jesteś zainteresowani schematów JSON hello toosee dla połączonej usługi toolink on tooa fabryki danych. 

| Środowisko obliczeniowe | Działania |
| --- | --- |
| [Klaster usługi HDInsight na żądanie](#on-demand-azure-hdinsight-cluster) lub [klastrem usługi HDInsight](#existing-azure-hdinsight-cluster) |[Działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity) |
| [Partia zadań Azure](#azure-batch) |[Niestandardowe działanie platformy .NET](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Działanie wykonywania wsadowego uczenia maszynowego](#machine-learning-batch-execution-activity), [działanie aktualizacji zasobu uczenia maszynowego](#machine-learning-update-resource-activity) |
| [Usługi Azure Data Lake Analytics](#azure-data-lake-analytics) |[Język U-SQL usługi Data Lake Analytics](#data-lake-analytics-u-sql-activity) |
| [Baza danych Azure SQL](#azure-sql-database-1), [magazyn danych Azure SQL](#azure-sql-data-warehouse-1), [programu SQL Server](#sql-server-1) |[Procedura składowana](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Klaster Azure HDInsight na żądanie
Witaj usługi fabryka danych Azure może automatycznie tworzyć opartych na systemie Windows/Linux na żądanie HDInsight klastra tooprocess danych. klaster Hello jest tworzony w tym samym regionie co konto magazynu hello (właściwość linkedServiceName w hello JSON) skojarzone z klastrem hello hello. Możesz uruchomić powitania po transformacji działania w tej połączonej usługi: [działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce ](#hdinsight-mapreduce-activity), [Przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Połączona usługa 
Hello w poniższej tabeli opisano hello właściwości używane w definicji Azure JSON hello usługi HDInsight połączony na żądanie.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |właściwości typu Hello należy ustawić wartość zbyt**HDInsightOnDemand**. |Tak |
| Wartość ClusterSize |Liczba węzłów procesu roboczego/danych w klastrze hello. klaster usługi HDInsight Hello jest tworzony z głównymi węzłami 2 oraz hello liczba węzłów procesu roboczego, które określisz dla tej właściwości. węzły Hello mają rozmiar Standard_D3, który ma 4 rdzenie, więc klastra z węzłem procesu roboczego 4 przyjmuje 24 rdzenie (4\*4 = 16 rdzenie dla węzłów procesu roboczego, a także 2\*rdzenie 4 = 8 dla węzłów głównych). Zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) szczegółowe informacje o hello Standard_D3 warstwy. |Tak |
| wartość TimeToLive |Witaj dozwolony czas bezczynności klastra usługi HDInsight na żądanie hello. Określa, jak długo klastra usługi HDInsight na żądanie hello pozostaje aktywne po zakończeniu działania uruchamiania, jeśli w klastrze hello nie ma żadnych aktywnych działań.<br/><br/>Na przykład, jeśli działanie Uruchom przyjmuje 6 minut i timetolive jest too5 minut, pozostaje klastra hello aktywności 5 minut po hello 6 minut przetwarzania uruchamiania działania hello. Jeśli inny uruchamiania działania jest wykonywane z okna 6 minut hello, jednak jest przetwarzany przez hello tego samego klastra.<br/><br/>Tworzenie klastra usługi HDInsight na żądanie jest kosztowna operacja (może to potrwać pewien czas), więc użyć tego ustawienia jako wydajności wymagane tooimprove fabryki danych przez ponowne użycie klastra usługi HDInsight na żądanie.<br/><br/>Jeśli ustawisz too0 wartość timetolive klaster hello jest usunięty jak działanie hello uruchomić w przetworzone. Na powitania drugiej strony, jeśli ustawisz wysokiej wartości, hello klastra może pozostać bezczynny, co niepotrzebnie wysokich kosztów. Dlatego jest ważne, aby ustawić odpowiednią wartość hello na podstawie Twoich potrzeb.<br/><br/>Można udostępniać wielu potoki hello tego samego wystąpienia klastra usługi HDInsight na żądanie hello, jeśli wartość właściwości timetolive hello jest skonfigurowana. |Tak |
| Wersja |Wersja klastra usługi HDInsight hello. Aby uzyskać więcej informacji, zobacz [obsługiwane wersje usługi HDInsight w fabryce danych Azure](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |Nie |
| linkedServiceName |Usługa Azure Storage połączone toobe usługi używane przez klaster na żądanie hello do przechowywania i przetwarzania danych. <p>Obecnie nie można utworzyć klastra usługi HDInsight na żądanie, korzystającą z usługi Azure Data Lake Store jako hello magazynu. Jeśli chcesz toostore hello dane z usługi HDInsight przetwarzania w usłudze Azure Data Lake Store, użyj danych hello toocopy działanie kopiowania z toohello magazynu obiektów Blob Azure hello Azure Data Lake Store.</p>  | Tak |
| additionalLinkedServiceNames |Określa, że dodatkowe konta magazynu dla hello HDInsight połączonej usługi, dzięki czemu usługi fabryka danych hello można zarejestrować je w Twoim imieniu. |Nie |
| osType |Typ systemu operacyjnego. Dozwolone wartości to: (domyślnie) systemu Windows i Linux |Nie |
| hcatalogLinkedServiceName |Nazwa Hello Azure SQL połączone usługi bazy danych HCatalog toohello punktu. klaster usługi HDInsight na żądanie Hello jest tworzona przy użyciu bazy danych Azure SQL hello jako hello potrzeby magazynu metadanych. |Nie |

### <a name="json-example"></a>Przykład JSON
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
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) artykułu. 

## <a name="existing-azure-hdinsight-cluster"></a>Istniejący klaster Azure HDInsight
Klaster usługi HDInsight można utworzyć tooregister usługi Azure HDInsight połączone z fabryką danych. Możesz uruchomić hello następujące działania przekształcania danych na tej połączonej usługi: [działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [MapReduce działanie](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Połączona usługa
w poniższej tabeli Hello zawiera opisy hello właściwości używane w definicji Azure JSON hello usługi Azure HDInsight połączone.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |właściwości typu Hello należy ustawić wartość zbyt**HDInsight**. |Tak |
| clusterUri |Witaj URI hello klastra usługi HDInsight. |Tak |
| nazwa użytkownika |Określ nazwę hello toobe użytkownika hello używanych tooconnect tooan istniejącym klastrze usługi HDInsight. |Tak |
| hasło |Określ hasło dla konta użytkownika hello. |Tak |
| linkedServiceName | Nazwa hello połączoną usługą magazynu Azure odwołujące się do magazynu obiektów blob Azure toohello używana przez hello klastra usługi HDInsight. <p>Obecnie nie można określić, czy usługa Azure Data Lake Store połączonej usługi dla tej właściwości. Jeśli klaster usługi HDInsight hello ma toohello dostępu do usługi Data Lake Store może dostęp do danych w hello Azure Data Lake Store z skryptów usługi Hive/Pig. </p>  |Tak |

Dla wersji obsługiwane klastrów usługi HDInsight, zobacz [obsługiwane wersje HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>Przykład JSON

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

## <a name="azure-batch"></a>Azure Batch
Tooregister usługi partia zadań Azure połączone można utworzyć puli partii maszynach wirtualnych (VM) przy użyciu fabryki danych. Możesz uruchomić niestandardowych działań platformy .NET przy użyciu partii zadań Azure lub usługi Azure HDInsight. Można uruchomić [działania niestandardowego .NET](#net-custom-activity) na tej połączonej usługi. 

### <a name="linked-service"></a>Połączona usługa
Hello w poniższej tabeli opisano właściwości hello używane w definicji Azure JSON hello usługi partia zadań Azure połączone.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |właściwości typu Hello należy ustawić wartość zbyt**AzureBatch**. |Tak |
| Nazwa konta |Nazwa konta usługi partia zadań Azure hello. |Tak |
| accessKey |Klucz dostępu dla konta usługi partia zadań Azure hello. |Tak |
| poolName |Nazwa puli hello maszyn wirtualnych. |Tak |
| linkedServiceName |Nazwa hello połączoną usługą magazynu Azure skojarzony z tą usługą partii zadań Azure połączone. Tej połączonej usługi jest używany na potrzeby przemieszczania plików wymagane działania hello toorun i przechowywanie dzienniki wykonywania hello działania. |Tak |


#### <a name="json-example"></a>Przykład JSON

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

## <a name="azure-machine-learning"></a>Azure Machine Learning
Możesz utworzyć tooregister usługi Azure Machine Learning połączone punktu końcowego z fabryką danych oceniania partii uczenia maszynowego. Dwa przekształcania działań, które można uruchomić na tym połączonej usługi: [działanie wykonywania wsadowego przez Machine Learning](#machine-learning-batch-execution-activity), [Machine Learning aktualizacji zasobów działania](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Połączona usługa
Hello w poniższej tabeli opisano właściwości hello używane w definicji hello Azure JSON usługi Azure Machine Learning połączone.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Typ |powinien mieć ustawioną właściwość type Hello: **uczenie maszynowe Azure**. |Tak |
| mlEndpoint |Witaj URL wsadowego oceniania. |Tak |
| apiKey |Witaj opublikowane interfejs API modelu obszaru roboczego. |Tak |

#### <a name="json-example"></a>Przykład JSON

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

## <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
Możesz utworzyć **Azure Data Lake Analytics** połączone toolink usługi fabryki danych Azure tooan usługi Azure Data Lake Analytics obliczeń przed użyciem hello [działanie U-SQL w programie Data Lake Analytics](data-factory-usql-activity.md) w potoku .

### <a name="linked-service"></a>Połączona usługa

w poniższej tabeli Hello zawiera opisy hello właściwości używane w definicji JSON hello usługi Azure Data Lake Analytics połączone. 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Typ |powinien mieć ustawioną właściwość type Hello: **AzureDataLakeAnalytics**. |Tak |
| Nazwa konta |Nazwa konta usługi Azure Data Lake Analytics. |Tak |
| Element dataLakeAnalyticsUri |Identyfikator URI, usługi Azure Data Lake Analytics. |Nie |
| Autoryzacji |Kod autoryzacji jest automatycznie pobierany po kliknięciu przycisku **autoryzacji** przycisk hello Edytor fabryki danych i kończenie hello operacji logowania OAuth. |Tak |
| subscriptionId |Identyfikator subskrypcji platformy Azure |Nie (Jeśli nie określono subskrypcji hello jest używana fabryka danych). |
| Grupy zasobów o nazwie |Nazwa grupy zasobów platformy Azure |Nie (Jeśli nie określono grupy zasobów hello jest używana fabryka danych). |
| Identyfikator sesji |Identyfikator sesji z sesji autoryzacji OAuth hello. Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz. Gdy używasz hello Edytor fabryki danych, ten identyfikator jest generowane automatycznie. |Tak |


#### <a name="json-example"></a>Przykład JSON
Poniższy przykład Hello zawiera definicję JSON dla usługi Azure Data Lake Analytics połączone.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Usługa Azure SQL Database
Tworzenie usługi SQL Azure połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](#stored-procedure-activity) tooinvoke procedury składowanej z potoku fabryki danych. 

### <a name="linked-service"></a>Połączona usługa
toodefine bazy danych SQL Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDatabase**i określ następujące właściwości w hello **typeProperties**sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Parametry połączenia |Określ informacje niezbędne wystąpienie bazy danych SQL Azure toohello tooconnect hello właściwości connectionString. |Tak |

#### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Zobacz [Łącznik usług SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) artykułu, aby uzyskać szczegółowe informacje o tej połączonej usługi.

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse
Tworzenie usługi Azure SQL Data Warehouse połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych. 

### <a name="linked-service"></a>Połączona usługa
toodefine Azure SQL Data Warehouse połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDW**i określ następujące właściwości w hello **typeProperties**sekcji:  

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Parametry połączenia |Określ informacje potrzebne wystąpienia usługi Azure SQL Data Warehouse toohello tooconnect hello właściwości connectionString. |Tak |

#### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu. 

## <a name="sql-server"></a>Oprogramowanie SQL Server 
Tworzenie usługi SQL Server połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych. 

### <a name="linked-service"></a>Połączona usługa
Tworzenie połączonej usługi typu **OnPremisesSqlServer** toolink fabrykę danych tooa bazy danych programu SQL Server lokalne. Hello w poniższej tabeli przedstawiono opis dla usługi programu SQL Server połączone określonych lokalnych tooon elementy JSON.

Witaj w poniższej tabeli przedstawiono opis dla określonych tooSQL elementów JSON usługi Serwer połączony.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| type |powinien mieć ustawioną właściwość type Hello: **OnPremisesSqlServer**. |Tak |
| Parametry połączenia |Określ informacje connectionString potrzebne tooconnect toohello lokalnej bazy danych SQL Server przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows. |Tak |
| gatewayName |Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu SQL Server. |Tak |
| nazwa użytkownika |Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows. Przykład: **domainname\\username**. |Nie |
| hasło |Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika. |Nie |

Można szyfrować poświadczeń przy użyciu hello **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia hello, jak pokazano w hello poniższy przykład (**EncryptedCredential** właściwość):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Przykład: JSON dla przy użyciu uwierzytelniania programu SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Przykład: JSON dla przy użyciu uwierzytelniania systemu Windows

Jeśli podano nazwę użytkownika i hasło, brama używa ich tooimpersonate hello określonego tooconnect toohello lokalnego programu SQL Server bazy danych kont użytkowników. W przeciwnym razie nawiązanie połączenia bramy toohello programu SQL Server bezpośrednio z kontekstu zabezpieczeń hello bramy (jego konta uruchamiania).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu.

## <a name="data-transformation-activities"></a>DZIAŁANIA PRZEKSZTAŁCENIA DANYCH

Działanie | Opis
-------- | -----------
[Działanie HDInsight Hive](#hdinsight-hive-activity) | Witaj HDInsight Hive działania w potoku fabryki danych wykonuje zapytań programu Hive samodzielnie lub w klastrze systemu Windows/Linux-based HDInsight na żądanie. 
[Działanie HDInsight Pig](#hdinsight-pig-activity) | Witaj HDInsight Pig działania w potoku fabryki danych wykonuje zapytania Pig samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.
[Działania technologii MapReduce w usłudze HDInsight](#hdinsight-mapreduce-activity) | Witaj działania HDInsight MapReduce w potoku fabryki danych wykonuje programy MapReduce samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.
[Działania przesyłania strumieniowego usługi HDInsight](#hdinsight-streaming-activity) | Witaj HDInsight działaniu przesyłania strumieniowego w potoku fabryki danych wykonuje przesyłania strumieniowego usługi Hadoop programy samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.
[Działania platformy Spark w usłudze HDInsight](#hdinsight-spark-activity) | Witaj HDInsight Spark działania w potoku fabryki danych wykonuje programy Spark w klastrze usługi HDInsight. 
[Działanie wykonywania wsadowego w usłudze Machine Learning](#machine-learning-batch-execution-activity) | Azure umożliwia fabryki danych tooeasily możesz utworzyć potoki korzystających z opublikowanych uczenie maszynowe Azure w sieci web usługi analizy predykcyjnej. Witaj działanie wykonywania wsadowego w potoku fabryki danych Azure można wywołać usługi Machine Learning web toomake operacje przewidywania dla usługi na powitania danych w partii. 
[Działania aktualizowania zasobów w usłudze Machine Learning](#machine-learning-update-resource-activity) | Wraz z upływem czasu hello modeli predykcyjnych w hello uczenia maszynowego oceniania eksperymenty muszą toobe retrained przy użyciu nowych danych wejściowych zestawów danych. Po wykonaniu ponownego trenowania chcesz hello tooupdate oceniania usługi sieci web z hello retrained modelu uczenia maszynowego. Można użyć hello usługi sieci web hello tooupdate działanie aktualizacji zasobu z hello nowo uczenia modelu.
[Działania procedur składowanych](#stored-procedure-activity) | Można użyć działania procedura składowana hello w tooinvoke potoku fabryki danych procedury składowanej w jednym z powitania po magazynów danych: baza danych SQL Azure, Magazyn danych SQL Azure, bazy danych serwera SQL w przedsiębiorstwie lub maszynie Wirtualnej platformy Azure. 
[Data Lake Analytics U-SQL działania](#data-lake-analytics-u-sql-activity) | Data Lake Analytics U-SQL działanie uruchamia skrypt U-SQL w klastrze usługi Azure Data Lake Analytics.  
[Niestandardowe działanie platformy .NET](#net-custom-activity) | Dane tootransform w taki sposób, który nie jest obsługiwany przez fabrykę danych należy można tworzyć niestandardowe działania na własną logikę przetwarzania danych i użyj hello działania w potoku hello. Można skonfigurować hello niestandardowych .NET działania toorun przy użyciu usługi partia zadań Azure lub klaster Azure HDInsight. 

     
## <a name="hdinsight-hive-activity"></a>Działania technologii Hive w usłudze HDInsight
Można określić hello następujące właściwości w definicji Hive JSON działania. Właściwość typu Hello hello działania musi być: **HDInsightHive**. Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightHive działania:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Skrypt |Określ wbudowanego skryptu Hive hello |Nie |
| Ścieżka skryptu |Magazyn hello Hive skryptu w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku. Użyj właściwości 'script' lub "scriptPath". Nie można używać razem. Nazwa pliku Hello jest rozróżniana wielkość liter. |Nie |
| Definiuje |Określ parametry jako pary klucz wartość dla odwołania do skryptu Hive hello za pomocą "hiveconf" |Nie |

Te właściwości typu są określone toohello Hive działania. Inne właściwości (poza sekcji typeProperties hello) są obsługiwane dla wszystkich działań.   

### <a name="json-example"></a>Przykład JSON
powitania po JSON definiuje działania HDInsight Hive w potoku.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Aby uzyskać więcej informacji, zobacz [Hive działania](data-factory-hive-activity.md) artykułu. 

## <a name="hdinsight-pig-activity"></a>Działania technologii Pig w usłudze HDInsight
Można określić hello następujące właściwości w definicji Pig działania w formacie JSON. Właściwość typu Hello hello działania musi być: **HDInsightPig**. Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightPig działania: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| Skrypt |Określ hello Pig skrypt wbudowany |Nie |
| Ścieżka skryptu |Przechowywanie skrypt programu Pig hello w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku. Użyj właściwości 'script' lub "scriptPath". Nie można używać razem. Nazwa pliku Hello jest rozróżniana wielkość liter. |Nie |
| Definiuje |Określ parametry jako pary klucz wartość dla przywołującego w hello skrypt programu Pig |Nie |

Te właściwości typu są określone toohello Pig działania. Inne właściwości (poza sekcji typeProperties hello) są obsługiwane dla wszystkich działań.   

### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Aby uzyskać więcej informacji, zobacz [działania Pig](#data-factory-pig-activity.md) artykułu. 

## <a name="hdinsight-mapreduce-activity"></a>Działania technologii MapReduce w usłudze HDInsight
Można określić hello następujące właściwości w definicji JSON działania MapReduce. Właściwość typu Hello hello działania musi być: **HDInsightMapReduce**. Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightMapReduce działania: 

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| jarLinkedService | Nazwa hello połączonej usługi dla usługi Azure Storage, który zawiera plik JAR hello hello. | Tak |
| jarFilePath | Ścieżka pliku JAR toohello w hello Azure Storage. | Tak | 
| className | Nazwa klasy głównym hello w pliku JAR hello. | Tak | 
| Argumenty | Lista argumentów rozdzielonych przecinkami hello MapReduce programu. W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce hello. toodifferentiate argumentów z argumentami MapReduce hello, rozważ użycie zarówno opcji i wartości jako argumenty, jak pokazano w hello poniższy przykład (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości) | Nie | 

### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [działania MapReduce](data-factory-map-reduce.md) artykułu. 

## <a name="hdinsight-streaming-activity"></a>Działania przesyłania strumieniowego usługi HDInsight
Można określić hello następujące właściwości w definicji działania przesyłania strumieniowego usługi Hadoop w formacie JSON. Właściwość typu Hello hello działania musi być: **HDInsightStreaming**. Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightStreaming działania: 

| Właściwość | Opis | 
| --- | --- |
| mapowania | Nazwa pliku wykonywalnego mapowania hello. Przykład Witaj cat.exe to hello mapowania pliku wykonywalnego.| 
| Reduktor | Nazwa pliku wykonywalnego reduktor hello. Przykład Witaj wc.exe to reduktor hello pliku wykonywalnego. | 
| Dane wejściowe | Plik wejściowy (w tym miejscu) dla hello mapowania. W przykładzie hello: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample jest hello kontenera obiektów blob, przykład/data/Gutenberg jest hello folder i davinci.txt jest hello obiektu blob. |
| Dane wyjściowe | Plik wyjściowy (w tym miejscu) dla reduktor hello. dane wyjściowe zadania przesyłania strumieniowego usługi Hadoop hello Hello są zapisywane toohello lokalizacji określonej dla tej właściwości. |
| filePaths | Ścieżki do plików wykonywalnych mapowania i reduktor hello. W przykładzie hello: "adfsample/example/apps/wc.exe" adfsample jest hello kontenera obiektów blob, przykład/aplikacji hello folderu, i wc.exe jest hello pliku wykonywalnego. | 
| fileLinkedService | Usługa Azure Storage połączone usługi, która reprezentuje hello Azure magazynu, który zawiera pliki hello określone w sekcji filePaths hello. | 
| Argumenty | Lista argumentów rozdzielonych przecinkami hello MapReduce programu. W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce hello. toodifferentiate argumentów z argumentami MapReduce hello, rozważ użycie zarówno opcji i wartości jako argumenty, jak pokazano w hello poniższy przykład (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości) | 
| getDebugInfo | Element opcjonalny. Jeśli je skonfigurowano tooFailure, dzienniki hello są pobierane tylko w przypadku awarii. Jeśli je skonfigurowano tooAll, dzienniki są zawsze pobierane niezależnie od hello stanu wykonywania. | 

> [!NOTE]
> Należy określić wyjściowy zestaw danych hello działaniu przesyłania strumieniowego usługi Hadoop dla hello **generuje** właściwości. Ten zestaw danych można tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogram (co godzinę, codziennie, itp.). Działanie hello nie przyjmuje dane wejściowe, można pominąć Określanie zestawem danych wejściowych dla działania hello na powitania **dane wejściowe** właściwości.  

## <a name="json-example"></a>Przykład JSON

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Aby uzyskać więcej informacji, zobacz [działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md) artykułu. 

## <a name="hdinsight-spark-activity"></a>Działania platformy Spark w usłudze HDInsight
Można określić hello następujące właściwości w definicji Spark działania w formacie JSON. Właściwość typu Hello hello działania musi być: **HDInsightSpark**. Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightSpark działania: 

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| Właściwość rootPath | Witaj kontenera obiektów Blob platformy Azure i folder zawierający plik Spark hello. Nazwa pliku Hello jest rozróżniana wielkość liter. | Tak |
| entryFilePath | Względna ścieżka folderu głównego toohello hello pakietu kodu Spark. | Tak |
| className | Klasy głównym aplikacji Java/Spark | Nie | 
| Argumenty | Lista argumentów wiersza polecenia toohello Spark program. | Nie | 
| proxyUser | program Spark hello tooexecute tooimpersonate Hello użytkownika konta | Nie | 
| sparkConfig | Właściwości konfiguracji platformy Spark. | Nie | 
| getDebugInfo | Określa, kiedy pliki dziennika Spark hello są kopiowane toohello magazynu Azure używanego przez klaster usługi HDInsight (lub) został określony przez sparkJobLinkedService. Dozwolone wartości: None, zawsze lub niepowodzenie. Wartość domyślna: Brak. | Nie | 
| sparkJobLinkedService | Witaj połączoną usługą magazynu Azure zawierający plik zadania hello Spark, zależności i dzienniki.  Jeśli nie określisz wartości dla tej właściwości, jest używany Magazyn hello skojarzony z klastrem usługi HDInsight. | Nie |

### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Należy zwrócić uwagę hello następujące punkty: 

- Witaj **typu** właściwość jest ustawiona zbyt**HDInsightSpark**.
- Witaj **właściwość rootPath** ustawiono zbyt**adfspark\\pyFiles** gdzie adfspark jest pyFiles i kontener obiektów Blob Azure hello jest poprawnie folderu, w tym kontenerze. W tym przykładzie hello magazynu obiektów Blob Azure jest hello, który jest skojarzony z klastrem Spark hello. Możesz przekazać tooa pliku hello innego magazynu Azure. Jeśli tak zrobisz, należy utworzyć toolink usługi Azure Storage połączone tej fabryki danych toohello konta magazynu. Następnie określ nazwę hello hello połączone usługi jako wartość hello **sparkJobLinkedService** właściwości. Zobacz [właściwości działania Spark](#spark-activity-properties) szczegóły dotyczące tej właściwości oraz inne właściwości obsługiwanych przez hello działania Spark.
- Witaj **entryFilePath** ustawiono toohello **test.py**, czyli plik python hello. 
- Witaj **getDebugInfo** właściwość jest ustawiona zbyt**zawsze**, co oznacza, że pliki dziennika hello są zawsze generowany (powodzenie lub niepowodzenie).  

    > [!IMPORTANT]
    > Zaleca się, czy nie ustawisz tooAlways tej właściwości w środowisku produkcyjnym, chyba że są Rozwiązywanie problemów. 
- Witaj **generuje** sekcja ma jeden wyjściowy zestaw danych. Należy określić wyjściowy zestaw danych, nawet jeśli hello spark program nie zwraca żadnych danych wyjściowych. Hello wyjściowego zestawu danych dysków hello harmonogram dla potoku hello (co godzinę, codziennie, itp.).

Aby uzyskać więcej informacji o działaniu hello, zobacz [działania Spark](data-factory-spark.md) artykułu.  

## <a name="machine-learning-batch-execution-activity"></a>Działanie wykonywania wsadowego w usłudze Machine Learning
Można określić hello następujące właściwości w definicji usługi Azure ML wsadowe wykonywanie działania JSON. Właściwość typu Hello hello działania musi być: **AzureMLBatchExecution**. Musisz utworzyć maszyny platformy Azure, najpierw uczenia połączonej usługi i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooAzureMLBatchExecution działania:

Właściwość | Opis | Wymagane 
-------- | ----------- | --------
WebServiceInputActivity | Hello dataset toobe przekazany jako dane wejściowe dla hello usługi sieci web uczenie Maszynowe Azure. Ten zestaw danych muszą także być ujęte w danych wejściowych hello hello działania. |Użyj WebServiceInputActivity lub webServiceInputs. | 
webServiceInputs | Określ zestawy danych toobe przekazany jako dane wejściowe dla hello usługi sieci web uczenie Maszynowe Azure. Jeśli usługa sieci web hello przyjmuje wielu danych wejściowych, należy użyć właściwości webServiceInputs hello zamiast hello WebServiceInputActivity właściwość. Zestawy danych, które odwołują się hello **webServiceInputs** również muszą być zawarte w hello działania **dane wejściowe**. | Użyj WebServiceInputActivity lub webServiceInputs. | 
webServiceOutputs | Witaj zestawów danych, które są przypisane jako dane wyjściowe dla usługi sieci web uczenie Maszynowe Azure hello. Usługa sieci web Hello zwraca dane wyjściowe w tym zestawie danych. | Tak | 
globalParameters | Określ wartości dla parametrów usługi sieci web hello w tej sekcji. | Nie | 

### <a name="json-example"></a>Przykład JSON
W tym przykładzie działanie hello ma hello dataset **MLSqlInput** jako dane wejściowe i **MLSqlOutput** jako dane wyjściowe hello. Witaj **MLSqlInput** jest przekazywany jako usługi sieci web toohello wejściowych przez przy użyciu hello **WebServiceInputActivity** właściwości JSON. Witaj **MLSqlOutput** jest przekazywany jako usługi sieci Web dane wyjściowe toohello przez przy użyciu hello **webServiceOutputs** właściwości JSON. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

W przykładzie JSON hello hello wdrożona Azure Machine Learning w sieci Web usługi używa czytnika i zapisywania danych tooread/zapisu dla modułu z / tooan bazy danych SQL Azure. Ta usługa sieci Web udostępnia następujące cztery parametry hello: Nazwa serwera, nazwa bazy danych, nazwę konta użytkownika serwera i hasło konta użytkownika serwera bazy danych.

> [!NOTE]
> Tylko wejściami i wyjściami hello AzureMLBatchExecution działania mogą być przekazywane jako parametry toohello usługi sieci Web. Na przykład hello powyżej fragment kodu JSON, MLSqlInput jest wejściowych toohello AzureMLBatchExecution działalność, która jest przekazywany jako wejściowych toohello usługi sieci Web za pomocą parametru WebServiceInputActivity.

## <a name="machine-learning-update-resource-activity"></a>Działanie aktualizowania zasobów w usłudze Machine Learning
Można określić hello następujące właściwości w definicji usługi Azure ML aktualizacji zasobów działania JSON. Właściwość typu Hello hello działania musi być: **AzureMLUpdateResource**. Musisz utworzyć maszyny platformy Azure, najpierw uczenia połączonej usługi i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooAzureMLUpdateResource działania:

Właściwość | Opis | Wymagane 
-------- | ----------- | --------
trainedModelName | Nazwa hello retrained modelu. | Tak |  
trainedModelDatasetName | Pliku zestawu danych wskazujące toohello iLearner zwrócony przez hello ponownego trenowania operacji. | Tak | 

### <a name="json-example"></a>Przykład JSON
potok Hello ma dwa działania: **AzureMLBatchExecution** i **AzureMLUpdateResource**. Witaj działanie wykonywania wsadowego usługi uczenie Maszynowe Azure pobiera dane szkoleniowe hello jako dane wejściowe i tworzy plik iLearner jako dane wyjściowe. działanie Hello wywołuje usługę sieci web szkolenia hello (eksperyment uczenia udostępniony jako usługa sieci web) przy użyciu danych wejściowych hello szkolenia danych i odbiera plik ilearner hello z hello Usługa sieci Web. Hello placeholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez hello fabryki danych Azure usługa toorun hello potoku.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Działania języka U-SQL usługi Data Lake Analytics
Można określić hello następujące właściwości w definicji JSON działanie U-SQL. Właściwość typu Hello hello działania musi być: **DataLakeAnalyticsU SQL**. Musisz utworzyć usługi Azure Data Lake Analytics połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello działania tooDataLakeAnalyticsU-SQL: 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| scriptPath |Ścieżka toofolder, zawierający skrypt hello U-SQL. Nazwa pliku hello jest rozróżniana wielkość liter. |Nie (Jeśli używasz skryptu) |
| Element scriptLinkedService |Połączonej usługi, która łączy hello magazynu, który zawiera hello skryptu toohello usługi fabryka danych |Nie (Jeśli używasz skryptu) |
| Skrypt |Określ skrypt wbudowany zamiast określania scriptPath i scriptLinkedService. Na przykład: "skrypt": "Test Utwórz bazę danych". |Nie (Jeśli używasz scriptPath i scriptLinkedService) |
| degreeOfParallelism |Maksymalna liczba węzłów Hello używać jednocześnie toorun hello zadania. |Nie |
| Priorytet |Określa, które spośród wszystkich znajdujących się w kolejce zadań powinna być wybranego toorun najpierw. Witaj hello niższą, wyższy priorytet hello hello. |Nie |
| parameters |Parametry skryptu hello U-SQL |Nie |

### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Aby uzyskać więcej informacji, zobacz [Data Lake Analytics U-SQL działania](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Działania procedur składowanych
Można określić hello następujące właściwości w definicji przechowywane procedury działania JSON. Właściwość typu Hello hello działania musi być: **SqlServerStoredProcedure**. Należy utworzyć jednego ze hello następujące połączone usługi oraz określić nazwę hello hello połączone usługi jako wartość hello **linkedServiceName** właściwości:

- Oprogramowanie SQL Server 
- Usługa Azure SQL Database
- Azure SQL Data Warehouse

Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooSqlServerStoredProcedure działania:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| storedProcedureName |Określ nazwę hello procedury hello przechowywane w bazie danych Azure SQL hello lub Azure SQL Data Warehouse jest reprezentowana przez hello połączone usługi, która hello używa tabeli danych wyjściowych. |Tak |
| storedProcedureParameters |Określ wartości dla parametrów procedury składowanej. Jeśli potrzebujesz toopass wartości null dla parametru, należy użyć składni hello: "param1": wartość null (małe litery). Zobacz powitania po toolearn próbki o korzystaniu z tej właściwości. |Nie |

Jeśli określisz wejściowy zestaw danych, musi być dostępny (w stanie "Gotowe") dla hello przechowywane procedury toorun działania. Witaj wejściowy zestaw danych nie mogą być używane w procedurze hello przechowywane jako parametr. Jest tylko zależności hello toocheck używane przed początkowy hello przechowywane procedury działania. Należy określić zestaw danych wyjściowych dla działania procedury składowanej. 

Wyjściowy zestaw danych określa hello **harmonogram** hello przechowywane procedury działania (co godzinę, co tydzień, co miesiąc, itp.). Witaj wyjściowego zestawu danych musi używać **połączona usługa** przywołujący tooan bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub baza danych SQL Server w której ma zostać hello toorun procedury składowanej. Witaj wyjściowego zestawu danych może służyć jako wynik hello toopass sposób hello przechowywane procedury dla dalszego przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) w potoku hello. Jednak automatycznie fabryki danych nie zapisuje dane wyjściowe hello toothis procedury przechowywanej zestawu danych. Jest to hello tej tabeli SQL tooa zapisy hello punktów zestawu danych wyjściowych do procedury składowanej. W niektórych przypadkach może być hello wyjściowy zestaw danych **fikcyjny dataset**, który jest używany tylko toospecify hello harmonogramu uruchamiania hello przechowywane procedury działania.  

### <a name="json-example"></a>Przykład JSON

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Aby uzyskać więcej informacji, zobacz [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) artykułu. 

## <a name="net-custom-activity"></a>Niestandardowe działanie platformy .NET
Można określić hello następujące właściwości niestandardowe działanie .NET definicji JSON. Właściwość typu Hello hello działania musi być: **DotNetActivity**. Należy utworzyć usługi Azure HDInsight połączone lub partii zadań Azure połączone usługi i określ nazwę hello hello połączone usługi jako wartość hello **linkedServiceName** właściwości. Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooDotNetActivity działania:
 
| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| AssemblyName | Nazwa zestawu hello. W przykładzie hello jest: **MyDotnetActivity.dll**. | Tak |
| Punkt wejścia |Nazwa klasy hello, który implementuje interfejs IDotNetActivity hello. W przykładzie hello jest: **MyDotNetActivityNS.MyDotNetActivity** gdzie MyDotNetActivityNS jest hello przestrzeni nazw, a MyDotNetActivity hello klasy.  | Tak | 
| PackageLinkedService | Nazwa hello połączoną usługą magazynu Azure wskazujące toohello magazynu obiektów blob, zawierający plik zip hello działania niestandardowego. W przykładzie hello jest: **AzureStorageLinkedService**.| Tak |
| PackageFile | Nazwa pliku zip hello. W przykładzie hello jest: **customactivitycontainer/MyDotNetActivity.zip**. | Tak |
| właściwości rozszerzone | Rozszerzone właściwości, które można definiować i przekazywania toohello kodu platformy .NET. W tym przykładzie hello **SliceStart** zmienna jest ustawiona wartość tooa oparta na powitania SliceStart zmienna. | Nie | 

### <a name="json-example"></a>Przykład JSON

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Aby uzyskać szczegółowe informacje, zobacz [skorzystać z działań niestandardowych w fabryce danych](data-factory-use-custom-activities.md) artykułu. 

## <a name="next-steps"></a>Następne kroki
Zobacz hello następujące samouczki: 

- [Samouczek: tworzenie potoku z działanie kopiowania](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Samouczek: tworzenie potoku z działaniem gałęzi](data-factory-build-your-first-pipeline-using-editor.md)