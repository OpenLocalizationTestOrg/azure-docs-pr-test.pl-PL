---
title: "Dodawanie wielu połączeń lokacja-lokacja bramy sieci VPN do sieci wirtualnej: Azure Portal: Resource Manager | Dokumentacja firmy Microsoft"
description: "Dodawaj połączeń S2S obejmujący wiele lokacji do bramy sieci VPN, który ma istniejącego połączenia"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: 7ec57789ee76f4ec54e4f7b68ea75c19522f3d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="c7c26-103">Dodaj połączenie lokacja-lokacja z sieci wirtualnej z istniejącego połączenia bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c7c26-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7c26-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c7c26-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c7c26-105">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="c7c26-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="c7c26-106">Ten artykuł przeprowadzi Cię przez dodawanie połączeń lokacja-lokacja (S2S) do bramy sieci VPN, który ma istniejącego połączenia przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c26-106">This article walks you through using the Azure portal to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="c7c26-107">Połączenia tego typu jest często określany jako "obejmujący wiele lokacji" konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c7c26-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="c7c26-108">Można dodać połączenia S2S na sieć wirtualną, która ma już połączenia S2S, połączenie punkt-lokacja lub połączenia do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="c7c26-108">You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="c7c26-109">Podczas dodawania połączenia istnieją pewne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="c7c26-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="c7c26-110">Sprawdź [przed rozpoczęciem](#before) w tym artykule, aby sprawdzić przed rozpoczęciem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c7c26-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span></span> 

<span data-ttu-id="c7c26-111">Ten artykuł dotyczy sieci wirtualnych utworzonych przy użyciu modelu wdrażania usługi Resource Manager mające bramy sieci RouteBased VPN.</span><span class="sxs-lookup"><span data-stu-id="c7c26-111">This article applies to VNets created using the Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="c7c26-112">Te kroki nie dotyczą konfiguracji połączenia ważnych ExpressRoute/lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="c7c26-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="c7c26-113">Zobacz [ważnych połączeń ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) informacji o ważnych połączenia.</span><span class="sxs-lookup"><span data-stu-id="c7c26-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="c7c26-114">Modele i metody wdrażania</span><span class="sxs-lookup"><span data-stu-id="c7c26-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="c7c26-115">Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c7c26-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="c7c26-116">Po udostępnieniu artykułu możemy link bezpośrednio do niego z tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="c7c26-116">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="c7c26-117"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c7c26-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="c7c26-118">Sprawdź następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c7c26-118">Verify the following items:</span></span>

* <span data-ttu-id="c7c26-119">Połączenie ExpressRoute/S2S coexisting nie są tworzone.</span><span class="sxs-lookup"><span data-stu-id="c7c26-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="c7c26-120">Masz sieci wirtualnej, który został utworzony przy użyciu modelu wdrażania usługi Resource Manager z istniejącym połączeniem.</span><span class="sxs-lookup"><span data-stu-id="c7c26-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="c7c26-121">Brama sieci wirtualnej sieci wirtualnej jest RouteBased.</span><span class="sxs-lookup"><span data-stu-id="c7c26-121">The virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="c7c26-122">Jeśli masz bramy sieci PolicyBased VPN, należy usunąć bramę sieci wirtualnej i Utwórz nową bramę sieci VPN jako RouteBased.</span><span class="sxs-lookup"><span data-stu-id="c7c26-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="c7c26-123">Żaden z zakresów adresów nakładać się na każdej sieci wirtualnych, które ta sieć wirtualna nawiązuje połączenie z.</span><span class="sxs-lookup"><span data-stu-id="c7c26-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="c7c26-124">Masz zgodne urządzenie sieci VPN i osoby, która jest w stanie go skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="c7c26-124">You have compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="c7c26-125">Zobacz artykuł [About VPN Devices](vpn-gateway-about-vpn-devices.md) (Urządzenia sieci VPN — informacje).</span><span class="sxs-lookup"><span data-stu-id="c7c26-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="c7c26-126">Jeśli nie dysponujesz wiedzą niezbędną do skonfigurowania urządzenia sieci VPN lub nie znasz zakresu adresów IP ujętego w konfiguracji sieci lokalnej, skontaktuj się z osobą, która może podać Ci te dane.</span><span class="sxs-lookup"><span data-stu-id="c7c26-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="c7c26-127">Masz zewnętrznie połączonej publiczny adres IP urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="c7c26-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="c7c26-128">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c7c26-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="c7c26-129"><a name="part1"></a>Część 1 — Konfigurowanie połączenia</span><span class="sxs-lookup"><span data-stu-id="c7c26-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="c7c26-130">W przeglądarce przejdź do witryny [Azure Portal](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c26-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c7c26-131">Kliknij przycisk **wszystkie zasoby** i Znajdź Twojej **bramy sieci wirtualnej** z listy zasobów i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="c7c26-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span></span>
3. <span data-ttu-id="c7c26-132">Na **Brama sieci wirtualnej** bloku, kliknij przycisk **połączenia**.</span><span class="sxs-lookup"><span data-stu-id="c7c26-132">On the **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="c7c26-133">![Blok połączeń](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="c7c26-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="c7c26-134">Na **połączeń** bloku, kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c7c26-134">On the **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="c7c26-135">![Dodawanie przycisku połączenia](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span><span class="sxs-lookup"><span data-stu-id="c7c26-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="c7c26-136">Na **Dodaj połączenie** bloku, wypełnij następujące pola:</span><span class="sxs-lookup"><span data-stu-id="c7c26-136">On the **Add connection** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="c7c26-137">**Nazwa:** nazwy, którego chcesz przypisać do lokacji, które tworzysz połączenie.</span><span class="sxs-lookup"><span data-stu-id="c7c26-137">**Name:** The name you want to give to the site you are creating the connection to.</span></span>
   * <span data-ttu-id="c7c26-138">**Typ połączenia:** wybierz **lokacja lokacja (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="c7c26-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="c7c26-139">![Dodawanie bloku połączenia](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span><span class="sxs-lookup"><span data-stu-id="c7c26-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="c7c26-140"><a name="part2"></a>Część 2 — Dodaj bramę sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="c7c26-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="c7c26-141">Kliknij przycisk **bramy sieci lokalnej** ***wybierz bramę sieci lokalnej***.</span><span class="sxs-lookup"><span data-stu-id="c7c26-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="c7c26-142">Spowoduje to otwarcie **wybierz bramę sieci lokalnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="c7c26-142">This will open the **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="c7c26-143">![Wybierz bramę sieci lokalnej](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span><span class="sxs-lookup"><span data-stu-id="c7c26-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="c7c26-144">Kliknij przycisk **Utwórz nowy** otworzyć **Utwórz bramę sieci lokalnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="c7c26-144">Click **Create new** to open the **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="c7c26-145">![Tworzenie bloku bramy sieci lokalnej](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span><span class="sxs-lookup"><span data-stu-id="c7c26-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="c7c26-146">Na **Utwórz bramę sieci lokalnej** bloku, wypełnij następujące pola:</span><span class="sxs-lookup"><span data-stu-id="c7c26-146">On the **Create local network gateway** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="c7c26-147">**Nazwa:** nazwa ma zostać przypisany do zasobu bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c7c26-147">**Name:** The name you want to give to the local network gateway resource.</span></span>
   * <span data-ttu-id="c7c26-148">**Adres IP:** publiczny adres IP urządzenia sieci VPN w witrynie, w której chcesz nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="c7c26-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span></span>
   * <span data-ttu-id="c7c26-149">**Przestrzeń adresowa:** przestrzeni adresowej, który ma być kierowane do nowej lokacji sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c7c26-149">**Address space:** The address space that you want to be routed to the new local network site.</span></span>
4. <span data-ttu-id="c7c26-150">Kliknij przycisk **OK** na **Utwórz bramę sieci lokalnej** bloku, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="c7c26-150">Click **OK** on the **Create local network gateway** blade to save the changes.</span></span>

## <span data-ttu-id="c7c26-151"><a name="part3"></a>Część 3 — Dodaj klucz udostępniony oraz utworzyć połączenie</span><span class="sxs-lookup"><span data-stu-id="c7c26-151"><a name="part3"></a>Part 3 - Add the shared key and create the connection</span></span>
1. <span data-ttu-id="c7c26-152">Na **Dodaj połączenie** bloku, Dodaj klucz udostępniony, który ma być używany do utworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="c7c26-152">On the **Add connection** blade, add the shared key that you want to use to create your connection.</span></span> <span data-ttu-id="c7c26-153">Można pobrać klucza wspólnego z urządzenia sieci VPN, lub wprowadź tutaj a następnie skonfiguruj urządzenia sieci VPN w celu używania klucza współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="c7c26-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span></span> <span data-ttu-id="c7c26-154">Ważne jest, że klucze są dokładnie takie same.</span><span class="sxs-lookup"><span data-stu-id="c7c26-154">The important thing is that the keys are exactly the same.</span></span>
   
    <span data-ttu-id="c7c26-155">![Klucz współużytkowany](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="c7c26-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="c7c26-156">W dolnej części bloku, kliknij przycisk **OK** do utworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="c7c26-156">At the bottom of the blade, click **OK** to create the connection.</span></span>

## <span data-ttu-id="c7c26-157"><a name="part4"></a>Część 4 - Sprawdź, czy połączenie sieci VPN</span><span class="sxs-lookup"><span data-stu-id="c7c26-157"><a name="part4"></a>Part 4 - Verify the VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c7c26-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7c26-158">Next steps</span></span>

<span data-ttu-id="c7c26-159">Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c7c26-159">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c7c26-160">Więcej informacji zawiera [ścieżka szkoleniowa](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) dotycząca maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c7c26-160">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
