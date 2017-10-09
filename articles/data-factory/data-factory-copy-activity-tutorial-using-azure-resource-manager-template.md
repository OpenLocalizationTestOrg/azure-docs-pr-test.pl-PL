---
title: "Samouczek: Tworzenie potoku przy użyciu szablonu usługi Resource Manager | Microsoft Docs"
description: "W tym samouczku przedstawiono tworzenie potoku usługi Azure Data Factory przy użyciu szablonu usługi Azure Resource Manager. Tego potoku kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="66295-104">Samouczek: Użyj Menedżera zasobów Azure szablonu toocreate danych toocopy potoku fabryki danych</span><span class="sxs-lookup"><span data-stu-id="66295-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66295-105">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="66295-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="66295-106">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="66295-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="66295-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="66295-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="66295-108">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66295-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="66295-109">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="66295-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="66295-110">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66295-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="66295-111">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="66295-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="66295-112">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="66295-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="66295-113">W tym samouczku przedstawiono sposób toouse toocreate szablonu usługi Azure Resource Manager fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="66295-114">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="66295-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="66295-115">Przekształca dane wyjściowe tooproduce danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="66295-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="66295-116">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="66295-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="66295-117">W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania).</span><span class="sxs-lookup"><span data-stu-id="66295-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="66295-118">działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane.</span><span class="sxs-lookup"><span data-stu-id="66295-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="66295-119">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="66295-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="66295-120">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="66295-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="66295-121">Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="66295-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="66295-122">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="66295-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="66295-123">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="66295-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="66295-124">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="66295-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="66295-125">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="66295-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="66295-126">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="66295-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="66295-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="66295-127">Prerequisites</span></span>
* <span data-ttu-id="66295-128">Przejdź przez [samouczek omówienie i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="66295-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="66295-129">Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu tooinstall najnowszą wersję programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="66295-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="66295-130">W tym samouczku używamy jednostek fabryki danych toodeploy środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66295-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="66295-131">(opcjonalnie) Zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md) toolearn informacje o szablonach usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="66295-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="66295-132">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="66295-132">In this tutorial</span></span>
<span data-ttu-id="66295-133">W tym samouczku tworzenie fabryki danych z powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="66295-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="66295-134">Jednostka</span><span class="sxs-lookup"><span data-stu-id="66295-134">Entity</span></span> | <span data-ttu-id="66295-135">Opis</span><span class="sxs-lookup"><span data-stu-id="66295-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66295-136">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="66295-136">Azure Storage linked service</span></span> |<span data-ttu-id="66295-137">Łączy fabrykę danych toohello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="66295-138">Usługa Azure Storage jest hello źródła danych magazynu i bazy danych Azure SQL jest magazynem danych zbiornika powitania dla aktywności kopiowania hello w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="66295-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="66295-139">Określa konto magazynu hello zawierający hello danych wejściowych dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="66295-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="66295-140">Połączona usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="66295-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="66295-141">Łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="66295-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="66295-142">Określa bazy danych Azure SQL hello przechowujący hello danych wyjściowych dla działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="66295-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="66295-143">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="66295-143">Azure Blob input dataset</span></span> |<span data-ttu-id="66295-144">Odwołuje się toohello połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="66295-145">Witaj połączonej usługi odwołuje się tooan konta magazynu Azure i zestawu danych obiektów Blob Azure hello Określa kontener hello, folder i nazwę pliku w magazynie hello, która przechowuje dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="66295-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="66295-146">Wyjściowy zestaw danych usługi Azure SQL</span><span class="sxs-lookup"><span data-stu-id="66295-146">Azure SQL output dataset</span></span> |<span data-ttu-id="66295-147">Odwołuje się toohello Azure połączoną usługą SQL.</span><span class="sxs-lookup"><span data-stu-id="66295-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="66295-148">Hello Azure połączoną usługą SQL odwołuje się tooan serwera Azure SQL i zestawu danych Azure SQL hello Określa nazwę hello hello tabeli, która przechowuje dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="66295-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="66295-149">Potok danych</span><span class="sxs-lookup"><span data-stu-id="66295-149">Data pipeline</span></span> |<span data-ttu-id="66295-150">potok Hello ma jedno działanie typu kopii, która przyjmuje jako dane wejściowe, zestawu danych obiektów blob platformy Azure hello i hello zestawu danych Azure SQL jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="66295-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="66295-151">działanie kopiowania Hello kopiuje dane z tabeli w bazie danych Azure SQL hello tooa obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="66295-152">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="66295-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="66295-153">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="66295-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="66295-154">Istnieją dwa typy działań: [przenoszenia danych](data-factory-data-movement-activities.md) i [przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="66295-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="66295-155">W tym samouczku jest tworzony potok z jednym działaniem (kopiowania).</span><span class="sxs-lookup"><span data-stu-id="66295-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Kopiowanie obiektów Blob platformy Azure tooAzure bazy danych SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="66295-157">Witaj poniższej sekcji przedstawiono hello pełną szablonu usługi Resource Manager do definiowania jednostek fabryki danych, aby szybko uruchomić przy użyciu szablonu hello hello samouczek i testowania.</span><span class="sxs-lookup"><span data-stu-id="66295-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="66295-158">toounderstand każdy obiekt fabryki danych jest zdefiniowany, zobacz [jednostek fabryki danych w szablonie hello](#data-factory-entities-in-the-template) sekcji.</span><span class="sxs-lookup"><span data-stu-id="66295-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="66295-159">Szablon JSON usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="66295-159">Data Factory JSON template</span></span>
<span data-ttu-id="66295-160">Witaj najwyższego poziomu szablonu usługi Resource Manager do definiowania fabryki danych jest:</span><span class="sxs-lookup"><span data-stu-id="66295-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="66295-161">Utwórz plik JSON o nazwie **ADFCopyTutorialARM.json** w **C:\ADFGetStarted** folder o hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="66295-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob tooAzure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="66295-162">Parametry JSON</span><span class="sxs-lookup"><span data-stu-id="66295-162">Parameters JSON</span></span>
<span data-ttu-id="66295-163">Utwórz plik JSON o nazwie **parameters.JSON następującym kodem ADFCopyTutorialARM** zawierający parametry szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="66295-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="66295-164">Określ nazwę i klucz konta usługi Azure Storage za pomocą parametrów storageAccountName i storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="66295-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="66295-165">Określ serwer SQL na platformie Azure, bazę danych, użytkownika i hasło w parametrach sqlServerName, databaseName, sqlServerUserName oraz sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="66295-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="66295-166">Może mieć osobny parametr pliki w formacie JSON do tworzenia, testowania i środowiska produkcyjnego, w których można używać z hello tego samego szablonu JSON fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="66295-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="66295-167">Za pomocą skryptu programu Power Shell można zautomatyzować wdrażanie jednostek usługi Data Factory w tych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="66295-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="66295-168">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="66295-168">Create data factory</span></span>
1. <span data-ttu-id="66295-169">Uruchom **programu Azure PowerShell** i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="66295-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="66295-170">Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="66295-171">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="66295-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="66295-172">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="66295-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="66295-173">Uruchom powitania po jednostek fabryki danych toodeploy polecenia przy użyciu szablonu usługi Resource Manager hello utworzonego w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="66295-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="66295-174">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="66295-174">Monitor pipeline</span></span>

1. <span data-ttu-id="66295-175">Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="66295-176">Kliknij przycisk **fabryki danych** hello lewym menu (lub) kliknij **więcej usług** i kliknij przycisk **fabryki danych** w obszarze **analizy i analiza** Kategoria.</span><span class="sxs-lookup"><span data-stu-id="66295-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menu fabryk danych](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="66295-178">W hello **fabryki danych** strony, wyszukiwanie i Znajdź fabrykę danych (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="66295-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Wyszukiwanie fabryki danych](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="66295-180">Kliknij fabrykę danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-180">Click your Azure data factory.</span></span> <span data-ttu-id="66295-181">Zostanie wyświetlona strona główna hello hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="66295-181">You see hello home page for hello data factory.</span></span>
   
    ![Strona główna fabryki danych](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="66295-183">Postępuj zgodnie z instrukcjami [monitorowanie zestawów danych i potoku](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello potoku i zestawy danych zostały utworzone w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="66295-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="66295-184">Obecnie program Visual Studio nie obsługuje monitorowania potoków usługi Data Factory.</span><span class="sxs-lookup"><span data-stu-id="66295-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="66295-185">Gdy wycinek jest hello **gotowe** stanu, sprawdź, czy dane hello jest skopiowany toohello **pustych elementów** tabeli w bazie danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="66295-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="66295-186">Aby uzyskać więcej informacji o jak toouse bloków portalu Azure toomonitor potoku i zestawy danych zostały utworzone w tym samouczku, zobacz [monitorowanie zestawów danych i potoku](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="66295-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="66295-187">Aby uzyskać więcej informacji dotyczących sposobu toouse hello Monitor & Zarządzaj aplikacji toomonitor danych potoków, zobacz [monitorowanie i zarządzanie nimi przy użyciu monitorowania aplikacji potoki fabryki danych Azure](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="66295-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="66295-188">Obiekty fabryki danych w szablonie hello</span><span class="sxs-lookup"><span data-stu-id="66295-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="66295-189">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="66295-189">Define data factory</span></span>
<span data-ttu-id="66295-190">Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="66295-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="66295-191">Hello dataFactoryName jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="66295-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="66295-192">Jest to unikatowy ciąg na podstawie identyfikatora hello zasobów grupy.</span><span class="sxs-lookup"><span data-stu-id="66295-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="66295-193">Definiowanie jednostek usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="66295-193">Defining Data Factory entities</span></span>
<span data-ttu-id="66295-194">Hello następujące jednostek fabryki danych są definiowane w szablonie JSON hello:</span><span class="sxs-lookup"><span data-stu-id="66295-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="66295-195">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="66295-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="66295-196">Połączona usługa Azure SQL</span><span class="sxs-lookup"><span data-stu-id="66295-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="66295-197">Zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="66295-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="66295-198">Zestaw danych usługi Azure SQL</span><span class="sxs-lookup"><span data-stu-id="66295-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="66295-199">Potok danych z działaniem kopiowania</span><span class="sxs-lookup"><span data-stu-id="66295-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="66295-200">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="66295-200">Azure Storage linked service</span></span>
<span data-ttu-id="66295-201">Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="66295-202">Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="66295-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="66295-203">W tej sekcji można określić nazwę hello i klucza konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="66295-204">Zobacz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="66295-205">Hello connectionString używa parametrów storageAccountName i storageAccountKey hello.</span><span class="sxs-lookup"><span data-stu-id="66295-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="66295-206">Hello wartości tych parametrów przekazane za pomocą pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="66295-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="66295-207">Definicja Hello również używa zmiennych: azureStroageLinkedService i dataFactoryName zdefiniowane w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="66295-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="66295-208">Połączona usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="66295-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="66295-209">AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="66295-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="66295-210">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="66295-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="66295-211">Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="66295-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="66295-212">W tej sekcji można określić nazwy serwera Azure SQL hello, nazwa bazy danych, nazwę użytkownika i hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="66295-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="66295-213">Zobacz [Azure SQL połączona usługa](data-factory-azure-sql-connector.md#linked-service-properties) szczegółowe informacje o toodefine właściwości używane w formacie JSON Azure SQL połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="66295-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="66295-214">Witaj connectionString używa sqlServerName, databaseName sqlServerUserName i sqlServerPassword parametry, których wartości są przekazywane za pomocą pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="66295-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="66295-215">Witaj definicji używa również następujące zmienne z szablonu hello hello: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="66295-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="66295-216">Zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="66295-216">Azure blob dataset</span></span>
<span data-ttu-id="66295-217">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="66295-218">W definicji zestawu danych obiektów blob platformy Azure należy określić nazwy kontenera obiektów blob, folderu i pliku zawierającego dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="66295-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="66295-219">Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="66295-220">Zestaw danych usługi Azure SQL</span><span class="sxs-lookup"><span data-stu-id="66295-220">Azure SQL dataset</span></span>
<span data-ttu-id="66295-221">Należy określić nazwę hello hello tabeli w bazie danych Azure SQL hello przechowujący dane hello skopiowane z hello magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66295-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="66295-222">Zobacz [właściwości zestawu danych Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawem danych usługi Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="66295-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="66295-223">Potok danych</span><span class="sxs-lookup"><span data-stu-id="66295-223">Data pipeline</span></span>
<span data-ttu-id="66295-224">Należy zdefiniować potok, który kopiuje dane z zestawu danych Azure SQL toohello hello obiektów blob platformy Azure zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="66295-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="66295-225">Zobacz [JSON potoku](data-factory-create-pipelines.md#pipeline-json) opisy toodefine elementów JSON potoku, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="66295-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob tooAzure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-hello-template"></a><span data-ttu-id="66295-226">Ponowne użycie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="66295-226">Reuse hello template</span></span>
<span data-ttu-id="66295-227">W samouczku hello utworzony szablon do definiowania jednostek fabryki danych i przekazywanie wartości parametrów szablonu.</span><span class="sxs-lookup"><span data-stu-id="66295-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="66295-228">potok Hello kopiuje dane z usługi Azure Storage konta tooan bazy danych SQL Azure określona za pomocą parametrów.</span><span class="sxs-lookup"><span data-stu-id="66295-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="66295-229">toouse hello tego samego szablonu toodeploy fabryki danych jednostek toodifferent środowiskach, Utwórz plik parametr dla każdego środowiska i użyć go w przypadku wdrażania środowiska toothat.</span><span class="sxs-lookup"><span data-stu-id="66295-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="66295-230">Przykład:</span><span class="sxs-lookup"><span data-stu-id="66295-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="66295-231">Należy zauważyć, że pierwszy parametr używa polecenia hello plik hello Środowisko deweloperskie, drugi dla środowiska testowego hello i hello trzeci co w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="66295-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="66295-232">Można również ponownie użyć tooperform szablonu hello powtarzanych zadań.</span><span class="sxs-lookup"><span data-stu-id="66295-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="66295-233">Na przykład należy toocreate wiele fabryk danych z jednego lub więcej potoki, które implementują hello sama logika, ale każdej fabryki danych używa innego konta magazynu i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="66295-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="66295-234">W tym scenariuszu, należy użyć hello tego samego szablonu hello — w tym samym środowisku (deweloperów, testów lub produkcji) z innym parametrem pliki toocreate fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="66295-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="66295-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="66295-235">Next steps</span></span>
<span data-ttu-id="66295-236">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="66295-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="66295-237">Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello:</span><span class="sxs-lookup"><span data-stu-id="66295-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="66295-238">toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="66295-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
