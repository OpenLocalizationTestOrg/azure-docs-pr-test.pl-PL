---
title: Lokalizacja zasobu aaaAzure w szablonie | Dokumentacja firmy Microsoft
description: "Pokazuje sposób tooset lokalizacji dla zasobu w szablonie usługi Azure Resource Manager"
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
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="48d61-103">Ustaw lokalizację zasobów w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48d61-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="48d61-104">W przypadku wdrażania szablonu, należy podać lokalizację każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="48d61-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="48d61-105">W tym temacie przedstawiono, jak typ toodetermine hello lokalizacje, które są dostępne tooyour subskrypcji dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="48d61-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="48d61-106">Określić obsługiwane lokalizacje</span><span class="sxs-lookup"><span data-stu-id="48d61-106">Determine supported locations</span></span>

<span data-ttu-id="48d61-107">Aby uzyskać pełną listę obsługiwanych lokalizacji dla każdego typu zasobu, zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="48d61-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="48d61-108">Jednak subskrypcji może nie mieć dostępu tooall hello lokalizacji na tej liście.</span><span class="sxs-lookup"><span data-stu-id="48d61-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="48d61-109">toosee niestandardową listą lokalizacje, które są dostępne tooyour subskrypcji, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="48d61-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="48d61-110">Witaj poniższym przykładzie użyto lokalizacje hello tooget środowiska PowerShell dla hello `Microsoft.Web\sites` typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="48d61-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="48d61-111">Witaj poniższym przykładzie użyto Azure CLI 2.0 tooget hello lokalizacji dla hello `Microsoft.Web\sites` typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="48d61-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="48d61-112">Ustaw lokalizację, w szablonie</span><span class="sxs-lookup"><span data-stu-id="48d61-112">Set location in template</span></span>

<span data-ttu-id="48d61-113">Po ustaleniu hello obsługiwane lokalizacje dla zasobów, należy tooset tej lokalizacji w szablonie.</span><span class="sxs-lookup"><span data-stu-id="48d61-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="48d61-114">Witaj najprostszy sposób tooset, ta wartość jest toocreate zasób grupy w lokalizacji, która obsługuje typy zasobów hello i ustawić także każdej lokalizacji`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="48d61-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="48d61-115">Można ponownie wdrożyć hello grup tooresource szablonów w różnych lokalizacjach i nie zmieniać wartości w szablonie hello lub parametrów.</span><span class="sxs-lookup"><span data-stu-id="48d61-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="48d61-116">Witaj poniższy przykład przedstawia konto magazynu, który jest wdrożony toohello tej samej lokalizacji co hello grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="48d61-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

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

<span data-ttu-id="48d61-117">Jeśli potrzebujesz toohardcode hello lokalizacji w szablonie, podaj nazwę hello regionów hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="48d61-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="48d61-118">Witaj poniższy przykład przedstawia konto magazynu, który jest zawsze wdrożone tooNorth środkowe stany USA:</span><span class="sxs-lookup"><span data-stu-id="48d61-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="48d61-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48d61-119">Next steps</span></span>
* <span data-ttu-id="48d61-120">Aby uzyskać zalecenia dotyczące toocreate szablonów, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="48d61-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

