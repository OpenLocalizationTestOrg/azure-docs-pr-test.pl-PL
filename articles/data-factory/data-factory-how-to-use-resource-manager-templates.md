---
title: "Użyj Menedżera zasobów szablonów w fabryce danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i szablony usługi Azure Resource Manager umożliwia tworzenie jednostek fabryki danych."
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
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="503de-103">Szablony umożliwiają utworzenie jednostek fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="503de-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="503de-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="503de-104">Overview</span></span>
<span data-ttu-id="503de-105">Podczas używania fabryki danych Azure potrzeby integracji danych może okazać się ponowne użycie tego samego wzorca w różnych środowiskach lub wykonania tego samego zadania kilkukrotnie w tym samym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="503de-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="503de-106">Szablony ułatwiają wdrożenia i zarządzania tych scenariuszy w łatwy sposób.</span><span class="sxs-lookup"><span data-stu-id="503de-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="503de-107">Szablony w fabryce danych Azure idealnie nadają się do scenariusze, które obejmują możliwość ponownego wykorzystania i powtórzenia.</span><span class="sxs-lookup"><span data-stu-id="503de-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="503de-108">Rozważmy sytuację, w którym organizacja ma 10 zakładu produkcyjnego całym świecie.</span><span class="sxs-lookup"><span data-stu-id="503de-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="503de-109">Dzienniki z każdego zakładu są przechowywane w bazie danych programu SQL Server oddzielny lokalny.</span><span class="sxs-lookup"><span data-stu-id="503de-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="503de-110">Firma chce utworzyć magazynu danych w chmurze na potrzeby analizy ad hoc.</span><span class="sxs-lookup"><span data-stu-id="503de-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="503de-111">Również chce mieć tej samej logiki, ale różne konfiguracje dla środowiska deweloperskie, badanie i produkcji.</span><span class="sxs-lookup"><span data-stu-id="503de-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="503de-112">W takim przypadku zadania konieczne jest powtórzenie w tym samym środowisku, ale o różnych wartościach między fabryk danych 10 dla każdego zakładu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="503de-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="503de-113">W efekcie **powtarzania** jest obecny.</span><span class="sxs-lookup"><span data-stu-id="503de-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="503de-114">Tworzenia szablonów umożliwia pozyskiwania to ogólny przepływ (to znaczy potoki o tych samych czynności z każdej fabryki danych), ale używa pliku osobny parametr dla każdego zakładu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="503de-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="503de-115">Ponadto, ponieważ organizacja chce wdrożyć te fabryki danych 10 wielokrotnie różnych środowiskach, szablony, mogą używać tego **możliwość ponownego wykorzystania** przy użyciu plików osobny parametr do tworzenia, testowania, i środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="503de-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="503de-116">Tworzenia szablonów z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="503de-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="503de-117">[Szablony usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) to doskonały sposób, aby osiągnąć tworzenia szablonów w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="503de-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="503de-118">Szablony Menedżera zasobów zdefiniuj infrastrukturze i konfiguracji rozwiązania Azure za pomocą pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="503de-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="503de-119">Ponieważ szablonów usługi Azure Resource Manager działa z usługami Azure all/większość, może być powszechnie używane w prosty sposób zarządzać wszystkie zasoby zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="503de-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="503de-120">Zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) Aby dowiedzieć się więcej o szablonach usługi Resource Manager ogólnie.</span><span class="sxs-lookup"><span data-stu-id="503de-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="503de-121">Samouczki</span><span class="sxs-lookup"><span data-stu-id="503de-121">Tutorials</span></span>
<span data-ttu-id="503de-122">Zobacz następujące samouczki krok po kroku instrukcje dotyczące tworzenia jednostek fabryki danych przy użyciu szablonów usługi Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="503de-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="503de-123">Samouczek: Tworzenie potoku, aby skopiować dane przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="503de-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="503de-124">Samouczek: Tworzenie potoku do przetwarzania danych przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="503de-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="503de-125">Szablony fabryki danych w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="503de-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="503de-126">Wyewidencjonuj następujących szablonów szybki start Azure w serwisie GitHub:</span><span class="sxs-lookup"><span data-stu-id="503de-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="503de-127">Tworzenie fabryki danych, aby skopiować dane z magazynu obiektów Blob Azure do bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="503de-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="503de-128">Tworzenie fabryki danych działania Hive w usłudze Azure HDInsight klastra</span><span class="sxs-lookup"><span data-stu-id="503de-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="503de-129">Tworzenie fabryki danych można skopiować danych z usług Salesforce do obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="503de-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="503de-130">Tworzenie fabryki danych, w którym jest powiązany działań: kopiuje dane z serwera FTP do obiektów blob Azure, wywołuje skrypt hive w klastrze usługi HDInsight na żądanie do przekształcania danych i kopiuje wynik do bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="503de-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="503de-131">Możesz także udostępnić szablony fabryki danych Azure na [Azure szybki start](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="503de-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="503de-132">Zapoznaj się [przewodnik wkład](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) podczas tworzenia szablonów, które mogą być współużytkowane przez to repozytorium.</span><span class="sxs-lookup"><span data-stu-id="503de-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="503de-133">Poniższe sekcje zawierają szczegółowe informacje na temat definiowania zasoby fabryki danych w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="503de-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="503de-134">Definiowanie zasoby fabryki danych w szablonach</span><span class="sxs-lookup"><span data-stu-id="503de-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="503de-135">Szablon najwyższego poziomu do definiowania fabryki danych jest:</span><span class="sxs-lookup"><span data-stu-id="503de-135">The top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="503de-136">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="503de-136">Define data factory</span></span>
<span data-ttu-id="503de-137">Fabrykę danych definiuje się w szablonie usługi Resource Manager jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="503de-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="503de-138">DataFactoryName jest zdefiniowana w "zmiennych" jako:</span><span class="sxs-lookup"><span data-stu-id="503de-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="503de-139">Zdefiniuj połączone usługi</span><span class="sxs-lookup"><span data-stu-id="503de-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="503de-140">Zobacz [połączonej usługi magazynu](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [obliczeniowe połączonych usług](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) szczegółowe informacje o właściwościach JSON dla określonej usługi połączonej chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="503de-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="503de-141">Parametr "dependsOn" Określa nazwę odpowiedniego fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="503de-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="503de-142">Przykład Definiowanie połączonej usługi magazynu Azure znajduje się w następującej definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="503de-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="503de-143">Zdefiniuj zbiory danych</span><span class="sxs-lookup"><span data-stu-id="503de-143">Define datasets</span></span>

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
<span data-ttu-id="503de-144">Zapoznaj się [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) szczegółowe informacje o właściwościach JSON dla określonego zestawu danych typu chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="503de-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="503de-145">Należy pamiętać, że parametr "dependsOn" Określa nazwę odpowiedniego fabryki danych i magazynu połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="503de-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="503de-146">Przykład definiujący typ zestawu danych z magazynu obiektów blob Azure znajduje się w następującej definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="503de-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="503de-147">Zdefiniuj potoki</span><span class="sxs-lookup"><span data-stu-id="503de-147">Define pipelines</span></span>

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

