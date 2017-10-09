---
title: aaaInvoke MapReduce Program z fabryki danych Azure
description: "Dowiedz się, jak dane tooprocess uruchamiając programy MapReduce w usłudze Azure HDInsight klastra z fabryki danych Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Wywoływanie programów MapReduce z fabryki danych
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

Witaj działania HDInsight MapReduce w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje programy MapReduce na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux. W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.

> [!NOTE] 
> Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu.  

## <a name="introduction"></a>Wprowadzenie
Potok w fabryce danych Azure przetwarza dane w usługach magazynu połączone, przy użyciu obliczeniowego połączonej usługi. Zawiera sekwencję działań, gdzie każde działanie wykonuje operację przetwarzania specyficznego dla. W tym artykule opisano przy użyciu hello HDInsight działania MapReduce.

Zobacz [Pig](data-factory-pig-activity.md) i [Hive](data-factory-hive-activity.md) szczegółowe informacje o uruchamianiu Pig/Hive skryptów w usłudze HDInsight opartych na systemie Windows/Linux klastra z potokiem przy użyciu działań HDInsight Pig i Hive. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON dla działania HDInsight MapReduce
W hello definicji JSON hello działanie usługi HDInsight: 

1. Zestaw hello **typu** z hello **działania** za**HDInsight**.
2. Określ nazwę hello klasa hello **className** właściwości.
3. Określ hello ścieżki toohello plik JAR w tym nazwę pliku hello **jarFilePath** właściwości.
4. Określ hello połączone usługi, która odwołuje się toohello magazynu obiektów Blob Azure, który zawiera plik JAR hello dla **jarLinkedService** właściwości.   
5. Określ wszelkie argumenty programu MapReduce hello w hello **argumenty** sekcji. W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce hello. toodifferentiate argumentów z argumentami MapReduce hello, rozważ użycie zarówno opcji i wartości jako argumenty, jak pokazano w hello poniższy przykład (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
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
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
Hello toorun działania MapReduce HDInsight można użyć dowolnego pliku jar MapReduce w klastrze usługi HDInsight. W przypadku hello poniższe definicji JSON próbki potoku, powitalne działanie HDInsight jest skonfigurowany toorun plik Mahout JAR.

## <a name="sample-on-github"></a>Przykładem w witrynie GitHub
Możesz pobrać przykład dotyczące używania hello działania MapReduce HDInsight z: [próbek fabryki danych w serwisie GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Uruchomienie programu wyrazów hello
potok Hello w tym przykładzie jest uruchamiane hello program wyrazów mapy/Zmniejsz w klastrze usługi Azure HDInsight.   

### <a name="linked-services"></a>Połączone usługi
Najpierw należy utworzyć hello toolink połączonej usługi magazynu Azure, który jest używany przez fabryki danych Azure toohello hello Azure HDInsight klastra. Jeśli użytkownik kopiowania/wklejania hello następującego kodu, nie zapomnij tooreplace **nazwa konta** i **klucz konta** o nazwie hello i klucza magazynu Azure. 

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Usługa Azure HDInsight połączone
Następnie utworzysz toolink połączonej usługi fabryki danych Azure toohello Twojego Azure HDInsight klastra. Jeśli użytkownik kopiowania/wklejania hello następującego kodu, Zastąp **nazwy klastra usługi HDInsight** o nazwie hello klastra usługi HDInsight i zmień wartości nazwy i hasła użytkownika.   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>Zestawy danych
#### <a name="output-dataset"></a>Wyjściowy zestaw danych
Witaj potoku, w tym przykładzie nie przyjmuje żadnych danych wejściowych. Należy określić dla działania MapReduce HDInsight hello wyjściowy zestaw danych. Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogramu.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Potok
potok Hello w tym przykładzie ma tylko jedno działanie, które jest typu: HDInsightMapReduce. Ważne właściwości hello w hello JSON, należą: 

| Właściwość | Uwagi |
|:--- |:--- |
| type |należy ustawić typ Hello zbyt**HDInsightMapReduce**. |
| className |Nazwa klasy hello jest: **wordcount** |
| jarFilePath |Ścieżki pliku jar toohello hello klasą. Jeśli użytkownik kopiowania/wklejania hello następującego kodu, nie zapomnij toochange nazwę hello hello klastra. |
| jarLinkedService |Usługa Azure Storage połączone usługi, który zawiera plik jar hello. Tej połączonej usługi odwołuje się toohello magazynu, który jest skojarzony z klastrem usługi HDInsight hello. |
| Argumenty |Hello wordcount program przyjmuje dwa argumenty wejściowe i wyjściowe. Plik wejściowy Hello jest hello davinci.txt pliku. |
| frequency/interval |wartości tych właściwości Hello odpowiada hello wyjściowego zestawu danych. |
| linkedServiceName |odwołuje się toohello HDInsight połączone usługi, którą ma zostać utworzony wcześniej. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Uruchamianie programów Spark
Można skorzystać z MapReduce działania toorun Spark programów w klastrze Spark w usłudze HDInsight. Zobacz [Wywoływanie programów platformy Spark z usługi Azure Data Factory](data-factory-spark.md).  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Zobacz też
* [Działanie gałęzi](data-factory-hive-activity.md)
* [Działanie pig](data-factory-pig-activity.md)
* [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
* [Wywoływanie programów platformy Spark](data-factory-spark.md)
* [Wywoływanie skryptów języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

