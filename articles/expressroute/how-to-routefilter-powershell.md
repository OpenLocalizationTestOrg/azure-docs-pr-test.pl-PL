---
title: "Konfigurowanie filtrów trasy dla komunikacji równorzędnej platformy Azure ExpressRoute Microsoft: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak trasy tooconfigure filtrów dla Peering firmy Microsoft przy użyciu programu PowerShell"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="84dee-103">Konfigurowanie filtrów tras dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="84dee-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="84dee-104">Filtry trasy są tooconsume sposób podzbiór obsługiwane usługi za pomocą komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="84dee-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="84dee-105">Witaj czynnościach w ramach tej pomocy artykułu, konfigurowanie i zarządzanie nimi Filtry trasy dla obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="84dee-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="84dee-106">Usługi Dynamics 365 i usługi Office 365, takich jak Exchange Online, SharePoint Online i Skype dla firm, są dostępne za pośrednictwem hello komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="84dee-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="84dee-107">W przypadku skonfigurowania komunikacji równorzędnej firmy Microsoft w obwodu usługi ExpressRoute, wszystkie usługi powiązane toothese prefiksy są rozgłaszane za pośrednictwem sesji BGP hello, które są ustalane.</span><span class="sxs-lookup"><span data-stu-id="84dee-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="84dee-108">Wartość społeczności protokołu BGP jest dołączone tooevery prefiks tooidentify hello usługa, która jest dostępna za pośrednictwem hello prefiks.</span><span class="sxs-lookup"><span data-stu-id="84dee-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="84dee-109">Listę wartości społeczności BGP hello i usług hello są one wykonywane na zawiera [społeczności BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="84dee-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="84dee-110">Jeśli potrzebujesz usług łączności tooall dużej liczby prefiksów są rozgłaszane za pomocą protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="84dee-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="84dee-111">To znacznie zwiększa rozmiar hello tabel tras hello obsługiwanego przez routery w sieci.</span><span class="sxs-lookup"><span data-stu-id="84dee-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="84dee-112">Jeśli planujesz tooconsume tylko podzestaw usług oferowanymi w ramach komunikacji równorzędnej firmy Microsoft, można zmniejszyć rozmiar hello tabel tras na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="84dee-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="84dee-113">Możesz:</span><span class="sxs-lookup"><span data-stu-id="84dee-113">You can:</span></span>

- <span data-ttu-id="84dee-114">Odfiltrować niechciane prefiksy, stosując filtry tras na Wspólnot protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="84dee-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="84dee-115">To jest standardową praktyką sieci i jest powszechnie używany w wielu sieciach.</span><span class="sxs-lookup"><span data-stu-id="84dee-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="84dee-116">Zdefiniuj filtry tras i zastosować je tooyour obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="84dee-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="84dee-117">Filtr tras jest nowy zasób umożliwia wybór hello listę usług, możesz zaplanować tooconsume za pomocą komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="84dee-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="84dee-118">Usługi routerami wysłać tylko hello listę prefiksów, które należy usług toohello określonych w filtrze trasy hello.</span><span class="sxs-lookup"><span data-stu-id="84dee-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="84dee-119"><a name="about"></a>Informacje o filtrach trasy</span><span class="sxs-lookup"><span data-stu-id="84dee-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="84dee-120">W przypadku skonfigurowania komunikacji równorzędnej firmy Microsoft na obwodu ExpressRoute, routery brzegowe Microsoft hello ustanowić parę sesje BGP z routerami krawędzi hello (należy do Ciebie lub dostawcą połączenia).</span><span class="sxs-lookup"><span data-stu-id="84dee-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="84dee-121">Nie trasy są anonsowany tooyour sieci.</span><span class="sxs-lookup"><span data-stu-id="84dee-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="84dee-122">tooenable sieci tooyour anonsów tras, należy skojarzyć filtr tras.</span><span class="sxs-lookup"><span data-stu-id="84dee-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="84dee-123">Filtr tras umożliwia zidentyfikowanie usług ma tooconsume za pomocą komunikacji równorzędnej firmy Microsoft obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="84dee-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="84dee-124">Jest zasadniczo białą listę wszystkich wartości społeczności BGP hello.</span><span class="sxs-lookup"><span data-stu-id="84dee-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="84dee-125">Gdy zasób filtr trasy jest zdefiniowana i dołączyć tooan obwodu usługi expressroute, wszystkie prefiksy, które mapują toohello BGP społeczności wartości są anonsowany tooyour sieci.</span><span class="sxs-lookup"><span data-stu-id="84dee-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="84dee-126">filtry tras stanie tooattach toobe z usługami Office 365 na nich, musi mieć usługi Office 365 tooconsume autoryzacji za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="84dee-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="84dee-127">Jeśli nie jesteś autoryzowanym tooconsume usługi Office 365 usługi ExpressRoute, filtry tras tooattach operacji hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="84dee-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="84dee-128">Aby uzyskać więcej informacji na temat procesu autoryzacji hello zobacz [Azure ExpressRoute dla usługi Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="84dee-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="84dee-129">Łączność tooDynamics 365 usługi nie wymagają żadnych poprzednich autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="84dee-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84dee-130">Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane za pomocą komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy.</span><span class="sxs-lookup"><span data-stu-id="84dee-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="84dee-131">Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="84dee-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="84dee-132"><a name="workflow"></a>Przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="84dee-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="84dee-133">toobe toosuccessfully mogli łączyć się tooservices za pośrednictwem komunikacji równorzędnej firmy Microsoft, należy wykonać następujące kroki konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="84dee-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="84dee-134">Musisz mieć aktywne obwodu usługi ExpressRoute z Microsoft równorzędna elastycznie.</span><span class="sxs-lookup"><span data-stu-id="84dee-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="84dee-135">Program hello następujące instrukcje tooaccomplish te zadania:</span><span class="sxs-lookup"><span data-stu-id="84dee-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="84dee-136">[Utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="84dee-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="84dee-137">Witaj obwodu ExpressRoute musi być w stanie elastycznie i włączona.</span><span class="sxs-lookup"><span data-stu-id="84dee-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="84dee-138">[Utwórz komunikacji równorzędnej firmy Microsoft](expressroute-circuit-peerings.md) Jeśli zarządzasz hello bezpośrednio sesję protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="84dee-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="84dee-139">Lub mieć dostawcą połączenia udostępniania Microsoft komunikacji równorzędnej dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="84dee-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="84dee-140">Należy utworzyć i skonfigurować filtr trasy.</span><span class="sxs-lookup"><span data-stu-id="84dee-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="84dee-141">Zidentyfikuj hello usług tooconsume za pomocą komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="84dee-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="84dee-142">Określenie listy hello BGP wartości społeczności związanych z usługami hello</span><span class="sxs-lookup"><span data-stu-id="84dee-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="84dee-143">Utwórz regułę tooallow hello prefiks listy zgodnych hello wartości społeczności BGP</span><span class="sxs-lookup"><span data-stu-id="84dee-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="84dee-144">Należy dołączyć obwodu ExpressRoute toohello hello trasy filtru.</span><span class="sxs-lookup"><span data-stu-id="84dee-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="84dee-145">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="84dee-145">Before you begin</span></span>

<span data-ttu-id="84dee-146">Przed rozpoczęciem konfiguracji upewnij się, że spełnia hello następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="84dee-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="84dee-147">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="84dee-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="84dee-148">Aby uzyskać więcej informacji, zobacz [zainstalować i skonfigurować Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="84dee-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="84dee-149">Pobieranie hello najnowszej wersji z galerii programu PowerShell hello, zamiast hello Instalatora.</span><span class="sxs-lookup"><span data-stu-id="84dee-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="84dee-150">obecnie Hello Instalatora nie obsługuje hello wymaganych poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84dee-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="84dee-151">Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="84dee-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="84dee-152">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="84dee-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="84dee-153">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="84dee-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="84dee-154">Witaj obwodu ExpressRoute musi być w stanie elastycznie i włączona.</span><span class="sxs-lookup"><span data-stu-id="84dee-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="84dee-155">Musisz mieć aktywne komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="84dee-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="84dee-156">Postępuj zgodnie z instrukcjami w [tworzenia i modyfikowania konfiguracji komunikacji równorzędnej](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="84dee-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="84dee-157">Zaloguj się za tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="84dee-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="84dee-158">Przed rozpoczęciem tej konfiguracji, należy zalogować się tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84dee-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="84dee-159">polecenia cmdlet Hello monituje o hello poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84dee-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="84dee-160">Po zalogowaniu pobraniu ustawienia konta tak, aby były dostępne tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84dee-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="84dee-161">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień, a następnie połącz tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="84dee-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="84dee-162">Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="84dee-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="84dee-163">Jeśli masz wiele subskrypcji Azure, sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="84dee-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="84dee-164">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="84dee-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="84dee-165"><a name="prefixes"></a>Krok 1.</span><span class="sxs-lookup"><span data-stu-id="84dee-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="84dee-166">Pobierz listę prefiksów wartości społeczności BGP</span><span class="sxs-lookup"><span data-stu-id="84dee-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="84dee-167">1. Pobierz listę wartości społeczności BGP</span><span class="sxs-lookup"><span data-stu-id="84dee-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="84dee-168">Użyj następującego polecenia cmdlet tooget hello lista BGP wartości społeczności związanych z usługami dostępny za pośrednictwem komunikacji równorzędnej firmy Microsoft hello i hello listę prefiksów skojarzonych z nimi:</span><span class="sxs-lookup"><span data-stu-id="84dee-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="84dee-169">2. Tworzenie listy wartości hello, które mają toouse</span><span class="sxs-lookup"><span data-stu-id="84dee-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="84dee-170">Należy sporządzić listę BGP społeczności wartości, które mają toouse hello trasy filtru.</span><span class="sxs-lookup"><span data-stu-id="84dee-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="84dee-171">Na przykład wartość społeczności BGP dla usługi Dynamics 365 hello jest 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="84dee-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="84dee-172"><a name="filter"></a>Krok 2.</span><span class="sxs-lookup"><span data-stu-id="84dee-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="84dee-173">Utwórz filtr tras i regułę filtra</span><span class="sxs-lookup"><span data-stu-id="84dee-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="84dee-174">Filtr tras może mieć tylko jedną regułę, a zasada hello musi być typu "Zezwalaj".</span><span class="sxs-lookup"><span data-stu-id="84dee-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="84dee-175">Ta zasada może mieć listy wartości społeczności BGP skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="84dee-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="84dee-176">1. Utwórz filtr trasy</span><span class="sxs-lookup"><span data-stu-id="84dee-176">1. Create a route filter</span></span>

<span data-ttu-id="84dee-177">Najpierw należy utworzyć filtr trasy hello.</span><span class="sxs-lookup"><span data-stu-id="84dee-177">First, create hello route filter.</span></span> <span data-ttu-id="84dee-178">polecenie Hello "New-AzureRmRouteFilter" tworzy tylko zasób filtr trasy.</span><span class="sxs-lookup"><span data-stu-id="84dee-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="84dee-179">Po utworzeniu zasobu hello, należy utworzyć regułę i dołączenie go toohello trasy filtru obiektu.</span><span class="sxs-lookup"><span data-stu-id="84dee-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="84dee-180">Uruchom następujące polecenie toocreate hello zasób filtr trasy:</span><span class="sxs-lookup"><span data-stu-id="84dee-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="84dee-181">2. Utwórz regułę filtru</span><span class="sxs-lookup"><span data-stu-id="84dee-181">2. Create a filter rule</span></span>

<span data-ttu-id="84dee-182">Można określić zestaw Wspólnot protokołu BGP jako listę rozdzielaną przecinkami, jak pokazano w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="84dee-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="84dee-183">Uruchom następujące polecenie toocreate hello nową regułę:</span><span class="sxs-lookup"><span data-stu-id="84dee-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="84dee-184">3. Dodaj filtr trasy toohello reguły hello</span><span class="sxs-lookup"><span data-stu-id="84dee-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="84dee-185">Uruchom następujące polecenie tooadd hello reguły toohello trasy filtru hello:</span><span class="sxs-lookup"><span data-stu-id="84dee-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="84dee-186"><a name="attach"></a>Krok 3.</span><span class="sxs-lookup"><span data-stu-id="84dee-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="84dee-187">Dołącz obwodu ExpressRoute tooan hello trasy filtru</span><span class="sxs-lookup"><span data-stu-id="84dee-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="84dee-188">Uruchom następujące polecenie tooattach hello trasy filtru toohello obwodu usługi expressroute, przy założeniu, że masz tylko komunikacji równorzędnej firmy Microsoft hello:</span><span class="sxs-lookup"><span data-stu-id="84dee-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="84dee-189"><a name="getproperties"></a>właściwości hello tooget filtr tras</span><span class="sxs-lookup"><span data-stu-id="84dee-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="84dee-190">właściwości hello tooget filtru trasy, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="84dee-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="84dee-191">Hello uruchom następujące polecenie tooget hello trasy filtru zasobów:</span><span class="sxs-lookup"><span data-stu-id="84dee-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="84dee-192">Pobrać reguły filtrowania hello trasy dla zasobu filtru tras hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="84dee-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="84dee-193"><a name="updateproperties"></a>właściwości hello tooupdate filtr tras</span><span class="sxs-lookup"><span data-stu-id="84dee-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="84dee-194">Jeśli filtr trasy hello jest już dołączony tooa obwód, listy społeczności BGP toohello aktualizacji automatycznie propaguje zmiany anonsu prefiksu za pośrednictwem hello ustanowić sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="84dee-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="84dee-195">Można aktualizować hello BGP społeczności listy filtru trasy przy użyciu następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="84dee-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="84dee-196"><a name="detach"></a>toodetach filtr tras z obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="84dee-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="84dee-197">Gdy filtr tras jest odłączony od hello obwodu usługi expressroute, prefiksy nie są rozgłaszane za pomocą sesji protokołu BGP hello.</span><span class="sxs-lookup"><span data-stu-id="84dee-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="84dee-198">Można odłączyć filtr tras z obwodu usługi ExpressRoute, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="84dee-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="84dee-199"><a name="delete"></a>toodelete filtr tras</span><span class="sxs-lookup"><span data-stu-id="84dee-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="84dee-200">Można tylko Usuń filtr trasy, jeśli nie jest dołączony tooany obwodu.</span><span class="sxs-lookup"><span data-stu-id="84dee-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="84dee-201">Upewnij się, że filtr trasy hello nie jest dołączony obwodu tooany przed podjęciem próby wykonania toodelete go.</span><span class="sxs-lookup"><span data-stu-id="84dee-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="84dee-202">Można usunąć filtr trasy, używając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="84dee-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="84dee-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84dee-203">Next steps</span></span>

<span data-ttu-id="84dee-204">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="84dee-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
