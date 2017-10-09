---
title: "aaaMove Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przenoszenie maszyny Wirtualnej systemu Linux tooanother subskrypcji platformy Azure lub grupy zasobów w modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Przenieś grupę zasobów lub subskrypcji tooanother maszyny Wirtualnej systemu Linux
W tym artykule przedstawiono sposób toomove maszyny Wirtualnej systemu Linux, między grupami zasobów lub subskrypcji. Przenoszenie maszyny Wirtualnej między subskrypcjami mogą być przydatne, jeśli utworzono Maszynę wirtualną w osobistych subskrypcji i teraz toomove go subskrypcji tooyour firmy.

> [!IMPORTANT]
>Nie można przenieść dysków zarządzanych w tej chwili. 
>
>Nowych identyfikatorów zasobów są tworzone w ramach przeniesienia hello. Po hello maszyny Wirtualnej został przeniesiony, należy tooupdate narzędzia i skrypty toouse hello nowego zasobu identyfikatorów. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Użyj hello Azure CLI toomove maszyny Wirtualnej
toosuccessfully przenieść Maszynę wirtualną, należy toomove hello maszyny Wirtualnej i wszystkie dodatkowe zasoby. Użyj hello **Pokaż grupy azure** polecenia toolist wszystkie zasoby hello w grupie zasobów i ich identyfikatorów. Pomaga toopipe hello dane wyjściowe tego polecenia tooa pliku, więc można skopiować i wkleić hello identyfikatorów na nowsze poleceń.

    azure group show <resourceGroupName>

toomove Maszynę wirtualną i jego grupa zasobów tooanother zasoby, używać hello **przenoszenia zasobów platformy azure** polecenia interfejsu wiersza polecenia. Witaj poniższy przykład pokazuje, jak toomove Maszynę wirtualną i zasoby najczęściej hello wymaga. Używamy hello **-i** parametru i przekazać na liście rozdzielanej przecinkami (bez spacji) identyfikatorów dla hello toomove zasobów.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Jeśli chcesz, aby toomove hello maszyny Wirtualnej i jej zasobów tooa innej subskrypcji, dodawać hello **— identyfikator subskrypcji docelowej &#60; destinationSubscriptionID &#62;** parametru toospecify hello docelowej subskrypcji.

Jeśli pracujesz z hello wiersza polecenia na komputerze z systemem Windows, należy tooadd  **$**  przed nazwy zmiennych hello przy deklarowaniu je. To nie jest wymagana w systemie Linux.

Pojawi się monit, które mają toomove hello tooconfirm określony zasób. Typ **Y** tooconfirm, które mają toomove hello zasobów.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Następne kroki
Wiele różnych typów zasobów można przenosić między grupami zasobów i subskrypcje. Aby uzyskać więcej informacji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../../resource-group-move-resources.md).    

