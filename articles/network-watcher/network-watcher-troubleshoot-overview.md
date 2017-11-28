---
title: "Rozwiązywanie problemów w obserwatora sieciowego Azure tooresource aaaIntroduction | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie funkcji hello obserwatora sieciowego zasobów rozwiązywania problemów"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="10d5b-103">Rozwiązywanie problemów w obserwatora sieciowego Azure tooresource wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="10d5b-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="10d5b-104">Bramy sieci wirtualnej zapewniają łączność między zasobami lokalnymi i innych sieci wirtualnych w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10d5b-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="10d5b-105">Bardzo ważne jest monitorowanie ich połączeń i te bram tooensuring komunikacja nie jest uszkodzona.</span><span class="sxs-lookup"><span data-stu-id="10d5b-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="10d5b-106">Obserwatora sieciowego zapewnia hello tootroubleshoot możliwości połączenia i bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10d5b-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="10d5b-107">Można go wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="10d5b-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="10d5b-108">Po wywołaniu obserwatora sieciowego diagnozuje hello kondycji bramy sieci wirtualnej hello lub połączenia i zwracany hello odpowiednie wyniki.</span><span class="sxs-lookup"><span data-stu-id="10d5b-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="10d5b-109">To żądanie jest długo działającą transakcję, hello są zwracane po zakończeniu hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="10d5b-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="10d5b-111">Wyniki</span><span class="sxs-lookup"><span data-stu-id="10d5b-111">Results</span></span>

<span data-ttu-id="10d5b-112">Witaj wstępne wyniki zwracane nadaj ogólny obraz kondycji hello hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="10d5b-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="10d5b-113">Więcej informacji można podać dla zasobów pokazane na powitania następujących sekcji:</span><span class="sxs-lookup"><span data-stu-id="10d5b-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="10d5b-114">Witaj poniżej znajduje się hello wartości zwracane z hello Rozwiązywanie problemów z interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="10d5b-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="10d5b-115">**wartość startTime** — ta wartość jest czas hello hello Rozwiązywanie problemów z wywołania interfejsu API uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="10d5b-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="10d5b-116">**wartość endTime** — ta wartość jest hello czas zakończenia hello rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="10d5b-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="10d5b-117">**Kod** — ta wartość jest zła, w przypadku awarii jednego diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="10d5b-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="10d5b-118">**wyniki** -wyników jest zbiór wyników zwróconych na powitania połączenie lub hello bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10d5b-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="10d5b-119">**Identyfikator** — ta wartość jest typem błędu hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="10d5b-120">**Podsumowanie** — ta wartość jest podsumowanie hello błędów.</span><span class="sxs-lookup"><span data-stu-id="10d5b-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="10d5b-121">**szczegółowe** -wartość zawiera szczegółowy opis błędu hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="10d5b-122">**recommendedActions** — ta właściwość jest kolekcją tootake zalecane działania.</span><span class="sxs-lookup"><span data-stu-id="10d5b-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="10d5b-123">**actionText** — ta wartość zawiera hello tekst opisujący jakie tootake akcji.</span><span class="sxs-lookup"><span data-stu-id="10d5b-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="10d5b-124">**actionUri** — ta wartość zawiera hello URI toodocumentation tooact.</span><span class="sxs-lookup"><span data-stu-id="10d5b-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="10d5b-125">**actionUriText** — ta wartość jest krótki opis hello akcji tekstu.</span><span class="sxs-lookup"><span data-stu-id="10d5b-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="10d5b-126">Hello następujące tabele Pokaż hello błędów różne typy (identyfikator w obszarze wyniki z powyższej listy hello) dostępnych i jeśli błędów hello tworzy dzienniki.</span><span class="sxs-lookup"><span data-stu-id="10d5b-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="10d5b-127">Brama</span><span class="sxs-lookup"><span data-stu-id="10d5b-127">Gateway</span></span>

