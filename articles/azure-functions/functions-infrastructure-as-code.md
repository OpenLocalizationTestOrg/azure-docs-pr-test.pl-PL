---
title: "Wdrażanie zasobu aaaAutomate aplikacji funkcji w funkcji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobuild szablonu usługi Azure Resource Manager, która wdraża aplikację funkcji."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure funkcje, funkcje, niekorzystającą architektury infrastruktury jako usługi kodu usługi azure resource manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Automatyzacji wdrażania zasobów dla aplikacji funkcja na usługi Azure Functions

Możesz użyć usługi Azure Resource Manager toodeploy szablonu aplikacji funkcji. W tym artykule opisano hello wymaganych zasobów i parametrów w ten sposób. Może być konieczne dodatkowe zasoby toodeploy, w zależności od hello [wyzwalaczy i powiązań](functions-triggers-bindings.md) w funkcji aplikacji.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Na przykład szablony Zobacz:
- [funkcji aplikacji w planie zużycie]
- [funkcji aplikacji w planie usługi aplikacji Azure]

## <a name="required-resources"></a>Wymagane zasoby

Aplikacja funkcji wymaga tych zasobów:

* [Usługi Azure Storage](../storage/index.md) konta
* Plan hostingu (użycie planu lub plan usługi aplikacji)
* Aplikacja — funkcja 

### <a name="storage-account"></a>Konto magazynu

