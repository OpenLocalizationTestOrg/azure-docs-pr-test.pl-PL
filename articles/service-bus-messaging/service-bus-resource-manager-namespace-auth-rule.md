---
title: "reguły autoryzacji usługi Service Bus aaaCreate przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Utworzyć regułę autoryzacji usługi Service Bus dla przestrzeni nazw i kolejki przy użyciu szablonu usługi Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a>Utworzyć regułę autoryzacji usługi Service Bus dla przestrzeni nazw i kolejki przy użyciu szablonu usługi Azure Resource Manager

W tym artykule przedstawiono sposób toouse szablonu usługi Azure Resource Manager, który tworzy [reguły autoryzacji](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) dla przestrzeni nazw usługi Service Bus i kolejki. Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].

Hello pełną szablonu, zobacz hello [szablonu reguły autoryzacji usługi Service Bus] [ Service Bus auth rule template] w witrynie GitHub.

> [!NOTE]
> Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.
> 
> * [Tworzenie przestrzeni nazw usługi Service Bus](service-bus-resource-manager-namespace.md)
> * [Tworzenie przestrzeni nazw usługi Service Bus z kolejki](service-bus-resource-manager-namespace-queue.md)
> * [Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji](service-bus-resource-manager-namespace-topic.md)
> * [Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj "Service Bus".
> 
> 

## <a name="what-will-you-deploy"></a>Co chcesz wdrożyć?
W przypadku tego szablonu zostanie wdrożona regułę autoryzacji usługi Service Bus dla przestrzeni nazw i jednostki obsługi komunikatów (w tym przypadku kolejki).

Ten szablon używa [dostępu sygnatury dostępu Współdzielonego](service-bus-sas.md) do uwierzytelniania. Sygnatury dostępu Współdzielonego umożliwia aplikacji tooauthenticate tooService magistrali przy użyciu klawisza dostępu skonfigurowane na powitania przestrzeni nazw lub na powitania wiadomości jednostki (kolejka lub temat) określone prawa, które są skojarzone. Następnie można użyć tego klucza toogenerate tokenu sygnatury dostępu Współdzielonego, którego klienci mogą z kolei używać tooService tooauthenticate magistrali.

toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:

[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)

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

### <a name="namespaceauthorizationrulename"></a>namespaceAuthorizationRuleName
Witaj Nazwa reguły autoryzacji hello hello przestrzeni nazw.

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
Nazwa Hello kolejki hello w przestrzeni nazw usługi Service Bus hello.

```json
"serviceBusQueueName": {
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
Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**i reguły autoryzacji usługi Service Bus dla przestrzeni nazw i jednostek.

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Następne kroki
Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeglądając następujące artykuły:

* [Zarządzanie usługi Service Bus przy użyciu programu PowerShell](service-bus-powershell-how-to-provision.md)
* [Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [Magistrala usług uwierzytelniania i autoryzacji](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
