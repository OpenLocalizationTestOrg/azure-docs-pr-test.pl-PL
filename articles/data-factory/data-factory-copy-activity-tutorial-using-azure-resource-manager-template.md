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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Samouczek: Użyj Menedżera zasobów Azure szablonu toocreate danych toocopy potoku fabryki danych 
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

W tym samouczku przedstawiono sposób toouse toocreate szablonu usługi Azure Resource Manager fabryki danych Azure. Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Przekształca dane wyjściowe tooproduce danych wejściowych. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Wymagania wstępne
* Przejdź przez [samouczek omówienie i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) i pełne hello **wymagań wstępnych** czynności.
* Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu tooinstall najnowszą wersję programu Azure PowerShell na komputerze. W tym samouczku używamy jednostek fabryki danych toodeploy środowiska PowerShell. 
* (opcjonalnie) Zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md) toolearn informacje o szablonach usługi Azure Resource Manager.

## <a name="in-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku tworzenie fabryki danych z powitania po jednostek fabryki danych:

| Jednostka | Opis |
| --- | --- |
| Połączona usługa Azure Storage |Łączy fabrykę danych toohello konta magazynu Azure. Usługa Azure Storage jest hello źródła danych magazynu i bazy danych Azure SQL jest magazynem danych zbiornika powitania dla aktywności kopiowania hello w samouczku hello. Określa konto magazynu hello zawierający hello danych wejściowych dla aktywności kopiowania hello. |
| Połączona usługa Azure SQL Database |Łączy fabrykę danych toohello bazy danych Azure SQL. Określa bazy danych Azure SQL hello przechowujący hello danych wyjściowych dla działania kopiowania hello. |
| Wejściowy zestaw danych obiektów blob platformy Azure |Odwołuje się toohello połączoną usługą magazynu Azure. Witaj połączonej usługi odwołuje się tooan konta magazynu Azure i zestawu danych obiektów Blob Azure hello Określa kontener hello, folder i nazwę pliku w magazynie hello, która przechowuje dane wejściowe hello. |
| Wyjściowy zestaw danych usługi Azure SQL |Odwołuje się toohello Azure połączoną usługą SQL. Hello Azure połączoną usługą SQL odwołuje się tooan serwera Azure SQL i zestawu danych Azure SQL hello Określa nazwę hello hello tabeli, która przechowuje dane wyjściowe hello. |
| Potok danych |potok Hello ma jedno działanie typu kopii, która przyjmuje jako dane wejściowe, zestawu danych obiektów blob platformy Azure hello i hello zestawu danych Azure SQL jako dane wyjściowe. działanie kopiowania Hello kopiuje dane z tabeli w bazie danych Azure SQL hello tooa obiektów blob platformy Azure. |

Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Istnieją dwa typy działań: [przenoszenia danych](data-factory-data-movement-activities.md) i [przekształcania danych](data-factory-data-transformation-activities.md). W tym samouczku jest tworzony potok z jednym działaniem (kopiowania).

