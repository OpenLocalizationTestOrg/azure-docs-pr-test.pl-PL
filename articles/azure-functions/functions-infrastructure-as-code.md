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
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="81122-104">Automatyzacji wdrażania zasobów dla aplikacji funkcja na usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="81122-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="81122-105">Możesz użyć usługi Azure Resource Manager toodeploy szablonu aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="81122-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="81122-106">W tym artykule opisano hello wymaganych zasobów i parametrów w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="81122-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="81122-107">Może być konieczne dodatkowe zasoby toodeploy, w zależności od hello [wyzwalaczy i powiązań](functions-triggers-bindings.md) w funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81122-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="81122-108">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="81122-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="81122-109">Na przykład szablony Zobacz:</span><span class="sxs-lookup"><span data-stu-id="81122-109">For sample templates, see:</span></span>
- <span data-ttu-id="81122-110">[funkcji aplikacji w planie zużycie]</span><span class="sxs-lookup"><span data-stu-id="81122-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="81122-111">[funkcji aplikacji w planie usługi aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="81122-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="81122-112">Wymagane zasoby</span><span class="sxs-lookup"><span data-stu-id="81122-112">Required resources</span></span>

<span data-ttu-id="81122-113">Aplikacja funkcji wymaga tych zasobów:</span><span class="sxs-lookup"><span data-stu-id="81122-113">A function app requires these resources:</span></span>

* <span data-ttu-id="81122-114">[Usługi Azure Storage](../storage/index.md) konta</span><span class="sxs-lookup"><span data-stu-id="81122-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="81122-115">Plan hostingu (użycie planu lub plan usługi aplikacji)</span><span class="sxs-lookup"><span data-stu-id="81122-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="81122-116">Aplikacja — funkcja</span><span class="sxs-lookup"><span data-stu-id="81122-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="81122-117">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="81122-117">Storage account</span></span>

<span data-ttu-id="81122-118">Konto magazynu platformy Azure jest wymagany dla funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81122-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="81122-119">Musisz mieć konto ogólnego przeznaczenia, który obsługuje obiekty BLOB, tabel, kolejek i plików.</span><span class="sxs-lookup"><span data-stu-id="81122-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="81122-120">Aby uzyskać więcej informacji, zobacz [wymagania dotyczące konta magazynu usługi Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="81122-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="81122-121">Ponadto hello właściwości `AzureWebJobsStorage` i `AzureWebJobsDashboard` muszą być określone jako ustawienia aplikacji hello konfiguracji lokacji.</span><span class="sxs-lookup"><span data-stu-id="81122-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="81122-122">środowisko wykonawcze usługi Azure Functions Hello używa hello `AzureWebJobsStorage` toocreate wewnętrzne kolejki parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="81122-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="81122-123">Witaj parametry połączenia `AzureWebJobsDashboard` jest używane toolog tooAzure tabeli magazynu i mocy hello **Monitor** kartę w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="81122-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="81122-124">Te właściwości są określone w hello `appSettings` kolekcji w hello `siteConfig` obiektu:</span><span class="sxs-lookup"><span data-stu-id="81122-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="81122-125">Plan hostingu</span><span class="sxs-lookup"><span data-stu-id="81122-125">Hosting plan</span></span>

