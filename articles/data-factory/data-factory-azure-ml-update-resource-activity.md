---
title: "modele uczenia maszynowego aaaUpdate przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate utworzyć predykcyjnej potoki przy użyciu fabryki danych Azure i usługi Azure Machine Learning"
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
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="01cb6-103">Aktualizowanie modeli uczenia maszynowego Azure przy użyciu działanie aktualizacji zasobu</span><span class="sxs-lookup"><span data-stu-id="01cb6-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="01cb6-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="01cb6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="01cb6-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="01cb6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="01cb6-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="01cb6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="01cb6-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="01cb6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="01cb6-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="01cb6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="01cb6-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="01cb6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="01cb6-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="01cb6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="01cb6-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="01cb6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="01cb6-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="01cb6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="01cb6-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="01cb6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="01cb6-114">W tym artykule uzupełnia hello głównego fabryki danych Azure - artykułu integracji usługi Azure Machine Learning: [tworzenie potoków predykcyjnej przy użyciu usługi Azure Machine Learning i fabryki danych Azure](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="01cb6-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="01cb6-115">Jeśli jeszcze tego nie zrobiono, przejrzyj artykuł głównego hello przed odczytaniem za pośrednictwem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="01cb6-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="01cb6-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="01cb6-116">Overview</span></span>
<span data-ttu-id="01cb6-117">Wraz z upływem czasu hello modeli predykcyjnych w eksperymentach oceniania uczenia Maszynowego Azure hello muszą toobe retrained przy użyciu nowych baz danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="01cb6-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="01cb6-118">Po wykonaniu ponownego trenowania chcesz hello tooupdate oceniania usługi sieci web z hello retrained model usługi uczenie Maszynowe.</span><span class="sxs-lookup"><span data-stu-id="01cb6-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="01cb6-119">ponownego trenowania tooenable typowe etapy Hello i aktualizowanie modeli uczenia Maszynowego Azure za pośrednictwem usług sieci web są:</span><span class="sxs-lookup"><span data-stu-id="01cb6-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="01cb6-120">Tworzenie eksperymentu w [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="01cb6-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="01cb6-121">Po zakończeniu hello modelu za pomocą usługi Azure ML Studio toopublish usług sieci web zarówno hello **eksperyment uczenia** i oceniania /**eksperyment predykcyjny**.</span><span class="sxs-lookup"><span data-stu-id="01cb6-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="01cb6-122">Witaj poniższej tabeli opisano usługi sieci web hello używane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="01cb6-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="01cb6-123">Zobacz [Retrain Machine Learning programowo modele](../machine-learning/machine-learning-retrain-models-programmatically.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="01cb6-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="01cb6-124">**Usługa sieci web szkolenia** — odbiera dane szkoleniowe i tworzy przeszkolone modeli.</span><span class="sxs-lookup"><span data-stu-id="01cb6-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="01cb6-125">dane wyjściowe Hello ponownego trenowania hello jest plikiem .ilearner w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb6-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="01cb6-126">Witaj **domyślny punkt końcowy** jest tworzona automatycznie dla podczas publikowania szkolenia hello Eksperymentując jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="01cb6-127">Można utworzyć więcej punktów końcowych, ale przykład Witaj używa tylko hello domyślnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="01cb6-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="01cb6-128">**Ocenianie usługi sieci web** — odbiera przykłady bez etykiety danych i sprawia, że prognoz.</span><span class="sxs-lookup"><span data-stu-id="01cb6-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="01cb6-129">dane wyjściowe Hello prognozowania może mieć różne formy, takich jak plik CSV lub wierszy w bazie danych Azure SQL, w zależności od konfiguracji hello hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="01cb6-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="01cb6-130">Hello domyślny punkt końcowy jest automatycznie utworzone po opublikowaniu hello eksperyment predykcyjny jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="01cb6-131">Hello poniższy rysunek przedstawia relację hello celów szkoleniowych i oceniania punktów końcowych w uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb6-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![Usługi sieci Web](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="01cb6-133">Można wywołać hello **usługi sieci web szkolenia** przy użyciu hello **działanie wykonywania wsadowego usługi Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="01cb6-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="01cb6-134">Wywoływanie usługi sieci web szkolenia jest taka sama jak wywoływania usługi sieci web uczenie Maszynowe Azure (oceniania usługi sieci web) dla punktów danych.</span><span class="sxs-lookup"><span data-stu-id="01cb6-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="01cb6-135">Witaj poprzedniego okładce sekcjach szczegółowo w sposób potoku tooinvoke usługi sieci web uczenie Maszynowe Azure z fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb6-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="01cb6-136">Można wywołać hello **oceniania usługi sieci web** przy użyciu hello **działanie usługi Azure ML aktualizacji zasobów** usługi sieci web hello tooupdate z hello nowo trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="01cb6-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="01cb6-137">Następujące przykłady Hello zawierają definicje połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="01cb6-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="01cb6-138">Ocenianie usługi sieci web to usługa sieci web klasycznego</span><span class="sxs-lookup"><span data-stu-id="01cb6-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="01cb6-139">Jeśli hello oceniania usługi sieci web jest **usługi sieci web klasycznego**, Utwórz drugi hello **punktu końcowego innych niż domyślne i nadaje się do aktualizacji** przy użyciu hello [portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="01cb6-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="01cb6-140">Zobacz [tworzenie punktów końcowych](../machine-learning/machine-learning-create-endpoint.md) artykułu dla czynności.</span><span class="sxs-lookup"><span data-stu-id="01cb6-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="01cb6-141">Po utworzeniu aktualizowalnych punktu końcowego innych niż domyślne hello hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="01cb6-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="01cb6-142">Kliknij przycisk **BATCH EXECUTION** tooget hello URI wartość hello **mlEndpoint** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="01cb6-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="01cb6-143">Kliknij przycisk **aktualizacji zasobów** link wartość identyfikatora URI hello tooget hello **updateResourceEndpoint** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="01cb6-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="01cb6-144">klucz interfejsu API Hello jest włączona sama strona punktu końcowego hello (w hello prawego dolnego rogu).</span><span class="sxs-lookup"><span data-stu-id="01cb6-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![można aktualizować punktu końcowego](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="01cb6-146">Hello poniższy przykład zawiera przykładowe definicji JSON hello usługi uczenie maszynowe Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="01cb6-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="01cb6-147">Witaj połączonej usługi używa hello apiKey do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="01cb6-147">hello linked service uses hello apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="01cb6-148">Ocenianie usługi sieci web to usługa sieci web usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01cb6-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="01cb6-149">Jeśli usługa sieci web hello jest nowy typ hello usługi sieci web, która udostępnia punkt końcowy usługi Azure Resource Manager, nie trzeba tooadd hello drugi **innych niż domyślne** punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="01cb6-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="01cb6-150">Witaj **updateResourceEndpoint** w hello połączonej usługi jest w formacie hello:</span><span class="sxs-lookup"><span data-stu-id="01cb6-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="01cb6-151">Podczas badania usługi sieci web hello na powitania można uzyskać wartości dla posiadaczy miejsce w adresie URL hello [portalu usługi sieci Web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="01cb6-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="01cb6-152">Nowy typ Hello aktualizacja zasobu punktu końcowego, wymaga tokenu usługi AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="01cb6-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="01cb6-153">Określ **servicePrincipalId** i **servicePrincipalKey**w uczenie maszynowe Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="01cb6-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="01cb6-154">Zobacz [jak toocreate service principal i przypisz uprawnienia toomanage zasobów platformy Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="01cb6-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="01cb6-155">Oto przykład definicji usługi uczenie maszynowe Azure połączone:</span><span class="sxs-lookup"><span data-stu-id="01cb6-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
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

<span data-ttu-id="01cb6-156">Witaj następujący scenariusz zawiera więcej szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="01cb6-156">hello following scenario provides more details.</span></span> <span data-ttu-id="01cb6-157">Ma przykład ponownego trenowania i aktualizowanie modeli uczenia Maszynowego Azure z potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb6-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="01cb6-158">Scenariusz: ponownego trenowania i aktualizowanie model usługi uczenie Maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="01cb6-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="01cb6-159">Ta sekcja zawiera przykładowe potok, który używa hello **działanie wykonywania wsadowego usługi uczenie Maszynowe Azure** tooretrain modelu.</span><span class="sxs-lookup"><span data-stu-id="01cb6-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="01cb6-160">potok Hello używa również hello **działania usługi Azure ML aktualizacji zasobów** tooupdate hello modelu w hello oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="01cb6-161">Witaj sekcji znajdują się również hello fragmenty kodu JSON dla wszystkich połączonych usług, zestawy danych i potoki w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="01cb6-162">Oto widok diagramu hello hello próbki potoku.</span><span class="sxs-lookup"><span data-stu-id="01cb6-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="01cb6-163">Jak widać, hello działania wykonanie partii usługi uczenie Maszynowe Azure ma hello szkolenia w danych wejściowych i szkolenia danych wyjściowych (plik iLearner).</span><span class="sxs-lookup"><span data-stu-id="01cb6-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="01cb6-164">Witaj działanie usługi Azure ML aktualizacji zasobów przyjmuje te dane wyjściowe szkolenia i aktualizacje hello modelu w hello oceniania punkt końcowy usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="01cb6-165">Witaj działanie aktualizacji zasobu nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="01cb6-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="01cb6-166">Hello placeholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez hello fabryki danych Azure usługa toorun hello potoku.</span><span class="sxs-lookup"><span data-stu-id="01cb6-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![diagram procesu](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="01cb6-168">Magazyn obiektów Blob Azure połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="01cb6-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="01cb6-169">Hello Azure Storage przechowuje hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="01cb6-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="01cb6-170">danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="01cb6-170">training data.</span></span> <span data-ttu-id="01cb6-171">Witaj danych wejściowych dla usługi sieci web szkolenia uczenie Maszynowe Azure hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="01cb6-172">Plik iLearner.</span><span class="sxs-lookup"><span data-stu-id="01cb6-172">iLearner file.</span></span> <span data-ttu-id="01cb6-173">dane wyjściowe z usługą sieci web szkolenia uczenie Maszynowe Azure hello Hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="01cb6-174">Ten plik jest również hello wejściowych toohello działanie aktualizacji zasobu.</span><span class="sxs-lookup"><span data-stu-id="01cb6-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="01cb6-175">Oto definicji JSON próbki hello hello połączone usługi:</span><span class="sxs-lookup"><span data-stu-id="01cb6-175">Here is hello sample JSON definition of hello linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="01cb6-176">Szkolenie wejściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="01cb6-176">Training input dataset:</span></span>
<span data-ttu-id="01cb6-177">Witaj następujący zestaw danych reprezentuje hello danych wejściowych szkoleniowych dla usługi sieci web szkolenia uczenie Maszynowe Azure hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="01cb6-178">Witaj działanie wykonywania wsadowego usługi uczenie Maszynowe Azure ma tego zestawu danych jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="01cb6-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="01cb6-179">Szkolenie wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="01cb6-179">Training output dataset:</span></span>
<span data-ttu-id="01cb6-180">Witaj następujący zestaw danych reprezentuje plik iLearner wyjściowy hello z usługi sieci web szkolenia uczenie Maszynowe Azure hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="01cb6-181">Działanie wykonywania wsadowego usługi Azure ML Hello tworzy tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="01cb6-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="01cb6-182">Ten zestaw danych jest także hello wejściowych toohello działania usługi Azure ML aktualizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="01cb6-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="01cb6-183">Połączona usługa dla punktu końcowego uczenia uczenie Maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="01cb6-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="01cb6-184">powitania po fragment kodu JSON definiuje usługę Azure Machine Learning połączone, wskazujące toohello domyślny punkt końcowy usługi sieci web szkolenia hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

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

<span data-ttu-id="01cb6-185">W **Azure ML Studio**, hello następujące wartości tooget **mlEndpoint** i **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="01cb6-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="01cb6-186">Kliknij przycisk **usług sieci WEB** w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="01cb6-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="01cb6-187">Kliknij przycisk hello **usługi sieci web uczenie** liście hello usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="01cb6-188">Kliknij przycisk Kopiuj obok zbyt**klucz interfejsu API** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="01cb6-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="01cb6-189">Wklej klucz hello hello Schowka do edytora JSON fabryki danych hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="01cb6-190">W hello **Azure ML studio**, kliknij przycisk **BATCH EXECUTION** łącza.</span><span class="sxs-lookup"><span data-stu-id="01cb6-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="01cb6-191">Kopiuj hello **przez identyfikator URI żądania** z hello **żądania** sekcji i wklej go do edytora JSON fabryki danych hello.</span><span class="sxs-lookup"><span data-stu-id="01cb6-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="01cb6-192">Połączonej usługi uczenie Maszynowe Azure punktu końcowego oceniania nadaje się do aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="01cb6-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="01cb6-193">powitania po fragment kodu JSON definiuje usługę Azure Machine Learning połączone, wskazujące toohello innych niż domyślne można aktualizować punkt końcowy hello oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="01cb6-194">Symbol zastępczy wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="01cb6-194">Placeholder output dataset:</span></span>
<span data-ttu-id="01cb6-195">Hello działania usługi Azure ML aktualizacji zasobów nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="01cb6-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="01cb6-196">Fabryka danych Azure wymaga jednak wyjściowego zestawu danych toodrive hello harmonogram potoku.</span><span class="sxs-lookup"><span data-stu-id="01cb6-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="01cb6-197">W związku z tym używamy zestawu manekina/symbol zastępczy danych, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="01cb6-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="01cb6-198">Potok</span><span class="sxs-lookup"><span data-stu-id="01cb6-198">Pipeline</span></span>
<span data-ttu-id="01cb6-199">potok Hello ma dwa działania: **AzureMLBatchExecution** i **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="01cb6-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="01cb6-200">Witaj działanie wykonywania wsadowego usługi uczenie Maszynowe Azure pobiera dane szkoleniowe hello jako dane wejściowe i tworzy plik iLearner jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="01cb6-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="01cb6-201">działanie Hello wywołuje usługę sieci web szkolenia hello (eksperyment uczenia udostępniony jako usługa sieci web) przy użyciu danych wejściowych hello szkolenia danych i odbiera plik ilearner hello z hello Usługa sieci Web.</span><span class="sxs-lookup"><span data-stu-id="01cb6-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="01cb6-202">Hello placeholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez hello fabryki danych Azure usługa toorun hello potoku.</span><span class="sxs-lookup"><span data-stu-id="01cb6-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

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
