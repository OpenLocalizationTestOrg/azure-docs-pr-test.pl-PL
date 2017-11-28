---
title: "Weryfikowanie łączności: ExpressRoute Azure przewodnik rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące rozwiązywania problemów i weryfikowanie łączności tooend zakończenia obwodu usługi ExpressRoute."
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
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="a426f-103">Sprawdzanie połączenia ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a426f-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="a426f-104">ExpressRoute, który rozciąga się sieci lokalnej na powitania firmy Microsoft w chmurze prywatnej połączenie, które umożliwiają to dostawca połączenia, obejmuje następujące trzy różne sieci strefy hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="a426f-105">Sieci klienta</span><span class="sxs-lookup"><span data-stu-id="a426f-105">Customer Network</span></span>
-   <span data-ttu-id="a426f-106">Dostawcy sieci</span><span class="sxs-lookup"><span data-stu-id="a426f-106">Provider Network</span></span>
-   <span data-ttu-id="a426f-107">Centrum danych firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="a426f-107">Microsoft Datacenter</span></span>

<span data-ttu-id="a426f-108">Witaj celem niniejszego dokumentu jest tooidentify użytkownika toohelp gdzie (lub nawet wtedy, gdy) istnieje problem z łącznością, w której strefy, co tooseek pomoże od zespołu odpowiednie tooresolve hello problemu.</span><span class="sxs-lookup"><span data-stu-id="a426f-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="a426f-109">Jeśli pomocy technicznej firmy Microsoft jest wymagana tooresolve problem, otwórz bilet pomocy technicznej z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="a426f-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a426f-110">Ten dokument jest zamierzone toohelp diagnozowania i rozwiązywania problemów proste.</span><span class="sxs-lookup"><span data-stu-id="a426f-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="a426f-111">Nie jest zamierzone toobe zastępczy pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a426f-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="a426f-112">Otwórz bilet pomocy technicznej z [Microsoft Support] [ Support] przypadku toosolve hello problem przy użyciu hello wskazówki.</span><span class="sxs-lookup"><span data-stu-id="a426f-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="a426f-113">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a426f-113">Overview</span></span>
<span data-ttu-id="a426f-114">Witaj Poniższy diagram przedstawia hello logicznej łączność sieci tooMicrosoft sieci klienta, za pomocą usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a426f-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="a426f-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="a426f-115">[![1]][1]</span></span>

