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
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="330a0-103">Tworzenie aplikacji sieci Web oraz usługi pamięć podręczna Redis przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="330a0-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="330a0-104">W tym temacie przedstawiono sposób toocreate szablonu usługi Azure Resource Manager, która wdraża aplikacji sieci Web platformy Azure z pamięcią podręczną Redis.</span><span class="sxs-lookup"><span data-stu-id="330a0-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="330a0-105">Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="330a0-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="330a0-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="330a0-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="330a0-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="330a0-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="330a0-108">Hello pełną szablonu, zobacz [aplikacji sieci Web za pomocą szablonu usługi pamięć podręczna Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="330a0-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="330a0-109">Zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="330a0-109">What you will deploy</span></span>
<span data-ttu-id="330a0-110">W tym szablonie zostanie wdrożona:</span><span class="sxs-lookup"><span data-stu-id="330a0-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="330a0-111">Aplikacja sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="330a0-111">Azure Web App</span></span>
* <span data-ttu-id="330a0-112">Pamięć podręczna Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="330a0-112">Azure Redis Cache.</span></span>

<span data-ttu-id="330a0-113">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="330a0-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="330a0-114">[![Wdrażanie tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="330a0-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="330a0-115">Parametry toospecify</span><span class="sxs-lookup"><span data-stu-id="330a0-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="330a0-116">Zmienne dla nazwy</span><span class="sxs-lookup"><span data-stu-id="330a0-116">Variables for names</span></span>
<span data-ttu-id="330a0-117">Ten szablon używa nazwy tooconstruct zmienne hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="330a0-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="330a0-118">Używa hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) funkcji tooconstruct wartość oparta na identyfikator grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="330a0-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="330a0-119">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="330a0-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="330a0-120">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="330a0-120">Redis Cache</span></span>
<span data-ttu-id="330a0-121">Tworzy hello pamięć podręczna Redis Azure używany z hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="330a0-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="330a0-122">Nazwa Hello hello pamięci podręcznej została określona w hello **cacheName** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="330a0-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="330a0-123">Szablon Hello tworzy hello pamięci podręcznej w hello tej samej lokalizacji co hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="330a0-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="330a0-124">Aplikacja internetowa</span><span class="sxs-lookup"><span data-stu-id="330a0-124">Web app</span></span>
<span data-ttu-id="330a0-125">Tworzy hello aplikacji sieci web o nazwie określonej w hello **podaną** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="330a0-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="330a0-126">Należy zauważyć, że tej aplikacji sieci web hello jest skonfigurowany z aplikacją ustawienie właściwości, które ją włączyć toowork z hello pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="330a0-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="330a0-127">Ta aplikacja, ustawienia dynamiczne są tworzone na podstawie wartości podana podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="330a0-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="330a0-128">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="330a0-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="330a0-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="330a0-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="330a0-130">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="330a0-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
