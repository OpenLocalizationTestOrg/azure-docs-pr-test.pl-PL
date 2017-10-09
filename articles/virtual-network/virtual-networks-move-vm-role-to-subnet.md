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
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="5affc-103">Przenoszenie maszyny Wirtualnej (klasyczne) lub usługi w chmurze rola wystąpienia tooa innej podsieci przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5affc-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="5affc-104">Możesz użyć programu PowerShell toomove maszyn wirtualnych (klasyczne) z jedną podsiecią tooanother w hello tej samej sieci wirtualnej (VNet).</span><span class="sxs-lookup"><span data-stu-id="5affc-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="5affc-105">Wystąpienia roli można przenieść edytowania pliku CSCFG hello, zamiast przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5affc-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="5affc-106">W tym artykule opisano, jak wdrożyć maszyn wirtualnych toomove za pośrednictwem hello klasycznego modelu wdrażania tylko.</span><span class="sxs-lookup"><span data-stu-id="5affc-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="5affc-107">Dlaczego przenieść maszyny wirtualne podsieci tooanother?</span><span class="sxs-lookup"><span data-stu-id="5affc-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="5affc-108">Podsieci migracji jest przydatne, gdy podsieć starsze hello jest zbyt mała i nie można rozwijać powodu tooexisting działających maszyn wirtualnych w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="5affc-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="5affc-109">W takim przypadku można tworzyć nowe, większy podsieci i migracji maszyn wirtualnych hello toohello nową podsieć, a następnie po zakończeniu migracji, można usunąć starego podsieci pusty hello.</span><span class="sxs-lookup"><span data-stu-id="5affc-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="5affc-110">Jak toomove tooanother podsieć maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5affc-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="5affc-111">toomove Maszynę wirtualną, uruchom polecenie cmdlet Set-AzureSubnet PowerShell hello, przy użyciu przykład Witaj poniżej jako szablon.</span><span class="sxs-lookup"><span data-stu-id="5affc-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="5affc-112">W poniższym przykładzie hello, możemy przechodzenia z jego obecny podsieci TestVM tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="5affc-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="5affc-113">Należy się tooreflect przykład hello tooedit środowiska.</span><span class="sxs-lookup"><span data-stu-id="5affc-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="5affc-114">Należy pamiętać, że po uruchomieniu polecenia cmdlet Update-AzureVM hello w ramach procedury będzie uruchamiany ponownie maszyny Wirtualnej w ramach procesu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="5affc-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="5affc-115">Jeśli określono wewnętrzny statycznego prywatnego adresu IP dla maszyny Wirtualnej, będziesz mieć tooclear ustawienie przed przejściem hello wirtualna tooa nowej podsieci.</span><span class="sxs-lookup"><span data-stu-id="5affc-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="5affc-116">W takim przypadku należy użyć następujących hello:</span><span class="sxs-lookup"><span data-stu-id="5affc-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="5affc-117">toomove podsieci tooanother wystąpienia roli</span><span class="sxs-lookup"><span data-stu-id="5affc-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="5affc-118">toomove wystąpienia roli, Edytuj plik CSCFG hello.</span><span class="sxs-lookup"><span data-stu-id="5affc-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="5affc-119">W poniższym przykładzie hello, możemy przechodzenia w sieci wirtualnej "Role0" *VNETName* z jego podsieci występuje zbyt*2 podsieci*.</span><span class="sxs-lookup"><span data-stu-id="5affc-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="5affc-120">Wystąpienia roli hello została już wdrożona, tylko będzie zmienić nazwę podsieci hello = 2 podsieci.</span><span class="sxs-lookup"><span data-stu-id="5affc-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="5affc-121">Należy się tooreflect przykład hello tooedit środowiska.</span><span class="sxs-lookup"><span data-stu-id="5affc-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
