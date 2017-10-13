---
title: "Potoki i działania w usłudze Azure Data Factory | Microsoft Docs"
description: "Informacje na temat potoków i działań w usłudze Azure Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/17/2017
ms.author: shlo
ms.openlocfilehash: 6dcc5c55fae5e2494526c492a1453747b4d6e179
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Potoki i działania w usłudze Azure Data Factory 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](v1/data-factory-create-pipelines.md)
> * [Wersja 2 — wersja zapoznawcza](concepts-pipelines-activities.md)

Ten artykuł ułatwia zapoznanie się z potokami i działaniami w usłudze Azure Data Factory oraz z konstruowaniem za ich pomocą pełnych przepływów pracy dla scenariuszy przenoszenia i przetwarzania danych.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz [Pipelines in Data Factory version 1](v1/data-factory-create-pipelines.md) (Potoki w usłudze Data Factory w wersji 1).
> 
> W tym artykule założono, że znasz już artykuł [Wprowadzenie do usługi Azure Data Factory ](introduction.md) i [samouczek Szybki start](quickstart-create-data-factory-powershell.md).

## <a name="overview"></a>Omówienie
Fabryka danych może obejmować jeden lub wiele potoków. Potoki to logiczne grupy działań, które wspólnie wykonują zadanie. Na przykład potok może zawierać zestaw działań, które pozyskują i oczyszczają dane dziennika, a następnie uruchamiają zadanie usługi Spark na klastrze HDInsight w celu przeanalizowania danych dziennika. Zaletą korzystania z potoku jest możliwość zarządzania działaniami jako zestawem, a nie indywidualnie. Na przykład zamiast zarządzać poszczególnymi działaniami można wdrożyć i zaplanować potok.  

Działania w potoku definiują akcje do wykonania na danych. Możesz na przykład użyć działania kopiowania w celu skopiowania danych z lokalnego programu SQL Server do usługi Azure Blob Storage. Następnie użyj działania usługi Hive, które uruchamia skrypt Hive w klastrze usługi Apache HDInsight w celu przetworzenia/przekształcenia danych z magazynu obiektów blob, aby utworzyć dane wyjściowe. Na koniec użyj drugiego działania kopiowania w celu skopiowania danych wyjściowych do usługi Microsoft Azure SQL Data Warehouse, na podstawie której tworzone są rozwiązania raportowania analizy biznesowej (BI).

Usługa Data Factory obsługuje trzy typy działań: [działania przenoszenia danych](copy-activity-overview.md), [działania przekształcania danych](transform-data.md) i [działania sterowania](control-flow-web-activity.md). Dane działanie może — ale nie musi — korzystać z wejściowych [zestawów danych](concepts-datasets-linked-services.md) i generować co najmniej jeden wyjściowy [zestaw danych](concepts-datasets-linked-services.md). Na poniższym diagramie przedstawiono relację między potokiem, działaniem i zestawem danych w usłudze Data Factory:

![Relacja między zestawem danych, działaniem i potokiem](media/concepts-pipelines-activities/relationship-between-dataset-pipeline-activity.png)

Zestaw danych wejściowych reprezentuje dane wejściowe dla działania w potoku, a zestaw danych wyjściowych reprezentuje dane wyjściowe dla działania. Zestawy danych identyfikują dane w różnych magazynach danych, takich jak tabele, pliki, foldery i dokumenty. Po utworzeniu zestawu danych można go użyć z działaniami w potoku. Na przykład zestaw danych może być zestawem danych wejściowych/wyjściowych działania kopiowania lub działania HDInsightHive. Aby uzyskać więcej informacji na temat zestawów danych, zobacz artykuł [Datasets in Azure Data Factory](concepts-datasets-linked-services.md) (Zestawy danych w usłudze Azure Data Factory).

## <a name="data-movement-activities"></a>Działania dotyczące przenoszenia danych
Działanie kopiowania w usłudze Data Factory kopiuje dane z magazynu danych źródła do magazynu danych ujścia. Usługa Data Factory obsługuje magazyny danych wymienione w tabeli w tej sekcji. Dane z dowolnego źródła można zapisać do dowolnego ujścia. Kliknij magazyn danych, aby dowiedzieć się, jak kopiować dane do i z tego magazynu.

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores.md)]

Aby uzyskać więcej informacji, zobacz artykuł [Działanie kopiowania — omówienie](copy-activity-overview.md).

