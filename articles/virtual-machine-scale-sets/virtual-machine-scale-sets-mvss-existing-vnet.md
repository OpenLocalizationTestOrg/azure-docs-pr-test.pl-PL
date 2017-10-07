---
title: "Odwołanie istniejącej sieci wirtualnej w szablonie zestaw skalowania Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd a wirtualnych sieci tooan istniejącego zestawu skalowania maszyn wirtualnych Azure szablonu"
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
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="0bdf3-103">Dodaj odwołanie tooan istniejącej sieci wirtualnej w szablonie zestaw skalowania Azure</span><span class="sxs-lookup"><span data-stu-id="0bdf3-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="0bdf3-104">W tym artykule przedstawiono sposób toomodify hello [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) toodeploy w istniejącej sieci wirtualnej, zamiast tworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="0bdf3-105">Zmień hello definicji szablonu</span><span class="sxs-lookup"><span data-stu-id="0bdf3-105">Change hello template definition</span></span>

<span data-ttu-id="0bdf3-106">Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i widoczne naszych szablon do wdrażania do istniejącej sieci wirtualnej zestaw skalowania hello [tutaj](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="0bdf3-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="0bdf3-107">Przeanalizujmy hello toocreate różnicowego używany ten szablon (`git diff minimum-viable-scale-set existing-vnet`) element przez element:</span><span class="sxs-lookup"><span data-stu-id="0bdf3-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="0bdf3-108">Najpierw dodamy `subnetId` parametru.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="0bdf3-109">Ten ciąg zostanie przekazany hello Konfiguracja zestawu skali, pozwalając hello zestawu skalowania maszyny wirtualnej utworzone wcześniej podsieci hello tooidentify toodeploy maszyn wirtualnych do.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="0bdf3-110">Ten ciąg musi mieć formę hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="0bdf3-111">Na przykład ustawić toodeploy hello skali w istniejącej sieci wirtualnej o nazwie `myvnet`, podsieci `mysubnet`, grupy zasobów `myrg`i subskrypcji `00000000-0000-0000-0000-000000000000`, będzie hello subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="0bdf3-112">Następnie możemy usunąć zasób sieci wirtualnej hello z hello `resources` tablicy, ponieważ firma Microsoft używają istniejącej sieci wirtualnej i nie wymagają toodeploy nowy.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

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

<span data-ttu-id="0bdf3-113">Hello sieci wirtualnej już istnieje, przed wdrożeniem hello szablon, więc nie ma żadnych toospecify potrzeby klauzulę dependsOn od skali hello Ustaw toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0bdf3-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="0bdf3-114">W związku z tym usunąć te wiersze:</span><span class="sxs-lookup"><span data-stu-id="0bdf3-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="0bdf3-115">Na koniec jest przekazywana w hello `subnetId` parametru ustawionych przez użytkownika hello (zamiast `resourceId` tooget hello identyfikator sieci wirtualnej w hello jest tego samego wdrożenia, czyli, jakie hello minimalnej wielkości ustawić szablonu).</span><span class="sxs-lookup"><span data-stu-id="0bdf3-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="0bdf3-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0bdf3-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
