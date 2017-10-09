---
title: "aaaCreate Azure Service Bus przestrzeni nazw subskrypcję tematu przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji przy użyciu szablonu Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a>Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji przy użyciu szablonu usługi Azure Resource Manager

W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą przestrzeni nazw usługi Service Bus i tematu i subskrypcji w ramach tego obszaru nazw. Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].

Hello pełną szablonu, zobacz hello [przestrzeni nazw usługi Service Bus z tematów i subskrypcji] [ Service Bus namespace with topic and subscription] szablonu.

> [!NOTE]
> Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.
> 
> * [Tworzenie przestrzeni nazw usługi Service Bus](service-bus-resource-manager-namespace.md)
> * [Tworzenie przestrzeni nazw usługi Service Bus z kolejki](service-bus-resource-manager-namespace-queue.md)
> * [Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji](service-bus-resource-manager-namespace-auth-rule.md)
> * [Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj "Service Bus".
> 
> 

## <a name="what-will-you-deploy"></a>Co chcesz wdrożyć?

W przypadku tego szablonu zostanie wdrożona przestrzeni nazw usługi Service Bus z tematów i subskrypcji.

[Tematy usługi Service Bus i subskrypcje](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) Podaj jeden do wielu formę komunikacji w *publikowania/subskrypcji* wzorca.

toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:

[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry

Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu. Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello. Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z. Definiuje parametry dla wartości, które będą zawsze hello takie same. Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.

Szablon Hello definiuje hello następujące parametry.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
Nazwa Hello toocreate przestrzeni nazw usługi Service Bus hello.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
Nazwa Hello tematu hello utworzone w przestrzeni nazw usługi Service Bus hello.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
Nazwa Hello subskrypcji hello utworzone w przestrzeni nazw usługi Service Bus hello.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
wersja interfejsu API usługi Service Bus Hello hello szablonu.

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a>Toodeploy zasobów
Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**, tematu i subskrypcji.

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a>Następne kroki
Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeglądając następujące artykuły:

* [Zarządzanie usługi Service Bus przy użyciu programu PowerShell](service-bus-manage-with-ps.md)
* [Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
