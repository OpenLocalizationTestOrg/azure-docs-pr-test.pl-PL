---
title: "aaaBuild pierwszy fabryki danych (szablonu usługi Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym samouczku przedstawiono tworzenie przykładowego potoku usługi Azure Data Factory przy użyciu szablonu usługi Azure Resource Manager."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="9c0e1-103">Samouczek: tworzenie pierwszej fabryki danych Azure przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9c0e1-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c0e1-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c0e1-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="9c0e1-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9c0e1-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="9c0e1-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c0e1-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="9c0e1-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c0e1-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="9c0e1-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9c0e1-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="9c0e1-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="9c0e1-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="9c0e1-110">W tym artykule używamy toocreate szablonu usługi Azure Resource Manager Twojego pierwszego fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="9c0e1-111">Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="9c0e1-112">Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="9c0e1-113">To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="9c0e1-114">potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="9c0e1-115">Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="9c0e1-116">Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="9c0e1-117">Witaj potoku, w tym samouczku jest tylko jedno działanie typu: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="9c0e1-118">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9c0e1-119">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9c0e1-120">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9c0e1-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c0e1-121">Prerequisites</span></span>
* <span data-ttu-id="9c0e1-122">Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="9c0e1-123">Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu tooinstall najnowszą wersję programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="9c0e1-124">Zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md) toolearn informacje o szablonach usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="9c0e1-125">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="9c0e1-125">In this tutorial</span></span>
| <span data-ttu-id="9c0e1-126">Jednostka</span><span class="sxs-lookup"><span data-stu-id="9c0e1-126">Entity</span></span> | <span data-ttu-id="9c0e1-127">Opis</span><span class="sxs-lookup"><span data-stu-id="9c0e1-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c0e1-128">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c0e1-128">Azure Storage linked service</span></span> |<span data-ttu-id="9c0e1-129">Łączy fabrykę danych toohello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="9c0e1-130">blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="9c0e1-131">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="9c0e1-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="9c0e1-132">Łącza fabrykę danych toohello klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="9c0e1-133">Hello klastra jest automatycznie tworzony tooprocess danych i zostaną usunięte po ukończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="9c0e1-134">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c0e1-134">Azure Blob input dataset</span></span> |<span data-ttu-id="9c0e1-135">Odwołuje się toohello połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="9c0e1-136">Witaj połączonej usługi odwołuje się tooan konta magazynu Azure i zestawu danych obiektów Blob Azure hello Określa kontener hello, folder i nazwę pliku w magazynie hello, która przechowuje dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="9c0e1-137">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c0e1-137">Azure Blob output dataset</span></span> |<span data-ttu-id="9c0e1-138">Odwołuje się toohello połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="9c0e1-139">Witaj połączonej usługi odwołuje się tooan konta magazynu Azure i zestawu danych obiektów Blob Azure hello Określa kontener hello, folder i nazwę pliku w magazynie hello, która przechowuje dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="9c0e1-140">Potok danych</span><span class="sxs-lookup"><span data-stu-id="9c0e1-140">Data pipeline</span></span> |<span data-ttu-id="9c0e1-141">potok Hello ma jedno działanie typu HDInsightHive, który zużywa hello wejściowy zestaw danych i tworzy hello wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="9c0e1-142">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="9c0e1-143">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="9c0e1-144">Istnieją dwa typy działań: [przenoszenia danych](data-factory-data-movement-activities.md) i [przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="9c0e1-145">W tym samouczku tworzony jest potok z jednym działaniem (Działanie programu Hive).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="9c0e1-146">Witaj poniższej sekcji przedstawiono hello pełną szablonu usługi Resource Manager do definiowania jednostek fabryki danych, aby szybko uruchomić przy użyciu szablonu hello hello samouczek i testowania.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="9c0e1-147">toounderstand każdy obiekt fabryki danych jest zdefiniowany, zobacz [jednostek fabryki danych w szablonie hello](#data-factory-entities-in-the-template) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="9c0e1-148">Szablon JSON usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="9c0e1-148">Data Factory JSON template</span></span>
<span data-ttu-id="9c0e1-149">Witaj najwyższego poziomu szablonu usługi Resource Manager do definiowania fabryki danych jest:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
<span data-ttu-id="9c0e1-150">Utwórz plik JSON o nazwie **ADFTutorialARM.json** w **C:\ADFGetStarted** folder o hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="9c0e1-151">Temat [Samouczek: Tworzenie potoku za pomocą działania kopiowania przy użyciu szablonu usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) zawiera kolejny przykład szablonu usługi Resource Manager umożliwiającego utworzenie fabryki danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="9c0e1-152">Parametry JSON</span><span class="sxs-lookup"><span data-stu-id="9c0e1-152">Parameters JSON</span></span>
<span data-ttu-id="9c0e1-153">Utwórz plik JSON o nazwie **parameters.JSON następującym kodem ADFTutorialARM** zawierający parametry szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="9c0e1-154">Określ nazwę hello oraz klucz konta magazynu Azure hello **storageAccountName** i **storageAccountKey** parametrów w tym pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="9c0e1-155">Może mieć osobny parametr pliki w formacie JSON do tworzenia, testowania i środowiska produkcyjnego, w których można używać z hello tego samego szablonu JSON fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="9c0e1-156">Za pomocą skryptu programu Power Shell można zautomatyzować wdrażanie jednostek usługi Data Factory w tych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="9c0e1-157">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="9c0e1-157">Create data factory</span></span>
1. <span data-ttu-id="9c0e1-158">Uruchom **programu Azure PowerShell** i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="9c0e1-159">Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="9c0e1-160">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="9c0e1-161">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="9c0e1-162">Ta subskrypcja powinien Witaj, taka sama, jak hello jedną używaną w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="9c0e1-163">Uruchom powitania po jednostek fabryki danych toodeploy polecenia przy użyciu szablonu usługi Resource Manager hello utworzonego w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="9c0e1-164">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="9c0e1-164">Monitor pipeline</span></span>
1. <span data-ttu-id="9c0e1-165">Po zalogowaniu toohello [portalu Azure](https://portal.azure.com/), kliknij przycisk **Przeglądaj** i wybierz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="9c0e1-166">![Przeglądaj->Fabryki danych](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="9c0e1-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="9c0e1-167">W hello **fabryki danych** bloku, kliknij przycisk fabryki danych hello (**TutorialFactoryARM**) utworzony.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="9c0e1-168">W hello **fabryki danych** bloku fabrykę danych, kliknij przycisk **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Kafelek diagramu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="9c0e1-170">W hello **widoku diagramu**, zobacz Omówienie potoki hello i używać zestawów danych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Widok diagramu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="9c0e1-172">Hello widoku diagramu, kliknij dwukrotnie hello dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="9c0e1-173">Użytkownik widzi tego hello wycinek, który jest obecnie przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="9c0e1-175">Po zakończeniu przetwarzania zostanie wyświetlony wycinek hello **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="9c0e1-176">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="9c0e1-177">W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="9c0e1-179">Gdy wycinek hello jest **gotowe** stanu, należy sprawdzić hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="9c0e1-180">Zobacz [monitorowanie zestawów danych i potoku](data-factory-monitor-manage-pipelines.md) instrukcje dotyczące sposobu toouse hello Azure bloki portalu toomonitor hello potoku i zestawy danych zostały utworzone w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="9c0e1-181">Umożliwia także monitora i zarządzanie aplikacjami toomonitor Twojego potokach danych.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="9c0e1-182">Zobacz [monitorowanie i zarządzanie nimi przy użyciu monitorowania aplikacji potoki fabryki danych Azure](data-factory-monitor-manage-app.md) szczegóły dotyczące używania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9c0e1-183">Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="9c0e1-184">W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="9c0e1-185">Obiekty fabryki danych w szablonie hello</span><span class="sxs-lookup"><span data-stu-id="9c0e1-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="9c0e1-186">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="9c0e1-186">Define data factory</span></span>
<span data-ttu-id="9c0e1-187">Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="9c0e1-188">Hello dataFactoryName jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="9c0e1-189">Jest to unikatowy ciąg na podstawie identyfikatora hello zasobów grupy.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="9c0e1-190">Definiowanie jednostek usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="9c0e1-190">Defining Data Factory entities</span></span>
<span data-ttu-id="9c0e1-191">Hello następujące jednostek fabryki danych są definiowane w szablonie JSON hello:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="9c0e1-192">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c0e1-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="9c0e1-193">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="9c0e1-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="9c0e1-194">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c0e1-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="9c0e1-195">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c0e1-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="9c0e1-196">Potok danych z działaniem kopiowania</span><span class="sxs-lookup"><span data-stu-id="9c0e1-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="9c0e1-197">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9c0e1-197">Azure Storage linked service</span></span>
<span data-ttu-id="9c0e1-198">W tej sekcji można określić nazwę hello i klucza konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="9c0e1-199">Zobacz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="9c0e1-200">Witaj **connectionString** używa hello parametry storageAccountName i storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="9c0e1-201">Hello wartości tych parametrów przekazane za pomocą pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="9c0e1-202">Definicja Hello również używa zmiennych: azureStroageLinkedService i dataFactoryName zdefiniowane w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="9c0e1-203">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="9c0e1-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="9c0e1-204">Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artykuł szczegółowe informacje o toodefine właściwości używane w formacie JSON na żądanie połączoną usługą usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="9c0e1-205">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-205">Note hello following points:</span></span> 

* <span data-ttu-id="9c0e1-206">Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello powyżej JSON.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="9c0e1-207">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="9c0e1-208">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="9c0e1-209">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="9c0e1-210">Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="9c0e1-211">Po usunięciu klastra hello HDInsight nie usunie tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="9c0e1-212">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-212">This behavior is by design.</span></span> <span data-ttu-id="9c0e1-213">Z usługą HDInsight połączony na żądanie, klastra usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="9c0e1-214">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="9c0e1-215">Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="9c0e1-216">nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="9c0e1-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="9c0e1-217">Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="9c0e1-218">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="9c0e1-219">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c0e1-219">Azure blob input dataset</span></span>
<span data-ttu-id="9c0e1-220">Należy określić nazwy hello folder, plik zawierający dane wejściowe hello i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="9c0e1-221">Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="9c0e1-222">Ta definicja używa następujących parametrów zdefiniowanych w szablonie parametru hello: blobContainer, inputBlobFolder i inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="9c0e1-223">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9c0e1-223">Azure Blob output dataset</span></span>
<span data-ttu-id="9c0e1-224">Należy określić nazwy hello kontenera obiektów blob i folderu, która przechowuje dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="9c0e1-225">Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9c0e1-226">Ta definicja używa następujących parametrów zdefiniowanych w szablonie parametru hello hello: blobContainer i outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="9c0e1-227">Potok danych</span><span class="sxs-lookup"><span data-stu-id="9c0e1-227">Data pipeline</span></span>
<span data-ttu-id="9c0e1-228">Definiuje się potok przekształcający dane za pomocą skryptu Hive uruchamianego w klastrze usługi Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="9c0e1-229">Zobacz [JSON potoku](data-factory-create-pipelines.md#pipeline-json) opisy toodefine elementów JSON potoku, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a><span data-ttu-id="9c0e1-230">Ponowne użycie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="9c0e1-230">Reuse hello template</span></span>
<span data-ttu-id="9c0e1-231">W samouczku hello utworzony szablon do definiowania jednostek fabryki danych i przekazywanie wartości parametrów szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="9c0e1-232">toouse hello tego samego szablonu toodeploy fabryki danych jednostek toodifferent środowiskach, Utwórz plik parametr dla każdego środowiska i użyć go w przypadku wdrażania środowiska toothat.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="9c0e1-233">Przykład:</span><span class="sxs-lookup"><span data-stu-id="9c0e1-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="9c0e1-234">Należy zauważyć, że pierwszy parametr używa polecenia hello plik hello Środowisko deweloperskie, drugi dla środowiska testowego hello i hello trzeci co w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="9c0e1-235">Można również ponownie użyć tooperform szablonu hello powtarzanych zadań.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="9c0e1-236">Na przykład należy toocreate wiele fabryk danych z jednego lub więcej potoki, które implementują hello samej logiki, ale każdy inny magazynu Azure danych fabryki używa i konta bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="9c0e1-237">W tym scenariuszu, należy użyć hello tego samego szablonu hello — w tym samym środowisku (deweloperów, testów lub produkcji) z innym parametrem pliki toocreate fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="9c0e1-238">Szablon usługi Resource Manager do tworzenia bramy</span><span class="sxs-lookup"><span data-stu-id="9c0e1-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="9c0e1-239">Poniżej przedstawiono szablon usługi Resource Manager próbki do tworzenia logicznej bramy w hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="9c0e1-240">Zainstaluj bramę na komputerze lokalnym lub maszyny Wirtualnej Azure IaaS i zarejestruj bramę hello usłudze fabryka danych przy użyciu klucza.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="9c0e1-241">Szczegółowe informacje znajdują się w artykule [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) (Przenoszenie danych między komputerem lokalnym i chmurą).</span><span class="sxs-lookup"><span data-stu-id="9c0e1-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="9c0e1-242">Ten szablon służy do tworzenia fabryki danych o nazwie GatewayUsingArmDF z bramą o nazwie: GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="9c0e1-243">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9c0e1-243">See Also</span></span>
| <span data-ttu-id="9c0e1-244">Temat</span><span class="sxs-lookup"><span data-stu-id="9c0e1-244">Topic</span></span> | <span data-ttu-id="9c0e1-245">Opis</span><span class="sxs-lookup"><span data-stu-id="9c0e1-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="9c0e1-246">Potoki</span><span class="sxs-lookup"><span data-stu-id="9c0e1-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="9c0e1-247">Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="9c0e1-248">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="9c0e1-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="9c0e1-249">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="9c0e1-250">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="9c0e1-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="9c0e1-251">W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="9c0e1-252">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="9c0e1-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="9c0e1-253">W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9c0e1-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