| <span data-ttu-id="10d5b-128">Typ błędu</span><span class="sxs-lookup"><span data-stu-id="10d5b-128">Fault Type</span></span> | <span data-ttu-id="10d5b-129">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="10d5b-129">Reason</span></span> | <span data-ttu-id="10d5b-130">Log</span><span class="sxs-lookup"><span data-stu-id="10d5b-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="10d5b-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="10d5b-131">NoFault</span></span> | <span data-ttu-id="10d5b-132">Gdy błąd nie została wykryta.</span><span class="sxs-lookup"><span data-stu-id="10d5b-132">When no error is detected.</span></span> |<span data-ttu-id="10d5b-133">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-133">Yes</span></span>|
| <span data-ttu-id="10d5b-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="10d5b-134">GatewayNotFound</span></span> | <span data-ttu-id="10d5b-135">Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie.</span><span class="sxs-lookup"><span data-stu-id="10d5b-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="10d5b-136">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-136">No</span></span>|
| <span data-ttu-id="10d5b-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="10d5b-137">PlannedMaintenance</span></span> |  <span data-ttu-id="10d5b-138">Wystąpienie bramy jest w trakcie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="10d5b-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="10d5b-139">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-139">No</span></span>|
| <span data-ttu-id="10d5b-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="10d5b-140">UserDrivenUpdate</span></span> | <span data-ttu-id="10d5b-141">Gdy aktualizacja użytkownika jest w toku.</span><span class="sxs-lookup"><span data-stu-id="10d5b-141">When a user update is in progress.</span></span> <span data-ttu-id="10d5b-142">Może to być operacji zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="10d5b-142">This could be a resize operation.</span></span> | <span data-ttu-id="10d5b-143">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-143">No</span></span> |
| <span data-ttu-id="10d5b-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="10d5b-144">VipUnResponsive</span></span> | <span data-ttu-id="10d5b-145">Nie można osiągnąć hello głównej wystąpienie hello bramy.</span><span class="sxs-lookup"><span data-stu-id="10d5b-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="10d5b-146">Dzieje się tak, gdy hello badania kondycji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="10d5b-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="10d5b-147">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-147">No</span></span> |
| <span data-ttu-id="10d5b-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="10d5b-148">PlatformInActive</span></span> | <span data-ttu-id="10d5b-149">Istnieje problem z platformą hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="10d5b-150">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-150">No</span></span>|
| <span data-ttu-id="10d5b-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="10d5b-151">ServiceNotRunning</span></span> | <span data-ttu-id="10d5b-152">Usługa podstawowej Hello nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="10d5b-152">hello underlying service is not running.</span></span> | <span data-ttu-id="10d5b-153">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-153">No</span></span>|
| <span data-ttu-id="10d5b-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="10d5b-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="10d5b-155">Połączenia nie istnieje w bramie hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="10d5b-156">Jest to tylko ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="10d5b-156">This is only a warning.</span></span>| <span data-ttu-id="10d5b-157">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-157">No</span></span>|
| <span data-ttu-id="10d5b-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="10d5b-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="10d5b-159">Połączenia nie są połączone.</span><span class="sxs-lookup"><span data-stu-id="10d5b-159">Connections are not connected.</span></span> <span data-ttu-id="10d5b-160">Jest to tylko ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="10d5b-160">This is only a warning.</span></span>| <span data-ttu-id="10d5b-161">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-161">Yes</span></span>|
| <span data-ttu-id="10d5b-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="10d5b-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="10d5b-163">Bieżące użycie procesora CPU bramy Hello jest > 95%.</span><span class="sxs-lookup"><span data-stu-id="10d5b-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="10d5b-164">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="10d5b-165">Połączenie</span><span class="sxs-lookup"><span data-stu-id="10d5b-165">Connection</span></span>

