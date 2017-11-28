---
title: "potoki danych predykcyjnej aaaCreate przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate utworzyć predykcyjnej potoki przy użyciu fabryki danych Azure i usługi Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="0d738-103">Tworzenie potoków predykcyjnej przy użyciu usługi Azure Machine Learning i fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="0d738-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="0d738-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="0d738-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="0d738-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="0d738-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="0d738-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="0d738-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="0d738-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="0d738-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="0d738-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="0d738-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="0d738-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0d738-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="0d738-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0d738-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="0d738-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="0d738-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="0d738-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0d738-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="0d738-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="0d738-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="0d738-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0d738-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="0d738-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0d738-115">Azure Machine Learning</span></span>
<span data-ttu-id="0d738-116">[Usługa Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) umożliwia toobuild możesz, testowania i wdrażania rozwiązań analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="0d738-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="0d738-117">Z wysokiego poziomu punktu widzenia można to zrobić w trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="0d738-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="0d738-118">**Tworzenie eksperymentu uczenia**.</span><span class="sxs-lookup"><span data-stu-id="0d738-118">**Create a training experiment**.</span></span> <span data-ttu-id="0d738-119">W tym kroku są wykonywane przy użyciu hello Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="0d738-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="0d738-120">Witaj ML studio to środowisko visual programowanie zespołowe używanie tootrain i testowanie modelu analizy predykcyjnej przy użyciu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="0d738-121">**Przekonwertuj go eksperyment predykcyjny tooa**.</span><span class="sxs-lookup"><span data-stu-id="0d738-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="0d738-122">Po modelu po zapoznaniu z istniejącymi danymi i są gotowe toouse go tooscore nowe dane, Przygotuj i usprawnić eksperymentu wyników.</span><span class="sxs-lookup"><span data-stu-id="0d738-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="0d738-123">**Go wdrożyć jako usługę sieci web**.</span><span class="sxs-lookup"><span data-stu-id="0d738-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="0d738-124">Możesz opublikować oceniania eksperymentu jako usługi sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="0d738-125">Można wysyłać modelu tooyour danych za pomocą tego punktu końcowego usługi sieci web i odbierać prognoz wyniku z modelu hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="0d738-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0d738-126">Azure Data Factory</span></span>
<span data-ttu-id="0d738-127">Fabryka danych jest usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować hello **przepływu** i **przekształcania** danych.</span><span class="sxs-lookup"><span data-stu-id="0d738-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="0d738-128">Można utworzyć integracji danych rozwiązania przy użyciu fabryki danych Azure, które można pozyskiwania danych z różnych baz danych, proces/transformacji danych hello i publikowanie magazyny danych toohello hello wynik danych.</span><span class="sxs-lookup"><span data-stu-id="0d738-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="0d738-129">Usługi fabryka danych pozwala toocreate potoki danych, które Przenieś i przekształcania danych, a następnie uruchom potoki hello zgodnie z zaplanowanym harmonogramem (co godzinę, codziennie, co tydzień, itp.).</span><span class="sxs-lookup"><span data-stu-id="0d738-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="0d738-130">Ponadto zapewnia elementy powiązane hello toodisplay zaawansowane wizualizacje i zależności między Twojej potoki danych i monitorowania sieci potoki danych z problemów znaleźć tooeasily pojedynczego ujednoliconego podglądu, a ustawienia alertów monitorowania.</span><span class="sxs-lookup"><span data-stu-id="0d738-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="0d738-131">Zobacz [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i [kompilacji swój pierwszy potok](data-factory-build-your-first-pipeline.md) tooquickly artykuły wprowadzenie hello usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="0d738-132">Fabryki danych i jednocześnie uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="0d738-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="0d738-133">Azure umożliwia fabryki danych tooeasily możesz utworzyć potoki, które używają opublikowanych [usługi Azure Machine Learning] [ azure-machine-learning] usługi analizy predykcyjnej sieci web.</span><span class="sxs-lookup"><span data-stu-id="0d738-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="0d738-134">Przy użyciu hello **działanie wykonywania wsadowego** w potoku fabryki danych Azure, można wywołać usługi Azure ML web toomake operacje przewidywania dla usługi na powitania danych w partii.</span><span class="sxs-lookup"><span data-stu-id="0d738-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="0d738-135">Zobacz [uczenie Maszynowe Azure wywoływania usługi sieci web przy użyciu hello działanie wykonywania wsadowego](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0d738-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="0d738-136">Wraz z upływem czasu hello modeli predykcyjnych w eksperymentach oceniania uczenia Maszynowego Azure hello muszą toobe retrained przy użyciu nowych baz danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="0d738-137">Model usługi uczenie Maszynowe Azure z potoku fabryki danych można ponownie ucz, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0d738-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="0d738-138">Opublikuj eksperyment uczenia hello (eksperyment predykcyjny nie) jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="0d738-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="0d738-139">Należy wykonać ten krok w hello Azure ML Studio, tak jak tooexpose eksperyment predykcyjny jako usługę sieci web w poprzednim scenariuszu hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="0d738-140">Użyj hello działanie wykonywania wsadowego usługi Azure ML tooinvoke hello usługę sieci web eksperyment uczenia hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="0d738-141">Zasadniczo można użyć hello tooinvoke działanie wykonywania wsadowego usługi uczenie Maszynowe Azure zarówno uczenie usługi sieci web i oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="0d738-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="0d738-142">Po wykonaniu ponownego trenowania zaktualizuj hello oceniania usługi sieci web (eksperyment predykcyjny udostępniony jako usługa sieci web) z hello nowo uczonego modelu przy użyciu hello **działanie aktualizacji zasobu usługi Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="0d738-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="0d738-143">Zobacz [aktualizowanie modeli przy użyciu działanie aktualizacji zasobu](data-factory-azure-ml-update-resource-activity.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0d738-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="0d738-144">Wywoływanie usługi sieci web przy użyciu działanie wykonywania wsadowego</span><span class="sxs-lookup"><span data-stu-id="0d738-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="0d738-145">Przenoszenie danych tooorchestrate fabryki danych Azure i przetwarzania, a następnie wykonaj wykonywania wsadowego usługi za pomocą usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0d738-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="0d738-146">Poniżej przedstawiono kroki najwyższego poziomu hello:</span><span class="sxs-lookup"><span data-stu-id="0d738-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="0d738-147">Tworzenie usługi Azure Machine Learning połączone.</span><span class="sxs-lookup"><span data-stu-id="0d738-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="0d738-148">Należy hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="0d738-148">You need hello following values:</span></span>

   1. <span data-ttu-id="0d738-149">**Identyfikator URI żądania** dla hello API wykonywania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="0d738-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="0d738-150">Hello przez identyfikator URI żądania można znaleźć, klikając hello **BATCH EXECUTION** łącze na stronie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="0d738-151">**Klucz interfejsu API** dla hello opublikowane usługi sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="0d738-152">Klucz interfejsu API hello można znaleźć, klikając hello usługi sieci web, które zostały opublikowane.</span><span class="sxs-lookup"><span data-stu-id="0d738-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="0d738-153">Użyj hello **AzureMLBatchExecution** działania.</span><span class="sxs-lookup"><span data-stu-id="0d738-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Pulpit nawigacyjny uczenia maszynowego](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Identyfikator URI partii](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="0d738-156">Scenariusz: Eksperymentów przy użyciu sieci Web usługi wejść/wyjść odwołujące się toodata w magazynie obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="0d738-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="0d738-157">W tym scenariuszu hello usługi sieci Web Azure Machine Learning sprawia, że prognoz przy użyciu danych z pliku w magazynie obiektów blob platformy Azure i przechowuje wyniki prognozowania hello w magazynie obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="0d738-158">Witaj następujące JSON definiuje potoku fabryki danych do działania AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="0d738-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="0d738-159">działanie Hello ma hello dataset **DecisionTreeInputBlob** jako dane wejściowe i **DecisionTreeResultBlob** jako dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="0d738-160">Witaj **DecisionTreeInputBlob** jest przekazywany jako usługi sieci web toohello wejściowych przez przy użyciu hello **WebServiceInputActivity** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="0d738-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="0d738-161">Witaj **DecisionTreeResultBlob** jest przekazywany jako usługi sieci Web dane wyjściowe toohello przez przy użyciu hello **webServiceOutputs** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="0d738-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0d738-162">Jeśli usługa sieci web hello przyjmuje wielu danych wejściowych, użyj hello **webServiceInputs** zamiast za pomocą właściwości **WebServiceInputActivity**.</span><span class="sxs-lookup"><span data-stu-id="0d738-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="0d738-163">Zobacz hello [usługi sieci Web wymaga wielu nakładów](#web-service-requires-multiple-inputs) sekcji, na przykład za pomocą właściwości webServiceInputs hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="0d738-164">Zestawy danych, które odwołują się hello **WebServiceInputActivity**/**webServiceInputs** i **webServiceOutputs** właściwości (w  **typeProperties**) również muszą być zawarte w hello działania **dane wejściowe** i **generuje**.</span><span class="sxs-lookup"><span data-stu-id="0d738-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="0d738-165">W eksperymencie uczenie Maszynowe Azure wprowadzania usługi sieci web i porty wyjścia i parametry globalne mają nazwy domyślnej ("input1", "input2"), które można dostosować.</span><span class="sxs-lookup"><span data-stu-id="0d738-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="0d738-166">nazwy Hello, używane w przypadku webServiceInputs, webServiceOutputs i ustawienia globalParameters musi dokładnie odpowiadać hello nazw hello eksperymenty.</span><span class="sxs-lookup"><span data-stu-id="0d738-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="0d738-167">Ładunek żądania próbki hello można wyświetlić na stronie pomocy wykonywania wsadowego hello mapowanie hello oczekiwano tooverify punktu końcowego uczenia Maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="0d738-168">Tylko wejściami i wyjściami hello AzureMLBatchExecution działania mogą być przekazywane jako parametry toohello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0d738-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="0d738-169">Na przykład hello powyżej fragment kodu JSON, DecisionTreeInputBlob jest wejściowych toohello AzureMLBatchExecution działalność, która jest przekazywany jako wejściowych toohello usługi sieci Web za pomocą parametru WebServiceInputActivity.</span><span class="sxs-lookup"><span data-stu-id="0d738-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="0d738-170">Przykład</span><span class="sxs-lookup"><span data-stu-id="0d738-170">Example</span></span>
<span data-ttu-id="0d738-171">Ten przykład używa usługi Azure Storage toohold zarówno hello danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="0d738-172">Firma Microsoft zaleca zapoznanie hello [kompilacji swój pierwszy potok z fabryką danych] [ adf-build-1st-pipeline] samouczka przed rozpoczęciem tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="0d738-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="0d738-173">W tym przykładzie, należy użyć hello Edytor fabryki danych toocreate fabryki danych artefakty (połączone usługi, zestawy danych, potoku).</span><span class="sxs-lookup"><span data-stu-id="0d738-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="0d738-174">Utwórz **połączona usługa** dla Twojego **usługi Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="0d738-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="0d738-175">Witaj plików wejściowych i wyjściowych znajdują się w różnych kont magazynu, należy najpierw dwóch połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="0d738-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="0d738-176">Oto przykład JSON:</span><span class="sxs-lookup"><span data-stu-id="0d738-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="0d738-177">Utwórz hello **wejściowych** fabryki danych Azure **zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="0d738-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="0d738-178">W odróżnieniu od niektórych innych fabryki danych zestawów danych, te zestawy danych musi zawierać zarówno **folderPath** i **fileName** wartości.</span><span class="sxs-lookup"><span data-stu-id="0d738-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="0d738-179">Można użyć partycjonowania toocause każdej partii tooprocess wykonywania (każdy wycinek danych) lub utworzyć unikatowe dane wejściowe i plików wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="0d738-180">Może być konieczne tooinclude hello tootransform niektóre działania nadrzędnego danych wejściowych w formacie pliku CSV hello i umieścić go w hello konta magazynu dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="0d738-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="0d738-181">W takim przypadku nie obejmuje hello **zewnętrznych** i **externalData** ustawienia w powitania po przykład oraz DecisionTreeInputBlob Twojego będą hello wyjściowy zestaw danych z innego działania.</span><span class="sxs-lookup"><span data-stu-id="0d738-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="0d738-182">Plik wejściowy csv musi mieć wiersz nagłówka kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="0d738-183">Jeśli używasz hello **działanie kopiowania** toocreate/przeniesienia hello csv do magazynu obiektów blob hello, należy ustawić właściwość obiektu sink hello **blobWriterAddHeader** za**true**.</span><span class="sxs-lookup"><span data-stu-id="0d738-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="0d738-184">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0d738-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="0d738-185">Jeśli plik csv hello nie ma wiersz nagłówka hello, mogą pojawić się hello następujący błąd: **błąd w działaniu: Wystąpił błąd podczas odczytywania ciągu. Nieoczekiwany token: metodzie StartObject. Ścieżka ', wiersz 1, umieść 1**.</span><span class="sxs-lookup"><span data-stu-id="0d738-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="0d738-186">Utwórz hello **dane wyjściowe** fabryki danych Azure **zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="0d738-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="0d738-187">W tym przykładzie użyto partycjonowania toocreate ścieżka wyjściowa unikatowy dla każdego wykonania wycinka.</span><span class="sxs-lookup"><span data-stu-id="0d738-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="0d738-188">Bez hello partycje, działanie hello zastąpiłaby hello pliku.</span><span class="sxs-lookup"><span data-stu-id="0d738-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="0d738-189">Utwórz **połączona usługa** typu: **AzureMLLinkedService**, zapewniając klucza hello interfejsu API i modelu adres URL wykonywania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="0d738-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="0d738-190">Na koniec tworzenie potoku nadrzędnym **AzureMLBatchExecution** działania.</span><span class="sxs-lookup"><span data-stu-id="0d738-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="0d738-191">W czasie wykonywania potoku wykonuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0d738-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="0d738-192">Pobiera lokalizację pliku wejściowego hello hello z zestawów danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="0d738-193">Wywołuje wykonywania wsadowego usługi uczenie maszynowe Azure hello interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0d738-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="0d738-194">Kopie hello wykonanie partii danych wyjściowych toohello blob podane w zestawie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0d738-195">Działanie AzureMLBatchExecution może mieć zero lub więcej wejściami i wyjściami jeden lub więcej.</span><span class="sxs-lookup"><span data-stu-id="0d738-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="0d738-196">Zarówno **start** i **zakończenia** dat i godzin musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0d738-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0d738-197">Na przykład: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="0d738-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="0d738-198">Witaj **zakończenia** czasu jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="0d738-198">hello **end** time is optional.</span></span> <span data-ttu-id="0d738-199">Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin.**"</span><span class="sxs-lookup"><span data-stu-id="0d738-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="0d738-200">potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="0d738-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="0d738-201">Szczegółowe informacje dotyczące właściwości kodu JSON znajdują się w artykule [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) (Dokumentacja dotycząca skryptów JSON).</span><span class="sxs-lookup"><span data-stu-id="0d738-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0d738-202">Określenie danych wejściowych dla działania AzureMLBatchExecution hello jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="0d738-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="0d738-203">Scenariusz: Eksperymentów przy użyciu modułów odczytywania/zapisywania toorefer toodata w różnych miejsc</span><span class="sxs-lookup"><span data-stu-id="0d738-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="0d738-204">Inny typowy scenariusz, podczas tworzenia eksperymenty uczenie Maszynowe Azure jest toouse składników zapisywania i odczytywania modułów.</span><span class="sxs-lookup"><span data-stu-id="0d738-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="0d738-205">Moduł czytnika Hello jest tooload używane dane do eksperymentu, a moduł zapisywania hello jest toosave danych z eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="0d738-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="0d738-206">Szczegółowe informacje na temat składników zapisywania i odczytywania modułów, zobacz [czytnika](https://msdn.microsoft.com/library/azure/dn905997.aspx) i [zapisywania](https://msdn.microsoft.com/library/azure/dn905984.aspx) tematy w bibliotece MSDN.</span><span class="sxs-lookup"><span data-stu-id="0d738-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="0d738-207">Korzystając z hello składników zapisywania i odczytywania modułów, jest dobrym rozwiązaniem toouse parametr usługi sieci Web dla każdej właściwości w tych modułów odczytywania/zapisywania.</span><span class="sxs-lookup"><span data-stu-id="0d738-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="0d738-208">Te parametry sieci web umożliwiają tooconfigure hello wartości w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0d738-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="0d738-209">Na przykład można utworzyć eksperyment przy użyciu modułu reader używa usługi Azure SQL Database: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0d738-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="0d738-210">Po wdrożeniu usługi sieci web hello ma konsumentów hello tooenable toospecify usługi sieci web hello o nazwie YYY.database.windows.net innego serwera SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="0d738-211">Tooallow parametr usługi sieci Web można użyć tego toobe wartość skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="0d738-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="0d738-212">Usługi sieci Web w danych wejściowych i wyjściowych różnią się od parametry usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0d738-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="0d738-213">Pierwszy scenariusz hello już wspomniano, jak dane wejściowe i wyjściowe można określić dla usługi sieci Web uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="0d738-214">W tym scenariuszu należy przekazać parametry usługi sieci Web, które odpowiadają tooproperties odczytywania/zapisywania modułów.</span><span class="sxs-lookup"><span data-stu-id="0d738-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="0d738-215">Przyjrzyjmy się scenariusz użycia parametry usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0d738-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="0d738-216">Masz wdrożonej usługi sieci web uczenie maszynowe Azure używającej tooread moduł czytnika danych z jednego źródła danych hello obsługiwane przez usługi Azure Machine Learning (na przykład: baza danych SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="0d738-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="0d738-217">Po wykonaniu hello wsadowe hello wyniki są zapisywane za pomocą modułu zapisywania (baza danych SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="0d738-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="0d738-218">Nie sieci web usługi wejściami i wyjściami są definiowane w hello eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="0d738-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="0d738-219">W takim przypadku firma Microsoft zaleca, aby skonfigurować parametry usługi sieci web odpowiednich hello składników zapisywania i odczytywania modułów.</span><span class="sxs-lookup"><span data-stu-id="0d738-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="0d738-220">Taka konfiguracja pozwala hello odczytywania/zapisywania skonfigurowane podczas używania działania AzureMLBatchExecution hello toobe modułów.</span><span class="sxs-lookup"><span data-stu-id="0d738-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="0d738-221">Określ parametry usługi sieci Web w hello **globalParameters** sekcji w działaniu hello JSON w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="0d738-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="0d738-222">Można również użyć [funkcji fabryki danych](data-factory-functions-variables.md) do przekazywania wartości hello parametry usługi sieci Web, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0d738-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="0d738-223">Parametry usługi sieci Web Hello jest rozróżniana wielkość liter, dlatego upewnij się, czy nazwy hello, które określisz w działaniu hello JSON pasują hello te udostępniane przez hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0d738-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="0d738-224">Przy użyciu tooread moduł czytnika danych z wielu plików w obiekcie Blob Azure</span><span class="sxs-lookup"><span data-stu-id="0d738-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="0d738-225">Dane big data potoków z działania, takie jak Pig i Hive można utworzyć jeden lub więcej plików wyjściowych bez rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="0d738-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="0d738-226">Na przykład po określeniu tabelę zewnętrzną Hive hello danych dla tabeli zewnętrznej Hive hello można przechowywane w magazynu obiektów blob platformy Azure z powitania po 000000_0 nazwy.</span><span class="sxs-lookup"><span data-stu-id="0d738-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="0d738-227">Moduł czytnika hello w tooread eksperymentu korzystanie z wielu plików i używać ich na potrzeby prognoz.</span><span class="sxs-lookup"><span data-stu-id="0d738-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="0d738-228">Korzystając z hello czytnika modułu w eksperymencie usługi Azure Machine Learning, obiektów Blob platformy Azure można określić jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0d738-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="0d738-229">pliki Hello w hello magazynu obiektów blob platformy Azure mogą być pliki wyjściowe hello (przykład: 000000_0) który są produkowane przez Pig i Hive skryptu uruchomionego w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d738-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="0d738-230">Witaj moduł czytnika pozwala tooread plików (nie rozszerzenia) przez skonfigurowanie hello **toocontainer ścieżki, w katalogu/obiektów blob**.</span><span class="sxs-lookup"><span data-stu-id="0d738-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="0d738-231">Hello **toocontainer ścieżki** punktów toohello kontenera i **katalogu/obiektów blob** punktów toofolder zawierający pliki hello, jak pokazano w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="0d738-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="0d738-232">Hello gwiazdka oznacza to, \*) **Określa, że hello wszystkie pliki w hello kontenera lub folder (oznacza to, aggregateddata/rocznie danych = miesiąc-2014-6 /\*)** są odczytywane w ramach eksperymentu hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Właściwości obiektów Blob platformy Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="0d738-234">Przykład</span><span class="sxs-lookup"><span data-stu-id="0d738-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="0d738-235">W potoku z działania AzureMLBatchExecution o parametry usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="0d738-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="0d738-236">W hello powyżej przykład JSON:</span><span class="sxs-lookup"><span data-stu-id="0d738-236">In hello above JSON example:</span></span>

* <span data-ttu-id="0d738-237">Azure Machine Learning w sieci Web usługi używa czytnika i zapisywania danych tooread/zapisu dla modułu z wdrożonych Hello / tooan bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="0d738-238">Ta usługa sieci Web udostępnia następujące cztery parametry hello: Nazwa serwera, nazwa bazy danych, nazwę konta użytkownika serwera i hasło konta użytkownika serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0d738-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="0d738-239">Zarówno **start** i **zakończenia** dat i godzin musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0d738-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0d738-240">Na przykład: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="0d738-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="0d738-241">Witaj **zakończenia** czasu jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="0d738-241">hello **end** time is optional.</span></span> <span data-ttu-id="0d738-242">Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin.**"</span><span class="sxs-lookup"><span data-stu-id="0d738-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="0d738-243">potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="0d738-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="0d738-244">Szczegółowe informacje dotyczące właściwości kodu JSON znajdują się w artykule [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) (Dokumentacja dotycząca skryptów JSON).</span><span class="sxs-lookup"><span data-stu-id="0d738-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="0d738-245">Inne scenariusze</span><span class="sxs-lookup"><span data-stu-id="0d738-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="0d738-246">Usługa sieci Web wymaga wielu danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="0d738-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="0d738-247">Jeśli usługa sieci web hello przyjmuje wielu danych wejściowych, użyj hello **webServiceInputs** zamiast za pomocą właściwości **WebServiceInputActivity**.</span><span class="sxs-lookup"><span data-stu-id="0d738-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="0d738-248">Zestawy danych, które odwołują się hello **webServiceInputs** również muszą być zawarte w hello działania **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="0d738-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="0d738-249">W eksperymencie uczenie Maszynowe Azure wprowadzania usługi sieci web i porty wyjścia i parametry globalne mają nazwy domyślnej ("input1", "input2"), które można dostosować.</span><span class="sxs-lookup"><span data-stu-id="0d738-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="0d738-250">nazwy Hello, używane w przypadku webServiceInputs, webServiceOutputs i ustawienia globalParameters musi dokładnie odpowiadać hello nazw hello eksperymenty.</span><span class="sxs-lookup"><span data-stu-id="0d738-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="0d738-251">Ładunek żądania próbki hello można wyświetlić na stronie pomocy wykonywania wsadowego hello mapowanie hello oczekiwano tooverify punktu końcowego uczenia Maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="0d738-252">Usługa sieci Web nie wymaga danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="0d738-252">Web Service does not require an input</span></span>
<span data-ttu-id="0d738-253">Azure ML wsadowe wykonywanie usług sieci web może być używane toorun przepływów pracy, na przykład R lub Python skrypty, które nie mogą wymagać wszystkie dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0d738-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="0d738-254">Lub eksperymentu hello mogą być skonfigurowane przy użyciu modułu nie ujawnia żadnych GlobalParameters czytniku.</span><span class="sxs-lookup"><span data-stu-id="0d738-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="0d738-255">W takim przypadku hello AzureMLBatchExecution działania zostanie skonfigurowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d738-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="0d738-256">Usługa sieci Web nie wymaga danych wejściowych/wyjściowych</span><span class="sxs-lookup"><span data-stu-id="0d738-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="0d738-257">Witaj usługi sieci web wykonywania wsadowego uczenie Maszynowe Azure może nie mieć żadnych danych wyjściowych z usługą sieci Web skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="0d738-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="0d738-258">W tym przykładzie nie istnieje usługi sieci Web w danych wejściowych lub wyjściowych, ani nie skonfigurowano żadnych GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="0d738-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="0d738-259">Nadal jest wyjściem skonfigurowane w działaniu hello, się, ale nie zostanie podany jako webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="0d738-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="0d738-260">Czytników używa usługi sieci Web i zapisywania i hello działania działa tylko wtedy, gdy inne działania zakończyło się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="0d738-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="0d738-261">Hello Azure ML web składników zapisywania i odczytywania modułów usługi może być skonfigurowany toorun z lub bez żadnych GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="0d738-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="0d738-262">Można jednak, że usługa tooembed wywołuje w potoku, która używa usługi hello tooinvoke zależności zestawu danych tylko wtedy, gdy niektóre nadrzędnego przetwarzanie zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="0d738-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="0d738-263">Po zakończeniu wykonywania wsadowego usługi hello przy użyciu tej metody, można również uruchomić innych działań.</span><span class="sxs-lookup"><span data-stu-id="0d738-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="0d738-264">W takim przypadku można wyrazić hello zależności za pomocą działania wejściach i wyjściach, bez nazw ich jako usługi sieci Web wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0d738-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="0d738-265">Witaj **takeaways** są:</span><span class="sxs-lookup"><span data-stu-id="0d738-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="0d738-266">Jeśli punkt końcowy eksperyment używa WebServiceInputActivity: jest reprezentowana przez zestaw danych obiektów blob i znajduje się w danych wejściowych działania hello i hello WebServiceInputActivity właściwość.</span><span class="sxs-lookup"><span data-stu-id="0d738-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="0d738-267">W przeciwnym razie hello WebServiceInputActivity właściwość została pominięta.</span><span class="sxs-lookup"><span data-stu-id="0d738-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="0d738-268">Jeśli punkt końcowy eksperyment używa webServiceOutput(s): są reprezentowane przez zestawy danych obiektów blob i zawarte w danych wyjściowych działania hello oraz we właściwości webServiceOutputs hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="0d738-269">generuje Hello działania i webServiceOutputs są mapowane według nazwy hello każdego danych wyjściowych w eksperymencie hello.</span><span class="sxs-lookup"><span data-stu-id="0d738-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="0d738-270">W przeciwnym razie wartość właściwości webServiceOutputs hello jest pomijany.</span><span class="sxs-lookup"><span data-stu-id="0d738-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="0d738-271">Jeśli punkt końcowy eksperyment przedstawia globalParameter(s), otrzymują one we właściwości globalParameters działania hello jako pary kluczy, wartość.</span><span class="sxs-lookup"><span data-stu-id="0d738-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="0d738-272">W przeciwnym razie wartość właściwości globalParameters hello jest pomijany.</span><span class="sxs-lookup"><span data-stu-id="0d738-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="0d738-273">Witaj kluczy jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="0d738-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="0d738-274">[Funkcje fabryki danych Azure](data-factory-functions-variables.md) mogą być używane w hello wartości.</span><span class="sxs-lookup"><span data-stu-id="0d738-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="0d738-275">Dodatkowe zestawy danych może być zawarta w właściwości wejściami i wyjściami hello działania, bez przywoływane w hello typeProperties działania.</span><span class="sxs-lookup"><span data-stu-id="0d738-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="0d738-276">Te zestawy danych będą zarządzały sposobem wykonania przy użyciu zależności wycinka, ale w przeciwnym razie są ignorowane przez hello AzureMLBatchExecution działania.</span><span class="sxs-lookup"><span data-stu-id="0d738-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="0d738-277">Aktualizowanie modeli przy użyciu działanie aktualizacji zasobu</span><span class="sxs-lookup"><span data-stu-id="0d738-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="0d738-278">Po wykonaniu ponownego trenowania zaktualizuj hello oceniania usługi sieci web (eksperyment predykcyjny udostępniony jako usługa sieci web) z hello nowo uczonego modelu przy użyciu hello **działanie aktualizacji zasobu usługi Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="0d738-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="0d738-279">Zobacz [aktualizowanie modeli przy użyciu działanie aktualizacji zasobu](data-factory-azure-ml-update-resource-activity.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0d738-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="0d738-280">Czytnik i modułów zapisywania</span><span class="sxs-lookup"><span data-stu-id="0d738-280">Reader and Writer Modules</span></span>
<span data-ttu-id="0d738-281">Typowy scenariusz użycia parametrów usługi sieci Web jest używanie hello czytników SQL Azure i zapisywania.</span><span class="sxs-lookup"><span data-stu-id="0d738-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="0d738-282">Moduł czytnika Hello jest tooload używane dane do eksperymentu z usług zarządzania danych poza Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0d738-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="0d738-283">Moduł zapisywania Hello jest toosave danych z eksperymentów do usługi zarządzania danych poza Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0d738-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="0d738-284">Aby uzyskać więcej informacji o SQL Azure/obiektów Blob Azure odczytywania/zapisywania, zobacz [czytnika](https://msdn.microsoft.com/library/azure/dn905997.aspx) i [zapisywania](https://msdn.microsoft.com/library/azure/dn905984.aspx) tematy w bibliotece MSDN.</span><span class="sxs-lookup"><span data-stu-id="0d738-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="0d738-285">przykład Witaj w poprzedniej sekcji hello używane hello obiektów Blob platformy Azure i zapisu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d738-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="0d738-286">W tej sekcji omówiono przy użyciu czytnik Azure SQL i składnika zapisywania usługi Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0d738-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0d738-287">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="0d738-287">Frequently asked questions</span></span>
<span data-ttu-id="0d738-288">**Pytanie:** mam wiele plików, które są generowane przez mój potoki danych big data.</span><span class="sxs-lookup"><span data-stu-id="0d738-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="0d738-289">Toowork działania AzureMLBatchExecution hello można używać we wszystkich plikach hello?</span><span class="sxs-lookup"><span data-stu-id="0d738-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="0d738-290">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="0d738-290">**A:** Yes.</span></span> <span data-ttu-id="0d738-291">Zobacz hello **przy użyciu tooread moduł czytnika danych z wielu plików w obiekcie Blob Azure** sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0d738-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="0d738-292">Działanie oceniania partii zadań Azure ML</span><span class="sxs-lookup"><span data-stu-id="0d738-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="0d738-293">Jeśli używasz hello **AzureMLBatchScoring** toointegrate działania przy użyciu usługi Azure Machine Learning, firma Microsoft zaleca się używanie hello najnowsza wersja **AzureMLBatchExecution** działania.</span><span class="sxs-lookup"><span data-stu-id="0d738-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="0d738-294">Witaj działania AzureMLBatchExecution została wprowadzona w hello sierpnia 2015 wersji zestawu Azure SDK i programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d738-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="0d738-295">Jeśli chcesz toocontinue przy użyciu działania AzureMLBatchScoring hello nadal odczytu za pomocą tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d738-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="0d738-296">Wsadowe ocenianie przez ML działanie Azure przy użyciu usługi Azure Storage dla wejścia/wyjścia</span><span class="sxs-lookup"><span data-stu-id="0d738-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="0d738-297">Parametry usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="0d738-297">Web Service Parameters</span></span>
<span data-ttu-id="0d738-298">Dodaj toospecify wartości parametrów usługi sieci Web, **typeProperties** toohello sekcji **AzureMLBatchScoringActivty** sekcji w potoku hello JSON, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0d738-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="0d738-299">Można również użyć [funkcji fabryki danych](data-factory-functions-variables.md) do przekazywania wartości hello parametry usługi sieci Web, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0d738-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="0d738-300">Parametry usługi sieci Web Hello jest rozróżniana wielkość liter, dlatego upewnij się, czy nazwy hello, które określisz w działaniu hello JSON pasują hello te udostępniane przez hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0d738-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="0d738-301">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0d738-301">See Also</span></span>
* [<span data-ttu-id="0d738-302">Azure wpis w blogu: wprowadzenie do fabryki danych Azure i usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0d738-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
