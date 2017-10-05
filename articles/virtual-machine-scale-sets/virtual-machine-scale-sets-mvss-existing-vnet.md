---
title: "Odwołanie istniejącej sieci wirtualnej w szablonie zestaw skalowania Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać sieć wirtualną do istniejącego zestawu skalowania maszyn wirtualnych Azure szablonu"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: 28117d467b491704aed8d45e5eba42530579dfa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="7789b-103">Dodaj odwołanie do istniejącej sieci wirtualnej w szablonie zestaw skalowania Azure</span><span class="sxs-lookup"><span data-stu-id="7789b-103">Add reference to an existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="7789b-104">W tym artykule przedstawiono sposób modyfikowania [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) do wdrożenia w ramach istniejącej sieci wirtualnej, zamiast tworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="7789b-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="7789b-105">Zmiany definicji szablonu</span><span class="sxs-lookup"><span data-stu-id="7789b-105">Change the template definition</span></span>

<span data-ttu-id="7789b-106">Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i naszych szablon do wdrażania do istniejącej sieci wirtualnej zestaw skali są widoczne [tutaj](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7789b-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="7789b-107">Przeanalizujmy różnicowego używany do tworzenia tego szablonu (`git diff minimum-viable-scale-set existing-vnet`) element przez element:</span><span class="sxs-lookup"><span data-stu-id="7789b-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="7789b-108">Najpierw dodamy `subnetId` parametru.</span><span class="sxs-lookup"><span data-stu-id="7789b-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="7789b-109">Ten ciąg zostanie przekazany Konfiguracja zestawu skali, dzięki czemu zestaw do identyfikowania wstępnie utworzone podsieci do wdrażania maszyn wirtualnych do skalowania.</span><span class="sxs-lookup"><span data-stu-id="7789b-109">This string will be passed into the scale set configuration, allowing the scale set to identify the pre-created subnet to deploy virtual machines into.</span></span> <span data-ttu-id="7789b-110">Ten ciąg musi mieć postać: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="7789b-110">This string must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="7789b-111">Na przykład, aby wdrożyć skali należy ustawić w istniejącej sieci wirtualnej o nazwie `myvnet`, podsieci `mysubnet`, grupy zasobów `myrg`i subskrypcji `00000000-0000-0000-0000-000000000000`, będzie subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="7789b-111">For instance, to deploy the scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, the subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

<span data-ttu-id="7789b-112">Następnie można usunąć zasobu sieci wirtualnej z `resources` tablicy, ponieważ firma Microsoft używają istniejącej sieci wirtualnej, a nie potrzeba wdrożenia nowej.</span><span class="sxs-lookup"><span data-stu-id="7789b-112">Next, we can delete the virtual network resource from the `resources` array, since we are using an existing virtual network and don't need to deploy a new one.</span></span>

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

<span data-ttu-id="7789b-113">Sieć wirtualna już istnieje przed wdrożeniem szablon, więc nie istnieje potrzeba do określenia klauzuli dependsOn od skali ustawioną sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7789b-113">The virtual network already exists before the template is deployed, so there is no need to specify a dependsOn clause from the scale set to the virtual network.</span></span> <span data-ttu-id="7789b-114">W związku z tym usunąć te wiersze:</span><span class="sxs-lookup"><span data-stu-id="7789b-114">Thus, we delete these lines:</span></span>

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

<span data-ttu-id="7789b-115">Na koniec jest przekazywana w `subnetId` parametru ustawiony przez użytkownika (zamiast `resourceId` można pobrać identyfikatora sieci wirtualnej w ramach tego samego wdrożenia, który ma co minimalnej wielkości ustawić szablon jest).</span><span class="sxs-lookup"><span data-stu-id="7789b-115">Finally, we pass in the `subnetId` parameter set by the user (instead of using `resourceId` to get the id of a vnet in the same deployment, which is what the minimum viable scale set template does).</span></span>

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a><span data-ttu-id="7789b-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7789b-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
