---
title: "aaaTransform danych przy użyciu działania Pig w fabryce danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się używania hello Pig działania w skryptów usługi Pig toorun usługi Azure data factory w klastrze usługi HDInsight na — żądanie/swój własny."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Przekształcanie danych za pomocą działania Pig w fabryce danych Azure
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

Witaj HDInsight Pig działania w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje zapytania Pig na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux. W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.

> [!NOTE] 
> Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu. 

## <a name="syntax"></a>Składnia

```JSON
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
## <a name="syntax-details"></a>Szczegóły składni
| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa działania hello |Tak |
| description |Tekst opisujący, jakie działanie hello jest używany dla |Nie |
| type |HDinsightPig |Tak |
| Dane wejściowe |Co najmniej jeden dane wejściowe używane przez hello działania Pig |Nie |
| dane wyjściowe |Jeden lub więcej danych wyjściowych utworzonego przez hello działania Pig |Tak |
| linkedServiceName |Klaster usługi HDInsight toohello odwołanie w zarejestrowany jako połączonej usługi z fabryki danych |Tak |
| Skrypt |Określ hello Pig skrypt wbudowany |Nie |
| Ścieżka skryptu |Przechowywanie skrypt programu Pig hello w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku. Użyj właściwości 'script' lub "scriptPath". Nie można używać razem. Nazwa pliku Hello jest rozróżniana wielkość liter. |Nie |
| Definiuje |Określ parametry jako pary klucz wartość dla przywołującego w hello skrypt programu Pig |Nie |

## <a name="example"></a>Przykład
Zastanówmy się przykładem gry rejestruje analytics miejscu tooidentify hello czasu poświęcanego przez odtwarzacze granie w gry uruchomiony przez firmę.

następującego przykładowego dziennika gier Hello jest plików rozdzielanych przecinkami (,). Zawiera ona następujące pola — ProfileID, SessionStart, czas trwania, SrcIPAddress i GameType hello.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Witaj **wieprzowa skryptu** tooprocess te dane:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

tooexecute Pig tego skryptu w potoku fabryki danych hello następujące kroki:

1. Utwórz tooregister połączonej usługi [klaster obliczeniowy własne HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub skonfiguruj [klastra obliczeniowego HDInsight na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Umożliwia wywołanie tej połączonej usługi **HDInsightLinkedService**.
2. Utwórz [połączona usługa](data-factory-azure-blob-connector.md) tooconfigure hello połączenia tooAzure obiektu Blob magazynu obsługującego hello danych. Umożliwia wywołanie tej połączonej usługi **StorageLinkedService**.
3. Utwórz [zestawów danych](data-factory-create-datasets.md) wskazanie toohello dane wejściowe i hello dane wyjściowe. Teraz wywołać zestawu danych wejściowych hello **PigSampleIn** i hello wyjściowy zestaw danych **PigSampleOut**.
4. Skopiuj zapytanie Pig hello w pliku hello skonfigurowane w kroku #2 magazynu obiektów Blob Azure. Jeśli hello magazynu platformy Azure obsługującym hello danych różni się od hello jedną obsługującego hello pliku zapytania, Utwórz oddzielne połączoną usługą magazynu Azure. Można znaleźć usługi toohello połączone w hello działania konfiguracji. Użyj ** scriptPath ** pliku skryptu toopig toospecify hello ścieżki i **scriptLinkedService**. 
   
   > [!NOTE]
   > Można też podać hello Pig skrypt wbudowany w definicji działania hello przy użyciu hello **skryptu** właściwości. Jednak nie zaleca tego podejścia jako wszystkie znaki specjalne w skrypcie hello musi toobe anulowane i może spowodować problemy debugowania. Witaj najlepszym rozwiązaniem jest toofollow krok #4.
   > 
   > 
5. Tworzenie potoku hello z hello HDInsightPig działania. To działanie przetwarza dane wejściowe hello, uruchamiając skrypt programu Pig w klastrze usługi HDInsight.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
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
6. Wdróż hello potoku. Zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu, aby uzyskać szczegółowe informacje. 
7. Monitorowanie za pomocą funkcji monitorowania fabryki danych hello potoku hello i widoki zarządzania. Zobacz [monitorowanie i zarządzanie nimi potoki fabryki danych](data-factory-monitor-manage-pipelines.md) artykułu, aby uzyskać szczegółowe informacje.

## <a name="specifying-parameters-for-a-pig-script"></a>Określanie parametrów dla skryptu Pig
Należy wziąć pod uwagę hello poniższy przykład: gier dzienniki są codziennie pozyskanych w magazynie obiektów Blob Azure i przechowywane w folderze partycjonowanej na podstawie daty i godziny. Mają skrypt programu Pig hello tooparameterize i przekazać lokalizacji folderu wejściowych hello dynamicznie w czasie wykonywania, a także wygenerować hello dane wyjściowe z Data i godzina.

toouse sparametryzowana skrypt programu Pig, wykonaj następujące hello:

* Zdefiniuj parametry hello w **definiuje**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
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
* W hello skrypt programu Pig, można znaleźć przy użyciu parametrów toohello "**$parameterName**" jak pokazano w hello poniższy przykład:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Zobacz też
* [Działanie gałęzi](data-factory-hive-activity.md)
* [Działania MapReduce](data-factory-map-reduce.md)
* [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
* [Wywoływanie programów platformy Spark](data-factory-spark.md)
* [Wywoływanie skryptów języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

