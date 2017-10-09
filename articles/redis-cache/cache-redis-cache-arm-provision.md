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
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="418b5-103">Tworzenie pamięci podręcznej Redis przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="418b5-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="418b5-104">W tym temacie omówiono sposób toocreate szablonu usługi Azure Resource Manager, która wdraża pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="418b5-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="418b5-105">Witaj w pamięci podręcznej może służyć z istniejącego magazynu konta tookeep danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="418b5-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="418b5-106">Możesz także dowiedzieć się, jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="418b5-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="418b5-107">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="418b5-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="418b5-108">Obecnie ustawień diagnostycznych są udostępniane dla wszystkich usług pamięć podręczna w hello tym samym regionie, w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="418b5-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="418b5-109">Aktualizacja jednej pamięci podręcznej w regionie hello ma wpływ na wszystkie inne pamięci podręcznych w regionie hello.</span><span class="sxs-lookup"><span data-stu-id="418b5-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="418b5-110">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="418b5-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="418b5-111">Hello pełną szablonu, zobacz [szablonu pamięci podręcznej Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="418b5-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="418b5-112">Szablony Menedżera zasobów dla nowych hello [warstwy Premium](cache-premium-tier-intro.md) są dostępne.</span><span class="sxs-lookup"><span data-stu-id="418b5-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="418b5-113">Tworzenie pamięci podręcznej Redis Premium z klastra</span><span class="sxs-lookup"><span data-stu-id="418b5-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="418b5-114">Tworzenie z trwałości danych pamięci podręcznej Redis w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="418b5-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="418b5-115">Tworzenie pamięci podręcznej Redis w warstwie Premium z sieci wirtualnej i opcjonalnie klastra</span><span class="sxs-lookup"><span data-stu-id="418b5-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="418b5-116">toocheck hello najnowsze szablonów, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) i wyszukaj `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="418b5-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="418b5-117">Zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="418b5-117">What you will deploy</span></span>
<span data-ttu-id="418b5-118">W tym szablonie wdroży pamięć podręczna Redis Azure używającej istniejącego konta magazynu dla danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="418b5-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="418b5-119">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="418b5-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="418b5-120">[![Wdrażanie tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="418b5-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="418b5-121">Parametry</span><span class="sxs-lookup"><span data-stu-id="418b5-121">Parameters</span></span>
<span data-ttu-id="418b5-122">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="418b5-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="418b5-123">Szablon Hello zawiera sekcji parametrów zawierający wszystkie hello wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="418b5-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="418b5-124">Należy zdefiniować parametr dla tych wartości, które różnią się na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="418b5-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="418b5-125">Definiuje parametry dla wartości, które zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="418b5-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="418b5-126">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="418b5-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="418b5-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="418b5-127">redisCacheLocation</span></span>
<span data-ttu-id="418b5-128">Lokalizacja Hello hello pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="418b5-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="418b5-129">Aby uzyskać najlepszą wydajność, użyj hello sam lokalizacji jako hello używane z pamięci podręcznej hello toobe aplikacji.</span><span class="sxs-lookup"><span data-stu-id="418b5-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="418b5-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="418b5-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="418b5-131">Witaj nazwa hello istniejących toouse konto magazynu diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="418b5-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="418b5-132">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="418b5-132">enableNonSslPort</span></span>
<span data-ttu-id="418b5-133">Wartość logiczna, która wskazuje, czy tooallow dostęp za pośrednictwem portów bez użycia protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="418b5-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="418b5-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="418b5-134">diagnosticsStatus</span></span>
<span data-ttu-id="418b5-135">Wartość, która wskazuje, czy włączono diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="418b5-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="418b5-136">Użyj wartości ON lub OFF.</span><span class="sxs-lookup"><span data-stu-id="418b5-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="418b5-137">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="418b5-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="418b5-138">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="418b5-138">Redis Cache</span></span>
<span data-ttu-id="418b5-139">Tworzy hello pamięć podręczna Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="418b5-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="418b5-140">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="418b5-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="418b5-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="418b5-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="418b5-142">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="418b5-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