<span data-ttu-id="a426f-116">W hello poprzedzających diagramu liczby hello wskazują punkty klucza sieci.</span><span class="sxs-lookup"><span data-stu-id="a426f-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="a426f-117">punkty sieci Hello odwołuje się często za pośrednictwem tego artykułu numeru skojarzone.</span><span class="sxs-lookup"><span data-stu-id="a426f-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="a426f-118">W zależności od połączenia ExpressRoute hello modelu (chmury Exchange wspólnej lokalizacji, bezpośrednie połączenie sieci Ethernet lub dowolny z każdym (IPVPN)) hello sieci punkty 3 i 4 mogą być przełączniki (warstwy 2 urządzenia).</span><span class="sxs-lookup"><span data-stu-id="a426f-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="a426f-119">punkty klucza sieciowego Hello przedstawione są następujące:</span><span class="sxs-lookup"><span data-stu-id="a426f-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="a426f-120">Urządzenie obliczeniowe klienta (na przykład serwera lub komputera)</span><span class="sxs-lookup"><span data-stu-id="a426f-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="a426f-121">CEs: Routery brzegowe klienta uzyskują</span><span class="sxs-lookup"><span data-stu-id="a426f-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="a426f-122">PEs (skierowane do CE): Dostawca krawędzi routery czy przełączniki które stoją routery brzegowe klienta uzyskują.</span><span class="sxs-lookup"><span data-stu-id="a426f-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="a426f-123">Określony tooas PE CEs w niniejszym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="a426f-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="a426f-124">PEs (MSEE połączonej): Dostawca krawędzi routery czy przełączniki które stoją MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a426f-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="a426f-125">Określony tooas PE MSEEs w niniejszym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="a426f-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="a426f-126">MSEEs: Routery Microsoft Edge przedsiębiorstwa (MSEE) ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a426f-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="a426f-127">Brama sieci wirtualnej (VNet)</span><span class="sxs-lookup"><span data-stu-id="a426f-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="a426f-128">Obliczenia bazy danych urządzenia na powitania sieci wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="a426f-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="a426f-129">Jeśli modele łączności chmury Exchange wspólnej lokalizacji lub połączenia Ethernet Point-to-Point hello są używane, router brzegowy klienta hello (2) czy ustanowić komunikację równorzędną za MSEEs (5) Protokół BGP.</span><span class="sxs-lookup"><span data-stu-id="a426f-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="a426f-130">Sieci punkty 3 i 4 będzie nadal istnieje, ale nieco przejrzyste jako urządzenia warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="a426f-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="a426f-131">Jeśli model usługi łączności dowolny z każdym (IPVPN) hello jest używany, hello PEs (skierowane do MSEE) (4) czy nawiązania komunikacji równorzędnej z MSEEs (5) Protokół BGP.</span><span class="sxs-lookup"><span data-stu-id="a426f-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="a426f-132">Tras czy rozpropagowane wstecz toohello sieci klienta za pośrednictwem sieci dostawcy usług IPVPN hello.</span><span class="sxs-lookup"><span data-stu-id="a426f-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="a426f-133">Wysoką dostępność usługi ExpressRoute firma Microsoft wymaga parę nadmiarowych sesje BGP między MSEEs (5) i PE-MSEEs (4).</span><span class="sxs-lookup"><span data-stu-id="a426f-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="a426f-134">Parę nadmiarowych ścieżek sieciowych zaleca się między sieci klienta i serwera CEs PE.</span><span class="sxs-lookup"><span data-stu-id="a426f-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="a426f-135">Jednak w model połączenia dowolny z każdym (IPVPN), pojedyncze urządzenie CE (2) może być połączone tooone lub więcej PEs (3).</span><span class="sxs-lookup"><span data-stu-id="a426f-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="a426f-136">(punktowi hello sieci określona przez liczbę hello skojarzone) obejmuje toovalidate obwodu usługi ExpressRoute, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a426f-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="a426f-137">Sprawdź poprawność aprowizacji obwodów i stan (5)</span><span class="sxs-lookup"><span data-stu-id="a426f-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="a426f-138">Sprawdzanie poprawności co najmniej jeden ExpressRoute komunikacji równorzędnej jest skonfigurowany (5)</span><span class="sxs-lookup"><span data-stu-id="a426f-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="a426f-139">Sprawdź poprawność ARP od dostawcy usług firmy Microsoft i hello (łącze od 4 do 5)</span><span class="sxs-lookup"><span data-stu-id="a426f-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="a426f-140">Sprawdź poprawność protokołu BGP oraz tras na powitania MSEE (BGP między 4 too5 i 5 too6 Jeśli sieci wirtualnej jest podłączona)</span><span class="sxs-lookup"><span data-stu-id="a426f-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="a426f-141">Sprawdź hello statystyki ruchu (ruchu przechodzącego przez 5)</span><span class="sxs-lookup"><span data-stu-id="a426f-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="a426f-142">Więcej operacji sprawdzania poprawności i kontroli zostaną dodane w hello o przyszłych, zajrzyj tu co miesiąc!</span><span class="sxs-lookup"><span data-stu-id="a426f-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="a426f-143">Sprawdź poprawność aprowizacji obwodów i stanu</span><span class="sxs-lookup"><span data-stu-id="a426f-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="a426f-144">Niezależnie od tego modelu łączności hello obwodu usługi ExpressRoute ma toobe utworzone, dlatego usługa klucz wygenerowany dla aprowizacji obwodów.</span><span class="sxs-lookup"><span data-stu-id="a426f-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="a426f-145">Inicjowanie obsługi administracyjnej obwodu usługi ExpressRoute ustanawia nadmiarowych połączeń warstwy 2 między PE-MSEEs (4) i MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="a426f-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="a426f-146">Aby uzyskać więcej informacji dotyczących sposobu toocreate, modyfikowanie, udostępnić i sprawdzić obwodu usługi ExpressRoute, zobacz artykuł hello [tworzenia i modyfikowania obwodu usługi expressroute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="a426f-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="a426f-147">Klucz usługi unikatowo identyfikuje obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a426f-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="a426f-148">Ten klucz jest wymagany dla większości poleceń programu powershell hello wymienione w niniejszym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="a426f-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="a426f-149">Ponadto, jeśli będzie potrzebna pomoc przez firmę Microsoft lub tootroubleshoot partner usługi ExpressRoute problemu ExpressRoute, dostarcza hello usługi klucza tooreadily zidentyfikować hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="a426f-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="a426f-150">Weryfikacja za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a426f-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="a426f-151">W portalu Azure hello, można sprawdzić stan hello obwodu usługi ExpressRoute, wybierając ![2][2] na powitania po lewej stronie paska menu, a następnie wybierając hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="a426f-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="a426f-152">Wybranie ExpressRoute obwodu wymienione w obszarze "Wszystkie zasoby" zostanie otwarty blok obwodu ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="a426f-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="a426f-153">W hello ![3][3] części bloku hello hello ExpressRoute essentials są wyświetlane, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="a426f-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="a426f-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="a426f-154">![4][4]</span></span>    

