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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Samouczek: tworzenie pierwszej fabryki danych Azure przy użyciu szablonu usługi Azure Resource Manager
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-build-your-first-pipeline.md)
> * [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [Program PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

W tym artykule używamy toocreate szablonu usługi Azure Resource Manager Twojego pierwszego fabryki danych Azure. Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.

Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**. To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych. potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia. 

> [!NOTE]
> Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych. Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Witaj potoku, w tym samouczku jest tylko jedno działanie typu: HDInsightHive. Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Wymagania wstępne
* Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.
* Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu tooinstall najnowszą wersję programu Azure PowerShell na komputerze.
* Zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md) toolearn informacje o szablonach usługi Azure Resource Manager. 

## <a name="in-this-tutorial"></a>Informacje o tym samouczku
| Jednostka | Opis |
| --- | --- |
| Połączona usługa Azure Storage |Łączy fabrykę danych toohello konta magazynu Azure. blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie. |
| Połączona usługa HDInsight na żądanie |Łącza fabrykę danych toohello klastra usługi HDInsight na żądanie. Hello klastra jest automatycznie tworzony tooprocess danych i zostaną usunięte po ukończeniu przetwarzania hello. |
| Wejściowy zestaw danych obiektów blob platformy Azure |Odwołuje się toohello połączoną usługą magazynu Azure. Witaj połączonej usługi odwołuje się tooan konta magazynu Azure i zestawu danych obiektów Blob Azure hello Określa kontener hello, folder i nazwę pliku w magazynie hello, która przechowuje dane wejściowe hello. |
| Wyjściowy zestaw danych obiektów blob platformy Azure |Odwołuje się toohello połączoną usługą magazynu Azure. Witaj połączonej usługi odwołuje się tooan konta magazynu Azure i zestawu danych obiektów Blob Azure hello Określa kontener hello, folder i nazwę pliku w magazynie hello, która przechowuje dane wyjściowe hello. |
| Potok danych |potok Hello ma jedno działanie typu HDInsightHive, który zużywa hello wejściowy zestaw danych i tworzy hello wyjściowego zestawu danych. |

Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Istnieją dwa typy działań: [przenoszenia danych](data-factory-data-movement-activities.md) i [przekształcania danych](data-factory-data-transformation-activities.md). W tym samouczku tworzony jest potok z jednym działaniem (Działanie programu Hive).

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
Utwórz plik JSON o nazwie **ADFTutorialARM.json** w **C:\ADFGetStarted** folder o hello następującej zawartości:

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
> Temat [Samouczek: Tworzenie potoku za pomocą działania kopiowania przy użyciu szablonu usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) zawiera kolejny przykład szablonu usługi Resource Manager umożliwiającego utworzenie fabryki danych platformy Azure.  
> 
> 

## <a name="parameters-json"></a>Parametry JSON
Utwórz plik JSON o nazwie **parameters.JSON następującym kodem ADFTutorialARM** zawierający parametry szablonu usługi Azure Resource Manager hello.  

> [!IMPORTANT]
> Określ nazwę hello oraz klucz konta magazynu Azure hello **storageAccountName** i **storageAccountKey** parametrów w tym pliku parametrów. 
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
   * Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello. Ta subskrypcja powinien Witaj, taka sama, jak hello jedną używaną w hello portalu Azure.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Uruchom powitania po jednostek fabryki danych toodeploy polecenia przy użyciu szablonu usługi Resource Manager hello utworzonego w kroku 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorowanie potoku
1. Po zalogowaniu toohello [portalu Azure](https://portal.azure.com/), kliknij przycisk **Przeglądaj** i wybierz **fabryki danych**.
     ![Przeglądaj->Fabryki danych](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. W hello **fabryki danych** bloku, kliknij przycisk fabryki danych hello (**TutorialFactoryARM**) utworzony.    
3. W hello **fabryki danych** bloku fabrykę danych, kliknij przycisk **Diagram**.

     ![Kafelek diagramu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. W hello **widoku diagramu**, zobacz Omówienie potoki hello i używać zestawów danych w tym samouczku.
   
   ![Widok diagramu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Hello widoku diagramu, kliknij dwukrotnie hello dataset **AzureBlobOutput**. Użytkownik widzi tego hello wycinek, który jest obecnie przetwarzane.
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Po zakończeniu przetwarzania zostanie wyświetlony wycinek hello **gotowe** stanu. Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut). W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Gdy wycinek hello jest **gotowe** stanu, należy sprawdzić hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.  

Zobacz [monitorowanie zestawów danych i potoku](data-factory-monitor-manage-pipelines.md) instrukcje dotyczące sposobu toouse hello Azure bloki portalu toomonitor hello potoku i zestawy danych zostały utworzone w tym samouczku.

Umożliwia także monitora i zarządzanie aplikacjami toomonitor Twojego potokach danych. Zobacz [monitorowanie i zarządzanie nimi przy użyciu monitorowania aplikacji potoki fabryki danych Azure](data-factory-monitor-manage-app.md) szczegóły dotyczące używania aplikacji hello. 

> [!IMPORTANT]
> Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie. W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.
> 
> 

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
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Jest to unikatowy ciąg na podstawie identyfikatora hello zasobów grupy.  

### <a name="defining-data-factory-entities"></a>Definiowanie jednostek usługi Data Factory
Hello następujące jednostek fabryki danych są definiowane w szablonie JSON hello: 

* [Połączona usługa Azure Storage](#azure-storage-linked-service)
* [Połączona usługa HDInsight na żądanie](#hdinsight-on-demand-linked-service)
* [Wejściowy zestaw danych obiektów blob platformy Azure](#azure-blob-input-dataset)
* [Wyjściowy zestaw danych obiektów blob platformy Azure](#azure-blob-output-dataset)
* [Potok danych z działaniem kopiowania](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
W tej sekcji można określić nazwę hello i klucza konta magazynu Azure. Zobacz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure. 

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
Witaj **connectionString** używa hello parametry storageAccountName i storageAccountKey. Hello wartości tych parametrów przekazane za pomocą pliku konfiguracji. Definicja Hello również używa zmiennych: azureStroageLinkedService i dataFactoryName zdefiniowane w szablonie hello. 

#### <a name="hdinsight-on-demand-linked-service"></a>Połączona usługa HDInsight na żądanie
Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artykuł szczegółowe informacje o toodefine właściwości używane w formacie JSON na żądanie połączoną usługą usługi HDInsight.  

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
Należy zwrócić uwagę hello następujące punkty: 

* Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello powyżej JSON. Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie). 
* Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).
* Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. Z usługą HDInsight połączony na żądanie, klastra usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello.
  
    Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.

Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).

#### <a name="azure-blob-input-dataset"></a>Wejściowy zestaw danych obiektów blob platformy Azure
Należy określić nazwy hello folder, plik zawierający dane wejściowe hello i kontener obiektów blob. Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure. 

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
Ta definicja używa następujących parametrów zdefiniowanych w szablonie parametru hello: blobContainer, inputBlobFolder i inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure
Należy określić nazwy hello kontenera obiektów blob i folderu, która przechowuje dane wyjściowe hello. Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.  

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

Ta definicja używa następujących parametrów zdefiniowanych w szablonie parametru hello hello: blobContainer i outputBlobFolder. 

#### <a name="data-pipeline"></a>Potok danych
Definiuje się potok przekształcający dane za pomocą skryptu Hive uruchamianego w klastrze usługi Azure HDInsight na żądanie. Zobacz [JSON potoku](data-factory-create-pipelines.md#pipeline-json) opisy toodefine elementów JSON potoku, w tym przykładzie. 

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

## <a name="reuse-hello-template"></a>Ponowne użycie szablonu hello
W samouczku hello utworzony szablon do definiowania jednostek fabryki danych i przekazywanie wartości parametrów szablonu. toouse hello tego samego szablonu toodeploy fabryki danych jednostek toodifferent środowiskach, Utwórz plik parametr dla każdego środowiska i użyć go w przypadku wdrażania środowiska toothat.     

Przykład:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Należy zauważyć, że pierwszy parametr używa polecenia hello plik hello Środowisko deweloperskie, drugi dla środowiska testowego hello i hello trzeci co w środowisku produkcyjnym hello.  

Można również ponownie użyć tooperform szablonu hello powtarzanych zadań. Na przykład należy toocreate wiele fabryk danych z jednego lub więcej potoki, które implementują hello samej logiki, ale każdy inny magazynu Azure danych fabryki używa i konta bazy danych SQL Azure. W tym scenariuszu, należy użyć hello tego samego szablonu hello — w tym samym środowisku (deweloperów, testów lub produkcji) z innym parametrem pliki toocreate fabryki danych. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Szablon usługi Resource Manager do tworzenia bramy
Poniżej przedstawiono szablon usługi Resource Manager próbki do tworzenia logicznej bramy w hello ponownie. Zainstaluj bramę na komputerze lokalnym lub maszyny Wirtualnej Azure IaaS i zarejestruj bramę hello usłudze fabryka danych przy użyciu klucza. Szczegółowe informacje znajdują się w artykule [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) (Przenoszenie danych między komputerem lokalnym i chmurą).

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
Ten szablon służy do tworzenia fabryki danych o nazwie GatewayUsingArmDF z bramą o nazwie: GatewayUsingARM. 

## <a name="see-also"></a>Zobacz też
| Temat | Opis |
|:--- |:--- |
| [Potoki](data-factory-create-pipelines.md) |Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy. |
| [Zestawy danych](data-factory-create-datasets.md) |Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory. |
| [Planowanie i wykonywanie](data-factory-scheduling-and-execution.md) |W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure. |
| [Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania](data-factory-monitor-manage-app.md) |W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania. |

