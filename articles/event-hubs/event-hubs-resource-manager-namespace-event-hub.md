---
title: "aaaCreate Azure Event Hubs przestrzeni nazw i konsumentów grupy przy użyciu szablonu | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Event Hubs przy użyciu Centrum zdarzeń i grupy odbiorców za pomocą szablonów usługi Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>Tworzenie przestrzeni nazw usługi Event Hubs z grupy koncentratora i odbiorców zdarzeń przy użyciu szablonu usługi Azure Resource Manager

W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą przestrzeni nazw typu centra zdarzeń z Centrum zdarzeń jednego i grupie użytkowników. Witaj artykuł przedstawia sposób toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager][Authoring Azure Resource Manager templates].

Hello pełną szablonu, zobacz hello [szablonu zdarzenia koncentratora i konsumentów grupy] [ Event Hub and consumer group template] w witrynie GitHub.

> [!NOTE]
> toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj usługi Event Hubs.
> 
> 

## <a name="what-will-you-deploy"></a>Co chcesz wdrożyć?
W przypadku tego szablonu zostanie wdrożona do przestrzeni nazw usługi Event Hubs z Centrum zdarzeń i grupy odbiorców.

[Centra zdarzeń](event-hubs-what-is-event-hubs.md) jest zdarzeniem przetwarzania używanej tooprovide zdarzenia i dane telemetryczne wejściowych tooAzure w bardzo dużej skali, z małymi opóźnieniami i wysoką niezawodnością.

toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:

[![Wdrażanie tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry
Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu. Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello. Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub oparte na powitania toowhich środowiska, które wdrażasz. Definiuje parametry dla wartości, które zawsze hello takie same. Każda wartość parametru szablonu hello definiuje hello zasoby, które zostały wdrożone.

Szablon Hello definiuje hello następujące parametry:

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
Nazwa Hello hello centra zdarzeń w przestrzeni nazw toocreate.

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
Nazwa Hello hello Centrum zdarzeń utworzonych w hello centra zdarzeń w przestrzeni nazw.

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
Nazwa Hello grupy konsumentów hello utworzone dla hello Centrum zdarzeń.

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
Wersja Hello interfejsu API hello szablonu.

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Toodeploy zasobów
Tworzy nazw typu **EventHubs**, z Centrum zdarzeń i grupy odbiorców.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
