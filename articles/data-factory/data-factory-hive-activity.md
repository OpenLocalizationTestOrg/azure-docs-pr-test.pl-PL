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
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="92586-103">Przekształcanie danych za pomocą działania Hive w fabryce danych Azure</span><span class="sxs-lookup"><span data-stu-id="92586-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="92586-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="92586-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="92586-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="92586-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="92586-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="92586-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="92586-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="92586-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="92586-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="92586-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="92586-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="92586-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="92586-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="92586-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="92586-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="92586-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="92586-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="92586-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="92586-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="92586-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="92586-114">Hello HDInsight Hive działania w fabryce danych [potoku](data-factory-create-pipelines.md) wykonuje zapytania Hive na [własne](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub [na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) klastrów HDInsight opartych na systemie Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="92586-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="92586-115">W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="92586-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="92586-116">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i hello samouczek: [kompilacji swój pierwszy potok danych](data-factory-build-your-first-pipeline.md) przed przeczytaniem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="92586-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="92586-117">Składnia</span><span class="sxs-lookup"><span data-stu-id="92586-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="92586-118">Szczegóły składni</span><span class="sxs-lookup"><span data-stu-id="92586-118">Syntax details</span></span>
| <span data-ttu-id="92586-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="92586-119">Property</span></span> | <span data-ttu-id="92586-120">Opis</span><span class="sxs-lookup"><span data-stu-id="92586-120">Description</span></span> | <span data-ttu-id="92586-121">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92586-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92586-122">name</span><span class="sxs-lookup"><span data-stu-id="92586-122">name</span></span> |<span data-ttu-id="92586-123">Nazwa działania hello</span><span class="sxs-lookup"><span data-stu-id="92586-123">Name of hello activity</span></span> |<span data-ttu-id="92586-124">Tak</span><span class="sxs-lookup"><span data-stu-id="92586-124">Yes</span></span> |
| <span data-ttu-id="92586-125">description</span><span class="sxs-lookup"><span data-stu-id="92586-125">description</span></span> |<span data-ttu-id="92586-126">Tekst opisujący, jakie działanie hello jest używany dla</span><span class="sxs-lookup"><span data-stu-id="92586-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="92586-127">Nie</span><span class="sxs-lookup"><span data-stu-id="92586-127">No</span></span> |
| <span data-ttu-id="92586-128">type</span><span class="sxs-lookup"><span data-stu-id="92586-128">type</span></span> |<span data-ttu-id="92586-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="92586-129">HDinsightHive</span></span> |<span data-ttu-id="92586-130">Tak</span><span class="sxs-lookup"><span data-stu-id="92586-130">Yes</span></span> |
| <span data-ttu-id="92586-131">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="92586-131">inputs</span></span> |<span data-ttu-id="92586-132">Dane wejściowe używane na powitania Hive działania</span><span class="sxs-lookup"><span data-stu-id="92586-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="92586-133">Nie</span><span class="sxs-lookup"><span data-stu-id="92586-133">No</span></span> |
| <span data-ttu-id="92586-134">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="92586-134">outputs</span></span> |<span data-ttu-id="92586-135">Dane wyjściowe, generowane przez działanie Hive hello</span><span class="sxs-lookup"><span data-stu-id="92586-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="92586-136">Tak</span><span class="sxs-lookup"><span data-stu-id="92586-136">Yes</span></span> |
| <span data-ttu-id="92586-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="92586-137">linkedServiceName</span></span> |<span data-ttu-id="92586-138">Klaster usługi HDInsight toohello odwołanie w zarejestrowany jako połączonej usługi z fabryki danych</span><span class="sxs-lookup"><span data-stu-id="92586-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="92586-139">Tak</span><span class="sxs-lookup"><span data-stu-id="92586-139">Yes</span></span> |
| <span data-ttu-id="92586-140">Skrypt</span><span class="sxs-lookup"><span data-stu-id="92586-140">script</span></span> |<span data-ttu-id="92586-141">Określ wbudowanego skryptu Hive hello</span><span class="sxs-lookup"><span data-stu-id="92586-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="92586-142">Nie</span><span class="sxs-lookup"><span data-stu-id="92586-142">No</span></span> |
| <span data-ttu-id="92586-143">Ścieżka skryptu</span><span class="sxs-lookup"><span data-stu-id="92586-143">script path</span></span> |<span data-ttu-id="92586-144">Magazyn hello Hive skryptu w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku.</span><span class="sxs-lookup"><span data-stu-id="92586-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="92586-145">Użyj właściwości 'script' lub "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="92586-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="92586-146">Nie można używać razem.</span><span class="sxs-lookup"><span data-stu-id="92586-146">Both cannot be used together.</span></span> <span data-ttu-id="92586-147">Nazwa pliku Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="92586-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="92586-148">Nie</span><span class="sxs-lookup"><span data-stu-id="92586-148">No</span></span> |
| <span data-ttu-id="92586-149">Definiuje</span><span class="sxs-lookup"><span data-stu-id="92586-149">defines</span></span> |<span data-ttu-id="92586-150">Określ parametry jako pary klucz wartość dla odwołania do skryptu Hive hello za pomocą "hiveconf"</span><span class="sxs-lookup"><span data-stu-id="92586-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="92586-151">Nie</span><span class="sxs-lookup"><span data-stu-id="92586-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="92586-152">Przykład</span><span class="sxs-lookup"><span data-stu-id="92586-152">Example</span></span>
<span data-ttu-id="92586-153">Zastanówmy się przykładem gry rejestruje analytics miejscu tooidentify hello czasu poświęcanego przez użytkowników granie w gry uruchomiony przez firmę.</span><span class="sxs-lookup"><span data-stu-id="92586-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="92586-154">Hello następujące dziennik jest przykładowy dziennik gier, czyli przecinkami (`,`) oddzielone i zawiera następujące pola — ProfileID, SessionStart, czas trwania, SrcIPAddress i GameType hello.</span><span class="sxs-lookup"><span data-stu-id="92586-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="92586-155">Witaj **wykonanie skryptu technologii Hive** tooprocess te dane:</span><span class="sxs-lookup"><span data-stu-id="92586-155">hello **Hive script** tooprocess this data:</span></span>

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

