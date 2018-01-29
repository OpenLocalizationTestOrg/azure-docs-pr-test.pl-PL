---
title: "Tworzenie fabryki danych na platformie Azure przy użyciu szablonu usługi Resource Manager | Microsoft Docs"
description: "W tym samouczku przedstawiono tworzenie przykładowego potoku usługi Azure Data Factory przy użyciu szablonu usługi Azure Resource Manager."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/22/2018
ms.author: spelluru
ms.openlocfilehash: 5008d8f0ce36f09ff26bf10fadbf14da6b474ea9
ms.sourcegitcommit: 79683e67911c3ab14bcae668f7551e57f3095425
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="tutorial-create-an-azure-data-factory-using-azure-resource-manager-template"></a>Samouczek: tworzenie fabryki danych na platformie Azure przy użyciu szablonu usługi Azure Resource Manager
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](v1/data-factory-build-your-first-pipeline-using-arm.md)
> * [Wersja 2 — wersja zapoznawcza](quickstart-create-data-factory-resource-manager-template.md) 

W tym przewodniku Szybki start wyjaśniono, jak skorzystać z szablonu usługi Azure Resource Manager w celu utworzenia fabryki danych na platformie Azure. Potok tworzony w tej fabryce danych **kopiuje** dane z jednego folderu do innego folderu w usłudze Azure Blob Storage. Aby zapoznać się z samouczkiem dotyczącym **przekształcania** danych za pomocą usługi Azure Data Factory, zobacz [Tutorial: Transform data using Spark (Samouczek: Przekształcanie danych przy użyciu usługi Spark)](transform-data-using-spark.md). 

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz artykuł dotyczący [tworzenia pierwszej fabryki danych przy użyciu usługi Data Factory w wersji 1](v1/data-factory-build-your-first-pipeline-using-arm.md).
>
> Ten artykuł nie zawiera szczegółowego wprowadzenia do usługi Data Factory. Aby zapoznać się z wprowadzeniem do usługi Azure Data Factory, zobacz [Wprowadzenie do usługi Azure Data Factory](introduction.md).

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

