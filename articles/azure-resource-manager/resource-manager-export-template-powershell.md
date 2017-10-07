---
title: "Szablon usługi Resource Manager aaaExport przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i programu Azure PowerShell tooexport szablonu z grupą zasobów."
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
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="21745-103">Eksportowanie szablonów usługi Azure Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="21745-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="21745-104">Menedżer zasobów pozwala tooexport szablonem usługi Resource Manager z istniejących zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="21745-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="21745-105">Możesz użyć tego toolearn wygenerowanego szablonu o hello szablonu składni lub tooautomate hello ponowne wdrożenie rozwiązania zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="21745-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="21745-106">Jest ważne toonote, że istnieją dwa różne sposoby tooexport szablonu:</span><span class="sxs-lookup"><span data-stu-id="21745-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="21745-107">Można wyeksportować szablon rzeczywiste hello używany we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="21745-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="21745-108">Hello wyeksportowanego szablonu obejmuje wszystkie hello parametry i zmienne, dokładnie tak, jak znalazły się na oryginalnym szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="21745-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="21745-109">Takie podejście jest przydatne, gdy będziesz potrzebować tooretrieve szablonu.</span><span class="sxs-lookup"><span data-stu-id="21745-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="21745-110">Można wyeksportować szablon, który reprezentuje bieżący stan hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="21745-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="21745-111">Witaj wyeksportowanego szablonu nie jest oparta na dowolnego szablonu, który został użyty do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="21745-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="21745-112">Zamiast tego tworzy szablon, który jest migawką hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="21745-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="21745-113">Witaj wyeksportowanego szablonu ma wiele wartości stałe i prawdopodobnie nie jako wiele parametrów, jak zwykle należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="21745-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="21745-114">Takie podejście jest przydatne, gdy zmieniono hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="21745-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="21745-115">Teraz należy grupy zasobów hello toocapture jako szablon.</span><span class="sxs-lookup"><span data-stu-id="21745-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="21745-116">W tym temacie opisano obie te metody.</span><span class="sxs-lookup"><span data-stu-id="21745-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="21745-117">Wdrażanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="21745-117">Deploy a solution</span></span>

<span data-ttu-id="21745-118">tooillustrate zarówno zbliża się do eksportowania szablonu, Zacznijmy poprzez wdrożenie rozwiązania tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="21745-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="21745-119">Jeśli masz już grupę zasobów w ramach subskrypcji, które mają tooexport, nie masz toodeploy tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="21745-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="21745-120">Jednak hello dalszej części tego artykułu odwołuje się szablon toohello dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="21745-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="21745-121">skrypt przykładowy Hello wdraża konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="21745-121">hello example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="21745-122">Zapisz szablon z historii wdrożenia</span><span class="sxs-lookup"><span data-stu-id="21745-122">Save template from deployment history</span></span>

<span data-ttu-id="21745-123">Można pobrać szablonu z historii wdrożenia przy użyciu hello [AzureRmResourceGroupDeploymentTemplate Zapisz](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) polecenia.</span><span class="sxs-lookup"><span data-stu-id="21745-123">You can retrieve a template from your deployment history by using hello [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="21745-124">następujące przykładowe zapisuje hello szablon, który wcześniej wdrażanie Hello:</span><span class="sxs-lookup"><span data-stu-id="21745-124">hello following example saves hello template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="21745-125">Zwraca lokalizację hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="21745-125">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="21745-126">Otwórz plik hello i Zauważ, że jest ona hello dokładne szablon, który można użyć do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="21745-126">Open hello file, and notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="21745-127">Witaj, parametry i zmienne odpowiada hello szablonu z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="21745-127">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="21745-128">Tego szablonu można wdrożyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="21745-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="21745-129">Eksportowanie grupy zasobów jako szablon</span><span class="sxs-lookup"><span data-stu-id="21745-129">Export resource group as template</span></span>

<span data-ttu-id="21745-130">Zamiast pobierania szablonu z historii wdrożenia hello, można pobrać szablonu, który reprezentuje hello bieżący stan grupy zasobów przy użyciu hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) polecenia.</span><span class="sxs-lookup"><span data-stu-id="21745-130">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="21745-131">Użyj tego polecenia, gdy wprowadzono wiele zmian tooyour zasobów grupy, a nie istniejący szablon reprezentuje wszystkie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="21745-131">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="21745-132">Zwraca lokalizację hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="21745-132">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="21745-133">Otwórz plik hello i zwróć uwagę, że jest inny niż szablon hello w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="21745-133">Open hello file, and notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="21745-134">Zawiera różne parametry i żadnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="21745-134">It has different parameters and no variables.</span></span> <span data-ttu-id="21745-135">Magazyn Hello jednostki SKU i lokalizacji są toovalues ustalony.</span><span class="sxs-lookup"><span data-stu-id="21745-135">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="21745-136">Witaj poniższy przykład przedstawia hello wyeksportowanego szablonu, ale szablon ma nazwę parametru nieco inne:</span><span class="sxs-lookup"><span data-stu-id="21745-136">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="21745-137">Można ponownie wdrożyć tego szablonu, ale wymaga to odgadnięcie unikatową nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="21745-137">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="21745-138">Nazwa parametru Hello różni się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="21745-138">hello name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="21745-139">Dostosowywanie wyeksportowanego szablonu</span><span class="sxs-lookup"><span data-stu-id="21745-139">Customize exported template</span></span>

<span data-ttu-id="21745-140">Toomake tego szablonu można modyfikować jej toouse łatwiejsze i bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="21745-140">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="21745-141">tooallow więcej lokalizacje, zmień hello lokalizacji właściwości toouse hello tej samej lokalizacji co hello grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="21745-141">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="21745-142">tooavoid o tooguess uniques nazwę konta magazynu, Usuń parametr hello nazwy konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="21745-142">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="21745-143">Dodaj parametr sufiks nazwy magazynu oraz Magazyn wersji:</span><span class="sxs-lookup"><span data-stu-id="21745-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="21745-144">Dodaj zmienną, który konstruuje hello nazwy konta magazynu z funkcją uniqueString hello:</span><span class="sxs-lookup"><span data-stu-id="21745-144">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="21745-145">Ustaw nazwę hello zmiennej toohello konta magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="21745-145">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="21745-146">Ustaw parametr toohello SKU hello:</span><span class="sxs-lookup"><span data-stu-id="21745-146">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="21745-147">Twój szablon wygląda teraz następująco:</span><span class="sxs-lookup"><span data-stu-id="21745-147">Your template now looks like:</span></span>

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

<span data-ttu-id="21745-148">Należy ponownie wdrożyć hello zmodyfikowany szablon.</span><span class="sxs-lookup"><span data-stu-id="21745-148">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21745-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21745-149">Next steps</span></span>
* <span data-ttu-id="21745-150">Aby dowiedzieć się, jak za pomocą portalu tooexport hello szablonu, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="21745-150">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="21745-151">Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="21745-151">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="21745-152">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="21745-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
