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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="5b0da-103">Przekształcanie danych za pomocą działaniu przesyłania strumieniowego usługi Hadoop w usłudze fabryka danych Azure</span><span class="sxs-lookup"><span data-stu-id="5b0da-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5b0da-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="5b0da-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5b0da-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="5b0da-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5b0da-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="5b0da-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5b0da-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="5b0da-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5b0da-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="5b0da-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5b0da-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b0da-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5b0da-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b0da-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5b0da-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="5b0da-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5b0da-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5b0da-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5b0da-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="5b0da-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5b0da-114">Można użyć hello HDInsightStreamingActivity działania Wywołaj zadania przesyłania strumieniowego usługi Hadoop z potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0da-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="5b0da-115">Witaj następujący fragment kodu JSON przedstawiono hello składnię przy użyciu hello HDInsightStreamingActivity w pliku JSON potoku.</span><span class="sxs-lookup"><span data-stu-id="5b0da-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="5b0da-116">Witaj HDInsight działaniu przesyłania strumieniowego w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje programy przesyłania strumieniowego usługi Hadoop na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight opartych na systemie Windows/Linux klaster.</span><span class="sxs-lookup"><span data-stu-id="5b0da-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5b0da-117">W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5b0da-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="5b0da-118">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="5b0da-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="5b0da-119">Przykładowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="5b0da-119">JSON sample</span></span>
<span data-ttu-id="5b0da-120">klaster usługi HDInsight Hello jest wypełniane automatycznie przy użyciu programów przykład (wc.exe i cat.exe) i data (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="5b0da-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="5b0da-121">Domyślnie nazwa kontenera hello, który jest używany przez klaster usługi HDInsight hello jest nazwa hello hello samego klastra.</span><span class="sxs-lookup"><span data-stu-id="5b0da-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="5b0da-122">Na przykład jeśli nazwa klastra jest myhdicluster, nazwa kontenera obiektów blob hello skojarzone byłoby myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="5b0da-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="5b0da-123">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="5b0da-123">Note hello following points:</span></span>

1. <span data-ttu-id="5b0da-124">Zestaw hello **linkedServiceName** toohello nazwę hello połączonej usługi, wskazujące tooyour klastra usługi HDInsight, na które hello przesyłania strumieniowego mapreduce uruchomieniu zadania.</span><span class="sxs-lookup"><span data-stu-id="5b0da-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="5b0da-125">Ustaw typ hello działania hello zbyt**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="5b0da-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="5b0da-126">Dla hello **mapowania** właściwość, należy określić nazwę hello mapowania pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="5b0da-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="5b0da-127">Przykład Witaj cat.exe to hello mapowania pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="5b0da-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="5b0da-128">Dla hello **reduktor** właściwość, należy określić nazwę hello reduktor pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="5b0da-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="5b0da-129">Przykład Witaj wc.exe to reduktor hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="5b0da-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="5b0da-130">Dla hello **wejściowych** type — właściwość, należy określić hello plik wejściowy (w tym miejscu hello) hello mapowania.</span><span class="sxs-lookup"><span data-stu-id="5b0da-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="5b0da-131">W przykładzie hello: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample jest hello kontenera obiektów blob, przykład/data/Gutenberg jest hello folder i davinci.txt jest hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="5b0da-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="5b0da-132">Dla hello **dane wyjściowe** typu właściwości, określ plik wyjściowy hello (w tym miejscu hello) reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="5b0da-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="5b0da-133">dane wyjściowe zadania przesyłania strumieniowego usługi Hadoop hello Hello są zapisywane toohello lokalizacji określonej dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="5b0da-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="5b0da-134">W hello **filePaths** Określ hello ścieżki do plików wykonywalnych mapowania i reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="5b0da-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="5b0da-135">W przykładzie hello: "adfsample/example/apps/wc.exe" adfsample jest hello kontenera obiektów blob, przykład/aplikacji hello folderu, i wc.exe jest hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="5b0da-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="5b0da-136">Dla hello **fileLinkedService** właściwości, określ hello połączonej usługi, która reprezentuje hello Azure magazynu, który zawiera pliki hello określone w sekcji filePaths hello usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0da-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="5b0da-137">Dla hello **argumenty** właściwość argumentami hello hello strumienia zadania.</span><span class="sxs-lookup"><span data-stu-id="5b0da-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="5b0da-138">Witaj **getDebugInfo** właściwości to opcjonalny element.</span><span class="sxs-lookup"><span data-stu-id="5b0da-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="5b0da-139">Jeśli je skonfigurowano tooFailure, dzienniki hello są pobierane tylko w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="5b0da-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="5b0da-140">Jeśli je skonfigurowano tooAlways, dzienniki są zawsze pobierane niezależnie od hello stanu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5b0da-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="5b0da-141">Jak pokazano w przykładzie hello, określ wyjściowy zestaw danych hello działaniu przesyłania strumieniowego usługi Hadoop dla hello **generuje** właściwości.</span><span class="sxs-lookup"><span data-stu-id="5b0da-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="5b0da-142">Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="5b0da-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="5b0da-143">Nie trzeba toospecify żadnych wejściowy zestaw danych dla działania hello na powitania **dane wejściowe** właściwości.</span><span class="sxs-lookup"><span data-stu-id="5b0da-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="5b0da-144">Przykład</span><span class="sxs-lookup"><span data-stu-id="5b0da-144">Example</span></span>
<span data-ttu-id="5b0da-145">potok Hello w tym przewodniku jest uruchamiane przesyłania strumieniowego programu mapy/Zmniejsz hello wyrazów w klastrze usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b0da-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="5b0da-146">Połączone usługi</span><span class="sxs-lookup"><span data-stu-id="5b0da-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="5b0da-147">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5b0da-147">Azure Storage linked service</span></span>
<span data-ttu-id="5b0da-148">Najpierw należy utworzyć hello toolink połączonej usługi magazynu Azure, który jest używany przez fabryki danych Azure toohello hello Azure HDInsight klastra.</span><span class="sxs-lookup"><span data-stu-id="5b0da-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="5b0da-149">Jeśli użytkownik kopiowania/wklejania hello następującego kodu, nie zapomnij tooreplace konta nazwy i klucza konta o nazwie hello i klucza magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0da-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="5b0da-150">Usługa Azure HDInsight połączone</span><span class="sxs-lookup"><span data-stu-id="5b0da-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="5b0da-151">Następnie utworzysz toolink połączonej usługi fabryki danych Azure toohello Twojego Azure HDInsight klastra.</span><span class="sxs-lookup"><span data-stu-id="5b0da-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="5b0da-152">Jeśli użytkownik kopiowania/wklejania hello następującego kodu, zastąp nazwę klastra usługi HDInsight hello nazwą klastra usługi HDInsight i zmień wartości nazwy i hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b0da-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="5b0da-153">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="5b0da-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="5b0da-154">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="5b0da-154">Output dataset</span></span>
<span data-ttu-id="5b0da-155">Witaj potoku, w tym przykładzie nie przyjmuje żadnych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5b0da-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="5b0da-156">Należy określić wyjściowy zestaw danych hello działaniu przesyłania strumieniowego usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b0da-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="5b0da-157">Ten zestaw danych jest tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="5b0da-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="5b0da-158">Potok</span><span class="sxs-lookup"><span data-stu-id="5b0da-158">Pipeline</span></span>
<span data-ttu-id="5b0da-159">potok Hello w tym przykładzie ma tylko jedno działanie, które jest typu: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="5b0da-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="5b0da-160">klaster usługi HDInsight Hello jest wypełniane automatycznie przy użyciu programów przykład (wc.exe i cat.exe) i data (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="5b0da-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="5b0da-161">Domyślnie nazwa kontenera hello, który jest używany przez klaster usługi HDInsight hello jest nazwa hello hello samego klastra.</span><span class="sxs-lookup"><span data-stu-id="5b0da-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="5b0da-162">Na przykład jeśli nazwa klastra jest myhdicluster, nazwa kontenera obiektów blob hello skojarzone byłoby myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="5b0da-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="5b0da-163">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5b0da-163">See Also</span></span>
* [<span data-ttu-id="5b0da-164">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="5b0da-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="5b0da-165">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="5b0da-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="5b0da-166">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="5b0da-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="5b0da-167">Wywoływanie programów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="5b0da-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="5b0da-168">Wywoływanie skryptów języka R</span><span class="sxs-lookup"><span data-stu-id="5b0da-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

