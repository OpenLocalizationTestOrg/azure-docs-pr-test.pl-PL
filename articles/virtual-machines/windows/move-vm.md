---
title: aaaMove zasobu maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Przenieś maszynę Wirtualną systemu Windows tooanother subskrypcji platformy Azure lub grupy zasobów w modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Przenieś maszynę Wirtualną systemu Windows tooanother subskrypcji platformy Azure lub grupy zasobów
W tym artykule przedstawiono sposób toomove maszyny Wirtualnej systemu Windows, między grupami zasobów lub subskrypcji. Przenoszenie między subskrypcjami mogą być przydatne, jeśli pierwotnie utworzono Maszynę wirtualną w osobistych subskrypcji i teraz toomove on toocontinue subskrypcji firmy tooyour swoją pracę.

> [!IMPORTANT]
>Nie można przenieść dysków zarządzanych w tej chwili. 
>
>Nowych identyfikatorów zasobów są tworzone w ramach przeniesienia hello. Po hello maszyny Wirtualnej został przeniesiony, należy tooupdate narzędzia i skrypty toouse hello nowego zasobu identyfikatorów. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Użyj programu Powershell toomove maszyny Wirtualnej
toomove grupę zasobów tooanother maszyny wirtualnej, należy się również o przeniesieniu wszystkich zasobów zależnych hello toomake. polecenia cmdlet Move-AzureRMResource hello toouse, potrzebna Nazwa zasobu hello i hello typu zasobu. Możesz uzyskać zarówno z polecenia cmdlet hello AzureRMResource Znajdź.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove potrzebujemy toomove wielu zasobów maszyny Wirtualnej. Firma Microsoft wystarczy utworzyć oddzielne zmienne dla każdego zasobu, a następnie na liście. W tym przykładzie obejmuje większość hello podstawowych zasobów dla maszyny Wirtualnej, ale można dodać więcej zgodnie z potrzebami.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

toomove hello zasobów toodifferent subskrypcji, obejmują hello **- DestinationSubscriptionId** parametru. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Konieczne będzie podanie tooconfirm, które mają toomove hello określonych zasobów. Typ **Y** tooconfirm, które mają toomove hello zasobów.

## <a name="next-steps"></a>Następne kroki
Wiele różnych typów zasobów można przenosić między grupami zasobów i subskrypcje. Aby uzyskać więcej informacji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../../resource-group-move-resources.md).    

