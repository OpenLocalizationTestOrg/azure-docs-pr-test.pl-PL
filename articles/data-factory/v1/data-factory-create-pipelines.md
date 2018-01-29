---
title: "Utwórz/harmonogram potoki, łańcucha działań w fabryce danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się utworzyć dane potok w fabryce danych Azure, aby przenieść i przekształcania danych. Utworzenie przepływu pracy opartych na danych wygenerowało gotowe do użycia informacji."
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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: c8ddd2b49ca48f3bf232a8650d870a8b7159f66a
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Potoki i działań w fabryce danych Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](data-factory-create-pipelines.md)
> * [Wersja 2 — wersja zapoznawcza](../concepts-pipelines-activities.md)

> [!NOTE]
> Ten artykuł dotyczy wersji 1 usługi Data Factory, która jest ogólnie dostępna (GA). Jeśli używasz wersji 2 usługi fabryka danych, która jest w wersji zapoznawczej, zobacz [potoków w wersji 2](../concepts-pipelines-activities.md).

Ten artykuł ułatwia zapoznanie się z potokami i działaniami w usłudze Azure Data Factory oraz z konstruowaniem za ich pomocą pełnych przepływów pracy dla scenariuszy przenoszenia i przetwarzania danych.  

> [!NOTE]
> W tym artykule przyjęto założenie, że przejściu [wprowadzenie do fabryki danych Azure](data-factory-introduction.md). Jeśli nie masz hands-na-doświadczenie w tworzeniu fabryki danych, pośrednictwa [samouczek przekształcania danych](data-factory-build-your-first-pipeline.md) i/lub [samouczek przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) można lepiej zrozumieć, w tym artykule.  

## <a name="overview"></a>Przegląd
Fabryka danych może obejmować jeden lub wiele potoków. Potoki to logiczne grupy działań, które wspólnie wykonują zadanie. Działania w potoku definiują akcje do wykonania na danych. Możesz na przykład użyć działania kopiowania w celu skopiowania danych z lokalnego programu SQL Server do usługi Azure Blob Storage. Następnie użyj działania usługi Hive, które uruchamia skrypt Hive w klastrze usługi Apache HDInsight w celu przetworzenia/przekształcenia danych z magazynu obiektów blob, aby utworzyć dane wyjściowe. Na koniec użyj drugiego działania kopiowania w celu skopiowania danych wyjściowych do usługi Microsoft Azure SQL Data Warehouse, na podstawie której tworzone są rozwiązania raportowania analizy biznesowej (BI). 

Dane działanie może — ale nie musi — korzystać z wejściowych [zestawów danych](data-factory-create-datasets.md) i generować co najmniej jeden wyjściowy [zestaw danych](data-factory-create-datasets.md). Na poniższym diagramie przedstawiono relację między potokiem, działaniem i zestawem danych w usłudze Data Factory: 

