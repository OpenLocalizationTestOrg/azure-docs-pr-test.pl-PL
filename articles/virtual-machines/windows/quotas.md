---
title: "przydziały vCPU dla platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o vCPU przydziały dla platformy Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: drewm
ms.openlocfilehash: b481299b62d452bc306c1f9c1fa2cdccd49b818e
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="virtual-machine-vcpu-quotas"></a>Przydziały vCPU maszyny wirtualnej

Przydziały vCPU dla maszyn wirtualnych i zestawy skalowania maszyny wirtualnej są rozmieszczone w dwóch warstw dla każdej subskrypcji, w każdym regionie. Pierwsza warstwa jest całkowita regionalnych Vcpu, a druga warstwa jest różnych maszyny Wirtualnej rozmiar rodziny rdzeni takich jak Vcpu standardowe rodziny D. Zawsze, gdy jest nowej maszyny Wirtualnej wdrożone Vcpu nowo wdrożonej maszyny Wirtualnej nie może przekraczać przydziału vCPU dla określonej rodziny rozmiar maszyny Wirtualnej lub przydziału całkowita vCPU regionalnych. W przypadku przekroczenia jednej z tych przydziałów wdrożenia maszyny Wirtualnej nie jest dozwolone. Istnieje również limit przydziału dla ogólnej liczby maszyn wirtualnych w tym regionie. Szczegółowe informacje o każdej z tych przydziałów są widoczne w **użycia + przydziały** sekcji **subskrypcji** strony [portalu Azure](https://portal.azure.com), lub można zbadać wartości przy użyciu Środowiska PowerShell.

 
## <a name="check-usage"></a>Sprawdź użycie

Można użyć [Get-AzureRmVMUsage](/powershell/module/azurerm.compute/get-azurermvmusage) polecenia cmdlet, aby sprawdzić użycie przydziału.

```azurepowershell-interactive
Get-AzureRmVMUsage -Location "East US"
```

Dane wyjściowe będą wyglądać podobnie do poniższego:

```
Name                             Current Value Limit  Unit
----                             ------------- -----  ----
Availability Sets                            0  2000 Count
Total Regional vCPUs                         4   260 Count
Virtual Machines                             4 10000 Count
Virtual Machine Scale Sets                   1  2000 Count
Standard B Family vCPUs                      1    10 Count
Standard DSv2 Family vCPUs                   1   100 Count
Standard Dv2 Family vCPUs                    2   100 Count
Basic A Family vCPUs                         0   100 Count
Standard A0-A7 Family vCPUs                  0   250 Count
Standard A8-A11 Family vCPUs                 0   100 Count
Standard D Family vCPUs                      0   100 Count
Standard G Family vCPUs                      0   100 Count
Standard DS Family vCPUs                     0   100 Count
Standard GS Family vCPUs                     0   100 Count
Standard F Family vCPUs                      0   100 Count
Standard FS Family vCPUs                     0   100 Count
Standard NV Family vCPUs                     0    24 Count
Standard NC Family vCPUs                     0    48 Count
Standard H Family vCPUs                      0     8 Count
Standard Av2 Family vCPUs                    0   100 Count
Standard LS Family vCPUs                     0   100 Count
Standard Dv2 Promo Family vCPUs              0   100 Count
Standard DSv2 Promo Family vCPUs             0   100 Count
Standard MS Family vCPUs                     0     0 Count
Standard Dv3 Family vCPUs                    0   100 Count
Standard DSv3 Family vCPUs                   0   100 Count
Standard Ev3 Family vCPUs                    0   100 Count
Standard ESv3 Family vCPUs                   0   100 Count
Standard FSv2 Family vCPUs                   0   100 Count
Standard ND Family vCPUs                     0     0 Count
Standard NCv2 Family vCPUs                   0     0 Count
Standard NCv3 Family vCPUs                   0     0 Count
Standard LSv2 Family vCPUs                   0     0 Count
Standard Storage Managed Disks               2 10000 Count
Premium Storage Managed Disks                1 10000 Count

```


## <a name="reserved-vm-instances"></a>Wystąpienia zarezerwowane maszyn wirtualnych
Ograniczone do jednego subskrypcji, wystąpień maszyny Wirtualnej zarezerwowana doda aspekt nowe do przydziały vCPU. Te wartości opisano liczbę wystąpień podane rozmiar, który musi być możliwy do wdrożenia w ramach subskrypcji. Funkcje te działają jako element zastępczy w systemie przydziału, aby upewnić się, że ten przydział jest zarezerwowana do upewnij się, że można wdrożyć w ramach subskrypcji są zastrzeżone wystąpień. Na przykład jeśli określonej subskrypcji ma 10 Standard_D1 zastrzeżone wystąpień ograniczenie użycia dla wystąpień zastrzeżone Standard_D1 będzie 10. Spowoduje to Azure upewnić się, że zawsze są dostępne w całkowita regionalnych Vcpu przydział do zastosowania w przypadku wystąpienia Standard_D1 Vcpu co najmniej 10 i są dostępne w standardowe rodziny D vCPU przydział do zastosowania w przypadku wystąpienia Standard_D1 Vcpu co najmniej 10.

Jeśli zwiększenia limitu przydziału jest wymagana, aby zakupić pojedynczego RI subskrypcji, możesz [zażądać zwiększenia limitu przydziału](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) w ramach subskrypcji.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących rozliczeń i przydziały, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=/azure/billing/TOC.json).