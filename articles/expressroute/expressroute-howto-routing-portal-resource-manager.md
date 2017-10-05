---
title: "Jak skonfigurować obwód (równorzędna) dla usługi routingu: Menedżer zasobów: Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje tworzenia i inicjowania obsługi komunikacji równorzędnej prywatnej, publicznej i firmy Microsoft obwodu usługi ExpressRoute. W tym artykule opisano również, jak aktualizować i usuwać komunikację równoległą dla obwodu oraz sprawdzać jej stan."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="31567-104">Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="31567-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="31567-105">W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="31567-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="31567-106">Można również sprawdzić stan, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="31567-107">Jeśli chcesz użyć innej metody do pracy z obwodu, wybierz artykułu z poniższej listy:</span><span class="sxs-lookup"><span data-stu-id="31567-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="31567-108">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="31567-108">Configuration prerequisites</span></span>

* <span data-ttu-id="31567-109">Pamiętaj, aby przed rozpoczęciem konfiguracji przejrzeć strony z [wymaganiami wstępnymi](expressroute-prerequisites.md), [wymaganiami routingu](expressroute-routing.md) oraz [przepływami pracy](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="31567-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="31567-110">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="31567-111">Zanim przejdziesz dalej, postępuj zgodnie z instrukcjami, aby [utworzyć obwód usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md), który powinien zostać włączony przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="31567-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="31567-112">Obwód usługi expressroute musi być w stanie zainicjowane i włączone dla możesz mieć możliwość uruchamiania poleceń cmdlet w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="31567-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="31567-113">Jeśli planujesz używać udostępnionego skrótu MD5/klucz, należy użyć tej funkcji po obu stronach tunelu i ograniczyć liczbę znaków do maksymalnie 25.</span><span class="sxs-lookup"><span data-stu-id="31567-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="31567-114">Te instrukcje dotyczą tylko obwodów utworzonych przy pomocy dostawców oferujących usługi łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="31567-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="31567-115">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia konfiguruje i zarządza nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="31567-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="31567-116">Obecnie nie anonsujemy komunikacji równorzędnej skonfigurowanej przez dostawców usług w portalu zarządzania usługami.</span><span class="sxs-lookup"><span data-stu-id="31567-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="31567-117">Pracujemy nad tym, by wkrótce włączyć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="31567-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="31567-118">Skontaktuj się z dostawcą usług przed rozpoczęciem konfigurowania komunikacji równorzędnych protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="31567-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="31567-119">Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="31567-120">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="31567-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="31567-121">Musisz jednak pamiętać, aby kończyć konfiguracje poszczególnych komunikacji równorzędnych pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="31567-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="31567-122">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="31567-122">Azure private peering</span></span>

<span data-ttu-id="31567-123">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="31567-124">Aby utworzyć prywatną komunikację równorzędną</span><span class="sxs-lookup"><span data-stu-id="31567-124">To create Azure private peering</span></span>

1. <span data-ttu-id="31567-125">Skonfiguruj obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="31567-126">Zanim przejdziesz dalej, upewnij się, że obwód jest w całości obsługiwany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="31567-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![Lista](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="31567-128">Skonfiguruj prywatną komunikację równorzędną Azure dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="31567-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="31567-129">Zanim przejdziesz do następnych kroków, upewnij się, czy masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="31567-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="31567-130">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="31567-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="31567-131">Podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="31567-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="31567-132">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="31567-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="31567-133">Podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="31567-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="31567-134">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="31567-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="31567-135">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="31567-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="31567-136">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="31567-136">AS number for peering.</span></span> <span data-ttu-id="31567-137">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="31567-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="31567-138">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="31567-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="31567-139">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="31567-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="31567-140">**Opcjonalne -** skrótu MD5, jeśli chcesz użyć jednego.</span><span class="sxs-lookup"><span data-stu-id="31567-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="31567-141">Wybierz Azure prywatnej komunikacji równorzędnej wierszy, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="31567-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![Prywatne](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="31567-143">Skonfiguruj prywatną komunikację równorzędną.</span><span class="sxs-lookup"><span data-stu-id="31567-143">Configure private peering.</span></span> <span data-ttu-id="31567-144">Na poniższej ilustracji przedstawiono przykład konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="31567-144">The following image shows a configuration example:</span></span>

  ![Skonfiguruj prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="31567-146">Po określeniu wszystkich parametrów zapisz konfigurację.</span><span class="sxs-lookup"><span data-stu-id="31567-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="31567-147">Po zaakceptowaniu pomyślnie konfiguracji, zobacz podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="31567-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Zapisz prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="31567-149">Aby wyświetlić szczegóły dotyczące prywatnej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="31567-149">To view Azure private peering details</span></span>

<span data-ttu-id="31567-150">Możesz wyświetlić właściwości prywatnej komunikacji równorzędnej Azure, wybierając ją.</span><span class="sxs-lookup"><span data-stu-id="31567-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![Wyświetl prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="31567-152">Aby zaktualizować konfigurację prywatnej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="31567-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="31567-153">Można wybrać wiersz dotyczący komunikacji równorzędnej i zmodyfikować jej właściwości.</span><span class="sxs-lookup"><span data-stu-id="31567-153">You can select the row for peering and modify the peering properties.</span></span>

![Zaktualizuj prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="31567-155">Aby usunąć prywatną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="31567-155">To delete Azure private peering</span></span>

<span data-ttu-id="31567-156">Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="31567-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![usunięcie prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="31567-158">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="31567-158">Azure public peering</span></span>

<span data-ttu-id="31567-159">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie konfiguracji platformy Azure publicznej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="31567-160">Aby utworzyć publiczną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="31567-160">To create Azure public peering</span></span>

1. <span data-ttu-id="31567-161">Skonfiguruj obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="31567-162">Zanim przejdziesz dalej, upewnij się, że obwód jest w całości obsługiwany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="31567-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Lista publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="31567-164">Skonfiguruj publiczną konfigurację równorzędną Azure dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="31567-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="31567-165">Zanim przejdziesz do następnych kroków, upewnij się, czy masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="31567-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="31567-166">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="31567-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="31567-167">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="31567-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="31567-168">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="31567-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="31567-169">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="31567-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="31567-170">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="31567-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="31567-171">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="31567-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="31567-172">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="31567-172">AS number for peering.</span></span> <span data-ttu-id="31567-173">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="31567-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="31567-174">**Opcjonalne -** skrótu MD5, jeśli chcesz użyć jednego.</span><span class="sxs-lookup"><span data-stu-id="31567-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="31567-175">Wybierz Azure wiersza publicznej komunikacji równorzędnej, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="31567-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![Wybierz publicznej komunikacji równorzędnej wiersza](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="31567-177">Skonfiguruj publiczną komunikację równorzędną.</span><span class="sxs-lookup"><span data-stu-id="31567-177">Configure public peering.</span></span> <span data-ttu-id="31567-178">Na poniższej ilustracji przedstawiono przykład konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="31567-178">The following image shows a configuration example:</span></span>

  ![Skonfiguruj publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="31567-180">Po określeniu wszystkich parametrów zapisz konfigurację.</span><span class="sxs-lookup"><span data-stu-id="31567-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="31567-181">Po zaakceptowaniu pomyślnie konfiguracji, zobacz podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="31567-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Zapisz publicznej komunikacji równorzędnej konfiguracji](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="31567-183">Aby wyświetlić szczegóły dotyczące publicznej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="31567-183">To view Azure public peering details</span></span>

<span data-ttu-id="31567-184">Możesz wyświetlić właściwości publicznej komunikacji równorzędnej Azure, wybierając ją.</span><span class="sxs-lookup"><span data-stu-id="31567-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![właściwości publicznej komunikacji równorzędnej widoku](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="31567-186">Aby zaktualizować konfigurację publicznej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="31567-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="31567-187">Można wybrać wiersz dotyczący komunikacji równorzędnej i zmodyfikować jej właściwości.</span><span class="sxs-lookup"><span data-stu-id="31567-187">You can select the row for peering and modify the peering properties.</span></span>

![Wybierz publicznej komunikacji równorzędnej wiersza](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="31567-189">Aby usunąć publiczną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="31567-189">To delete Azure public peering</span></span>

<span data-ttu-id="31567-190">Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="31567-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![Usuń publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="31567-192">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="31567-192">Microsoft peering</span></span>

<span data-ttu-id="31567-193">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31567-194">Z obwody usługi ExpressRoute, które zostały skonfigurowane przed 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft ma wszystkie prefiksy usługi anonsowane przez firmę Microsoft, zaglądanie, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="31567-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="31567-195">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane do momentu filtr tras jest dołączony do obwodu.</span><span class="sxs-lookup"><span data-stu-id="31567-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="31567-196">Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="31567-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="31567-197">Aby utworzyć komunikację równorzędną Microsoft</span><span class="sxs-lookup"><span data-stu-id="31567-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="31567-198">Skonfiguruj obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31567-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="31567-199">Zanim przejdziesz dalej, upewnij się, że obwód jest w całości obsługiwany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="31567-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Lista komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="31567-201">Skonfiguruj komunikację równorzędną Microsoft dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="31567-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="31567-202">Zanim przejdziesz dalej, upewnij się, że masz poniższe informacje.</span><span class="sxs-lookup"><span data-stu-id="31567-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="31567-203">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="31567-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="31567-204">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="31567-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="31567-205">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="31567-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="31567-206">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="31567-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="31567-207">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="31567-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="31567-208">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="31567-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="31567-209">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="31567-209">AS number for peering.</span></span> <span data-ttu-id="31567-210">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="31567-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="31567-211">Anonsowane prefiksy: musisz podać listę wszystkich prefiksów, które planujesz anonsować za pośrednictwem sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="31567-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="31567-212">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="31567-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="31567-213">Jeśli planujesz wysłać zestaw prefiksy, możesz wysłać rozdzielana przecinkami lista.</span><span class="sxs-lookup"><span data-stu-id="31567-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="31567-214">Prefiksy te muszą być zarejestrowane na Ciebie w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="31567-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="31567-215">**Opcjonalne -** klienta ASN: jeśli prefiksy reklamy, które nie zostały zarejestrowane do komunikacji równorzędnej jako numer, można określić numer AS, z którym są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="31567-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="31567-216">Nazwa rejestru routingu: możesz określić RIR/IRR, względem którego rejestrowany jest numer AS i prefiksy.</span><span class="sxs-lookup"><span data-stu-id="31567-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="31567-217">**Opcjonalne -** skrótu MD5, jeśli chcesz użyć jednego.</span><span class="sxs-lookup"><span data-stu-id="31567-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="31567-218">Możesz wybrać komunikacji równorzędnej, którą chcesz skonfigurować, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="31567-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="31567-219">Zaznacz wiersz dotyczący komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31567-219">Select the Microsoft peering row.</span></span>

  ![Wybierz wiersz komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="31567-221">Skonfiguruj komunikację równorzędną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31567-221">Configure Microsoft peering.</span></span> <span data-ttu-id="31567-222">Na poniższej ilustracji przedstawiono przykład konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="31567-222">The following image shows a configuration example:</span></span>

  ![Konfigurowanie komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="31567-224">Po określeniu wszystkich parametrów zapisz konfigurację.</span><span class="sxs-lookup"><span data-stu-id="31567-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="31567-225">Jeśli obwodu pobiera do "Weryfikacji potrzebne" stan (jak pokazano w obrazie), należy otworzyć bilet pomocy technicznej, aby przedstawić dowód własności prefiksów do działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="31567-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Zapisywanie konfiguracji komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="31567-227">Możesz otworzyć bilet pomocy technicznej bezpośrednio z portalu, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="31567-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="31567-228">Po zaakceptowaniu pomyślnie konfiguracji, zobacz podobną do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="31567-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="31567-229">Aby wyświetlić szczegóły dotyczące komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="31567-229">To view Microsoft peering details</span></span>

<span data-ttu-id="31567-230">Możesz wyświetlić właściwości publicznej komunikacji równorzędnej Azure, wybierając ją.</span><span class="sxs-lookup"><span data-stu-id="31567-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="31567-231">Aby zaktualizować konfigurację komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="31567-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="31567-232">Można wybrać wiersz dotyczący komunikacji równorzędnej i zmodyfikować jej właściwości.</span><span class="sxs-lookup"><span data-stu-id="31567-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="31567-233">Aby usunąć komunikację równorzędną firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="31567-233">To delete Microsoft peering</span></span>

<span data-ttu-id="31567-234">Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="31567-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="31567-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31567-235">Next steps</span></span>

<span data-ttu-id="31567-236">Następny krok [połączyć sieć wirtualną z obwodem usługi ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="31567-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="31567-237">Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="31567-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="31567-238">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="31567-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="31567-239">Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="31567-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