### <a name="azure-powershell"></a>Azure PowerShell
Zainstaluj najnowsze moduły programu Azure PowerShell, wykonując instrukcje podane w temacie [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="resource-manager-templates"></a>Szablony usługi Resource Manager
Ogólne informacje na temat szablonów usługi Azure Resource Manager zawiera temat [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). 

W poniższej sekcji przedstawiono pełny szablon usługi Resource Manager umożliwiający definiowanie jednostek usługi Data Factory, dzięki czemu można szybko przejść przez samouczek i przetestować szablon. Aby dowiedzieć się, jak jest zdefiniowana każda jednostka usługi Data Factory, zobacz sekcję [Jednostki usługi Data Factory w szablonie](#data-factory-entities-in-the-template).

## <a name="data-factory-json"></a>Plik JSON usługi Data Factory 
Utwórz plik JSON o nazwie **ADFTutorialARM.json** w folderze **C:\ADFTutorial** o następującej zawartości:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "dataFactoryName": {
            "type": "string",
            "metadata": {
                "description": "Name of the data factory. Must be globally unique."
            }
        },
        "dataFactoryLocation": {
            "type": "string",
            "allowedValues": [
                "East US",
                "East US 2",
                "West Europe"
            ],
            "defaultValue": "East US",
            "metadata": {
                "description": "Location of the data factory. Currently, only East US, East US 2, and West Europe are supported. "
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Azure storage account that contains the input/output data."
            }
        },
        "storageAccountKey": {
            "type": "securestring",
            "metadata": {
                "description": "Key for the Azure storage account."
            }
        },
        "blobContainer": {
            "type": "string",
            "metadata": {
                "description": "Name of the blob container in the Azure Storage account."
            }
        },
        "inputBlobFolder": {
            "type": "string",
            "metadata": {
                "description": "The folder in the blob container that has the input file."
            }
        },
        "inputBlobName": {
            "type": "string",
            "metadata": {
                "description": "Name of the input file/blob."
            }
        },
        "outputBlobFolder": {
            "type": "string",
            "metadata": {
                "description": "The folder in the blob container that will hold the transformed data."
            }
        },
        "outputBlobName": {
            "type": "string",
            "metadata": {
                "description": "Name of the output file/blob."
            }
        },
        "triggerStartTime": {
            "type": "string",
            "metadata": {
                "description": "Start time for the trigger."
            }
        },
        "triggerEndTime": {
            "type": "string",
            "metadata": {
                "description": "End time for the trigger."
            }
        }
    },
    "variables": {
        "azureStorageLinkedServiceName": "ArmtemplateStorageLinkedService",
        "inputDatasetName": "ArmtemplateTestDatasetIn",
        "outputDatasetName": "ArmtemplateTestDatasetOut",
        "pipelineName": "ArmtemplateSampleCopyPipeline",
        "triggerName": "ArmTemplateTestTrigger"
    },
    "resources": [{
        "name": "[parameters('dataFactoryName')]",
        "apiVersion": "2017-09-01-preview",
        "type": "Microsoft.DataFactory/factories",
        "location": "[parameters('dataFactoryLocation')]",
        "properties": {
            "loggingStorageAccountName": "[parameters('storageAccountName')]",
            "loggingStorageAccountKey": "[parameters('storageAccountKey')]"
        },
        "resources": [{
                "type": "linkedservices",
                "name": "[variables('azureStorageLinkedServiceName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureStorage",
                    "description": "Azure Storage linked service",
                    "typeProperties": {
                        "connectionString": {
                            "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]",
                            "type": "SecureString"
                        }
                    }
                }
            },
            {
                "type": "datasets",
                "name": "[variables('inputDatasetName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureBlob",
                    "typeProperties": {
                        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'), '/')]",
                        "fileName": "[parameters('inputBlobName')]"
                    },
                    "linkedServiceName": {
                        "referenceName": "[variables('azureStorageLinkedServiceName')]",
                        "type": "LinkedServiceReference"
                    }
                }
            },
            {
                "type": "datasets",
                "name": "[variables('outputDatasetName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureBlob",
                    "typeProperties": {
                        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'), '/')]",
                        "fileName": "[parameters('outputBlobName')]"
                    },
                    "linkedServiceName": {
                        "referenceName": "[variables('azureStorageLinkedServiceName')]",
                        "type": "LinkedServiceReference"
                    }
                }
            },
            {
                "type": "pipelines",
                "name": "[variables('pipelineName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]",
                    "[variables('inputDatasetName')]",
                    "[variables('outputDatasetName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "activities": [{
                        "type": "Copy",
                        "typeProperties": {
                            "source": {
                                "type": "BlobSource"
                            },
                            "sink": {
                                "type": "BlobSink"
                            }
                        },
                        "name": "MyCopyActivity",
                        "inputs": [{
                            "referenceName": "[variables('inputDatasetName')]",
                            "type": "DatasetReference"
                        }],
                        "outputs": [{
                            "referenceName": "[variables('outputDatasetName')]",
                            "type": "DatasetReference"
                        }]
                    }]
                }
            },
            {
                "type": "triggers",
                "name": "[variables('triggerName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]",
                    "[variables('inputDatasetName')]",
                    "[variables('outputDatasetName')]",
                    "[variables('pipelineName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "ScheduleTrigger",
                    "typeProperties": {
                        "recurrence": {
                            "frequency": "Hour",
                            "interval": 1,
                            "startTime": "[parameters('triggerStartTime')]",
                            "endTime": "[parameters('triggerEndTime')]",
                            "timeZone": "UTC"
                        }
                    },
                    "pipelines": [{
                        "pipelineReference": {
                            "type": "PipelineReference",
                            "referenceName": "ArmtemplateSampleCopyPipeline"
                        },
                        "parameters": {}
                    }]
                }
            }
        ]
    }]
}
```

## <a name="parameters-json"></a>Parametry JSON
Utwórz plik JSON o nazwie **ADFTutorialARM-Parameters.json** zawierający parametry szablonu usługi Azure Resource Manager.  

> [!IMPORTANT]
> - Określ nazwę i klucz konta usługi Azure Storage w pliku parametrów za pomocą parametrów **storageAccountName** i **storageAccountKey**. W tym magazynie obiektów blob platformy Azure utworzono kontener adftutorial i przekazano przykładowy plik (emp.txt) do folderu wejściowego. 
> - Za pomocą parametru **dataFactoryName** określ nazwę fabryki danych unikatową w skali globalnej, na przykład: ARMTutorialFactoryJohnDoe11282017. 
> - Za pomocą parametru **triggerStartTime** podaj bieżący dzień w formacie: `2017-11-28T00:00:00`.
> - Za pomocą parametru **triggerEndTime** podaj kolejny dzień w formacie: `2017-11-29T00:00:00`. Możesz również sprawdzić bieżącą godzinę w strefie UTC i określić czas zakończenia za godzinę lub dwie. Jeśli na przykład bieżąca godzina w strefie UTC to 1:32, podaj wartość `2017-11-29:03:00:00` jako czas zakończenia. W tym przypadku wyzwalacz uruchomi potok dwukrotnie (o godz. 2:00 i 3:00).

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "dataFactoryName": {
      "value": "<datafactoryname>"
    },    
    "dataFactoryLocation": {
      "value": "East US"
    },
    "storageAccountName": {
      "value": "<yourstroageaccountname>"
    },
    "storageAccountKey": {
      "value": "<yourstorageaccountkey>"
    },
    "blobContainer": {
      "value": "adftutorial"
    },
    "inputBlobFolder": {
      "value": "input"
    },
    "inputBlobName": {
      "value": "emp.txt"
    },
    "outputBlobFolder": {
      "value": "output"
    },
    "outputBlobName": {
      "value": "emp.txt"
    },
    "triggerStartTime": {
        "value": "2017-11-28T00:00:00. Set to today"
    },
    "triggerEndTime": {
        "value": "2017-11-29T00:00:00. Set to tomorrow"
    }
  }
}
```

