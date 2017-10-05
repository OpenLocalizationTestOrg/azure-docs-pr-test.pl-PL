---
title: "Eksportowanie szablonu usługi Resource Manager z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Resource Manager i interfejsu wiersza polecenia Azure, aby wyeksportować szablon na podstawie grupy zasobów."
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
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="27fc8-103">Eksportowanie szablonów usługi Azure Resource Manager z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="27fc8-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="27fc8-104">Usługa Resource Manager umożliwia wyeksportowanie szablonu usługi Resource Manager z istniejących zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="27fc8-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="27fc8-105">Możesz użyć wygenerowanego szablonu, aby dowiedzieć się więcej o składni szablonu lub aby zautomatyzować ponowne wdrożenie rozwiązania, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="27fc8-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="27fc8-106">Należy pamiętać, że istnieją dwa różne sposoby eksportowania szablonu:</span><span class="sxs-lookup"><span data-stu-id="27fc8-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="27fc8-107">Możesz wyeksportować szablon, który faktycznie został użyty na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="27fc8-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="27fc8-108">W wyeksportowanym szablonie wszystkie parametry i zmienne występują dokładnie tak, jak w oryginalnym szablonie.</span><span class="sxs-lookup"><span data-stu-id="27fc8-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="27fc8-109">Takie podejście jest przydatne, gdy jest potrzebne do pobierania szablonu.</span><span class="sxs-lookup"><span data-stu-id="27fc8-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="27fc8-110">Możesz wyeksportować szablon, który reprezentuje bieżący stan grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="27fc8-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="27fc8-111">Wyeksportowany szablon nie jest oparty na żadnym szablonie użytym do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="27fc8-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="27fc8-112">Utworzony szablon będzie stanowić migawkę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="27fc8-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="27fc8-113">W wyeksportowanym szablonie zawartych jest wiele zakodowanych wartości i prawdopodobnie mniej parametrów, niż się zwykle definiuje.</span><span class="sxs-lookup"><span data-stu-id="27fc8-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="27fc8-114">Takie rozwiązanie jest przydatne, gdy zostały zmodyfikowane grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="27fc8-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="27fc8-115">Będzie więc trzeba przechwycić grupę zasobów jako szablon.</span><span class="sxs-lookup"><span data-stu-id="27fc8-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="27fc8-116">W tym temacie opisano obie te metody.</span><span class="sxs-lookup"><span data-stu-id="27fc8-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="27fc8-117">Wdrażanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="27fc8-117">Deploy a solution</span></span>

<span data-ttu-id="27fc8-118">Aby zilustrować obu podejść eksportowania szablonu, Zacznijmy od wdrażanie rozwiązania do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="27fc8-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="27fc8-119">Jeśli masz już grupę zasobów w ramach subskrypcji, który chcesz wyeksportować, nie trzeba wdrożyć to rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="27fc8-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="27fc8-120">Jednak w dalszej części tego artykułu odwołuje się do szablonu dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="27fc8-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="27fc8-121">Przykładowy skrypt wdraża konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="27fc8-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="27fc8-122">Zapisz szablon z historii wdrożenia</span><span class="sxs-lookup"><span data-stu-id="27fc8-122">Save template from deployment history</span></span>

