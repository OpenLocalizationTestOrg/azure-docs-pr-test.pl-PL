---
title: aaaControl routingu w klasycznym Azure Virtual Network - CLI - | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak hello toocontrol routingu w sieci wirtualnych za pomocą wiersza polecenia platformy Azure w hello klasycznego modelu wdrażania"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="3480d-103">Formant routingu i użyj wirtualnych urządzeń (klasyczne) przy użyciu interfejsu wiersza polecenia Azure hello</span><span class="sxs-lookup"><span data-stu-id="3480d-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3480d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3480d-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="3480d-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3480d-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="3480d-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="3480d-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="3480d-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="3480d-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="3480d-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="3480d-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3480d-109">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3480d-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="3480d-110">Możesz również [kontrolować routingu i używaniu urządzeń wirtualnych w modelu wdrażania usługi Resource Manager hello](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3480d-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="3480d-111">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="3480d-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="3480d-112">Polecenia hello toorun wyświetlaną w tym dokumencie, utworzyć środowisko hello pokazano [Utwórz sieć wirtualną (klasyczne) przy użyciu interfejsu wiersza polecenia Azure hello](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3480d-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="3480d-113">Utwórz hello przez dla podsieci frontonu hello</span><span class="sxs-lookup"><span data-stu-id="3480d-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="3480d-114">tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="3480d-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="3480d-115">Witaj uruchom następujące polecenie Tryb tooclassic tooswitch:</span><span class="sxs-lookup"><span data-stu-id="3480d-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="3480d-116">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="3480d-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="3480d-117">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci frontonu hello:</span><span class="sxs-lookup"><span data-stu-id="3480d-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="3480d-118">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="3480d-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="3480d-119">Parametry:</span><span class="sxs-lookup"><span data-stu-id="3480d-119">Parameters:</span></span>
   
   * <span data-ttu-id="3480d-120">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="3480d-120">**-l (or --location)**.</span></span> <span data-ttu-id="3480d-121">Region platformy Azure, której hello Nowa grupa NSG zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="3480d-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="3480d-122">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="3480d-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="3480d-123">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="3480d-123">**-n (or --name)**.</span></span> <span data-ttu-id="3480d-124">Nazwa hello Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="3480d-124">Name for hello new NSG.</span></span> <span data-ttu-id="3480d-125">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="3480d-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="3480d-126">Uruchom następujące polecenie toocreate trasy w toosend tabeli tras hello hello wszystkich toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3480d-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="3480d-127">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="3480d-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="3480d-128">Parametry:</span><span class="sxs-lookup"><span data-stu-id="3480d-128">Parameters:</span></span>
   
   * <span data-ttu-id="3480d-129">**-r (lub--nazwa tabeli tras)**.</span><span class="sxs-lookup"><span data-stu-id="3480d-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="3480d-130">Nazwa tabeli tras hello, gdzie ma zostać dodana hello trasy.</span><span class="sxs-lookup"><span data-stu-id="3480d-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="3480d-131">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="3480d-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="3480d-132">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="3480d-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="3480d-133">Prefiks adresu podsieci hello, gdy pakiety są przeznaczone do.</span><span class="sxs-lookup"><span data-stu-id="3480d-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="3480d-134">W naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="3480d-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="3480d-135">**-t (lub--następnego przeskoku typu)**.</span><span class="sxs-lookup"><span data-stu-id="3480d-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="3480d-136">Typ obiektu ruchu zostaną wysłane do.</span><span class="sxs-lookup"><span data-stu-id="3480d-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="3480d-137">Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.</span><span class="sxs-lookup"><span data-stu-id="3480d-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="3480d-138">**-p (lub--dalej przeskoku — adres ip**).</span><span class="sxs-lookup"><span data-stu-id="3480d-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="3480d-139">Adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="3480d-139">IP address for next hop.</span></span> <span data-ttu-id="3480d-140">W naszym scenariuszu *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="3480d-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="3480d-141">Witaj uruchom następujące polecenie tabeli tras hello tooassociate utworzone za pomocą hello **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="3480d-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="3480d-142">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="3480d-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="3480d-143">Parametry:</span><span class="sxs-lookup"><span data-stu-id="3480d-143">Parameters:</span></span>
   
   * <span data-ttu-id="3480d-144">**-t (lub--vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="3480d-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="3480d-145">Nazwa sieci wirtualnej, w którym znajduje się podsieci hello hello.</span><span class="sxs-lookup"><span data-stu-id="3480d-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="3480d-146">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="3480d-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="3480d-147">**-n (lub--nazwy podsieci**.</span><span class="sxs-lookup"><span data-stu-id="3480d-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="3480d-148">Nazwa tabeli tras hello podsieci hello zostaną dodane do.</span><span class="sxs-lookup"><span data-stu-id="3480d-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="3480d-149">W naszym scenariuszu jest to *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="3480d-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="3480d-150">Utwórz hello przez hello zaplecza podsieci</span><span class="sxs-lookup"><span data-stu-id="3480d-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="3480d-151">Tabela tras hello toocreate i trasy wymagane do podsieci wewnętrznej hello oparta na scenariuszu hello pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3480d-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="3480d-152">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:</span><span class="sxs-lookup"><span data-stu-id="3480d-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="3480d-153">Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3480d-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="3480d-154">Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:</span><span class="sxs-lookup"><span data-stu-id="3480d-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

