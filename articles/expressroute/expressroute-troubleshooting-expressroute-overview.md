---
title: "Weryfikowanie łączności: ExpressRoute Azure przewodnik rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące rozwiązywania problemów i weryfikowanie łączności kompleksowe obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="29024-103">Sprawdzanie połączenia ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29024-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="29024-104">ExpressRoute, który rozciąga się sieci lokalnej do firmy Microsoft w chmurze prywatnej połączenie, które umożliwiają to dostawca połączenia, obejmuje następujące trzy strefy odrębnych sieci:</span><span class="sxs-lookup"><span data-stu-id="29024-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="29024-105">Sieci klienta</span><span class="sxs-lookup"><span data-stu-id="29024-105">Customer Network</span></span>
-   <span data-ttu-id="29024-106">Dostawcy sieci</span><span class="sxs-lookup"><span data-stu-id="29024-106">Provider Network</span></span>
-   <span data-ttu-id="29024-107">Centrum danych firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="29024-107">Microsoft Datacenter</span></span>

<span data-ttu-id="29024-108">Ten dokument ma na celu pomóc użytkownikowi ustalając, gdzie (lub nawet wtedy, gdy) występuje problem łączności i które strefie w ten sposób poszukiwania pomoc od odpowiedniego zespołu, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="29024-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="29024-109">Jeśli wymagane jest pomocy technicznej firmy Microsoft, aby rozwiązać problem, otwórz bilet pomocy technicznej z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="29024-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29024-110">Ten dokument ma na celu pomoc diagnozowania i rozwiązywania problemów proste.</span><span class="sxs-lookup"><span data-stu-id="29024-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="29024-111">Nie ma być zastępczy pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29024-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="29024-112">Otwórz bilet pomocy technicznej z [Microsoft Support] [ Support] Jeśli nie możesz rozwiązać problem przy użyciu wskazówki.</span><span class="sxs-lookup"><span data-stu-id="29024-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="29024-113">Omówienie</span><span class="sxs-lookup"><span data-stu-id="29024-113">Overview</span></span>
<span data-ttu-id="29024-114">Na poniższym diagramie przedstawiono logicznej łączność sieci klienta do sieci firmy Microsoft przy użyciu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29024-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="29024-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="29024-115">[![1]][1]</span></span>

