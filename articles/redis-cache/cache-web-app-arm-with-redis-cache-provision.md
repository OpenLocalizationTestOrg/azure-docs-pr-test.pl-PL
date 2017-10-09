---
title: "aaaProvision aplikacji sieci Web z pamięci podręcznej Redis"
description: "Użyj aplikacji sieci web toodeploy szablonu usługi Azure Resource Manager z pamięci podręcznej Redis."
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a>Tworzenie aplikacji sieci Web oraz usługi pamięć podręczna Redis przy użyciu szablonu
W tym temacie przedstawiono sposób toocreate szablonu usługi Azure Resource Manager, która wdraża aplikacji sieci Web platformy Azure z pamięcią podręczną Redis. Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

Hello pełną szablonu, zobacz [aplikacji sieci Web za pomocą szablonu usługi pamięć podręczna Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).

## <a name="what-you-will-deploy"></a>Zostanie wdrożona
W tym szablonie zostanie wdrożona:

* Aplikacja sieci Web platformy Azure
* Pamięć podręczna Azure Redis.

toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:

[![Wdrażanie tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)

## <a name="parameters-toospecify"></a>Parametry toospecify
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a>Zmienne dla nazwy
Ten szablon używa nazwy tooconstruct zmienne hello zasobów. Używa hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) funkcji tooconstruct wartość oparta na identyfikator grupy zasobów.

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a>Toodeploy zasobów
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a>Pamięć podręczna Redis
Tworzy hello pamięć podręczna Redis Azure używany z hello aplikacji sieci web. Nazwa Hello hello pamięci podręcznej została określona w hello **cacheName** zmiennej.

Szablon Hello tworzy hello pamięci podręcznej w hello tej samej lokalizacji co hello grupy zasobów.

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a>Aplikacja internetowa
Tworzy hello aplikacji sieci web o nazwie określonej w hello **podaną** zmiennej.

Należy zauważyć, że tej aplikacji sieci web hello jest skonfigurowany z aplikacją ustawienie właściwości, które ją włączyć toowork z hello pamięci podręcznej Redis. Ta aplikacja, ustawienia dynamiczne są tworzone na podstawie wartości podana podczas wdrażania.

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