## <a name="data-transformation-activities"></a>Działania dotyczące przekształcania danych
Usługa Azure Data Factory obsługuje następujące działania przekształcania, które można dodawać indywidualnie do potoków lub łączyć je z innymi działaniami.

Działanie przekształcania danych | Środowisko obliczeniowe
---------------------------- | -------------------
[Hive](transform-data-using-hadoop-hive.md) | HDInsight [Hadoop]
[Pig](transform-data-using-hadoop-pig.md) | HDInsight [Hadoop]
[MapReduce](transform-data-using-hadoop-map-reduce.md) | HDInsight [Hadoop]
[Przesyłanie strumieniowe usługi Hadoop](transform-data-using-hadoop-streaming.md) | HDInsight [Hadoop]
[Spark](transform-data-using-spark.md) | HDInsight [Hadoop]
[Działania usługi Machine Learning: wykonywanie wsadowe i aktualizacja zasobów](transform-data-using-machine-learning.md) | Maszyna wirtualna platformy Azure
[Procedura składowana](transform-data-using-stored-procedure.md) | Azure SQL, Azure SQL Data Warehouse lub SQL Server
[U-SQL](transform-data-using-data-lake-analytics.md) | Azure Data Lake Analytics

Aby uzyskać więcej informacji, zobacz artykuł z [działaniami dotyczącymi przekształcania danych](transform-data.md). 

## <a name="control-activities"></a>Działania sterowania
Obsługiwane są następujące działania przepływu sterowania:

Działanie sterowania | Opis
---------------- | -----------
[Działanie Execute Pipeline](control-flow-execute-pipeline-activity.md) | Działanie Execute Pipeline umożliwia potokowi usługi Data Factory wywoływanie innego potoku.
[Działanie ForEach](control-flow-for-each-activity.md) | Działanie ForEach definiuje powtarzający się przepływ sterowania w potoku. To działanie służy do wykonywania iteracji po kolekcji i wykonuje określone działania w pętli. Implementacja pętli tego działania przypomina strukturę pętli Foreach w językach programowania.
[Działanie WebActivity](control-flow-web-activity.md) | Działanie WebActivity może być używane do wywoływania niestandardowego punktu końcowego REST z potoku usługi Data Factory. Można przekazywać zestawy danych i połączone usługi do zużycia i dostępu przez działanie. 
[Działanie Lookup](control-flow-lookup-activity.md) | Działanie Lookup może być używane do odczytywania lub wyszukiwania rekordu/nazwy tabeli/wartości z dowolnego źródła zewnętrznego. Do tych danych wyjściowych mogą także odwoływać się kolejne działania. 
[Działanie GetMetadata](control-flow-get-metadata-activity.md) | Działanie GetMetadata umożliwia pobieranie metadanych dowolnych danych z usługi Azure Data Factory. 
Działanie Do Until | Wprowadza pętlę Do-Until, przypominającą strukturę pętli Do-Until w językach programowania.
Działanie If Condition | Działanie If Condition umożliwia tworzenie gałęzi na podstawie warunków, które mogą być prawdziwe lub fałszywe. 

