---
title: "Tworzenie pierwszej fabryki danych (szablon usługi Resource Manager) | Microsoft Docs"
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
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="d4ef0-103">Samouczek: tworzenie pierwszej fabryki danych Azure przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d4ef0-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4ef0-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d4ef0-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="d4ef0-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4ef0-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="d4ef0-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4ef0-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="d4ef0-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4ef0-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="d4ef0-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d4ef0-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="d4ef0-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d4ef0-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="d4ef0-110">W tym artykule opisano użycie szablonu usługi Azure Resource Manager do tworzenia pierwszej fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="d4ef0-111">Aby wykonać instrukcje z tego samouczka przy użyciu innych narzędzi/zestawów SDK, wybierz jedną z opcji z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="d4ef0-112">Potok w tym samouczku zawiera jedno działanie: **działanie Hive usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="d4ef0-113">To działanie uruchamia skrypt Hive w klastrze Azure HDInsight, który przekształca dane wejściowe, aby wygenerować dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="d4ef0-114">Uruchamianie potoku zaplanowano raz w miesiącu między określonym czasem rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4ef0-115">Potok danych przedstawiony w tym samouczku przekształca dane wejściowe w celu wygenerowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="d4ef0-116">Aby zapoznać się z samouczkiem dotyczącym kopiowania danych przy użyciu usługi Azure Data Factory, zobacz [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) (Samouczek: Kopiowanie danych z usługi Blob Storage do usługi SQL Database).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="d4ef0-117">Potok w tym samouczku zawiera tylko jedno działanie typu: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="d4ef0-118">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="d4ef0-119">Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="d4ef0-120">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d4ef0-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d4ef0-121">Prerequisites</span></span>
* <span data-ttu-id="d4ef0-122">Przeczytanie artykułu [Omówienie samouczka](data-factory-build-your-first-pipeline.md) oraz wykonanie kroków **wymagań wstępnych**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="d4ef0-123">Postępuj zgodnie z instrukcjami w artykule [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell), aby zainstalować najnowszą wersję programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="d4ef0-124">Artykuł [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) (Tworzenie szablonów usługi Azure Resource Manager) zawiera informacje dotyczące szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="d4ef0-125">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="d4ef0-125">In this tutorial</span></span>
| <span data-ttu-id="d4ef0-126">Jednostka</span><span class="sxs-lookup"><span data-stu-id="d4ef0-126">Entity</span></span> | <span data-ttu-id="d4ef0-127">Opis</span><span class="sxs-lookup"><span data-stu-id="d4ef0-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4ef0-128">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d4ef0-128">Azure Storage linked service</span></span> |<span data-ttu-id="d4ef0-129">Łączy konto usługi Azure Storage z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="d4ef0-130">Konto usługi Azure Storage będzie przechowywać dane wejściowe i wyjściowe dla potoku w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="d4ef0-131">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="d4ef0-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="d4ef0-132">Łączy klaster usługi HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="d4ef0-133">Klaster jest automatycznie tworzony na potrzeby przetwarzania danych i usuwany po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="d4ef0-134">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ef0-134">Azure Blob input dataset</span></span> |<span data-ttu-id="d4ef0-135">Przywołuje połączoną usługę Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="d4ef0-136">Połączona usługa przywołuje konto usługi Azure Storage, a zestaw danych obiektów blob platformy Azure określa kontener, folder i nazwę pliku w magazynie, który przechowuje dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="d4ef0-137">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ef0-137">Azure Blob output dataset</span></span> |<span data-ttu-id="d4ef0-138">Przywołuje połączoną usługę Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="d4ef0-139">Połączona usługa przywołuje konto usługi Azure Storage, a zestaw danych obiektów blob platformy Azure określa kontener, folder i nazwę pliku w magazynie, który przechowuje dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="d4ef0-140">Potok danych</span><span class="sxs-lookup"><span data-stu-id="d4ef0-140">Data pipeline</span></span> |<span data-ttu-id="d4ef0-141">Potok ma jedno działanie typu HDInsightHive, które zużywa wejściowy zestaw danych i tworzy wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="d4ef0-142">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="d4ef0-143">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="d4ef0-144">Istnieją dwa typy działań: [przenoszenia danych](data-factory-data-movement-activities.md) i [przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="d4ef0-145">W tym samouczku tworzony jest potok z jednym działaniem (Działanie programu Hive).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="d4ef0-146">W poniższej sekcji przedstawiono pełny szablon usługi Resource Manager umożliwiający definiowanie jednostek usługi Data Factory, dzięki czemu można szybko przejść przez samouczek i przetestować szablon.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="d4ef0-147">Aby dowiedzieć się, jak jest zdefiniowana każda jednostka usługi Data Factory, zobacz sekcję [Jednostki usługi Data Factory w szablonie](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="d4ef0-148">Szablon JSON usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="d4ef0-148">Data Factory JSON template</span></span>
<span data-ttu-id="d4ef0-149">Szablon najwyższego poziomu usługi Resource Manager umożliwiający zdefiniowanie fabryki danych to:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="d4ef0-150">Utwórz plik JSON o nazwie **ADFTutorialARM.json** w folderze **C:\ADFGetStarted** o następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
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
> <span data-ttu-id="d4ef0-151">Temat [Samouczek: Tworzenie potoku za pomocą działania kopiowania przy użyciu szablonu usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) zawiera kolejny przykład szablonu usługi Resource Manager umożliwiającego utworzenie fabryki danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="d4ef0-152">Parametry JSON</span><span class="sxs-lookup"><span data-stu-id="d4ef0-152">Parameters JSON</span></span>
<span data-ttu-id="d4ef0-153">Utwórz plik JSON o nazwie **ADFTutorialARM-Parameters.json** zawierający parametry szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d4ef0-154">Określ nazwę i klucz konta usługi Azure Storage w pliku parametrów za pomocą parametrów **storageAccountName** i **storageAccountKey**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="d4ef0-155">Można używać oddzielnych plików parametrów JSON dla środowisk programistycznego, testowego i produkcyjnego do użycia z tym samym szablonem JSON usługi Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="d4ef0-156">Za pomocą skryptu programu Power Shell można zautomatyzować wdrażanie jednostek usługi Data Factory w tych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="d4ef0-157">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="d4ef0-157">Create data factory</span></span>
1. <span data-ttu-id="d4ef0-158">Uruchom program **Azure PowerShell** i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="d4ef0-159">Uruchom poniższe polecenie i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="d4ef0-160">Uruchom poniższe polecenie, aby wyświetlić wszystkie subskrypcje dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="d4ef0-161">Uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="d4ef0-162">Ta subskrypcja powinna być taka sama jak używana w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="d4ef0-163">Uruchom następujące polecenie, aby wdrożyć jednostki usługi Data Factory przy użyciu szablonu usługi Resource Manager utworzonego w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="d4ef0-164">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="d4ef0-164">Monitor pipeline</span></span>
1. <span data-ttu-id="d4ef0-165">Po zalogowaniu się do witryny [Azure Portal](https://portal.azure.com/) kliknij przycisk **Przeglądaj** i wybierz opcję **Fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="d4ef0-166">![Przeglądaj->Fabryki danych](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="d4ef0-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="d4ef0-167">W bloku **Fabryki danych** kliknij utworzoną przez siebie fabrykę danych (**TutorialFactoryARM**).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="d4ef0-168">W bloku **Fabryka danych** dla swojej fabryki danych kliknij opcję **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Kafelek diagramu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="d4ef0-170">Na stronie **Widok diagramu** zostanie wyświetlony przegląd potoków i zestawów danych używanych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Widok diagramu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="d4ef0-172">Na stronie Widok diagramu kliknij dwukrotnie zestaw danych **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="d4ef0-173">Zostanie wyświetlony wycinek, który jest obecnie przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-173">You see that the slice that is currently being processed.</span></span>
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="d4ef0-175">Po zakończeniu przetwarzania wycinek będzie mieć stan **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="d4ef0-176">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="d4ef0-177">Dlatego należy oczekiwać, że przetworzenie wycinka przez potok zajmie **około 30 minut**.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="d4ef0-179">Gdy wycinek będzie w stanie **Gotowe**, sprawdź folder **partitioneddata** w kontenerze **adfgetstarted** w magazynie obiektów blob pod kątem danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="d4ef0-180">Zobacz artykuł [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) (Monitorowanie zestawów danych i potoku), aby uzyskać instrukcje dotyczące korzystania z bloków w witrynie Azure Portal w celu monitorowania potoku i zestawów danych utworzonych przez siebie w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="d4ef0-181">Do monitorowania potoków danych możesz też użyć aplikacji Monitorowanie i zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="d4ef0-182">Szczegółowe informacje dotyczące korzystania z aplikacji znajdują się w artykule [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) (Monitorowanie potoków usługi Fabryka danych Azure oraz zarządzanie nimi za pomocą aplikacji do monitorowania).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4ef0-183">Po pomyślnym przetworzeniu wycinka plik wejściowy zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="d4ef0-184">Tak więc, jeśli chcesz ponownie uruchomić wycinek lub ponownie wykonać instrukcje z tego samouczka, przekaż plik wejściowy (input.log) do folderu inputdata kontenera adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="d4ef0-185">Jednostki usługi Data Factory w szablonie</span><span class="sxs-lookup"><span data-stu-id="d4ef0-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="d4ef0-186">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="d4ef0-186">Define data factory</span></span>
<span data-ttu-id="d4ef0-187">Fabrykę danych definiuje się w szablonie usługi Resource Manager jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="d4ef0-188">Parametr dataFactoryName jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="d4ef0-189">To jest unikatowy ciąg oparty na identyfikatorze grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="d4ef0-190">Definiowanie jednostek usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="d4ef0-190">Defining Data Factory entities</span></span>
<span data-ttu-id="d4ef0-191">Następujące jednostki usługi Data Factory są zdefiniowane w szablonie JSON:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="d4ef0-192">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d4ef0-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="d4ef0-193">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="d4ef0-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="d4ef0-194">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ef0-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="d4ef0-195">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ef0-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="d4ef0-196">Potok danych z działaniem kopiowania</span><span class="sxs-lookup"><span data-stu-id="d4ef0-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d4ef0-197">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d4ef0-197">Azure Storage linked service</span></span>
<span data-ttu-id="d4ef0-198">W tej sekcji określa się nazwę i klucz konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="d4ef0-199">Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure Storage zawiera temat [Połączona usługa Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="d4ef0-200">Parametr **connectionString** używa parametrów storageAccountName i storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="d4ef0-201">Wartości tych parametrów są przekazywane przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="d4ef0-202">Definicja używa także zmiennych azureStorageLinkedService i dataFactoryName zdefiniowanych w szablonie.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="d4ef0-203">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="d4ef0-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="d4ef0-204">Szczegółowe informacje o właściwościach JSON używanych do definiowania połączonej usługi HDInsight na żądanie zawiera temat [Usługi połączone usługi Compute](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="d4ef0-205">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-205">Note the following points:</span></span> 

* <span data-ttu-id="d4ef0-206">Usługa Data Factory tworzy klaster usługi HDInsight **oparty na systemie Linux** za pomocą powyższego kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="d4ef0-207">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="d4ef0-208">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d4ef0-209">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="d4ef0-210">Klaster usługi HDInsight tworzy **kontener domyślny** w magazynie obiektów blob określonym w kodzie JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="d4ef0-211">Usługa HDInsight nie powoduje usunięcia tego kontenera w przypadku usunięcia klastra.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="d4ef0-212">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-212">This behavior is by design.</span></span> <span data-ttu-id="d4ef0-213">W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony za każdym razem, gdy trzeba przetworzyć wycinek — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**) — i zostaje usunięty po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="d4ef0-214">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="d4ef0-215">Jeśli nie są potrzebne do rozwiązywania problemów z zadaniami, można je usunąć, aby zmniejszyć koszt przechowywania.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="d4ef0-216">Nazwy tych kontenerów są zgodne ze wzorcem: „adf**twojanazwafabrykidanych**-**nazwapołączonejusługi**-znacznikdatygodziny”.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="d4ef0-217">Aby usunąć kontenery z usługi Azure Blob Storage, użyj takich narzędzi, jak [Microsoft Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="d4ef0-218">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="d4ef0-219">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ef0-219">Azure blob input dataset</span></span>
<span data-ttu-id="d4ef0-220">Określane są nazwy kontenera obiektów blob, folderu i pliku, który zawiera dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="d4ef0-221">Szczegóły dotyczące właściwości JSON używanych do definiowania zestawu danych obiektów blob platformy Azure zawiera temat [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) (Właściwości zestawu danych obiektów blob plaformy Azure).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="d4ef0-222">Ta definicja wykorzystuje następujące parametry zdefiniowane w szablonie parametrów: blobContainer, inputBlobFolder i inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d4ef0-223">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4ef0-223">Azure Blob output dataset</span></span>
<span data-ttu-id="d4ef0-224">Określane są nazwy kontenera obiektów blob i folderu przechowującego dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="d4ef0-225">Szczegóły dotyczące właściwości JSON używanych do definiowania zestawu danych obiektów blob platformy Azure zawiera temat [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) (Właściwości zestawu danych obiektów blob plaformy Azure).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="d4ef0-226">Ta definicja wykorzystuje następujące parametry zdefiniowane w szablonie parametrów: blobContainer i outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="d4ef0-227">Potok danych</span><span class="sxs-lookup"><span data-stu-id="d4ef0-227">Data pipeline</span></span>
<span data-ttu-id="d4ef0-228">Definiuje się potok przekształcający dane za pomocą skryptu Hive uruchamianego w klastrze usługi Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="d4ef0-229">Opisy elementów JSON używanych do definiowania potoku w tym przykładzie zawiera temat [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) (Kod JSON potoku).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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

## <a name="reuse-the-template"></a><span data-ttu-id="d4ef0-230">Ponowne użycie szablonu</span><span class="sxs-lookup"><span data-stu-id="d4ef0-230">Reuse the template</span></span>
<span data-ttu-id="d4ef0-231">W ramach samouczka został utworzony szablon służący do definiowania jednostek usługi Data Factory i szablon służący do przekazywania wartości dla parametrów.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="d4ef0-232">Aby użyć tego samego szablonu do wdrożenia jednostek usługi Data Factory w różnych środowiskach, należy utworzyć plik parametrów dla każdego środowiska i użyć go podczas wdrażania do środowiska.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="d4ef0-233">Przykład:</span><span class="sxs-lookup"><span data-stu-id="d4ef0-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="d4ef0-234">Należy zauważyć, że pierwsze polecenie używa pliku parametrów dla środowiska programistycznego, drugie dla środowiska testowego, a trzecie dla środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="d4ef0-235">Można także ponownie użyć szablonu do wykonywania powtarzających się zadań.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="d4ef0-236">Na przykład w sytuacji, gdy jest potrzebne utworzenie wielu fabryk danych z co najmniej jednym potokiem, które implementują tę samą logikę, lecz każda fabryka danych używa innego magazynu platformy Azure i kont usługi Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="d4ef0-237">W tym scenariuszu do tworzenia fabryk danych jest używany ten sam szablon w tym samym środowisku (programistycznym, testowym lub produkcyjnym) w połączeniu z różnymi plikami parametrów.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="d4ef0-238">Szablon usługi Resource Manager do tworzenia bramy</span><span class="sxs-lookup"><span data-stu-id="d4ef0-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="d4ef0-239">Poniżej przedstawiono przykładowy szablon usługi Resource Manager do tworzenia logicznej bramy w tle.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="d4ef0-240">Zainstaluj bramę na komputerze lokalnym lub maszynie wirtualnej IaaS platformy Azure i zarejestruj bramę w usłudze Data Factory przy użyciu klucza.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="d4ef0-241">Szczegółowe informacje znajdują się w artykule [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) (Przenoszenie danych między komputerem lokalnym i chmurą).</span><span class="sxs-lookup"><span data-stu-id="d4ef0-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="d4ef0-242">Ten szablon służy do tworzenia fabryki danych o nazwie GatewayUsingArmDF z bramą o nazwie: GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="d4ef0-243">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d4ef0-243">See Also</span></span>
| <span data-ttu-id="d4ef0-244">Temat</span><span class="sxs-lookup"><span data-stu-id="d4ef0-244">Topic</span></span> | <span data-ttu-id="d4ef0-245">Opis</span><span class="sxs-lookup"><span data-stu-id="d4ef0-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="d4ef0-246">Potoki</span><span class="sxs-lookup"><span data-stu-id="d4ef0-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="d4ef0-247">Ten artykuł ułatwia zapoznanie się z potokami i działaniami w usłudze Azure Data Factory oraz ze sposobem konstruowania za ich pomocą przepływów pracy typu end-to-end opartych na danych na potrzeby scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="d4ef0-248">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="d4ef0-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="d4ef0-249">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="d4ef0-250">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="d4ef0-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="d4ef0-251">W tym artykule wyjaśniono aspekty planowania i wykonywania modelu aplikacji usługi Fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="d4ef0-252">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="d4ef0-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="d4ef0-253">Ten artykuł zawiera instrukcje dotyczące monitorowania i debugowania potoków oraz zarządzania nimi przy użyciu aplikacji do monitorowania i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d4ef0-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

