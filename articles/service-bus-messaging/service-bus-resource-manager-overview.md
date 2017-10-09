---
title: "zasoby usługi Azure Service Bus aaaCreate przy użyciu szablonów usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Używanie usługi Azure Resource Manager szablony tooautomate hello tworzenia zasobów usługi Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Tworzenie zasobów usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager

W tym artykule opisano sposób toocreate i wdrażanie zasobów usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager, programu PowerShell i dostawcy zasobów usługi Service Bus hello.

Szablony usługi Azure Resource Manager pomagają zdefiniować hello toodeploy zasobów dla rozwiązania i toospecify parametry i zmienne, które pozwalają tooinput wartości dla różnych środowisk. Szablon Hello składa się z kodu JSON i wyrażeń, że możesz użyć wartości tooconstruct dla danego wdrożenia. Aby uzyskać szczegółowe informacje na temat pisania szablonów usługi Azure Resource Manager oraz omówienie formacie szablonu hello, zobacz [struktury i składni szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> jak Hello przykłady w tym artykule Pokaż toouse Azure Resource Manager toocreate przestrzeni nazw usługi Service Bus i jednostek (kolejki) wiadomości. Inne przykłady szablonów można znaleźć hello [galerię szablonów Szybki Start Azure] [ Azure Quickstart Templates gallery] i wyszukaj "Service Bus".
>
>

## <a name="service-bus-resource-manager-templates"></a>Szablony Menedżera zasobów magistrali usług

Te szablony usługi magistrali usługi Azure Resource Manager są dostępne do pobrania i wdrożenia. Kliknij hello następującego łącza Aby uzyskać szczegółowe informacje o każdym z nich, przy użyciu łącza toohello szablonów w witrynie GitHub:

* [Tworzenie przestrzeni nazw usługi Service Bus](service-bus-resource-manager-namespace.md)
* [Tworzenie przestrzeni nazw usługi Service Bus z kolejki](service-bus-resource-manager-namespace-queue.md)
* [Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji](service-bus-resource-manager-namespace-topic.md)
* [Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji](service-bus-resource-manager-namespace-auth-rule.md)
* [Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Wdrażanie przy użyciu programu PowerShell

Hello Poniższa procedura opisuje sposób toouse PowerShell toodeploy szablonu usługi Azure Resource Manager tworzącą **standardowe** warstwy przestrzeń nazw magistrali usług i kolejką w tej przestrzeni nazw. Ten przykład jest oparty na powitania [tworzenie przestrzeni nazw usługi Service Bus z kolejką](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) szablonu. Witaj przybliżonej przepływu pracy jest następujący:

1. Instalowanie programu PowerShell.
2. Utwórz szablon hello i (opcjonalnie) pliku parametrów.
3. W programie PowerShell Zaloguj się za tooyour konto platformy Azure.
4. Utwórz nową grupę zasobów, jeśli jeszcze nie istnieje.
5. Testowanie wdrażania hello.
6. W razie potrzeby można ustawić trybu wdrożenia hello.
7. Wdrażanie szablonu hello.

Aby uzyskać pełne informacje na temat wdrażania szablonów usługi Azure Resource Manager, zobacz [wdrożenie zasobów przy użyciu szablonów usługi Azure Resource Manager][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>Instalowanie programu PowerShell

Zainstaluj program Azure PowerShell, wykonując instrukcje hello w [wprowadzenie do programu Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Tworzenie szablonu

Witaj w klonowania lub kopiowanie [201 magistrali usług — Tworzenie kolejki](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) szablonu z serwisu GitHub:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Utwórz plik parametrów (opcjonalnie)

toouse pliku następujące parametry opcjonalne hello kopiowania [201 magistrali usług — Tworzenie kolejki](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) pliku. Zastąp wartość hello `serviceBusNamespaceName` o nazwie hello przestrzeni nazw usługi Service Bus hello toocreate w tym wdrożeniu, a następnie zastąp wartości hello `serviceBusQueueName` o nazwie hello kolejki hello ma toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz hello [parametry](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tematu.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Zaloguj się za tooAzure i ustawić hello subskrypcji platformy Azure

Uruchom hello następujące polecenie z wiersza polecenia programu PowerShell:

```powershell
Login-AzureRmAccount
```

Jesteś zostanie wyświetlony monit o toolog na tooyour konto platformy Azure. Po zalogowaniu, uruchom następujące polecenie tooview hello dostępnych subskrypcji.

```powershell
Get-AzureRMSubscription
```

To polecenie zwraca listę dostępnych subskrypcji platformy Azure. Wybierz subskrypcję dla hello bieżącej sesji, uruchamiając następujące polecenie hello. Zastąp `<YourSubscriptionId>` z hello identyfikatora GUID dla hello subskrypcji platformy Azure ma toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Witaj grupy zasobów

Jeśli nie masz istniejący zasób grupy, Utwórz nową grupę zasobów o hello ** New-AzureRmResourceGroup ** polecenia. Podaj nazwę grupy zasobów hello i lokalizację toouse hello. Na przykład:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

Jeśli to się powiedzie, zostanie wyświetlone podsumowanie hello nowej grupy zasobów.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Testowe wdrożenie na powitania

Sprawdzanie poprawności wdrożenia, uruchamiając hello `Test-AzureRmResourceGroupDeployment` polecenia cmdlet. Podczas testowania wdrożenia hello, należy podać parametry, dokładnie tak jak w przypadku wykonywania hello wdrożenia.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Tworzenie wdrożenia hello

toocreate hello nowe wdrożenie, uruchom hello `New-AzureRmResourceGroupDeployment` polecenia cmdlet i podaj niezbędne parametry powitania po wyświetleniu monitu. Parametry Hello obejmować nazwę dla danego wdrożenia hello nazwy grupy zasobów i ścieżka hello lub pliku szablonu toohello adresu URL. Jeśli hello **tryb** parametr nie zostanie określony, hello wartość domyślną **przyrostowe** jest używany. Aby uzyskać więcej informacji, zobacz [przyrostowe i pełne wdrożeń](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Witaj następujących wierszy polecenia można hello trzech parametrów w oknie programu PowerShell hello:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify pliku parametrów zamiast tego należy użyć następującego polecenia hello.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

Umożliwia także parametry wbudowanego po uruchomieniu polecenia cmdlet wdrażania hello. polecenie Hello jest następujący:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun [pełną](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) wdrożenia, zestaw hello **tryb** parametru zbyt**Complete**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Sprawdź hello wdrożenia
Jeśli pomyślnie są wdrażane zasoby hello, w oknie programu PowerShell hello zostanie wyświetlone podsumowanie wdrożenia hello:

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Następne kroki
Teraz przedstawiono podstawowy przepływ pracy hello i polecenia służące do wdrażania szablonu usługi Azure Resource Manager. Aby uzyskać szczegółowe informacje odwiedź hello następującego łącza:

* [Omówienie usługi Azure Resource Manager][Azure Resource Manager overview]
* [Wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
