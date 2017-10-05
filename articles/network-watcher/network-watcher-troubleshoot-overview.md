---
title: "Wprowadzenie do rozwiązywania problemów w obserwatora sieciowego Azure zasobów | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie funkcji rozwiązywania problemów z zasobów obserwatora sieciowego"
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="4eef8-103">Wprowadzenie do rozwiązywania problemów w obserwatora sieciowego Azure zasobów</span><span class="sxs-lookup"><span data-stu-id="4eef8-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="4eef8-104">Bramy sieci wirtualnej zapewniają łączność między zasobami lokalnymi i innych sieci wirtualnych w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4eef8-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="4eef8-105">Monitorowanie tych bram i ich połączeń jest bardzo istotne dla zapewnienia komunikacji nie jest uszkodzona.</span><span class="sxs-lookup"><span data-stu-id="4eef8-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="4eef8-106">Obserwatora sieciowego umożliwia rozwiązywanie problemów z bramy sieci wirtualnej i połączenia.</span><span class="sxs-lookup"><span data-stu-id="4eef8-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="4eef8-107">Można go wywołać za pomocą portalu, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4eef8-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="4eef8-108">Po wywołaniu obserwatora sieciowego diagnozuje kondycji bramy sieci wirtualnej lub połączenia i zwracają odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="4eef8-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="4eef8-109">To żądanie jest długo działającą transakcję, wyniki są zwracane po zakończeniu diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="4eef8-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="4eef8-111">Wyniki</span><span class="sxs-lookup"><span data-stu-id="4eef8-111">Results</span></span>

<span data-ttu-id="4eef8-112">Wstępne wyników zwróconych nadaj ogólny obraz kondycji zasobu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="4eef8-113">Lepszy informacje mogą być dostępne dla zasobów, jak pokazano w poniższej sekcji:</span><span class="sxs-lookup"><span data-stu-id="4eef8-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="4eef8-114">Poniżej znajduje się wartości zwracane z Rozwiązywanie problemów z interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="4eef8-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="4eef8-115">**wartość startTime** — ta wartość jest uruchomieniu wywołania interfejsu API Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="4eef8-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="4eef8-116">**wartość endTime** — ta wartość jest czas zakończenia rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="4eef8-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="4eef8-117">**Kod** — ta wartość jest zła, w przypadku awarii jednego diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="4eef8-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="4eef8-118">**wyniki** -wyników jest zbiór wyników zwróconych na połączenie lub brama sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4eef8-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="4eef8-119">**Identyfikator** — ta wartość jest typu błędu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="4eef8-120">**Podsumowanie** — ta wartość jest podsumowanie usterki.</span><span class="sxs-lookup"><span data-stu-id="4eef8-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="4eef8-121">**szczegółowe** -wartość zawiera szczegółowy opis błędu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="4eef8-122">**recommendedActions** — ta właściwość jest kolekcją zalecane akcje.</span><span class="sxs-lookup"><span data-stu-id="4eef8-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="4eef8-123">**actionText** — ta wartość zawiera opis czynności do wykonania.</span><span class="sxs-lookup"><span data-stu-id="4eef8-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="4eef8-124">**actionUri** — ta wartość Określa identyfikator URI do dokumentacji na temat sposobu działania.</span><span class="sxs-lookup"><span data-stu-id="4eef8-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="4eef8-125">**actionUriText** — ta wartość jest krótki opis tekst akcji.</span><span class="sxs-lookup"><span data-stu-id="4eef8-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="4eef8-126">W poniższej tabeli przedstawiono typy inny błąd (identyfikator w obszarze wyniki z powyższej listy), które są dostępne, a jeśli błąd tworzy dzienniki.</span><span class="sxs-lookup"><span data-stu-id="4eef8-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="4eef8-127">Brama</span><span class="sxs-lookup"><span data-stu-id="4eef8-127">Gateway</span></span>