> [!IMPORTANT]
> Można używać oddzielnych plików parametrów JSON dla środowisk programistycznego, testowego i produkcyjnego do użycia z tym samym szablonem JSON usługi Data Factory. Za pomocą skryptu programu Power Shell można zautomatyzować wdrażanie jednostek usługi Data Factory w tych środowiskach. 

## <a name="deploy-data-factory-entities"></a>Wdrażanie jednostek usługi Data Factory 
W programie PowerShell uruchom następujące polecenie, aby wdrożyć jednostki usługi Data Factory przy użyciu utworzonego wcześniej szablonu usługi Resource Manager. 

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFTutorial\ADFTutorialARM.json -TemplateParameterFile C:\ADFTutorial\ADFTutorialARM-Parameters.json
```

Zostaną wyświetlone dane wyjściowe podobne do tych w następującym przykładzie: 

```
DeploymentName          : MyARMDeployment
ResourceGroupName       : ADFTutorialResourceGroup
ProvisioningState       : Succeeded
Timestamp               : 11/29/2017 3:11:13 AM
Mode                    : Incremental
TemplateLink            :
Parameters              :
                          Name                 Type            Value
                          ===============      ============    ==========
                          dataFactoryName      String          <data factory name>
                          dataFactoryLocation  String          East US
                          storageAccountName   String          <storage account name>
                          storageAccountKey    SecureString
                          blobContainer        String          adftutorial
                          inputBlobFolder      String          input
                          inputBlobName        String          emp.txt
                          outputBlobFolder     String          output
                          outputBlobName       String          emp.txt
                          triggerStartTime     String          11/29/2017 12:00:00 AM
                          triggerEndTime       String          11/29/2017 4:00:00 AM

Outputs                 :
DeploymentDebugLogLevel :
```

## <a name="start-the-trigger"></a>Uruchamianie wyzwalacza

Szablon umożliwia wdrożenie następujących jednostek usługi Data Factory: 

- Połączona usługa Azure Storage
- Zestawy danych obiektów blob platformy Azure (wejściowe i wyjściowe)
- Potok z działaniem kopiowania
- Wyzwalacz potoku

Wdrożony wyzwalacz jest w stanie zatrzymanym. Można go uruchomić, na przykład korzystając z polecenia cmdlet **Start-AzureRmDataFactoryV2Trigger** programu PowerShell. Poniższa procedura zawiera szczegółowy opis kroków: 

1. W oknie programu PowerShell utwórz zmienną do przechowywania nazwy grupy zasobów. Skopiuj poniższe polecenie do okna programu PowerShell i naciśnij klawisz ENTER. Jeśli podano inną nazwę grupy zasobów, uruchamiając polecenie New-AzureRmResourceGroupDeployment, zaktualizuj tę wartość. 

    ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ``` 