<span data-ttu-id="29024-116">Na powyższym diagramie liczby wskazują punkty klucza sieci.</span><span class="sxs-lookup"><span data-stu-id="29024-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="29024-117">Punkty sieci odwołuje się często za pośrednictwem tego artykułu numeru skojarzone.</span><span class="sxs-lookup"><span data-stu-id="29024-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="29024-118">W zależności od modelu łączności ExpressRoute (chmury Exchange wspólnej lokalizacji, bezpośrednie połączenie sieci Ethernet lub dowolny z każdym (IPVPN)) punktów sieci, 3 i 4 może być przełączników (warstwy 2 urządzenia).</span><span class="sxs-lookup"><span data-stu-id="29024-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="29024-119">Punkty klucza sieciowego przedstawione są następujące:</span><span class="sxs-lookup"><span data-stu-id="29024-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="29024-120">Urządzenie obliczeniowe klienta (na przykład serwera lub komputera)</span><span class="sxs-lookup"><span data-stu-id="29024-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="29024-121">CEs: Routery brzegowe klienta uzyskują</span><span class="sxs-lookup"><span data-stu-id="29024-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="29024-122">PEs (skierowane do CE): Dostawca krawędzi routery czy przełączniki które stoją routery brzegowe klienta uzyskują.</span><span class="sxs-lookup"><span data-stu-id="29024-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="29024-123">Nazywane PE CEs w niniejszym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="29024-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="29024-124">PEs (MSEE połączonej): Dostawca krawędzi routery czy przełączniki które stoją MSEEs.</span><span class="sxs-lookup"><span data-stu-id="29024-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="29024-125">Nazywane PE MSEEs w niniejszym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="29024-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="29024-126">MSEEs: Routery Microsoft Edge przedsiębiorstwa (MSEE) ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29024-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="29024-127">Brama sieci wirtualnej (VNet)</span><span class="sxs-lookup"><span data-stu-id="29024-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="29024-128">Obliczenia bazy danych urządzenia w sieci wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="29024-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="29024-129">Użycie chmury Exchange wspólnej lokalizacji lub połączenia Ethernet Point-to-Point modeli łączności router brzegowy klienta (2) czy ustanowić komunikację równorzędną za MSEEs (5) Protokół BGP.</span><span class="sxs-lookup"><span data-stu-id="29024-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="29024-130">Sieci punkty 3 i 4 będzie nadal istnieje, ale nieco przejrzyste jako urządzenia warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="29024-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="29024-131">Jeśli jest używany model usługi łączności dowolny z każdym (IPVPN), PEs (skierowane do MSEE) (4) czy nawiązania komunikacji równorzędnej z MSEEs (5) Protokół BGP.</span><span class="sxs-lookup"><span data-stu-id="29024-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="29024-132">Trasy następnie będzie propagowane do sieci klienta za pośrednictwem sieci dostawcy usług IPVPN.</span><span class="sxs-lookup"><span data-stu-id="29024-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="29024-133">Wysoką dostępność usługi ExpressRoute firma Microsoft wymaga parę nadmiarowych sesje BGP między MSEEs (5) i PE-MSEEs (4).</span><span class="sxs-lookup"><span data-stu-id="29024-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="29024-134">Parę nadmiarowych ścieżek sieciowych zaleca się między sieci klienta i serwera CEs PE.</span><span class="sxs-lookup"><span data-stu-id="29024-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="29024-135">Jednak w modelu połączenia dowolny z każdym (IPVPN), może być połączone jednym urządzeniu CE (2) do co najmniej jeden PEs (3).</span><span class="sxs-lookup"><span data-stu-id="29024-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="29024-136">Aby sprawdzić poprawność obwodu usługi ExpressRoute, następujące czynności są objęte (z punktem sieci określona przez liczbę skojarzone):</span><span class="sxs-lookup"><span data-stu-id="29024-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="29024-137">Sprawdź poprawność aprowizacji obwodów i stan (5)</span><span class="sxs-lookup"><span data-stu-id="29024-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="29024-138">Sprawdzanie poprawności co najmniej jeden ExpressRoute komunikacji równorzędnej jest skonfigurowany (5)</span><span class="sxs-lookup"><span data-stu-id="29024-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="29024-139">Sprawdzanie poprawności ARP między firmą Microsoft a usługi dostawcy (łącze od 4 do 5)</span><span class="sxs-lookup"><span data-stu-id="29024-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="29024-140">Sprawdź poprawność protokołu BGP oraz tras na MSEE (BGP od 4 do 5 i 5-6 Jeśli sieci wirtualnej jest podłączona)</span><span class="sxs-lookup"><span data-stu-id="29024-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="29024-141">Sprawdź statystyki ruchu (ruchu przechodzącego przez 5)</span><span class="sxs-lookup"><span data-stu-id="29024-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="29024-142">Więcej operacji sprawdzania poprawności i kontroli zostaną dodane w przyszłości, zajrzyj tu co miesiąc!</span><span class="sxs-lookup"><span data-stu-id="29024-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="29024-143">Sprawdź poprawność aprowizacji obwodów i stanu</span><span class="sxs-lookup"><span data-stu-id="29024-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="29024-144">Niezależnie od tego modelu łączności obwodu usługi ExpressRoute musi być utworzony i w związku z tym wygenerowany klucz usługi dla aprowizacji obwodów.</span><span class="sxs-lookup"><span data-stu-id="29024-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="29024-145">Inicjowanie obsługi administracyjnej obwodu usługi ExpressRoute ustanawia nadmiarowych połączeń warstwy 2 między PE-MSEEs (4) i MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="29024-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="29024-146">Aby uzyskać więcej informacji na temat sposobu tworzenia, modyfikowania, udostępnić i sprawdzić obwodu usługi ExpressRoute, zobacz artykuł [tworzenia i modyfikowania obwodu usługi expressroute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="29024-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="29024-147">Klucz usługi unikatowo identyfikuje obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29024-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="29024-148">Ten klucz jest wymagany dla większości poleceń programu powershell wymienione w niniejszym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="29024-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="29024-149">Ponadto należy będziesz potrzebować pomocy firmy Microsoft lub partnerem ExpressRoute, aby rozwiązać problem ExpressRoute, podaj klucz usługi, aby łatwo zidentyfikować obwodu.</span><span class="sxs-lookup"><span data-stu-id="29024-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="29024-150">Weryfikacja za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="29024-150">Verification via the Azure portal</span></span>
<span data-ttu-id="29024-151">W portalu Azure można sprawdzić stan obwodu usługi ExpressRoute, wybierając ![2][2] w menu po lewej stronie paska i wybierając obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="29024-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="29024-152">Wybieranie ExpressRoute obwodu wymienione w obszarze "Wszystkie zasoby" spowoduje otwarcie bloku obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29024-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="29024-153">W ![3][3] bloku ExpressRoute essentials przedstawiono, jak pokazano na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="29024-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="29024-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="29024-154">![4][4]</span></span>    