<span data-ttu-id="a426f-155">W hello ExpressRoute Essentials *obwodu stan* wskazuje stan hello obwodu hello na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a426f-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="a426f-156">*Dostawca stanu* wskazuje, czy został obwodu hello *obsługiwane administracyjnie nie zainicjowano obsługę administracyjną* po stronie dostawcy usług hello.</span><span class="sxs-lookup"><span data-stu-id="a426f-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="a426f-157">Dla usługi ExpressRoute obwodu toobe operacyjne, hello *obwodu stan* musi być *włączone* i hello *stan dostawcy* musi być *obsługiwane administracyjnie*.</span><span class="sxs-lookup"><span data-stu-id="a426f-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="a426f-158">Jeśli hello *obwodu stan* jest wyłączona, skontaktuj się z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="a426f-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="a426f-159">Jeśli hello *stan dostawcy* jest nieudostępniane, skontaktuj się z dostawcą usług.</span><span class="sxs-lookup"><span data-stu-id="a426f-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="a426f-160">Weryfikacja za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a426f-160">Verification via PowerShell</span></span>
<span data-ttu-id="a426f-161">toolist wszystkie hello obwody usługi ExpressRoute w grupie zasobów, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="a426f-162">Nazwę grupy zasobów można uzyskać za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a426f-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="a426f-163">Zobacz poprzednie podsekcji hello tego dokumentu i należy pamiętać, że hello nazwę grupy zasobów jest wymieniona w zrzut ekranu przedstawiający przykładowy hello.</span><span class="sxs-lookup"><span data-stu-id="a426f-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="a426f-164">tooselect danego obwodu usługi expressroute w grupie zasobów, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="a426f-165">Przykładowa odpowiedź jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-165">A sample response is:</span></span>

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

