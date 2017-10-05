---
title: "Odwołanie obraz niestandardowy w skali Azure Ustaw szablon | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać do istniejącego zestawu skalowania maszyn wirtualnych Azure szablonu niestandardowego obrazu"
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
ms.openlocfilehash: cf52fc9e95267c4bc5c0106aadf626685ddd5c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a><span data-ttu-id="bd46e-103">Dodawanie niestandardowego obrazu do szablonu zestaw skalowania Azure</span><span class="sxs-lookup"><span data-stu-id="bd46e-103">Add a custom image to an Azure scale set template</span></span>

<span data-ttu-id="bd46e-104">W tym artykule przedstawiono sposób modyfikowania [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) do wdrożenia z niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="bd46e-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy from custom image.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="bd46e-105">Zmiany definicji szablonu</span><span class="sxs-lookup"><span data-stu-id="bd46e-105">Change the template definition</span></span>

<span data-ttu-id="bd46e-106">Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i naszych szablonu dla wdrażania skali zestawu z niestandardowego obrazu widoczne [tutaj](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bd46e-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="bd46e-107">Przeanalizujmy różnicowego używany do tworzenia tego szablonu (`git diff minimum-viable-scale-set custom-image`) element przez element:</span><span class="sxs-lookup"><span data-stu-id="bd46e-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="bd46e-108">Tworzenie obrazu dysku zarządzanego</span><span class="sxs-lookup"><span data-stu-id="bd46e-108">Creating a managed disk image</span></span>

<span data-ttu-id="bd46e-109">Jeśli masz już obraz niestandardowy dysku zarządzanego (zasobu typu `Microsoft.Compute/images`), a następnie można pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="bd46e-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="bd46e-110">Najpierw dodamy `sourceImageVhdUri` parametr, który jest identyfikatorem URI do ogólnych obiektu blob w magazynie Azure, który zawiera niestandardowy obraz do wdrożenia z.</span><span class="sxs-lookup"><span data-stu-id="bd46e-110">First, we add a `sourceImageVhdUri` parameter, which is the URI to the generalized blob in Azure Storage that contains the custom image to deploy from.</span></span>


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "The source of the generalized blob containing the custom image"
+      }
     }
   },
   "variables": {},
```

<span data-ttu-id="bd46e-111">Następnie dodamy zasobu typu `Microsoft.Compute/images`, która jest oparta na ogólnych znajdujący się pod identyfikatorem URI obiektu blob obrazu dysków zarządzanych w `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="bd46e-111">Next, we add a resource of type `Microsoft.Compute/images`, which is the managed disk image based on the generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="bd46e-112">Ten obraz musi być w tym samym regionie co zestaw skalowania, która korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="bd46e-112">This image must be in the same region as the scale set that uses it.</span></span> <span data-ttu-id="bd46e-113">We właściwościach obrazu określono typ systemu operacyjnego, lokalizacji obiektu blob (z `sourceImageVhdUri` parametru), a typ konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="bd46e-113">In the properties of the image, we specify the OS type, the location of the blob (from the `sourceImageVhdUri` parameter), and the storage account type:</span></span>

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

<span data-ttu-id="bd46e-114">W zestawie skalowania zasobu, dodamy `dependsOn` klauzuli odwołujących się do niestandardowego obrazu, aby upewnić się, że obraz jest tworzony przed skali podejmuje próbę wdrożenia z tego obrazu:</span><span class="sxs-lookup"><span data-stu-id="bd46e-114">In the scale set resource, we add a `dependsOn` clause referring to the custom image to make sure the image gets created before the scale set tries to deploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a><span data-ttu-id="bd46e-115">Zmiana skali Ustaw właściwości, aby używać obrazu dysku twardego zarządzanego</span><span class="sxs-lookup"><span data-stu-id="bd46e-115">Changing scale set properties to use the managed disk image</span></span>

<span data-ttu-id="bd46e-116">W `imageReference` skali ustawić `storageProfile`, zamiast określania wydawcy, oferty, jednostki sku i wersji obrazu platformy, określono `id` z `Microsoft.Compute/images` zasobów:</span><span class="sxs-lookup"><span data-stu-id="bd46e-116">In the `imageReference` of the scale set `storageProfile`, instead of specifying the publisher, offer, sku, and version of a platform image, we specify the `id` of the `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="bd46e-117">W tym przykładzie używamy `resourceId` funkcji, aby uzyskać identyfikator zasobu obrazu utworzonego w tym samym szablonie.</span><span class="sxs-lookup"><span data-stu-id="bd46e-117">In this example, we use the `resourceId` function to get the resource ID of the image created in the same template.</span></span> <span data-ttu-id="bd46e-118">Jeśli wcześniej utworzono obrazu dysku twardego zarządzanego, należy zamiast tego Podaj identyfikator obrazu.</span><span class="sxs-lookup"><span data-stu-id="bd46e-118">If you have created the managed disk image beforehand, you should provide the id of that image instead.</span></span> <span data-ttu-id="bd46e-119">Ten identyfikator musi mieć postać: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="bd46e-119">This id must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd46e-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd46e-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