## <a name="pipeline-json"></a>Format JSON potoku
Przyjrzyjmy się bliżej definicji potoku w formacie JSON. Ogólna struktura potoku wygląda następująco:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description": "pipeline description",
        "activities":
        [
        ],
        "parameters": {
         }
    }
}
```

Tag | Opis | Typ | Wymagany
--- | ----------- | ---- | --------
name | Nazwa potoku. Określ nazwę, która reprezentuje akcję wykonywaną przez potok. <br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>•   Następujące znaki nie są dozwolone: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\”</li></ul> | Ciąg | Tak
description | Wprowadź tekst opisujący przeznaczenie potoku. | Ciąg | Nie
activities | W sekcji **activities** można zdefiniować jedno lub więcej działań. Sprawdź sekcję [Format JSON działania](#activity-json), aby uzyskać szczegółowe informacje na temat elementu JSON activities. | Tablica | Tak
parameters | Sekcja **parameters** może zawierać jeden lub kilka parametrów zdefiniowanych w potoku, co zwiększa elastyczność i możliwość ponownego zastosowania potoku. | List | Nie

## <a name="activity-json"></a>Format JSON działania
W sekcji **activities** można zdefiniować jedno lub więcej działań. Istnieją dwa główne typy działań: działania wykonywania i sterowania.

### <a name="execution-activities"></a>Działania wykonywania
Działania wykonywania obejmują [działania przenoszenia danych](#data-movement-activities) i [działania przekształcania danych](#data-transformation-activities). Ich struktura najwyższego poziomu wygląda następująco:

```json
{
    "name": "Execution Activity Name",
    "description": "description", 
    "type": "<ActivityType>",
    "typeProperties":
    {
    },
    "linkedServiceName": "MyLinkedService",
    "policy":
    {
    },
    "dependsOn":
    {
    }
}
```

Poniższa tabela zawiera opis właściwości w definicji JSON działania:

Tag | Opis | Wymagany
--- | ----------- | ---------
name | Nazwa działania. Określ nazwę, która reprezentuje akcję wykonywaną przez działanie. <br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\” | Tak</li></ul>
description | Tekst opisujący przeznaczenie działania | Tak
type | Typ działania. Poszczególne typy działań opisano w sekcjach [Działania przenoszenia danych](#data-movement-activities), [Działania przekształcania danych](#data-transformation-activities) i [Działania sterowania](#control-activities). | Tak
linkedServiceName | Nazwa połączonej usługi używana na potrzeby działania.<br/><br/>Działanie może wymagać określenia połączonej usługi, która stanowi łącze do wymaganego środowiska obliczeniowego. | Tak dla działań HDInsight, oceny partii Azure Machine Learning i procedury składowanej. <br/><br/>Nie dla wszystkich innych
typeProperties | Właściwości w sekcji typeProperties zależą od typu działania. Aby wyświetlić właściwości typu dla działania, kliknij linki do działań w poprzedniej sekcji. | Nie
policy | Zasady, które mają wpływ na zachowanie działania w czasie wykonania. Ta właściwość zawiera zachowania związane z limitem czasu i ponownymi próbami. Jeśli nie jest określona, używane są wartości domyślne. Więcej informacji można znaleźć w sekcji [Zasady działania](#activity-policy). | Nie
dependsOn | Ta właściwość jest używana do definiowania zależności działania oraz sposobu, w jaki kolejne działania zależą od poprzednich działań. Więcej informacji można znaleźć w sekcji [Zależności działania](#activity-dependency) | Nie

### <a name="activity-policy"></a>Zasady działania
Zasady wpływają na zachowanie działania w czasie wykonania, określając opcje konfiguracji. Zasady działania są dostępne tylko dla działań wykonywania. 

### <a name="activity-policy-json-definition"></a>Definicja JSON zasad działania

```json
{
    "name": "MyPipelineName",
    "properties": {
      "activities": [
        {
          "name": "MyCopyBlobtoSqlActivity"
          "type": "Copy",
          "typeProperties": {
            ...
          },
         "policy": {
            "timeout": "00:10:00",
            "retry": 1,
            "retryIntervalInSeconds": 60
         }
        }
      ],
        "parameters": {
           ...
        }
    }
}
```
Nazwa JSON | Opis | Dozwolone wartości | Wymagany
--------- | ----------- | -------------- | --------
timeout | Określa limit czasu pracy działania. | Zakres czasu | Nie. Domyślny limit czasu wynosi 7 dni.
retry | Maksymalna liczba ponownych prób | Liczba całkowita | Nie. Wartość domyślna to 0
retryIntervalInSeconds | Opóźnienie między ponownymi próbami w sekundach | Liczba całkowita | Nie. Wartość domyślna to 20 sekund

### <a name="control-activity"></a>Działanie sterowania
Działania sterowania mają następującą strukturę najwyższego poziomu.

```json
{
    "name": "Control Activity Name",
    "description": "description", 
    "type": "<ActivityType>",
    "typeProperties":
    {
    },
    "dependsOn":
    {
    }
}
```

Tag | Opis | Wymagany
--- | ----------- | --------
name | Nazwa działania. Określ nazwę, która reprezentuje akcję wykonywaną przez działanie.<br/><ul><li>Maksymalna liczba znaków: 260</li><li>Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</li><li>Następujące znaki nie są dozwolone: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\” | Tak</li><ul> 
description | Tekst opisujący przeznaczenie działania | Tak
type | Typ działania. Poszczególne typy działań opisano w sekcjach [Działania przenoszenia danych](#data-movement-activities), [Działania przekształcania danych](#data-transformation-activities) i [Działania sterowania](#control-activities). | Tak
typeProperties | Właściwości w sekcji typeProperties zależą od typu działania. Aby wyświetlić właściwości typu dla działania, kliknij linki do działań w poprzedniej sekcji. | Nie
dependsOn | Ta właściwość jest używana do definiowania zależności działania oraz sposobu, w jaki kolejne działania zależą od poprzednich działań. Więcej informacji można znaleźć w sekcji [Zależność działania](#activity-dependency). | Nie

### <a name="activity-dependency"></a>Zależność działania
Zależność działania definiuje, w jaki sposób kolejne działania zależą od poprzednich działań, określając warunek kontynuowania wykonywania kolejnego działania. Działanie może zależeć od jednego lub wielu poprzednich działań, z różnymi warunkami zależności. 

Różne warunki zależności to: Succeeded (powodzenie), Failed (niepowodzenie), Skipped (pominięto) i Completed (ukończono).

Na przykład jeśli potok zawiera zależność Działanie A -> Działanie B, różne możliwe scenariusze to:

- Działanie B zawiera warunek zależności dla Działanie A z parametrem **succeeded**: Działanie B jest uruchamiane tylko wtedy, gdy ostateczny stan Działania A to succeeded
- Działanie B zawiera warunek zależności dla Działanie A z parametrem **failed**: Działanie B jest uruchamiane tylko wtedy, gdy ostateczny stan Działania A to failed
- Działanie B zawiera warunek zależności dla Działanie A z parametrem **completed**: Działanie B jest uruchamiane tylko wtedy, gdy ostateczny stan Działania A to succeeded lub failed
- Działanie B zawiera warunek zależności dla Działanie A z parametrem **skipped**: Działanie B jest uruchamiane tylko wtedy, gdy ostateczny stan Działania A to skipped. Stan skipped występuje w scenariuszu Działanie X -> Działanie Y -> Działanie Z, w którym każde działanie jest uruchamiane tylko w przypadku pomyślnego zakończenia poprzedniego działania. W przypadku niepowodzenia Działania X, Działanie Y ma stan „skipped”, ponieważ nigdy nie zostaje wykonane. Podobnie Działanie Z również ma stan „skipped”.

#### <a name="example-activity-2-depends-on-the-activity-1-succeeding"></a>Przykład: Działanie 2 zależy od pomyślnego zakończenia Działania 1

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description": "pipeline description",
        "activities": [
         {
            "name": "MyFirstActivity",
            "type": "Copy",
            "typeProperties": {
            },
            "linkedServiceName": {
            }
        },
        {
            "name": "MySecondActivity",
            "type": "Copy",
            "typeProperties": {
            },
            "linkedServiceName": {
            },
            "dependsOn": [
            {
                "activity": "MyFirstActivity",
                "dependencyConditions": [
                    "Succeeded"
                ]
            }
          ]
        }
      ],
      "parameters": {
       }
    }
}

```

