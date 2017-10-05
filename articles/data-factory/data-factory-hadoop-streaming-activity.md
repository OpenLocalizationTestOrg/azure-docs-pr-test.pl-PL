---
title: "Przekształcanie danych za pomocą działaniu przesyłania strumieniowego usługi Hadoop - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używasz działaniu przesyłania strumieniowego usługi Hadoop w fabryce danych Azure do przekształcania danych, uruchamiając programy przesyłania strumieniowego usługi Hadoop w klastrze usługi HDInsight na — żądanie/swój własny."
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
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="32c97-103">Przekształcanie danych za pomocą działaniu przesyłania strumieniowego usługi Hadoop w usłudze fabryka danych Azure</span><span class="sxs-lookup"><span data-stu-id="32c97-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="32c97-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="32c97-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="32c97-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="32c97-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="32c97-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="32c97-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="32c97-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="32c97-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="32c97-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="32c97-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="32c97-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32c97-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="32c97-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32c97-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="32c97-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="32c97-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="32c97-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="32c97-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="32c97-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="32c97-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="32c97-114">Można użyć działania HDInsightStreamingActivity wywołania zadania przesyłania strumieniowego usługi Hadoop z potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="32c97-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="32c97-115">Poniższy fragment kodu JSON przedstawiono składnię przy użyciu HDInsightStreamingActivity w pliku JSON potoku.</span><span class="sxs-lookup"><span data-stu-id="32c97-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="32c97-116">HDInsight działaniu przesyłania strumieniowego w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje programy przesyłania strumieniowego usługi Hadoop na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="32c97-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="32c97-117">W tym artykule opiera się na [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań obsługiwanych transformacji.</span><span class="sxs-lookup"><span data-stu-id="32c97-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="32c97-118">Jeśli jesteś nowym użytkownikiem usługi fabryka danych Azure, zapoznaj się z artykułem [wprowadzenie do fabryki danych Azure](data-factory-introduction.md) i wykonaj samouczka: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="32c97-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="32c97-119">Przykładowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="32c97-119">JSON sample</span></span>
<span data-ttu-id="32c97-120">Klaster usługi HDInsight jest wypełniane automatycznie przy użyciu programów przykład (wc.exe i cat.exe) i data (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="32c97-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="32c97-121">Domyślnie nazwa kontenera, w którym jest używane przez klaster usługi HDInsight jest nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="32c97-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="32c97-122">Na przykład jeśli nazwa klastra jest myhdicluster, nazwa kontenera obiektów blob skojarzony byłoby myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="32c97-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="32c97-123">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="32c97-123">Note the following points:</span></span>

1. <span data-ttu-id="32c97-124">Ustaw **linkedServiceName** do nazwy połączonej usługi, która wskazuje z HDInsight klastra uruchamiania przesyłania strumieniowego zadania mapreduce.</span><span class="sxs-lookup"><span data-stu-id="32c97-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="32c97-125">Ustaw typ działanie, aby **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="32c97-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="32c97-126">Aby uzyskać **mapowania** właściwości, określ nazwę pliku wykonywalnego mapowania.</span><span class="sxs-lookup"><span data-stu-id="32c97-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="32c97-127">W tym przykładzie cat.exe jest mapowania pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="32c97-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="32c97-128">Aby uzyskać **reduktor** właściwości, określ nazwę pliku wykonywalnego reduktor.</span><span class="sxs-lookup"><span data-stu-id="32c97-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="32c97-129">W tym przykładzie wc.exe jest reduktor pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="32c97-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="32c97-130">Aby uzyskać **wejściowych** typu właściwości, określ plik wejściowy (w tym o lokalizacji) dla mapowania.</span><span class="sxs-lookup"><span data-stu-id="32c97-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="32c97-131">W tym przykładzie: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample jest kontenera obiektów blob, przykład/data/Gutenberg jest folder i davinci.txt jest obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="32c97-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="32c97-132">Aby uzyskać **dane wyjściowe** typu właściwości, określ plik wyjściowy (w tym o lokalizacji) dla reduktor.</span><span class="sxs-lookup"><span data-stu-id="32c97-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="32c97-133">Dane wyjściowe zadania przesyłania strumieniowego usługi Hadoop jest zapisany w lokalizacji określonej dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="32c97-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="32c97-134">W **filePaths** sekcji, określ ścieżki dla plików wykonywalnych mapowania i reduktor.</span><span class="sxs-lookup"><span data-stu-id="32c97-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="32c97-135">W tym przykładzie: "adfsample/example/apps/wc.exe" adfsample jest kontenera obiektów blob, przykład/aplikacji jest folder i wc.exe jest plikiem wykonywalnym.</span><span class="sxs-lookup"><span data-stu-id="32c97-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="32c97-136">Aby uzyskać **fileLinkedService** właściwości, określ połączoną usługą magazynu Azure reprezentujący magazynu Azure, który zawiera pliki określone w sekcji filePaths.</span><span class="sxs-lookup"><span data-stu-id="32c97-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="32c97-137">Dla **argumenty** właściwości, określ argumenty dla zadania przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="32c97-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="32c97-138">**GetDebugInfo** właściwości to opcjonalny element.</span><span class="sxs-lookup"><span data-stu-id="32c97-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="32c97-139">Jeśli ustawiono awarii, dzienniki są pobierane tylko w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="32c97-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="32c97-140">Gdy ma wartość Always, dzienniki są zawsze pobierane niezależnie od stanu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="32c97-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="32c97-141">Jak pokazano w przykładzie, podajesz wyjściowy zestaw danych w działaniu przesyłania strumieniowego usługi Hadoop dla **generuje** właściwości.</span><span class="sxs-lookup"><span data-stu-id="32c97-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="32c97-142">Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany do kierowania harmonogram potoku.</span><span class="sxs-lookup"><span data-stu-id="32c97-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="32c97-143">Nie należy określić wszystkie wejściowy zestaw danych działania dla **dane wejściowe** właściwości.</span><span class="sxs-lookup"><span data-stu-id="32c97-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="32c97-144">Przykład</span><span class="sxs-lookup"><span data-stu-id="32c97-144">Example</span></span>
<span data-ttu-id="32c97-145">Potoku, w tym przewodniku uruchamia program mapy/Zmniejsz przesyłania strumieniowego wyrazów w klastrze usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="32c97-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="32c97-146">Połączone usługi</span><span class="sxs-lookup"><span data-stu-id="32c97-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="32c97-147">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="32c97-147">Azure Storage linked service</span></span>
<span data-ttu-id="32c97-148">Najpierw należy utworzyć połączonej usługi, aby połączyć magazyn Azure, który jest używany przez klaster Azure HDInsight z fabryką danych Azure.</span><span class="sxs-lookup"><span data-stu-id="32c97-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="32c97-149">Jeśli użytkownik skopiuj/Wklej następujący kod, pamiętaj zastąpić nazwę konta i klucz konta o nazwie i klucza magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="32c97-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="32c97-150">Usługa Azure HDInsight połączone</span><span class="sxs-lookup"><span data-stu-id="32c97-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="32c97-151">Następnie można utworzyć połączonej usługi do połączenia z klastrem usługi HDInsight Azure z fabryką danych Azure.</span><span class="sxs-lookup"><span data-stu-id="32c97-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="32c97-152">Jeśli użytkownik skopiuj/Wklej następujący kod, zastąp nazwą klastra usługi HDInsight nazwą klastra usługi HDInsight i zmień wartości nazwy i hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32c97-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="32c97-153">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="32c97-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="32c97-154">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="32c97-154">Output dataset</span></span>
<span data-ttu-id="32c97-155">Potok, w tym przykładzie nie przyjmuje żadnych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="32c97-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="32c97-156">Podajesz wyjściowy zestaw danych w działaniu przesyłania strumieniowego usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="32c97-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="32c97-157">Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany do kierowania harmonogram potoku.</span><span class="sxs-lookup"><span data-stu-id="32c97-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="32c97-158">Potok</span><span class="sxs-lookup"><span data-stu-id="32c97-158">Pipeline</span></span>
<span data-ttu-id="32c97-159">Potok, w tym przykładzie jest tylko jedno działanie, które jest typu: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="32c97-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="32c97-160">Klaster usługi HDInsight jest wypełniane automatycznie przy użyciu programów przykład (wc.exe i cat.exe) i data (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="32c97-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="32c97-161">Domyślnie nazwa kontenera, w którym jest używane przez klaster usługi HDInsight jest nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="32c97-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="32c97-162">Na przykład jeśli nazwa klastra jest myhdicluster, nazwa kontenera obiektów blob skojarzony byłoby myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="32c97-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="32c97-163">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="32c97-163">See Also</span></span>
* [<span data-ttu-id="32c97-164">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="32c97-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="32c97-165">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="32c97-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="32c97-166">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="32c97-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="32c97-167">Wywoływanie programów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="32c97-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="32c97-168">Wywoływanie skryptów języka R</span><span class="sxs-lookup"><span data-stu-id="32c97-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