<span data-ttu-id="81122-126">Definicja Hello hello plan hostingu różni się w zależności od tego, czy używasz planu zużycia lub usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81122-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="81122-127">Zobacz [wdrażanie aplikacji funkcji w planie zużycie hello](#consumption) i [wdrażanie aplikacji na powitania planu usługi aplikacji — funkcja](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="81122-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="81122-128">Funkcja aplikacji</span><span class="sxs-lookup"><span data-stu-id="81122-128">Function app</span></span>

<span data-ttu-id="81122-129">zasób aplikacji Hello funkcja jest definiowana za pomocą zasobu typu **Microsoft.Web/Site** i rodzaj **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="81122-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="81122-130">Wdrażanie aplikacji na powitania użycie planu — funkcja</span><span class="sxs-lookup"><span data-stu-id="81122-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="81122-131">Można uruchomić aplikacji funkcji w dwóch różnych trybach: hello planowania użycia i hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81122-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="81122-132">plan zużycie Hello automatycznie przydzieli moc obliczeniową po kodzie działa, skaluje się jako niezbędne toohandle obciążenia i następnie skalowany w dół, gdy kodu nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="81122-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="81122-133">Tak nie masz toopay bezczynnych maszyn wirtualnych, a nie ma zdolności tooreserve z wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="81122-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="81122-134">toolearn więcej informacji na temat hostingu planów, zobacz [planów Azure — użytek funkcje i usługi aplikacji](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="81122-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="81122-135">Aby uzyskać przykładowy szablon usługi Azure Resource Manager, zobacz [funkcji aplikacji w planie zużycie].</span><span class="sxs-lookup"><span data-stu-id="81122-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="81122-136">Tworzenie planu zużycie</span><span class="sxs-lookup"><span data-stu-id="81122-136">Create a Consumption plan</span></span>

<span data-ttu-id="81122-137">Plan zużycie jest specjalny typ zasobu "serverfarm".</span><span class="sxs-lookup"><span data-stu-id="81122-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="81122-138">Należy określić przy użyciu hello `Dynamic` wartość hello `computeMode` i `sku` właściwości:</span><span class="sxs-lookup"><span data-stu-id="81122-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="81122-139">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="81122-139">Create a function app</span></span>

<span data-ttu-id="81122-140">Ponadto planu zużycie wymaga dwóch dodatkowych ustawień konfiguracji lokacji hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` i `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="81122-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="81122-141">Te właściwości skonfiguruj hello magazynu konta i ścieżce pliku przechowywania kodu aplikacji hello funkcji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="81122-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="81122-142">Wdrażanie aplikacji na powitania planu usługi aplikacji — funkcja</span><span class="sxs-lookup"><span data-stu-id="81122-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="81122-143">W hello planu usługi aplikacji aplikacji funkcja działa na dedykowanych maszynach wirtualnych na podstawowa, standardowa i Premium jednostki SKU, podobne tooweb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81122-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="81122-144">Aby uzyskać szczegółowe informacje dotyczące sposobu działania hello planu usługi App Service, zobacz hello [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81122-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="81122-145">Aby uzyskać przykładowy szablon usługi Azure Resource Manager, zobacz [funkcji aplikacji w planie usługi aplikacji Azure].</span><span class="sxs-lookup"><span data-stu-id="81122-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="81122-146">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="81122-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="81122-147">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="81122-147">Create a function app</span></span> 

<span data-ttu-id="81122-148">Po wybraniu opcji skalowania tworzenia aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="81122-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="81122-149">Aplikacja Hello jest hello kontener, który zawiera wszystkie funkcje.</span><span class="sxs-lookup"><span data-stu-id="81122-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="81122-150">Aplikacja funkcji ma wiele zasoby podrzędne używane w danym wdrożeniu, w tym ustawienia aplikacji i opcje kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="81122-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="81122-151">Możesz również wybrać tooremove hello **sourcecontrols** zasobu podrzędnego i użyj innego [opcji wdrażania](functions-continuous-deployment.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="81122-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81122-152">toosuccessfully wdrażanie aplikacji przy użyciu usługi Azure Resource Manager, jest ważne toounderstand wdrażanie zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="81122-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="81122-153">W hello poniższy przykład, najwyższego poziomu konfiguracji są stosowane przy użyciu **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="81122-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="81122-154">Jest ważne tooset poziomu te konfiguracje u góry, ponieważ ich przedstawienia informacji toohello funkcji środowiska uruchomieniowego i wdrażania aparat.</span><span class="sxs-lookup"><span data-stu-id="81122-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="81122-155">Przed elementem podrzędnym hello jest wymaganych informacji najwyższego poziomu **sourcecontrols/sieci web** zasobów są stosowane.</span><span class="sxs-lookup"><span data-stu-id="81122-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="81122-156">Chociaż jest to możliwe tooconfigure tych ustawień w hello podrzędnymi **config/appSettings** zasobów, w niektórych przypadkach należy wdrożyć aplikację funkcja *przed* **config/appSettings**  została zastosowana.</span><span class="sxs-lookup"><span data-stu-id="81122-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="81122-157">Na przykład w przypadku używania funkcji z [Logic Apps](../logic-apps/index.md), funkcji są zależność innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="81122-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="81122-158">Ten szablon używa hello [projektu](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) wartość ustawienia aplikacji, która ustawia hello podstawowego katalogu, w którym hello aparat wdrażania funkcji (Kudu) wyszukuje kodu do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="81122-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="81122-159">W naszym repozytorium naszej funkcji znajdują się w podfolderze hello **src** folderu.</span><span class="sxs-lookup"><span data-stu-id="81122-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="81122-160">Tak, w hello poprzedzających przykład, możemy ustawić wartość ustawienia aplikacji hello także`src`.</span><span class="sxs-lookup"><span data-stu-id="81122-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="81122-161">Jeśli funkcji znajdują się w katalogu głównego repozytorium hello, lub jeśli nie są wdrażane z kontroli źródła, możesz usunąć tę wartość ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81122-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="81122-162">Wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="81122-162">Deploy your template</span></span>

<span data-ttu-id="81122-163">Można użyć dowolnego hello następujące sposoby toodeploy szablonu:</span><span class="sxs-lookup"><span data-stu-id="81122-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="81122-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81122-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="81122-165">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="81122-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="81122-166">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81122-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="81122-167">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="81122-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="81122-168">TooAzure przycisk Wdrażaj</span><span class="sxs-lookup"><span data-stu-id="81122-168">Deploy tooAzure button</span></span>

<span data-ttu-id="81122-169">Zastąp ```<url-encoded-path-to-azuredeploy-json>``` z [zakodowane w adresie URL](https://www.bing.com/search?q=url+encode) wersji hello ścieżka pierwotnych z `azuredeploy.json` pliku w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="81122-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="81122-170">Oto przykład, który używa języka znaczników markdown:</span><span class="sxs-lookup"><span data-stu-id="81122-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="81122-171">Oto przykład, który używa HTML:</span><span class="sxs-lookup"><span data-stu-id="81122-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="81122-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="81122-172">Next steps</span></span>

<span data-ttu-id="81122-173">Dowiedz się więcej na temat toodevelop i konfigurowanie usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="81122-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="81122-174">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="81122-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="81122-175">Jak tooconfigure Azure funkcji ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="81122-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="81122-176">Tworzenie pierwszej funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="81122-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[funkcji aplikacji w planie zużycie]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[funkcji aplikacji w planie usługi aplikacji Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
