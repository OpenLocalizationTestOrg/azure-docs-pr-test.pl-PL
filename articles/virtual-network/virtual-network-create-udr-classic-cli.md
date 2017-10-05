---
title: Kontrolowanie routingu w klasycznym Azure Virtual Network - CLI - | Dokumentacja firmy Microsoft
description: "Informacje o sposobie kontrolowania routingu w sieci wirtualnych w klasycznym modelu wdrażania przy użyciu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 8fcb98723e7e872c932908e3456dc8680deb0901
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-the-azure-cli"></a><span data-ttu-id="d88ef-103">Kontrolowanie routingu i używaniu urządzeń wirtualnych (klasyczne) przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d88ef-103">Control routing and use virtual appliances (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d88ef-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d88ef-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="d88ef-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d88ef-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="d88ef-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="d88ef-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="d88ef-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="d88ef-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="d88ef-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="d88ef-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d88ef-109">W tym artykule opisano klasyczny model wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d88ef-109">This article covers the classic deployment model.</span></span> <span data-ttu-id="d88ef-110">Możesz również [kontrolować routingu i używaniu urządzeń wirtualnych w modelu wdrażania usługi Resource Manager](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d88ef-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="d88ef-111">Poniższe przykładowe polecenia interfejsu wiersza polecenia Azure oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza powyżej.</span><span class="sxs-lookup"><span data-stu-id="d88ef-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="d88ef-112">Jeśli chcesz uruchomić polecenia wyświetlaną w tym dokumencie, należy utworzyć w środowisku pokazanym w [Utwórz sieć wirtualną (klasyczne) przy użyciu interfejsu wiersza polecenia Azure](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d88ef-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="d88ef-113">Utwórz przez podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="d88ef-113">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="d88ef-114">Aby utworzyć tabelę tras i trasy wymagane do podsieci frontonu oparte na powyższym scenariuszu, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="d88ef-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="d88ef-115">Uruchom następujące polecenie, aby przełączyć do trybu klasycznego:</span><span class="sxs-lookup"><span data-stu-id="d88ef-115">Run the following command to switch to classic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="d88ef-116">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d88ef-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="d88ef-117">Uruchom następujące polecenie, aby utworzyć tabelę tras dla podsieci frontonu:</span><span class="sxs-lookup"><span data-stu-id="d88ef-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="d88ef-118">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d88ef-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="d88ef-119">Parametry:</span><span class="sxs-lookup"><span data-stu-id="d88ef-119">Parameters:</span></span>
   
   * <span data-ttu-id="d88ef-120">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-120">**-l (or --location)**.</span></span> <span data-ttu-id="d88ef-121">Region platformy Azure, w którym zostanie utworzona nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="d88ef-121">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="d88ef-122">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="d88ef-123">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-123">**-n (or --name)**.</span></span> <span data-ttu-id="d88ef-124">Nazwa nowej grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="d88ef-124">Name for the new NSG.</span></span> <span data-ttu-id="d88ef-125">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="d88ef-126">Uruchom następujące polecenie, aby utworzyć trasę w tabeli tras do wysyłania całego ruchu kierowanego do podsieci zaplecza (192.168.2.0/24), aby **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="d88ef-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="d88ef-127">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d88ef-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="d88ef-128">Parametry:</span><span class="sxs-lookup"><span data-stu-id="d88ef-128">Parameters:</span></span>
   
   * <span data-ttu-id="d88ef-129">**-r (lub--nazwa tabeli tras)**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="d88ef-130">Nazwa tabeli tras, w którym można dodać trasy.</span><span class="sxs-lookup"><span data-stu-id="d88ef-130">Name of the route table where the route will be added.</span></span> <span data-ttu-id="d88ef-131">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="d88ef-132">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="d88ef-133">Prefiks adresu podsieci, gdy pakiety są przeznaczone do.</span><span class="sxs-lookup"><span data-stu-id="d88ef-133">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="d88ef-134">W naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="d88ef-135">**-t (lub--następnego przeskoku typu)**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="d88ef-136">Typ obiektu ruchu zostaną wysłane do.</span><span class="sxs-lookup"><span data-stu-id="d88ef-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="d88ef-137">Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="d88ef-138">**-p (lub--dalej przeskoku — adres ip**).</span><span class="sxs-lookup"><span data-stu-id="d88ef-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="d88ef-139">Adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="d88ef-139">IP address for next hop.</span></span> <span data-ttu-id="d88ef-140">W naszym scenariuszu *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="d88ef-141">Uruchom następujące polecenie, aby skojarzyć utworzone za pomocą tabeli tras **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="d88ef-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="d88ef-142">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d88ef-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="d88ef-143">Parametry:</span><span class="sxs-lookup"><span data-stu-id="d88ef-143">Parameters:</span></span>
   
   * <span data-ttu-id="d88ef-144">**-t (lub--vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="d88ef-145">Nazwa sieci wirtualnej, w którym znajduje się podsieci.</span><span class="sxs-lookup"><span data-stu-id="d88ef-145">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="d88ef-146">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="d88ef-147">**-n (lub--nazwy podsieci**.</span><span class="sxs-lookup"><span data-stu-id="d88ef-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="d88ef-148">Nazwa tabeli tras zostanie dodany do podsieci.</span><span class="sxs-lookup"><span data-stu-id="d88ef-148">Name of the subnet the route table will be added to.</span></span> <span data-ttu-id="d88ef-149">W naszym scenariuszu jest to *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="d88ef-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="d88ef-150">Utwórz przez podsieci wewnętrznej</span><span class="sxs-lookup"><span data-stu-id="d88ef-150">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="d88ef-151">Aby utworzyć tabelę tras i trasy wymagane do podsieci zaplecza opartą na tym scenariuszu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d88ef-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="d88ef-152">Uruchom następujące polecenie, aby utworzyć tabelę tras dla podsieci wewnętrznej:</span><span class="sxs-lookup"><span data-stu-id="d88ef-152">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="d88ef-153">Uruchom następujące polecenie, aby utworzyć trasę w tabeli tras do wysyłania całego ruchu kierowanego do podsieci frontonu (192.168.1.0/24), aby **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="d88ef-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="d88ef-154">Uruchom następujące polecenie, aby skojarzyć tabela tras o **zaplecza** podsieci:</span><span class="sxs-lookup"><span data-stu-id="d88ef-154">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