| <span data-ttu-id="4eef8-128">Typ błędu</span><span class="sxs-lookup"><span data-stu-id="4eef8-128">Fault Type</span></span> | <span data-ttu-id="4eef8-129">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="4eef8-129">Reason</span></span> | <span data-ttu-id="4eef8-130">Log</span><span class="sxs-lookup"><span data-stu-id="4eef8-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="4eef8-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="4eef8-131">NoFault</span></span> | <span data-ttu-id="4eef8-132">Gdy błąd nie została wykryta.</span><span class="sxs-lookup"><span data-stu-id="4eef8-132">When no error is detected.</span></span> |<span data-ttu-id="4eef8-133">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-133">Yes</span></span>|
| <span data-ttu-id="4eef8-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="4eef8-134">GatewayNotFound</span></span> | <span data-ttu-id="4eef8-135">Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie.</span><span class="sxs-lookup"><span data-stu-id="4eef8-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="4eef8-136">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-136">No</span></span>|
| <span data-ttu-id="4eef8-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="4eef8-137">PlannedMaintenance</span></span> |  <span data-ttu-id="4eef8-138">Wystąpienie bramy jest w trakcie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="4eef8-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="4eef8-139">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-139">No</span></span>|
| <span data-ttu-id="4eef8-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="4eef8-140">UserDrivenUpdate</span></span> | <span data-ttu-id="4eef8-141">Gdy aktualizacja użytkownika jest w toku.</span><span class="sxs-lookup"><span data-stu-id="4eef8-141">When a user update is in progress.</span></span> <span data-ttu-id="4eef8-142">Może to być operacji zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="4eef8-142">This could be a resize operation.</span></span> | <span data-ttu-id="4eef8-143">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-143">No</span></span> |
| <span data-ttu-id="4eef8-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="4eef8-144">VipUnResponsive</span></span> | <span data-ttu-id="4eef8-145">Nie można osiągnąć podstawowego wystąpienia bramy.</span><span class="sxs-lookup"><span data-stu-id="4eef8-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="4eef8-146">Dzieje się tak, gdy badania kondycji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="4eef8-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="4eef8-147">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-147">No</span></span> |
| <span data-ttu-id="4eef8-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="4eef8-148">PlatformInActive</span></span> | <span data-ttu-id="4eef8-149">Istnieje problem z platformą.</span><span class="sxs-lookup"><span data-stu-id="4eef8-149">There is an issue with the platform.</span></span> | <span data-ttu-id="4eef8-150">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-150">No</span></span>|
| <span data-ttu-id="4eef8-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="4eef8-151">ServiceNotRunning</span></span> | <span data-ttu-id="4eef8-152">Usługa podstawowy nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4eef8-152">The underlying service is not running.</span></span> | <span data-ttu-id="4eef8-153">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-153">No</span></span>|
| <span data-ttu-id="4eef8-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="4eef8-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="4eef8-155">Połączenia nie istnieje w bramie.</span><span class="sxs-lookup"><span data-stu-id="4eef8-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="4eef8-156">Jest to tylko ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4eef8-156">This is only a warning.</span></span>| <span data-ttu-id="4eef8-157">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-157">No</span></span>|
| <span data-ttu-id="4eef8-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="4eef8-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="4eef8-159">Połączenia nie są połączone.</span><span class="sxs-lookup"><span data-stu-id="4eef8-159">Connections are not connected.</span></span> <span data-ttu-id="4eef8-160">Jest to tylko ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4eef8-160">This is only a warning.</span></span>| <span data-ttu-id="4eef8-161">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-161">Yes</span></span>|
| <span data-ttu-id="4eef8-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="4eef8-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="4eef8-163">Bieżące użycie procesora CPU bramy jest > 95%.</span><span class="sxs-lookup"><span data-stu-id="4eef8-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="4eef8-164">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="4eef8-165">Połączenie</span><span class="sxs-lookup"><span data-stu-id="4eef8-165">Connection</span></span>