![Relacja między potoku, działania i zestawu danych](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Potok umożliwia zarządzanie działania zgodnie z ustaleniami zamiast nich osobno. Na przykład można wdrożyć, zaplanować, wstrzymać i wznowić potoku, zamiast dotyczących działania w potoku niezależnie.

Usługa Data Factory obsługuje dwa typy działań — w zakresie przekształcania oraz przenoszenia danych. Każde działanie może mieć zero lub więcej danych wejściowych [zestawów danych](data-factory-create-datasets.md) i tworzące co najmniej jeden wyjściowy zestaw danych.

Zestaw danych wejściowych reprezentuje dane wejściowe dla działania w potoku, a zestaw danych wyjściowych reprezentuje dane wyjściowe dla działania. Zestawy danych identyfikują dane w różnych magazynach danych, takich jak tabele, pliki, foldery i dokumenty. Po utworzeniu zestawu danych można go użyć z działaniami w potoku. Na przykład zestaw danych może być zestawem danych wejściowych/wyjściowych działania kopiowania lub działania HDInsightHive. Aby uzyskać więcej informacji na temat zestawów danych, zobacz artykuł [Datasets in Azure Data Factory](data-factory-create-datasets.md) (Zestawy danych w usłudze Azure Data Factory).

### <a name="data-movement-activities"></a>Działania dotyczące przenoszenia danych
Działanie kopiowania w usłudze Data Factory kopiuje dane z magazynu danych źródła do magazynu danych ujścia. Usługa Data Factory obsługuje następujące magazyny danych. Dane z dowolnego źródła można zapisać do dowolnego ujścia. Kliknij magazyn danych, aby dowiedzieć się, jak kopiować dane do i z tego magazynu.

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Magazyny danych oznaczone znakiem * mogą być konfigurowane lokalnie lub w usłudze Azure IaaS i wymagają zainstalowania [bramy zarządzania danymi](data-factory-data-management-gateway.md) na maszynie lokalnej lub w usłudze Azure IaaS.

Aby uzyskać więcej informacji, zobacz artykuł [Działania dotyczące przenoszenia danych](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Działania dotyczące przekształcania danych
[!INCLUDE [data-factory-transformation-activities](../../../includes/data-factory-transformation-activities.md)]

Aby uzyskać więcej informacji, zobacz artykuł [Działania dotyczące przekształcania danych](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Niestandardowe działania programu .NET 
Jeśli musisz przenieść, zapisać danych do/z danych czy aktywność kopiowania nie obsługuje, lub Przekształcanie danych za pomocą własną logikę, Utwórz **działania niestandardowego .NET**. Aby uzyskać szczegółowe informacje na temat tworzenia i używania niestandardowego działania, zobacz artykuł [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) (Korzystanie z niestandardowych działań w potoku usługi Azure Data Factory).

## <a name="schedule-pipelines"></a>Potoki harmonogramu
Potok jest aktywna tylko między jego **start** czasu i **zakończenia** czasu. Nie jest wykonywany przed godziną rozpoczęcia lub późniejsza niż godzina zakończenia. Jeśli potoku jest wstrzymana, nie zostanie wykonana niezależnie od jego czas rozpoczęcia i zakończenia. Dla potoku do uruchamiania jego powinien nie można wstrzymać. Zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) zrozumieć, jak działa planowania i wykonywania w fabryce danych Azure.

## <a name="pipeline-json"></a>Format JSON potoku
Przyjrzyjmy się bliżej definicji potoku w formacie JSON. Ogólna struktura potoku wygląda następująco:

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
| name |Nazwa potoku. Określ nazwę, która reprezentuje akcję wykonywaną przez potok. <br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Yes |
| description | Wprowadź tekst opisujący przeznaczenie potoku. |Yes |
| activities | W sekcji **activities** można zdefiniować jedno lub więcej działań. Zobacz następną sekcję, aby uzyskać szczegółowe informacje dotyczące działań elementu JSON. | Yes |  
| rozpoczynanie | Data i godzina rozpoczęcia dla potoku. Musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Na przykład: `2016-10-14T16:32:41Z`. <br/><br/>Użytkownik może określić czas lokalny, na przykład czas EST. Oto przykład: `2016-02-27T06:00:00-05:00`", która jest szacowana AM 6<br/><br/>Właściwości początkową i końcową razem Określ aktywny okres potoku. Wycinki danych wyjściowych tylko są tworzone z aktywny okres. |Nie<br/><br/>Jeśli określono wartość dla właściwości końca, należy określić wartość dla właściwości rozpoczęcia.<br/><br/>Godziny rozpoczęcia i zakończenia może jednocześnie być puste, aby utworzyć potok. Należy określić zarówno wartości można ustawić okresu aktywności w potoku do uruchamiania. Jeśli nie określono godziny rozpoczęcia i zakończenia podczas tworzenia potoku, można ustawić ich później za pomocą polecenia cmdlet Set-AzureRmDataFactoryPipelineActivePeriod. |
| end | Data czas zakończenia dla potoku. Jeśli zostanie określona, musi być w formacie ISO. Na przykład: `2016-10-14T17:32:41Z` <br/><br/>Użytkownik może określić czas lokalny, na przykład czas EST. Oto przykład: `2016-02-27T06:00:00-05:00`, która jest szacowana AM 6<br/><br/>Aby działają przez nieograniczony czas potoku, należy określić 9999-09-09 jako wartość właściwości end. <br/><br/> Potok jest aktywna tylko między jego czas rozpoczęcia i godzina zakończenia. Nie jest wykonywany przed godziną rozpoczęcia lub późniejsza niż godzina zakończenia. Jeśli potoku jest wstrzymana, nie zostanie wykonana niezależnie od jego czas rozpoczęcia i zakończenia. Dla potoku do uruchamiania jego powinien nie można wstrzymać. Zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) zrozumieć, jak działa planowania i wykonywania w fabryce danych Azure. |Nie <br/><br/>Jeśli określono wartość dla właściwości rozpoczęcia, należy określić wartość dla właściwości end.<br/><br/>Zobacz uwagi dla **start** właściwości. |
| isPaused | Jeśli ma wartość true, potoku nie działa. Jest w stanie wstrzymania. Wartość domyślna = false. Ta właściwość umożliwia włączanie lub wyłączanie potoku. |Nie |
| pipelineMode | Metoda planowania działa dla potoku. Dozwolone wartości to: (domyślnie), zaplanowane jednorazowe.<br/><br/>"Zaplanowana" wskazuje, że potoku jest uruchamiane w określonych odstępach czasu zgodnie z jego aktywny okres (czas rozpoczęcia i zakończenia). "Jednorazowe" wskazuje, że potoku jest uruchamiana tylko raz. Potoki jednorazowe utworzonej nie może być zmodyfikowany zaktualizowane obecnie. Zobacz [potoku Onetime](#onetime-pipeline) szczegółowe informacje o ustawienie jednorazowe. |Nie |
| expirationTime | Czas, po utworzeniu, dla którego [potoku jednorazowego](#onetime-pipeline) jest prawidłowa i powinny być zainicjowana. Jeśli nie ma żadnych aktywnych nie powiodło się, lub oczekujące działa, proces zostanie automatycznie usunięta po osiągnie czas wygaśnięcia. Wartość domyślna:`"expirationTime": "3.00:00:00"`|Nie |
| Zbiory danych |Lista zestawów danych, który będzie używany przez działania zdefiniowane w potoku. Ta właściwość może służyć do definiowania zestawów danych, które są specyficzne dla tego potoku i nie jest zdefiniowany w fabryce danych. Zestaw danych zdefiniowany w ramach tego potoku można używać tylko w ramach tego potoku i nie może zostać udostępniony. Zobacz [zakres zestawów danych](data-factory-create-datasets.md#scoped-datasets) szczegółowe informacje. |Nie |

## <a name="activity-json"></a>Format JSON działania
W sekcji **activities** można zdefiniować jedno lub więcej działań. Każde działanie ma następującą strukturę najwyższego poziomu:

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

Poniższa tabela zawiera opis właściwości w definicji JSON działania:

| Tag | Opis | Wymagane |
| --- | --- | --- |
| name | Nazwa działania. Określ nazwę, która reprezentuje akcję wykonywaną przez działanie. <br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Yes |
| description | Tekst opisujący przeznaczenie działania |Yes |
| type | Typ działania. Zobacz [działań przepływu danych](#data-movement-activities) i [działań przekształcania danych](#data-transformation-activities) sekcje dla różnych typów działań. |Yes |
| Dane wejściowe |Tabele wejściowe używane na potrzeby działania<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Yes |
| wyjścia |Tabele wyjściowe używany przez działanie.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Yes |
| linkedServiceName |Nazwa połączonej usługi używana na potrzeby działania. <br/><br/>Działanie może wymagać określenia połączonej usługi, która stanowi łącze do wymaganego środowiska obliczeniowego. |Tak w przypadku działania usługi HDInsight i Azure Machine Learning działanie wsadowego oceniania <br/><br/>Nie dla wszystkich innych |
| typeProperties |Właściwości w **typeProperties** sekcji są zależne od typu działania. Aby wyświetlić właściwości typu dla działania, kliknij linki do działań w poprzedniej sekcji. | Nie |
| policy |Zasady, które mają wpływ na zachowanie działania w czasie wykonania. Jeśli nie zostanie określona, używane są zasady domyślne. |Nie |
| Harmonogram | Właściwość "harmonogramu" służy do definiowania żądanego planowania dla działania. Właściwości podrzędnych są takie same jak te w [właściwości availability w zestawie danych](data-factory-create-datasets.md#dataset-availability). |Nie |


### <a name="policies"></a>Zasady
Zasady wpływają na zachowanie czasu wykonania działania, w szczególności, podczas przetwarzania wycinka tabeli. Poniższa tabela zawiera szczegółowe informacje.

| Właściwość | Dozwolone wartości | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| Współbieżność |Liczba całkowita <br/><br/>Wartość maksymalna: 10 |1 |Liczba równoczesnych wykonania działania.<br/><br/>Określa Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków. Na przykład jeśli działanie musi przechodzić przez duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza przetwarzania danych. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Określa kolejność wycinki danych, które są przetwarzane.<br/><br/>Na przykład jeśli masz wycinków 2 (w toku co 4 godziny, a innym godzinie 5), a oba oczekują na wykonanie. Jeśli ustawisz executionPriorityOrder jako NewestFirst wycinka godzinie 5 jest przetwarzana najpierw. Podobnie jeśli ustawisz executionPriorityORder jako OldestFIrst wycinka godzinie 4 jest przetwarzany. |
| retry |Liczba całkowita<br/><br/>Maksymalna wartość może być 10 |0 |Liczba ponownych prób przed przetwarzania danych dla wycinka jest oznaczony jako błąd. Do określonego ponownych próba zostanie ponowiona wykonania działania dla wycinka danych. Ponów próbę odbywa się jak najszybciej po awarii. |
| timeout |TimeSpan |00:00:00 |Limit czasu działania. Przykład: 00:10:00 (oznacza limitu 10 minut)<br/><br/>Jeśli wartość nie została określona lub jest równa 0, limit czasu to nieskończoność.<br/><br/>Jeśli czas przetwarzania danych na wycinek przekracza wartość limitu czasu, anulowaniu, a system podejmuje próbę przetwarzania. Liczba ponownych prób zależy od właściwości ponów próbę. W przypadku przekroczenia limitu czasu stan jest ustawiony na upłynął limit czasu. |
| Opóźnienie |TimeSpan |00:00:00 |Określ opóźnienie przetwarzania danych powoduje uruchomienie wycinka.<br/><br/>Wykonanie działań dotyczących wycinek danych jest uruchomiona po opóźnienie oczekiwany czas wykonywania.<br/><br/>Przykład: 00:10:00 (oznacza opóźnienia w ciągu 10 minut) |
| Parametr longRetry |Liczba całkowita<br/><br/>Wartość maksymalna: 10 |1 |Liczba długa ponownych prób przed wycinek wykonanie nie powiodło się.<br/><br/>Parametr longRetry prób uzyskają przez longRetryInterval. Dlatego jeśli trzeba określić czas między ponownymi próbami, użyj longRetry. Jeśli został określony zarówno longRetry, jak i ponów próbę, każdej próbie longRetry zawiera ponownych prób i maksymalną liczbę prób ponawiania * longRetry.<br/><br/>Na przykład, jeśli mamy poniższe ustawienia w zasadach działania:<br/>Spróbuj ponownie: 3<br/>Parametr longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Załóżmy istnieje tylko jeden wycinek do wykonania (oczekiwanie stanu) i wykonania działania zawsze kończy się niepowodzeniem. Początkowo może być 3 wykonywanie kolejnych prób. Po każdej próbie stanu wycinka byłoby ponów próbę. Po pierwsze 3 prób się za pośrednictwem stanu wycinka będą LongRetry.<br/><br/>Po upływie godziny (to znaczy wartość longRetryInteval w) będzie inny zestaw 3 wykonywanie kolejnych prób. Po wykonaniu tej nie będzie można stanu wycinka i będą podejmowane próby. Dlatego całkowity 6 podejmowano.<br/><br/>Jeśli wykonanie żadnych zakończy się powodzeniem, stan wycinek jest gotowy, a próby są próby.<br/><br/>Parametr longRetry mogą być używane w sytuacji, w których danych zależnych dociera deterministyczna razy lub ogólnej środowiska jest niestabilnym, w których przetwarzania danych. W takich przypadkach to ponownych prób po kolei może nie pomagają i w ten sposób po interwału czasu powoduje żądanego wyniku.<br/><br/>Word Przestroga: nie należy ustawiać wysokiej wartości longRetry lub longRetryInterval. Zazwyczaj wyższej wartości oznacza innych kwestii systemowych. |
| longRetryInterval |TimeSpan |00:00:00 |Opóźnienie między próbami czas ponów |

## <a name="sample-copy-pipeline"></a>Przykładowy potok kopiowania
W poniższym przykładowym potoku występuje jedno działanie typu **Copy** w sekcji **activities**. W tym przykładzie [działanie copy](data-factory-data-movement-activities.md) kopiuje dane z usługi Azure Blob Storage do usługi Azure SQL Database. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
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

Pamiętaj o następujących kwestiach:

* W sekcji działań jest tylko jedno działanie, którego parametr **type** (typ) został ustawiony na wartość **Copy**.
* Dane wejściowe dla działania mają ustawienie **InputDataset**, a dane wyjściowe — **OutputDataset**. Definiowanie zestawów danych w formacie JSON opisano w artykule [Zestawy danych](data-factory-create-datasets.md). 
* W sekcji **typeProperties** parametr **BlobSource** został określony jako typ źródłowy, a parametr **SqlSink** został określony jako typ ujścia. W [działań przepływu danych](#data-movement-activities) sekcji, kliknij przechowywać dane chcesz używać jako źródła lub zbiorniku, aby dowiedzieć się więcej na temat przenoszenia danych do/z tego magazynu danych. 

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob do bazy danych SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Przykładowy potok przekształcania
W poniższym przykładowym potoku występuje jedno działanie typu **HDInsightHive** w sekcji **activities**. W tym przykładzie [działanie HDInsight Hive](data-factory-hive-activity.md) przekształca dane z usługi Azure Blob Storage przez uruchomienie pliku skryptu Hive na klastrze usługi Azure HDInsight Hadoop. 

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

Pamiętaj o następujących kwestiach: 

* W sekcji działań jest tylko jedno działanie, którego parametr **type** został ustawiony na wartość **HDInsightHive**.
* Plik skryptu programu Hive **partitionweblogs.hql** jest przechowywany na koncie usługi Azure Storage (określonym za pomocą elementu scriptLinkedService o nazwie **AzureStorageLinkedService**) oraz w folderze **script** w kontenerze **adfgetstarted**.
* `defines` Sekcji służy do określania ustawienia środowiska uruchomieniowego, które są przekazywane do skryptu hive jako wartości konfiguracji gałąź (np. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Sekcja **typeProperties** jest inna dla każdego działania przekształcania. Informacje na temat właściwości typu obsługiwane dla działania przekształcania, kliknij działanie transformacji w [działań przekształcania danych](#data-transformation-activities) tabeli. 

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: tworzenie swój pierwszy potok do przetwarzania danych przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Wiele działań w potoku
Poprzednie dwa przykładowe potoki zawierają tylko po jednym działaniu. Potok może obejmować więcej niż jedno działanie.  

Jeśli masz wiele działań w potoku dane wyjściowe działania nie jest wejściem innego działania, działania mogą działać równolegle Jeśli wycinki danych wejściowych dla działania jest gotowe. 

Powiązane z dwóch działań, konfigurując wyjściowy zestaw danych z jednego działania jako wejściowego zestawu danych z innych działań. Drugi działania wykonuje, tylko jeśli pierwsza z nich zakończy się pomyślnie.

![Tworzenie łańcuchów działań w tym samym potoku](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

W tym przykładzie potoku ma dwa działania: działania Activity1 i Activity2. Działania Activity1 przyjmuje Dataset1 jako dane wejściowe i generuje dane wyjściowe Dataset2. Działanie przyjmuje Dataset2 jako dane wejściowe i generuje dane wyjściowe Dataset3. Ponieważ dane wyjściowe działania Activity1 (Dataset2) jest Activity2, uruchamia Activity2 tylko wtedy, gdy działanie zakończy się pomyślnie i utworzenie wycinka Dataset2 danych wejściowych. Jeśli działania Activity1 jakiegoś powodu nie powiedzie się i nie tworzy wycinek Dataset2, 2 działania nie zostanie uruchomiony dla tego wycinka (na przykład: 9 AM do 10 AM). 

Można również łańcucha działań, które znajdują się w różnych potoków.

![Tworzenie łańcuchów działań w dwóch potoki](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

W tym przykładzie Pipeline1 ma tylko jedno działanie, która przyjmuje Dataset1 jako dane wejściowe i tworzy Dataset2 jako dane wyjściowe. Pipeline2 ma również tylko jedno działanie, który pobiera Dataset2 jako dane wejściowe i Dataset3 jako dane wyjściowe. 

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

Zobacz następujące samouczki krok po kroku tworzenia potoki przy użyciu jednej z tych narzędzi i zestawy SDK.
 
- [Tworzenie potoku z działaniem przekształcania danych](data-factory-build-your-first-pipeline.md)
- [Tworzenie potoku z działaniem przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Po potoku jest utworzony wdrożone, można zarządzać i monitorować Twoje potoki przy użyciu bloków portalu Azure lub monitora i zarządzania aplikacji. Zobacz poniższe tematy zawierają instrukcje krok po kroku. 

- [Monitorowanie i zarządzanie nimi potoki przy użyciu bloków portalu Azure](data-factory-monitor-manage-pipelines.md).
- [Monitorowanie i zarządzanie nimi potoki za pomocą monitora i zarządzanie aplikacjami](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Jednorazowe potoku
Możesz utworzyć i zaplanować potoku do uruchamiania okresowo (na przykład: co godzinę lub codziennie) w ciągu godziny rozpoczęcia i zakończenia określonego w definicji potoku. Zobacz [planowania wykonania](#scheduling-and-execution) szczegółowe informacje. Można również utworzyć potok, który jest uruchamiany tylko raz. Aby to zrobić, należy ustawić **pipelineMode** właściwości w definicji potoku **jednorazowe** jak pokazano w poniższym przykładzie JSON. Wartość domyślna dla tej właściwości to **zaplanowane**.

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

Pamiętaj o następujących kwestiach:

* **Uruchom** i **zakończenia** nie określono godziny dla potoku.
* **Dostępność** danych wejściowych i wyjściowych zestawów danych jest określony (**częstotliwość** i **interwał**), nawet jeśli fabryki danych nie używa wartości.  
* Widok diagramu jednorazowe potoki nie są wyświetlane. To zachowanie jest celowe.
* Nie można zaktualizować jednorazowe potoków. Można sklonować potoku jednorazowego, zmień jego nazwę, zaktualizuj właściwości i wdróż je aby utworzyć nową.


## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat zestawów danych, zobacz [utworzyć zestawy danych](data-factory-create-datasets.md) artykułu. 
- Aby uzyskać więcej informacji o sposobie planowania i wykonywania potoków, zobacz [planowania i wykonywania w fabryce danych Azure](data-factory-scheduling-and-execution.md) artykułu. 
  

