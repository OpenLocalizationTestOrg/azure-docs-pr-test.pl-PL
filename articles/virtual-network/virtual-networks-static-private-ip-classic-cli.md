---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych (klasyczne) - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych (klasyczne) za pomocą hello Azure interfejsu wiersza polecenia (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="a5bbb-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej (klasyczne) przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a5bbb-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a5bbb-104">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="a5bbb-105">Możesz również [Zarządzanie statycznego prywatnego adresu IP w modelu wdrażania usługi Resource Manager hello](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a5bbb-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="a5bbb-106">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="a5bbb-107">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a5bbb-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="a5bbb-108">Jak toospecify statycznych prywatnych adresów IP podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a5bbb-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="a5bbb-109">toocreate nowej maszyny Wirtualnej o nazwie *DNS01* w nową usługę w chmurze o nazwie *TestService* oparte na powyższym scenariuszu hello, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="a5bbb-110">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a5bbb-111">Uruchom hello **tworzenia usługi azure** poleceń usługi w chmurze hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="a5bbb-112">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="a5bbb-113">Uruchom hello **azure tworzenie maszyny wirtualnej** polecenia toocreate hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="a5bbb-114">Zwróć uwagę, wartość hello statycznego prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="a5bbb-115">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="a5bbb-116">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="a5bbb-117">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-117">**-l (or --location)**.</span></span> <span data-ttu-id="a5bbb-118">Region platformy Azure, w której zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="a5bbb-119">W naszym scenariuszu jest to *centralus*.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="a5bbb-120">**-n (lub nazwę maszyny wirtualnej —)**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="a5bbb-121">Nazwa hello toobe maszyny Wirtualnej utworzone.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="a5bbb-122">**-w (lub--wirtualnej nazwy sieciowej)**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="a5bbb-123">Nazwa hello sieci wirtualnej, w której zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="a5bbb-124">**-S (lub--static ip)**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="a5bbb-125">Statycznego prywatnego adresu IP dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="a5bbb-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-126">**TestService**.</span></span> <span data-ttu-id="a5bbb-127">Nazwa usługi w chmurze hello której zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="a5bbb-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="a5bbb-129">Obraz używany hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="a5bbb-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-130">**adminuser**.</span></span> <span data-ttu-id="a5bbb-131">Administrator lokalny hello maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="a5bbb-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="a5bbb-133">Hasło administratora lokalnego dla maszyny Wirtualnej systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="a5bbb-134">Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a5bbb-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="a5bbb-135">tooview hello statycznego prywatnego adresu IP adres dla hello maszyny Wirtualnej utworzone za pomocą skryptu hello powyżej, uruchom następujące polecenie z wiersza polecenia platformy Azure hello i sprawdź wartość hello *StaticIP sieci*:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="a5bbb-136">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="a5bbb-137">Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a5bbb-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="a5bbb-138">tooremove hello statycznego prywatnego adresu IP dodane toohello maszyny Wirtualnej w skrypcie hello powyżej hello uruchom następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="a5bbb-139">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="a5bbb-140">Jak tooadd statycznego prywatnego tooan IP istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a5bbb-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="a5bbb-141">tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu skryptu hello powyżej runt następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="a5bbb-142">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a5bbb-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="a5bbb-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5bbb-143">Next steps</span></span>
* <span data-ttu-id="a5bbb-144">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="a5bbb-145">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="a5bbb-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="a5bbb-146">Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5bbb-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

