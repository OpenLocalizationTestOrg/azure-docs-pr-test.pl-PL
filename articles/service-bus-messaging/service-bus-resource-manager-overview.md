---
title: "Tworzenie zasobów Azure Service Bus przy użyciu szablonów usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Szablony usługi Azure Resource Manager umożliwia zautomatyzowanie tworzenie zasobów usługi Service Bus"
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
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="022e2-103">Tworzenie zasobów usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="022e2-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="022e2-104">W tym artykule opisano sposób tworzenia i wdrażania zasobów usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager, programu PowerShell i dostawcy zasobów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="022e2-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="022e2-105">Szablony usługi Azure Resource Manager pomagają zdefiniować zasobów do wdrożenia rozwiązania, aby określić parametry i zmienne, które umożliwią wprowadzanie wartości dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="022e2-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="022e2-106">Szablon składa się z kodu JSON i wyrażeń, które służy do tworzenia wartości na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="022e2-107">Aby uzyskać szczegółowe informacje na temat pisania szablonów usługi Azure Resource Manager i omówione w formacie szablonu, zobacz [struktury i składni szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="022e2-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="022e2-108">Przykłady w tym artykule pokazano, jak używać usługi Azure Resource Manager do tworzenia nazw usługi Service Bus i jednostki obsługi komunikatów (kolejki).</span><span class="sxs-lookup"><span data-stu-id="022e2-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="022e2-109">Inne przykłady szablonów można znaleźć [galerię szablonów Szybki Start Azure] [ Azure Quickstart Templates gallery] i wyszukaj "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="022e2-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="022e2-110">Szablony Menedżera zasobów magistrali usług</span><span class="sxs-lookup"><span data-stu-id="022e2-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="022e2-111">Te szablony usługi magistrali usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="022e2-112">Kliknij poniższe łącza, aby uzyskać szczegółowe informacje o każdym z nich, wraz z łączami do szablonów w witrynie GitHub:</span><span class="sxs-lookup"><span data-stu-id="022e2-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="022e2-113">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="022e2-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="022e2-114">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="022e2-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="022e2-115">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="022e2-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="022e2-116">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="022e2-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="022e2-117">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="022e2-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="022e2-118">Wdrażanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="022e2-118">Deploy with PowerShell</span></span>

<span data-ttu-id="022e2-119">W poniższej procedurze opisano sposób użycia programu PowerShell do wdrożenia szablonu usługi Azure Resource Manager, która tworzy **standardowe** warstwy przestrzeń nazw magistrali usług i kolejką w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="022e2-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="022e2-120">Ten przykład jest oparty na [tworzenie przestrzeni nazw usługi Service Bus z kolejką](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) szablonu.</span><span class="sxs-lookup"><span data-stu-id="022e2-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="022e2-121">Przybliżony przepływu pracy jest następujący:</span><span class="sxs-lookup"><span data-stu-id="022e2-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="022e2-122">Instalowanie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="022e2-122">Install PowerShell.</span></span>
2. <span data-ttu-id="022e2-123">Utwórz szablon i (opcjonalnie) pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="022e2-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="022e2-124">W programie PowerShell należy zalogować się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="022e2-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="022e2-125">Utwórz nową grupę zasobów, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="022e2-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="022e2-126">Testowanie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-126">Test the deployment.</span></span>
6. <span data-ttu-id="022e2-127">W razie potrzeby można ustawić trybu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="022e2-128">Wdrażanie szablonu.</span><span class="sxs-lookup"><span data-stu-id="022e2-128">Deploy the template.</span></span>

