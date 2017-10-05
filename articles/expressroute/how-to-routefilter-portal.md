---
title: "Konfigurowanie filtrów trasy dla komunikacji równorzędnej platformy Azure ExpressRoute Microsoft: Portal | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania filtrów tras dla Peering firmy Microsoft przy użyciu portalu Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: f17bf3e475a33cfc617e8a026e9606b3792101f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="336f8-103">Konfigurowanie filtrów tras dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="336f8-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="336f8-104">Filtry trasy są sposób korzystać z podzbioru obsługiwane usługi za pomocą komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="336f8-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="336f8-105">Kroki opisane w tym artykule ułatwiające konfigurowanie i Zarządzanie filtrami trasy dla obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="336f8-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="336f8-106">Usługi Dynamics 365 i usługi Office 365, takich jak Exchange Online, SharePoint Online i Skype dla firm, są dostępne za pośrednictwem komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="336f8-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="336f8-107">W przypadku skonfigurowania komunikacji równorzędnej firmy Microsoft w obwodu usługi ExpressRoute, wszystkie prefiksy związane z tych usług są rozgłaszane za pośrednictwem sesji protokołu BGP, które są ustalane.</span><span class="sxs-lookup"><span data-stu-id="336f8-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="336f8-108">Wartość społeczności protokołu BGP jest dołączony do każdego prefiksu do identyfikowania usługa, która jest dostępna za pośrednictwem prefiks.</span><span class="sxs-lookup"><span data-stu-id="336f8-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="336f8-109">Aby uzyskać listę wartości społeczności BGP i usług, są one wykonywane na, zobacz [społeczności BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="336f8-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="336f8-110">Jeśli potrzebujesz łączności z usługami wszystkich dużej liczby prefiksów są rozgłaszane za pomocą protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="336f8-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="336f8-111">To znacznie zwiększa rozmiar tabel tras obsługiwanego przez routery w sieci.</span><span class="sxs-lookup"><span data-stu-id="336f8-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="336f8-112">Jeśli planujesz używać tylko podzestaw usługami oferowanymi w ramach komunikacji równorzędnej firmy Microsoft, można zmniejszyć rozmiar tabel tras na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="336f8-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="336f8-113">Możesz:</span><span class="sxs-lookup"><span data-stu-id="336f8-113">You can:</span></span>

