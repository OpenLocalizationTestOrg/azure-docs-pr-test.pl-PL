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
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="eec11-103">Tworzenie zasobów usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eec11-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="eec11-104">W tym artykule opisano sposób toocreate i wdrażanie zasobów usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager, programu PowerShell i dostawcy zasobów usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="eec11-105">Szablony usługi Azure Resource Manager pomagają zdefiniować hello toodeploy zasobów dla rozwiązania i toospecify parametry i zmienne, które pozwalają tooinput wartości dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="eec11-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="eec11-106">Szablon Hello składa się z kodu JSON i wyrażeń, że możesz użyć wartości tooconstruct dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eec11-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="eec11-107">Aby uzyskać szczegółowe informacje na temat pisania szablonów usługi Azure Resource Manager oraz omówienie formacie szablonu hello, zobacz [struktury i składni szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eec11-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eec11-108">jak Hello przykłady w tym artykule Pokaż toouse Azure Resource Manager toocreate przestrzeni nazw usługi Service Bus i jednostek (kolejki) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="eec11-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="eec11-109">Inne przykłady szablonów można znaleźć hello [galerię szablonów Szybki Start Azure] [ Azure Quickstart Templates gallery] i wyszukaj "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="eec11-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="eec11-110">Szablony Menedżera zasobów magistrali usług</span><span class="sxs-lookup"><span data-stu-id="eec11-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="eec11-111">Te szablony usługi magistrali usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eec11-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="eec11-112">Kliknij hello następującego łącza Aby uzyskać szczegółowe informacje o każdym z nich, przy użyciu łącza toohello szablonów w witrynie GitHub:</span><span class="sxs-lookup"><span data-stu-id="eec11-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="eec11-113">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="eec11-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="eec11-114">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="eec11-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="eec11-115">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eec11-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="eec11-116">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="eec11-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="eec11-117">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="eec11-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="eec11-118">Wdrażanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eec11-118">Deploy with PowerShell</span></span>

<span data-ttu-id="eec11-119">Hello Poniższa procedura opisuje sposób toouse PowerShell toodeploy szablonu usługi Azure Resource Manager tworzącą **standardowe** warstwy przestrzeń nazw magistrali usług i kolejką w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="eec11-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="eec11-120">Ten przykład jest oparty na powitania [tworzenie przestrzeni nazw usługi Service Bus z kolejką](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) szablonu.</span><span class="sxs-lookup"><span data-stu-id="eec11-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="eec11-121">Witaj przybliżonej przepływu pracy jest następujący:</span><span class="sxs-lookup"><span data-stu-id="eec11-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="eec11-122">Instalowanie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eec11-122">Install PowerShell.</span></span>
2. <span data-ttu-id="eec11-123">Utwórz szablon hello i (opcjonalnie) pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="eec11-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="eec11-124">W programie PowerShell Zaloguj się za tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eec11-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="eec11-125">Utwórz nową grupę zasobów, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="eec11-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="eec11-126">Testowanie wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-126">Test hello deployment.</span></span>
6. <span data-ttu-id="eec11-127">W razie potrzeby można ustawić trybu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="eec11-128">Wdrażanie szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-128">Deploy hello template.</span></span>

