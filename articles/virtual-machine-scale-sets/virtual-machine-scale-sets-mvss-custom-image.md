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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="3fc88-103">Dodawanie zestawu szablonu niestandardowego obrazu tooan Azure skali</span><span class="sxs-lookup"><span data-stu-id="3fc88-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="3fc88-104">W tym artykule przedstawiono sposób toomodify hello [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) toodeploy z niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="3fc88-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="3fc88-105">Zmień hello definicji szablonu</span><span class="sxs-lookup"><span data-stu-id="3fc88-105">Change hello template definition</span></span>

<span data-ttu-id="3fc88-106">Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i widoczne naszych szablon do wdrażania zestaw z obrazu niestandardowego skalowania hello [tutaj](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="3fc88-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="3fc88-107">Przeanalizujmy hello toocreate różnicowego używany ten szablon (`git diff minimum-viable-scale-set custom-image`) element przez element:</span><span class="sxs-lookup"><span data-stu-id="3fc88-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="3fc88-108">Tworzenie obrazu dysku zarządzanego</span><span class="sxs-lookup"><span data-stu-id="3fc88-108">Creating a managed disk image</span></span>

<span data-ttu-id="3fc88-109">Jeśli masz już obraz niestandardowy dysku zarządzanego (zasobu typu `Microsoft.Compute/images`), a następnie można pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="3fc88-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="3fc88-110">Najpierw dodamy `sourceImageVhdUri` parametru, który jest hello URI toohello uogólniony blob w magazynie Azure, zawierającą hello toodeploy niestandardowego obrazu z.</span><span class="sxs-lookup"><span data-stu-id="3fc88-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="3fc88-111">Następnie dodamy zasobu typu `Microsoft.Compute/images`, która obrazu dysku twardego zarządzanego hello opiera się na powitania uogólniony obiektu blob znajduje się pod identyfikatorem URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="3fc88-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="3fc88-112">Ten obraz musi być w hello hello skali zestaw, który używa tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="3fc88-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="3fc88-113">We właściwościach hello hello obrazu, możemy określić typ hello systemu operacyjnego, hello lokalizacji obiektu hello blob (z hello `sourceImageVhdUri` parametru), a typ konta magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="3fc88-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="3fc88-114">W hello zestawu skalowania zasobu, dodamy `dependsOn` klauzuli przywołuje toomake niestandardowego obrazu toohello się obraz powitania pobiera utworzone przed zestaw skali hello próbuje toodeploy z tego obrazu:</span><span class="sxs-lookup"><span data-stu-id="3fc88-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="3fc88-115">Zmiana skali ustawić właściwości toouse hello dysków zarządzanych w obrazie</span><span class="sxs-lookup"><span data-stu-id="3fc88-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="3fc88-116">W hello `imageReference` skali hello ustawić `storageProfile`, zamiast określania hello wydawcy, oferty, jednostki sku i wersji obrazu platformy, określono hello `id` z hello `Microsoft.Compute/images` zasobów:</span><span class="sxs-lookup"><span data-stu-id="3fc88-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="3fc88-117">W tym przykładzie używamy hello `resourceId` funkcja tooget hello identyfikator zasobu obrazu hello utworzone w hello sam szablonu.</span><span class="sxs-lookup"><span data-stu-id="3fc88-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="3fc88-118">Jeśli wcześniej utworzono obrazu dysku twardego zarządzanego hello, należy zamiast tego Podaj identyfikator hello tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="3fc88-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="3fc88-119">Ten identyfikator musi mieć formę hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="3fc88-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3fc88-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3fc88-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
