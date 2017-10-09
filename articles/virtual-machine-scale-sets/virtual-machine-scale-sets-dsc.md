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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="5fe29-103">Za pomocą zestawów skali maszyny wirtualnej z hello Azure rozszerzenia usługi Konfiguracja DSC</span><span class="sxs-lookup"><span data-stu-id="5fe29-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="5fe29-104">[Zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md) mogą być używane z hello [konfiguracji żądanego stanu Azure (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) rozszerzenia obsługi.</span><span class="sxs-lookup"><span data-stu-id="5fe29-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="5fe29-105">Zestawy skalowania maszyny wirtualnej zapewniają toodeploy sposób zarządzania dużą liczbą maszyn wirtualnych i elastycznie można skalować i zmniejszanie w tooload odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5fe29-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="5fe29-106">DSC jest hello tooconfigure używanych maszyn wirtualnych, zgodnie z ich do trybu online, działają hello produkcji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="5fe29-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="5fe29-107">Różnice między wdrożeniem maszyny tooVirtual i zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5fe29-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5fe29-108">Szablon Hello struktury dla zestawu skalowania maszyny wirtualnej różni się nieznacznie z jednej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5fe29-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="5fe29-109">W szczególności jednej maszyny Wirtualnej wdraża rozszerzenia w węźle "virtualMachines" hello.</span><span class="sxs-lookup"><span data-stu-id="5fe29-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="5fe29-110">Brak wpisu typu "rozszerzenia", w którym DSC jest dodany szablon toohello</span><span class="sxs-lookup"><span data-stu-id="5fe29-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="5fe29-111">Węzeł zestaw skali maszyny wirtualnej ma sekcję "właściwości" z hello "VirtualMachineProfile", "extensionProfile" atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5fe29-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="5fe29-112">DSC zostanie dodany w obszarze "rozszerzenia"</span><span class="sxs-lookup"><span data-stu-id="5fe29-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="5fe29-113">Zachowanie dla zestawu skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5fe29-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="5fe29-114">zachowanie powitania dla zestawu skalowania maszyny wirtualnej jest zachowanie toohello identyczne dla jednej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5fe29-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="5fe29-115">Po utworzeniu nowej maszyny Wirtualnej, jest on automatycznie udostępniane z hello rozszerzenia usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="5fe29-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="5fe29-116">Jeśli nowsza wersja powitalne WMF wymaganego przez rozszerzenie hello ponowny rozruch hello maszyny Wirtualnej przed przełączeniem do trybu online.</span><span class="sxs-lookup"><span data-stu-id="5fe29-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="5fe29-117">Po jest w trybie online, pliki do pobrania .zip konfiguracji hello DSC i udostępnij je na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5fe29-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="5fe29-118">Więcej informacji można znaleźć w [hello Omówienie rozszerzenia DSC Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fe29-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fe29-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fe29-119">Next steps</span></span>
<span data-ttu-id="5fe29-120">Sprawdź hello [szablonu usługi Azure Resource Manager dla rozszerzenia hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fe29-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5fe29-121">Dowiedz się, jak hello [rozszerzenia DSC bezpieczną obsługę poświadczeń](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fe29-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="5fe29-122">Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure hello, zobacz [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fe29-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="5fe29-123">Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="5fe29-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