1. Utwórz zmienną do przechowywania nazwy fabryki danych. Podaj tę samą nazwę, którą określono w pliku ADFTutorialARM-Parameters.json.   

    ```powershell
    $dataFactoryName = "<yourdatafactoryname>"
    ```
3. Ustaw zmienną dla nazwy wyzwalacza. Nazwa wyzwalacza jest trwale zakodowana w pliku szablonu usługi Resource Manager (ADFTutorialARM.json).

    ```powershell
    $triggerName = "ArmTemplateTestTrigger"
    ```
4. Po podaniu nazw fabryki danych i wyzwalacza, pobierz **stan wyzwalacza**, uruchamiając następujące polecenie programu PowerShell:

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $triggerName
    ```

    Oto przykładowe dane wyjściowe: 

    ```json
    TriggerName       : ArmTemplateTestTrigger
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ARMFactory1128
    Properties        : Microsoft.Azure.Management.DataFactory.Models.ScheduleTrigger
    RuntimeState      : Stopped
    ```
    
    Zwróć uwagę, że stan środowiska uruchomieniowego wyzwalacza to **Zatrzymany**. 
5. **Uruchom wyzwalacz**. Wyzwalacz uruchamia potok zdefiniowany w szablonie o pełnej godzinie. Na przykład jeśli polecenie zostanie wykonane o godzinie 14:25, po raz pierwszy wyzwalacz uruchomi potok o godzinie 15:00. Następnie potok będzie uruchamiany co godzinę do czasu zakończenia podanego dla wyzwalacza. 

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -TriggerName $triggerName
    ```
    
    Oto przykładowe dane wyjściowe: 
    
    ```
    Confirm
    Are you sure you want to start trigger 'ArmTemplateTestTrigger' in data factory 'ARMFactory1128'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    True
    ```