Konto magazynu platformy Azure jest wymagany dla funkcji aplikacji. Musisz mieć konto ogólnego przeznaczenia, który obsługuje obiekty BLOB, tabel, kolejek i plików. Aby uzyskać więcej informacji, zobacz [wymagania dotyczące konta magazynu usługi Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Ponadto hello właściwości `AzureWebJobsStorage` i `AzureWebJobsDashboard` muszą być określone jako ustawienia aplikacji hello konfiguracji lokacji. środowisko wykonawcze usługi Azure Functions Hello używa hello `AzureWebJobsStorage` toocreate wewnętrzne kolejki parametrów połączenia. Witaj parametry połączenia `AzureWebJobsDashboard` jest używane toolog tooAzure tabeli magazynu i mocy hello **Monitor** kartę w portalu hello.

Te właściwości są określone w hello `appSettings` kolekcji w hello `siteConfig` obiektu:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Plan hostingu

Definicja Hello hello plan hostingu różni się w zależności od tego, czy używasz planu zużycia lub usługi aplikacji. Zobacz [wdrażanie aplikacji funkcji w planie zużycie hello](#consumption) i [wdrażanie aplikacji na powitania planu usługi aplikacji — funkcja](#app-service-plan).

### <a name="function-app"></a>Funkcja aplikacji

zasób aplikacji Hello funkcja jest definiowana za pomocą zasobu typu **Microsoft.Web/Site** i rodzaj **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Wdrażanie aplikacji na powitania użycie planu — funkcja

Można uruchomić aplikacji funkcji w dwóch różnych trybach: hello planowania użycia i hello planu usługi aplikacji. plan zużycie Hello automatycznie przydzieli moc obliczeniową po kodzie działa, skaluje się jako niezbędne toohandle obciążenia i następnie skalowany w dół, gdy kodu nie jest uruchomiona. Tak nie masz toopay bezczynnych maszyn wirtualnych, a nie ma zdolności tooreserve z wyprzedzeniem. toolearn więcej informacji na temat hostingu planów, zobacz [planów Azure — użytek funkcje i usługi aplikacji](functions-scale.md).

Aby uzyskać przykładowy szablon usługi Azure Resource Manager, zobacz [funkcji aplikacji w planie zużycie].

### <a name="create-a-consumption-plan"></a>Tworzenie planu zużycie

Plan zużycie jest specjalny typ zasobu "serverfarm". Należy określić przy użyciu hello `Dynamic` wartość hello `computeMode` i `sku` właściwości:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji

Ponadto planu zużycie wymaga dwóch dodatkowych ustawień konfiguracji lokacji hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` i `WEBSITE_CONTENTSHARE`. Te właściwości skonfiguruj hello magazynu konta i ścieżce pliku przechowywania kodu aplikacji hello funkcji i konfiguracji.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Wdrażanie aplikacji na powitania planu usługi aplikacji — funkcja

W hello planu usługi aplikacji aplikacji funkcja działa na dedykowanych maszynach wirtualnych na podstawowa, standardowa i Premium jednostki SKU, podobne tooweb aplikacji. Aby uzyskać szczegółowe informacje dotyczące sposobu działania hello planu usługi App Service, zobacz hello [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Aby uzyskać przykładowy szablon usługi Azure Resource Manager, zobacz [funkcji aplikacji w planie usługi aplikacji Azure].

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji 

Po wybraniu opcji skalowania tworzenia aplikacji funkcji. Aplikacja Hello jest hello kontener, który zawiera wszystkie funkcje.

Aplikacja funkcji ma wiele zasoby podrzędne używane w danym wdrożeniu, w tym ustawienia aplikacji i opcje kontroli źródła. Możesz również wybrać tooremove hello **sourcecontrols** zasobu podrzędnego i użyj innego [opcji wdrażania](functions-continuous-deployment.md) zamiast tego.

> [!IMPORTANT]
> toosuccessfully wdrażanie aplikacji przy użyciu usługi Azure Resource Manager, jest ważne toounderstand wdrażanie zasobów na platformie Azure. W hello poniższy przykład, najwyższego poziomu konfiguracji są stosowane przy użyciu **siteConfig**. Jest ważne tooset poziomu te konfiguracje u góry, ponieważ ich przedstawienia informacji toohello funkcji środowiska uruchomieniowego i wdrażania aparat. Przed elementem podrzędnym hello jest wymaganych informacji najwyższego poziomu **sourcecontrols/sieci web** zasobów są stosowane. Chociaż jest to możliwe tooconfigure tych ustawień w hello podrzędnymi **config/appSettings** zasobów, w niektórych przypadkach należy wdrożyć aplikację funkcja *przed* **config/appSettings**  została zastosowana. Na przykład w przypadku używania funkcji z [Logic Apps](../logic-apps/index.md), funkcji są zależność innego zasobu.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Ten szablon używa hello [projektu](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) wartość ustawienia aplikacji, która ustawia hello podstawowego katalogu, w którym hello aparat wdrażania funkcji (Kudu) wyszukuje kodu do wdrożenia. W naszym repozytorium naszej funkcji znajdują się w podfolderze hello **src** folderu. Tak, w hello poprzedzających przykład, możemy ustawić wartość ustawienia aplikacji hello także`src`. Jeśli funkcji znajdują się w katalogu głównego repozytorium hello, lub jeśli nie są wdrażane z kontroli źródła, możesz usunąć tę wartość ustawienia aplikacji.

## <a name="deploy-your-template"></a>Wdrażanie szablonu

Można użyć dowolnego hello następujące sposoby toodeploy szablonu:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Interfejs wiersza polecenia platformy Azure](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Witryna Azure Portal](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [Interfejs API REST](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>TooAzure przycisk Wdrażaj

Zastąp ```<url-encoded-path-to-azuredeploy-json>``` z [zakodowane w adresie URL](https://www.bing.com/search?q=url+encode) wersji hello ścieżka pierwotnych z `azuredeploy.json` pliku w witrynie GitHub.

Oto przykład, który używa języka znaczników markdown:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

Oto przykład, który używa HTML:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat toodevelop i konfigurowanie usługi Azure Functions.

* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)
* [Jak tooconfigure Azure funkcji ustawień aplikacji](functions-how-to-use-azure-function-app-settings.md)
* [Tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md)

<!-- LINKS -->

[funkcji aplikacji w planie zużycie]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[funkcji aplikacji w planie usługi aplikacji Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
