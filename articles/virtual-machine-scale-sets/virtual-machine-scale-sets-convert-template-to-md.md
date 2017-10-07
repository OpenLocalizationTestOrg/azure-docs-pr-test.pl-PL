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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Konwertuj szablonu zestaw skalowania zestaw szablonu tooa dysków zarządzanych w skali

Klienci z szablonem usługi Resource Manager służący do tworzenia ustawić nie za pomocą dysków zarządzanych w skali możesz toomodify on toouse zarządzane dysku. W tym artykule przedstawiono sposób toodo tym, używając jako przykład żądanie ściągnięcia z hello [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates), społeczność repozytorium dla przykładowych szablonów usługi Resource Manager. żądanie ściągnięcia pełne Hello są widoczne w tym miejscu: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), i hello odpowiednich części różnicowego hello są poniżej, oraz objaśnienia:

## <a name="making-hello-os-disks-managed"></a>Tworzenie dysków systemu operacyjnego hello zarządzanych

W hello diff poniżej widać, usunęliśmy kilku zmiennych toostorage powiązane konta i dysku właściwości. Typ konta magazynu nie jest już konieczne (Standard_LRS jest domyślnym hello), ale firma Microsoft może nadal określić czy firma zamierza. Tylko Standard_LRS i Premium_LRS są obsługiwane z dyskiem zarządzanym. Nowy sufiks konta magazynu, macierzy unikatowy ciąg i liczba sa były używane w hello starego szablonu toogenerate nazw kont magazynu. Te zmienne nie są już konieczne hello nowego szablonu ponieważ dysków zarządzanych automatycznie tworzy kont magazynu w imieniu powitania klienta. Podobnie, nazwa kontenera wirtualnego dysku twardego i nazwa dysku systemu operacyjnego nie są już wymagane ponieważ dysków zarządzanych automatycznie nazwy hello podstawowej kontenerów obiektów blob magazynu i dyski.

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


W różnicowego hello poniżej, firma Microsoft może zobacz, czy Zaktualizowaliśmy hello obliczeniowe interfejsu api w wersji too2016-04-30-preview, hello tak szybko, jak wymagana wersja do obsługi dysków zarządzanych zestawów skali. Należy pamiętać, że firma Microsoft może nadal niezarządzane dysków w nowej wersji interfejsu api hello z hello stara składnia w razie potrzeby. Innymi słowy, tylko aktualizacji hello obliczeniowe interfejsu api w wersji i nie należy zmieniać cokolwiek innego, hello szablonu powinno być kontynuowane toowork jako przed.

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

W różnicowego hello poniżej możemy stwierdzić, że zostaną usunięte zasobów konta magazynu hello z tablicy zasobów hello całkowicie. Firma Microsoft nie jest już potrzebne dysków zarządzanych w tworzy je automatycznie w naszym imieniu.

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

W różnicowego hello poniżej, firma Microsoft może zobacz usuwania hello zależy od klauzuli odwołujące się z hello skali zestaw toohello pętli, które tworzenia kont magazynu. Hello starego szablonu to został sprawdzeniu, czy hello konta magazynu zostały utworzone przed zestaw skali hello rozpoczęcia tworzenia, ale ta klauzula nie jest już konieczne z dysków zarządzanych. Firma Microsoft również Usuń właściwość kontenery vhd hello i hello Właściwość Nazwa dysku systemu operacyjnego, jak te właściwości są automatycznie obsługiwane pod maską hello przez dysków zarządzanych. Jeśli firma zamierza, firma Microsoft może dodać `"managedDisk": { "storageAccountType": "Premium_LRS" }` w konfiguracji "osDisk" hello, jeśli firma chce dysków systemu operacyjnego w warstwie premium. Tylko maszyny wirtualne z wielkie lub małe firmy "w hello wirtualna sku można używać dysków premium.

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

Nie ma jawnego właściwości w konfiguracji zestaw skalowania hello czy toouse zarządzane lub niezarządzane dysku. zestaw skali Hello wie, które toouse na podstawie właściwości hello, które znajdują się w profilu magazynu hello. W związku z tym ważne jest podczas modyfikowania hello tooensure szablon, że właściwości prawa hello znajdują się w profilu magazynu hello hello zestawu skali.


## <a name="data-disks"></a>Dyski danych

Zmiany hello powyżej hello skali zestaw używa zarządzanych dysków dla hello systemu operacyjnego na dysku, ale informacje o dyskach danych? tooadd dysków z danymi, Dodaj właściwość "dataDisks" hello "storageProfile" na poziomie takie same jak "osDisk" hello. Hello hello właściwość ma wartość JSON listę obiektów, z których każdy ma właściwości "lun" (która muszą być unikatowe dla każdego dysku danych na maszynie Wirtualnej), "createOption" ("pusta" jest obecnie hello — opcja obsługiwana tylko), a "diskSizeGB" (rozmiar dysku hello w gigabajtach hello; musi być większa niż 0 i mniejsza niż 1024) w hello poniższy przykład: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Jeśli określisz `n` dysków w tej macierzy, pobiera zestawu każdej maszyny Wirtualnej w skali hello `n` dysków z danymi. Należy jednak pamiętać, że te dyski danych są urządzeniach niesformatowanych. Nie są sformatowane. Jest tooattach klienta toohello, paritition i format hello dysków przed ich użyciem. Opcjonalnie można również określono `"managedDisk": { "storageAccountType": "Premium_LRS" }` w każdym toospecify obiektu dysku danych powinien być dysk danych — warstwa premium. Tylko maszyny wirtualne z wielkie lub małe firmy "w hello wirtualna sku można używać dysków premium.

Zobacz toolearn więcej informacji o użyciu dysków z danymi zestawy skalowania [w tym artykule](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Następne kroki
Na przykład szablony Menedżera zasobów za pomocą zestawów skali, wyszukaj termin "vmss" w hello [repozytorium github szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).

Aby uzyskać ogólne informacje, zapoznaj się z hello [strony głównej docelowej dla zestawów skalowania](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

