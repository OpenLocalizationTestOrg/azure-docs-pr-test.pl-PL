---
title: "Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i skonfigurować maszyny wirtualne z wieloma kartami sieciowymi przy użyciu programu PowerShell."
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
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="52b0e-103">Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi</span><span class="sxs-lookup"><span data-stu-id="52b0e-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="52b0e-104">Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele interfejsów sieciowych (NIC) do wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="52b0e-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="52b0e-105">Wiele kart sieciowych są wymagane w przypadku wielu sieci wirtualnych urządzeń, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.</span><span class="sxs-lookup"><span data-stu-id="52b0e-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="52b0e-106">Wiele kart sieciowych zapewniają również izolacji ruchu między kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="52b0e-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Obsługa wielu kart interfejsu Sieciowego dla maszyny Wirtualnej](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="52b0e-108">Na rysunku przedstawiono Maszynę wirtualną z trzema kartami sieciowymi, każdy jest połączony z innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="52b0e-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52b0e-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="52b0e-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="52b0e-110">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="52b0e-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="52b0e-111">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="52b0e-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="52b0e-112">VIP połączonych z Internetem (wdrożenia klasyczne) jest obsługiwane tylko dla karty sieciowej "domyślny".</span><span class="sxs-lookup"><span data-stu-id="52b0e-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="52b0e-113">Istnieje tylko jeden adresów VIP na adres IP domyślnej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="52b0e-114">W tym czasie wystąpienia poziomu publicznego adresu IP (LPIP) adresy (wdrożenia klasyczne) nie są obsługiwane dla wielu maszyn wirtualnych kart Sieciowych.</span><span class="sxs-lookup"><span data-stu-id="52b0e-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="52b0e-115">Kolejność kart sieciowych wewnątrz maszyny wirtualnej będzie losowa i może również ulec zmianie między aktualizacjami infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="52b0e-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="52b0e-116">Jednak adresów IP i odpowiednie ethernet MAC adresy będą pozostają takie same.</span><span class="sxs-lookup"><span data-stu-id="52b0e-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="52b0e-117">Załóżmy na przykład **Eth1** ma adres IP 10.1.0.100 i adres MAC 00-0D-3A-B0-39-0D; po aktualizacji infrastruktury platformy Azure i ponowne uruchomienie komputera, można zmienić na **Eth2**, ale adresów IP i MAC parowanie jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="52b0e-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="52b0e-118">Jeśli ponowne uruchomienie jest inicjowane przez klienta, kolejność kart interfejsu Sieciowego jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="52b0e-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="52b0e-119">Adres dla każdej karty Sieciowej na każdej maszynie Wirtualnej musi znajdować się w podsieci, wiele kart sieciowych na jednej maszynie Wirtualnej każdego można przypisać adresy znajdujące się w tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="52b0e-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="52b0e-120">Rozmiar maszyny Wirtualnej określa liczbę kart Sieciowych, który można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="52b0e-121">Odwołanie [systemu Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykuły, aby określić, jak wiele kart Sieciowych każdego rozmiaru maszyny Wirtualnej obsługuje rozmiary maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="52b0e-122">Grupy zabezpieczeń sieci (NSG)</span><span class="sxs-lookup"><span data-stu-id="52b0e-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="52b0e-123">W ramach wdrożenia usługi Resource Manager dowolnej karty interfejsu Sieciowego na maszynie Wirtualnej może być skojarzony z sieciowej grupy zabezpieczeń (NSG), w tym wszystkie karty sieciowe na maszynie Wirtualnej, który ma wiele kart sieciowych włączone.</span><span class="sxs-lookup"><span data-stu-id="52b0e-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="52b0e-124">Jeśli karta sieciowa zostanie przypisany adres znajdujący się w podsieci, w którym jest skojarzona z grupy NSG podsieci, następnie zasady w tej podsieci NSG również zastosowanie do tej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="52b0e-125">Oprócz kojarzenia podsieci z grup NSG, można również skojarzyć karty Sieciowej z grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="52b0e-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="52b0e-126">Jeśli podsieć jest skojarzony z grupy NSG, a karta sieciowa w tej podsieci indywidualnie powiązanego z grupy NSG, skojarzone reguły NSG są stosowane w **przepływ kolejności** zgodnie z kierunek ruchu przekazywany do lub z karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="52b0e-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="52b0e-127">**Ruch przychodzący** których obiektem docelowym jest karta sieciowa w pytanie najpierw przechodzi przez podsieci, wyzwolenie reguły NSG podsieci, przed przekazaniem do karty Sieciowej, a następnie wyzwolenie reguły NSG karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="52b0e-128">**Ruch wychodzący** źródłem jest zagrożona kart przepływa pierwszy na wyjściu z karty Sieciowej, wyzwolenie reguły NSG karty Sieciowej, przed przechodzącej przez podsieci, a następnie wyzwolenie reguły NSG podsieci.</span><span class="sxs-lookup"><span data-stu-id="52b0e-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="52b0e-129">Dowiedz się więcej o [grup zabezpieczeń sieci](virtual-networks-nsg.md) i sposób stosowania oparte na skojarzenia z podsieci, maszyn wirtualnych i karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="52b0e-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="52b0e-130">Konfigurowanie wielu kart Sieciowych maszyny Wirtualnej w ramach wdrożenia klasycznego</span><span class="sxs-lookup"><span data-stu-id="52b0e-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="52b0e-131">Poniższe instrukcje umożliwia tworzenie wielu kart Sieciowych maszyny Wirtualnej zawierający 3 kart sieciowych: domyślna karta sieciowa a dwie dodatkowe karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="52b0e-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="52b0e-132">Kroki konfiguracji spowoduje utworzenie maszyny Wirtualnej, który zostanie skonfigurowany zgodnie z poniższym fragment pliku konfiguracji usługi:</span><span class="sxs-lookup"><span data-stu-id="52b0e-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

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
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="52b0e-133">Przed próbą uruchomienia poleceń środowiska PowerShell w tym przykładzie należy się następujące wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="52b0e-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="52b0e-134">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="52b0e-134">An Azure subscription.</span></span>
* <span data-ttu-id="52b0e-135">Skonfigurowanej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-135">A configured virtual network.</span></span> <span data-ttu-id="52b0e-136">Zobacz [omówienie sieci wirtualnych](virtual-networks-overview.md) uzyskać więcej informacji o sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="52b0e-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="52b0e-137">Najnowszą wersję programu Azure PowerShell pobrane i zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52b0e-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="52b0e-138">Zobacz artykuł [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52b0e-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="52b0e-139">Aby utworzyć Maszynę wirtualną z wieloma kartami sieciowymi, wykonaj następujące kroki, wprowadzając każde polecenie w ramach jednej sesji programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="52b0e-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="52b0e-140">Wybierz obraz maszyny Wirtualnej z galerii obrazu maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="52b0e-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="52b0e-141">Należy pamiętać, że obrazy często zmieniana i są dostępne w poszczególnych regionach.</span><span class="sxs-lookup"><span data-stu-id="52b0e-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="52b0e-142">Obraz określony w poniższym przykładzie może zmienić lub może nie może być w danym regionie, dlatego należy określić obraz, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="52b0e-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="52b0e-143">Tworzenie konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="52b0e-144">Utwórz identyfikator logowania administratora domyślnego.</span><span class="sxs-lookup"><span data-stu-id="52b0e-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="52b0e-145">Dodawanie dodatkowych kart sieciowych do konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="52b0e-146">Podaj podsieć lub adres IP dla domyślnej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="52b0e-147">Utwórz maszynę Wirtualną w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="52b0e-148">Sieć wirtualna określone w tym miejscu musi już istnieć (określone w wymaganiach wstępnych).</span><span class="sxs-lookup"><span data-stu-id="52b0e-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="52b0e-149">W poniższym przykładzie określa sieć wirtualną o nazwie **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="52b0e-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="52b0e-150">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="52b0e-150">Limitations</span></span>
<span data-ttu-id="52b0e-151">Następujące ograniczenia mają zastosowanie w przypadku korzystania z wielu kart sieciowych:</span><span class="sxs-lookup"><span data-stu-id="52b0e-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="52b0e-152">Maszyny wirtualne z wieloma kartami sieciowymi muszą być tworzone w sieci wirtualnej platformy Azure (sieci wirtualne).</span><span class="sxs-lookup"><span data-stu-id="52b0e-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="52b0e-153">Nie można skonfigurować sieci wirtualnej nie maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="52b0e-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="52b0e-154">Wszystkie maszyny wirtualne w zestawie dostępności muszą używać wielu kart sieciowych lub jednej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="52b0e-155">Nie może być wiele maszyn wirtualnych kart Sieciowych i jednej karty Sieciowej maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="52b0e-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="52b0e-156">Te same zasady mają zastosowanie dla maszyn wirtualnych w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="52b0e-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="52b0e-157">Dla wielu kart interfejsu Sieciowego maszyn wirtualnych ich nie muszą mieć taką samą liczbę kart sieciowych, tak długo, jak długo każdy z nich ma co najmniej dwóch.</span><span class="sxs-lookup"><span data-stu-id="52b0e-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="52b0e-158">Nie można skonfigurować maszynę Wirtualną z jednej karty Sieciowej z wielu kart sieciowych (i na odwrót) po wdrożeniu, bez usunięcia i ponownego utworzenia go.</span><span class="sxs-lookup"><span data-stu-id="52b0e-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="52b0e-159">Pomocniczy dostęp kart sieciowych do innych podsieci</span><span class="sxs-lookup"><span data-stu-id="52b0e-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="52b0e-160">Domyślnie dodatkowej karty sieciowe nie zostanie skonfigurowany dla bramy domyślnej z powodu którego będzie ograniczony przepływ ruchu na dodatkowej karty sieciowe muszą mieścić się w tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="52b0e-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="52b0e-161">Jeśli użytkownicy chcesz włączyć dodatkowej kart sieciowych do komunikowania się poza własnej podsieci, muszą dodać wpis w tabeli routingu, aby skonfigurować bramę, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="52b0e-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="52b0e-162">Maszyny wirtualne utworzone przed lipca 2015 może mieć brama domyślna jest skonfigurowana dla wszystkich kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="52b0e-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="52b0e-163">Brama domyślna dla dodatkowej kart sieciowych nie zostaną usunięte, dopóki te maszyny wirtualne są ponownie uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="52b0e-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="52b0e-164">W systemach operacyjnych, w których jest używany model routingu słabe hosta, takich jak Linux Jeśli ruch przychodzące i wychodzące używane różne karty sieciowe mogą być dzielone łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="52b0e-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="52b0e-165">Konfigurowanie maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="52b0e-165">Configure Windows VMs</span></span>
<span data-ttu-id="52b0e-166">Załóżmy, że ma maszyny Wirtualnej systemu Windows z dwiema kartami sieciowymi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="52b0e-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="52b0e-167">Podstawowy adres IP karty Sieciowej: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="52b0e-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="52b0e-168">Pomocniczego adresu IP karty Sieciowej: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="52b0e-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="52b0e-169">Tabeli tras IPv4 dla tej maszyny Wirtualnej będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="52b0e-169">The IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="52b0e-170">Zwróć uwagę, że trasa domyślna (0.0.0.0) jest dostępna tylko dla podstawowego karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="52b0e-171">Nie można uzyskać dostęp do zasobów spoza podsieci dodatkowej karty sieciowej, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="52b0e-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="52b0e-172">Aby dodać trasy domyślnej na pomocniczej karcie interfejsu Sieciowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52b0e-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="52b0e-173">W wierszu polecenia uruchom poniższe polecenie, aby zidentyfikować numer indeksu dodatkowej karty sieciowej:</span><span class="sxs-lookup"><span data-stu-id="52b0e-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="52b0e-174">Zwróć uwagę, drugi wpis w tabeli z indeksem 27 (w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="52b0e-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="52b0e-175">W wierszu polecenia Uruchom **dodać trasy** polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="52b0e-176">W tym przykładzie 192.168.2.1 jest określany jako brama domyślna dodatkowej karty sieciowej:</span><span class="sxs-lookup"><span data-stu-id="52b0e-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="52b0e-177">Aby przetestować połączenie, przejdź wstecz do wiersza polecenia, a następnie spróbuj wysyłania poleceń ping do różnych podsieci z pomocniczego karty Sieciowej jako pokazano int eh w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="52b0e-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="52b0e-178">Możesz również sprawdzić tabeli routingu do sprawdzenia nowo dodanego trasy, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="52b0e-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="52b0e-179">Konfigurowanie maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="52b0e-179">Configure Linux VMs</span></span>
<span data-ttu-id="52b0e-180">Dla maszyn wirtualnych systemu Linux ponieważ domyślnie korzysta z hosta słabe routingu, zaleca się czy dodatkowej karty sieciowe są ograniczone do przepływów ruchu sieciowego tylko w obrębie tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="52b0e-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="52b0e-181">Jednak w przypadku niektórych scenariuszy wymaga łączności spoza podsieci, użytkowników należy włączyć na podstawie zasad routingu, aby upewnić się, że ruch przychodzące i wychodzące używa tej samej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="52b0e-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52b0e-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52b0e-182">Next steps</span></span>
* <span data-ttu-id="52b0e-183">Wdrażanie [MultiNIC maszyn wirtualnych, w przypadku aplikacji warstwy 2 w ramach wdrożenia usługi Resource Manager](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="52b0e-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="52b0e-184">Wdrażanie [MultiNIC maszyn wirtualnych, w przypadku aplikacji warstwy 2 w ramach wdrożenia klasycznego](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="52b0e-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