<span data-ttu-id="92586-156">tooexecute tej gałęzi skryptu w potoku fabryki danych, należy toodo hello poniżej</span><span class="sxs-lookup"><span data-stu-id="92586-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="92586-157">Utwórz tooregister połączonej usługi [klaster obliczeniowy własne HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) lub skonfiguruj [klastra obliczeniowego HDInsight na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="92586-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="92586-158">Umożliwia wywołanie tej połączonej usługi "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="92586-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="92586-159">Utwórz [połączona usługa](data-factory-azure-blob-connector.md) tooconfigure hello połączenia tooAzure obiektu Blob magazynu obsługującego hello danych.</span><span class="sxs-lookup"><span data-stu-id="92586-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="92586-160">Umożliwia wywołanie tej połączonej usługi "StorageLinkedService"</span><span class="sxs-lookup"><span data-stu-id="92586-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="92586-161">Utwórz [zestawów danych](data-factory-create-datasets.md) wskazanie toohello dane wejściowe i hello dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="92586-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="92586-162">Umożliwia wywołanie hello wejściowy zestaw danych "HiveSampleIn" i hello wyjściowy zestaw danych "HiveSampleOut"</span><span class="sxs-lookup"><span data-stu-id="92586-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="92586-163">Skopiuj zapytanie Hive hello jako plik tooAzure skonfigurowane w kroku #2 magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="92586-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="92586-164">Jeśli hello magazynu do obsługi danych hello różni się od hello jedną hosting tego pliku kwerendy, Utwórz oddzielne połączoną usługą magazynu Azure i zapoznaj tooit w działaniu hello.</span><span class="sxs-lookup"><span data-stu-id="92586-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="92586-165">Użyj ** scriptPath ** toospecify hello ścieżki toohive zapytania pliku i **scriptLinkedService** toospecify hello Azure magazynu, który zawiera plik skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="92586-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="92586-166">Można też podać wbudowanego skryptu Hive hello w definicji działania hello przy użyciu hello **skryptu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="92586-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="92586-167">Nie zaleca się tą metodą wszystkie znaki specjalne w skrypcie hello w dokumencie JSON hello musi toobe zmienione znaczenie i mogą Przyczyna debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="92586-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="92586-168">Witaj najlepszym rozwiązaniem jest toofollow krok #4.</span><span class="sxs-lookup"><span data-stu-id="92586-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="92586-169">Utworzyć potok z hello HDInsightHive działania.</span><span class="sxs-lookup"><span data-stu-id="92586-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="92586-170">działanie Hello procesów/transformacje hello danych.</span><span class="sxs-lookup"><span data-stu-id="92586-170">hello activity processes/transforms hello data.</span></span>

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
6. <span data-ttu-id="92586-171">Wdróż hello potoku.</span><span class="sxs-lookup"><span data-stu-id="92586-171">Deploy hello pipeline.</span></span> <span data-ttu-id="92586-172">Zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="92586-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="92586-173">Monitorowanie za pomocą funkcji monitorowania fabryki danych hello potoku hello i widoki zarządzania.</span><span class="sxs-lookup"><span data-stu-id="92586-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="92586-174">Zobacz [monitorowanie i zarządzanie nimi potoki fabryki danych](data-factory-monitor-manage-pipelines.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="92586-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="92586-175">Określanie parametrów dla skryptu Hive</span><span class="sxs-lookup"><span data-stu-id="92586-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="92586-176">W tym przykładzie gier dzienniki są codziennie pozyskanych w magazynie obiektów Blob Azure i są przechowywane w folderze na partycje za pomocą daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="92586-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="92586-177">Mają skryptu Hive hello tooparameterize i przekazać lokalizacji folderu wejściowych hello dynamicznie w czasie wykonywania, a także wygenerować hello dane wyjściowe z datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="92586-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="92586-178">toouse sparametryzowana skryptu Hive, wykonaj następujące hello</span><span class="sxs-lookup"><span data-stu-id="92586-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="92586-179">Zdefiniuj parametry hello w **definiuje**.</span><span class="sxs-lookup"><span data-stu-id="92586-179">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="92586-180">W hello skryptu Hive, można znaleźć przy użyciu parametru toohello **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="92586-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="92586-181">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="92586-181">See Also</span></span>
* [<span data-ttu-id="92586-182">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="92586-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="92586-183">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="92586-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="92586-184">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="92586-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="92586-185">Wywoływanie programów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="92586-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="92586-186">Wywoływanie skryptów języka R</span><span class="sxs-lookup"><span data-stu-id="92586-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

