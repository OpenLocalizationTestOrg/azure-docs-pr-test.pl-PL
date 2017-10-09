---
title: "aaaControl routingu i wirtualnych urządzeń za pomocą hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocontrol routingu i wirtualnych urządzeń za pomocą hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="ec9bb-103">Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ec9bb-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec9bb-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec9bb-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="ec9bb-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ec9bb-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="ec9bb-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="ec9bb-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="ec9bb-107">PowerShell (wdrożenia klasycznego)</span><span class="sxs-lookup"><span data-stu-id="ec9bb-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="ec9bb-108">Interfejs wiersza polecenia (wdrożenia klasycznego)</span><span class="sxs-lookup"><span data-stu-id="ec9bb-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ec9bb-109">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="ec9bb-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ec9bb-110">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ec9bb-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="ec9bb-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="ec9bb-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="ec9bb-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="ec9bb-113">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="ec9bb-114">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="ec9bb-115">Utwórz hello przez hello podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="ec9bb-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="ec9bb-116">tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="ec9bb-117">Utwórz tabelę tras dla podsieci frontonu hello z hello [utworzyć tabelę tras az sieci](/cli/azure/network/route-table#create) polecenia:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="ec9bb-118">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="ec9bb-119">Utwórz trasę, która wysyła wszystkie toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4) przy użyciu hello [utwórz trasę tabeli tras sieciowych az](/cli/azure/network/route-table/route#create) polecenia:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="ec9bb-120">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="ec9bb-121">Parametry:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-121">Parameters:</span></span>

    * <span data-ttu-id="ec9bb-122">**--Nazwa tabeli tras**.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-122">**--route-table-name**.</span></span> <span data-ttu-id="ec9bb-123">Nazwa tabeli tras hello, gdzie ma zostać dodana hello trasy.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="ec9bb-124">W naszym scenariuszu *frontonu przez*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="ec9bb-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-125">**--address-prefix**.</span></span> <span data-ttu-id="ec9bb-126">Prefiks adresu podsieci hello, gdy pakiety są przeznaczone do.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="ec9bb-127">W naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="ec9bb-128">**--następnego przeskoku typu**.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-128">**--next-hop-type**.</span></span> <span data-ttu-id="ec9bb-129">Typ obiektu ruchu zostaną wysłane do.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="ec9bb-130">Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="ec9bb-131">**--dalej przeskoku — adres ip**.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="ec9bb-132">Adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-132">IP address for next hop.</span></span> <span data-ttu-id="ec9bb-133">W naszym scenariuszu *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="ec9bb-134">Uruchom hello [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) tabeli tras hello tooassociate polecenia utworzone powyżej z hello **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="ec9bb-135">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="ec9bb-136">Parametry:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-136">Parameters:</span></span>
    
    * <span data-ttu-id="ec9bb-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-137">**--vnet-name**.</span></span> <span data-ttu-id="ec9bb-138">Nazwa sieci wirtualnej, w którym znajduje się podsieci hello hello.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="ec9bb-139">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="ec9bb-140">Utwórz hello przez hello zaplecza podsieci</span><span class="sxs-lookup"><span data-stu-id="ec9bb-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="ec9bb-141">Witaj toocreate tabeli tras i trasy, potrzebnego do podsieci wewnętrznej hello oparta na scenariuszu hello powyżej pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="ec9bb-142">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="ec9bb-143">Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="ec9bb-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="ec9bb-144">Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="ec9bb-145">Włącz przesyłanie dalej IP na FW1</span><span class="sxs-lookup"><span data-stu-id="ec9bb-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="ec9bb-146">przesyłanie dalej IP tooenable w hello używany przez kartę Sieciową **FW1**pełnego hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="ec9bb-147">Uruchom hello [Pokaż kart sieciowych az](/cli/azure/network/nic#show) poleceń z bieżącej hello toodisplay filtru JMESPATH **Włącz przesyłanie dalej ip** wartość **przesyłanie dalej IP włączyć**.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="ec9bb-148">Powinna być ustawiona zbyt*false*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="ec9bb-149">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-149">Output:</span></span>

        false

2. <span data-ttu-id="ec9bb-150">Witaj uruchom następujące polecenie tooenable przesyłanie dalej IP:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="ec9bb-151">Można przejrzeć konsoli toohello strumienia wyjściowego hello, lub po prostu sprawdź jeszcze raz dla określonych hello **enableIpForwarding** wartość:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="ec9bb-152">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-152">Output:</span></span>

        true

    <span data-ttu-id="ec9bb-153">Parametry:</span><span class="sxs-lookup"><span data-stu-id="ec9bb-153">Parameters:</span></span>

    <span data-ttu-id="ec9bb-154">**przesyłanie dalej ip —**: *true* lub *false*.</span><span class="sxs-lookup"><span data-stu-id="ec9bb-154">**--ip-forwarding**: *true* or *false*.</span></span>

