---
title: "szablony Menedżera zasobów aaaUse w fabryce danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i używanie usługi Azure Resource Manager szablony toocreate fabryki danych jednostki."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="0567d-103">Użyj jednostek fabryki danych Azure toocreate szablonów</span><span class="sxs-lookup"><span data-stu-id="0567d-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="0567d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0567d-104">Overview</span></span>
<span data-ttu-id="0567d-105">Podczas używania fabryki danych Azure potrzeby integracji danych może okazać się ponowne użycie hello tego samego wzorca różnych środowiskach lub implementacja hello samo zadanie kilkukrotnie w hello takie same rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0567d-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="0567d-106">Szablony ułatwiają wdrożenia i zarządzania tych scenariuszy w łatwy sposób.</span><span class="sxs-lookup"><span data-stu-id="0567d-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="0567d-107">Szablony w fabryce danych Azure idealnie nadają się do scenariusze, które obejmują możliwość ponownego wykorzystania i powtórzenia.</span><span class="sxs-lookup"><span data-stu-id="0567d-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="0567d-108">Należy wziąć pod uwagę hello sytuacji, gdy organizacja ma 10 zakładu produkcyjnego w hello world.</span><span class="sxs-lookup"><span data-stu-id="0567d-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="0567d-109">Dzienniki Hello z każdego zakładu są przechowywane w bazie danych programu SQL Server oddzielny lokalny.</span><span class="sxs-lookup"><span data-stu-id="0567d-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="0567d-110">Witaj firma chce toobuild magazynu danych w chmurze hello analizy ad hoc.</span><span class="sxs-lookup"><span data-stu-id="0567d-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="0567d-111">Chce ona również toohave hello samej logiki, ale różne konfiguracje dla środowiska deweloperskie, badanie i produkcji.</span><span class="sxs-lookup"><span data-stu-id="0567d-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="0567d-112">W takim przypadku zadania musi toobe powtarzany w tym samym środowisku Witaj, ale o różnych wartościach między hello 10 fabryk danych dla każdego zakładu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0567d-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="0567d-113">W efekcie **powtarzania** jest obecny.</span><span class="sxs-lookup"><span data-stu-id="0567d-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="0567d-114">Abstrakcja hello to ogólny przepływ umożliwia tworzenia szablonów (to znaczy potoków o hello tego samego działania z każdej fabryki danych), ale używa pliku osobny parametr dla każdego zakładu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0567d-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="0567d-115">Ponadto ponieważ hello obowiązującymi w organizacji toodeploy tych fabryk danych 10 wielokrotnie w różnych środowiskach, szablony, mogą używać tego **możliwość ponownego wykorzystania** przy użyciu plików osobny parametr do tworzenia aplikacji, przetestować, i środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="0567d-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="0567d-116">Tworzenia szablonów z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0567d-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="0567d-117">[Szablony usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) to doskonały sposób tworzenia ze tooachieve szablonów w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="0567d-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="0567d-118">Szablony Menedżera zasobów zdefiniuj hello infrastrukturze i konfiguracji rozwiązania Azure za pomocą pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="0567d-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="0567d-119">Ponieważ szablonów usługi Azure Resource Manager pracować z wszystkich/większość usług platformy Azure, powszechnie umożliwia tooeasily zarządzania wszystkie zasoby zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0567d-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="0567d-120">Zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) ogólnie hello toolearn więcej na temat szablonów Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0567d-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="0567d-121">Samouczki</span><span class="sxs-lookup"><span data-stu-id="0567d-121">Tutorials</span></span>
<span data-ttu-id="0567d-122">Zobacz następujące samouczki dla jednostek fabryki danych toocreate instrukcje krok po kroku przy użyciu szablonów usługi Resource Manager hello:</span><span class="sxs-lookup"><span data-stu-id="0567d-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="0567d-123">Samouczek: Tworzenie potoku toocopy danych przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0567d-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="0567d-124">Samouczek: Tworzenie potoku tooprocess danych przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0567d-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="0567d-125">Szablony fabryki danych w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="0567d-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="0567d-126">Wyewidencjonuj hello następujących szablonów szybki start Azure w serwisie GitHub:</span><span class="sxs-lookup"><span data-stu-id="0567d-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="0567d-127">Utwórz toocopy fabryka danych z magazynu obiektów Blob Azure tooAzure bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="0567d-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="0567d-128">Tworzenie fabryki danych działania Hive w usłudze Azure HDInsight klastra</span><span class="sxs-lookup"><span data-stu-id="0567d-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="0567d-129">Tworzenie z obiektów blob tooAzure Salesforce toocopy fabryki danych</span><span class="sxs-lookup"><span data-stu-id="0567d-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="0567d-130">Tworzenie fabryki danych, w którym jest powiązany działań: kopiuje dane z serwera FTP tooAzure obiektów blob, wywołuje skrypt hive na dane HDInsight hello tootransform klastra na żądanie i kopiuje wynik do bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0567d-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="0567d-131">Możesz wolnego tooshare szablonów fabryki danych Azure na [Azure szybki start](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="0567d-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="0567d-132">Zobacz toohello [przewodnik wkład](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) podczas tworzenia szablonów, które mogą być współużytkowane przez to repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0567d-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="0567d-133">Witaj następujące sekcje zawierają szczegółowe informacje o Definiowanie zasoby fabryki danych w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0567d-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="0567d-134">Definiowanie zasoby fabryki danych w szablonach</span><span class="sxs-lookup"><span data-stu-id="0567d-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="0567d-135">Witaj szablon najwyższego poziomu do definiowania fabryki danych jest:</span><span class="sxs-lookup"><span data-stu-id="0567d-135">hello top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="0567d-136">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="0567d-136">Define data factory</span></span>
<span data-ttu-id="0567d-137">Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="0567d-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="0567d-138">Hello dataFactoryName jest zdefiniowana w "zmiennych" jako:</span><span class="sxs-lookup"><span data-stu-id="0567d-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="0567d-139">Zdefiniuj połączone usługi</span><span class="sxs-lookup"><span data-stu-id="0567d-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="0567d-140">Zobacz [połączonej usługi magazynu](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [obliczeniowe połączonych usług](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) szczegółowe informacje na temat właściwości JSON hello hello określonych połączonej usługi mają toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0567d-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="0567d-141">Parametr "dependsOn" Hello Określa nazwę hello odpowiedniego fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0567d-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="0567d-142">Przykład Definiowanie połączonej usługi magazynu Azure znajduje się w następującej definicji JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0567d-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="0567d-143">Zdefiniuj zbiory danych</span><span class="sxs-lookup"><span data-stu-id="0567d-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="0567d-144">Odwołuje się zbyt[obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) szczegółowe informacje na temat właściwości JSON hello hello określonego zestawu danych typu mają toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0567d-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="0567d-145">Parametr "dependsOn" hello Uwaga Określa nazwę hello odpowiednie dane fabryki i magazynu połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="0567d-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="0567d-146">Przykład definiujący typ zestawu danych z magazynu obiektów blob Azure znajduje się w następującej definicji JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0567d-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="0567d-147">Zdefiniuj potoki</span><span class="sxs-lookup"><span data-stu-id="0567d-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="0567d-148">Odwołuje się zbyt[Definiowanie potoki](data-factory-create-pipelines.md#pipeline-json) dla szczegółowe informacje o właściwości JSON hello definiujące hello określonych potoku i działania mają toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0567d-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="0567d-149">Parametr "dependsOn" hello Uwaga określa nazwy fabryki danych hello oraz odpowiedni połączonych usług lub zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="0567d-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="0567d-150">Przykład potok, który kopiuje dane z magazynu obiektów Blob Azure tooAzure bazy danych SQL znajduje się w powitania po fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="0567d-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="0567d-151">Ustawianie szablonu usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="0567d-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="0567d-152">Najlepsze rozwiązania na ustawianie, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0567d-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="0567d-153">Ogólnie rzecz biorąc użycia parametru można zmniejszyć do minimum, zwłaszcza jeśli zmienne, które mogą być używane zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="0567d-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="0567d-154">Tylko podać parametry w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="0567d-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="0567d-155">Ustawienia zależą od środowiska (przykład: Programowanie, testowe i produkcyjne)</span><span class="sxs-lookup"><span data-stu-id="0567d-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="0567d-156">Klucze tajne (takie jak hasła)</span><span class="sxs-lookup"><span data-stu-id="0567d-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="0567d-157">Jeśli potrzebujesz kluczy tajnych toopull z [usługi Azure Key Vault](../key-vault/key-vault-get-started.md) wdrażając jednostek fabryki danych Azure za pomocą szablonów, należy określić hello **magazynu kluczy** i **nazwa klucza tajnego** opisane w Poniższy przykład Hello:</span><span class="sxs-lookup"><span data-stu-id="0567d-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="0567d-158">Podczas eksportowania szablonów dla fabryki danych istniejących obecnie nie jest jeszcze obsługiwana, jest hello działa.</span><span class="sxs-lookup"><span data-stu-id="0567d-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