![Kopiowanie obiektów Blob platformy Azure tooAzure bazy danych SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

Witaj poniższej sekcji przedstawiono hello pełną szablonu usługi Resource Manager do definiowania jednostek fabryki danych, aby szybko uruchomić przy użyciu szablonu hello hello samouczek i testowania. toounderstand każdy obiekt fabryki danych jest zdefiniowany, zobacz [jednostek fabryki danych w szablonie hello](#data-factory-entities-in-the-template) sekcji.

## <a name="data-factory-json-template"></a>Szablon JSON usługi Data Factory
Witaj najwyższego poziomu szablonu usługi Resource Manager do definiowania fabryki danych jest: 

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
Utwórz plik JSON o nazwie **ADFCopyTutorialARM.json** w **C:\ADFGetStarted** folder o hello następującej zawartości:

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

## <a name="parameters-json"></a>Parametry JSON
Utwórz plik JSON o nazwie **parameters.JSON następującym kodem ADFCopyTutorialARM** zawierający parametry szablonu usługi Azure Resource Manager hello. 

> [!IMPORTANT]
> Określ nazwę i klucz konta usługi Azure Storage za pomocą parametrów storageAccountName i storageAccountKey.  
> 
> Określ serwer SQL na platformie Azure, bazę danych, użytkownika i hasło w parametrach sqlServerName, databaseName, sqlServerUserName oraz sqlServerPassword.  

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
> Może mieć osobny parametr pliki w formacie JSON do tworzenia, testowania i środowiska produkcyjnego, w których można używać z hello tego samego szablonu JSON fabryki danych. Za pomocą skryptu programu Power Shell można zautomatyzować wdrażanie jednostek usługi Data Factory w tych środowiskach.  
> 
> 

## <a name="create-data-factory"></a>Tworzenie fabryki danych
1. Uruchom **programu Azure PowerShell** i hello uruchom następujące polecenie:
   * Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Uruchom powitania po jednostek fabryki danych toodeploy polecenia przy użyciu szablonu usługi Resource Manager hello utworzonego w kroku 1.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorowanie potoku

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta platformy Azure.
2. Kliknij przycisk **fabryki danych** hello lewym menu (lub) kliknij **więcej usług** i kliknij przycisk **fabryki danych** w obszarze **analizy i analiza** Kategoria.
   
    ![Menu fabryk danych](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. W hello **fabryki danych** strony, wyszukiwanie i Znajdź fabrykę danych (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Wyszukiwanie fabryki danych](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Kliknij fabrykę danych platformy Azure. Zostanie wyświetlona strona główna hello hello fabryki danych.
   
    ![Strona główna fabryki danych](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Postępuj zgodnie z instrukcjami [monitorowanie zestawów danych i potoku](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello potoku i zestawy danych zostały utworzone w tym samouczku. Obecnie program Visual Studio nie obsługuje monitorowania potoków usługi Data Factory.
7. Gdy wycinek jest hello **gotowe** stanu, sprawdź, czy dane hello jest skopiowany toohello **pustych elementów** tabeli w bazie danych Azure SQL hello.


Aby uzyskać więcej informacji o jak toouse bloków portalu Azure toomonitor potoku i zestawy danych zostały utworzone w tym samouczku, zobacz [monitorowanie zestawów danych i potoku](data-factory-monitor-manage-pipelines.md) .

Aby uzyskać więcej informacji dotyczących sposobu toouse hello Monitor & Zarządzaj aplikacji toomonitor danych potoków, zobacz [monitorowanie i zarządzanie nimi przy użyciu monitorowania aplikacji potoki fabryki danych Azure](data-factory-monitor-manage-app.md).

## <a name="data-factory-entities-in-hello-template"></a>Obiekty fabryki danych w szablonie hello
### <a name="define-data-factory"></a>Definiowanie fabryki danych
Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

Hello dataFactoryName jest zdefiniowany jako: 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

Jest to unikatowy ciąg na podstawie identyfikatora hello zasobów grupy.  

### <a name="defining-data-factory-entities"></a>Definiowanie jednostek usługi Data Factory
Hello następujące jednostek fabryki danych są definiowane w szablonie JSON hello: 

1. [Połączona usługa Azure Storage](#azure-storage-linked-service)
2. [Połączona usługa Azure SQL](#azure-sql-database-linked-service)
3. [Zestaw danych obiektów blob platformy Azure](#azure-blob-dataset)
4. [Zestaw danych usługi Azure SQL](#azure-sql-dataset)
5. [Potok danych z działaniem kopiowania](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). W tej sekcji można określić nazwę hello i klucza konta magazynu Azure. Zobacz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure. 

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

Hello connectionString używa parametrów storageAccountName i storageAccountKey hello. Hello wartości tych parametrów przekazane za pomocą pliku konfiguracji. Definicja Hello również używa zmiennych: azureStroageLinkedService i dataFactoryName zdefiniowane w szablonie hello. 

#### <a name="azure-sql-database-linked-service"></a>Połączona usługa Azure SQL Database
AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). W tej sekcji można określić nazwy serwera Azure SQL hello, nazwa bazy danych, nazwę użytkownika i hasło użytkownika. Zobacz [Azure SQL połączona usługa](data-factory-azure-sql-connector.md#linked-service-properties) szczegółowe informacje o toodefine właściwości używane w formacie JSON Azure SQL połączonej usługi.  

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

Witaj connectionString używa sqlServerName, databaseName sqlServerUserName i sqlServerPassword parametry, których wartości są przekazywane za pomocą pliku konfiguracji. Witaj definicji używa również następujące zmienne z szablonu hello hello: azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>Zestaw danych obiektów blob platformy Azure
Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. W definicji zestawu danych obiektów blob platformy Azure należy określić nazwy kontenera obiektów blob, folderu i pliku zawierającego dane wejściowe hello. Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure. 

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

#### <a name="azure-sql-dataset"></a>Zestaw danych usługi Azure SQL
Należy określić nazwę hello hello tabeli w bazie danych Azure SQL hello przechowujący dane hello skopiowane z hello magazynu obiektów Blob platformy Azure. Zobacz [właściwości zestawu danych Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawem danych usługi Azure SQL. 

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

#### <a name="data-pipeline"></a>Potok danych
Należy zdefiniować potok, który kopiuje dane z zestawu danych Azure SQL toohello hello obiektów blob platformy Azure zestawu danych. Zobacz [JSON potoku](data-factory-create-pipelines.md#pipeline-json) opisy toodefine elementów JSON potoku, w tym przykładzie. 

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

## <a name="reuse-hello-template"></a>Ponowne użycie szablonu hello
W samouczku hello utworzony szablon do definiowania jednostek fabryki danych i przekazywanie wartości parametrów szablonu. potok Hello kopiuje dane z usługi Azure Storage konta tooan bazy danych SQL Azure określona za pomocą parametrów. toouse hello tego samego szablonu toodeploy fabryki danych jednostek toodifferent środowiskach, Utwórz plik parametr dla każdego środowiska i użyć go w przypadku wdrażania środowiska toothat.     

Przykład:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Należy zauważyć, że pierwszy parametr używa polecenia hello plik hello Środowisko deweloperskie, drugi dla środowiska testowego hello i hello trzeci co w środowisku produkcyjnym hello.  

Można również ponownie użyć tooperform szablonu hello powtarzanych zadań. Na przykład należy toocreate wiele fabryk danych z jednego lub więcej potoki, które implementują hello sama logika, ale każdej fabryki danych używa innego konta magazynu i bazy danych SQL. W tym scenariuszu, należy użyć hello tego samego szablonu hello — w tym samym środowisku (deweloperów, testów lub produkcji) z innym parametrem pliki toocreate fabryki danych.   

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.
