---
title: "Jak tooconfigure routing (równorzędna) dla obwodu usługi ExpressRoute: Menedżer zasobów: Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej hello prywatny, publiczny oraz obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
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
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="fd91e-104">Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fd91e-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="fd91e-105">W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager hello przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fd91e-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="fd91e-106">Można również sprawdzić stan hello, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="fd91e-107">Jeśli chcesz toouse toowork inną metodę z obwodu wybierz artykułu z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="fd91e-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="fd91e-108">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fd91e-108">Configuration prerequisites</span></span>

* <span data-ttu-id="fd91e-109">Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) strony, hello [wymagania dotyczące routingu](expressroute-routing.md) strony i hello [przepływy pracy](expressroute-workflows.md) strona przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="fd91e-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="fd91e-110">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="fd91e-111">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="fd91e-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="fd91e-112">Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie poleceń cmdlet hello stanie toorun toobe w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="fd91e-113">Jeśli planujesz toouse udostępnionego skrótu MD5/klucz można toouse się, że to po obu stronach hello tunelu i limit hello liczbę znaków tooa maksymalnie 25.</span><span class="sxs-lookup"><span data-stu-id="fd91e-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="fd91e-114">Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="fd91e-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="fd91e-115">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia konfiguruje i zarządza nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fd91e-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fd91e-116">Mamy obecnie nie anonsuje skonfigurowane przez dostawców usług za pośrednictwem portalu zarządzania usługami hello komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="fd91e-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="fd91e-117">Pracujemy nad tym, by wkrótce włączyć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="fd91e-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="fd91e-118">Skontaktuj się z dostawcą usług przed rozpoczęciem konfigurowania komunikacji równorzędnych protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="fd91e-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="fd91e-119">Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="fd91e-120">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="fd91e-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="fd91e-121">Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.</span><span class="sxs-lookup"><span data-stu-id="fd91e-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="fd91e-122">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="fd91e-122">Azure private peering</span></span>

