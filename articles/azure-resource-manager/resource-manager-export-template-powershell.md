---
title: "Eksportowanie szablonu usługi Resource Manager z programem Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Resource Manager i programu Azure PowerShell, aby wyeksportować szablon na podstawie grupy zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 7543811eb9448222b6e7c266756e68debc7d54be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="6aa34-103">Eksportowanie szablonów usługi Azure Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6aa34-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="6aa34-104">Usługa Resource Manager umożliwia wyeksportowanie szablonu usługi Resource Manager z istniejących zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6aa34-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="6aa34-105">Możesz użyć wygenerowanego szablonu, aby dowiedzieć się więcej o składni szablonu lub aby zautomatyzować ponowne wdrożenie rozwiązania, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="6aa34-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="6aa34-106">Należy pamiętać, że istnieją dwa różne sposoby eksportowania szablonu:</span><span class="sxs-lookup"><span data-stu-id="6aa34-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="6aa34-107">Możesz wyeksportować szablon, który faktycznie został użyty na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6aa34-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="6aa34-108">W wyeksportowanym szablonie wszystkie parametry i zmienne występują dokładnie tak, jak w oryginalnym szablonie.</span><span class="sxs-lookup"><span data-stu-id="6aa34-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="6aa34-109">Takie podejście jest przydatne, gdy jest potrzebne do pobierania szablonu.</span><span class="sxs-lookup"><span data-stu-id="6aa34-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="6aa34-110">Możesz wyeksportować szablon, który reprezentuje bieżący stan grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6aa34-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="6aa34-111">Wyeksportowany szablon nie jest oparty na żadnym szablonie użytym do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6aa34-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="6aa34-112">Utworzony szablon będzie stanowić migawkę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6aa34-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="6aa34-113">W wyeksportowanym szablonie zawartych jest wiele zakodowanych wartości i prawdopodobnie mniej parametrów, niż się zwykle definiuje.</span><span class="sxs-lookup"><span data-stu-id="6aa34-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="6aa34-114">Takie rozwiązanie jest przydatne, gdy zostały zmodyfikowane grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6aa34-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="6aa34-115">Będzie więc trzeba przechwycić grupę zasobów jako szablon.</span><span class="sxs-lookup"><span data-stu-id="6aa34-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="6aa34-116">W tym temacie opisano obie te metody.</span><span class="sxs-lookup"><span data-stu-id="6aa34-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="6aa34-117">Wdrażanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6aa34-117">Deploy a solution</span></span>

<span data-ttu-id="6aa34-118">Aby zilustrować obu podejść eksportowania szablonu, Zacznijmy od wdrażanie rozwiązania do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6aa34-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="6aa34-119">Jeśli masz już grupę zasobów w ramach subskrypcji, który chcesz wyeksportować, nie trzeba wdrożyć to rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="6aa34-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="6aa34-120">Jednak w dalszej części tego artykułu odwołuje się do szablonu dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6aa34-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="6aa34-121">Przykładowy skrypt wdraża konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6aa34-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="6aa34-122">Zapisz szablon z historii wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6aa34-122">Save template from deployment history</span></span>

<span data-ttu-id="6aa34-123">Można pobrać szablonu z historii wdrożenia za pomocą [AzureRmResourceGroupDeploymentTemplate Zapisz](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6aa34-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="6aa34-124">Poniższy przykład zapisuje szablon, który wcześniej wdrażania:</span><span class="sxs-lookup"><span data-stu-id="6aa34-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="6aa34-125">Zwraca lokalizację szablonu.</span><span class="sxs-lookup"><span data-stu-id="6aa34-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="6aa34-126">Otwórz plik i zwróć uwagę, że jest dokładne szablon, którego można użyć do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6aa34-126">Open the file, and notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="6aa34-127">Parametry i zmienne pasuje do szablonu z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="6aa34-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="6aa34-128">Tego szablonu można wdrożyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="6aa34-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="6aa34-129">Eksportowanie grupy zasobów jako szablon</span><span class="sxs-lookup"><span data-stu-id="6aa34-129">Export resource group as template</span></span>

<span data-ttu-id="6aa34-130">Zamiast pobierania szablonu z historii wdrażania, można pobrać szablonu, która reprezentuje bieżący stan grupy zasobów za pomocą [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6aa34-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="6aa34-131">Użyj tego polecenia, gdy wprowadzono wiele zmian w danej grupie zasobów, a nie istniejący szablon reprezentuje wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="6aa34-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="6aa34-132">Zwraca lokalizację szablonu.</span><span class="sxs-lookup"><span data-stu-id="6aa34-132">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="6aa34-133">Otwórz plik i zwróć uwagę, że różni się od szablonu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6aa34-133">Open the file, and notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="6aa34-134">Zawiera różne parametry i żadnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="6aa34-134">It has different parameters and no variables.</span></span> <span data-ttu-id="6aa34-135">Magazyn jednostki SKU i lokalizacji są zakodowane na stałe wartości.</span><span class="sxs-lookup"><span data-stu-id="6aa34-135">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="6aa34-136">W poniższym przykładzie przedstawiono wyeksportowanego szablonu, ale szablon ma nazwę parametru nieco inne:</span><span class="sxs-lookup"><span data-stu-id="6aa34-136">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="6aa34-137">Można ponownie wdrożyć tego szablonu, ale wymaga to odgadnięcie unikatową nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6aa34-137">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="6aa34-138">Nazwa parametru jest nieco inne.</span><span class="sxs-lookup"><span data-stu-id="6aa34-138">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="6aa34-139">Dostosowywanie wyeksportowanego szablonu</span><span class="sxs-lookup"><span data-stu-id="6aa34-139">Customize exported template</span></span>

<span data-ttu-id="6aa34-140">Można zmodyfikować tego szablonu, aby była łatwiejsza w użyciu i bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="6aa34-140">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="6aa34-141">Aby umożliwić więcej lokalizacji, zmień właściwość lokalizacji do użycia w tej samej lokalizacji co grupa zasobów:</span><span class="sxs-lookup"><span data-stu-id="6aa34-141">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="6aa34-142">Aby uniknąć konieczności odgadnąć uniques nazwę konta magazynu, należy usunąć parametr nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6aa34-142">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="6aa34-143">Dodaj parametr sufiks nazwy magazynu oraz Magazyn wersji:</span><span class="sxs-lookup"><span data-stu-id="6aa34-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="6aa34-144">Dodawanie zmiennej, która tworzy nazwę konta magazynu przy użyciu funkcji uniqueString:</span><span class="sxs-lookup"><span data-stu-id="6aa34-144">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="6aa34-145">Do zmiennej, należy ustawić nazwę konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="6aa34-145">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="6aa34-146">Jednostka SKU zestawu do parametru:</span><span class="sxs-lookup"><span data-stu-id="6aa34-146">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="6aa34-147">Twój szablon wygląda teraz następująco:</span><span class="sxs-lookup"><span data-stu-id="6aa34-147">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="6aa34-148">Należy ponownie wdrożyć zmodyfikowany szablon.</span><span class="sxs-lookup"><span data-stu-id="6aa34-148">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aa34-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6aa34-149">Next steps</span></span>
* <span data-ttu-id="6aa34-150">Aby uzyskać informacje dotyczące korzystania z portalu, aby wyeksportować szablon, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="6aa34-150">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="6aa34-151">Aby określić parametry w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="6aa34-151">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="6aa34-152">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6aa34-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