## <a name="sample-copy-pipeline"></a>Przykładowy potok kopiowania
W poniższym przykładowym potoku występuje jedno działanie typu **Copy** w sekcji **activities**. W tym przykładzie [działanie copy](copy-activity-overview.md) kopiuje dane z usługi Azure Blob Storage do usługi Azure SQL Database.

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
        "policy": {
          "retry": 2,
          "timeout": "01:00:00"
        }
      }
    ]
  }
} 
```
Pamiętaj o następujących kwestiach:

- W sekcji działań jest tylko jedno działanie, którego parametr **type** (typ) został ustawiony na wartość **Copy**.
- Dane wejściowe dla działania mają ustawienie **InputDataset**, a dane wyjściowe — **OutputDataset**. Definiowanie zestawów danych w formacie JSON opisano w artykule [Zestawy danych](concepts-datasets-linked-services.md).
- W sekcji **typeProperties** parametr **BlobSource** został określony jako typ źródłowy, a parametr **SqlSink** został określony jako typ ujścia. W sekcji [działania ruchu danych](#data-movement-activities) kliknij magazyn danych, którego chcesz użyć jako źródła lub ujścia, aby uzyskać dodatkowe informacje na temat przenoszenia danych z/do tego magazynu danych.

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [Szybki start: tworzenie fabryki danych](quickstart-create-data-factory-powershell.md).

## <a name="sample-transformation-pipeline"></a>Przykładowy potok przekształcania
W poniższym przykładowym potoku występuje jedno działanie typu **HDInsightHive** w sekcji **activities**. W tym przykładzie [działanie HDInsight Hive](transform-data-using-hadoop-hive.md) przekształca dane z usługi Azure Blob Storage przez uruchomienie pliku skryptu Hive na klastrze usługi Azure HDInsight Hadoop.

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
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ]
    }
}
```
Pamiętaj o następujących kwestiach:

