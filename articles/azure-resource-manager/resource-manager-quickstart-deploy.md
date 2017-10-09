---
title: "tooAzure zasobów aaaDeploy | Dokumentacja firmy Microsoft"
description: "Za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure tooAzure zasobów toodeploy. zasoby Hello są definiowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="34632-104">Wdrażanie tooAzure zasobów</span><span class="sxs-lookup"><span data-stu-id="34632-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="34632-105">W tym temacie przedstawiono sposób toodeploy tooyour zasobów subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="34632-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="34632-106">Możesz użyć programu Azure PowerShell lub interfejsu wiersza polecenia Azure toodeploy szablonu usługi Resource Manager, który definiuje infrastrukturę Twojego rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="34632-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="34632-107">Aby tooconcepts wprowadzenie usługi Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34632-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="34632-108">Kroki wdrażania</span><span class="sxs-lookup"><span data-stu-id="34632-108">Steps for deployment</span></span>

<span data-ttu-id="34632-109">W tym temacie założono wdrażasz hello [przykład magazynu szablonu](#example-storage-template) w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="34632-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="34632-110">Można użyć innego szablonu, ale hello parametry, które przekazujesz są inne niż to, co przedstawiono w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="34632-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="34632-111">Po utworzeniu szablonu, hello ogólne kroki dotyczące wdrażania szablonu są:</span><span class="sxs-lookup"><span data-stu-id="34632-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="34632-112">Zaloguj się na koncie tooyour</span><span class="sxs-lookup"><span data-stu-id="34632-112">Log in tooyour account</span></span>
2. <span data-ttu-id="34632-113">Wybierz toouse subskrypcji hello (wymagane tylko jeśli masz wiele subskrypcji, i chcesz toouse, który nie jest hello domyślne subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="34632-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="34632-114">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="34632-114">Create a resource group</span></span>
4. <span data-ttu-id="34632-115">Wdrażanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="34632-115">Deploy hello template</span></span>
5. <span data-ttu-id="34632-116">Sprawdzenie stanu wdrożenia</span><span class="sxs-lookup"><span data-stu-id="34632-116">Check your deployment status</span></span>

<span data-ttu-id="34632-117">Witaj poniższe sekcje pokazują, jak tooperform tych kroków [PowerShell](#powershell) lub [interfejsu wiersza polecenia Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="34632-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="34632-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34632-118">PowerShell</span></span>

1. <span data-ttu-id="34632-119">tooinstall programu Azure PowerShell, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34632-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="34632-120">tooquickly wprowadzenie do wdrożenia, użyj następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="34632-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="34632-121">Witaj `Set-AzureRmContext` polecenia cmdlet jest potrzebne tylko wtedy, jeśli chcesz toouse subskrypcji innych niż domyślne subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34632-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="34632-122">toosee wszystkie subskrypcje i ich identyfikatorów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="34632-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="34632-123">Witaj wdrożenia może zająć kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="34632-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="34632-124">Po zakończeniu zostanie wyświetlony komunikat podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="34632-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="34632-125">toosee, które były zasobów konta grupy i magazynu wdrożone tooyour subskrypcji, użyj:</span><span class="sxs-lookup"><span data-stu-id="34632-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="34632-126">Podczas wdrażania szablonu możesz określić parametry szablonu jako parametry programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34632-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="34632-127">Hello wcześniejszego przykładu nie zawiera żadnych parametrów szablonu, aby były używane wartości domyślne hello w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="34632-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="34632-128">toodeploy magazynu innego konta i podaj wartości parametrów dla prefiksu nazwy hello magazynu i konto magazynu hello jednostka SKU, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="34632-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="34632-129">Masz teraz dwa konta magazynu w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="34632-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="34632-130">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34632-130">Azure CLI</span></span>

1. <span data-ttu-id="34632-131">tooinstall wiersza polecenia platformy Azure, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="34632-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="34632-132">tooquickly wprowadzenie do wdrażania, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="34632-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="34632-133">Witaj `az account set` polecenia jest potrzebne tylko wtedy, jeśli chcesz toouse subskrypcji innych niż domyślne subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34632-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="34632-134">toosee wszystkie subskrypcje i ich identyfikatorów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="34632-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="34632-135">Witaj wdrożenia może zająć kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="34632-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="34632-136">Po zakończeniu zostanie wyświetlony komunikat podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="34632-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="34632-137">toosee, które były zasobów konta grupy i magazynu wdrożone tooyour subskrypcji, użyj:</span><span class="sxs-lookup"><span data-stu-id="34632-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="34632-138">Podczas wdrażania szablonu możesz określić parametry szablonu jako parametry programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34632-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="34632-139">Hello wcześniejszego przykładu nie zawiera żadnych parametrów szablonu, aby były używane wartości domyślne hello w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="34632-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="34632-140">toodeploy magazynu innego konta i podaj wartości parametrów dla prefiksu nazwy hello magazynu i konto magazynu hello jednostka SKU, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="34632-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="34632-141">Masz teraz dwa konta magazynu w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="34632-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="34632-142">Przykładowy szablon magazynu</span><span class="sxs-lookup"><span data-stu-id="34632-142">Example storage template</span></span>

<span data-ttu-id="34632-143">Użyj powitania po przykładowy szablon toodeploy subskrypcja tooyour konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="34632-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="34632-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34632-144">Next steps</span></span>

* <span data-ttu-id="34632-145">Aby uzyskać szczegółowe informacje o korzystaniu z programu PowerShell toodeploy szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="34632-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="34632-146">Aby uzyskać szczegółowe informacje dotyczące korzystania z szablonów toodeploy wiersza polecenia platformy Azure, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="34632-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



