---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych za pomocą hello Azure interfejsu wiersza polecenia (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="32a8c-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej z wykorzystaniem hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="32a8c-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="32a8c-104">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="32a8c-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="32a8c-105">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="32a8c-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="32a8c-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="32a8c-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="32a8c-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) — nasze CLI następnej generacji dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="32a8c-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="32a8c-108">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="32a8c-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="32a8c-109">Możesz również [Zarządzanie statycznego prywatnego adresu IP w hello klasycznego modelu wdrażania](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="32a8c-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="32a8c-110">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="32a8c-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="32a8c-111">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="32a8c-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="32a8c-112">Jak toospecify statycznych prywatnych adresów IP podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="32a8c-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="32a8c-113">toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="32a8c-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="32a8c-114">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="32a8c-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="32a8c-115">Uruchom hello **trybie azure config** tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="32a8c-116">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="32a8c-117">Uruchom hello **utworzyć sieć platformy azure publicznego ip** toocreate publicznego adresu IP dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="32a8c-118">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="32a8c-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="32a8c-119">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="32a8c-120">**-g (lub --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="32a8c-121">Nazwa hello zasobów grupy hello publiczny adres IP zostanie utworzony w.</span><span class="sxs-lookup"><span data-stu-id="32a8c-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="32a8c-122">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-122">**-n (or --name)**.</span></span> <span data-ttu-id="32a8c-123">Nazwa hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="32a8c-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="32a8c-124">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-124">**-l (or --location)**.</span></span> <span data-ttu-id="32a8c-125">Region platformy Azure, w której zostanie utworzona hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="32a8c-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="32a8c-126">W naszym scenariuszu jest to *centralus*.</span><span class="sxs-lookup"><span data-stu-id="32a8c-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="32a8c-127">Uruchom hello **tworzenie kart interfejsu sieciowego azure** toocreate polecenia ze statycznego prywatnego adresu IP karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="32a8c-128">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="32a8c-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="32a8c-129">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="32a8c-130">**-(lub--prywatny adres ip)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="32a8c-131">Statycznego prywatnego adresu IP dla hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="32a8c-132">**-m (lub--nazwy podsieci-sieci wirtualnej)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="32a8c-133">Nazwa hello sieci wirtualnej, w której zostanie utworzona hello karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="32a8c-134">**-k (lub--nazwy podsieci)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="32a8c-135">Nazwa podsieci hello której zostanie utworzona hello karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="32a8c-136">Uruchom hello **tworzenia maszyny wirtualnej azure** hello toocreate polecenia przy użyciu hello publicznego adresu IP i karty Sieciowej maszyny Wirtualnej utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="32a8c-137">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="32a8c-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="32a8c-138">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="32a8c-139">**-y (lub--os-type)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="32a8c-140">Typ systemu operacyjnego systemu hello maszynę Wirtualną, albo *Windows* lub *Linux*.</span><span class="sxs-lookup"><span data-stu-id="32a8c-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="32a8c-141">**-f (lub nazwę karty sieciowej —)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="32a8c-142">Użyje nazwy hello hello karty Sieciowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="32a8c-143">**-i (lub--nazwa publicznego ip)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="32a8c-144">Użyje nazwy hello publicznego adresu IP hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="32a8c-145">**-F (lub--vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="32a8c-146">Nazwa hello sieci wirtualnej, w której zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="32a8c-147">**-j (lub--vnet-podsieci name)**.</span><span class="sxs-lookup"><span data-stu-id="32a8c-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="32a8c-148">Nazwa podsieci hello której zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="32a8c-149">Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="32a8c-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="32a8c-150">tooview hello statycznego prywatnego adresu IP adres dla hello maszyny Wirtualnej utworzone za pomocą skryptu hello powyżej, uruchom następujące polecenie z wiersza polecenia platformy Azure hello i sprawdź wartości hello *metody alokacji prywatnego adresu IP* i *prywatny adres IP*:</span><span class="sxs-lookup"><span data-stu-id="32a8c-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="32a8c-151">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="32a8c-152">Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="32a8c-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="32a8c-153">Nie można usunąć statycznego prywatnego adresu IP z karty Sieciowej w wiersza polecenia platformy Azure dla Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="32a8c-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="32a8c-154">Należy utworzyć nowe kartę Sieciową, która korzysta z dynamicznego adresu IP, Usuń hello poprzedniej karty Sieciowej z hello maszyny Wirtualnej, a następnie dodaj nowe hello toohello karty Sieciowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="32a8c-155">toochange hello kart interfejsu Sieciowego dla hello wirtualna używana int eh powyższych poleceń, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="32a8c-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="32a8c-156">Uruchom hello **tworzenie kart interfejsu sieciowego azure** polecenia toocreate nowej karty Sieciowej, za pomocą alokacji dynamicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="32a8c-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="32a8c-157">Zwróć uwagę, jak nie ma potrzeby adres IP hello toospecify teraz.</span><span class="sxs-lookup"><span data-stu-id="32a8c-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="32a8c-158">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="32a8c-159">Uruchom hello **zestawu azure vm** hello toochange polecenia używane przez hello maszyny Wirtualnej karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="32a8c-160">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="32a8c-161">Jeśli, uruchom hello **usunąć kart interfejsu sieciowego azure** polecenia toodelete hello starego karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="32a8c-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="32a8c-162">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="32a8c-163">Jak tooadd statycznego prywatnego adresu IP adresów tooan istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="32a8c-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="32a8c-164">tooadd statyczne prywatnego adresu IP adres toohello kart używane przez maszynę Wirtualną, utworzone za pomocą skryptu hello powyżej, uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="32a8c-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="32a8c-165">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32a8c-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="32a8c-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32a8c-166">Next steps</span></span>
* <span data-ttu-id="32a8c-167">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="32a8c-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="32a8c-168">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="32a8c-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="32a8c-169">Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="32a8c-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