- <span data-ttu-id="336f8-114">Odfiltrować niechciane prefiksy, stosując filtry tras na Wspólnot protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="336f8-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="336f8-115">To jest standardową praktyką sieci i jest powszechnie używany w wielu sieciach.</span><span class="sxs-lookup"><span data-stu-id="336f8-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="336f8-116">Zdefiniuj filtry tras i zastosować je do obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="336f8-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="336f8-117">Filtr tras jest nowy zasób, który umożliwia wybranie na liście usług, której planujesz używać za pomocą komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="336f8-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="336f8-118">Usługi routerami wysłać tylko listę prefiksów, które należą do usługi określone w filtrze trasy.</span><span class="sxs-lookup"><span data-stu-id="336f8-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="336f8-119"><a name="about"></a>Informacje o filtrach trasy</span><span class="sxs-lookup"><span data-stu-id="336f8-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="336f8-120">W przypadku skonfigurowania komunikacji równorzędnej firmy Microsoft na obwodu ExpressRoute, routery brzegowe Microsoft ustanowić parę sesje BGP z routerami krawędzi (należy do Ciebie lub dostawcą połączenia).</span><span class="sxs-lookup"><span data-stu-id="336f8-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="336f8-121">Nie trasy są anonsowane do sieci.</span><span class="sxs-lookup"><span data-stu-id="336f8-121">No routes are advertised to your network.</span></span> <span data-ttu-id="336f8-122">Aby włączyć anonsów tras do sieci, należy skojarzyć filtr tras.</span><span class="sxs-lookup"><span data-stu-id="336f8-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="336f8-123">Filtr tras umożliwia zidentyfikowanie usług, które chcesz korzystać za pośrednictwem komunikacji równorzędnej firmy Microsoft obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="336f8-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="336f8-124">Jest zasadniczo białą listę wszystkich wartości społeczności protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="336f8-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="336f8-125">Gdy zasób filtru trasa jest zdefiniowana i dołączony do obwodu usługi ExpressRoute, wszystkie prefiksy mapowane na wartości społeczności BGP są rozgłaszane do sieci.</span><span class="sxs-lookup"><span data-stu-id="336f8-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="336f8-126">Aby można było dołączyć filtry tras z usługami Office 365 na nich, musi mieć autoryzację do korzystania z usług Office 365 za pomocą usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="336f8-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="336f8-127">Jeśli nie masz uprawnień do korzystania z usług Office 365 za pomocą usługi ExpressRoute, operacja dołączyć filtry tras kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="336f8-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="336f8-128">Aby uzyskać więcej informacji na temat procesu autoryzacji, zobacz [Azure ExpressRoute dla usługi Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="336f8-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="336f8-129">Łączności z usługami Dynamics 365 nie wymaga żadnych poprzednich autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="336f8-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="336f8-130">Z obwody usługi ExpressRoute, które zostały skonfigurowane przed 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft ma wszystkie prefiksy usługi anonsowane przez firmę Microsoft, zaglądanie, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="336f8-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="336f8-131">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane do momentu filtr tras jest dołączony do obwodu.</span><span class="sxs-lookup"><span data-stu-id="336f8-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="336f8-132"><a name="workflow"></a>Przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="336f8-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="336f8-133">Aby móc nawiązywać połączeń z usługami za pomocą komunikacji równorzędnej firmy Microsoft, wykonaj następujące kroki konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="336f8-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="336f8-134">Musisz mieć aktywne obwodu usługi ExpressRoute z Microsoft równorzędna elastycznie.</span><span class="sxs-lookup"><span data-stu-id="336f8-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="336f8-135">Wykonanie tych zadań, można użyć poniższych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="336f8-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="336f8-136">[Utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) i mieć obwodu włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="336f8-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="336f8-137">Obwód usługi expressroute musi być w stanie elastycznie i włączona.</span><span class="sxs-lookup"><span data-stu-id="336f8-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="336f8-138">[Utwórz komunikacji równorzędnej firmy Microsoft](expressroute-howto-routing-portal-resource-manager.md) Jeśli zarządzasz bezpośrednio za pomocą sesji protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="336f8-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="336f8-139">Lub mieć dostawcą połączenia udostępniania Microsoft komunikacji równorzędnej dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="336f8-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="336f8-140">Należy utworzyć i skonfigurować filtr trasy.</span><span class="sxs-lookup"><span data-stu-id="336f8-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="336f8-141">Identyfikowanie usług o użycie za pomocą komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="336f8-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="336f8-142">Określenie listy wartości społeczności BGP powiązanego ze wskazanymi usługami</span><span class="sxs-lookup"><span data-stu-id="336f8-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="336f8-143">Utwórz regułę w celu zezwalania na liście prefiks zgodne wartości społeczności BGP</span><span class="sxs-lookup"><span data-stu-id="336f8-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="336f8-144">Należy dołączyć filtru tras z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="336f8-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="336f8-145">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="336f8-145">Before you begin</span></span>

