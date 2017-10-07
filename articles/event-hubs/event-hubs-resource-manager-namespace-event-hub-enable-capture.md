---
title: "przestrzeń nazw usługi Azure Event Hubs i włączyć funkcję przechwytywania przy użyciu szablonu aaaCreate | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Azure Event Hubs z jednym centrum zdarzeń i włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Tworzenie przestrzeni nazw usługi Event Hubs z centrum zdarzeń i włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager

W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą centra zdarzeń w przestrzeni nazw z wystąpieniem koncentratora jedno zdarzenie, a także umożliwia hello [funkcja przechwytywania](event-hubs-capture-overview.md) na powitania Centrum zdarzeń. Witaj artykule opisano sposób toodefine zasobów, do których są wdrażane i jak toodefine parametrów, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.

Artykuł przedstawia sposób toospecify przechwytywania zdarzeń w obiektach blob magazynu Azure lub usługi Azure Data Lake Store oparte na powitania docelowym.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager][Authoring Azure Resource Manager templates].

Aby uzyskać więcej informacji na temat praktycznych rozwiązań i wzorców dotyczących konwencji nazewnictwa zasobów platformy Azure, zobacz [Azure Resources Naming Conventions (Konwencje nazewnictwa zasobów platformy Azure)][Azure Resources naming conventions].

Dla szablonów pełną hello kliknij hello następującego łącza GitHub:

- [Centrum i włączyć funkcję przechwytywania tooStorage szablonu zdarzenia][Event Hub and enable Capture tooStorage template] 
- [Centrum i włączyć funkcję przechwytywania tooAzure usługi Data Lake Store szablonu zdarzenia][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj usługi Event Hubs.
> 
> 

## <a name="what-will-you-deploy"></a>Co chcesz wdrożyć?

Ten szablon umożliwia wdrożenie przestrzeni nazw usługi Event Hubs z centrum zdarzeń oraz włączenie [funkcji przechwytywania usługi Event Hubs](event-hubs-capture-overview.md).

[Centra zdarzeń](event-hubs-what-is-event-hubs.md) jest zdarzeniem przetwarzania używanej tooprovide zdarzenia i dane telemetryczne wejściowych tooAzure w bardzo dużej skali, z małymi opóźnieniami i wysoką niezawodnością. Zdarzenie koncentratory przechwytywania umożliwia tooautomatically należy dostarczyć hello przesyłanie strumieniowe danych w magazynie obiektów Blob tooAzure centra zdarzeń lub usługi Azure Data Lake Store, w ramach określonego rozmiaru czasowych lub wybrane.

Kliknij powitania po tooenable przycisku przechwytywania centra zdarzeń do usługi Azure Storage:

[![Wdrażanie tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Kliknij powitania po tooenable przycisku przechwytywania centra zdarzeń do usługi Azure Data Lake Store:

[![Wdrażanie tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry

Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu. Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello. Należy zdefiniować parametr dla tych wartości, które różnią się na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z. Definiuje parametry dla wartości, które zawsze hello takie same. Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.

Szablon Hello definiuje hello następujące parametry.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

Nazwa Hello hello [przestrzeni nazw usługi Event Hubs](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

Nazwa Hello hello Centrum zdarzeń utworzonych w hello [przestrzeni nazw usługi Event Hubs](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

Witaj liczba dni wiadomości powitania tooretain w Centrum zdarzeń hello. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

Liczba Hello toocreate partycji w Centrum zdarzeń hello.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Włącz przechwytywanie na powitania Centrum zdarzeń.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

Określ dane zdarzeń hello tooserialize format kodowania Hello.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

Interwał czasu Hello, w którym przechwytywania centra zdarzeń rozpoczyna się przechwytywanie danych hello.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
rozmiar interwału powitania jaką przechwytywania uruchamia przechwytywanie danych hello.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

format nazwy Hello używane przez pliki Avro hello toowrite przechwytywania centrów zdarzeń. Format nazwy funkcji przechwytywania musi zawierać pola `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` i `{Second}`. Mogą one być uporządkowane w dowolnej kolejności z ogranicznikami lub bez nich.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

Wersja Hello interfejsu API hello szablonu.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Użyj hello następujące parametry, jeżeli wybierz magazyn Azure jako lokalizacja docelowa.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Przechwytywanie wymaga się, że konto usługi Azure Storage zasobów tooenable identyfikator Przechwytywanie tooyour żądanego konta magazynu.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Witaj kontenera obiektów blob, w którym toocapture danych zdarzenia.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Użyj hello następujące parametry, jeżeli wybierzesz Azure Data Lake Store jako lokalizacja docelowa. Należy ustawić uprawnienia w ścieżce usługi Data Lake Store, w której ma zostać tooCapture hello zdarzeń. Zobacz uprawnienia tooset [w tym artykule](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

Identyfikator subskrypcji dla przestrzeni nazw usługi Event Hubs hello i usługi Azure Data Lake Store. Oba te zasoby muszą znajdować się pod hello tego samego identyfikatora subskrypcji.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

nazwę usługi Azure Data Lake Store Hello hello przechwycić zdarzeń.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

Ścieżka folderu docelowego Hello hello przechwycić zdarzeń.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy zasobów usługi Azure Storage jako miejsce docelowe toocaptured zdarzenia

Tworzy nazw typu **EventHubs**, z Centrum zdarzeń jednej, a także umożliwia przechwytywanie tooAzure magazynu obiektów Blob.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Toodeploy zasobów dla usługi Azure Data Lake Store jako miejsce docelowe

Tworzy nazw typu **EventHubs**, z Centrum zdarzeń jednej, a także umożliwia przechwytywanie tooAzure Data Lake Store.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Wdrażanie sieci tooenable szablonu przechwytywania centra zdarzeń w magazynie Azure:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Wdrażanie sieci tooenable szablonu przechwytywania centra zdarzeń do usługi Azure Data Lake Store:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Wybieranie usługi Azure Blob Storage jako lokalizacji docelowej:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Wybieranie usługi Azure Data Lake Store jako lokalizacji docelowej:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Następne kroki

Można również skonfigurować przechwytywania centra zdarzeń za pomocą hello [portalu Azure](https://portal.azure.com). Aby uzyskać więcej informacji, zobacz [włączyć przechwytywania centra zdarzeń przy użyciu hello portalu Azure](event-hubs-capture-enable-through-portal.md).

Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