<span data-ttu-id="eec11-129">Aby uzyskać pełne informacje na temat wdrażania szablonów usługi Azure Resource Manager, zobacz [wdrożenie zasobów przy użyciu szablonów usługi Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="eec11-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="eec11-130">Instalowanie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eec11-130">Install PowerShell</span></span>

<span data-ttu-id="eec11-131">Zainstaluj program Azure PowerShell, wykonując instrukcje hello w [wprowadzenie do programu Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="eec11-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="eec11-132">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="eec11-132">Create a template</span></span>

<span data-ttu-id="eec11-133">Witaj w klonowania lub kopiowanie [201 magistrali usług — Tworzenie kolejki](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) szablonu z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="eec11-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="eec11-134">Utwórz plik parametrów (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="eec11-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="eec11-135">toouse pliku następujące parametry opcjonalne hello kopiowania [201 magistrali usług — Tworzenie kolejki](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) pliku.</span><span class="sxs-lookup"><span data-stu-id="eec11-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="eec11-136">Zastąp wartość hello `serviceBusNamespaceName` o nazwie hello przestrzeni nazw usługi Service Bus hello toocreate w tym wdrożeniu, a następnie zastąp wartości hello `serviceBusQueueName` o nazwie hello kolejki hello ma toocreate.</span><span class="sxs-lookup"><span data-stu-id="eec11-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="eec11-137">Aby uzyskać więcej informacji, zobacz hello [parametry](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tematu.</span><span class="sxs-lookup"><span data-stu-id="eec11-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="eec11-138">Zaloguj się za tooAzure i ustawić hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eec11-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="eec11-139">Uruchom hello następujące polecenie z wiersza polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="eec11-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="eec11-140">Jesteś zostanie wyświetlony monit o toolog na tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eec11-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="eec11-141">Po zalogowaniu, uruchom następujące polecenie tooview hello dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eec11-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="eec11-142">To polecenie zwraca listę dostępnych subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eec11-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="eec11-143">Wybierz subskrypcję dla hello bieżącej sesji, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="eec11-144">Zastąp `<YourSubscriptionId>` z hello identyfikatora GUID dla hello subskrypcji platformy Azure ma toouse.</span><span class="sxs-lookup"><span data-stu-id="eec11-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="eec11-145">Witaj grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="eec11-145">Set hello resource group</span></span>

<span data-ttu-id="eec11-146">Jeśli nie masz istniejący zasób grupy, Utwórz nową grupę zasobów o hello ** New-AzureRmResourceGroup ** polecenia.</span><span class="sxs-lookup"><span data-stu-id="eec11-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="eec11-147">Podaj nazwę grupy zasobów hello i lokalizację toouse hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="eec11-148">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eec11-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="eec11-149">Jeśli to się powiedzie, zostanie wyświetlone podsumowanie hello nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="eec11-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="eec11-150">Testowe wdrożenie na powitania</span><span class="sxs-lookup"><span data-stu-id="eec11-150">Test hello deployment</span></span>

<span data-ttu-id="eec11-151">Sprawdzanie poprawności wdrożenia, uruchamiając hello `Test-AzureRmResourceGroupDeployment` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eec11-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="eec11-152">Podczas testowania wdrożenia hello, należy podać parametry, dokładnie tak jak w przypadku wykonywania hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eec11-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="eec11-153">Tworzenie wdrożenia hello</span><span class="sxs-lookup"><span data-stu-id="eec11-153">Create hello deployment</span></span>

<span data-ttu-id="eec11-154">toocreate hello nowe wdrożenie, uruchom hello `New-AzureRmResourceGroupDeployment` polecenia cmdlet i podaj niezbędne parametry powitania po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="eec11-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="eec11-155">Parametry Hello obejmować nazwę dla danego wdrożenia hello nazwy grupy zasobów i ścieżka hello lub pliku szablonu toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="eec11-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="eec11-156">Jeśli hello **tryb** parametr nie zostanie określony, hello wartość domyślną **przyrostowe** jest używany.</span><span class="sxs-lookup"><span data-stu-id="eec11-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="eec11-157">Aby uzyskać więcej informacji, zobacz [przyrostowe i pełne wdrożeń](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="eec11-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="eec11-158">Witaj następujących wierszy polecenia można hello trzech parametrów w oknie programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="eec11-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="eec11-159">toospecify pliku parametrów zamiast tego należy użyć następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="eec11-160">Umożliwia także parametry wbudowanego po uruchomieniu polecenia cmdlet wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="eec11-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="eec11-161">polecenie Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="eec11-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="eec11-162">toorun [pełną](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) wdrożenia, zestaw hello **tryb** parametru zbyt**Complete**:</span><span class="sxs-lookup"><span data-stu-id="eec11-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="eec11-163">Sprawdź hello wdrożenia</span><span class="sxs-lookup"><span data-stu-id="eec11-163">Verify hello deployment</span></span>
<span data-ttu-id="eec11-164">Jeśli pomyślnie są wdrażane zasoby hello, w oknie programu PowerShell hello zostanie wyświetlone podsumowanie wdrożenia hello:</span><span class="sxs-lookup"><span data-stu-id="eec11-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="eec11-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eec11-165">Next steps</span></span>
<span data-ttu-id="eec11-166">Teraz przedstawiono podstawowy przepływ pracy hello i polecenia służące do wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eec11-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="eec11-167">Aby uzyskać szczegółowe informacje odwiedź hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="eec11-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="eec11-168">[Omówienie usługi Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="eec11-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="eec11-169">[Wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="eec11-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="eec11-170">Tworzenie szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eec11-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
