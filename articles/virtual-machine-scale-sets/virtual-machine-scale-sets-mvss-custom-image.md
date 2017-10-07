---
title: "Odwołanie obraz niestandardowy w skali Azure Ustaw szablon | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd niestandardowego obrazu tooan istniejący szablon Azure zestaw skali maszyny wirtualnej"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Dodawanie zestawu szablonu niestandardowego obrazu tooan Azure skali

W tym artykule przedstawiono sposób toomodify hello [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) toodeploy z niestandardowego obrazu.

## <a name="change-hello-template-definition"></a>Zmień hello definicji szablonu

Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i widoczne naszych szablon do wdrażania zestaw z obrazu niestandardowego skalowania hello [tutaj](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Przeanalizujmy hello toocreate różnicowego używany ten szablon (`git diff minimum-viable-scale-set custom-image`) element przez element:

### <a name="creating-a-managed-disk-image"></a>Tworzenie obrazu dysku zarządzanego

Jeśli masz już obraz niestandardowy dysku zarządzanego (zasobu typu `Microsoft.Compute/images`), a następnie można pominąć tę sekcję.

Najpierw dodamy `sourceImageVhdUri` parametru, który jest hello URI toohello uogólniony blob w magazynie Azure, zawierającą hello toodeploy niestandardowego obrazu z.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Następnie dodamy zasobu typu `Microsoft.Compute/images`, która obrazu dysku twardego zarządzanego hello opiera się na powitania uogólniony obiektu blob znajduje się pod identyfikatorem URI `sourceImageVhdUri`. Ten obraz musi być w hello hello skali zestaw, który używa tego samego regionu. We właściwościach hello hello obrazu, możemy określić typ hello systemu operacyjnego, hello lokalizacji obiektu hello blob (z hello `sourceImageVhdUri` parametru), a typ konta magazynu hello:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

W hello zestawu skalowania zasobu, dodamy `dependsOn` klauzuli przywołuje toomake niestandardowego obrazu toohello się obraz powitania pobiera utworzone przed zestaw skali hello próbuje toodeploy z tego obrazu:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Zmiana skali ustawić właściwości toouse hello dysków zarządzanych w obrazie

W hello `imageReference` skali hello ustawić `storageProfile`, zamiast określania hello wydawcy, oferty, jednostki sku i wersji obrazu platformy, określono hello `id` z hello `Microsoft.Compute/images` zasobów:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

W tym przykładzie używamy hello `resourceId` funkcja tooget hello identyfikator zasobu obrazu hello utworzone w hello sam szablonu. Jeśli wcześniej utworzono obrazu dysku twardego zarządzanego hello, należy zamiast tego Podaj identyfikator hello tego obrazu. Ten identyfikator musi mieć formę hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Następne kroki

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