<span data-ttu-id="336f8-146">Przed rozpoczęciem konfiguracji upewnij się, że spełniają następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="336f8-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="336f8-147">Przegląd [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="336f8-147">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="336f8-148">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="336f8-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="336f8-149">Zanim przejdziesz dalej, postępuj zgodnie z instrukcjami, aby [utworzyć obwód usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md), który powinien zostać włączony przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="336f8-149">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="336f8-150">Obwód usługi expressroute musi być w stanie elastycznie i włączona.</span><span class="sxs-lookup"><span data-stu-id="336f8-150">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="336f8-151">Musisz mieć aktywne komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="336f8-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="336f8-152">Postępuj zgodnie z instrukcjami w [tworzenia i modyfikowania konfiguracji komunikacji równorzędnej](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="336f8-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="336f8-153"><a name="prefixes"></a>Krok 1.</span><span class="sxs-lookup"><span data-stu-id="336f8-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="336f8-154">Pobierz listę prefiksów wartości społeczności BGP</span><span class="sxs-lookup"><span data-stu-id="336f8-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="336f8-155">1. Pobierz listę wartości społeczności BGP</span><span class="sxs-lookup"><span data-stu-id="336f8-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="336f8-156">BGP wartości społeczności związanych z usługami dostępny za pośrednictwem komunikacji równorzędnej firmy Microsoft jest dostępna w [wymagania dotyczące routingu usługi ExpressRoute](expressroute-routing.md) strony.</span><span class="sxs-lookup"><span data-stu-id="336f8-156">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="336f8-157">2. Tworzenie listy wartości, które ma być używany</span><span class="sxs-lookup"><span data-stu-id="336f8-157">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="336f8-158">Tworzenie listy wartości społeczności protokołu BGP, które mają być używane w filtrze trasy.</span><span class="sxs-lookup"><span data-stu-id="336f8-158">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="336f8-159">Na przykład wartość społeczności BGP dla usługi Dynamics 365 jest 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="336f8-159">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="336f8-160"><a name="filter"></a>Krok 2.</span><span class="sxs-lookup"><span data-stu-id="336f8-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="336f8-161">Utwórz filtr tras i regułę filtra</span><span class="sxs-lookup"><span data-stu-id="336f8-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="336f8-162">Filtr tras może mieć tylko jedną regułę, a reguła musi być typu "Zezwalaj".</span><span class="sxs-lookup"><span data-stu-id="336f8-162">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="336f8-163">Ta zasada może mieć listy wartości społeczności BGP skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="336f8-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="336f8-164">1. Utwórz filtr trasy</span><span class="sxs-lookup"><span data-stu-id="336f8-164">1. Create a route filter</span></span>
<span data-ttu-id="336f8-165">Można utworzyć filtr trasy, wybierając opcję, aby utworzyć nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="336f8-165">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="336f8-166">Kliknij przycisk **nowy** > **sieci** > **RouteFilter**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="336f8-166">Click **New** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="336f8-168">Filtr trasy należy umieścić w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="336f8-168">You must place the route filter in a resource group.</span></span> 

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="336f8-170">2. Utwórz regułę filtru</span><span class="sxs-lookup"><span data-stu-id="336f8-170">2. Create a filter rule</span></span>

<span data-ttu-id="336f8-171">Można dodawać i aktualizować zasady, wybierając kartę Zarządzaj reguły filtru trasy.</span><span class="sxs-lookup"><span data-stu-id="336f8-171">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="336f8-173">Można wybrać usługi, którą chcesz nawiązać połączenie z listy rozwijanej i zapisać regułę po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="336f8-173">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="336f8-175"><a name="attach"></a>Krok 3.</span><span class="sxs-lookup"><span data-stu-id="336f8-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="336f8-176">Dołącz filtru tras z obwodem usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="336f8-176">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="336f8-177">Filtr trasy do obwodu można dołączyć, wybierając przycisk "Dodaj obwodu" i wybierając obwodu usługi expressroute z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="336f8-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="336f8-179"><a name="getproperties"></a>Aby uzyskać właściwości filtru trasy</span><span class="sxs-lookup"><span data-stu-id="336f8-179"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="336f8-180">Po otwarciu zasobu w portalu można wyświetlić właściwości filtru trasy.</span><span class="sxs-lookup"><span data-stu-id="336f8-180">You can view properties of a route filter when you open the resource in the portal.</span></span>

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="336f8-182"><a name="updateproperties"></a>Aby zaktualizować właściwości filtru tras</span><span class="sxs-lookup"><span data-stu-id="336f8-182"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="336f8-183">Można zaktualizować listy wartości społeczności BGP dołączony do obwodu, wybierając przycisk "Zarządzaj regułę".</span><span class="sxs-lookup"><span data-stu-id="336f8-183">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![Utwórz filtr trasy](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="336f8-186"><a name="detach"></a>Aby odłączyć filtr tras z obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="336f8-186"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="336f8-187">Aby odłączyć obwodu z filtru trasy, kliknij prawym przyciskiem myszy w obwodzie i kliknij "Skojarzenie".</span><span class="sxs-lookup"><span data-stu-id="336f8-187">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="336f8-189"><a name="delete"></a>Aby usunąć filtr trasy</span><span class="sxs-lookup"><span data-stu-id="336f8-189"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="336f8-190">Możesz usunąć filtr tras, wybierając przycisk Usuń.</span><span class="sxs-lookup"><span data-stu-id="336f8-190">You can delete a route filter by selecting the delete button.</span></span> 

![Utwórz filtr trasy](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="336f8-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="336f8-192">Next steps</span></span>

<span data-ttu-id="336f8-193">Więcej informacji na temat usługi ExpressRoute znajduje się w artykule [ExpressRoute FAQ](expressroute-faqs.md) (Usługa ExpressRoute — często zadawane pytania).</span><span class="sxs-lookup"><span data-stu-id="336f8-193">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>