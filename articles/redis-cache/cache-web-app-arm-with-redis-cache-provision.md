---
title: "Zainicjuj obsługę aplikacji sieci Web z pamięci podręcznej Redis"
description: "Szablon usługi Azure Resource Manager umożliwia wdrażanie aplikacji sieci web z pamięci podręcznej Redis."
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
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="43eb3-103">Tworzenie aplikacji sieci Web oraz usługi pamięć podręczna Redis przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="43eb3-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="43eb3-104">W tym temacie dowiesz się, jak utworzyć szablon usługi Azure Resource Manager, która wdraża aplikacji sieci Web platformy Azure z pamięcią podręczną Redis.</span><span class="sxs-lookup"><span data-stu-id="43eb3-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="43eb3-105">Dowiesz się, jak do definiowania zasobów, do których są wdrażane i sposób definiowania parametrów, które są określone, gdy wdrożenie jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="43eb3-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="43eb3-106">Można użyć tego szablonu na potrzeby własnych wdrożeń lub dostosować go do konkretnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="43eb3-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="43eb3-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="43eb3-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="43eb3-108">Zakończenie szablonu, zobacz [aplikacji sieci Web za pomocą szablonu usługi pamięć podręczna Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="43eb3-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="43eb3-109">Zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="43eb3-109">What you will deploy</span></span>
<span data-ttu-id="43eb3-110">W tym szablonie zostanie wdrożona:</span><span class="sxs-lookup"><span data-stu-id="43eb3-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="43eb3-111">Aplikacja sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43eb3-111">Azure Web App</span></span>
* <span data-ttu-id="43eb3-112">Pamięć podręczna Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="43eb3-112">Azure Redis Cache.</span></span>

<span data-ttu-id="43eb3-113">Aby automatycznie uruchomić wdrożenie, kliknij poniższy przycisk:</span><span class="sxs-lookup"><span data-stu-id="43eb3-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="43eb3-114">[![Wdrażanie na platformie Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="43eb3-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="43eb3-115">W celu określenia</span><span class="sxs-lookup"><span data-stu-id="43eb3-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="43eb3-116">Zmienne dla nazwy</span><span class="sxs-lookup"><span data-stu-id="43eb3-116">Variables for names</span></span>
<span data-ttu-id="43eb3-117">Ten szablon używa zmiennych do konstruowania nazwy dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="43eb3-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="43eb3-118">Używa [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) funkcji, aby utworzyć wartość oparte na identyfikator grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="43eb3-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="43eb3-119">Zasoby wymagające wdrożenia</span><span class="sxs-lookup"><span data-stu-id="43eb3-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="43eb3-120">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="43eb3-120">Redis Cache</span></span>
<span data-ttu-id="43eb3-121">Tworzy pamięć podręczna Redis Azure używany w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="43eb3-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="43eb3-122">Nazwa pamięci podręcznej została określona w **cacheName** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="43eb3-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="43eb3-123">Szablon tworzy pamięci podręcznej w tej samej lokalizacji co grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="43eb3-123">The template creates the cache in the same location as the resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="43eb3-124">Aplikacja internetowa</span><span class="sxs-lookup"><span data-stu-id="43eb3-124">Web app</span></span>
<span data-ttu-id="43eb3-125">Tworzenie aplikacji sieci web o nazwie określonej w **podaną** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="43eb3-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="43eb3-126">Zwróć uwagę, że aplikacji sieci web jest skonfigurowany z właściwościami ustawienie aplikacji, które było w stanie pracy w pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="43eb3-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="43eb3-127">Ta aplikacja, ustawienia dynamiczne są tworzone na podstawie wartości podana podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="43eb3-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="43eb3-128">Polecenia umożliwiające uruchomienie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="43eb3-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="43eb3-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43eb3-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="43eb3-130">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43eb3-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
