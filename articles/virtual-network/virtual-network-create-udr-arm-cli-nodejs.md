---
title: "Kontrolowanie routingu i wirtualnych urządzeń przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie kontrolowania routingu i wirtualnych urządzeń przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="7af20-103">Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7af20-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7af20-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7af20-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="7af20-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7af20-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="7af20-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="7af20-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="7af20-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="7af20-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="7af20-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="7af20-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="7af20-109">Utwórz niestandardowy routing i wirtualnych urządzeń przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7af20-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7af20-110">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="7af20-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="7af20-111">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7af20-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="7af20-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="7af20-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7af20-113">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](virtual-network-create-udr-arm-cli.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="7af20-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="7af20-114">Poniższe przykładowe polecenia interfejsu wiersza polecenia Azure oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza powyżej.</span><span class="sxs-lookup"><span data-stu-id="7af20-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="7af20-115">Jeśli chcesz uruchomić polecenia wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie na platformie Azure**, Zastąp domyślne wartości parametrów, jeśli to konieczne i postępuj zgodnie z instrukcjami w portalu.</span><span class="sxs-lookup"><span data-stu-id="7af20-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="7af20-116">Utwórz przez podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="7af20-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="7af20-117">Aby utworzyć tabelę tras i trasy wymagane do podsieci frontonu oparte na powyższym scenariuszu, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="7af20-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="7af20-118">Uruchom następujące polecenie, aby utworzyć tabelę tras dla podsieci frontonu:</span><span class="sxs-lookup"><span data-stu-id="7af20-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="7af20-119">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7af20-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="7af20-120">Parametry:</span><span class="sxs-lookup"><span data-stu-id="7af20-120">Parameters:</span></span>
   
   * <span data-ttu-id="7af20-121">**-g (lub --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="7af20-122">Nazwa grupy zasobów, w której zostanie utworzona przez.</span><span class="sxs-lookup"><span data-stu-id="7af20-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="7af20-123">W naszym scenariuszu jest to *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="7af20-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="7af20-124">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-124">**-l (or --location)**.</span></span> <span data-ttu-id="7af20-125">Region platformy Azure, w której zostanie utworzona przez nowe.</span><span class="sxs-lookup"><span data-stu-id="7af20-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="7af20-126">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="7af20-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="7af20-127">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-127">**-n (or --name)**.</span></span> <span data-ttu-id="7af20-128">Nazwa nowej przez.</span><span class="sxs-lookup"><span data-stu-id="7af20-128">Name for the new UDR.</span></span> <span data-ttu-id="7af20-129">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="7af20-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="7af20-130">Uruchom następujące polecenie, aby utworzyć trasę w tabeli tras do wysyłania całego ruchu kierowanego do podsieci zaplecza (192.168.2.0/24), aby **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="7af20-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="7af20-131">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7af20-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="7af20-132">Parametry:</span><span class="sxs-lookup"><span data-stu-id="7af20-132">Parameters:</span></span>
   
   * <span data-ttu-id="7af20-133">**-r (lub--nazwa tabeli tras)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="7af20-134">Nazwa tabeli tras, w którym można dodać trasy.</span><span class="sxs-lookup"><span data-stu-id="7af20-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="7af20-135">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="7af20-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="7af20-136">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="7af20-137">Prefiks adresu podsieci, gdy pakiety są przeznaczone do.</span><span class="sxs-lookup"><span data-stu-id="7af20-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="7af20-138">W naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="7af20-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="7af20-139">**-y (lub--następnego przeskoku typu)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="7af20-140">Typ obiektu ruchu zostaną wysłane do.</span><span class="sxs-lookup"><span data-stu-id="7af20-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="7af20-141">Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.</span><span class="sxs-lookup"><span data-stu-id="7af20-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="7af20-142">**-p (lub--dalej przeskoku — adres ip**).</span><span class="sxs-lookup"><span data-stu-id="7af20-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="7af20-143">Adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="7af20-143">IP address for next hop.</span></span> <span data-ttu-id="7af20-144">W naszym scenariuszu *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="7af20-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="7af20-145">Uruchom następujące polecenie, aby skojarzyć utworzone powyżej z tabeli tras **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="7af20-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="7af20-146">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7af20-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="7af20-147">Parametry:</span><span class="sxs-lookup"><span data-stu-id="7af20-147">Parameters:</span></span>
   
   * <span data-ttu-id="7af20-148">**-e (lub--vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="7af20-149">Nazwa sieci wirtualnej, w którym znajduje się podsieci.</span><span class="sxs-lookup"><span data-stu-id="7af20-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="7af20-150">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="7af20-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="7af20-151">Utwórz przez podsieci wewnętrznej</span><span class="sxs-lookup"><span data-stu-id="7af20-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="7af20-152">Aby utworzyć tabelę tras i trasy wymagane dla podsieci zaplecza opartą na tym scenariuszu powyżej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7af20-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="7af20-153">Uruchom następujące polecenie, aby utworzyć tabelę tras dla podsieci wewnętrznej:</span><span class="sxs-lookup"><span data-stu-id="7af20-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="7af20-154">Uruchom następujące polecenie, aby utworzyć trasę w tabeli tras do wysyłania całego ruchu kierowanego do podsieci frontonu (192.168.1.0/24), aby **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="7af20-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="7af20-155">Uruchom następujące polecenie, aby skojarzyć tabela tras o **zaplecza** podsieci:</span><span class="sxs-lookup"><span data-stu-id="7af20-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="7af20-156">Włącz przesyłanie dalej IP na FW1</span><span class="sxs-lookup"><span data-stu-id="7af20-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="7af20-157">Aby włączyć przesyłanie dalej IP w używany przez kartę Sieciową **FW1**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7af20-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="7af20-158">Uruchom polecenie i zwróć uwagę, wartość **przesyłanie dalej IP włączyć**.</span><span class="sxs-lookup"><span data-stu-id="7af20-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="7af20-159">Należy wybrać opcję *false*.</span><span class="sxs-lookup"><span data-stu-id="7af20-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="7af20-160">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7af20-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="7af20-161">Uruchom następujące polecenie, aby włączyć przesyłanie dalej IP:</span><span class="sxs-lookup"><span data-stu-id="7af20-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="7af20-162">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7af20-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="7af20-163">Parametry:</span><span class="sxs-lookup"><span data-stu-id="7af20-163">Parameters:</span></span>
   
   * <span data-ttu-id="7af20-164">**-f (lub--Włącz przesyłanie dalej ip)**.</span><span class="sxs-lookup"><span data-stu-id="7af20-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="7af20-165">*wartość true,* lub *false*.</span><span class="sxs-lookup"><span data-stu-id="7af20-165">*true* or *false*.</span></span>