- W sekcji działań jest tylko jedno działanie, którego parametr **type** został ustawiony na wartość **HDInsightHive**.
- Plik skryptu programu Hive **partitionweblogs.hql** jest przechowywany na koncie usługi Azure Storage (określonym za pomocą elementu scriptLinkedService o nazwie AzureStorageLinkedService) oraz w folderze script w kontenerze `adfgetstarted`.
- Sekcja `defines` służy do określania ustawień środowiska uruchomieniowego, które są przekazywane do skryptu Hive jako wartości konfiguracyjne magazynu Hive (np. $`{hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Sekcja **typeProperties** jest inna dla każdego działania przekształcania. Aby uzyskać informacje na temat właściwości typu obsługiwanych dla działania przekształcania, kliknij działanie przekształcania w sekcji [Działania przekształcania danych](#data-transformation-activities).

Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [Tutorial: transform data using Spark](tutorial-transform-data-spark-powershell.md) (Szybki start: przekształcanie danych przy użyciu usługi Spark). 

## <a name="multiple-activities-in-a-pipeline"></a>Wiele działań w potoku
Poprzednie dwa przykładowe potoki zawierają tylko po jednym działaniu. Potok może obejmować więcej niż jedno działanie. Jeśli potok zawiera wiele działań, a kolejne działania nie są zależne od poprzednich, działania mogą być wykonywane równolegle. 

Można połączyć dwa działania przy użyciu [zależności działania](#activity-dependency), która definiuje, w jaki sposób kolejne działania zależą od poprzednich działań, określając warunek kontynuowania wykonywania kolejnego działania. Działanie może zależeć od jednego lub kilku poprzednich działań, z różnymi warunkami zależności. 

## <a name="scheduling-pipelines"></a>Planowanie potoków
Planowanie potoków odbywa się przy użyciu wyzwalaczy. Istnieją różne typy wyzwalaczy (wyzwalacz harmonogramu, który umożliwia uruchamianie potoków w zależności od godziny, a także wyzwalacz ręczny, który uruchamia potoki na żądanie). Więcej informacji na temat wyzwalaczy zawiera artykuł na temat [wykonywania potoku i wyzwalaczy](concepts-pipeline-execution-triggers.md). 

Aby wyzwalacz uruchamiał potok, należy dołączyć odwołanie do konkretnego potoku do definicji wyzwalacza. Między potokami i wyzwalaczami występuje relacja typu „wiele do wielu”. Wiele wyzwalaczy może uruchamiać jeden potok, a jeden wyzwalacz może uruchamiać wiele potoków. Po zdefiniowaniu wyzwalacza należy go uruchomić, aby rozpoczął wyzwalanie potoków. Więcej informacji na temat wyzwalaczy zawiera artykuł na temat [wykonywania potoku i wyzwalaczy](concepts-pipeline-execution-triggers.md). 

Na przykład załóżmy, że masz wyzwalacz harmonogramu „Trigger A”, który powinien uruchamiać potok „MyCopyPipeline.” Wyzwalacz jest definiowany zgodnie z poniższym przykładem:

### <a name="trigger-a-definition"></a>Definicja wyzwalacza Trigger A

```json
{
  "name": "TriggerA",
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      ...
      }
    },
    "pipeline": {
      "pipelineReference": {
        "type": "PipelineReference",
        "referenceName": "MyCopyPipeline"
      },
      "parameters": {
        "copySourceName": "FileSource"
      }
    }
  }
}
```



## <a name="next-steps"></a>Następne kroki
Następujące samouczki zawierają instrukcje krok po kroku tworzenia potoków z działaniami: 

- [Tworzenie potoku z działaniem kopiowania](quickstart-create-data-factory-powershell.md)
- [Tworzenie potoku z działaniem przekształcania danych](tutorial-transform-data-spark-powershell.md)