| <span data-ttu-id="10d5b-166">Typ błędu</span><span class="sxs-lookup"><span data-stu-id="10d5b-166">Fault Type</span></span> | <span data-ttu-id="10d5b-167">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="10d5b-167">Reason</span></span> | <span data-ttu-id="10d5b-168">Log</span><span class="sxs-lookup"><span data-stu-id="10d5b-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="10d5b-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="10d5b-169">NoFault</span></span> | <span data-ttu-id="10d5b-170">Gdy błąd nie została wykryta.</span><span class="sxs-lookup"><span data-stu-id="10d5b-170">When no error is detected.</span></span> |<span data-ttu-id="10d5b-171">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-171">Yes</span></span>|
| <span data-ttu-id="10d5b-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="10d5b-172">GatewayNotFound</span></span> | <span data-ttu-id="10d5b-173">Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie.</span><span class="sxs-lookup"><span data-stu-id="10d5b-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="10d5b-174">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-174">No</span></span>|
| <span data-ttu-id="10d5b-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="10d5b-175">PlannedMaintenance</span></span> | <span data-ttu-id="10d5b-176">Wystąpienie bramy jest w trakcie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="10d5b-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="10d5b-177">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-177">No</span></span>|
| <span data-ttu-id="10d5b-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="10d5b-178">UserDrivenUpdate</span></span> | <span data-ttu-id="10d5b-179">Gdy aktualizacja użytkownika jest w toku.</span><span class="sxs-lookup"><span data-stu-id="10d5b-179">When a user update is in progress.</span></span> <span data-ttu-id="10d5b-180">Może to być operacji zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="10d5b-180">This could be a resize operation.</span></span>  | <span data-ttu-id="10d5b-181">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-181">No</span></span> |
| <span data-ttu-id="10d5b-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="10d5b-182">VipUnResponsive</span></span> | <span data-ttu-id="10d5b-183">Nie można osiągnąć hello głównej wystąpienie hello bramy.</span><span class="sxs-lookup"><span data-stu-id="10d5b-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="10d5b-184">Zdarza się, gdy hello badania kondycji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="10d5b-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="10d5b-185">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-185">No</span></span> |
| <span data-ttu-id="10d5b-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="10d5b-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="10d5b-187">Brak konfiguracji połączenia.</span><span class="sxs-lookup"><span data-stu-id="10d5b-187">Connection configuration is missing.</span></span> | <span data-ttu-id="10d5b-188">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-188">No</span></span> |
| <span data-ttu-id="10d5b-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="10d5b-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="10d5b-190">Witaj połączenia jest oznaczony jako "odłączony".</span><span class="sxs-lookup"><span data-stu-id="10d5b-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="10d5b-191">Nie</span><span class="sxs-lookup"><span data-stu-id="10d5b-191">No</span></span>|
| <span data-ttu-id="10d5b-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="10d5b-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="10d5b-193">Witaj podległej usłudze nie ma powitalne skonfigurowane połączenie.</span><span class="sxs-lookup"><span data-stu-id="10d5b-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="10d5b-194">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-194">Yes</span></span> |
| <span data-ttu-id="10d5b-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="10d5b-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="10d5b-196">źródłowa usługa Hello jest oznaczona jako stan wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="10d5b-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="10d5b-197">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-197">Yes</span></span>|
| <span data-ttu-id="10d5b-198">Authentication</span><span class="sxs-lookup"><span data-stu-id="10d5b-198">Authentication</span></span> | <span data-ttu-id="10d5b-199">Niezgodność klucz wstępny.</span><span class="sxs-lookup"><span data-stu-id="10d5b-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="10d5b-200">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-200">Yes</span></span>|
| <span data-ttu-id="10d5b-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="10d5b-201">PeerReachability</span></span> | <span data-ttu-id="10d5b-202">Brama równorzędnej Hello jest nieosiągalny.</span><span class="sxs-lookup"><span data-stu-id="10d5b-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="10d5b-203">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-203">Yes</span></span>|
| <span data-ttu-id="10d5b-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="10d5b-204">IkePolicyMismatch</span></span> | <span data-ttu-id="10d5b-205">Brama równorzędnej Hello ma zasady IKE, które nie są obsługiwane przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="10d5b-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="10d5b-206">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-206">Yes</span></span>|
| <span data-ttu-id="10d5b-207">Błąd WfpParse</span><span class="sxs-lookup"><span data-stu-id="10d5b-207">WfpParse Error</span></span> | <span data-ttu-id="10d5b-208">Wystąpił błąd podczas analizowania dziennika platformy filtrowania systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="10d5b-209">Tak</span><span class="sxs-lookup"><span data-stu-id="10d5b-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="10d5b-210">Obsługiwane typy bramy</span><span class="sxs-lookup"><span data-stu-id="10d5b-210">Supported Gateway types</span></span>

<span data-ttu-id="10d5b-211">Witaj Poniższa lista zawiera obsługę hello Pokazuje połączenia i bram, które są obsługiwane w rozwiązywaniu problemów obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="10d5b-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="10d5b-212">**Typy bramy**</span><span class="sxs-lookup"><span data-stu-id="10d5b-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="10d5b-213">Sieć VPN</span><span class="sxs-lookup"><span data-stu-id="10d5b-213">VPN</span></span>      | <span data-ttu-id="10d5b-214">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-214">Supported</span></span>        |
|<span data-ttu-id="10d5b-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="10d5b-215">ExpressRoute</span></span> | <span data-ttu-id="10d5b-216">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-216">Not Supported</span></span> |
|<span data-ttu-id="10d5b-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="10d5b-217">Hypernet</span></span> | <span data-ttu-id="10d5b-218">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-218">Not Supported</span></span>|
|<span data-ttu-id="10d5b-219">**Typy z siecią VPN**</span><span class="sxs-lookup"><span data-stu-id="10d5b-219">**VPN types**</span></span> | |
|<span data-ttu-id="10d5b-220">Na podstawie trasy</span><span class="sxs-lookup"><span data-stu-id="10d5b-220">Route Based</span></span> | <span data-ttu-id="10d5b-221">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-221">Supported</span></span>|
|<span data-ttu-id="10d5b-222">Na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="10d5b-222">Policy Based</span></span> | <span data-ttu-id="10d5b-223">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-223">Not Supported</span></span>|
|<span data-ttu-id="10d5b-224">**Typy połączeń**</span><span class="sxs-lookup"><span data-stu-id="10d5b-224">**Connection types**</span></span>||
|<span data-ttu-id="10d5b-225">Protokół IPSec</span><span class="sxs-lookup"><span data-stu-id="10d5b-225">IPSec</span></span>| <span data-ttu-id="10d5b-226">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-226">Supported</span></span>|
|<span data-ttu-id="10d5b-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="10d5b-227">VNet2Vnet</span></span>| <span data-ttu-id="10d5b-228">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-228">Supported</span></span>|
|<span data-ttu-id="10d5b-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="10d5b-229">ExpressRoute</span></span>| <span data-ttu-id="10d5b-230">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-230">Not Supported</span></span>|
|<span data-ttu-id="10d5b-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="10d5b-231">Hypernet</span></span>| <span data-ttu-id="10d5b-232">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-232">Not Supported</span></span>|
|<span data-ttu-id="10d5b-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="10d5b-233">VPNClient</span></span>| <span data-ttu-id="10d5b-234">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="10d5b-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="10d5b-235">Pliki dziennika</span><span class="sxs-lookup"><span data-stu-id="10d5b-235">Log files</span></span>