<span data-ttu-id="503de-148">Zapoznaj się [Definiowanie potoki](data-factory-create-pipelines.md#pipeline-json) szczegółowe informacje na temat właściwości JSON definiujący określone potoku i działań, które chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="503de-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="503de-149">Należy pamiętać, parametr "dependsOn" Nazwa fabryki danych i wszystkie odpowiednie połączonych usług lub zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="503de-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="503de-150">Przykład potok, który kopiuje dane z magazynu obiektów Blob Azure do bazy danych SQL Azure znajduje się w następujący fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="503de-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

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
        "description": "Copy data frm Azure blob to Azure SQL",
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
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="503de-151">Ustawianie szablonu usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="503de-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="503de-152">Najlepsze rozwiązania na ustawianie, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) artykułu.</span><span class="sxs-lookup"><span data-stu-id="503de-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="503de-153">Ogólnie rzecz biorąc użycia parametru można zmniejszyć do minimum, zwłaszcza jeśli zmienne, które mogą być używane zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="503de-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="503de-154">Tylko podać parametry w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="503de-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="503de-155">Ustawienia zależą od środowiska (przykład: Programowanie, testowe i produkcyjne)</span><span class="sxs-lookup"><span data-stu-id="503de-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="503de-156">Klucze tajne (takie jak hasła)</span><span class="sxs-lookup"><span data-stu-id="503de-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="503de-157">Jeśli chcesz ściągnąć kluczy tajnych ze [usługi Azure Key Vault](../key-vault/key-vault-get-started.md) wdrażając jednostek fabryki danych Azure za pomocą szablonów, należy określić **magazynu kluczy** i **nazwa klucza tajnego** opisane w Poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="503de-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

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
> <span data-ttu-id="503de-158">Podczas eksportowania szablonów dla fabryki danych istniejących obecnie nie jest jeszcze obsługiwana, jest działa.</span><span class="sxs-lookup"><span data-stu-id="503de-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