<span data-ttu-id="fd91e-123">Ta sekcja pomoże Ci tworzenie, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="fd91e-124">toocreate Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="fd91e-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="fd91e-125">Skonfiguruj hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="fd91e-126">Upewnij się, że obwód hello jest w pełni zaaprowizowanym przez dostawcę łączności hello przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="fd91e-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![Lista](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fd91e-128">Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="fd91e-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="fd91e-129">Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:</span><span class="sxs-lookup"><span data-stu-id="fd91e-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="fd91e-130">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fd91e-131">Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fd91e-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fd91e-132">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="fd91e-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fd91e-133">Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fd91e-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fd91e-134">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fd91e-135">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="fd91e-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fd91e-136">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-136">AS number for peering.</span></span> <span data-ttu-id="fd91e-137">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="fd91e-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="fd91e-138">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="fd91e-139">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="fd91e-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="fd91e-140">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="fd91e-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fd91e-141">Wybierz hello Azure prywatnej komunikacji równorzędnej wierszy, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="fd91e-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![Prywatne](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="fd91e-143">Skonfiguruj prywatną komunikację równorzędną.</span><span class="sxs-lookup"><span data-stu-id="fd91e-143">Configure private peering.</span></span> <span data-ttu-id="fd91e-144">następujące obraz powitania przedstawiono przykład konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fd91e-144">hello following image shows a configuration example:</span></span>

  ![Skonfiguruj prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="fd91e-146">Zapisz konfigurację hello, po określeniu wszystkich parametrów.</span><span class="sxs-lookup"><span data-stu-id="fd91e-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="fd91e-147">Po zaakceptowaniu pomyślnie hello konfiguracji, zostanie wyświetlony coś podobnego toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="fd91e-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Zapisz prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="fd91e-149">tooview Azure prywatnej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="fd91e-149">tooview Azure private peering details</span></span>

<span data-ttu-id="fd91e-150">Można wyświetlić właściwości hello prywatnej komunikacji równorzędnej platformy Azure, wybierając hello komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![Wyświetl prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="fd91e-152">tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fd91e-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="fd91e-153">Możesz wybrać hello wiersza dla komunikacji równorzędnej i modyfikowanie właściwości komunikacji równorzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-153">You can select hello row for peering and modify hello peering properties.</span></span>

![Zaktualizuj prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="fd91e-155">toodelete Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="fd91e-155">toodelete Azure private peering</span></span>

<span data-ttu-id="fd91e-156">Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń hello, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="fd91e-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![usunięcie prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="fd91e-158">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="fd91e-158">Azure public peering</span></span>

<span data-ttu-id="fd91e-159">Ta sekcja pomoże Ci tworzenie, pobrać, aktualizowanie i usuwanie hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="fd91e-160">toocreate Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="fd91e-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="fd91e-161">Skonfiguruj obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="fd91e-162">Upewnij się, że obwód hello jest w pełni zaaprowizowanym przez dostawcę łączności hello przed kontynuowaniem dalszych.</span><span class="sxs-lookup"><span data-stu-id="fd91e-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Lista publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fd91e-164">Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="fd91e-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="fd91e-165">Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:</span><span class="sxs-lookup"><span data-stu-id="fd91e-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="fd91e-166">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fd91e-167">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="fd91e-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fd91e-168">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="fd91e-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fd91e-169">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="fd91e-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fd91e-170">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fd91e-171">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="fd91e-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fd91e-172">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-172">AS number for peering.</span></span> <span data-ttu-id="fd91e-173">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="fd91e-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fd91e-174">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="fd91e-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fd91e-175">Wybierz hello Azure publicznej komunikacji równorzędnej wierszy, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="fd91e-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![Wybierz publicznej komunikacji równorzędnej wiersza](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="fd91e-177">Skonfiguruj publiczną komunikację równorzędną.</span><span class="sxs-lookup"><span data-stu-id="fd91e-177">Configure public peering.</span></span> <span data-ttu-id="fd91e-178">następujące obraz powitania przedstawiono przykład konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fd91e-178">hello following image shows a configuration example:</span></span>

  ![Skonfiguruj publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="fd91e-180">Zapisz konfigurację hello, po określeniu wszystkich parametrów.</span><span class="sxs-lookup"><span data-stu-id="fd91e-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="fd91e-181">Po zaakceptowaniu pomyślnie hello konfiguracji, zostanie wyświetlony coś podobnego toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="fd91e-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Zapisz publicznej komunikacji równorzędnej konfiguracji](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="fd91e-183">tooview Azure publicznej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="fd91e-183">tooview Azure public peering details</span></span>

<span data-ttu-id="fd91e-184">Można wyświetlić właściwości hello publicznej komunikacji równorzędnej platformy Azure, wybierając hello komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![właściwości publicznej komunikacji równorzędnej widoku](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="fd91e-186">tooupdate Azure publicznej konfiguracji komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="fd91e-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="fd91e-187">Możesz wybrać hello wiersza dla komunikacji równorzędnej i modyfikowanie właściwości komunikacji równorzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-187">You can select hello row for peering and modify hello peering properties.</span></span>

![Wybierz publicznej komunikacji równorzędnej wiersza](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="fd91e-189">toodelete Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="fd91e-189">toodelete Azure public peering</span></span>

<span data-ttu-id="fd91e-190">Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="fd91e-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![Usuń publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="fd91e-192">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd91e-192">Microsoft peering</span></span>

<span data-ttu-id="fd91e-193">Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd91e-194">Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane przez hello komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="fd91e-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="fd91e-195">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="fd91e-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="fd91e-196">Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fd91e-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="fd91e-197">toocreate komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd91e-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="fd91e-198">Skonfiguruj obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fd91e-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="fd91e-199">Upewnij się, że obwód hello jest w pełni zaaprowizowanym przez dostawcę łączności hello przed kontynuowaniem dalszych.</span><span class="sxs-lookup"><span data-stu-id="fd91e-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Lista komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fd91e-201">Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd91e-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="fd91e-202">Upewnij się, że masz hello następujących informacji, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="fd91e-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="fd91e-203">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fd91e-204">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="fd91e-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fd91e-205">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="fd91e-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fd91e-206">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="fd91e-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fd91e-207">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fd91e-208">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="fd91e-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fd91e-209">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-209">AS number for peering.</span></span> <span data-ttu-id="fd91e-210">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="fd91e-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fd91e-211">Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="fd91e-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="fd91e-212">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="fd91e-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="fd91e-213">Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listę rozdzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="fd91e-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="fd91e-214">Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="fd91e-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="fd91e-215">**Opcjonalne -** klienta ASN: w przypadku prefiksów reklamy, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer hello można określić jako numer toowhich są zarejestrowani.</span><span class="sxs-lookup"><span data-stu-id="fd91e-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="fd91e-216">Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="fd91e-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="fd91e-217">**Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="fd91e-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fd91e-218">Możesz wybrać hello równorzędna ma tooconfigure, jak pokazano w hello następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="fd91e-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="fd91e-219">Wybierz wiersz komunikacji równorzędnej firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-219">Select hello Microsoft peering row.</span></span>

  ![Wybierz wiersz komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="fd91e-221">Skonfiguruj komunikację równorzędną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd91e-221">Configure Microsoft peering.</span></span> <span data-ttu-id="fd91e-222">następujące obraz powitania przedstawiono przykład konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fd91e-222">hello following image shows a configuration example:</span></span>

  ![Konfigurowanie komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="fd91e-224">Zapisz konfigurację hello, po określeniu wszystkich parametrów.</span><span class="sxs-lookup"><span data-stu-id="fd91e-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="fd91e-225">Jeśli obwodu pobiera tooa potrzebne weryfikacji stanu (jak pokazano w obrazie hello), należy otworzyć tooshow biletu pomocy technicznej dowód własności hello prefiksy tooour z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="fd91e-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Zapisywanie konfiguracji komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="fd91e-227">Jak pokazano w hello poniższy przykład, można otworzyć bilet pomocy technicznej bezpośrednio z portalu hello:</span><span class="sxs-lookup"><span data-stu-id="fd91e-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="fd91e-228">Po zaakceptowaniu pomyślnie hello konfiguracji, zostanie wyświetlony coś podobnego toohello po obrazu:</span><span class="sxs-lookup"><span data-stu-id="fd91e-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="fd91e-229">Szczegóły komunikacji równorzędnej tooview firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd91e-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="fd91e-230">Można wyświetlić właściwości hello publicznej komunikacji równorzędnej platformy Azure, wybierając hello komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fd91e-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="fd91e-231">konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd91e-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="fd91e-232">Możesz wybrać hello wiersza dla komunikacji równorzędnej i modyfikowanie właściwości komunikacji równorzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="fd91e-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="fd91e-233">toodelete komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd91e-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="fd91e-234">Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń hello, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="fd91e-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="fd91e-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd91e-235">Next steps</span></span>

<span data-ttu-id="fd91e-236">Następny krok [połączyć sieć wirtualną tooan obwodu usługi expressroute](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="fd91e-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="fd91e-237">Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="fd91e-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="fd91e-238">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="fd91e-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="fd91e-239">Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="fd91e-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
