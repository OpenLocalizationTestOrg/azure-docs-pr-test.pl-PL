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
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="4da6e-103">Wywoływanie programów MapReduce z fabryki danych</span><span class="sxs-lookup"><span data-stu-id="4da6e-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4da6e-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="4da6e-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4da6e-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="4da6e-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4da6e-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="4da6e-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4da6e-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="4da6e-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4da6e-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="4da6e-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4da6e-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4da6e-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4da6e-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4da6e-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4da6e-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="4da6e-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4da6e-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4da6e-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4da6e-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="4da6e-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="4da6e-114">Witaj działania HDInsight MapReduce w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje programy MapReduce na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="4da6e-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4da6e-115">W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4da6e-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="4da6e-116">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4da6e-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="4da6e-117">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="4da6e-117">Introduction</span></span>
<span data-ttu-id="4da6e-118">Potok w fabryce danych Azure przetwarza dane w usługach magazynu połączone, przy użyciu obliczeniowego połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4da6e-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="4da6e-119">Zawiera sekwencję działań, gdzie każde działanie wykonuje operację przetwarzania specyficznego dla.</span><span class="sxs-lookup"><span data-stu-id="4da6e-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="4da6e-120">W tym artykule opisano przy użyciu hello HDInsight działania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4da6e-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="4da6e-121">Zobacz [Pig](data-factory-pig-activity.md) i [Hive](data-factory-hive-activity.md) szczegółowe informacje o uruchamianiu Pig/Hive skryptów w usłudze HDInsight opartych na systemie Windows/Linux klastra z potokiem przy użyciu działań HDInsight Pig i Hive.</span><span class="sxs-lookup"><span data-stu-id="4da6e-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="4da6e-122">JSON dla działania HDInsight MapReduce</span><span class="sxs-lookup"><span data-stu-id="4da6e-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="4da6e-123">W hello definicji JSON hello działanie usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4da6e-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="4da6e-124">Zestaw hello **typu** z hello **działania** za**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4da6e-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="4da6e-125">Określ nazwę hello klasa hello **className** właściwości.</span><span class="sxs-lookup"><span data-stu-id="4da6e-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="4da6e-126">Określ hello ścieżki toohello plik JAR w tym nazwę pliku hello **jarFilePath** właściwości.</span><span class="sxs-lookup"><span data-stu-id="4da6e-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="4da6e-127">Określ hello połączone usługi, która odwołuje się toohello magazynu obiektów Blob Azure, który zawiera plik JAR hello dla **jarLinkedService** właściwości.</span><span class="sxs-lookup"><span data-stu-id="4da6e-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="4da6e-128">Określ wszelkie argumenty programu MapReduce hello w hello **argumenty** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4da6e-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="4da6e-129">W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="4da6e-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="4da6e-130">toodifferentiate argumentów z argumentami MapReduce hello, rozważ użycie zarówno opcji i wartości jako argumenty, jak pokazano w hello poniższy przykład (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości).</span><span class="sxs-lookup"><span data-stu-id="4da6e-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

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
<span data-ttu-id="4da6e-131">Hello toorun działania MapReduce HDInsight można użyć dowolnego pliku jar MapReduce w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4da6e-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="4da6e-132">W przypadku hello poniższe definicji JSON próbki potoku, powitalne działanie HDInsight jest skonfigurowany toorun plik Mahout JAR.</span><span class="sxs-lookup"><span data-stu-id="4da6e-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="4da6e-133">Przykładem w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="4da6e-133">Sample on GitHub</span></span>
<span data-ttu-id="4da6e-134">Możesz pobrać przykład dotyczące używania hello działania MapReduce HDInsight z: [próbek fabryki danych w serwisie GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="4da6e-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="4da6e-135">Uruchomienie programu wyrazów hello</span><span class="sxs-lookup"><span data-stu-id="4da6e-135">Running hello Word Count program</span></span>
<span data-ttu-id="4da6e-136">potok Hello w tym przykładzie jest uruchamiane hello program wyrazów mapy/Zmniejsz w klastrze usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4da6e-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="4da6e-137">Połączone usługi</span><span class="sxs-lookup"><span data-stu-id="4da6e-137">Linked Services</span></span>
<span data-ttu-id="4da6e-138">Najpierw należy utworzyć hello toolink połączonej usługi magazynu Azure, który jest używany przez fabryki danych Azure toohello hello Azure HDInsight klastra.</span><span class="sxs-lookup"><span data-stu-id="4da6e-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="4da6e-139">Jeśli użytkownik kopiowania/wklejania hello następującego kodu, nie zapomnij tooreplace **nazwa konta** i **klucz konta** o nazwie hello i klucza magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="4da6e-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="4da6e-140">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4da6e-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="4da6e-141">Usługa Azure HDInsight połączone</span><span class="sxs-lookup"><span data-stu-id="4da6e-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="4da6e-142">Następnie utworzysz toolink połączonej usługi fabryki danych Azure toohello Twojego Azure HDInsight klastra.</span><span class="sxs-lookup"><span data-stu-id="4da6e-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="4da6e-143">Jeśli użytkownik kopiowania/wklejania hello następującego kodu, Zastąp **nazwy klastra usługi HDInsight** o nazwie hello klastra usługi HDInsight i zmień wartości nazwy i hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4da6e-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="4da6e-144">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="4da6e-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="4da6e-145">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="4da6e-145">Output dataset</span></span>
<span data-ttu-id="4da6e-146">Witaj potoku, w tym przykładzie nie przyjmuje żadnych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4da6e-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="4da6e-147">Należy określić dla działania MapReduce HDInsight hello wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="4da6e-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="4da6e-148">Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="4da6e-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="4da6e-149">Potok</span><span class="sxs-lookup"><span data-stu-id="4da6e-149">Pipeline</span></span>
<span data-ttu-id="4da6e-150">potok Hello w tym przykładzie ma tylko jedno działanie, które jest typu: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="4da6e-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="4da6e-151">Ważne właściwości hello w hello JSON, należą:</span><span class="sxs-lookup"><span data-stu-id="4da6e-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="4da6e-152">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4da6e-152">Property</span></span> | <span data-ttu-id="4da6e-153">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4da6e-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="4da6e-154">type</span><span class="sxs-lookup"><span data-stu-id="4da6e-154">type</span></span> |<span data-ttu-id="4da6e-155">należy ustawić typ Hello zbyt**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="4da6e-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="4da6e-156">className</span><span class="sxs-lookup"><span data-stu-id="4da6e-156">className</span></span> |<span data-ttu-id="4da6e-157">Nazwa klasy hello jest: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="4da6e-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="4da6e-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="4da6e-158">jarFilePath</span></span> |<span data-ttu-id="4da6e-159">Ścieżki pliku jar toohello hello klasą.</span><span class="sxs-lookup"><span data-stu-id="4da6e-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="4da6e-160">Jeśli użytkownik kopiowania/wklejania hello następującego kodu, nie zapomnij toochange nazwę hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4da6e-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="4da6e-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="4da6e-161">jarLinkedService</span></span> |<span data-ttu-id="4da6e-162">Usługa Azure Storage połączone usługi, który zawiera plik jar hello.</span><span class="sxs-lookup"><span data-stu-id="4da6e-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="4da6e-163">Tej połączonej usługi odwołuje się toohello magazynu, który jest skojarzony z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4da6e-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="4da6e-164">Argumenty</span><span class="sxs-lookup"><span data-stu-id="4da6e-164">arguments</span></span> |<span data-ttu-id="4da6e-165">Hello wordcount program przyjmuje dwa argumenty wejściowe i wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4da6e-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="4da6e-166">Plik wejściowy Hello jest hello davinci.txt pliku.</span><span class="sxs-lookup"><span data-stu-id="4da6e-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="4da6e-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4da6e-167">frequency/interval</span></span> |<span data-ttu-id="4da6e-168">wartości tych właściwości Hello odpowiada hello wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4da6e-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="4da6e-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4da6e-169">linkedServiceName</span></span> |<span data-ttu-id="4da6e-170">odwołuje się toohello HDInsight połączone usługi, którą ma zostać utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4da6e-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

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

## <a name="run-spark-programs"></a><span data-ttu-id="4da6e-171">Uruchamianie programów Spark</span><span class="sxs-lookup"><span data-stu-id="4da6e-171">Run Spark programs</span></span>
<span data-ttu-id="4da6e-172">Można skorzystać z MapReduce działania toorun Spark programów w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4da6e-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="4da6e-173">Zobacz [Wywoływanie programów platformy Spark z usługi Azure Data Factory](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="4da6e-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="4da6e-174">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4da6e-174">See Also</span></span>
* [<span data-ttu-id="4da6e-175">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="4da6e-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="4da6e-176">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="4da6e-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="4da6e-177">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="4da6e-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="4da6e-178">Wywoływanie programów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="4da6e-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="4da6e-179">Wywoływanie skryptów języka R</span><span class="sxs-lookup"><span data-stu-id="4da6e-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

