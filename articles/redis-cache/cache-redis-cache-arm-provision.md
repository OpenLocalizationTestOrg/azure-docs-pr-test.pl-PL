---
title: "aaaProvision pamięci podręcznej Redis przy użyciu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager szablonu toodeploy pamięć podręczna Redis Azure."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Tworzenie pamięci podręcznej Redis przy użyciu szablonu
W tym temacie omówiono sposób toocreate szablonu usługi Azure Resource Manager, która wdraża pamięci podręcznej Redis Azure. Witaj w pamięci podręcznej może służyć z istniejącego magazynu konta tookeep danych diagnostycznych. Możesz także dowiedzieć się, jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.

Obecnie ustawień diagnostycznych są udostępniane dla wszystkich usług pamięć podręczna w hello tym samym regionie, w ramach subskrypcji. Aktualizacja jednej pamięci podręcznej w regionie hello ma wpływ na wszystkie inne pamięci podręcznych w regionie hello.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

Hello pełną szablonu, zobacz [szablonu pamięci podręcznej Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Szablony Menedżera zasobów dla nowych hello [warstwy Premium](cache-premium-tier-intro.md) są dostępne. 
> 
> * [Tworzenie pamięci podręcznej Redis Premium z klastra](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Tworzenie z trwałości danych pamięci podręcznej Redis w warstwie Premium](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Tworzenie pamięci podręcznej Redis w warstwie Premium z sieci wirtualnej i opcjonalnie klastra](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck hello najnowsze szablonów, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) i wyszukaj `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Zostanie wdrożona
W tym szablonie wdroży pamięć podręczna Redis Azure używającej istniejącego konta magazynu dla danych diagnostycznych.

toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:

[![Wdrażanie tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry
Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu. Szablon Hello zawiera sekcji parametrów zawierający wszystkie hello wartości parametrów.
Należy zdefiniować parametr dla tych wartości, które różnią się na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z. Definiuje parametry dla wartości, które zawsze hello takie same. Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
Lokalizacja Hello hello pamięci podręcznej Redis. Aby uzyskać najlepszą wydajność, użyj hello sam lokalizacji jako hello używane z pamięci podręcznej hello toobe aplikacji.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
Witaj nazwa hello istniejących toouse konto magazynu diagnostyki. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>EnableNonSslPort
Wartość logiczna, która wskazuje, czy tooallow dostęp za pośrednictwem portów bez użycia protokołu SSL.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Wartość, która wskazuje, czy włączono diagnostyki. Użyj wartości ON lub OFF.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Toodeploy zasobów
### <a name="redis-cache"></a>Pamięć podręczna Redis
Tworzy hello pamięć podręczna Redis Azure.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


