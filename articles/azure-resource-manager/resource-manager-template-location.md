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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Ustaw lokalizację zasobów w szablonach usługi Azure Resource Manager
W przypadku wdrażania szablonu, należy podać lokalizację każdego zasobu. W tym temacie przedstawiono, jak typ toodetermine hello lokalizacje, które są dostępne tooyour subskrypcji dla każdego zasobu.

## <a name="determine-supported-locations"></a>Określić obsługiwane lokalizacje

Aby uzyskać pełną listę obsługiwanych lokalizacji dla każdego typu zasobu, zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/). Jednak subskrypcji może nie mieć dostępu tooall hello lokalizacji na tej liście. toosee niestandardową listą lokalizacje, które są dostępne tooyour subskrypcji, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure. 

Witaj poniższym przykładzie użyto lokalizacje hello tooget środowiska PowerShell dla hello `Microsoft.Web\sites` typu zasobu:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Witaj poniższym przykładzie użyto Azure CLI 2.0 tooget hello lokalizacji dla hello `Microsoft.Web\sites` typu zasobu:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Ustaw lokalizację, w szablonie

Po ustaleniu hello obsługiwane lokalizacje dla zasobów, należy tooset tej lokalizacji w szablonie. Witaj najprostszy sposób tooset, ta wartość jest toocreate zasób grupy w lokalizacji, która obsługuje typy zasobów hello i ustawić także każdej lokalizacji`[resourceGroup().location]`. Można ponownie wdrożyć hello grup tooresource szablonów w różnych lokalizacjach i nie zmieniać wartości w szablonie hello lub parametrów. 

Witaj poniższy przykład przedstawia konto magazynu, który jest wdrożony toohello tej samej lokalizacji co hello grupy zasobów:

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

Jeśli potrzebujesz toohardcode hello lokalizacji w szablonie, podaj nazwę hello regionów hello obsługiwane. Witaj poniższy przykład przedstawia konto magazynu, który jest zawsze wdrożone tooNorth środkowe stany USA:

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

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać zalecenia dotyczące toocreate szablonów, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).