<span data-ttu-id="a426f-166">tooconfirm, jeśli działa obwodu usługi ExpressRoute, należy zwrócić szczególną uwagę toohello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="a426f-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="a426f-167">Jeśli hello *CircuitProvisioningState* jest wyłączona, skontaktuj się z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="a426f-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="a426f-168">Jeśli hello *ServiceProviderProvisioningState* jest nieudostępniane, skontaktuj się z dostawcą usług.</span><span class="sxs-lookup"><span data-stu-id="a426f-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="a426f-169">Weryfikacja za pomocą programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="a426f-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="a426f-170">toolist wszystkie hello obwody usługi ExpressRoute w ramach subskrypcji, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="a426f-171">tooselect danego obwodu ExpressRoute, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="a426f-172">Przykładowa odpowiedź jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="a426f-173">tooconfirm jeśli działa obwodu usługi ExpressRoute, należy zwrócić szczególną uwagę toohello następujące pola: ServiceProviderProvisioningState: stan elastycznie: włączone</span><span class="sxs-lookup"><span data-stu-id="a426f-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="a426f-174">Jeśli hello *stan* jest wyłączona, skontaktuj się z [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="a426f-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="a426f-175">Jeśli hello *ServiceProviderProvisioningState* jest nieudostępniane, skontaktuj się z dostawcą usług.</span><span class="sxs-lookup"><span data-stu-id="a426f-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="a426f-176">Sprawdź poprawność konfiguracji komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="a426f-176">Validate Peering Configuration</span></span>
<span data-ttu-id="a426f-177">Dostawcy usług powitania po hello ukończono aprowizacji obwodu ExpressRoute hello konfigurację routingu mogą być tworzone przez hello obwodu ExpressRoute między MSEE-PRs (4) i MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="a426f-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="a426f-178">Każdy obwód usługi ExpressRoute może mieć jedną, dwie lub trzy konteksty routingu włączona: prywatnej komunikacji równorzędnej platformy Azure (ruchu tooprivate sieci wirtualne na platformie Azure), publicznej komunikacji równorzędnej platformy Azure (ruchu toopublic adresy IP na platformie Azure) i (ruchu tooOffice 365 komunikacji równorzędnej firmy Microsoft i Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="a426f-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="a426f-179">Aby uzyskać więcej informacji na temat toocreate i modyfikować konfigurację routingu, zobacz artykuł hello [tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="a426f-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="a426f-180">Weryfikacja za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a426f-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="a426f-181">Brak znaną usterką w portalu Azure, w którym są komunikacji równorzędnych ExpressRoute hello *nie* wyświetlana w portalu hello skonfigurowanie hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="a426f-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="a426f-182">Dodawanie komunikacji równorzędnych ExpressRoute za pośrednictwem portalu hello lub programu PowerShell *zastąpienie ustawień dostawcy usługi hello*.</span><span class="sxs-lookup"><span data-stu-id="a426f-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="a426f-183">Ta akcja dzieli hello routingu na powitania obwodu ExpressRoute i wymaga obsługi hello hello usługi dostawcy toorestore hello ustawień i ponownie ustanowić normalna routingu.</span><span class="sxs-lookup"><span data-stu-id="a426f-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="a426f-184">Komunikacji równorzędnych ExpressRoute hello należy modyfikować tylko wtedy, jeśli jest pewność, że tego dostawcę usługi hello zapewnia tylko warstwy 2 usługi!</span><span class="sxs-lookup"><span data-stu-id="a426f-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="a426f-185">W przypadku warstwy 3 dostarczane przez hello komunikacji równorzędnych dostawcy i hello usługi są puste w portalu hello, programu PowerShell może być ustawienia skonfigurowanego dostawcy usługi hello toosee używane.</span><span class="sxs-lookup"><span data-stu-id="a426f-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="a426f-186">W portalu Azure hello, można sprawdzić stan obwodu usługi ExpressRoute, wybierając ![2][2] na powitania po lewej stronie paska menu, a następnie wybierając hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="a426f-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="a426f-187">Wybieranie ExpressRoute obwodu wymienione w obszarze "Wszystkie zasoby" zostaną otwarte bloku obwodu ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="a426f-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="a426f-188">W hello ![3][3] części bloku hello hello ExpressRoute otrzyma essentials, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="a426f-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="a426f-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="a426f-189">![5][5]</span></span>

<span data-ttu-id="a426f-190">W hello poprzedzających przykładzie jako dostrzeżone Azure prywatnej komunikacji równorzędnej kontekstu routingu jest włączone, natomiast Azure publicznego i konteksty routingu komunikacji równorzędnej firmy Microsoft nie są włączone.</span><span class="sxs-lookup"><span data-stu-id="a426f-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="a426f-191">Pomyślnie włączono kontekstu komunikacji równorzędnej musi również hello podsieci podstawowego i pomocniczego point-to-point (wymagane dla protokołu BGP) na liście.</span><span class="sxs-lookup"><span data-stu-id="a426f-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="a426f-192">Witaj /30 podsieci służą do adresu IP interfejsu hello hello MSEEs i PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a426f-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="a426f-193">Jeśli nie włączono komunikacji równorzędnej, sprawdź, jeśli hello podstawowych i pomocniczych podsieci przypisane zgodne konfiguracji hello na PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a426f-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="a426f-194">Jeśli nie, toochange hello konfiguracji na routerach MSEE, zapoznaj się zbyt[Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="a426f-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="a426f-195">Weryfikacja za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a426f-195">Verification via PowerShell</span></span>
<span data-ttu-id="a426f-196">tooget hello Azure prywatnej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="a426f-197">Przykładowa odpowiedź dla pomyślnie skonfigurowano prywatnej komunikacji równorzędnej, jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="a426f-198">Pomyślnie włączono kontekstu komunikacji równorzędnej musi prefiksy adresów podstawowych i pomocniczych hello na liście.</span><span class="sxs-lookup"><span data-stu-id="a426f-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="a426f-199">Witaj /30 podsieci służą do adresu IP interfejsu hello hello MSEEs i PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a426f-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="a426f-200">tooget hello Azure publicznej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="a426f-201">tooget hello Microsoft komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="a426f-202">Jeśli nie skonfigurowano komunikacji równorzędnej, może to być komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="a426f-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="a426f-203">Przykładowa odpowiedź, gdy hello wyrażony w komunikacji równorzędnej (Azure publicznej komunikacji równorzędnej, w tym przykładzie) nie jest skonfigurowany w ramach obwodu hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="a426f-204">Jeśli komunikacji równorzędnej nie jest włączona, upewnij się, hello przypisanych podsieci podstawowego i pomocniczego dopasowania hello konfiguracji na powitania połączony PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="a426f-205">Również poprawić Sprawdź, czy hello *VlanId*, *AzureASN*, i *PeerASN* są używane na MSEEs i jeśli te wartości mapuje toohello używane na powitania połączone PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="a426f-206">Jeśli wybrano opcję tworzenia skrótu MD5, klucz udostępniony hello powinny być takie same na pary MSEE i PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="a426f-207">Konfiguracja hello toochange na routerach MSEE hello, można znaleźć za [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="a426f-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="a426f-208">Weryfikacja za pomocą programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="a426f-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="a426f-209">tooget hello Azure prywatnej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a426f-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="a426f-210">Przykładowa odpowiedź dla pomyślnie skonfigurowano prywatnej komunikacji równorzędnej jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="a426f-211">Pomyślnie włączono A komunikacji równorzędnej kontekstu musi podsieci podstawowego i pomocniczego elementu równorzędnego hello wymienione.</span><span class="sxs-lookup"><span data-stu-id="a426f-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="a426f-212">Witaj /30 podsieci służą do adresu IP interfejsu hello hello MSEEs i PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a426f-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="a426f-213">tooget hello Azure publicznej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="a426f-214">tooget hello Microsoft komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="a426f-215">Jeśli komunikacji równorzędnych warstwy 3 zostały określone przez usługodawcę hello, ustawienie komunikacji równorzędnych ExpressRoute hello za pośrednictwem portalu hello lub programu PowerShell zastępuje ustawienia dostawcy usługi hello.</span><span class="sxs-lookup"><span data-stu-id="a426f-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="a426f-216">Resetowanie ustawień komunikacji równorzędnej hello dostawcy po stronie wymaga obsługi hello hello dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="a426f-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="a426f-217">Komunikacji równorzędnych ExpressRoute hello należy modyfikować tylko wtedy, jeśli jest pewność, że tego dostawcę usługi hello zapewnia tylko warstwy 2 usługi!</span><span class="sxs-lookup"><span data-stu-id="a426f-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="a426f-218">Jeśli komunikacji równorzędnej nie jest włączona, upewnij się, hello podstawowego i pomocniczego elementu równorzędnego przypisanych podsieci dopasowania hello konfiguracji na powitania połączony PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="a426f-219">Również poprawić Sprawdź, czy hello *VlanId*, *AzureAsn*, i *PeerAsn* są używane na MSEEs i jeśli te wartości mapuje toohello używane na powitania połączone PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="a426f-220">Konfiguracja hello toochange na routerach MSEE hello, można znaleźć za [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="a426f-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="a426f-221">Sprawdź poprawność ARP od dostawcy usług firmy Microsoft i hello</span><span class="sxs-lookup"><span data-stu-id="a426f-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="a426f-222">Ta sekcja używa poleceń programu PowerShell (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="a426f-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="a426f-223">Jeśli z polecenia programu PowerShell usługi Azure Resource Manager, upewnij się, że masz dostęp administratora/współadministratora subskrypcji toohello za pośrednictwem [klasycznego portalu Azure][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="a426f-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="a426f-224">Rozwiązywanie problemów przy użyciu usługi Azure Resource Manager polecenia można znaleźć w artykule toohello [pobierania ARP tabele w modelu wdrażania usługi Resource Manager hello] [ ARP] dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a426f-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="a426f-225">można tooget ARP, zarówno hello portalu Azure, jak i poleceń programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a426f-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="a426f-226">Jeśli za pomocą polecenia programu PowerShell usługi Azure Resource Manager hello zostaną napotkane błędy, klasycznym poleceń programu PowerShell powinna działać jako klasycznego środowiska PowerShell poleceń również współpracować z obwody usługi ExpressRoute Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="a426f-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="a426f-227">tooget hello tabeli protokołu ARP z hello głównej MSEE routera hello prywatnej komunikacji równorzędnej, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="a426f-228">Przykład odpowiedzi dla polecenia hello, w scenariuszu pomyślne hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="a426f-229">Analogicznie, można sprawdzić hello tabeli protokołu ARP z hello MSEE w hello *głównej*/*dodatkowej* ścieżki dla *prywatnej* /  *Publiczny*/*Microsoft* komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="a426f-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="a426f-230">Witaj poniższy przykład, że pokazuje hello odpowiedzi polecenia powitania dla komunikacji równorzędnej nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a426f-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="a426f-231">Jeśli nie ma tabeli protokołu ARP hello adresy IP interfejsów hello zamapowane tooMAC adresy, hello Przejrzyj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="a426f-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="a426f-232">Jeśli hello pierwszy adres IP podsieci hello /30 hello łącza między hello MSEE PR a MSEE jest używana w hello interfejsu MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="a426f-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="a426f-233">Azure zawsze używa hello drugiego adresu IP dla MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a426f-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="a426f-234">Upewnij się, jeśli powitania klienta (C-znacznik) i znaczniki sieci VLAN usługi (S-Tag) odpowiadają na pary MSEE PR i MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="a426f-235">Sprawdź poprawność protokołu BGP oraz tras na powitania MSEE</span><span class="sxs-lookup"><span data-stu-id="a426f-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="a426f-236">Ta sekcja używa poleceń programu PowerShell (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="a426f-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="a426f-237">Jeśli z polecenia programu PowerShell usługi Azure Resource Manager, upewnij się, że masz dostęp administratora/współadministratora subskrypcji toohello za pośrednictwem [klasycznego portalu Azure][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="a426f-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="a426f-238">tooget BGP informacje, oba hello portalu Azure i poleceń programu PowerShell usługi Azure Resource Manager może zostać użyty.</span><span class="sxs-lookup"><span data-stu-id="a426f-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="a426f-239">Jeśli za pomocą polecenia programu PowerShell usługi Azure Resource Manager hello zostaną napotkane błędy, klasycznym poleceń programu PowerShell powinna działać jako klasycznego środowiska PowerShell poleceń również współpracować z obwody usługi ExpressRoute Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="a426f-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="a426f-240">tooget hello tabeli routingu (BGP sąsiada) podsumowania dla określonego kontekstu routingu, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a426f-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="a426f-241">Oto przykład odpowiedzi jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="a426f-242">Jak przedstawiono hello poprzedzających przykład, polecenie hello jest przydatne toodetermine na jak długo została ustanowiona hello kontekstu routingu.</span><span class="sxs-lookup"><span data-stu-id="a426f-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="a426f-243">Wskazuje ona także liczby prefiksów trasy anonsowane przez router hello w komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="a426f-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="a426f-244">Jeśli hello stan jest aktywny lub bezczynności, sprawdź hello podstawowego i pomocniczego elementu równorzędnego przypisanych podsieci dopasowania hello konfiguracji na powitania połączony PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="a426f-245">Również poprawić Sprawdź, czy hello *VlanId*, *AzureAsn*, i *PeerAsn* są używane na MSEEs i jeśli te wartości mapuje toohello używane na powitania połączone PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="a426f-246">Jeśli wybrano opcję tworzenia skrótu MD5, klucz udostępniony hello powinny być takie same na pary MSEE i PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="a426f-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="a426f-247">Konfiguracja hello toochange na routerach MSEE hello, można znaleźć za[Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="a426f-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="a426f-248">Jeśli niektóre miejsca docelowe są niedostępne w szczególności komunikacji równorzędnej, sprawdź hello tabeli tras MSEEs hello należących toohello określonego kontekstu komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="a426f-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="a426f-249">Jeśli zgodny prefiks (może być NATed IP) znajduje się w tabeli routingu hello, następnie sprawdź, czy istnieją zapór / / listy ACL grupy NSG na ścieżce hello i jeżeli pozwalają hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="a426f-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="a426f-250">tooget hello pełne tabeli routingu z MSEE na powitania *głównej* ścieżki dla konkretnego hello *prywatnej* kontekstu routingu hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="a426f-251">Przykład pomyślnego wyniku dla polecenia hello jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="a426f-252">Analogicznie, można sprawdzić hello tabeli routingu z hello MSEE w hello *głównej*/*dodatkowej* ścieżki dla *prywatnej* / *Publicznych*/*Microsoft* komunikacji równorzędnej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="a426f-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="a426f-253">Witaj poniższy przykład, że pokazuje hello odpowiedzi polecenia powitania dla komunikacji równorzędnej nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="a426f-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="a426f-254">Sprawdź hello statystyki ruchu</span><span class="sxs-lookup"><span data-stu-id="a426f-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="a426f-255">tooget hello łączyć statystyki ruchu ścieżki podstawowego i pomocniczego — bajtów i wylogowywanie — kontekstu komunikacji równorzędnej, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a426f-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="a426f-256">Przykładowe dane wyjściowe polecenia hello jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="a426f-257">Przykładowe dane wyjściowe polecenia powitania dla nieistniejącego komunikacji równorzędnej jest:</span><span class="sxs-lookup"><span data-stu-id="a426f-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="a426f-258">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a426f-258">Next Steps</span></span>
<span data-ttu-id="a426f-259">Aby uzyskać więcej informacji lub uzyskać pomoc zapoznaj się hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="a426f-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="a426f-260">[Pomoc techniczna firmy Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="a426f-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="a426f-261">[Tworzenie i modyfikowanie obwodu usługi ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="a426f-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="a426f-262">[Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="a426f-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Połączenie logiczne Express Route"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Wszystkie zasoby ikony"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Ikona — omówienie"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Zrzut ekranu przykładu ExpressRoute Essentials"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Zrzut ekranu przykładu ExpressRoute Essentials"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