<span data-ttu-id="022e2-129">Aby uzyskać pełne informacje na temat wdrażania szablonów usługi Azure Resource Manager, zobacz [wdrożenie zasobów przy użyciu szablonów usługi Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="022e2-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="022e2-130">Instalowanie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="022e2-130">Install PowerShell</span></span>

<span data-ttu-id="022e2-131">Instalowanie programu Azure PowerShell zgodnie z instrukcjami w [wprowadzenie do programu Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="022e2-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="022e2-132">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="022e2-132">Create a template</span></span>

<span data-ttu-id="022e2-133">Klonuj lub kopiowanie [201 magistrali usług — Tworzenie kolejki](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) szablonu z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="022e2-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="022e2-134">Utwórz plik parametrów (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="022e2-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="022e2-135">Aby użyć pliku następujące parametry opcjonalne, skopiuj [201 magistrali usług — Tworzenie kolejki](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) pliku.</span><span class="sxs-lookup"><span data-stu-id="022e2-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="022e2-136">Zastąp wartość `serviceBusNamespaceName` z nazwą przestrzeni nazw usługi Service Bus chcesz utworzyć w tym wdrożeniu i zastąp wartość `serviceBusQueueName` nazwą kolejki, w którym chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="022e2-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

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

<span data-ttu-id="022e2-137">Aby uzyskać więcej informacji, zobacz [parametry](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tematu.</span><span class="sxs-lookup"><span data-stu-id="022e2-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="022e2-138">Logowanie do platformy Azure i ustaw subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="022e2-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="022e2-139">Z wiersza polecenia programu PowerShell, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="022e2-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="022e2-140">Zostanie wyświetlony monit logowania do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="022e2-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="022e2-141">Po zalogowaniu, uruchom następujące polecenie, aby wyświetlić dostępne subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="022e2-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="022e2-142">To polecenie zwraca listę dostępnych subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="022e2-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="022e2-143">Wybierz subskrypcję dla bieżącej sesji, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="022e2-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="022e2-144">Zastąp `<YourSubscriptionId>` o identyfikatorze GUID dla subskrypcji platformy Azure, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="022e2-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="022e2-145">Ustaw grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="022e2-145">Set the resource group</span></span>

<span data-ttu-id="022e2-146">Jeśli nie masz istniejący zasób grupy, Utwórz nową grupę zasobów o ** New-AzureRmResourceGroup ** polecenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="022e2-147">Podaj nazwę grupy zasobów i lokalizacji, w której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="022e2-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="022e2-148">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="022e2-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="022e2-149">Jeśli to się powiedzie, zostanie wyświetlone podsumowanie nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="022e2-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="022e2-150">Testowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="022e2-150">Test the deployment</span></span>

<span data-ttu-id="022e2-151">Sprawdzanie poprawności wdrożenia, uruchamiając `Test-AzureRmResourceGroupDeployment` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="022e2-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="022e2-152">Podczas testowania wdrożenia, należy podać parametry, dokładnie tak jak w przypadku wykonywania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="022e2-153">Tworzenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="022e2-153">Create the deployment</span></span>

<span data-ttu-id="022e2-154">Aby utworzyć nowe wdrożenie, uruchom `New-AzureRmResourceGroupDeployment` polecenia cmdlet i podaj niezbędne parametry, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="022e2-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="022e2-155">Parametry zawierają nazwę dla danego wdrożenia, nazwę grupy zasobów, a ścieżka lub adres URL do pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="022e2-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="022e2-156">Jeśli **tryb** parametr nie zostanie określony, wartością domyślną **przyrostowe** jest używany.</span><span class="sxs-lookup"><span data-stu-id="022e2-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="022e2-157">Aby uzyskać więcej informacji, zobacz [przyrostowe i pełne wdrożeń](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="022e2-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="022e2-158">Polecenie wyświetla monit o podanie trzy parametry w oknie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="022e2-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="022e2-159">Aby zamiast tego określ plik parametrów, należy użyć następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="022e2-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="022e2-160">Umożliwia także parametry wbudowanego po uruchomieniu polecenia cmdlet wdrażania.</span><span class="sxs-lookup"><span data-stu-id="022e2-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="022e2-161">Polecenie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="022e2-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="022e2-162">Do uruchomienia [pełną](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) wdrożenia, ustaw **tryb** parametr **Complete**:</span><span class="sxs-lookup"><span data-stu-id="022e2-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="022e2-163">Weryfikacja wdrażania</span><span class="sxs-lookup"><span data-stu-id="022e2-163">Verify the deployment</span></span>
<span data-ttu-id="022e2-164">Jeśli zasoby zostały pomyślnie wdrożone, zostanie wyświetlone podsumowanie wdrożenia w oknie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="022e2-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="022e2-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="022e2-165">Next steps</span></span>
<span data-ttu-id="022e2-166">Teraz przedstawiono podstawowy przepływ pracy i polecenia służące do wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="022e2-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="022e2-167">Bardziej szczegółowe informacje można znaleźć w następujących łączy:</span><span class="sxs-lookup"><span data-stu-id="022e2-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="022e2-168">[Omówienie usługi Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="022e2-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="022e2-169">[Wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="022e2-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="022e2-170">Tworzenie szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="022e2-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
