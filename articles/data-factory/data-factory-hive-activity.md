---
title: "aaaTransform danych przy użyciu Hive działania - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się używania hello Hive działania w zapytań Hive toorun fabryki danych Azure w klastrze usługi HDInsight na — żądanie/swój własny."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Przekształcanie danych za pomocą działania Hive w fabryce danych Azure 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Działanie gałęzi](data-factory-hive-activity.md) 
> * [Działanie pig](data-factory-pig-activity.md)
> * [Działania MapReduce](data-factory-map-reduce.md)
> * [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Działanie Spark](data-factory-spark.md)
> * [Działanie wykonywania wsadowego w usłudze Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Działania aktualizowania zasobów w usłudze Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Działania procedur składowanych](data-factory-stored-proc-activity.md)
> * [Działania języka U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Działania niestandardowe .NET](data-factory-use-custom-activities.md)

Hello HDInsight Hive działania w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje zapytania Hive na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux. W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.

> [!NOTE] 
> Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu. 

## <a name="syntax"></a>Składnia

```JSON
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
## <a name="syntax-details"></a>Szczegóły składni
| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa działania hello |Tak |
| description |Tekst opisujący, jakie działanie hello jest używany dla |Nie |
| type |HDinsightHive |Tak |
| Dane wejściowe |Dane wejściowe używane na powitania Hive działania |Nie |
| dane wyjściowe |Dane wyjściowe, generowane przez działanie Hive hello |Tak |
| linkedServiceName |Klaster usługi HDInsight toohello odwołanie w zarejestrowany jako połączonej usługi z fabryki danych |Tak |
| Skrypt |Określ wbudowanego skryptu Hive hello |Nie |
| Ścieżka skryptu |Magazyn hello Hive skryptu w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku. Użyj właściwości 'script' lub "scriptPath". Nie można używać razem. Nazwa pliku Hello jest rozróżniana wielkość liter. |Nie |
| Definiuje |Określ parametry jako pary klucz wartość dla odwołania do skryptu Hive hello za pomocą "hiveconf" |Nie |

## <a name="example"></a>Przykład
Zastanówmy się przykładem gry rejestruje analytics miejscu tooidentify hello czasu poświęcanego przez użytkowników granie w gry uruchomiony przez firmę. 

Hello następujące dziennik jest przykładowy dziennik gier, czyli przecinkami (`,`) oddzielone i zawiera następujące pola — ProfileID, SessionStart, czas trwania, SrcIPAddress i GameType hello.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Witaj **wykonanie skryptu technologii Hive** tooprocess te dane:

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

tooexecute tej gałęzi skryptu w potoku fabryki danych, należy toodo hello poniżej

1. Utwórz tooregister połączonej usługi [klaster obliczeniowy własne HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub skonfiguruj [klastra obliczeniowego HDInsight na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Umożliwia wywołanie tej połączonej usługi "HDInsightLinkedService".
2. Utwórz [połączona usługa](data-factory-azure-blob-connector.md) tooconfigure hello połączenia tooAzure obiektu Blob magazynu obsługującego hello danych. Umożliwia wywołanie tej połączonej usługi "StorageLinkedService"
3. Utwórz [zestawów danych](data-factory-create-datasets.md) wskazanie toohello dane wejściowe i hello dane wyjściowe. Umożliwia wywołanie hello wejściowy zestaw danych "HiveSampleIn" i hello wyjściowy zestaw danych "HiveSampleOut"
4. Skopiuj zapytanie Hive hello jako plik tooAzure skonfigurowane w kroku #2 magazynu obiektów Blob. Jeśli hello magazynu do obsługi danych hello różni się od hello jedną hosting tego pliku kwerendy, Utwórz oddzielne połączoną usługą magazynu Azure i zapoznaj tooit w działaniu hello. Użyj ** scriptPath ** toospecify hello ścieżki toohive zapytania pliku i **scriptLinkedService** toospecify hello Azure magazynu, który zawiera plik skryptu hello. 
   
   > [!NOTE]
   > Można też podać wbudowanego skryptu Hive hello w definicji działania hello przy użyciu hello **skryptu** właściwości. Nie zaleca się tą metodą wszystkie znaki specjalne w skrypcie hello w dokumencie JSON hello musi toobe zmienione znaczenie i mogą Przyczyna debugowanie problemów. Witaj najlepszym rozwiązaniem jest toofollow krok #4.
   > 
   > 
5. Utworzyć potok z hello HDInsightHive działania. działanie Hello procesów/transformacje hello danych.

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Wdróż hello potoku. Zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu, aby uzyskać szczegółowe informacje. 
7. Monitorowanie za pomocą funkcji monitorowania fabryki danych hello potoku hello i widoki zarządzania. Zobacz [monitorowanie i zarządzanie nimi potoki fabryki danych](data-factory-monitor-manage-pipelines.md) artykułu, aby uzyskać szczegółowe informacje. 

## <a name="specifying-parameters-for-a-hive-script"></a>Określanie parametrów dla skryptu Hive
W tym przykładzie gier dzienniki są codziennie pozyskanych w magazynie obiektów Blob Azure i są przechowywane w folderze na partycje za pomocą daty i godziny. Mają skryptu Hive hello tooparameterize i przekazać lokalizacji folderu wejściowych hello dynamicznie w czasie wykonywania, a także wygenerować hello dane wyjściowe z datę i godzinę.

toouse sparametryzowana skryptu Hive, wykonaj następujące hello

* Zdefiniuj parametry hello w **definiuje**.

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* W hello skryptu Hive, można znaleźć przy użyciu parametru toohello **${hiveconf:parameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>Zobacz też
* [Działanie pig](data-factory-pig-activity.md)
* [Działania MapReduce](data-factory-map-reduce.md)
* [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
* [Wywoływanie programów platformy Spark](data-factory-spark.md)
* [Wywoływanie skryptów języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

