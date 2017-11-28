---
title: "aaaAzure rozwiązania analizy sieci w Log Analytics | Dokumentacja firmy Microsoft"
description: "Możesz użyć hello rozwiązania Azure Networking analizy dzienników grupy zabezpieczeń sieci platformy Azure tooreview analizy dzienników i dzienniki bramy aplikacji Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="74978-103">Sieć platformy Azure monitorowanie rozwiązań w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="74978-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="74978-104">Analiza dzienników oferuje hello następujące rozwiązania do monitorowania sieci:</span><span class="sxs-lookup"><span data-stu-id="74978-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="74978-105">Monitor wydajności sieci (NPM) do</span><span class="sxs-lookup"><span data-stu-id="74978-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="74978-106">Monitorowanie kondycji hello sieci</span><span class="sxs-lookup"><span data-stu-id="74978-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="74978-107">Azure tooreview analytics bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="74978-108">Dzienniki bramy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="74978-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="74978-109">Azure metryki bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="74978-110">Grupy zabezpieczeń sieci Azure tooreview analityka</span><span class="sxs-lookup"><span data-stu-id="74978-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="74978-111">Dzienniki grupy zabezpieczeń sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="74978-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="74978-112">Monitor wydajności sieci (NPM)</span><span class="sxs-lookup"><span data-stu-id="74978-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="74978-113">Witaj [monitora wydajności sieci](log-analytics-network-performance-monitor.md) rozwiązanie do zarządzania jest rozwiązanie, monitoruje kondycję hello, dostępności i uzyskiwanie sieci do monitorowania sieci.</span><span class="sxs-lookup"><span data-stu-id="74978-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="74978-114">Jest używana toomonitor łączność między:</span><span class="sxs-lookup"><span data-stu-id="74978-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="74978-115">Chmura publiczna i lokalnych</span><span class="sxs-lookup"><span data-stu-id="74978-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="74978-116">centra danych i lokalizacje użytkownika (biurach oddziałów)</span><span class="sxs-lookup"><span data-stu-id="74978-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="74978-117">podsieci hosting różnych warstw aplikacji wielowarstwowych.</span><span class="sxs-lookup"><span data-stu-id="74978-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="74978-118">Aby uzyskać więcej informacji, zobacz [monitora wydajności sieci](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="74978-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="74978-119">Azure analytics bramy aplikacji i grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="74978-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="74978-120">toouse hello rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="74978-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="74978-121">Dodaj tooLog rozwiązania zarządzania hello Analytics, a</span><span class="sxs-lookup"><span data-stu-id="74978-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="74978-122">Włącz diagnostykę toodirect hello diagnostyki tooa analizy dzienników z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="74978-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="74978-123">Nie jest magazynu obiektów Blob tooAzure niezbędne toowrite hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="74978-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="74978-124">Można włączyć diagnostyki i hello odpowiednie rozwiązanie dla jednej lub obu z bramy aplikacji i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="74978-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="74978-125">Jeśli nie włączaj rejestrowania diagnostyki dla określonego typu zasobu, ale zainstalować rozwiązanie hello hello bloków pulpitu nawigacyjnego dla tego zasobu są puste i wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="74978-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="74978-126">W stycznia 2017 r. hello obsługiwane sposób wysyłania dzienników z bramy aplikacji i grup zabezpieczeń sieci tooLog zmienić Analytics.</span><span class="sxs-lookup"><span data-stu-id="74978-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="74978-127">Jeśli widzisz hello **Analytics sieci Azure (przestarzałe)** rozwiązania, odwoływać się za[migracja z rozwiązania do analizy sieci starego hello](#migrating-from-the-old-networking-analytics-solution) czynności należy toofollow.</span><span class="sxs-lookup"><span data-stu-id="74978-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="74978-128">Przejrzyj szczegóły zbierania danych w sieci Azure</span><span class="sxs-lookup"><span data-stu-id="74978-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="74978-129">Hello Azure Application Gateway analizy i rozwiązania do zarządzania analytics hello sieciowej grupy zabezpieczeń zbierania dzienników diagnostycznych bezpośrednio z bramy aplikacji Azure i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="74978-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="74978-130">Nie jest konieczne toowrite hello dzienniki tooAzure magazynu obiektów Blob i agent nie jest wymagany do zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="74978-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="74978-131">Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla analizy brama aplikacji w usłudze Azure i hello analytics grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="74978-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="74978-132">Platforma</span><span class="sxs-lookup"><span data-stu-id="74978-132">Platform</span></span> | <span data-ttu-id="74978-133">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="74978-133">Direct agent</span></span> | <span data-ttu-id="74978-134">Agent menedżera operacji centrum systemów</span><span class="sxs-lookup"><span data-stu-id="74978-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="74978-135">Azure</span><span class="sxs-lookup"><span data-stu-id="74978-135">Azure</span></span> | <span data-ttu-id="74978-136">Wymagane programu Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="74978-136">Operations Manager required?</span></span> | <span data-ttu-id="74978-137">Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="74978-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="74978-138">Częstotliwość zbierania</span><span class="sxs-lookup"><span data-stu-id="74978-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="74978-139">Azure</span><span class="sxs-lookup"><span data-stu-id="74978-139">Azure</span></span> |  |  |<span data-ttu-id="74978-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="74978-140">&#8226;</span></span> |  |  |<span data-ttu-id="74978-141">Podczas rejestrowania</span><span class="sxs-lookup"><span data-stu-id="74978-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="74978-142">Azure rozwiązania analizy brama aplikacji w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="74978-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure symbol analizy bramy aplikacji](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="74978-144">powitania po dzienniki są obsługiwane w przypadku bram aplikacji:</span><span class="sxs-lookup"><span data-stu-id="74978-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="74978-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="74978-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="74978-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="74978-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="74978-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="74978-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="74978-148">następujące metryki Hello są obsługiwane w przypadku bram aplikacji:</span><span class="sxs-lookup"><span data-stu-id="74978-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="74978-149">Przepływność 5 minut</span><span class="sxs-lookup"><span data-stu-id="74978-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="74978-150">Instalowanie i konfigurowanie hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="74978-150">Install and configure hello solution</span></span>
<span data-ttu-id="74978-151">Użyj hello następujące instrukcje tooinstall i skonfiguruj rozwiązania analizy hello Azure Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="74978-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="74978-152">Włącz hello rozwiązania analizy bramy aplikacji Azure z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="74978-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="74978-153">Włączanie rejestrowania diagnostyki dla hello [bramy aplikacji](../application-gateway/application-gateway-diagnostics.md) ma toomonitor.</span><span class="sxs-lookup"><span data-stu-id="74978-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="74978-154">Włącz diagnostykę bramy aplikacji Azure w portalu hello</span><span class="sxs-lookup"><span data-stu-id="74978-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="74978-155">W hello portalu Azure Przejdź toomonitor zasobów bramy aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="74978-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="74978-156">Wybierz *dzienników diagnostycznych* hello tooopen po stronie</span><span class="sxs-lookup"><span data-stu-id="74978-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![obraz zasobu bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="74978-158">Kliknij przycisk *Włącz diagnostykę* hello tooopen po stronie</span><span class="sxs-lookup"><span data-stu-id="74978-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![obraz zasobu bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="74978-160">Kliknij tooturn diagnostykę, *na* w obszarze *stanu*</span><span class="sxs-lookup"><span data-stu-id="74978-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="74978-161">Kliknij przycisk wyboru hello *wysyłania tooLog analityka*</span><span class="sxs-lookup"><span data-stu-id="74978-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="74978-162">Wybierz istniejący obszar roboczy analizy dzienników lub tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="74978-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="74978-163">Kliknij przycisk wyboru hello **dziennika** dla każdego toocollect typy dziennika hello</span><span class="sxs-lookup"><span data-stu-id="74978-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="74978-164">Kliknij przycisk *zapisać* tooenable hello rejestrowania diagnostyki tooLog analityka</span><span class="sxs-lookup"><span data-stu-id="74978-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="74978-165">Włącz diagnostykę sieci platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="74978-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="74978-166">Witaj następującego skryptu programu PowerShell zawiera przykładowy sposób tooenable diagnostyczne dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74978-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="74978-167">Użyj analizy bramy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="74978-167">Use Azure Application Gateway analytics</span></span>
![Obraz kafelka analytics bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="74978-169">Po kliknięciu hello **analytics Azure Application Gateway** kafelka na powitania omówienie wyświetlanie podsumowań dzienników i następnie przejść do szczegółów w toodetails dla hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="74978-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="74978-170">Rejestruje dostęp do bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="74978-171">Błędy na kliencie i serwerze dla dzienników dostępu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="74978-172">Liczba żądań na godzinę dla każdej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="74978-173">Nieudane żądania na godzinę dla każdej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="74978-174">Błędy przez agenta użytkownika dla bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="74978-175">Wydajność bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-175">Application Gateway performance</span></span>
  * <span data-ttu-id="74978-176">Kondycja hosta bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="74978-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="74978-177">Maksymalne i 95 percentyl żądań bramy aplikacji nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="74978-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Obraz pulpitu nawigacyjnego analytics bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Obraz pulpitu nawigacyjnego analytics bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="74978-180">Na powitania **analytics Azure Application Gateway** pulpitu nawigacyjnego, przejrzyj hello informacje podsumowania w jednym z bloków hello, a następnie kliknij jedną tooview szczegółowe informacje dotyczące hello dziennik wyszukiwania strony.</span><span class="sxs-lookup"><span data-stu-id="74978-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="74978-181">Na wszystkich stronach wyszukiwania dziennika hello można wyświetlić wyniki według czasu, szczegółowe wyniki i historię dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74978-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="74978-182">Można również filtrować według aspekty toonarrow hello wyników.</span><span class="sxs-lookup"><span data-stu-id="74978-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="74978-183">Grupy zabezpieczeń sieci Azure rozwiązania analizy w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="74978-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Symbol Analytics sieciowej grupy zabezpieczeń usługi Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="74978-185">powitania po dzienniki są obsługiwane w przypadku grup zabezpieczeń sieci:</span><span class="sxs-lookup"><span data-stu-id="74978-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="74978-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="74978-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="74978-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="74978-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="74978-188">Instalowanie i konfigurowanie hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="74978-188">Install and configure hello solution</span></span>
<span data-ttu-id="74978-189">Użyj hello następujące instrukcje tooinstall i skonfiguruj rozwiązania Azure Networking analizy hello:</span><span class="sxs-lookup"><span data-stu-id="74978-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="74978-190">Włącz hello rozwiązania analizy Azure sieciową grupę zabezpieczeń z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="74978-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="74978-191">Włączanie rejestrowania diagnostyki dla hello [sieciowej grupy zabezpieczeń](../virtual-network/virtual-network-nsg-manage-log.md) zasoby, które chcesz toomonitor.</span><span class="sxs-lookup"><span data-stu-id="74978-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="74978-192">Włącz diagnostykę grupy zabezpieczeń sieci platformy Azure w portalu hello</span><span class="sxs-lookup"><span data-stu-id="74978-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="74978-193">W hello portalu Azure Przejdź toohello sieciowej grupy zabezpieczeń zasobów toomonitor</span><span class="sxs-lookup"><span data-stu-id="74978-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="74978-194">Wybierz *dzienników diagnostycznych* hello tooopen po stronie</span><span class="sxs-lookup"><span data-stu-id="74978-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Obraz zasobów Azure sieciowej grupy zabezpieczeń](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="74978-196">Kliknij przycisk *Włącz diagnostykę* hello tooopen po stronie</span><span class="sxs-lookup"><span data-stu-id="74978-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Obraz zasobów Azure sieciowej grupy zabezpieczeń](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="74978-198">Kliknij tooturn diagnostykę, *na* w obszarze *stanu*</span><span class="sxs-lookup"><span data-stu-id="74978-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="74978-199">Kliknij przycisk wyboru hello *wysyłania tooLog analityka*</span><span class="sxs-lookup"><span data-stu-id="74978-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="74978-200">Wybierz istniejący obszar roboczy analizy dzienników lub tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="74978-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="74978-201">Kliknij przycisk wyboru hello **dziennika** dla każdego toocollect typy dziennika hello</span><span class="sxs-lookup"><span data-stu-id="74978-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="74978-202">Kliknij przycisk *zapisać* tooenable hello rejestrowania diagnostyki tooLog analityka</span><span class="sxs-lookup"><span data-stu-id="74978-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="74978-203">Włącz diagnostykę sieci platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="74978-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="74978-204">Witaj następującego skryptu programu PowerShell zawiera przykładowy sposób tooenable diagnostyczne dla grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="74978-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="74978-205">Użyj grupy zabezpieczeń sieci Azure analityka</span><span class="sxs-lookup"><span data-stu-id="74978-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="74978-206">Po kliknięciu hello **analytics sieciowej grupy zabezpieczeń usługi Azure** kafelka na powitania omówienie wyświetlanie podsumowań dzienników i następnie przejść do szczegółów w toodetails dla hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="74978-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="74978-207">Grupy zabezpieczeń sieci zablokowane przepływów</span><span class="sxs-lookup"><span data-stu-id="74978-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="74978-208">Reguły grupy zabezpieczeń sieci z przepływami zablokowanych</span><span class="sxs-lookup"><span data-stu-id="74978-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="74978-209">Adresy MAC z przepływami zablokowanych</span><span class="sxs-lookup"><span data-stu-id="74978-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="74978-210">Dozwolone przepływów grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="74978-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="74978-211">Reguły grupy zabezpieczeń sieci z przepływami dozwolone</span><span class="sxs-lookup"><span data-stu-id="74978-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="74978-212">Adresy MAC z przepływami dozwolone</span><span class="sxs-lookup"><span data-stu-id="74978-212">MAC addresses with allowed flows</span></span>

![Obraz pulpitu nawigacyjnego analytics sieciowej grupy zabezpieczeń usługi Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Obraz pulpitu nawigacyjnego analytics sieciowej grupy zabezpieczeń usługi Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="74978-215">Na powitania **analytics sieciowej grupy zabezpieczeń usługi Azure** pulpitu nawigacyjnego, przejrzyj hello informacje podsumowania w jednym z bloków hello, a następnie kliknij jedną tooview szczegółowe informacje dotyczące hello dziennik wyszukiwania strony.</span><span class="sxs-lookup"><span data-stu-id="74978-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="74978-216">Na wszystkich stronach wyszukiwania dziennika hello można wyświetlić wyniki według czasu, szczegółowe wyniki i historię dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="74978-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="74978-217">Można również filtrować według aspekty toonarrow hello wyników.</span><span class="sxs-lookup"><span data-stu-id="74978-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="74978-218">Migracja z rozwiązania do analizy sieci starego hello</span><span class="sxs-lookup"><span data-stu-id="74978-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="74978-219">W stycznia 2017 r. hello obsługiwane sposób wysyłania dzienników z bramy aplikacji Azure i grup zabezpieczeń sieci Azure tooLog zmienić Analytics.</span><span class="sxs-lookup"><span data-stu-id="74978-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="74978-220">Te zmiany zapewniają hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="74978-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="74978-221">Dzienniki są zapisywane bezpośrednio tooLog Analytics bez hello muszą toouse konta magazynu</span><span class="sxs-lookup"><span data-stu-id="74978-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="74978-222">Mniejsze opóźnienia od czasu hello, kiedy są dzienniki generowane toothem dostępne w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="74978-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="74978-223">Mniejszej liczby kroków konfiguracji</span><span class="sxs-lookup"><span data-stu-id="74978-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="74978-224">Format wspólne dla wszystkich typów Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="74978-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="74978-225">Witaj toouse aktualizacja rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="74978-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="74978-226">Skonfiguruj toobe diagnostyki wysyłane bezpośrednio tooLog Analytics z bramy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="74978-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="74978-227">Skonfiguruj toobe diagnostyki wysyłane bezpośrednio tooLog Analytics z grup zabezpieczeń sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="74978-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="74978-228">Włącz hello *analizy bramy aplikacji Azure* i hello *analiza grupy zabezpieczeń sieci Azure* rozwiązania za pomocą hello procesu opisanego w [rozwiązań dodać analizy dzienników Witaj galerii rozwiązań](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="74978-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="74978-229">Wszystkie zapisane kwerendy, pulpity nawigacyjne lub alerty toouse hello nowy typ danych</span><span class="sxs-lookup"><span data-stu-id="74978-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="74978-230">Typ jest tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="74978-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="74978-231">Można użyć dzienników sieci toofilter tooAzure hello typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="74978-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="74978-232">Zamiast:</span><span class="sxs-lookup"><span data-stu-id="74978-232">Instead of:</span></span> | <span data-ttu-id="74978-233">Za pomocą:</span><span class="sxs-lookup"><span data-stu-id="74978-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="74978-234">Dla dowolnego pola, które sufiks \_s, \_d, lub \_g w nazwie hello, zmień hello pierwszy znak toolower przypadku</span><span class="sxs-lookup"><span data-stu-id="74978-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="74978-235">Dla dowolnego pola, które sufiks \_o w polu Nazwa danych hello jest podzielony na poszczególnych pól na podstawie nazw pól hello zagnieżdżone.</span><span class="sxs-lookup"><span data-stu-id="74978-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="74978-236">Usuń hello *Azure Networking Analytics (przestarzały)* rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="74978-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="74978-237">Jeśli używasz programu PowerShell, użyj`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="74978-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="74978-238">Dane zbierane przed hello zmiany nie jest widoczna w hello nowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="74978-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="74978-239">Możesz kontynuować tooquery dla tego danych przy użyciu hello stary typ i nazwy pola.</span><span class="sxs-lookup"><span data-stu-id="74978-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="74978-240">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="74978-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="74978-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74978-241">Next steps</span></span>
* <span data-ttu-id="74978-242">Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane diagnostyczne platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="74978-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