<span data-ttu-id="10d5b-236">pliki dziennika Hello zasobów rozwiązywania problemów są przechowywane na koncie magazynu po zakończeniu rozwiązywania problemów z zasobów.</span><span class="sxs-lookup"><span data-stu-id="10d5b-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="10d5b-237">Witaj poniższy obraz przedstawia zawartość przykład hello wywołanie, które spowodowało wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="10d5b-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![plik zip][1]

> [!NOTE]
> <span data-ttu-id="10d5b-239">W niektórych przypadkach tylko podzbiór plików dzienników hello są zapisywane toostorage.</span><span class="sxs-lookup"><span data-stu-id="10d5b-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="10d5b-240">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="10d5b-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="10d5b-241">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="10d5b-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="10d5b-242">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="10d5b-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="10d5b-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="10d5b-243">ConnectionStats.txt</span></span>

<span data-ttu-id="10d5b-244">Witaj **ConnectionStats.txt** plik zawiera ogólna Statystyka o hello połączenia, w tym Bajty przychodzące i wychodzące, stan połączenia i hello czasu hello jest nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="10d5b-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="10d5b-245">Jeśli Rozwiązywanie problemów z interfejsu API toohello wywołania hello zwraca dobrej kondycji, jest jedynym elementem hello zwrócił w pliku zip hello **ConnectionStats.txt** pliku.</span><span class="sxs-lookup"><span data-stu-id="10d5b-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="10d5b-246">Witaj zawartość tego pliku są podobne toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="10d5b-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="10d5b-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="10d5b-247">CPUStats.txt</span></span>

<span data-ttu-id="10d5b-248">Witaj **CPUStats.txt** plik zawiera użycie procesora CPU i pamięci w czasie hello testów.</span><span class="sxs-lookup"><span data-stu-id="10d5b-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="10d5b-249">Witaj zawartość tego pliku jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="10d5b-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="10d5b-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="10d5b-250">IKEErrors.txt</span></span>

<span data-ttu-id="10d5b-251">Witaj **IKEErrors.txt** plik zawiera błędy IKE, które zostały odnalezione podczas monitorowania.</span><span class="sxs-lookup"><span data-stu-id="10d5b-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="10d5b-252">Witaj poniższy przykład przedstawia hello zawartość pliku IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="10d5b-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="10d5b-253">Błędy mogą się różnić w zależności od hello problem.</span><span class="sxs-lookup"><span data-stu-id="10d5b-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="10d5b-254">Wyczyszczona wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="10d5b-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="10d5b-255">Witaj **Scrubbed wfpdiag.txt** plik dziennika zawiera hello wfp dziennika.</span><span class="sxs-lookup"><span data-stu-id="10d5b-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="10d5b-256">Ten dziennik zawiera rejestrowanie IKE/AuthIP błędy i listy pakietów.</span><span class="sxs-lookup"><span data-stu-id="10d5b-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="10d5b-257">Witaj poniższy przykład przedstawia hello zawartość pliku Scrubbed wfpdiag.txt hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="10d5b-258">W tym przykładzie hello klucza współużytkowanego połączenia jest niepoprawny, co wynika z wiersza 3 powitania od dołu hello.</span><span class="sxs-lookup"><span data-stu-id="10d5b-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="10d5b-259">Hello poniższy przykład jest po prostu fragment hello cały dziennik dziennika hello mogą być obszerne w zależności od hello problem.</span><span class="sxs-lookup"><span data-stu-id="10d5b-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="10d5b-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="10d5b-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="10d5b-261">Witaj **wfpdiag.txt.sum** plik jest dziennika pokazującego buforów hello i przetworzonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="10d5b-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="10d5b-262">Witaj poniższym przykładzie jest hello zawartości pliku wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="10d5b-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="10d5b-263">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10d5b-263">Next steps</span></span>

<span data-ttu-id="10d5b-264">Dowiedz się, jak toodiagnose bramy sieci VPN i połączeń za pośrednictwem hello portalu odwiedzając [bramy Rozwiązywanie problemów — Azure portal](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="10d5b-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
