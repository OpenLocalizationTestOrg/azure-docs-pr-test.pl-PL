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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Dodaj odwołanie tooan istniejącej sieci wirtualnej w szablonie zestaw skalowania Azure

W tym artykule przedstawiono sposób toomodify hello [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) toodeploy w istniejącej sieci wirtualnej, zamiast tworzyć nowy.

## <a name="change-hello-template-definition"></a>Zmień hello definicji szablonu

Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i widoczne naszych szablon do wdrażania do istniejącej sieci wirtualnej zestaw skalowania hello [tutaj](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Przeanalizujmy hello toocreate różnicowego używany ten szablon (`git diff minimum-viable-scale-set existing-vnet`) element przez element:

Najpierw dodamy `subnetId` parametru. Ten ciąg zostanie przekazany hello Konfiguracja zestawu skali, pozwalając hello zestawu skalowania maszyny wirtualnej utworzone wcześniej podsieci hello tooidentify toodeploy maszyn wirtualnych do. Ten ciąg musi mieć formę hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Na przykład ustawić toodeploy hello skali w istniejącej sieci wirtualnej o nazwie `myvnet`, podsieci `mysubnet`, grupy zasobów `myrg`i subskrypcji `00000000-0000-0000-0000-000000000000`, będzie hello subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

Następnie możemy usunąć zasób sieci wirtualnej hello z hello `resources` tablicy, ponieważ firma Microsoft używają istniejącej sieci wirtualnej i nie wymagają toodeploy nowy.

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

Hello sieci wirtualnej już istnieje, przed wdrożeniem hello szablon, więc nie ma żadnych toospecify potrzeby klauzulę dependsOn od skali hello Ustaw toohello sieci wirtualnej. W związku z tym usunąć te wiersze:

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

Na koniec jest przekazywana w hello `subnetId` parametru ustawionych przez użytkownika hello (zamiast `resourceId` tooget hello identyfikator sieci wirtualnej w hello jest tego samego wdrożenia, czyli, jakie hello minimalnej wielkości ustawić szablonu).

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




## <a name="next-steps"></a>Następne kroki

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
