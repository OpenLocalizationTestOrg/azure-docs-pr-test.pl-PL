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
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Aktualizowanie modeli uczenia maszynowego Azure przy użyciu działanie aktualizacji zasobu

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Działanie gałęzi](data-factory-hive-activity.md) 
> * [Działanie pig](data-factory-pig-activity.md)
> * [Działania MapReduce](data-factory-map-reduce.md)
> * [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Działanie Spark](data-factory-spark.md)
> * [Działanie wykonywania wsadowego w usłudze Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Działania aktualizowania zasobów w usłudze Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Działania procedur składowanych](data-factory-stored-proc-activity.md)
> * [Działania języka U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Działania niestandardowe .NET](data-factory-use-custom-activities.md)

W tym artykule uzupełnia hello głównego fabryki danych Azure - artykułu integracji usługi Azure Machine Learning: [tworzenie potoków predykcyjnej przy użyciu usługi Azure Machine Learning i fabryki danych Azure](data-factory-azure-ml-batch-execution-activity.md). Jeśli jeszcze tego nie zrobiono, przejrzyj artykuł głównego hello przed odczytaniem za pośrednictwem tego artykułu. 

## <a name="overview"></a>Omówienie
Wraz z upływem czasu hello modeli predykcyjnych w eksperymentach oceniania uczenia Maszynowego Azure hello muszą toobe retrained przy użyciu nowych baz danych wejściowych. Po wykonaniu ponownego trenowania chcesz hello tooupdate oceniania usługi sieci web z hello retrained model usługi uczenie Maszynowe. ponownego trenowania tooenable typowe etapy Hello i aktualizowanie modeli uczenia Maszynowego Azure za pośrednictwem usług sieci web są:

