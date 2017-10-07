---
title: "aaaUsing zarządzane dyski w szablonach usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje, w jaki sposób toouse Zarządzanie misks w szablonach usługi Azure Resource Manager"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: ea83f4ed11acfd8f642dbc8331fa8cf077ef577c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Za pomocą Managed dysków w szablonach usługi Azure Resource Manager

Ten dokument przeprowadzi Cię przez hello różnice między dyskami zarządzane i niezarządzane, korzystając z maszyn wirtualnych tooprovision szablonów usługi Azure Resource Manager. Pomoże to tooupdate istniejących szablonów, które korzystają z niezarządzanego dysków toomanaged dysków. Odwołania, jest używany hello [101 maszyny wirtualnej — prosty — windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) szablonu jako przewodnika. Widać hello szablonu przy użyciu zarówno [dyskach zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) i przy użyciu poprzedniej wersji [niezarządzanych dysków](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) Jeśli chcesz toodirectly porównania.

## <a name="unmanaged-disks-template-formatting"></a>Niezarządzane formatowania szablonu dysków

toobegin, możemy też zwrócić uwagę na sposób niezarządzany dyski są wdrażane. Podczas tworzenia dysków niezarządzane, należy się pliki VHD hello toohold konta magazynu. Możesz utworzyć nowe konto magazynu lub użyć już istniejącego. W tym artykule opisano, jak toocreate nowe konto magazynu. tooaccomplish, to należy zasób konta magazynu w bloku zasobów hello, jak pokazano poniżej.

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

W ramach hello obiektu maszyny wirtualnej potrzebujemy zależności hello tooensure konta magazynu, utworzony przed hello maszyny wirtualnej. W ramach hello `storageProfile` sekcji, a następnie określ hello pełny identyfikator URI hello lokalizacja wirtualnego dysku twardego, który odwołuje się do konta magazynu hello i jest wymagany dla dysku hello systemu operacyjnego i dysków z danymi. 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a>Zarządzane formatowania szablonu dysków

Zarządzane dysków Azure hello dysku staje się zasobem najwyższego poziomu i nie wymaga już utworzone przez użytkownika hello toobe konta magazynu. Dyski zarządzanych najpierw były widoczne w hello `2016-04-30-preview` wersja interfejsu API są dostępne w wszystkie kolejne wersje interfejsu API i są teraz hello domyślny typ dysku. Witaj sekcje przeprowadzenie hello domyślne ustawienia i szczegółów jak toofurther dostosować dysków.

> [!NOTE]
> Zalecane jest toouse interfejsu API w wersji nowszej niż `2016-04-30-preview` jako wystąpiły zmiany podziału między `2016-04-30-preview` i `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Domyślne ustawienia dysków zarządzanych

toocreate maszynę Wirtualną za pomocą dysków zarządzanych, użytkownik nie jest już konieczne zasobów konta magazynu hello toocreate i można zaktualizować zasobu maszyny wirtualnej w następujący sposób. W szczególności należy pamiętać, że hello `apiVersion` odzwierciedla `2017-03-30` i hello `osDisk` i `dataDisks` nie można znaleźć tooa określonego identyfikatora URI dla hello wirtualnego dysku twardego. Wdrażając bez określenia dodatkowych właściwości użyje dysku hello [magazynu Standard-LRS](storage-redundancy.md). Jeśli nazwa nie zostanie określona, zajmuje hello format `<VMName>_OsDisk_1_<randomstring>` dla dysku systemu operacyjnego hello i `<VMName>_disk<#>_<randomstring>` dla każdego dysku danych. Domyślnie szyfrowania dysków Azure jest wyłączony; buforowanie jest odczytu/zapisu dla dysku systemu operacyjnego hello i brak w przypadku dysków z danymi. W poniższym przykładzie hello mogą pojawić się, że istnieje zależność konta magazynu, mimo że to jest tylko do przechowywania diagnostyki i nie jest wymagany dla magazynu danych na dysku.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a>Przy użyciu zasobów dysków zarządzanych w najwyższego poziomu

Jako alternatywne toospecifying hello konfigurację dysku w hello obiektu maszyny wirtualnej można tworzyć zasób dysku najwyższego poziomu i dołącz je jako część hello tworzenie maszyny wirtualnej. Na przykład możemy utworzyć zasób dysku następujący toouse jako dysk danych.

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

W ramach hello obiektu maszyny Wirtualnej możemy odwołania tego dysku toobe obiektu, który jest dołączony. Określ identyfikator ID zasobu hello z hello zarządzane dysku utworzone hello `managedDisk` właściwość umożliwia dołączanie hello hello dysku jako hello zostanie utworzona maszyna wirtualna. Należy pamiętać, że hello `apiVersion` dla hello zasobu maszyny Wirtualnej jest ustawiony za`2017-03-30`. Należy również zauważyć, że utworzyliśmy zależności na powitania tooensure zasobu dysku, którym pomyślnie zostały utworzone przed utworzeniem maszyny Wirtualnej. 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Tworzenie zestawów dostępności zarządzanych maszyn wirtualnych za pomocą dysków zarządzanych

toocreate zarządzane dostępności zestawów z maszyn wirtualnych za pomocą dysków zarządzanych, Dodaj hello `sku` obiektu toohello dostępności ustawić zasobów i ustawić hello `name` właściwości zbyt`Aligned`. To zapewnia, że dyski powitania dla każdej maszyny Wirtualnej są wystarczająco odizolowane od siebie nawzajem tooavoid pojedynczych punktów awarii. Należy również zauważyć, że hello `apiVersion` dla zestawu dostępności hello zasobów ustawiono zbyt`2017-03-30`.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a>Dodatkowe scenariusze i dostosowania

toofind pełne informacje dotyczące hello specyfikacji interfejsu API REST, zapoznaj się z tematem hello [tworzenie dysków zarządzanych w dokumentacji interfejsu API REST](/rest/api/manageddisks/disks/disks-create-or-update). Dostępne są dodatkowe scenariusze, a także domyślne i dopuszczalne wartości, które mogą być przesłane toohello API za pomocą szablonu wdrożenia. 

## <a name="next-steps"></a>Następne kroki

* Pełna szablonów, które zarządzanych dysków można znaleźć hello następującego łącza repozytorium Szybki Start Azure.
    * [Maszyny Wirtualnej systemu Windows z dyskiem zarządzanym](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Maszyny Wirtualnej systemu Linux z dyskiem zarządzanym](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Pełną listę szablonów zarządzanych dysku](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Odwiedź hello [omówienie dysków zarządzanych Azure](storage-managed-disks-overview.md) dokumentu toolearn więcej informacji o dyskach zarządzanych.
* Przejrzyj dokumentację referencyjną szablonu hello zasobów maszyny wirtualnej, przechodząc na stronę hello [odwołania do szablonu Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) dokumentu.
* Przejrzyj dokumentację referencyjną szablonu hello zasoby dyskowe, przechodząc na stronę hello [odwołania do szablonu Microsoft.Compute/disks](/templates/microsoft.compute/disks) dokumentu.
 