6. Uruchom ponownie polecenie Get-AzureRmDataFactoryV2Trigger, aby upewnić się, że wyzwalacz został uruchomiony.  

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -TriggerName $triggerName
    ```
    
    Oto przykładowe dane wyjściowe:
    
    ```
    TriggerName       : ArmTemplateTestTrigger
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ARMFactory1128
    Properties        : Microsoft.Azure.Management.DataFactory.Models.ScheduleTrigger
    RuntimeState      : Started
    ```

## <a name="monitor-the-pipeline"></a>Monitorowanie potoku
1. Po zalogowaniu się do witryny [Azure Portal](https://portal.azure.com/) kliknij pozycję **Więcej usług**, przeprowadź wyszukiwanie przy użyciu słowa kluczowego, takiego jak **fabryki da**, i wybierz pozycję **Fabryki danych**.

    ![Menu przeglądania fabryk danych](media/quickstart-create-data-factory-resource-manager-template/browse-data-factories-menu.png)
2. Na stronie **Fabryki danych** kliknij utworzoną fabrykę danych. W razie potrzeby przefiltruj listę, wpisując nazwę fabryki danych.  

    ![Wybieranie fabryki danych](media/quickstart-create-data-factory-resource-manager-template/select-data-factory.png)
3. Na stronie fabryki danych kliknij kafelek **Monitorowanie i zarządzanie**. 

    ![Kafelek Monitorowanie i zarządzanie](media/quickstart-create-data-factory-resource-manager-template/monitor-manage-tile.png)
4. Na osobnej karcie w przeglądarce internetowej powinna zostać otwarta **aplikacja Integracja danych**. Przełącz się na **kartę monitora**, jeśli nie jest ona aktywna. Zwróć uwagę, że uruchomienie potoku zostało wyzwolone przez **wyzwalacz harmonogramu**. 

    ![Monitorowanie uruchomienia potoku](media/quickstart-create-data-factory-resource-manager-template/monitor-pipeline-run.png)    

    > [!IMPORTANT]
    > Wyświetlane uruchomienia potoku są ustawione tylko na pełne godziny (na przykład: 4:00, 5:00, 6:00 itd.). Kliknij przycisk **Odśwież** na pasku narzędzi, aby odświeżyć listę po upływie kolejnej godziny. 
5. Kliknij link w kolumnie **Akcje**. 

    ![Link akcji potoku](media/quickstart-create-data-factory-resource-manager-template/pipeline-actions-link.png)
6. Zostaną wyświetlone uruchomienia działania skojarzone z uruchomieniem potoku. W tym przewodniku Szybki start potok ma tylko jedno działanie typu Kopiowanie. Widać uruchomienie tego działania. 

    ![Uruchomienia działania](media/quickstart-create-data-factory-resource-manager-template/activity-runs.png)
1. Kliknij link w kolumnie **Dane wyjściowe**. Dane wyjściowe operacji kopiowania zostaną wyświetlone w oknie **Dane wyjściowe**. Kliknij przycisk Maksymalizuj, aby wyświetlić pełne dane wyjściowe. Zmaksymalizowane okno możesz przywrócić lub zamknąć. 

    ![Okno danych wyjściowych](media/quickstart-create-data-factory-resource-manager-template/output-window.png)
7. Po sprawdzeniu stanu uruchomienia zatrzymaj wyzwalacz. Wyzwalacz uruchamia potok co godzinę. Przy każdym uruchomieniu potok kopiuje ten sam plik z folderu wejściowego do folderu wyjściowego. Aby zatrzymać wyzwalacz, uruchom następujące polecenie w oknie programu PowerShell. 
    
    ```powershell
    Stop-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $triggerName
    ```

[!INCLUDE [data-factory-quickstart-verify-output-cleanup.md](../../includes/data-factory-quickstart-verify-output-cleanup.md)] 

## <a name="json-definitions-for-entities"></a>Definicje JSON dotyczące jednostek
Następujące jednostki usługi Data Factory są zdefiniowane w szablonie JSON: 

- [Połączona usługa Azure Storage](#azure-storage-linked-service)
- [Wejściowy zestaw danych obiektów blob platformy Azure](#azure-blob-input-dataset)
- [Wyjściowy zestaw danych obiektów blob platformy Azure](#azure-blob-output-dataset)
- [Potok danych z działaniem kopiowania](#data-pipeline)
- [Wyzwalacz](#trigger)

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
Polecenie AzureStorageLinkedService łączy konto usługi Azure Storage z fabryką danych. W ramach wymagań wstępnych utworzono kontener i przekazano dane na to konto magazynu. W tej sekcji określa się nazwę i klucz konta magazynu platformy Azure. Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure Storage zawiera temat [Połączona usługa Azure Storage](connector-azure-blob-storage.md#linked-service-properties). 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[parameters('dataFactoryName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": {
                "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]",
                "type": "SecureString"
            }
        }
    }
}
```

Parametr connectionString używa parametrów storageAccountName i storageAccountKey. Wartości tych parametrów są przekazywane przy użyciu pliku konfiguracji. Definicja używa także zmiennych azureStorageLinkedService i dataFactoryName zdefiniowanych w szablonie. 

#### <a name="azure-blob-input-dataset"></a>Wejściowy zestaw danych obiektów blob platformy Azure
Połączona usługa magazynu Azure określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z kontem magazynu Azure. W definicji zestawu danych obiektów blob Azure określane są nazwy kontenera obiektów blob, folderu i pliku, który zawiera dane wejściowe. Szczegóły dotyczące właściwości JSON używanych do definiowania zestawu danych obiektów blob platformy Azure zawiera temat [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) (Właściwości zestawu danych obiektów blob plaformy Azure). 

```json
{
    "type": "datasets",
    "name": "[variables('inputDatasetName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'), '/')]",
        "fileName": "[parameters('inputBlobName')]"
    },
    "linkedServiceName": {
        "referenceName": "[variables('azureStorageLinkedServiceName')]",
        "type": "LinkedServiceReference"
    }
    }
},

```

#### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure
Należy podać nazwę folderu usługi Azure Blob Storage, w którym są przechowywane dane skopiowane z folderu wejściowego. Szczegóły dotyczące właściwości JSON używanych do definiowania zestawu danych obiektów blob platformy Azure zawiera temat [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) (Właściwości zestawu danych obiektów blob plaformy Azure). 

