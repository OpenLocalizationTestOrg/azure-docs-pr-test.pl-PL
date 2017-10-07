---
title: "dysków zarządzanych w szablonie toouse ustawić aaaConvert skali usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Konwertuj szablonu zestaw skalowania zestaw szablonu tooa dysków zarządzanych w skali."
keywords: zestawy skalowania maszyny wirtualnej
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="4ff7a-104">Konwertuj szablonu zestaw skalowania zestaw szablonu tooa dysków zarządzanych w skali</span><span class="sxs-lookup"><span data-stu-id="4ff7a-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="4ff7a-105">Klienci z szablonem usługi Resource Manager służący do tworzenia ustawić nie za pomocą dysków zarządzanych w skali możesz toomodify on toouse zarządzane dysku.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="4ff7a-106">W tym artykule przedstawiono sposób toodo tym, używając jako przykład żądanie ściągnięcia z hello [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates), społeczność repozytorium dla przykładowych szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="4ff7a-107">żądanie ściągnięcia pełne Hello są widoczne w tym miejscu: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), i hello odpowiednich części różnicowego hello są poniżej, oraz objaśnienia:</span><span class="sxs-lookup"><span data-stu-id="4ff7a-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="4ff7a-108">Tworzenie dysków systemu operacyjnego hello zarządzanych</span><span class="sxs-lookup"><span data-stu-id="4ff7a-108">Making hello OS disks managed</span></span>

<span data-ttu-id="4ff7a-109">W hello diff poniżej widać, usunęliśmy kilku zmiennych toostorage powiązane konta i dysku właściwości.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="4ff7a-110">Typ konta magazynu nie jest już konieczne (Standard_LRS jest domyślnym hello), ale firma Microsoft może nadal określić czy firma zamierza.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="4ff7a-111">Tylko Standard_LRS i Premium_LRS są obsługiwane z dyskiem zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="4ff7a-112">Nowy sufiks konta magazynu, macierzy unikatowy ciąg i liczba sa były używane w hello starego szablonu toogenerate nazw kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="4ff7a-113">Te zmienne nie są już konieczne hello nowego szablonu ponieważ dysków zarządzanych automatycznie tworzy kont magazynu w imieniu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="4ff7a-114">Podobnie, nazwa kontenera wirtualnego dysku twardego i nazwa dysku systemu operacyjnego nie są już wymagane ponieważ dysków zarządzanych automatycznie nazwy hello podstawowej kontenerów obiektów blob magazynu i dyski.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="4ff7a-115">W różnicowego hello poniżej, firma Microsoft może zobacz, czy Zaktualizowaliśmy hello obliczeniowe interfejsu api w wersji too2016-04-30-preview, hello tak szybko, jak wymagana wersja do obsługi dysków zarządzanych zestawów skali.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="4ff7a-116">Należy pamiętać, że firma Microsoft może nadal niezarządzane dysków w nowej wersji interfejsu api hello z hello stara składnia w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="4ff7a-117">Innymi słowy, tylko aktualizacji hello obliczeniowe interfejsu api w wersji i nie należy zmieniać cokolwiek innego, hello szablonu powinno być kontynuowane toowork jako przed.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="4ff7a-118">W różnicowego hello poniżej możemy stwierdzić, że zostaną usunięte zasobów konta magazynu hello z tablicy zasobów hello całkowicie.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="4ff7a-119">Firma Microsoft nie jest już potrzebne dysków zarządzanych w tworzy je automatycznie w naszym imieniu.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="4ff7a-120">W różnicowego hello poniżej, firma Microsoft może zobacz usuwania hello zależy od klauzuli odwołujące się z hello skali zestaw toohello pętli, które tworzenia kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="4ff7a-121">Hello starego szablonu to został sprawdzeniu, czy hello konta magazynu zostały utworzone przed zestaw skali hello rozpoczęcia tworzenia, ale ta klauzula nie jest już konieczne z dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="4ff7a-122">Firma Microsoft również Usuń właściwość kontenery vhd hello i hello Właściwość Nazwa dysku systemu operacyjnego, jak te właściwości są automatycznie obsługiwane pod maską hello przez dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="4ff7a-123">Jeśli firma zamierza, firma Microsoft może dodać `"managedDisk": { "storageAccountType": "Premium_LRS" }` w konfiguracji "osDisk" hello, jeśli firma chce dysków systemu operacyjnego w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="4ff7a-124">Tylko maszyny wirtualne z wielkie lub małe firmy "w hello wirtualna sku można używać dysków premium.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="4ff7a-125">Nie ma jawnego właściwości w konfiguracji zestaw skalowania hello czy toouse zarządzane lub niezarządzane dysku.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="4ff7a-126">zestaw skali Hello wie, które toouse na podstawie właściwości hello, które znajdują się w profilu magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="4ff7a-127">W związku z tym ważne jest podczas modyfikowania hello tooensure szablon, że właściwości prawa hello znajdują się w profilu magazynu hello hello zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="4ff7a-128">Dyski danych</span><span class="sxs-lookup"><span data-stu-id="4ff7a-128">Data disks</span></span>

<span data-ttu-id="4ff7a-129">Zmiany hello powyżej hello skali zestaw używa zarządzanych dysków dla hello systemu operacyjnego na dysku, ale informacje o dyskach danych? tooadd dysków z danymi, Dodaj właściwość "dataDisks" hello "storageProfile" na poziomie takie same jak "osDisk" hello.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="4ff7a-130">Hello hello właściwość ma wartość JSON listę obiektów, z których każdy ma właściwości "lun" (która muszą być unikatowe dla każdego dysku danych na maszynie Wirtualnej), "createOption" ("pusta" jest obecnie hello — opcja obsługiwana tylko), a "diskSizeGB" (rozmiar dysku hello w gigabajtach hello; musi być większa niż 0 i mniejsza niż 1024) w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4ff7a-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="4ff7a-131">Jeśli określisz `n` dysków w tej macierzy, pobiera zestawu każdej maszyny Wirtualnej w skali hello `n` dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="4ff7a-132">Należy jednak pamiętać, że te dyski danych są urządzeniach niesformatowanych.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="4ff7a-133">Nie są sformatowane.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-133">They are not formatted.</span></span> <span data-ttu-id="4ff7a-134">Jest tooattach klienta toohello, paritition i format hello dysków przed ich użyciem.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="4ff7a-135">Opcjonalnie można również określono `"managedDisk": { "storageAccountType": "Premium_LRS" }` w każdym toospecify obiektu dysku danych powinien być dysk danych — warstwa premium.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="4ff7a-136">Tylko maszyny wirtualne z wielkie lub małe firmy "w hello wirtualna sku można używać dysków premium.</span><span class="sxs-lookup"><span data-stu-id="4ff7a-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="4ff7a-137">Zobacz toolearn więcej informacji o użyciu dysków z danymi zestawy skalowania [w tym artykule](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="4ff7a-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ff7a-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ff7a-138">Next steps</span></span>
<span data-ttu-id="4ff7a-139">Na przykład szablony Menedżera zasobów za pomocą zestawów skali, wyszukaj termin "vmss" w hello [repozytorium github szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="4ff7a-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="4ff7a-140">Aby uzyskać ogólne informacje, zapoznaj się z hello [strony głównej docelowej dla zestawów skalowania](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="4ff7a-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

