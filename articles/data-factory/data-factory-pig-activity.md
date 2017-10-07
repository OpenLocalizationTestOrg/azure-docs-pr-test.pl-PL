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
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="c1691-103">Przekształcanie danych za pomocą działania Pig w fabryce danych Azure</span><span class="sxs-lookup"><span data-stu-id="c1691-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="c1691-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="c1691-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="c1691-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="c1691-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="c1691-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="c1691-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="c1691-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="c1691-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="c1691-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="c1691-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="c1691-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c1691-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="c1691-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c1691-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="c1691-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="c1691-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="c1691-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c1691-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="c1691-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="c1691-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="c1691-114">Witaj HDInsight Pig działania w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje zapytania Pig na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="c1691-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c1691-115">W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c1691-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="c1691-116">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c1691-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="c1691-117">Składnia</span><span class="sxs-lookup"><span data-stu-id="c1691-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="c1691-118">Szczegóły składni</span><span class="sxs-lookup"><span data-stu-id="c1691-118">Syntax details</span></span>
| <span data-ttu-id="c1691-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c1691-119">Property</span></span> | <span data-ttu-id="c1691-120">Opis</span><span class="sxs-lookup"><span data-stu-id="c1691-120">Description</span></span> | <span data-ttu-id="c1691-121">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c1691-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1691-122">name</span><span class="sxs-lookup"><span data-stu-id="c1691-122">name</span></span> |<span data-ttu-id="c1691-123">Nazwa działania hello</span><span class="sxs-lookup"><span data-stu-id="c1691-123">Name of hello activity</span></span> |<span data-ttu-id="c1691-124">Tak</span><span class="sxs-lookup"><span data-stu-id="c1691-124">Yes</span></span> |
| <span data-ttu-id="c1691-125">description</span><span class="sxs-lookup"><span data-stu-id="c1691-125">description</span></span> |<span data-ttu-id="c1691-126">Tekst opisujący, jakie działanie hello jest używany dla</span><span class="sxs-lookup"><span data-stu-id="c1691-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="c1691-127">Nie</span><span class="sxs-lookup"><span data-stu-id="c1691-127">No</span></span> |
| <span data-ttu-id="c1691-128">type</span><span class="sxs-lookup"><span data-stu-id="c1691-128">type</span></span> |<span data-ttu-id="c1691-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="c1691-129">HDinsightPig</span></span> |<span data-ttu-id="c1691-130">Tak</span><span class="sxs-lookup"><span data-stu-id="c1691-130">Yes</span></span> |
| <span data-ttu-id="c1691-131">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="c1691-131">inputs</span></span> |<span data-ttu-id="c1691-132">Co najmniej jeden dane wejściowe używane przez hello działania Pig</span><span class="sxs-lookup"><span data-stu-id="c1691-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="c1691-133">Nie</span><span class="sxs-lookup"><span data-stu-id="c1691-133">No</span></span> |
| <span data-ttu-id="c1691-134">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="c1691-134">outputs</span></span> |<span data-ttu-id="c1691-135">Jeden lub więcej danych wyjściowych utworzonego przez hello działania Pig</span><span class="sxs-lookup"><span data-stu-id="c1691-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="c1691-136">Tak</span><span class="sxs-lookup"><span data-stu-id="c1691-136">Yes</span></span> |
| <span data-ttu-id="c1691-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c1691-137">linkedServiceName</span></span> |<span data-ttu-id="c1691-138">Klaster usługi HDInsight toohello odwołanie w zarejestrowany jako połączonej usługi z fabryki danych</span><span class="sxs-lookup"><span data-stu-id="c1691-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="c1691-139">Tak</span><span class="sxs-lookup"><span data-stu-id="c1691-139">Yes</span></span> |
| <span data-ttu-id="c1691-140">Skrypt</span><span class="sxs-lookup"><span data-stu-id="c1691-140">script</span></span> |<span data-ttu-id="c1691-141">Określ hello Pig skrypt wbudowany</span><span class="sxs-lookup"><span data-stu-id="c1691-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="c1691-142">Nie</span><span class="sxs-lookup"><span data-stu-id="c1691-142">No</span></span> |
| <span data-ttu-id="c1691-143">Ścieżka skryptu</span><span class="sxs-lookup"><span data-stu-id="c1691-143">script path</span></span> |<span data-ttu-id="c1691-144">Przechowywanie skrypt programu Pig hello w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku.</span><span class="sxs-lookup"><span data-stu-id="c1691-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="c1691-145">Użyj właściwości 'script' lub "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="c1691-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="c1691-146">Nie można używać razem.</span><span class="sxs-lookup"><span data-stu-id="c1691-146">Both cannot be used together.</span></span> <span data-ttu-id="c1691-147">Nazwa pliku Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="c1691-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="c1691-148">Nie</span><span class="sxs-lookup"><span data-stu-id="c1691-148">No</span></span> |
| <span data-ttu-id="c1691-149">Definiuje</span><span class="sxs-lookup"><span data-stu-id="c1691-149">defines</span></span> |<span data-ttu-id="c1691-150">Określ parametry jako pary klucz wartość dla przywołującego w hello skrypt programu Pig</span><span class="sxs-lookup"><span data-stu-id="c1691-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="c1691-151">Nie</span><span class="sxs-lookup"><span data-stu-id="c1691-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="c1691-152">Przykład</span><span class="sxs-lookup"><span data-stu-id="c1691-152">Example</span></span>
<span data-ttu-id="c1691-153">Zastanówmy się przykładem gry rejestruje analytics miejscu tooidentify hello czasu poświęcanego przez odtwarzacze granie w gry uruchomiony przez firmę.</span><span class="sxs-lookup"><span data-stu-id="c1691-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="c1691-154">następującego przykładowego dziennika gier Hello jest plików rozdzielanych przecinkami (,).</span><span class="sxs-lookup"><span data-stu-id="c1691-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="c1691-155">Zawiera ona następujące pola — ProfileID, SessionStart, czas trwania, SrcIPAddress i GameType hello.</span><span class="sxs-lookup"><span data-stu-id="c1691-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="c1691-156">Witaj **wieprzowa skryptu** tooprocess te dane:</span><span class="sxs-lookup"><span data-stu-id="c1691-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="c1691-157">tooexecute Pig tego skryptu w potoku fabryki danych hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c1691-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="c1691-158">Utwórz tooregister połączonej usługi [klaster obliczeniowy własne HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub skonfiguruj [klastra obliczeniowego HDInsight na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c1691-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="c1691-159">Umożliwia wywołanie tej połączonej usługi **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c1691-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="c1691-160">Utwórz [połączona usługa](data-factory-azure-blob-connector.md) tooconfigure hello połączenia tooAzure obiektu Blob magazynu obsługującego hello danych.</span><span class="sxs-lookup"><span data-stu-id="c1691-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="c1691-161">Umożliwia wywołanie tej połączonej usługi **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c1691-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="c1691-162">Utwórz [zestawów danych](data-factory-create-datasets.md) wskazanie toohello dane wejściowe i hello dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c1691-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="c1691-163">Teraz wywołać zestawu danych wejściowych hello **PigSampleIn** i hello wyjściowy zestaw danych **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="c1691-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="c1691-164">Skopiuj zapytanie Pig hello w pliku hello skonfigurowane w kroku #2 magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="c1691-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="c1691-165">Jeśli hello magazynu platformy Azure obsługującym hello danych różni się od hello jedną obsługującego hello pliku zapytania, Utwórz oddzielne połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c1691-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="c1691-166">Można znaleźć usługi toohello połączone w hello działania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c1691-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="c1691-167">Użyj ** scriptPath ** pliku skryptu toopig toospecify hello ścieżki i **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c1691-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c1691-168">Można też podać hello Pig skrypt wbudowany w definicji działania hello przy użyciu hello **skryptu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c1691-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="c1691-169">Jednak nie zaleca tego podejścia jako wszystkie znaki specjalne w skrypcie hello musi toobe anulowane i może spowodować problemy debugowania.</span><span class="sxs-lookup"><span data-stu-id="c1691-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="c1691-170">Witaj najlepszym rozwiązaniem jest toofollow krok #4.</span><span class="sxs-lookup"><span data-stu-id="c1691-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="c1691-171">Tworzenie potoku hello z hello HDInsightPig działania.</span><span class="sxs-lookup"><span data-stu-id="c1691-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="c1691-172">To działanie przetwarza dane wejściowe hello, uruchamiając skrypt programu Pig w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c1691-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="c1691-173">Wdróż hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c1691-173">Deploy hello pipeline.</span></span> <span data-ttu-id="c1691-174">Zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c1691-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="c1691-175">Monitorowanie za pomocą funkcji monitorowania fabryki danych hello potoku hello i widoki zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c1691-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="c1691-176">Zobacz [monitorowanie i zarządzanie nimi potoki fabryki danych](data-factory-monitor-manage-pipelines.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c1691-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="c1691-177">Określanie parametrów dla skryptu Pig</span><span class="sxs-lookup"><span data-stu-id="c1691-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="c1691-178">Należy wziąć pod uwagę hello poniższy przykład: gier dzienniki są codziennie pozyskanych w magazynie obiektów Blob Azure i przechowywane w folderze partycjonowanej na podstawie daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="c1691-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="c1691-179">Mają skrypt programu Pig hello tooparameterize i przekazać lokalizacji folderu wejściowych hello dynamicznie w czasie wykonywania, a także wygenerować hello dane wyjściowe z Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="c1691-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="c1691-180">toouse sparametryzowana skrypt programu Pig, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c1691-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="c1691-181">Zdefiniuj parametry hello w **definiuje**.</span><span class="sxs-lookup"><span data-stu-id="c1691-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="c1691-182">W hello skrypt programu Pig, można znaleźć przy użyciu parametrów toohello "**$parameterName**" jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c1691-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="c1691-183">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c1691-183">See Also</span></span>
* [<span data-ttu-id="c1691-184">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="c1691-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="c1691-185">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="c1691-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="c1691-186">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="c1691-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="c1691-187">Wywoływanie programów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="c1691-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="c1691-188">Wywoływanie skryptów języka R</span><span class="sxs-lookup"><span data-stu-id="c1691-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

