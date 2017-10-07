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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Użyj jednostek fabryki danych Azure toocreate szablonów
## <a name="overview"></a>Omówienie
Podczas używania fabryki danych Azure potrzeby integracji danych może okazać się ponowne użycie hello tego samego wzorca różnych środowiskach lub implementacja hello samo zadanie kilkukrotnie w hello takie same rozwiązania. Szablony ułatwiają wdrożenia i zarządzania tych scenariuszy w łatwy sposób. Szablony w fabryce danych Azure idealnie nadają się do scenariusze, które obejmują możliwość ponownego wykorzystania i powtórzenia.

Należy wziąć pod uwagę hello sytuacji, gdy organizacja ma 10 zakładu produkcyjnego w hello world. Dzienniki Hello z każdego zakładu są przechowywane w bazie danych programu SQL Server oddzielny lokalny. Witaj firma chce toobuild magazynu danych w chmurze hello analizy ad hoc. Chce ona również toohave hello samej logiki, ale różne konfiguracje dla środowiska deweloperskie, badanie i produkcji.

W takim przypadku zadania musi toobe powtarzany w tym samym środowisku Witaj, ale o różnych wartościach między hello 10 fabryk danych dla każdego zakładu produkcyjnego. W efekcie **powtarzania** jest obecny. Abstrakcja hello to ogólny przepływ umożliwia tworzenia szablonów (to znaczy potoków o hello tego samego działania z każdej fabryki danych), ale używa pliku osobny parametr dla każdego zakładu produkcyjnego.

Ponadto ponieważ hello obowiązującymi w organizacji toodeploy tych fabryk danych 10 wielokrotnie w różnych środowiskach, szablony, mogą używać tego **możliwość ponownego wykorzystania** przy użyciu plików osobny parametr do tworzenia aplikacji, przetestować, i środowisk produkcyjnych.

## <a name="templating-with-azure-resource-manager"></a>Tworzenia szablonów z usługą Azure Resource Manager
[Szablony usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) to doskonały sposób tworzenia ze tooachieve szablonów w fabryce danych Azure. Szablony Menedżera zasobów zdefiniuj hello infrastrukturze i konfiguracji rozwiązania Azure za pomocą pliku JSON. Ponieważ szablonów usługi Azure Resource Manager pracować z wszystkich/większość usług platformy Azure, powszechnie umożliwia tooeasily zarządzania wszystkie zasoby zasobów platformy Azure. Zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) ogólnie hello toolearn więcej na temat szablonów Resource Manager.

## <a name="tutorials"></a>Samouczki
Zobacz następujące samouczki dla jednostek fabryki danych toocreate instrukcje krok po kroku przy użyciu szablonów usługi Resource Manager hello:

* [Samouczek: Tworzenie potoku toocopy danych przy użyciu szablonu usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Samouczek: Tworzenie potoku tooprocess danych przy użyciu szablonu usługi Azure Resource Manager](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Szablony fabryki danych w witrynie GitHub
Wyewidencjonuj hello następujących szablonów szybki start Azure w serwisie GitHub:

* [Utwórz toocopy fabryka danych z magazynu obiektów Blob Azure tooAzure bazy danych SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Tworzenie fabryki danych działania Hive w usłudze Azure HDInsight klastra](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [Tworzenie z obiektów blob tooAzure Salesforce toocopy fabryki danych](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Tworzenie fabryki danych, w którym jest powiązany działań: kopiuje dane z serwera FTP tooAzure obiektów blob, wywołuje skrypt hive na dane HDInsight hello tootransform klastra na żądanie i kopiuje wynik do bazy danych SQL Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

Możesz wolnego tooshare szablonów fabryki danych Azure na [Azure szybki start](https://azure.microsoft.com/documentation/templates/). Zobacz toohello [przewodnik wkład](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) podczas tworzenia szablonów, które mogą być współużytkowane przez to repozytorium.

Witaj następujące sekcje zawierają szczegółowe informacje o Definiowanie zasoby fabryki danych w szablonie usługi Resource Manager.

## <a name="defining-data-factory-resources-in-templates"></a>Definiowanie zasoby fabryki danych w szablonach
Witaj szablon najwyższego poziomu do definiowania fabryki danych jest:

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

### <a name="define-data-factory"></a>Definiowanie fabryki danych
Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Hello dataFactoryName jest zdefiniowana w "zmiennych" jako:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Zdefiniuj połączone usługi

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Zobacz [połączonej usługi magazynu](data-factory-azure-blob-connector.md#azure-storage-linked-service) lub [obliczeniowe połączonych usług](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) szczegółowe informacje na temat właściwości JSON hello hello określonych połączonej usługi mają toodeploy. Parametr "dependsOn" Hello Określa nazwę hello odpowiedniego fabryki danych. Przykład Definiowanie połączonej usługi magazynu Azure znajduje się w następującej definicji JSON hello:

### <a name="define-datasets"></a>Zdefiniuj zbiory danych

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
Odwołuje się zbyt[obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) szczegółowe informacje na temat właściwości JSON hello hello określonego zestawu danych typu mają toodeploy. Parametr "dependsOn" hello Uwaga Określa nazwę hello odpowiednie dane fabryki i magazynu połączonej usługi. Przykład definiujący typ zestawu danych z magazynu obiektów blob Azure znajduje się w następującej definicji JSON hello:

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

### <a name="define-pipelines"></a>Zdefiniuj potoki

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

Odwołuje się zbyt[Definiowanie potoki](data-factory-create-pipelines.md#pipeline-json) dla szczegółowe informacje o właściwości JSON hello definiujące hello określonych potoku i działania mają toodeploy. Parametr "dependsOn" hello Uwaga określa nazwy fabryki danych hello oraz odpowiedni połączonych usług lub zestawów danych. Przykład potok, który kopiuje dane z magazynu obiektów Blob Azure tooAzure bazy danych SQL znajduje się w powitania po fragment kodu JSON:

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
## <a name="parameterizing-data-factory-template"></a>Ustawianie szablonu usługi fabryka danych
Najlepsze rozwiązania na ustawianie, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) artykułu. Ogólnie rzecz biorąc użycia parametru można zmniejszyć do minimum, zwłaszcza jeśli zmienne, które mogą być używane zamiast tego. Tylko podać parametry w hello następujące scenariusze:

* Ustawienia zależą od środowiska (przykład: Programowanie, testowe i produkcyjne)
* Klucze tajne (takie jak hasła)

Jeśli potrzebujesz kluczy tajnych toopull z [usługi Azure Key Vault](../key-vault/key-vault-get-started.md) wdrażając jednostek fabryki danych Azure za pomocą szablonów, należy określić hello **magazynu kluczy** i **nazwa klucza tajnego** opisane w Poniższy przykład Hello:

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
> Podczas eksportowania szablonów dla fabryki danych istniejących obecnie nie jest jeszcze obsługiwana, jest hello działa.
>
>
