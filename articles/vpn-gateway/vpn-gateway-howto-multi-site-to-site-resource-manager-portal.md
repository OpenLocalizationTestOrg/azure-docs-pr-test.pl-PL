---
title: "Dodawanie wielu sieci VPN bramy lokacja-lokacja połączeń tooa sieci wirtualnej: Azure Portal: Resource Manager | Dokumentacja firmy Microsoft"
description: "Dodaj obejmujący wiele lokacji S2S połączeń tooa bramy sieci VPN z istniejącego połączenia"
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
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="287b5-103">Dodaj tooa połączenia lokacja-lokacja sieci wirtualnej z istniejącego połączenia bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="287b5-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="287b5-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="287b5-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="287b5-105">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="287b5-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="287b5-106">W tym artykule przedstawiono przy użyciu hello tooadd portalu Azure do lokacji (S2S) połączeń tooa bramy sieci VPN z istniejącego połączenia.</span><span class="sxs-lookup"><span data-stu-id="287b5-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="287b5-107">Ten typ połączenia jest często tooas określonej konfiguracji "obejmujący wiele lokacji".</span><span class="sxs-lookup"><span data-stu-id="287b5-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="287b5-108">Możesz dodać tooa połączenia S2S sieć wirtualną, która ma już połączenia S2S, połączenie punkt-lokacja lub połączenia do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="287b5-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="287b5-109">Podczas dodawania połączenia istnieją pewne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="287b5-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="287b5-110">Sprawdź hello [przed rozpoczęciem](#before) części tego artykułu tooverify, przed rozpoczęciem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="287b5-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="287b5-111">Ten artykuł dotyczy tooVNets utworzone przy użyciu modelu wdrażania usługi Resource Manager hello mające bramy sieci RouteBased VPN.</span><span class="sxs-lookup"><span data-stu-id="287b5-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="287b5-112">Te kroki należy stosować konfiguracje połączenia ważnych tooExpressRoute/lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="287b5-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="287b5-113">Zobacz [ważnych połączeń ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) informacji o ważnych połączenia.</span><span class="sxs-lookup"><span data-stu-id="287b5-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="287b5-114">Modele i metody wdrażania</span><span class="sxs-lookup"><span data-stu-id="287b5-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="287b5-115">Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="287b5-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="287b5-116">Artykuł jest dostępny, możemy połączyć bezpośrednio tooit z tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="287b5-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="287b5-117"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="287b5-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="287b5-118">Sprawdź hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="287b5-118">Verify hello following items:</span></span>

* <span data-ttu-id="287b5-119">Połączenie ExpressRoute/S2S coexisting nie są tworzone.</span><span class="sxs-lookup"><span data-stu-id="287b5-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="287b5-120">Masz sieci wirtualnej, który został utworzony przy użyciu modelu wdrażania usługi Resource Manager hello z istniejącego połączenia.</span><span class="sxs-lookup"><span data-stu-id="287b5-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="287b5-121">Brama sieci wirtualnej Hello sieci wirtualnej jest RouteBased.</span><span class="sxs-lookup"><span data-stu-id="287b5-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="287b5-122">Jeśli masz bramy sieci PolicyBased VPN, należy usunąć hello bramy sieci wirtualnej i Utwórz nową bramę sieci VPN jako RouteBased.</span><span class="sxs-lookup"><span data-stu-id="287b5-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="287b5-123">Nie zakresów adresów hello zachodzą na jakichkolwiek hello sieci wirtualnych, które ta sieć wirtualna nawiązuje połączenie z.</span><span class="sxs-lookup"><span data-stu-id="287b5-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="287b5-124">Masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go.</span><span class="sxs-lookup"><span data-stu-id="287b5-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="287b5-125">Zobacz artykuł [About VPN Devices](vpn-gateway-about-vpn-devices.md) (Urządzenia sieci VPN — informacje).</span><span class="sxs-lookup"><span data-stu-id="287b5-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="287b5-126">Jeśli nie znasz skonfigurowanie urządzenia sieci VPN lub masz doświadczenia w pracy z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która może zawiera te informacje dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="287b5-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="287b5-127">Masz zewnętrznie połączonej publiczny adres IP urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="287b5-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="287b5-128">Ten adres IP nie może się znajdować za translatorem adresów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="287b5-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="287b5-129"><a name="part1"></a>Część 1 — Konfigurowanie połączenia</span><span class="sxs-lookup"><span data-stu-id="287b5-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="287b5-130">W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="287b5-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="287b5-131">Kliknij przycisk **wszystkie zasoby** i Znajdź Twojej **bramy sieci wirtualnej** z listy hello zasobów i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="287b5-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="287b5-132">Na powitania **Brama sieci wirtualnej** bloku, kliknij przycisk **połączenia**.</span><span class="sxs-lookup"><span data-stu-id="287b5-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="287b5-133">![Blok połączeń](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Blok połączeń")</span><span class="sxs-lookup"><span data-stu-id="287b5-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="287b5-134">Na powitania **połączeń** bloku, kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="287b5-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="287b5-135">![Przycisk Dodaj połączenie](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "przycisku Dodaj połączenie")</span><span class="sxs-lookup"><span data-stu-id="287b5-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="287b5-136">Na powitania **Dodaj połączenie** bloku, wypełnij hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="287b5-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="287b5-137">**Nazwa:** hello nazwę lokacji toohello toogive tworzysz hello połączenie.</span><span class="sxs-lookup"><span data-stu-id="287b5-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="287b5-138">**Typ połączenia:** wybierz **lokacja lokacja (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="287b5-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="287b5-139">![Dodaj połączenie bloku](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Dodaj połączenie bloku")</span><span class="sxs-lookup"><span data-stu-id="287b5-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="287b5-140"><a name="part2"></a>Część 2 — Dodaj bramę sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="287b5-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="287b5-141">Kliknij przycisk **bramy sieci lokalnej** ***wybierz bramę sieci lokalnej***.</span><span class="sxs-lookup"><span data-stu-id="287b5-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="287b5-142">Spowoduje to otwarcie hello **wybierz bramę sieci lokalnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="287b5-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="287b5-143">![Wybierz bramę sieci lokalnej](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "wybierz bramę sieci lokalnej")</span><span class="sxs-lookup"><span data-stu-id="287b5-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="287b5-144">Kliknij przycisk **Utwórz nowy** tooopen hello **Utwórz bramę sieci lokalnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="287b5-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="287b5-145">![Bloku bramy sieci lokalnej Utwórz](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Utwórz bramę sieci lokalnej")</span><span class="sxs-lookup"><span data-stu-id="287b5-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="287b5-146">Na powitania **Utwórz bramę sieci lokalnej** bloku, wypełnij hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="287b5-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="287b5-147">**Nazwa:** hello nazwę zasobu bramy sieci lokalnej toohello toogive.</span><span class="sxs-lookup"><span data-stu-id="287b5-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="287b5-148">**Adres IP:** hello hello urządzenia sieci VPN w witrynie hello, który ma tooconnect do publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="287b5-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="287b5-149">**Przestrzeń adresowa:** hello przestrzeń adresów, które mają toobe kierowane toohello nowej lokacji sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="287b5-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="287b5-150">Kliknij przycisk **OK** na powitania **Utwórz bramę sieci lokalnej** zmiany hello toosave bloku.</span><span class="sxs-lookup"><span data-stu-id="287b5-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="287b5-151"><a name="part3"></a>Część 3 — Dodaj klucz udostępniony hello oraz tworzenie połączenia hello</span><span class="sxs-lookup"><span data-stu-id="287b5-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="287b5-152">Na powitania **Dodaj połączenie** bloku, Dodaj klucz udostępniony hello mają toouse toocreate połączenia.</span><span class="sxs-lookup"><span data-stu-id="287b5-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="287b5-153">Można albo Pobierz klucz udostępniony hello z urządzenia sieci VPN lub wprowadzić tutaj, a następnie skonfiguruj hello toouse urządzenia sieci VPN sam wspólny klucz.</span><span class="sxs-lookup"><span data-stu-id="287b5-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="287b5-154">ważne jest operacją hello klucze są dokładnie Hello hello takie same.</span><span class="sxs-lookup"><span data-stu-id="287b5-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="287b5-155">![Klucz współużytkowany](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Klucz współużytkowany")</span><span class="sxs-lookup"><span data-stu-id="287b5-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="287b5-156">U dołu hello hello bloku, kliknij przycisk **OK** toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="287b5-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="287b5-157"><a name="part4"></a>Część 4 - Sprawdź, czy hello połączenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="287b5-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="287b5-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="287b5-158">Next steps</span></span>

<span data-ttu-id="287b5-159">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="287b5-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="287b5-160">Zobacz maszyn wirtualnych hello [ścieżkę szkoleniową](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="287b5-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