| <span data-ttu-id="4eef8-166">Typ błędu</span><span class="sxs-lookup"><span data-stu-id="4eef8-166">Fault Type</span></span> | <span data-ttu-id="4eef8-167">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="4eef8-167">Reason</span></span> | <span data-ttu-id="4eef8-168">Log</span><span class="sxs-lookup"><span data-stu-id="4eef8-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="4eef8-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="4eef8-169">NoFault</span></span> | <span data-ttu-id="4eef8-170">Gdy błąd nie została wykryta.</span><span class="sxs-lookup"><span data-stu-id="4eef8-170">When no error is detected.</span></span> |<span data-ttu-id="4eef8-171">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-171">Yes</span></span>|
| <span data-ttu-id="4eef8-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="4eef8-172">GatewayNotFound</span></span> | <span data-ttu-id="4eef8-173">Nie można odnaleźć bramy lub bramy nie jest obsługiwana administracyjnie.</span><span class="sxs-lookup"><span data-stu-id="4eef8-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="4eef8-174">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-174">No</span></span>|
| <span data-ttu-id="4eef8-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="4eef8-175">PlannedMaintenance</span></span> | <span data-ttu-id="4eef8-176">Wystąpienie bramy jest w trakcie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="4eef8-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="4eef8-177">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-177">No</span></span>|
| <span data-ttu-id="4eef8-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="4eef8-178">UserDrivenUpdate</span></span> | <span data-ttu-id="4eef8-179">Gdy aktualizacja użytkownika jest w toku.</span><span class="sxs-lookup"><span data-stu-id="4eef8-179">When a user update is in progress.</span></span> <span data-ttu-id="4eef8-180">Może to być operacji zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="4eef8-180">This could be a resize operation.</span></span>  | <span data-ttu-id="4eef8-181">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-181">No</span></span> |
| <span data-ttu-id="4eef8-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="4eef8-182">VipUnResponsive</span></span> | <span data-ttu-id="4eef8-183">Nie można osiągnąć podstawowego wystąpienia bramy.</span><span class="sxs-lookup"><span data-stu-id="4eef8-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="4eef8-184">Zdarza się, gdy badania kondycji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="4eef8-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="4eef8-185">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-185">No</span></span> |
| <span data-ttu-id="4eef8-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="4eef8-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="4eef8-187">Brak konfiguracji połączenia.</span><span class="sxs-lookup"><span data-stu-id="4eef8-187">Connection configuration is missing.</span></span> | <span data-ttu-id="4eef8-188">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-188">No</span></span> |
| <span data-ttu-id="4eef8-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="4eef8-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="4eef8-190">Połączenie jest oznaczony jako "odłączony".</span><span class="sxs-lookup"><span data-stu-id="4eef8-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="4eef8-191">Nie</span><span class="sxs-lookup"><span data-stu-id="4eef8-191">No</span></span>|
| <span data-ttu-id="4eef8-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="4eef8-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="4eef8-193">Podległej usłudze nie ma skonfigurowanego połączenia.</span><span class="sxs-lookup"><span data-stu-id="4eef8-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="4eef8-194">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-194">Yes</span></span> |
| <span data-ttu-id="4eef8-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="4eef8-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="4eef8-196">Podstawowe usługi jest oznaczony jako stan wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="4eef8-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="4eef8-197">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-197">Yes</span></span>|
| <span data-ttu-id="4eef8-198">Authentication</span><span class="sxs-lookup"><span data-stu-id="4eef8-198">Authentication</span></span> | <span data-ttu-id="4eef8-199">Niezgodność klucz wstępny.</span><span class="sxs-lookup"><span data-stu-id="4eef8-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="4eef8-200">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-200">Yes</span></span>|
| <span data-ttu-id="4eef8-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="4eef8-201">PeerReachability</span></span> | <span data-ttu-id="4eef8-202">Brama elementu równorzędnego nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="4eef8-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="4eef8-203">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-203">Yes</span></span>|
| <span data-ttu-id="4eef8-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="4eef8-204">IkePolicyMismatch</span></span> | <span data-ttu-id="4eef8-205">Brama równorzędnej ma zasady IKE, które nie są obsługiwane przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="4eef8-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="4eef8-206">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-206">Yes</span></span>|
| <span data-ttu-id="4eef8-207">Błąd WfpParse</span><span class="sxs-lookup"><span data-stu-id="4eef8-207">WfpParse Error</span></span> | <span data-ttu-id="4eef8-208">Wystąpił błąd podczas analizowania dziennika platformy filtrowania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4eef8-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="4eef8-209">Tak</span><span class="sxs-lookup"><span data-stu-id="4eef8-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="4eef8-210">Obsługiwane typy bramy</span><span class="sxs-lookup"><span data-stu-id="4eef8-210">Supported Gateway types</span></span>

<span data-ttu-id="4eef8-211">Na poniższej liście przedstawiono obsługę Pokazuje połączenia i bram, które są obsługiwane w rozwiązywaniu problemów obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="4eef8-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="4eef8-212">**Typy bramy**</span><span class="sxs-lookup"><span data-stu-id="4eef8-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="4eef8-213">Sieć VPN</span><span class="sxs-lookup"><span data-stu-id="4eef8-213">VPN</span></span>      | <span data-ttu-id="4eef8-214">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-214">Supported</span></span>        |
|<span data-ttu-id="4eef8-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4eef8-215">ExpressRoute</span></span> | <span data-ttu-id="4eef8-216">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-216">Not Supported</span></span> |
|<span data-ttu-id="4eef8-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="4eef8-217">Hypernet</span></span> | <span data-ttu-id="4eef8-218">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-218">Not Supported</span></span>|
|<span data-ttu-id="4eef8-219">**Typy z siecią VPN**</span><span class="sxs-lookup"><span data-stu-id="4eef8-219">**VPN types**</span></span> | |
|<span data-ttu-id="4eef8-220">Na podstawie trasy</span><span class="sxs-lookup"><span data-stu-id="4eef8-220">Route Based</span></span> | <span data-ttu-id="4eef8-221">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-221">Supported</span></span>|
|<span data-ttu-id="4eef8-222">Na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="4eef8-222">Policy Based</span></span> | <span data-ttu-id="4eef8-223">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-223">Not Supported</span></span>|
|<span data-ttu-id="4eef8-224">**Typy połączeń**</span><span class="sxs-lookup"><span data-stu-id="4eef8-224">**Connection types**</span></span>||
|<span data-ttu-id="4eef8-225">Protokół IPSec</span><span class="sxs-lookup"><span data-stu-id="4eef8-225">IPSec</span></span>| <span data-ttu-id="4eef8-226">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-226">Supported</span></span>|
|<span data-ttu-id="4eef8-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="4eef8-227">VNet2Vnet</span></span>| <span data-ttu-id="4eef8-228">Obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-228">Supported</span></span>|
|<span data-ttu-id="4eef8-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4eef8-229">ExpressRoute</span></span>| <span data-ttu-id="4eef8-230">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-230">Not Supported</span></span>|
|<span data-ttu-id="4eef8-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="4eef8-231">Hypernet</span></span>| <span data-ttu-id="4eef8-232">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-232">Not Supported</span></span>|
|<span data-ttu-id="4eef8-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="4eef8-233">VPNClient</span></span>| <span data-ttu-id="4eef8-234">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4eef8-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="4eef8-235">Pliki dziennika</span><span class="sxs-lookup"><span data-stu-id="4eef8-235">Log files</span></span>