```json
{
    "type": "datasets",
    "name": "[variables('outputDatasetName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'), '/')]",
        "fileName": "[parameters('outputBlobName')]"
    },
    "linkedServiceName": {
        "referenceName": "[variables('azureStorageLinkedServiceName')]",
        "type": "LinkedServiceReference"
    }
    }
}
```

#### <a name="data-pipeline"></a>Potok danych
Należy zdefiniować potok, który kopiuje dane z jednego zestawu danych obiektów blob platformy Azure do innego zestawu danych obiektów blob platformy Azure. Opisy elementów JSON używanych do definiowania potoku w tym przykładzie zawiera temat [Pipeline JSON](concepts-pipelines-activities.md#pipeline-json) (Kod JSON potoku). 

```json
{
    "type": "pipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]",
    "[variables('inputDatasetName')]",
    "[variables('outputDatasetName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "activities": [
        {
        "type": "Copy",
        "typeProperties": {
            "source": {
            "type": "BlobSource"
            },
            "sink": {
            "type": "BlobSink"
            }
        },
        "name": "MyCopyActivity",
        "inputs": [
            {
            "referenceName": "[variables('inputDatasetName')]",
            "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
            "referenceName": "[variables('outputDatasetName')]",
            "type": "DatasetReference"
            }
        ]
        }
    ]
    }
}
```

#### <a name="trigger"></a>Wyzwalacz
Należy zdefiniować wyzwalacz, który uruchamia potok co godzinę. Wdrożony wyzwalacz jest w stanie zatrzymanym. Uruchom wyzwalacz za pomocą polecenia cmdlet **Start-AzureRmDataFactoryV2Trigger**. Więcej informacji na temat wyzwalaczy zawiera artykuł [Wyzwalacze i wykonywanie potoku](concepts-pipeline-execution-triggers.md#triggers). 

```json
{
    "type": "triggers",
    "name": "[variables('triggerName')]",
    "dependsOn": [
        "[parameters('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('inputDatasetName')]",
        "[variables('outputDatasetName')]",
        "[variables('pipelineName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
        "type": "ScheduleTrigger",
        "typeProperties": {
            "recurrence": {
                "frequency": "Hour",
                "interval": 1,
                "startTime": "2017-11-28T00:00:00",
                "endTime": "2017-11-29T00:00:00",
                "timeZone": "UTC"               
            }
        },
        "pipelines": [{
            "pipelineReference": {
                "type": "PipelineReference",
                "referenceName": "ArmtemplateSampleCopyPipeline"
            },
            "parameters": {}
        }]
    }
}
```

## <a name="reuse-the-template"></a>Ponowne użycie szablonu
W ramach samouczka został utworzony szablon służący do definiowania jednostek usługi Data Factory i szablon służący do przekazywania wartości dla parametrów. Aby użyć tego samego szablonu do wdrożenia jednostek usługi Data Factory w różnych środowiskach, należy utworzyć plik parametrów dla każdego środowiska i użyć go podczas wdrażania do środowiska.     

Przykład:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Należy zauważyć, że pierwsze polecenie używa pliku parametrów dla środowiska programistycznego, drugie dla środowiska testowego, a trzecie dla środowiska produkcyjnego.  

Można także ponownie użyć szablonu do wykonywania powtarzających się zadań. Na przykład może być potrzebne utworzenie wielu fabryk danych z co najmniej jednym potokiem, które implementują tę samą logikę, lecz każda fabryka danych używa innego konta magazynu platformy Azure. W tym scenariuszu do tworzenia fabryk danych jest używany ten sam szablon w tym samym środowisku (programistycznym, testowym lub produkcyjnym) w połączeniu z różnymi plikami parametrów. 


## <a name="next-steps"></a>Następne kroki
Potok w tym przykładzie kopiuje dane z jednej lokalizacji do innej lokalizacji w usłudze Azure Blob Storage. Zapoznaj się z [samouczkami](tutorial-copy-data-dot-net.md), aby dowiedzieć się więcej o korzystaniu z usługi Data Factory w dalszych scenariuszach. 
