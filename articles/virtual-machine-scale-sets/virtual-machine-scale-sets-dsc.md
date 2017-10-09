---
title: "aaaUsing żądanego stanu konfiguracji z zestawy skalowania maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: "Za pomocą zestawów skali maszyny wirtualnej z hello Azure rozszerzenia usługi Konfiguracja DSC"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Za pomocą zestawów skali maszyny wirtualnej z hello Azure rozszerzenia usługi Konfiguracja DSC
[Zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md) mogą być używane z hello [konfiguracji żądanego stanu Azure (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) rozszerzenia obsługi. Zestawy skalowania maszyny wirtualnej zapewniają toodeploy sposób zarządzania dużą liczbą maszyn wirtualnych i elastycznie można skalować i zmniejszanie w tooload odpowiedzi. DSC jest hello tooconfigure używanych maszyn wirtualnych, zgodnie z ich do trybu online, działają hello produkcji oprogramowania.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Różnice między wdrożeniem maszyny tooVirtual i zestawy skalowania maszyny wirtualnej
Szablon Hello struktury dla zestawu skalowania maszyny wirtualnej różni się nieznacznie z jednej maszyny Wirtualnej. W szczególności jednej maszyny Wirtualnej wdraża rozszerzenia w węźle "virtualMachines" hello. Brak wpisu typu "rozszerzenia", w którym DSC jest dodany szablon toohello

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

Węzeł zestaw skali maszyny wirtualnej ma sekcję "właściwości" z hello "VirtualMachineProfile", "extensionProfile" atrybutu. DSC zostanie dodany w obszarze "rozszerzenia"

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Zachowanie dla zestawu skalowania maszyny wirtualnej
zachowanie powitania dla zestawu skalowania maszyny wirtualnej jest zachowanie toohello identyczne dla jednej maszyny Wirtualnej. Po utworzeniu nowej maszyny Wirtualnej, jest on automatycznie udostępniane z hello rozszerzenia usługi Konfiguracja DSC. Jeśli nowsza wersja powitalne WMF wymaganego przez rozszerzenie hello ponowny rozruch hello maszyny Wirtualnej przed przełączeniem do trybu online. Po jest w trybie online, pliki do pobrania .zip konfiguracji hello DSC i udostępnij je na powitania maszyny Wirtualnej. Więcej informacji można znaleźć w [hello Omówienie rozszerzenia DSC Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Następne kroki
Sprawdź hello [szablonu usługi Azure Resource Manager dla rozszerzenia hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Dowiedz się, jak hello [rozszerzenia DSC bezpieczną obsługę poświadczeń](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure hello, zobacz [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

