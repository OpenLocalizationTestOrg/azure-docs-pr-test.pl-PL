---
title: "Lokalizacja zasobów platformy Azure w szablonie | Dokumentacja firmy Microsoft"
description: "Przedstawiono sposób ustawiania lokalizacji zasobu w szablonie usługi Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="3d0c6-103">Ustaw lokalizację zasobów w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d0c6-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="3d0c6-104">W przypadku wdrażania szablonu, należy podać lokalizację każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="3d0c6-105">W tym temacie przedstawiono sposób określenia lokalizacji, które są dostępne dla Twojej subskrypcji dla każdego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="3d0c6-106">Określić obsługiwane lokalizacje</span><span class="sxs-lookup"><span data-stu-id="3d0c6-106">Determine supported locations</span></span>

<span data-ttu-id="3d0c6-107">Aby uzyskać pełną listę obsługiwanych lokalizacji dla każdego typu zasobu, zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="3d0c6-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="3d0c6-108">Jednak subskrypcji może nie mieć dostępu do wszystkich lokalizacji na tej liście.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="3d0c6-109">Aby wyświetlić listę niestandardowe lokalizacje, które są dostępne dla Twojej subskrypcji, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="3d0c6-110">W poniższym przykładzie użyto programu PowerShell, aby pobrać lokalizacji dla `Microsoft.Web\sites` typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="3d0c6-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="3d0c6-111">W poniższym przykładzie użyto 2.0 interfejsu wiersza polecenia platformy Azure można pobrać lokalizacji dla `Microsoft.Web\sites` typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="3d0c6-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="3d0c6-112">Ustaw lokalizację, w szablonie</span><span class="sxs-lookup"><span data-stu-id="3d0c6-112">Set location in template</span></span>

<span data-ttu-id="3d0c6-113">Po ustaleniu obsługiwane lokalizacje dla zasobów, należy określić tę lokalizację w szablonie.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="3d0c6-114">Najprostszym sposobem ta wartość jest utworzenie grupy zasobów w lokalizacji, która obsługuje typy zasobów i ustawioną każdej lokalizacji `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="3d0c6-115">Można ponownie wdrożyć szablon do grup zasobów w różnych lokalizacjach i nie zmieniać wartości w szablonie lub parametrów.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="3d0c6-116">W poniższym przykładzie przedstawiono konta magazynu, który jest wdrożony w tej samej lokalizacji co grupa zasobów:</span><span class="sxs-lookup"><span data-stu-id="3d0c6-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="3d0c6-117">Jeśli potrzebujesz kodowania lokalizację w szablonie, podaj nazwę jednego z obsługiwanych regionów.</span><span class="sxs-lookup"><span data-stu-id="3d0c6-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="3d0c6-118">W poniższym przykładzie przedstawiono konta magazynu, który jest zawsze wdrożony w północno-środkowe stany:</span><span class="sxs-lookup"><span data-stu-id="3d0c6-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="3d0c6-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d0c6-119">Next steps</span></span>
* <span data-ttu-id="3d0c6-120">Aby uzyskać zalecenia dotyczące tworzenia szablonów, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="3d0c6-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

