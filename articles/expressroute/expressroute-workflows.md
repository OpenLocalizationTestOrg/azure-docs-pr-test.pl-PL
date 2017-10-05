---
title: "Przepływy pracy dotyczące konfigurowania obwodu usługi ExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona przeprowadzi Cię przez przepływy pracy dotyczące konfigurowania obwodu ExpressRoute i komunikacji równorzędnych"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="71476-103">Przepływy pracy ExpressRoute dla aprowizacji obwodu i stanów obwodu</span><span class="sxs-lookup"><span data-stu-id="71476-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="71476-104">Ta strona przeprowadzi Cię przez usługę routing przepływy pracy configuration na wysokim poziomie i inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="71476-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="71476-105">Poniższa ilustracja i odpowiadające jej kroki Pokaż zadania, które należy wykonać, aby przypisać obwodu usługi ExpressRoute udostępniane na trasie.</span><span class="sxs-lookup"><span data-stu-id="71476-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="71476-106">Za pomocą programu PowerShell skonfigurować obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="71476-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="71476-107">Postępuj zgodnie z instrukcjami [obwody tworzenia usługi ExpressRoute](expressroute-howto-circuit-classic.md) artykułu, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="71476-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="71476-108">Kolejność łączność z dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="71476-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="71476-109">Ten proces może być różna.</span><span class="sxs-lookup"><span data-stu-id="71476-109">This process varies.</span></span> <span data-ttu-id="71476-110">Aby uzyskać więcej informacji o sposobie kolejność łączności, skontaktuj się z dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="71476-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="71476-111">Upewnij się, że obwód zainicjowano pomyślnie sprawdzając stan za pomocą programu PowerShell inicjowania obwód usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="71476-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="71476-112">Konfigurowanie domen routingu.</span><span class="sxs-lookup"><span data-stu-id="71476-112">Configure routing domains.</span></span> <span data-ttu-id="71476-113">Jeśli dostawca połączenia zarządza warstwy 3, firma chce skonfigurować routing dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="71476-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="71476-114">Jeśli dostawca połączenia udostępnia tylko usługi warstwy 2, należy skonfigurować routing według wskazówek opisanych w [wymagania dotyczące routingu](expressroute-routing.md) i [konfiguracji routingu](expressroute-howto-routing-classic.md) stron.</span><span class="sxs-lookup"><span data-stu-id="71476-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="71476-115">Włącz Azure prywatnej komunikacji równorzędnej — należy włączyć komunikacji równorzędnej można nawiązać połączenia z maszynami wirtualnymi / wdrożone w ramach sieci wirtualnej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="71476-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="71476-116">Włącz Azure publicznej komunikacji równorzędnej — należy włączyć publicznej komunikacji równorzędnej platformy Azure, jeśli chcesz połączyć się z usługami platformy Azure hostowanej na publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="71476-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="71476-117">Jest to wymagane, aby uzyskać dostęp do zasobów platformy Azure, jeśli chcesz włączyć routing domyślny dla platformy Azure prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="71476-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="71476-118">Włączanie komunikacji równorzędnej firmy Microsoft — należy włączyć to z dostępem do usługi Office 365 i Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="71476-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="71476-119">Należy upewnić się, że używasz oddzielnego serwera proxy / krawędzi połączenia z firmą Microsoft w niż można użyć w Internecie.</span><span class="sxs-lookup"><span data-stu-id="71476-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="71476-120">Zarówno ExpressRoute, jak i z Internetu przy użyciu tej samej granicy powoduje asymetrycznego routingu i powodować awarie łączność w sieci.</span><span class="sxs-lookup"><span data-stu-id="71476-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="71476-121">Łączenie sieci wirtualne obwody usługi ExpressRoute — sieci wirtualne można połączyć z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="71476-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="71476-122">Postępuj zgodnie z instrukcjami [połączyć sieci wirtualnych](expressroute-howto-linkvnet-arm.md) do obwodu.</span><span class="sxs-lookup"><span data-stu-id="71476-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="71476-123">Te sieci wirtualnych może być w tej samej subskrypcji platformy Azure jako obwodu ExpressRoute lub może być w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="71476-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="71476-124">Inicjowanie obsługi administracyjnej stanów obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="71476-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="71476-125">Każdy obwód usługi ExpressRoute ma dwa stany:</span><span class="sxs-lookup"><span data-stu-id="71476-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="71476-126">Stan inicjowania obsługi administracyjnej dostawcy usługi</span><span class="sxs-lookup"><span data-stu-id="71476-126">Service provider provisioning state</span></span>
* <span data-ttu-id="71476-127">Stan</span><span class="sxs-lookup"><span data-stu-id="71476-127">Status</span></span>

<span data-ttu-id="71476-128">Stan reprezentuje stan inicjowania obsługi administracyjnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="71476-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="71476-129">Ta właściwość jest ustawiony na włączone po utworzeniu obwodu usługi Expressroute</span><span class="sxs-lookup"><span data-stu-id="71476-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="71476-130">Stan inicjowania obsługi administracyjnej dostawcy łączności reprezentuje stan po stronie dostawcy łączności.</span><span class="sxs-lookup"><span data-stu-id="71476-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="71476-131">Może to być *NotProvisioned*, *inicjowania obsługi administracyjnej*, lub *obsługiwane administracyjnie*.</span><span class="sxs-lookup"><span data-stu-id="71476-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="71476-132">Obwód usługi expressroute musi być w stanie obsługiwane administracyjnie dla Ciebie można było go używać.</span><span class="sxs-lookup"><span data-stu-id="71476-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="71476-133">Możliwe stany obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="71476-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="71476-134">Ta sekcja zawiera się możliwe stany obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="71476-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="71476-135">**W czasie tworzenia**</span><span class="sxs-lookup"><span data-stu-id="71476-135">**At creation time**</span></span>

