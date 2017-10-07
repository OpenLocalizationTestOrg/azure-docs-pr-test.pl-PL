---
title: "aaaTransform danych przy użyciu działaniu przesyłania strumieniowego usługi Hadoop - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można użyć hello działaniu przesyłania strumieniowego usługi Hadoop w danych tootransform fabryki danych Azure, uruchamiając programy przesyłania strumieniowego usługi Hadoop w klastrze usługi HDInsight na — żądanie/swój własny."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Przekształcanie danych za pomocą działaniu przesyłania strumieniowego usługi Hadoop w usłudze fabryka danych Azure
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

Można użyć hello HDInsightStreamingActivity działania Wywołaj zadania przesyłania strumieniowego usługi Hadoop z potoku fabryki danych Azure. Witaj następujący fragment kodu JSON przedstawiono hello składnię przy użyciu hello HDInsightStreamingActivity w pliku JSON potoku. 

Witaj HDInsight działaniu przesyłania strumieniowego w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje programy przesyłania strumieniowego usługi Hadoop na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight opartych na systemie Windows/Linux klaster. W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.

> [!NOTE] 
> Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu. 

## <a name="json-sample"></a>Przykładowy kod JSON
klaster usługi HDInsight Hello jest wypełniane automatycznie przy użyciu programów przykład (wc.exe i cat.exe) i data (davinci.txt). Domyślnie nazwa kontenera hello, który jest używany przez klaster usługi HDInsight hello jest nazwa hello hello samego klastra. Na przykład jeśli nazwa klastra jest myhdicluster, nazwa kontenera obiektów blob hello skojarzone byłoby myhdicluster. 

```JSON
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
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
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
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

Należy zwrócić uwagę hello następujące punkty:

1. Zestaw hello **linkedServiceName** toohello nazwę hello połączonej usługi, wskazujące tooyour klastra usługi HDInsight, na które hello przesyłania strumieniowego mapreduce uruchomieniu zadania.
2. Ustaw typ hello działania hello zbyt**HDInsightStreaming**.
3. Dla hello **mapowania** właściwość, należy określić nazwę hello mapowania pliku wykonywalnego. Przykład Witaj cat.exe to hello mapowania pliku wykonywalnego.
4. Dla hello **reduktor** właściwość, należy określić nazwę hello reduktor pliku wykonywalnego. Przykład Witaj wc.exe to reduktor hello pliku wykonywalnego.
5. Dla hello **wejściowych** type — właściwość, należy określić hello plik wejściowy (w tym miejscu hello) hello mapowania. W przykładzie hello: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample jest hello kontenera obiektów blob, przykład/data/Gutenberg jest hello folder i davinci.txt jest hello obiektu blob.
6. Dla hello **dane wyjściowe** typu właściwości, określ plik wyjściowy hello (w tym miejscu hello) reduktor hello. dane wyjściowe zadania przesyłania strumieniowego usługi Hadoop hello Hello są zapisywane toohello lokalizacji określonej dla tej właściwości.
7. W hello **filePaths** Określ hello ścieżki do plików wykonywalnych mapowania i reduktor hello. W przykładzie hello: "adfsample/example/apps/wc.exe" adfsample jest hello kontenera obiektów blob, przykład/aplikacji hello folderu, i wc.exe jest hello pliku wykonywalnego.
8. Dla hello **fileLinkedService** właściwości, określ hello połączonej usługi, która reprezentuje hello Azure magazynu, który zawiera pliki hello określone w sekcji filePaths hello usługi Magazyn Azure.
9. Dla hello **argumenty** właściwość argumentami hello hello strumienia zadania.
10. Witaj **getDebugInfo** właściwości to opcjonalny element. Jeśli je skonfigurowano tooFailure, dzienniki hello są pobierane tylko w przypadku awarii. Jeśli je skonfigurowano tooAlways, dzienniki są zawsze pobierane niezależnie od hello stanu wykonywania.

> [!NOTE]
> Jak pokazano w przykładzie hello, określ wyjściowy zestaw danych hello działaniu przesyłania strumieniowego usługi Hadoop dla hello **generuje** właściwości. Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogramu. Nie trzeba toospecify żadnych wejściowy zestaw danych dla działania hello na powitania **dane wejściowe** właściwości.  
> 
> 

## <a name="example"></a>Przykład
potok Hello w tym przewodniku jest uruchamiane przesyłania strumieniowego programu mapy/Zmniejsz hello wyrazów w klastrze usługi Azure HDInsight. 

### <a name="linked-services"></a>Połączone usługi
#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
Najpierw należy utworzyć hello toolink połączonej usługi magazynu Azure, który jest używany przez fabryki danych Azure toohello hello Azure HDInsight klastra. Jeśli użytkownik kopiowania/wklejania hello następującego kodu, nie zapomnij tooreplace konta nazwy i klucza konta o nazwie hello i klucza magazynu Azure. 

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
Następnie utworzysz toolink połączonej usługi fabryki danych Azure toohello Twojego Azure HDInsight klastra. Jeśli użytkownik kopiowania/wklejania hello następującego kodu, zastąp nazwę klastra usługi HDInsight hello nazwą klastra usługi HDInsight i zmień wartości nazwy i hasła użytkownika. 

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
Witaj potoku, w tym przykładzie nie przyjmuje żadnych danych wejściowych. Należy określić wyjściowy zestaw danych hello działaniu przesyłania strumieniowego usługi HDInsight. Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogramu. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Potok
potok Hello w tym przykładzie ma tylko jedno działanie, które jest typu: **HDInsightStreaming**. 

klaster usługi HDInsight Hello jest wypełniane automatycznie przy użyciu programów przykład (wc.exe i cat.exe) i data (davinci.txt). Domyślnie nazwa kontenera hello, który jest używany przez klaster usługi HDInsight hello jest nazwa hello hello samego klastra. Na przykład jeśli nazwa klastra jest myhdicluster, nazwa kontenera obiektów blob hello skojarzone byłoby myhdicluster.  

```JSON
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
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
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
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>Zobacz też
* [Działanie gałęzi](data-factory-hive-activity.md)
* [Działanie pig](data-factory-pig-activity.md)
* [Działania MapReduce](data-factory-map-reduce.md)
* [Wywoływanie programów platformy Spark](data-factory-spark.md)
* [Wywoływanie skryptów języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

