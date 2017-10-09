---
title: "Maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi przy użyciu programu PowerShell aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i konfigurowanie maszyn wirtualnych z wieloma kartami sieciowymi przy użyciu programu PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="8a6ae-103">Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi</span><span class="sxs-lookup"><span data-stu-id="8a6ae-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="8a6ae-104">Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele sieci tooeach interfejsów (NIC) z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="8a6ae-105">Wiele kart sieciowych są wymagane w przypadku wielu sieci wirtualnych urządzeń, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="8a6ae-106">Wiele kart sieciowych zapewniają również izolacji ruchu między kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Obsługa wielu kart interfejsu Sieciowego dla maszyny Wirtualnej](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="8a6ae-108">rysunek pokazuje Hello maszyny Wirtualnej z trzema kartami sieciowymi, każdy jest połączony tooa innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a6ae-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8a6ae-110">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8a6ae-111">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="8a6ae-112">VIP połączonych z Internetem (wdrożenia klasyczne) jest obsługiwany tylko na powitania "domyślne" karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="8a6ae-113">Istnieje tylko jeden adres IP toohello VIP o hello domyślną kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="8a6ae-114">W tym czasie wystąpienia poziomu publicznego adresu IP (LPIP) adresy (wdrożenia klasyczne) nie są obsługiwane dla wielu maszyn wirtualnych kart Sieciowych.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="8a6ae-115">Witaj kolejność kart sieciowych hello z wewnątrz hello maszyny Wirtualnej będzie losowe i można również zmienić między aktualizacjami infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="8a6ae-116">Jednak hello adresów IP i hello odpowiedni adres ethernet MAC pozostanie adresy hello takie same.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="8a6ae-117">Załóżmy na przykład **Eth1** ma adres IP 10.1.0.100 i adres MAC 00-0D-3A-B0-39-0D; po aktualizacji infrastruktury platformy Azure i uruchom ponownie komputer, którego można można zmienić za**Eth2**, ale hello adresów IP i MAC parowanie zostanie pozostają takie same hello.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="8a6ae-118">Jeśli ponowne uruchomienie jest inicjowane przez klienta, pozostaną hello kolejność kart hello takie same.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="8a6ae-119">Witaj adresów dla każdej karty Sieciowej na każdej maszynie Wirtualnej musi znajdować się w podsieci, wiele kart sieciowych w ramach jednej maszyny Wirtualnej każdego można przypisać adresy znajdujące się w hello tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="8a6ae-120">Hello rozmiar maszyny Wirtualnej określa hello liczbę kart Sieciowych, który można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="8a6ae-121">Odwołanie hello [systemu Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toodetermine artykuły rozmiary maszyny Wirtualnej, jak wiele kart Sieciowych każdego rozmiaru maszyny Wirtualnej obsługuje.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="8a6ae-122">Grupy zabezpieczeń sieci (NSG)</span><span class="sxs-lookup"><span data-stu-id="8a6ae-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="8a6ae-123">W ramach wdrożenia usługi Resource Manager dowolnej karty interfejsu Sieciowego na maszynie Wirtualnej może być skojarzony z sieciowej grupy zabezpieczeń (NSG), w tym wszystkie karty sieciowe na maszynie Wirtualnej, który ma wiele kart sieciowych włączone.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="8a6ae-124">Jeśli karta sieciowa zostanie przypisany adres znajdujący się w podsieci, w którym jest skojarzona z grupy NSG podsieci hello, następnie hello reguły w NSG podsieci hello stosuje się również toothat karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="8a6ae-125">Dodawanie podsieci tooassociating z grup NSG można także skojarzyć karty Sieciowej z grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="8a6ae-126">Jeśli podsieć jest skojarzony z grupy NSG, a karta sieciowa w tej podsieci indywidualnie powiązanego z grupy NSG, hello skojarzone reguły NSG są stosowane w **przepływ kolejności** zgodnie z toohello kierunek ruchu hello przekazywany do lub z Witaj karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="8a6ae-127">**Ruch przychodzący** których obiektem docelowym jest hello karty Sieciowej w pytanie najpierw przechodzi przez hello podsieci, wyzwolenie reguły NSG podsieci hello, przed przekazaniem do hello karty Sieciowej, a następnie wyzwolenie reguły NSG hello karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="8a6ae-128">**Ruch wychodzący** źródłem jest hello karty Sieciowej w przepływa pierwszy na wyjściu z hello karty Sieciowej, wyzwolenie reguły NSG hello karty Sieciowej, przed przechodzącej przez hello podsieci, a następnie wyzwolenie reguły NSG hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="8a6ae-129">Dowiedz się więcej o [grup zabezpieczeń sieci](virtual-networks-nsg.md) i jak są one stosowane na podstawie toosubnets skojarzenia, maszyn wirtualnych i karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="8a6ae-130">Jak tooConfigure wielu kart interfejsu Sieciowego maszyny Wirtualnej w ramach wdrożenia klasycznego</span><span class="sxs-lookup"><span data-stu-id="8a6ae-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="8a6ae-131">Poniższe instrukcje Hello umożliwia tworzenie wielu kart Sieciowych maszyny Wirtualnej zawierający 3 kart sieciowych: domyślna karta sieciowa a dwie dodatkowe karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="8a6ae-132">kroki konfiguracji Hello spowoduje utworzenie maszyny Wirtualnej, który zostanie skonfigurowany zgodnie z poniższym fragment pliku konfiguracji usługi toohello:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="8a6ae-133">Należy hello następujące wymagania wstępne, przed podjęciem próby poleceń programu PowerShell hello toorun w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="8a6ae-134">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-134">An Azure subscription.</span></span>
* <span data-ttu-id="8a6ae-135">Skonfigurowanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-135">A configured virtual network.</span></span> <span data-ttu-id="8a6ae-136">Zobacz [omówienie sieci wirtualnych](virtual-networks-overview.md) uzyskać więcej informacji o sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="8a6ae-137">najnowszą wersję programu Azure PowerShell Hello pobrane i zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="8a6ae-138">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="8a6ae-139">toocreate Maszynę wirtualną z wieloma kartami sieciowymi, pełną hello, wykonaj następujące kroki, wprowadzając każde polecenie w ramach jednej sesji programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="8a6ae-140">Wybierz obraz maszyny Wirtualnej z galerii obrazu maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="8a6ae-141">Należy pamiętać, że obrazy często zmieniana i są dostępne w poszczególnych regionach.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="8a6ae-142">Witaj obrazu określonego w poniższym przykładzie hello może zmienić lub może nie być w danym regionie, dlatego należy toospecify hello obrazu należy.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="8a6ae-143">Tworzenie konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="8a6ae-144">Utwórz identyfikator logowania administratora domyślnego hello.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="8a6ae-145">Dodawanie dodatkowych konfiguracji maszyny Wirtualnej toohello kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="8a6ae-146">Określ hello podsieć lub adres IP dla hello domyślną kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="8a6ae-147">Utwórz hello maszyny Wirtualnej w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="8a6ae-148">Witaj sieci wirtualnej, określone w tym miejscu musi już istnieć (jak wspomniano w hello wymagania wstępne).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="8a6ae-149">w poniższym przykładzie Hello określa sieć wirtualną o nazwie **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="8a6ae-150">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="8a6ae-150">Limitations</span></span>
<span data-ttu-id="8a6ae-151">Hello następujące ograniczenia mają zastosowanie w przypadku korzystania z wielu kart sieciowych:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="8a6ae-152">Maszyny wirtualne z wieloma kartami sieciowymi muszą być tworzone w sieci wirtualnej platformy Azure (sieci wirtualne).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="8a6ae-153">Nie można skonfigurować sieci wirtualnej nie maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="8a6ae-154">Wszystkie maszyny wirtualne w dostępności ustawiony toouse potrzeby wiele kart sieciowych lub jednej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="8a6ae-155">Nie może być wiele maszyn wirtualnych kart Sieciowych i jednej karty Sieciowej maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="8a6ae-156">Te same zasady mają zastosowanie dla maszyn wirtualnych w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="8a6ae-157">Dla wielu kart interfejsu Sieciowego maszyn wirtualnych, nie są one wymagane toohave hello samą liczbę kart sieciowych, jak długo każdy z nich ma co najmniej dwóch.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="8a6ae-158">Nie można skonfigurować maszynę Wirtualną z jednej karty Sieciowej z wielu kart sieciowych (i na odwrót) po wdrożeniu, bez usunięcia i ponownego utworzenia go.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="8a6ae-159">Dodatkowej podsieci tooother dostęp do kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="8a6ae-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="8a6ae-160">Domyślnie dodatkowej karty sieciowe nie zostanie skonfigurowany dla bramy domyślnej powodu toowhich hello ruchu na powitania dodatkowej karty sieciowe będą ograniczone toobe w hello tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="8a6ae-161">Jeśli użytkownicy hello tooenable dodatkowej tootalk kart sieciowych spoza własnej podsieci, muszą tooadd wpis w hello tabeli tooconfigure hello bramy routingu jako opisanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6ae-162">Maszyny wirtualne utworzone przed lipca 2015 może mieć brama domyślna jest skonfigurowana dla wszystkich kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="8a6ae-163">Hello brama domyślna dla dodatkowej kart sieciowych nie zostaną usunięte, dopóki te maszyny wirtualne są ponownie uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="8a6ae-164">W systemach operacyjnych, korzystających z hello słabe routingu modelu hosta, takich jak Linux Jeśli hello ruchu przychodzące i wychodzące używane różne karty sieciowe mogą być dzielone łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="8a6ae-165">Konfigurowanie maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8a6ae-165">Configure Windows VMs</span></span>
<span data-ttu-id="8a6ae-166">Załóżmy, że ma maszyny Wirtualnej systemu Windows z dwiema kartami sieciowymi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="8a6ae-167">Podstawowy adres IP karty Sieciowej: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="8a6ae-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="8a6ae-168">Pomocniczego adresu IP karty Sieciowej: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="8a6ae-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="8a6ae-169">Witaj tabelę tras IPv4 dla tej maszyny Wirtualnej będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-169">hello IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="8a6ae-170">Należy zauważyć, że hello trasa domyślna (0.0.0.0) jest tylko dostępne toohello podstawowej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="8a6ae-171">Nie będą mogli tooaccess zasobów spoza hello podsieć hello dodatkowej karty Sieciowej, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="8a6ae-172">tooadd trasy domyślne na hello dodatkowej karty Sieciowej, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="8a6ae-173">W wierszu polecenia Uruchom polecenie hello poniżej numer indeksu hello tooidentify hello dodatkowej karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="8a6ae-174">Zwróć uwagę, hello drugi wpis w tabeli hello z indeksem 27 (w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="8a6ae-175">W wierszu polecenia hello Uruchom hello **dodać trasy** polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="8a6ae-176">W tym przykładzie są określanie 192.168.2.1 jako brama domyślna hello hello dodatkowej karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="8a6ae-177">łączność tootest toohello wiersza polecenia i spróbuj tooping z innej podsieci hello dodatkowej karty Sieciowej jako pokazano int eh przykładzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="8a6ae-178">Można również sprawdzić, że Twoje hello toocheck tabeli tras nowo dodany trasy, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="8a6ae-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="8a6ae-179">Konfigurowanie maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="8a6ae-179">Configure Linux VMs</span></span>
<span data-ttu-id="8a6ae-180">Dla maszyn wirtualnych systemu Linux, ponieważ hello domyślne zachowanie używa słabe hosta routingu, zaleca się tym hello dodatkowej karty sieciowe są ograniczone tootraffic przepływów tylko w obrębie hello tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="8a6ae-181">Jednak w przypadku niektórych scenariuszy żądanie łączność poza hello podsieci, użytkowników, należy włączyć tooensure routingu opartego na zasadach, które hello wejściowych i używa ruch wychodzący hello tej samej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8a6ae-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a6ae-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a6ae-182">Next steps</span></span>
* <span data-ttu-id="8a6ae-183">Wdrażanie [MultiNIC maszyn wirtualnych, w przypadku aplikacji warstwy 2 w ramach wdrożenia usługi Resource Manager](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="8a6ae-184">Wdrażanie [MultiNIC maszyn wirtualnych, w przypadku aplikacji warstwy 2 w ramach wdrożenia klasycznego](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8a6ae-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

