---
title: "aaaExport szablonu usługi Resource Manager z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i interfejsu wiersza polecenia Azure tooexport szablonu z grupą zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="64216-103">Eksportowanie szablonów usługi Azure Resource Manager z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="64216-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="64216-104">Menedżer zasobów pozwala tooexport szablonem usługi Resource Manager z istniejących zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="64216-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="64216-105">Możesz użyć tego toolearn wygenerowanego szablonu o hello szablonu składni lub tooautomate hello ponowne wdrożenie rozwiązania zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="64216-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="64216-106">Jest ważne toonote, że istnieją dwa różne sposoby tooexport szablonu:</span><span class="sxs-lookup"><span data-stu-id="64216-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="64216-107">Można wyeksportować szablon rzeczywiste hello używany we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="64216-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="64216-108">Hello wyeksportowanego szablonu obejmuje wszystkie hello parametry i zmienne, dokładnie tak, jak znalazły się na oryginalnym szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="64216-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="64216-109">Takie podejście jest przydatne, gdy będziesz potrzebować tooretrieve szablonu.</span><span class="sxs-lookup"><span data-stu-id="64216-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="64216-110">Można wyeksportować szablon, który reprezentuje bieżący stan hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="64216-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="64216-111">Witaj wyeksportowanego szablonu nie jest oparta na dowolnego szablonu, który został użyty do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="64216-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="64216-112">Zamiast tego tworzy szablon, który jest migawką hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="64216-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="64216-113">Witaj wyeksportowanego szablonu ma wiele wartości stałe i prawdopodobnie nie jako wiele parametrów, jak zwykle należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="64216-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="64216-114">Takie podejście jest przydatne, gdy zmieniono hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="64216-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="64216-115">Teraz należy grupy zasobów hello toocapture jako szablon.</span><span class="sxs-lookup"><span data-stu-id="64216-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="64216-116">W tym temacie opisano obie te metody.</span><span class="sxs-lookup"><span data-stu-id="64216-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="64216-117">Wdrażanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="64216-117">Deploy a solution</span></span>

<span data-ttu-id="64216-118">tooillustrate zarówno zbliża się do eksportowania szablonu, Zacznijmy poprzez wdrożenie rozwiązania tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="64216-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="64216-119">Jeśli masz już grupę zasobów w ramach subskrypcji, które mają tooexport, nie masz toodeploy tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="64216-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="64216-120">Jednak hello dalszej części tego artykułu odwołuje się szablon toohello dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="64216-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="64216-121">skrypt przykładowy Hello wdraża konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="64216-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="64216-122">Zapisz szablon z historii wdrożenia</span><span class="sxs-lookup"><span data-stu-id="64216-122">Save template from deployment history</span></span>

<span data-ttu-id="64216-123">Można pobrać szablonu z historii wdrożenia przy użyciu hello [eksportowanie wdrożenia grupy az](/cli/azure/group/deployment#export) polecenia.</span><span class="sxs-lookup"><span data-stu-id="64216-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="64216-124">następujące przykładowe zapisuje hello szablon, który wcześniej wdrażanie Hello:</span><span class="sxs-lookup"><span data-stu-id="64216-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="64216-125">Zwraca hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="64216-125">It returns hello template.</span></span> <span data-ttu-id="64216-126">Skopiuj hello JSON i Zapisz jako plik.</span><span class="sxs-lookup"><span data-stu-id="64216-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="64216-127">Zwróć uwagę, jest hello dokładne szablon, który można użyć do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="64216-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="64216-128">Witaj, parametry i zmienne odpowiada hello szablonu z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="64216-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="64216-129">Tego szablonu można wdrożyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="64216-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="64216-130">Eksportowanie grupy zasobów jako szablon</span><span class="sxs-lookup"><span data-stu-id="64216-130">Export resource group as template</span></span>

<span data-ttu-id="64216-131">Zamiast pobierania szablonu z historii wdrożenia hello, można pobrać szablonu, który reprezentuje hello bieżący stan grupy zasobów przy użyciu hello [eksportowanie grupy az](/cli/azure/group#export) polecenia.</span><span class="sxs-lookup"><span data-stu-id="64216-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="64216-132">Użyj tego polecenia, gdy wprowadzono wiele zmian tooyour zasobów grupy, a nie istniejący szablon reprezentuje wszystkie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="64216-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="64216-133">Zwraca hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="64216-133">It returns hello template.</span></span> <span data-ttu-id="64216-134">Skopiuj hello JSON i Zapisz jako plik.</span><span class="sxs-lookup"><span data-stu-id="64216-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="64216-135">Należy zauważyć, że różni się od szablonu hello w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="64216-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="64216-136">Zawiera różne parametry i żadnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="64216-136">It has different parameters and no variables.</span></span> <span data-ttu-id="64216-137">Magazyn Hello jednostki SKU i lokalizacji są toovalues ustalony.</span><span class="sxs-lookup"><span data-stu-id="64216-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="64216-138">Witaj poniższy przykład przedstawia hello wyeksportowanego szablonu, ale szablon ma nazwę parametru nieco inne:</span><span class="sxs-lookup"><span data-stu-id="64216-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="64216-139">Można ponownie wdrożyć tego szablonu, ale wymaga to odgadnięcie unikatową nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="64216-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="64216-140">Nazwa parametru Hello różni się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="64216-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="64216-141">Dostosowywanie wyeksportowanego szablonu</span><span class="sxs-lookup"><span data-stu-id="64216-141">Customize exported template</span></span>

<span data-ttu-id="64216-142">Toomake tego szablonu można modyfikować jej toouse łatwiejsze i bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="64216-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="64216-143">tooallow więcej lokalizacje, zmień hello lokalizacji właściwości toouse hello tej samej lokalizacji co hello grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="64216-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="64216-144">tooavoid o tooguess uniques nazwę konta magazynu, Usuń parametr hello nazwy konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="64216-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="64216-145">Dodaj parametr sufiks nazwy magazynu oraz Magazyn wersji:</span><span class="sxs-lookup"><span data-stu-id="64216-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="64216-146">Dodaj zmienną, który konstruuje hello nazwy konta magazynu z funkcją uniqueString hello:</span><span class="sxs-lookup"><span data-stu-id="64216-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="64216-147">Ustaw nazwę hello zmiennej toohello konta magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="64216-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="64216-148">Ustaw parametr toohello SKU hello:</span><span class="sxs-lookup"><span data-stu-id="64216-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="64216-149">Twój szablon wygląda teraz następująco:</span><span class="sxs-lookup"><span data-stu-id="64216-149">Your template now looks like:</span></span>

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

<span data-ttu-id="64216-150">Należy ponownie wdrożyć hello zmodyfikowany szablon.</span><span class="sxs-lookup"><span data-stu-id="64216-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64216-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64216-151">Next steps</span></span>
* <span data-ttu-id="64216-152">Aby dowiedzieć się, jak za pomocą portalu tooexport hello szablonu, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="64216-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="64216-153">Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="64216-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="64216-154">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="64216-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>