---
title: "aaaMove maszyna wirtualna (klasyczna) lub usługi w chmurze rola wystąpienia tooa różnych podsieci - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomove maszyn wirtualnych (klasyczne) i rola usługi w chmurze wystąpienia tooa innej podsieci przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Przenoszenie maszyny Wirtualnej (klasyczne) lub usługi w chmurze rola wystąpienia tooa innej podsieci przy użyciu programu PowerShell
Możesz użyć programu PowerShell toomove maszyn wirtualnych (klasyczne) z jedną podsiecią tooanother w hello tej samej sieci wirtualnej (VNet). Wystąpienia roli można przenieść edytowania pliku CSCFG hello, zamiast przy użyciu programu PowerShell.

> [!NOTE]
> W tym artykule opisano, jak wdrożyć maszyn wirtualnych toomove za pośrednictwem hello klasycznego modelu wdrażania tylko.
> 
> 

Dlaczego przenieść maszyny wirtualne podsieci tooanother? Podsieci migracji jest przydatne, gdy podsieć starsze hello jest zbyt mała i nie można rozwijać powodu tooexisting działających maszyn wirtualnych w tej podsieci. W takim przypadku można tworzyć nowe, większy podsieci i migracji maszyn wirtualnych hello toohello nową podsieć, a następnie po zakończeniu migracji, można usunąć starego podsieci pusty hello.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Jak toomove tooanother podsieć maszyny Wirtualnej
toomove Maszynę wirtualną, uruchom polecenie cmdlet Set-AzureSubnet PowerShell hello, przy użyciu przykład Witaj poniżej jako szablon. W poniższym przykładzie hello, możemy przechodzenia z jego obecny podsieci TestVM tooSubnet-2. Należy się tooreflect przykład hello tooedit środowiska. Należy pamiętać, że po uruchomieniu polecenia cmdlet Update-AzureVM hello w ramach procedury będzie uruchamiany ponownie maszyny Wirtualnej w ramach procesu aktualizacji hello.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Jeśli określono wewnętrzny statycznego prywatnego adresu IP dla maszyny Wirtualnej, będziesz mieć tooclear ustawienie przed przejściem hello wirtualna tooa nowej podsieci. W takim przypadku należy użyć następujących hello:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove podsieci tooanother wystąpienia roli
toomove wystąpienia roli, Edytuj plik CSCFG hello. W poniższym przykładzie hello, możemy przechodzenia w sieci wirtualnej "Role0" *VNETName* z jego podsieci występuje zbyt*2 podsieci*. Wystąpienia roli hello została już wdrożona, tylko będzie zmienić nazwę podsieci hello = 2 podsieci. Należy się tooreflect przykład hello tooedit środowiska.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
