---
title: "Aktualizowanie modeli uczenia maszynowego przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tworzenia tworzenie potoków predykcyjnej przy użyciu fabryki danych Azure i usługi Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="c15fd-103">Aktualizowanie modeli uczenia maszynowego Azure przy użyciu działanie aktualizacji zasobu</span><span class="sxs-lookup"><span data-stu-id="c15fd-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="c15fd-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="c15fd-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="c15fd-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="c15fd-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="c15fd-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="c15fd-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="c15fd-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="c15fd-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="c15fd-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="c15fd-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="c15fd-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c15fd-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="c15fd-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c15fd-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="c15fd-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="c15fd-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="c15fd-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c15fd-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="c15fd-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="c15fd-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="c15fd-114">Główne fabryki danych Azure - artykułu integracji usługi Azure Machine Learning uzupełnia w tym artykule: [tworzenie potoków predykcyjnej przy użyciu usługi Azure Machine Learning i fabryki danych Azure](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="c15fd-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="c15fd-115">Jeśli nie zostało to jeszcze zrobione, należy przeczytać artykuł głównego przed odczytaniem za pośrednictwem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c15fd-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="c15fd-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c15fd-116">Overview</span></span>
<span data-ttu-id="c15fd-117">Wraz z upływem czasu modeli predykcyjnych w uczenie Maszynowe Azure oceniania eksperymenty konieczne retrained, przy użyciu nowych baz danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c15fd-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="c15fd-118">Po wykonaniu ponownego trenowania chcesz zaktualizować usługę sieci web oceniania retrained modelu uczenia Maszynowego.</span><span class="sxs-lookup"><span data-stu-id="c15fd-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="c15fd-119">Typowe kroki, aby włączyć ponownego trenowania i aktualizowanie modeli uczenia Maszynowego Azure za pośrednictwem usług sieci web są:</span><span class="sxs-lookup"><span data-stu-id="c15fd-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="c15fd-120">Tworzenie eksperymentu w [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="c15fd-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="c15fd-121">Po zakończeniu modelu publikowanie przy użyciu usługi Azure ML Studio usług sieci web dla obu **eksperyment uczenia** i oceniania /**eksperyment predykcyjny**.</span><span class="sxs-lookup"><span data-stu-id="c15fd-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="c15fd-122">W poniższej tabeli opisano usługi sieci web, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c15fd-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="c15fd-123">Zobacz [Retrain Machine Learning programowo modele](../machine-learning/machine-learning-retrain-models-programmatically.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c15fd-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="c15fd-124">**Usługa sieci web szkolenia** — odbiera dane szkoleniowe i tworzy przeszkolone modeli.</span><span class="sxs-lookup"><span data-stu-id="c15fd-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="c15fd-125">Dane wyjściowe ponownego trenowania jest plikiem .ilearner w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c15fd-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="c15fd-126">**Domyślny punkt końcowy** jest tworzona automatycznie dla podczas publikowania szkolenia Eksperymentując jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="c15fd-127">Można utworzyć więcej punktów końcowych, ale w przykładzie użyto tylko domyślny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c15fd-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="c15fd-128">**Ocenianie usługi sieci web** — odbiera przykłady bez etykiety danych i sprawia, że prognoz.</span><span class="sxs-lookup"><span data-stu-id="c15fd-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="c15fd-129">Dane wyjściowe prognozowania może mieć różne formy, takich jak plik CSV lub wierszy w bazie danych Azure SQL, w zależności od konfiguracji eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="c15fd-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="c15fd-130">Domyślny punkt końcowy jest utworzony automatycznie po opublikowaniu eksperyment predykcyjny jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="c15fd-131">Poniżej przedstawiono relacji między szkolenia i oceniania punktów końcowych w uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="c15fd-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![Usługi sieci Web](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="c15fd-133">Można wywołać **usługi sieci web szkolenia** za pomocą **działanie wykonywania wsadowego usługi Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="c15fd-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="c15fd-134">Wywoływanie usługi sieci web szkolenia jest taka sama jak wywoływania usługi sieci web uczenie Maszynowe Azure (oceniania usługi sieci web) dla punktów danych.</span><span class="sxs-lookup"><span data-stu-id="c15fd-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="c15fd-135">Poprzednich sekcjach opisano, jak wywołanie usługi sieci web uczenie Maszynowe Azure z potoku fabryki danych Azure szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="c15fd-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="c15fd-136">Można wywołać **oceniania usługi sieci web** za pomocą **działanie aktualizacji zasobu usługi Azure ML** aktualizowania usługi sieci web przy użyciu nowo trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="c15fd-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="c15fd-137">Poniższe przykłady zapewniają definicje połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="c15fd-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="c15fd-138">Ocenianie usługi sieci web to usługa sieci web klasycznego</span><span class="sxs-lookup"><span data-stu-id="c15fd-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="c15fd-139">Jeśli usługa sieci web oceniania **usługi sieci web klasycznego**, Utwórz drugi **punktu końcowego innych niż domyślne i nadaje się do aktualizacji** przy użyciu [portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c15fd-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="c15fd-140">Zobacz [tworzenie punktów końcowych](../machine-learning/machine-learning-create-endpoint.md) artykułu dla czynności.</span><span class="sxs-lookup"><span data-stu-id="c15fd-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="c15fd-141">Po utworzeniu punktu końcowego nadaje się do aktualizacji innych niż domyślne, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c15fd-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="c15fd-142">Kliknij przycisk **BATCH EXECUTION** można pobrać wartości identyfikatora URI dla **mlEndpoint** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="c15fd-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="c15fd-143">Kliknij przycisk **aktualizacji zasobów** łącze, aby pobrać wartości identyfikatora URI dla **updateResourceEndpoint** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="c15fd-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="c15fd-144">Klucz interfejsu API znajduje się na stronie punktu końcowego (w prawym dolnym rogu).</span><span class="sxs-lookup"><span data-stu-id="c15fd-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![można aktualizować punktu końcowego](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="c15fd-146">W poniższym przykładzie przedstawiono przykład definicji JSON usługi uczenie maszynowe Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="c15fd-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="c15fd-147">Połączona usługa używa apiKey do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c15fd-147">The linked service uses the apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="c15fd-148">Ocenianie usługi sieci web to usługa sieci web usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c15fd-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="c15fd-149">Jeśli usługa sieci web jest nowy typ usługi sieci web, która udostępnia punkt końcowy usługi Azure Resource Manager, nie trzeba dodać drugi **innych niż domyślne** punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c15fd-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="c15fd-150">**UpdateResourceEndpoint** w połączonej usługi jest w formacie:</span><span class="sxs-lookup"><span data-stu-id="c15fd-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="c15fd-151">Można uzyskać wartości dla posiadaczy miejsce w adresie URL podczas badania usługi sieci web na [portalu usługi sieci Web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c15fd-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="c15fd-152">Nowy typ punktu końcowego zasobów aktualizacji wymaga tokenu usługi AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c15fd-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="c15fd-153">Określ **servicePrincipalId** i **servicePrincipalKey**w uczenie maszynowe Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="c15fd-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="c15fd-154">Zobacz [jak tworzenie nazwy głównej usługi i przypisywanie uprawnień do zarządzania zasobów platformy Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c15fd-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="c15fd-155">Oto przykład definicji usługi uczenie maszynowe Azure połączone:</span><span class="sxs-lookup"><span data-stu-id="c15fd-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="c15fd-156">Poniższy scenariusz zawiera więcej szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="c15fd-156">The following scenario provides more details.</span></span> <span data-ttu-id="c15fd-157">Ma przykład ponownego trenowania i aktualizowanie modeli uczenia Maszynowego Azure z potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c15fd-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="c15fd-158">Scenariusz: ponownego trenowania i aktualizowanie model usługi uczenie Maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="c15fd-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="c15fd-159">Ta sekcja zawiera przykładowe potok, który używa **działanie wykonywania wsadowego usługi uczenie Maszynowe Azure** do retrain modelu.</span><span class="sxs-lookup"><span data-stu-id="c15fd-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="c15fd-160">Używa również potoku **działania usługi Azure ML aktualizacji zasobów** można zaktualizować modelu oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="c15fd-161">Sekcja ta zawiera też fragmenty kodu JSON dla wszystkich połączonych usług, zestawy danych i potoku w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c15fd-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="c15fd-162">Oto widok diagramu potoku próbki.</span><span class="sxs-lookup"><span data-stu-id="c15fd-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="c15fd-163">Jak widać, działanie wykonywania wsadowego uczenia Maszynowego Azure pobiera dane wejściowe szkolenia i szkolenia danych wyjściowych (plik iLearner).</span><span class="sxs-lookup"><span data-stu-id="c15fd-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="c15fd-164">Działanie usługi Azure ML aktualizacji zasobów przyjmuje te dane wyjściowe szkolenia i aktualizuje modelu w oceniania punkt końcowy usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="c15fd-165">Działanie aktualizacji zasobu nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="c15fd-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="c15fd-166">PlaceholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez usługi fabryka danych Azure do uruchamiania potoku.</span><span class="sxs-lookup"><span data-stu-id="c15fd-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![diagram procesu](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="c15fd-168">Magazyn obiektów Blob Azure połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="c15fd-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="c15fd-169">Magazyn Azure przechowuje następujące dane:</span><span class="sxs-lookup"><span data-stu-id="c15fd-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="c15fd-170">danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="c15fd-170">training data.</span></span> <span data-ttu-id="c15fd-171">Danych wejściowych dla usługi sieci web uczenie Maszynowe Azure szkolenia.</span><span class="sxs-lookup"><span data-stu-id="c15fd-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="c15fd-172">Plik iLearner.</span><span class="sxs-lookup"><span data-stu-id="c15fd-172">iLearner file.</span></span> <span data-ttu-id="c15fd-173">Dane wyjściowe z usługi sieci web szkolenia uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="c15fd-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="c15fd-174">Ten plik jest również dane wejściowe działanie aktualizacji zasobu.</span><span class="sxs-lookup"><span data-stu-id="c15fd-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="c15fd-175">Oto przykład definicji JSON połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="c15fd-175">Here is the sample JSON definition of the linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="c15fd-176">Szkolenie wejściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="c15fd-176">Training input dataset:</span></span>
<span data-ttu-id="c15fd-177">Następujący zestaw danych reprezentuje dane wejściowe szkolenia dla usługi sieci web uczenie Maszynowe Azure szkolenia.</span><span class="sxs-lookup"><span data-stu-id="c15fd-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="c15fd-178">Działanie wykonywania wsadowego usługi uczenie Maszynowe Azure ma tego zestawu danych jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="c15fd-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="c15fd-179">Szkolenie wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="c15fd-179">Training output dataset:</span></span>
<span data-ttu-id="c15fd-180">Następujący zestaw danych reprezentuje plik iLearner dane wyjściowe z usługi sieci web szkolenia uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="c15fd-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="c15fd-181">Działanie wykonywania wsadowego usługi Azure ML tworzy tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c15fd-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="c15fd-182">Ten zestaw danych jest także dane wejściowe działania usługi Azure ML aktualizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="c15fd-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="c15fd-183">Połączona usługa dla punktu końcowego uczenia uczenie Maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="c15fd-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="c15fd-184">Poniższy fragment kodu JSON definiuje usługi Azure Machine Learning połączone, która wskazuje domyślny punkt końcowy usługi sieci web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="c15fd-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="c15fd-185">W **Azure ML Studio**, wykonaj następujące czynności, aby uzyskać wartości dla **mlEndpoint** i **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="c15fd-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="c15fd-186">Kliknij przycisk **usług sieci WEB** w menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="c15fd-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="c15fd-187">Kliknij przycisk **usługi sieci web szkolenia** na liście usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="c15fd-188">Kliknij przycisk Kopiuj obok **klucz interfejsu API** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c15fd-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="c15fd-189">Wklej klucz Schowka do edytora JSON fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c15fd-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="c15fd-190">W **Azure ML studio**, kliknij przycisk **BATCH EXECUTION** łącza.</span><span class="sxs-lookup"><span data-stu-id="c15fd-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="c15fd-191">Kopiuj **przez identyfikator URI żądania** z **żądania** sekcji i wklej go w edytorze JSON fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c15fd-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="c15fd-192">Połączonej usługi uczenie Maszynowe Azure punktu końcowego oceniania nadaje się do aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="c15fd-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="c15fd-193">Poniższy fragment kodu JSON definiuje usługi Azure Machine Learning połączone, która wskazuje punkt końcowy nadaje się do aktualizacji innych niż domyślne oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="c15fd-194">Symbol zastępczy wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="c15fd-194">Placeholder output dataset:</span></span>
<span data-ttu-id="c15fd-195">Działanie usługi Azure ML aktualizacji zasobów nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="c15fd-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="c15fd-196">Fabryka danych Azure wymaga jednak wyjściowy zestaw danych do kierowania harmonogram potoku.</span><span class="sxs-lookup"><span data-stu-id="c15fd-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="c15fd-197">W związku z tym używamy zestawu manekina/symbol zastępczy danych, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c15fd-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="c15fd-198">Potok</span><span class="sxs-lookup"><span data-stu-id="c15fd-198">Pipeline</span></span>
<span data-ttu-id="c15fd-199">Potok zawiera dwa działania: **AzureMLBatchExecution** i **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="c15fd-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="c15fd-200">Działanie wykonywania wsadowego usługi uczenie Maszynowe Azure przyjmuje jako dane wejściowe dane szkoleniowe i tworzy plik iLearner jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c15fd-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="c15fd-201">Działanie wywołuje usługę sieci web szkolenia (eksperyment uczenia udostępniony jako usługa sieci web) przy użyciu danych wejściowych szkolenia i odbiera plik ilearner z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c15fd-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="c15fd-202">PlaceholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez usługi fabryka danych Azure do uruchamiania potoku.</span><span class="sxs-lookup"><span data-stu-id="c15fd-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![diagram procesu](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