<span data-ttu-id="71476-136">Zobaczysz obwodu usługi expressroute w następującym stanie zaraz po uruchomieniu polecenia cmdlet programu PowerShell, aby utworzyć obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="71476-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="71476-137">**Gdy dostawca połączenia Trwa inicjowanie obsługi administracyjnej obwodu**</span><span class="sxs-lookup"><span data-stu-id="71476-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="71476-138">Zobaczysz obwodu usługi expressroute w następującym stanie natychmiast po klucz usługi są przekazywane do dostawcy łączności i uruchomienia procesu inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="71476-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="71476-139">**Po zakończeniu procesu udostępniania dostawcy łączności**</span><span class="sxs-lookup"><span data-stu-id="71476-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="71476-140">Zostanie wyświetlone obwodu usługi expressroute w następującym stanie, jak dostawca połączenia zostało ukończone proces inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="71476-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="71476-141">Zainicjowano obsługę administracyjną i włączone jest tylko stan obwodu może być w dla Ciebie można było go używać.</span><span class="sxs-lookup"><span data-stu-id="71476-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="71476-142">Jeśli używasz dostawcy warstwy 2, można skonfigurować routing dla obwodu tylko wtedy, gdy znajduje się w tym stanie.</span><span class="sxs-lookup"><span data-stu-id="71476-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="71476-143">**Gdy dostawca połączenia jest anulowania obsługi obwodu**</span><span class="sxs-lookup"><span data-stu-id="71476-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="71476-144">Jeśli żądanego dostawcy usług w anulowanie zastrzeżenia obwodu ExpressRoute, zostanie wyświetlony obwodu ustawioną następującym stanie po zakończeniu procesu anulowania obsługi dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="71476-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="71476-145">Można ją włączyć ponownie, jeśli potrzebne lub uruchamiania poleceń cmdlet programu PowerShell, można usunąć obwodu.</span><span class="sxs-lookup"><span data-stu-id="71476-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="71476-146">Po uruchomieniu polecenia cmdlet programu PowerShell, aby usunąć obwód podczas inicjowania obsługi administracyjnej ServiceProviderProvisioningState lub obsługiwane administracyjnie operacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="71476-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="71476-147">We współpracy z dostawcą połączenia, aby najpierw anulowanie zastrzeżenia obwodu ExpressRoute, a następnie usuń obwodu.</span><span class="sxs-lookup"><span data-stu-id="71476-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="71476-148">Firma Microsoft będzie naliczać opłaty obwód, dopóki nie zostanie uruchomione polecenie cmdlet programu PowerShell, można usunąć obwodu.</span><span class="sxs-lookup"><span data-stu-id="71476-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="71476-149">Stan konfiguracji sesji routingu</span><span class="sxs-lookup"><span data-stu-id="71476-149">Routing session configuration state</span></span>
<span data-ttu-id="71476-150">BGP stan inicjowania obsługi pozwala sprawdzić, czy włączono sesję protokołu BGP na krawędzi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="71476-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="71476-151">Stan musi być włączona dla Ciebie można było użyć komunikację równorzędną.</span><span class="sxs-lookup"><span data-stu-id="71476-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="71476-152">Należy sprawdzić stan sesji protokołu BGP, szczególnie w przypadku komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="71476-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="71476-153">Oprócz BGP stan inicjowania obsługi, istnieje inny stan, o nazwie *stanu publiczne prefiksy anonsowane*.</span><span class="sxs-lookup"><span data-stu-id="71476-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="71476-154">Stan anonsowany prefiksów publicznych musi być w *skonfigurowane* stanu, zarówno na można się sesji protokołu BGP i routingu do pracy na trasie.</span><span class="sxs-lookup"><span data-stu-id="71476-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="71476-155">Jeśli ustawiono stan anonsowany prefiks publicznego *weryfikacji potrzebne* stanu sesji BGP nie jest włączone, ponieważ anonsowane prefiksy nie odpowiada numerowi AS w żadnym z rejestrów routingu.</span><span class="sxs-lookup"><span data-stu-id="71476-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="71476-156">Jeśli stan anonsowane prefiksy publiczny jest *weryfikowanie ręczne* stanu, należy otworzyć bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) i udowodnić, że posiadanych adresów IP anonsowane wraz z programem skojarzone z nimi numery systemu autonomicznego.</span><span class="sxs-lookup"><span data-stu-id="71476-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="71476-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71476-157">Next steps</span></span>
* <span data-ttu-id="71476-158">Skonfiguruj połączenie usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="71476-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="71476-159">Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="71476-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="71476-160">Configure routing (Konfigurowanie routingu)</span><span class="sxs-lookup"><span data-stu-id="71476-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="71476-161">Link a VNet to an ExpressRoute circuit (Łączenie sieci wirtualnej z obwodem usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="71476-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