<span data-ttu-id="4eef8-236">Pliki zasobów do rozwiązywania problemów z dziennika są przechowywane na koncie magazynu po zakończeniu rozwiązywania problemów z zasobów.</span><span class="sxs-lookup"><span data-stu-id="4eef8-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="4eef8-237">Na poniższej ilustracji przedstawiono przykład zawartość wywołanie, które spowodowało wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![plik zip][1]

> [!NOTE]
> <span data-ttu-id="4eef8-239">W niektórych przypadkach tylko podzestaw pliki dzienników są zapisywane w pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="4eef8-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="4eef8-240">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zapoznaj się [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="4eef8-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="4eef8-241">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="4eef8-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="4eef8-242">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj przy użyciu następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="4eef8-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="4eef8-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="4eef8-243">ConnectionStats.txt</span></span>

<span data-ttu-id="4eef8-244">**ConnectionStats.txt** plik zawiera ogólna Statystyka połączenia, w tym Bajty przychodzące i wychodzące, stan połączenia i czasu, połączenie zostało nawiązane.</span><span class="sxs-lookup"><span data-stu-id="4eef8-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="4eef8-245">Jeśli wywołanie do rozwiązywania problemów z interfejsu API zwraca dobrej kondycji, jest jedynym elementem zwrócił w pliku zip **ConnectionStats.txt** pliku.</span><span class="sxs-lookup"><span data-stu-id="4eef8-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="4eef8-246">Zawartość tego pliku są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4eef8-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="4eef8-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="4eef8-247">CPUStats.txt</span></span>

<span data-ttu-id="4eef8-248">**CPUStats.txt** plik zawiera użycie procesora CPU i pamięci w czasie testów.</span><span class="sxs-lookup"><span data-stu-id="4eef8-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="4eef8-249">Zawartość tego pliku jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4eef8-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="4eef8-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="4eef8-250">IKEErrors.txt</span></span>

<span data-ttu-id="4eef8-251">**IKEErrors.txt** plik zawiera błędy IKE, które zostały odnalezione podczas monitorowania.</span><span class="sxs-lookup"><span data-stu-id="4eef8-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="4eef8-252">W poniższym przykładzie przedstawiono zawartość pliku IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="4eef8-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="4eef8-253">Błędy mogą się różnić w zależności od tego problemu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="4eef8-254">Wyczyszczona wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="4eef8-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="4eef8-255">**Scrubbed wfpdiag.txt** plik dziennika zawiera dziennik platformy filtrowania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4eef8-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="4eef8-256">Ten dziennik zawiera rejestrowanie IKE/AuthIP błędy i listy pakietów.</span><span class="sxs-lookup"><span data-stu-id="4eef8-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="4eef8-257">W poniższym przykładzie przedstawiono zawartość pliku Scrubbed wfpdiag.txt.</span><span class="sxs-lookup"><span data-stu-id="4eef8-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="4eef8-258">W tym przykładzie klucza współużytkowanego połączenia jest niepoprawny, co wynika z 3 wiersza od dołu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="4eef8-259">Poniższy przykład się tylko fragment dziennika cały dziennik może być długi w zależności od tego problemu.</span><span class="sxs-lookup"><span data-stu-id="4eef8-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="4eef8-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="4eef8-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="4eef8-261">**Wfpdiag.txt.sum** plik jest dziennika pokazującego buforów i przetworzonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4eef8-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="4eef8-262">Poniższy przykład jest zawartość pliku wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="4eef8-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="4eef8-263">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4eef8-263">Next steps</span></span>

<span data-ttu-id="4eef8-264">Dowiedz się, jak diagnozować bramy sieci VPN i połączeń za pośrednictwem portalu, odwiedzając [bramy Rozwiązywanie problemów — Azure portal](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4eef8-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