<span data-ttu-id="27fc8-123">Można pobrać szablonu z historii wdrożenia za pomocą [eksportowanie wdrożenia grupy az](/cli/azure/group/deployment#export) polecenia.</span><span class="sxs-lookup"><span data-stu-id="27fc8-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="27fc8-124">Poniższy przykład zapisuje szablon, który wcześniej wdrażania:</span><span class="sxs-lookup"><span data-stu-id="27fc8-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="27fc8-125">Zwraca szablonu.</span><span class="sxs-lookup"><span data-stu-id="27fc8-125">It returns the template.</span></span> <span data-ttu-id="27fc8-126">Skopiuj kod JSON i Zapisz jako plik.</span><span class="sxs-lookup"><span data-stu-id="27fc8-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="27fc8-127">Zwróć uwagę, że jest dokładne szablon, którego można użyć do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="27fc8-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="27fc8-128">Parametry i zmienne pasuje do szablonu z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="27fc8-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="27fc8-129">Tego szablonu można wdrożyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="27fc8-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="27fc8-130">Eksportowanie grupy zasobów jako szablon</span><span class="sxs-lookup"><span data-stu-id="27fc8-130">Export resource group as template</span></span>

<span data-ttu-id="27fc8-131">Zamiast pobierania szablonu z historii wdrażania, można pobrać szablonu, która reprezentuje bieżący stan grupy zasobów za pomocą [eksportowanie grupy az](/cli/azure/group#export) polecenia.</span><span class="sxs-lookup"><span data-stu-id="27fc8-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="27fc8-132">Użyj tego polecenia, gdy wprowadzono wiele zmian w danej grupie zasobów, a nie istniejący szablon reprezentuje wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="27fc8-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="27fc8-133">Zwraca szablonu.</span><span class="sxs-lookup"><span data-stu-id="27fc8-133">It returns the template.</span></span> <span data-ttu-id="27fc8-134">Skopiuj kod JSON i Zapisz jako plik.</span><span class="sxs-lookup"><span data-stu-id="27fc8-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="27fc8-135">Należy zauważyć, że różni się od szablonu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="27fc8-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="27fc8-136">Zawiera różne parametry i żadnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="27fc8-136">It has different parameters and no variables.</span></span> <span data-ttu-id="27fc8-137">Magazyn jednostki SKU i lokalizacji są zakodowane na stałe wartości.</span><span class="sxs-lookup"><span data-stu-id="27fc8-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="27fc8-138">W poniższym przykładzie przedstawiono wyeksportowanego szablonu, ale szablon ma nazwę parametru nieco inne:</span><span class="sxs-lookup"><span data-stu-id="27fc8-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="27fc8-139">Można ponownie wdrożyć tego szablonu, ale wymaga to odgadnięcie unikatową nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="27fc8-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="27fc8-140">Nazwa parametru jest nieco inne.</span><span class="sxs-lookup"><span data-stu-id="27fc8-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="27fc8-141">Dostosowywanie wyeksportowanego szablonu</span><span class="sxs-lookup"><span data-stu-id="27fc8-141">Customize exported template</span></span>

<span data-ttu-id="27fc8-142">Można zmodyfikować tego szablonu, aby była łatwiejsza w użyciu i bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="27fc8-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="27fc8-143">Aby umożliwić więcej lokalizacji, zmień właściwość lokalizacji do użycia w tej samej lokalizacji co grupa zasobów:</span><span class="sxs-lookup"><span data-stu-id="27fc8-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="27fc8-144">Aby uniknąć konieczności odgadnąć uniques nazwę konta magazynu, należy usunąć parametr nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="27fc8-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="27fc8-145">Dodaj parametr sufiks nazwy magazynu oraz Magazyn wersji:</span><span class="sxs-lookup"><span data-stu-id="27fc8-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="27fc8-146">Dodawanie zmiennej, która tworzy nazwę konta magazynu przy użyciu funkcji uniqueString:</span><span class="sxs-lookup"><span data-stu-id="27fc8-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="27fc8-147">Do zmiennej, należy ustawić nazwę konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="27fc8-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="27fc8-148">Jednostka SKU zestawu do parametru:</span><span class="sxs-lookup"><span data-stu-id="27fc8-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="27fc8-149">Twój szablon wygląda teraz następująco:</span><span class="sxs-lookup"><span data-stu-id="27fc8-149">Your template now looks like:</span></span>

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

<span data-ttu-id="27fc8-150">Należy ponownie wdrożyć zmodyfikowany szablon.</span><span class="sxs-lookup"><span data-stu-id="27fc8-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27fc8-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="27fc8-151">Next steps</span></span>
* <span data-ttu-id="27fc8-152">Aby uzyskać informacje dotyczące korzystania z portalu, aby wyeksportować szablon, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="27fc8-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="27fc8-153">Aby określić parametry w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="27fc8-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="27fc8-154">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="27fc8-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>