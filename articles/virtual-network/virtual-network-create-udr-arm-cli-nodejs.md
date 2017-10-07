---
title: "aaaControl routingu i wirtualnych urządzeń za pomocą hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocontrol routingu i wirtualnych urządzeń za pomocą hello Azure CLI w wersji 1.0."
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
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="0e4bc-103">Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="0e4bc-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e4bc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e4bc-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="0e4bc-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e4bc-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="0e4bc-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="0e4bc-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="0e4bc-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="0e4bc-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="0e4bc-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="0e4bc-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="0e4bc-109">Utwórz niestandardowy routing i wirtualnych urządzeń przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0e4bc-110">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0e4bc-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="0e4bc-111">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="0e4bc-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="0e4bc-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0e4bc-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="0e4bc-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="0e4bc-114">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="0e4bc-115">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="0e4bc-116">Utwórz hello przez hello podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="0e4bc-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="0e4bc-117">tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="0e4bc-118">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci frontonu hello:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="0e4bc-119">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-119">Output:</span></span>
   
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
   
    <span data-ttu-id="0e4bc-120">Parametry:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-120">Parameters:</span></span>
   
   * <span data-ttu-id="0e4bc-121">**-g (lub --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="0e4bc-122">Nazwa grupy zasobów hello której zostanie utworzona przez hello.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="0e4bc-123">W naszym scenariuszu jest to *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="0e4bc-124">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-124">**-l (or --location)**.</span></span> <span data-ttu-id="0e4bc-125">Region platformy Azure, której hello przez nowe zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="0e4bc-126">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="0e4bc-127">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-127">**-n (or --name)**.</span></span> <span data-ttu-id="0e4bc-128">Nazwa hello przez nowe.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-128">Name for hello new UDR.</span></span> <span data-ttu-id="0e4bc-129">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="0e4bc-130">Uruchom następujące polecenie toocreate trasy w toosend tabeli tras hello hello wszystkich toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="0e4bc-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="0e4bc-131">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-131">Output:</span></span>
   
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
   
    <span data-ttu-id="0e4bc-132">Parametry:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-132">Parameters:</span></span>
   
   * <span data-ttu-id="0e4bc-133">**-r (lub--nazwa tabeli tras)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="0e4bc-134">Nazwa tabeli tras hello, gdzie ma zostać dodana hello trasy.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="0e4bc-135">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="0e4bc-136">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="0e4bc-137">Prefiks adresu podsieci hello, gdy pakiety są przeznaczone do.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="0e4bc-138">W naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="0e4bc-139">**-y (lub--następnego przeskoku typu)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="0e4bc-140">Typ obiektu ruchu zostaną wysłane do.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="0e4bc-141">Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="0e4bc-142">**-p (lub--dalej przeskoku — adres ip**).</span><span class="sxs-lookup"><span data-stu-id="0e4bc-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="0e4bc-143">Adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-143">IP address for next hop.</span></span> <span data-ttu-id="0e4bc-144">W naszym scenariuszu *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="0e4bc-145">Witaj uruchom następujące polecenie tabeli tras hello tooassociate utworzone powyżej z hello **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="0e4bc-146">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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
   
    <span data-ttu-id="0e4bc-147">Parametry:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-147">Parameters:</span></span>
   
   * <span data-ttu-id="0e4bc-148">**-e (lub--vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="0e4bc-149">Nazwa sieci wirtualnej, w którym znajduje się podsieci hello hello.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="0e4bc-150">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="0e4bc-151">Utwórz hello przez hello zaplecza podsieci</span><span class="sxs-lookup"><span data-stu-id="0e4bc-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="0e4bc-152">Witaj toocreate tabeli tras i trasy, potrzebnego do podsieci wewnętrznej hello oparta na scenariuszu hello powyżej pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="0e4bc-153">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="0e4bc-154">Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="0e4bc-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="0e4bc-155">Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="0e4bc-156">Włącz przesyłanie dalej IP na FW1</span><span class="sxs-lookup"><span data-stu-id="0e4bc-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="0e4bc-157">przesyłanie dalej IP tooenable w hello używany przez kartę Sieciową **FW1**pełnego hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="0e4bc-158">Uruchom polecenie hello, i zwróć uwagę, wartość hello **przesyłanie dalej IP włączyć**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="0e4bc-159">Powinna być ustawiona zbyt*false*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="0e4bc-160">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
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
2. <span data-ttu-id="0e4bc-161">Witaj uruchom następujące polecenie tooenable przesyłanie dalej IP:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="0e4bc-162">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
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
   
    <span data-ttu-id="0e4bc-163">Parametry:</span><span class="sxs-lookup"><span data-stu-id="0e4bc-163">Parameters:</span></span>
   
   * <span data-ttu-id="0e4bc-164">**-f (lub--Włącz przesyłanie dalej ip)**.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="0e4bc-165">*wartość true,* lub *false*.</span><span class="sxs-lookup"><span data-stu-id="0e4bc-165">*true* or *false*.</span></span>