<span data-ttu-id="29024-155">W ExpressRoute Essentials *obwodu stan* wskazuje stan obwodu po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29024-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="29024-156">*Dostawca stanu* wskazuje, czy został obwodu *obsługiwane administracyjnie nie zainicjowano obsługę administracyjną* po stronie dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="29024-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="29024-157">Dla obwodu usługi ExpressRoute działać *obwodu stan* musi być *włączone* i *stan dostawcy* musi być *obsługiwane administracyjnie*.</span><span class="sxs-lookup"><span data-stu-id="29024-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="29024-158">Jeśli *obwodu stan* jest wyłączona, skontaktuj się z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="29024-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="29024-159">Jeśli *stan dostawcy* jest nieudostępniane, skontaktuj się z dostawcą usług.</span><span class="sxs-lookup"><span data-stu-id="29024-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="29024-160">Weryfikacja za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="29024-160">Verification via PowerShell</span></span>
<span data-ttu-id="29024-161">Aby wyświetlić listę wszystkich obwody usługi ExpressRoute w grupie zasobów, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="29024-162">Nazwę grupy zasobów można uzyskać za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29024-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="29024-163">Zapoznaj się z podsekcją poprzedniej tego dokumentu i należy pamiętać, że nazwa grupy zasobów jest wymieniony w zrzut ekranu przykład.</span><span class="sxs-lookup"><span data-stu-id="29024-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="29024-164">Aby wybrać danego obwodu usługi expressroute w grupie zasobów, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="29024-165">Przykładowa odpowiedź jest:</span><span class="sxs-lookup"><span data-stu-id="29024-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="29024-166">Aby upewnić się, jeśli działa obwodu usługi ExpressRoute, zwracając szczególną uwagę na następujące pola:</span><span class="sxs-lookup"><span data-stu-id="29024-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="29024-167">Jeśli *CircuitProvisioningState* jest wyłączona, skontaktuj się z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="29024-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="29024-168">Jeśli *ServiceProviderProvisioningState* jest nieudostępniane, skontaktuj się z dostawcą usług.</span><span class="sxs-lookup"><span data-stu-id="29024-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="29024-169">Weryfikacja za pomocą programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="29024-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="29024-170">Aby wyświetlić listę wszystkich obwody usługi ExpressRoute w ramach subskrypcji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="29024-171">Aby wybrać danego obwodu ExpressRoute, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="29024-172">Przykładowa odpowiedź jest:</span><span class="sxs-lookup"><span data-stu-id="29024-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="29024-173">Aby upewnić się, jeśli działa obwodu usługi ExpressRoute, zwracając szczególną uwagę na następujące pola: ServiceProviderProvisioningState: stan elastycznie: włączone</span><span class="sxs-lookup"><span data-stu-id="29024-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="29024-174">Jeśli *stan* jest wyłączona, skontaktuj się z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="29024-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="29024-175">Jeśli *ServiceProviderProvisioningState* jest nieudostępniane, skontaktuj się z dostawcą usług.</span><span class="sxs-lookup"><span data-stu-id="29024-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="29024-176">Sprawdź poprawność konfiguracji komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="29024-176">Validate Peering Configuration</span></span>
<span data-ttu-id="29024-177">Po zakończeniu dostawcę usługi obwodu ExpressRoute inicjowania obsługi routingu konfiguracji mogą być tworzone za pośrednictwem obwodu ExpressRoute między MSEE-PRs (4) i MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="29024-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="29024-178">Każdy obwód usługi ExpressRoute może mieć jedną, dwie lub trzy konteksty routingu włączona: prywatnej komunikacji równorzędnej platformy Azure (ruch do prywatnej sieci wirtualnych na platformie Azure), publicznej komunikacji równorzędnej platformy Azure (ruch na publiczne adresy IP na platformie Azure) i komunikacji równorzędnej firmy Microsoft (ruch do usługi Office 365 i Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="29024-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="29024-179">Aby uzyskać więcej informacji na temat sposobu tworzenia i modyfikowania konfiguracji routingu, zobacz artykuł [tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="29024-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="29024-180">Weryfikacja za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="29024-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="29024-181">Jest znaną usterką w portalu Azure, w którym są komunikacji równorzędnych ExpressRoute *nie* wyświetlana w portalu, jeśli skonfigurowana przez dostawcę usług.</span><span class="sxs-lookup"><span data-stu-id="29024-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="29024-182">Dodawanie komunikacji równorzędnych ExpressRoute za pośrednictwem portalu lub programu PowerShell *zastąpienie ustawień dostawcy usługi*.</span><span class="sxs-lookup"><span data-stu-id="29024-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="29024-183">Ta akcja dzieli routingu obwodu ExpressRoute i wymaga obsługi usługodawcy do przywrócenia ustawień i ponownie ustanowić normalna routingu.</span><span class="sxs-lookup"><span data-stu-id="29024-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="29024-184">Komunikacji równorzędnych ExpressRoute należy modyfikować tylko wtedy, gdy jest pewne, czy dostawcy usług zapewnia tylko warstwy 2 usługi!</span><span class="sxs-lookup"><span data-stu-id="29024-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="29024-185">Jeśli warstwy 3 jest udostępniany przez dostawcę usług i komunikacji równorzędnych znajdują się w portalu, programu PowerShell można wyświetlić ustawienia skonfigurowanego dostawcy usługi.</span><span class="sxs-lookup"><span data-stu-id="29024-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="29024-186">W portalu Azure można sprawdzić stan obwodu usługi ExpressRoute, wybierając ![2][2] w menu po lewej stronie paska i wybierając obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="29024-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="29024-187">Wybieranie ExpressRoute obwodu wymienione w obszarze "Wszystkie zasoby" zostaną otwarte bloku obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29024-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="29024-188">W ![3][3] bloku ExpressRoute otrzyma essentials, jak pokazano na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="29024-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="29024-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="29024-189">![5][5]</span></span>

<span data-ttu-id="29024-190">W poprzednim przykładzie jako dostrzeżone Azure prywatnej komunikacji równorzędnej kontekstu routingu jest włączone, natomiast Azure publicznego i konteksty routingu komunikacji równorzędnej firmy Microsoft nie są włączone.</span><span class="sxs-lookup"><span data-stu-id="29024-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="29024-191">Pomyślnie włączono kontekstu komunikacji równorzędnej musi również podsieci podstawowego i pomocniczego point-to-point (wymagane dla protokołu BGP) na liście.</span><span class="sxs-lookup"><span data-stu-id="29024-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="29024-192">/ 30 podsieci są używane dla adresu IP interfejsu MSEEs i PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="29024-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="29024-193">Element równorzędny nie jest włączone, sprawdź, czy przypisanych podsieci podstawowego i zapasowego jest zgodna z konfiguracją na PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="29024-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="29024-194">Jeśli nie, aby zmienić konfigurację na routerach MSEE odwołują się do [tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="29024-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="29024-195">Weryfikacja za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="29024-195">Verification via PowerShell</span></span>
<span data-ttu-id="29024-196">Aby uzyskać Azure prywatnej komunikacji równorzędnej szczegółów konfiguracji, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="29024-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="29024-197">Przykładowa odpowiedź dla pomyślnie skonfigurowano prywatnej komunikacji równorzędnej, jest:</span><span class="sxs-lookup"><span data-stu-id="29024-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="29024-198">Pomyślnie włączono kontekstu komunikacji równorzędnej musi wyświetlonych prefiksów adresu podstawowego i pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="29024-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="29024-199">/ 30 podsieci są używane dla adresu IP interfejsu MSEEs i PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="29024-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="29024-200">Aby uzyskać Azure publicznej komunikacji równorzędnej szczegółów konfiguracji, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="29024-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="29024-201">Aby uzyskać szczegóły konfiguracji komunikacji równorzędnej firmy Microsoft, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="29024-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="29024-202">Jeśli nie skonfigurowano komunikacji równorzędnej, może to być komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="29024-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="29024-203">Przykładowa odpowiedź, jeśli podane komunikacji równorzędnej (Azure publicznej komunikacji równorzędnej, w tym przykładzie) nie został skonfigurowany w ramach obwodu:</span><span class="sxs-lookup"><span data-stu-id="29024-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="29024-204">Jeśli element równorzędny nie jest włączona, upewnij się, jeśli przypisanych podsieci podstawowego i zapasowego jest zgodna z konfiguracją w połączonej MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="29024-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="29024-205">Sprawdź także, czy poprawny *VlanId*, *AzureASN*, i *PeerASN* są używane na MSEEs i jeśli te wartości mapowany używane na połączonych MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="29024-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="29024-206">Jeśli wybrano opcję tworzenia skrótu MD5, udostępniony klucz powinny być takie same na pary MSEE i PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="29024-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="29024-207">Aby zmienić konfigurację na routerach MSEE, zajrzyj do [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="29024-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="29024-208">Weryfikacja za pomocą programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="29024-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="29024-209">Aby uzyskać Azure prywatnej komunikacji równorzędnej szczegółów konfiguracji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="29024-210">Przykładowa odpowiedź dla pomyślnie skonfigurowano prywatnej komunikacji równorzędnej jest:</span><span class="sxs-lookup"><span data-stu-id="29024-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="29024-211">Pomyślnie włączono A kontekstu komunikacji równorzędnej, musi na liście podsieci podstawowego i pomocniczego elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="29024-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="29024-212">/ 30 podsieci są używane dla adresu IP interfejsu MSEEs i PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="29024-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="29024-213">Aby uzyskać Azure publicznej komunikacji równorzędnej szczegółów konfiguracji, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="29024-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="29024-214">Aby uzyskać szczegóły konfiguracji komunikacji równorzędnej firmy Microsoft, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="29024-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="29024-215">Jeśli komunikacji równorzędnych warstwy 3 zostały określone przez dostawcę usług, ustawienia komunikacji równorzędnych ExpressRoute za pośrednictwem portalu lub programu PowerShell zastąpienie ustawień dostawcy usługi.</span><span class="sxs-lookup"><span data-stu-id="29024-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="29024-216">Resetowanie ustawień komunikacji równorzędnej dostawcy po stronie wymaga obsługi dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="29024-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="29024-217">Komunikacji równorzędnych ExpressRoute należy modyfikować tylko wtedy, gdy jest pewne, czy dostawcy usług zapewnia tylko warstwy 2 usługi!</span><span class="sxs-lookup"><span data-stu-id="29024-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="29024-218">Jeśli element równorzędny nie jest włączona, upewnij się, jeśli przypisanych podsieci podstawowego i pomocniczego elementu równorzędnego jest zgodna z konfiguracją w połączonej MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="29024-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="29024-219">Sprawdź także, czy poprawny *VlanId*, *AzureAsn*, i *PeerAsn* są używane na MSEEs i jeśli te wartości mapowany używane na połączonych MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="29024-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="29024-220">Aby zmienić konfigurację na routerach MSEE, zajrzyj do [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="29024-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="29024-221">Sprawdź poprawność ARP między firmy Microsoft i dostawcy usług</span><span class="sxs-lookup"><span data-stu-id="29024-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="29024-222">Ta sekcja używa poleceń programu PowerShell (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="29024-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="29024-223">Jeśli z polecenia programu PowerShell usługi Azure Resource Manager, upewnij się, że masz dostęp administratora/współadministratora do subskrypcji za pośrednictwem [klasycznego portalu Azure][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="29024-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="29024-224">Rozwiązywanie problemów przy użyciu usługi Azure Resource Manager polecenia można znaleźć na stronie [pobierania ARP tabele w modelu wdrażania usługi Resource Manager] [ ARP] dokumentu.</span><span class="sxs-lookup"><span data-stu-id="29024-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="29024-225">Aby uzyskać ARP, można użyć Azure portal i poleceń programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29024-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="29024-226">Jeśli za pomocą poleceń programu PowerShell usługi Azure Resource Manager zostaną napotkane błędy, klasycznym poleceń programu PowerShell powinna działać jako klasycznego środowiska PowerShell poleceń również współpracować z obwody usługi ExpressRoute Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="29024-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="29024-227">Można odczytać tabeli protokołu ARP routera MSEE głównej dla prywatnej komunikacji równorzędnej, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="29024-228">Oto przykład odpowiedzi dla polecenia, w tym scenariuszu powiodło się:</span><span class="sxs-lookup"><span data-stu-id="29024-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="29024-229">Podobnie można sprawdzić w tabeli protokołu ARP z MSEE w *głównej*/*dodatkowej* ścieżki dla *prywatnej*/*publiczny*  / *Microsoft* komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="29024-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="29024-230">W poniższym przykładzie przedstawiono odpowiedzi polecenia dla komunikacji równorzędnej nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="29024-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="29024-231">Jeśli w tabeli protokołu ARP nie mają adresy IP interfejsów mapowane na adresy MAC, przejrzyj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="29024-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="29024-232">Jeśli adres IP pierwszego /30 podsieci dla skojarzenia między MSEE PR i MSEE jest używany w interfejsie MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="29024-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="29024-233">Azure zawsze używa jako drugiego adresu IP dla MSEEs.</span><span class="sxs-lookup"><span data-stu-id="29024-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="29024-234">Upewnij się, jeśli klienta (C-znacznik) oraz znaczników sieci VLAN usługi (S-Tag) zgodne na pary MSEE PR i MSEE.</span><span class="sxs-lookup"><span data-stu-id="29024-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="29024-235">Sprawdź poprawność protokołu BGP oraz tras na MSEE</span><span class="sxs-lookup"><span data-stu-id="29024-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="29024-236">Ta sekcja używa poleceń programu PowerShell (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="29024-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="29024-237">Jeśli z polecenia programu PowerShell usługi Azure Resource Manager, upewnij się, że masz dostęp administratora/współadministratora do subskrypcji za pośrednictwem [klasycznego portalu Azure][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="29024-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="29024-238">Aby uzyskać informacje dotyczące protokołu BGP, można użyć Azure portal i poleceń programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29024-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="29024-239">Jeśli za pomocą poleceń programu PowerShell usługi Azure Resource Manager zostaną napotkane błędy, klasycznym poleceń programu PowerShell powinna działać jako klasycznego środowiska PowerShell poleceń również współpracować z obwody usługi ExpressRoute Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="29024-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="29024-240">Aby uzyskać podsumowanie tabeli routingu (sąsiadów BGP) dla określonego kontekstu routingu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="29024-241">Oto przykład odpowiedzi jest:</span><span class="sxs-lookup"><span data-stu-id="29024-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="29024-242">Jak pokazano w poprzednim przykładzie, polecenie jest przydatne do określenia, jak długo routingu kontekstu została ustanowiona.</span><span class="sxs-lookup"><span data-stu-id="29024-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="29024-243">Wskazuje ona także liczby prefiksów trasy anonsowane przez router komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="29024-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="29024-244">Jeśli stan jest aktywny lub bezczynności, sprawdź, czy przypisanych podsieci podstawowego i pomocniczego elementu równorzędnego jest zgodna z konfiguracją na połączonych MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="29024-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="29024-245">Sprawdź także, czy poprawny *VlanId*, *AzureAsn*, i *PeerAsn* są używane na MSEEs i jeśli te wartości mapowany używane na połączonych MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="29024-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="29024-246">Jeśli wybrano opcję tworzenia skrótu MD5, udostępniony klucz powinny być takie same na pary MSEE i PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="29024-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="29024-247">Aby zmienić konfigurację na routerach MSEE, zapoznaj się [tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="29024-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="29024-248">Jeśli niektóre miejsca docelowe są niedostępne w szczególności komunikacji równorzędnej, sprawdź tabelę tras z MSEEs należących do danego kontekstu komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="29024-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="29024-249">Jeśli zgodny prefiks (może być NATed IP) znajduje się w tabeli routingu, następnie sprawdź, czy istnieją zapór / / listy ACL grupy NSG na ścieżce i jeżeli pozwalają ruchu.</span><span class="sxs-lookup"><span data-stu-id="29024-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="29024-250">Można pobrać pełnej tabeli routingu z MSEE *głównej* ścieżki dla konkretnej *prywatnej* routingu kontekstu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="29024-251">Przykład pomyślnego wyniku dla polecenia jest:</span><span class="sxs-lookup"><span data-stu-id="29024-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="29024-252">Analogicznie, można sprawdzić tabeli routingu z MSEE w *głównej*/*dodatkowej* ścieżki dla *prywatnej* /  *Publiczny*/*Microsoft* komunikacji równorzędnej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="29024-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="29024-253">W poniższym przykładzie przedstawiono odpowiedzi polecenia dla komunikacji równorzędnej nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="29024-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="29024-254">Sprawdź statystyki ruchu</span><span class="sxs-lookup"><span data-stu-id="29024-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="29024-255">Aby uzyskać statystyki ruchu połączone ścieżki podstawowego i pomocniczego — bajtów i wylogowywanie — kontekstu komunikacji równorzędnej, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29024-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="29024-256">Przykładowe dane wyjściowe polecenia jest:</span><span class="sxs-lookup"><span data-stu-id="29024-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="29024-257">Przykładowe dane wyjściowe polecenia dla nieistniejącego komunikacji równorzędnej jest:</span><span class="sxs-lookup"><span data-stu-id="29024-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="29024-258">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29024-258">Next Steps</span></span>
<span data-ttu-id="29024-259">Aby uzyskać więcej informacji lub uzyskać pomoc zapoznaj się następujących łączy:</span><span class="sxs-lookup"><span data-stu-id="29024-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="29024-260">[Pomoc techniczna firmy Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="29024-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="29024-261">[Tworzenie i modyfikowanie obwodu usługi ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="29024-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="29024-262">[Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="29024-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="29024-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Połączenie logiczne Express Route"</span><span class="sxs-lookup"><span data-stu-id="29024-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="29024-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Wszystkie zasoby ikony"</span><span class="sxs-lookup"><span data-stu-id="29024-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="29024-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Ikona — omówienie"</span><span class="sxs-lookup"><span data-stu-id="29024-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="29024-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Zrzut ekranu przykładu ExpressRoute Essentials"</span><span class="sxs-lookup"><span data-stu-id="29024-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="29024-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Zrzut ekranu przykładu ExpressRoute Essentials"</span><span class="sxs-lookup"><span data-stu-id="29024-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