1. Tworzenie eksperymentu w [Azure ML Studio](https://studio.azureml.net).
2. Po zakończeniu hello modelu za pomocą usługi Azure ML Studio toopublish usług sieci web zarówno hello **eksperyment uczenia** i oceniania /**eksperyment predykcyjny**.

Witaj poniższej tabeli opisano usługi sieci web hello używane w tym przykładzie.  Zobacz [Retrain Machine Learning programowo modele](../machine-learning/machine-learning-retrain-models-programmatically.md) szczegółowe informacje.

- **Usługa sieci web szkolenia** — odbiera dane szkoleniowe i tworzy przeszkolone modeli. dane wyjściowe Hello ponownego trenowania hello jest plikiem .ilearner w magazynie obiektów Blob platformy Azure. Witaj **domyślny punkt końcowy** jest tworzona automatycznie dla podczas publikowania szkolenia hello Eksperymentując jako usługę sieci web. Można utworzyć więcej punktów końcowych, ale przykład Witaj używa tylko hello domyślnego punktu końcowego.
- **Ocenianie usługi sieci web** — odbiera przykłady bez etykiety danych i sprawia, że prognoz. dane wyjściowe Hello prognozowania może mieć różne formy, takich jak plik CSV lub wierszy w bazie danych Azure SQL, w zależności od konfiguracji hello hello eksperymentu. Hello domyślny punkt końcowy jest automatycznie utworzone po opublikowaniu hello eksperyment predykcyjny jako usługę sieci web. 

Hello poniższy rysunek przedstawia relację hello celów szkoleniowych i oceniania punktów końcowych w uczenie Maszynowe Azure.

![Usługi sieci Web](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Można wywołać hello **usługi sieci web szkolenia** przy użyciu hello **działanie wykonywania wsadowego usługi Azure ML**. Wywoływanie usługi sieci web szkolenia jest taka sama jak wywoływania usługi sieci web uczenie Maszynowe Azure (oceniania usługi sieci web) dla punktów danych. Witaj poprzedniego okładce sekcjach szczegółowo w sposób potoku tooinvoke usługi sieci web uczenie Maszynowe Azure z fabryki danych Azure. 

Można wywołać hello **oceniania usługi sieci web** przy użyciu hello **działanie usługi Azure ML aktualizacji zasobów** usługi sieci web hello tooupdate z hello nowo trenowanego modelu. Następujące przykłady Hello zawierają definicje połączonej usługi: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Ocenianie usługi sieci web to usługa sieci web klasycznego
Jeśli hello oceniania usługi sieci web jest **usługi sieci web klasycznego**, Utwórz drugi hello **punktu końcowego innych niż domyślne i nadaje się do aktualizacji** przy użyciu hello [portalu Azure](https://manage.windowsazure.com). Zobacz [tworzenie punktów końcowych](../machine-learning/machine-learning-create-endpoint.md) artykułu dla czynności. Po utworzeniu aktualizowalnych punktu końcowego innych niż domyślne hello hello następujące kroki:

* Kliknij przycisk **BATCH EXECUTION** tooget hello URI wartość hello **mlEndpoint** właściwości JSON.
* Kliknij przycisk **aktualizacji zasobów** link wartość identyfikatora URI hello tooget hello **updateResourceEndpoint** właściwości JSON. klucz interfejsu API Hello jest włączona sama strona punktu końcowego hello (w hello prawego dolnego rogu).

![można aktualizować punktu końcowego](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Hello poniższy przykład zawiera przykładowe definicji JSON hello usługi uczenie maszynowe Azure połączone. Witaj połączonej usługi używa hello apiKey do uwierzytelniania.  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Ocenianie usługi sieci web to usługa sieci web usługi Azure Resource Manager 
Jeśli usługa sieci web hello jest nowy typ hello usługi sieci web, która udostępnia punkt końcowy usługi Azure Resource Manager, nie trzeba tooadd hello drugi **innych niż domyślne** punktu końcowego. Witaj **updateResourceEndpoint** w hello połączonej usługi jest w formacie hello: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Podczas badania usługi sieci web hello na powitania można uzyskać wartości dla posiadaczy miejsce w adresie URL hello [portalu usługi sieci Web Azure Machine Learning](https://services.azureml.net/). Nowy typ Hello aktualizacja zasobu punktu końcowego, wymaga tokenu usługi AAD (Azure Active Directory). Określ **servicePrincipalId** i **servicePrincipalKey**w uczenie maszynowe Azure połączonej usługi. Zobacz [jak toocreate service principal i przypisz uprawnienia toomanage zasobów platformy Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md). Oto przykład definicji usługi uczenie maszynowe Azure połączone: 

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

Witaj następujący scenariusz zawiera więcej szczegółowych informacji. Ma przykład ponownego trenowania i aktualizowanie modeli uczenia Maszynowego Azure z potoku fabryki danych Azure.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Scenariusz: ponownego trenowania i aktualizowanie model usługi uczenie Maszynowe Azure
Ta sekcja zawiera przykładowe potok, który używa hello **działanie wykonywania wsadowego usługi uczenie Maszynowe Azure** tooretrain modelu. potok Hello używa również hello **działania usługi Azure ML aktualizacji zasobów** tooupdate hello modelu w hello oceniania usługi sieci web. Witaj sekcji znajdują się również hello fragmenty kodu JSON dla wszystkich połączonych usług, zestawy danych i potoki w przykładzie hello.

Oto widok diagramu hello hello próbki potoku. Jak widać, hello działania wykonanie partii usługi uczenie Maszynowe Azure ma hello szkolenia w danych wejściowych i szkolenia danych wyjściowych (plik iLearner). Witaj działanie usługi Azure ML aktualizacji zasobów przyjmuje te dane wyjściowe szkolenia i aktualizacje hello modelu w hello oceniania punkt końcowy usługi sieci web. Witaj działanie aktualizacji zasobu nie generuje żadnego wyniku. Hello placeholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez hello fabryki danych Azure usługa toorun hello potoku.

![diagram procesu](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Magazyn obiektów Blob Azure połączonej usługi:
Hello Azure Storage przechowuje hello następujące dane:

* danych szkoleniowych. Witaj danych wejściowych dla usługi sieci web szkolenia uczenie Maszynowe Azure hello.  
* Plik iLearner. dane wyjściowe z usługą sieci web szkolenia uczenie Maszynowe Azure hello Hello. Ten plik jest również hello wejściowych toohello działanie aktualizacji zasobu.  

Oto definicji JSON próbki hello hello połączone usługi:

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

### <a name="training-input-dataset"></a>Szkolenie wejściowy zestaw danych:
Witaj następujący zestaw danych reprezentuje hello danych wejściowych szkoleniowych dla usługi sieci web szkolenia uczenie Maszynowe Azure hello. Witaj działanie wykonywania wsadowego usługi uczenie Maszynowe Azure ma tego zestawu danych jako dane wejściowe.

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

### <a name="training-output-dataset"></a>Szkolenie wyjściowy zestaw danych:
Witaj następujący zestaw danych reprezentuje plik iLearner wyjściowy hello z usługi sieci web szkolenia uczenie Maszynowe Azure hello. Działanie wykonywania wsadowego usługi Azure ML Hello tworzy tego zestawu danych. Ten zestaw danych jest także hello wejściowych toohello działania usługi Azure ML aktualizacji zasobów.

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Połączona usługa dla punktu końcowego uczenia uczenie Maszynowe Azure
powitania po fragment kodu JSON definiuje usługę Azure Machine Learning połączone, wskazujące toohello domyślny punkt końcowy usługi sieci web szkolenia hello.

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

W **Azure ML Studio**, hello następujące wartości tooget **mlEndpoint** i **apiKey**:

1. Kliknij przycisk **usług sieci WEB** w menu po lewej stronie powitania.
2. Kliknij przycisk hello **usługi sieci web uczenie** liście hello usług sieci web.
3. Kliknij przycisk Kopiuj obok zbyt**klucz interfejsu API** pola tekstowego. Wklej klucz hello hello Schowka do edytora JSON fabryki danych hello.
4. W hello **Azure ML studio**, kliknij przycisk **BATCH EXECUTION** łącza.
5. Kopiuj hello **przez identyfikator URI żądania** z hello **żądania** sekcji i wklej go do edytora JSON fabryki danych hello.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Połączonej usługi uczenie Maszynowe Azure punktu końcowego oceniania nadaje się do aktualizacji:
powitania po fragment kodu JSON definiuje usługę Azure Machine Learning połączone, wskazujące toohello innych niż domyślne można aktualizować punkt końcowy hello oceniania usługi sieci web.  

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

### <a name="placeholder-output-dataset"></a>Symbol zastępczy wyjściowy zestaw danych:
Hello działania usługi Azure ML aktualizacji zasobów nie generuje żadnego wyniku. Fabryka danych Azure wymaga jednak wyjściowego zestawu danych toodrive hello harmonogram potoku. W związku z tym używamy zestawu manekina/symbol zastępczy danych, w tym przykładzie.  

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

### <a name="pipeline"></a>Potok
potok Hello ma dwa działania: **AzureMLBatchExecution** i **AzureMLUpdateResource**. Witaj działanie wykonywania wsadowego usługi uczenie Maszynowe Azure pobiera dane szkoleniowe hello jako dane wejściowe i tworzy plik iLearner jako dane wyjściowe. działanie Hello wywołuje usługę sieci web szkolenia hello (eksperyment uczenia udostępniony jako usługa sieci web) przy użyciu danych wejściowych hello szkolenia danych i odbiera plik ilearner hello z hello Usługa sieci Web. Hello placeholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez hello fabryki danych Azure usługa toorun hello potoku.

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
