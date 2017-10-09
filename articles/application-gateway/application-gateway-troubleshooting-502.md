---
title: "błędy nieprawidłowych brama bramy aplikacji Azure (502) aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy tootroubleshoot 502 bramy aplikacji"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="75fe0-103">Rozwiązywanie problemów z błędami Zła brama bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="75fe0-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="75fe0-104">Dowiedz się, jak tootroubleshoot zły bramy (502) błędy odebrane podczas korzystania z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75fe0-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="75fe0-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="75fe0-105">Overview</span></span>

<span data-ttu-id="75fe0-106">Po skonfigurowaniu bramy aplikacji, jeden z użytkowników mogą wystąpić błędy hello jest "Błąd serwera: 502 — Serwer sieci Web odebrał nieprawidłową odpowiedź działając jako brama lub serwer proxy".</span><span class="sxs-lookup"><span data-stu-id="75fe0-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="75fe0-107">Ten błąd może się tak zdarzyć powodu toohello następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="75fe0-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="75fe0-108">Azure bramy aplikacji [puli zaplecza nie jest skonfigurowany lub pusty](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="75fe0-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="75fe0-109">Brak maszyn wirtualnych hello lub wystąpień w [zestawu skali maszyny Wirtualnej są w dobrej kondycji](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="75fe0-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="75fe0-110">Maszyny wirtualne zaplecza lub wystąpienia zestawu skali maszyny Wirtualnej są [nie odpowiada toohello domyślnej funkcji badania kondycji](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="75fe0-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="75fe0-111">Nieprawidłowy lub niewłaściwego [konfiguracji sondy kondycji niestandardowych](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="75fe0-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="75fe0-112">[Żądania limitu czasu lub problemów z łącznością](#request-time-out) z żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75fe0-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="75fe0-113">Pusty BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="75fe0-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="75fe0-114">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="75fe0-114">Cause</span></span>

<span data-ttu-id="75fe0-115">Jeśli hello bramy aplikacji nie ma żadnych maszyn wirtualnych lub zestawu skali maszyny Wirtualnej skonfigurowana w puli adresów zaplecza hello, nie można przekierować wszystkie żądania klienta i zgłasza błąd zły bramy.</span><span class="sxs-lookup"><span data-stu-id="75fe0-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="75fe0-116">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="75fe0-116">Solution</span></span>

<span data-ttu-id="75fe0-117">Upewnij się, czy pula adresów zaplecza hello nie jest pusta.</span><span class="sxs-lookup"><span data-stu-id="75fe0-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="75fe0-118">Można to zrobić za pośrednictwem programu PowerShell, interfejsu wiersza polecenia lub portalu.</span><span class="sxs-lookup"><span data-stu-id="75fe0-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="75fe0-119">dane wyjściowe Hello hello poprzedzających polecenia cmdlet powinny zawierać puli adresów zaplecza niepusty.</span><span class="sxs-lookup"><span data-stu-id="75fe0-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="75fe0-120">Poniżej przedstawiono przykładowy, w których dwie pule są zwracane które są skonfigurowane przy użyciu nazwy FQDN lub adresów IP dla maszyn wirtualnych w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="75fe0-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="75fe0-121">Witaj stan inicjowania obsługi administracyjnej hello BackendAddressPool musi mieć wartość "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="75fe0-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="75fe0-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="75fe0-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="75fe0-123">Zła wystąpień w BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="75fe0-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="75fe0-124">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="75fe0-124">Cause</span></span>

<span data-ttu-id="75fe0-125">Jeśli wszystkie wystąpienia hello BackendAddressPool jest zła, następnie bramy aplikacji nie będzie zawierało wszystkie żądania użytkownika tooroute zaplecza w celu.</span><span class="sxs-lookup"><span data-stu-id="75fe0-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="75fe0-126">Przyczyną może być również przypadku hello wystąpień zaplecza są w dobrej kondycji, ale nie ma wdrożonych aplikacji hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="75fe0-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="75fe0-127">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="75fe0-127">Solution</span></span>

<span data-ttu-id="75fe0-128">Sprawdź, czy wystąpienia hello są w dobrej kondycji i aplikacja hello jest skonfigurowana prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="75fe0-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="75fe0-129">Sprawdź stanie toorespond tooa ping z inną maszynę Wirtualną w przypadku wystąpień zaplecza hello hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="75fe0-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="75fe0-130">Skonfigurowano publiczny punkt końcowy, upewnij się, że aplikacja sieci web toohello żądanie przeglądarki jest obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="75fe0-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="75fe0-131">Problemy z domyślnej funkcji badania kondycji</span><span class="sxs-lookup"><span data-stu-id="75fe0-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="75fe0-132">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="75fe0-132">Cause</span></span>

<span data-ttu-id="75fe0-133">błędy 502 można też częste wskaźników, które hello domyślnej funkcji badania kondycji jest nie jest w stanie tooreach zaplecza maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="75fe0-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="75fe0-134">Po zainicjowaniu obsługi wystąpienia bramy aplikacji, automatycznie konfiguruje domyślne tooeach sondy kondycji BackendAddressPool przy użyciu właściwości hello BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="75fe0-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="75fe0-135">Nie danych wprowadzonych przez użytkownika jest wymagana tooset sonda.</span><span class="sxs-lookup"><span data-stu-id="75fe0-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="75fe0-136">W szczególności w przypadku skonfigurowania reguły równoważenia obciążenia, skojarzenie jest nawiązywane pomiędzy BackendHttpSetting i BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="75fe0-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="75fe0-137">Dla każdego z tych skojarzenia i inicjuje brama aplikacji w wystąpieniu okresowego sprawdzania połączenia tooeach w hello BackendAddressPool portu hello określony w elemencie BackendHttpSetting hello skonfigurowano domyślnego badania.</span><span class="sxs-lookup"><span data-stu-id="75fe0-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="75fe0-138">Poniższa tabela zawiera listę wartości hello skojarzone z hello domyślnej funkcji badania kondycji.</span><span class="sxs-lookup"><span data-stu-id="75fe0-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="75fe0-139">Właściwość sondy</span><span class="sxs-lookup"><span data-stu-id="75fe0-139">Probe property</span></span> | <span data-ttu-id="75fe0-140">Wartość</span><span class="sxs-lookup"><span data-stu-id="75fe0-140">Value</span></span> | <span data-ttu-id="75fe0-141">Opis</span><span class="sxs-lookup"><span data-stu-id="75fe0-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="75fe0-142">Sonda adresu URL</span><span class="sxs-lookup"><span data-stu-id="75fe0-142">Probe URL</span></span> |<span data-ttu-id="75fe0-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="75fe0-143">http://127.0.0.1/</span></span> |<span data-ttu-id="75fe0-144">Ścieżka adresu URL</span><span class="sxs-lookup"><span data-stu-id="75fe0-144">URL path</span></span> |
| <span data-ttu-id="75fe0-145">Interwał</span><span class="sxs-lookup"><span data-stu-id="75fe0-145">Interval</span></span> |<span data-ttu-id="75fe0-146">30</span><span class="sxs-lookup"><span data-stu-id="75fe0-146">30</span></span> |<span data-ttu-id="75fe0-147">Interwał sondowania w sekundach</span><span class="sxs-lookup"><span data-stu-id="75fe0-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="75fe0-148">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="75fe0-148">Time-out</span></span> |<span data-ttu-id="75fe0-149">30</span><span class="sxs-lookup"><span data-stu-id="75fe0-149">30</span></span> |<span data-ttu-id="75fe0-150">Sonda limitu czasu w sekundach</span><span class="sxs-lookup"><span data-stu-id="75fe0-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="75fe0-151">Próg złej kondycji</span><span class="sxs-lookup"><span data-stu-id="75fe0-151">Unhealthy threshold</span></span> |<span data-ttu-id="75fe0-152">3</span><span class="sxs-lookup"><span data-stu-id="75fe0-152">3</span></span> |<span data-ttu-id="75fe0-153">Badania liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="75fe0-153">Probe retry count.</span></span> <span data-ttu-id="75fe0-154">serwera zaplecza Hello jest oznaczony w dół po licznik awarii kolejnych sondowania hello osiągnie hello próg złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="75fe0-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="75fe0-155">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="75fe0-155">Solution</span></span>

* <span data-ttu-id="75fe0-156">Upewnij się, że domyślna witryna jest skonfigurowana i prowadzi nasłuchiwanie na 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="75fe0-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="75fe0-157">Jeśli BackendHttpSetting Określa port inny niż 80, hello domyślnej witryny powinny być skonfigurowane toolisten na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="75fe0-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="75fe0-158">Witaj toohttp://127.0.0.1:port wywołania powinna zwrócić kod wyniku protokołu HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="75fe0-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="75fe0-159">To powinien być zwracany w hello 30 sekund limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="75fe0-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="75fe0-160">Upewnij się, że skonfigurowany port jest otwarty i czy nie ma żadnych reguł zapory lub grup zabezpieczeń sieci Azure, która zablokować przychodzący lub wychodzący ruch na porcie hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="75fe0-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="75fe0-161">Jeśli klasyczne maszyny wirtualne platformy Azure lub usługi w chmurze jest używana z nazwy FQDN lub publicznego adresu IP, upewnij się, hello odpowiadającego [punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="75fe0-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="75fe0-162">Jeśli hello maszyna wirtualna jest skonfigurowana za pośrednictwem usługi Azure Resource Manager i znajduje się poza hello sieci wirtualnej, w której wdrażana jest aplikacja bramy, [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) musi być skonfigurowany dostęp tooallow na powitania żądany port.</span><span class="sxs-lookup"><span data-stu-id="75fe0-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="75fe0-163">Problemy z sondy kondycji niestandardowych</span><span class="sxs-lookup"><span data-stu-id="75fe0-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="75fe0-164">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="75fe0-164">Cause</span></span>

<span data-ttu-id="75fe0-165">Sondy kondycji niestandardowe umożliwiają sondowanie zachowanie domyślne toohello dodatkowa elastyczność.</span><span class="sxs-lookup"><span data-stu-id="75fe0-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="75fe0-166">Podczas korzystania z niestandardowego sond, użytkownicy mogą skonfigurować interwał sondowania powitania, hello adres URL i tootest ścieżkę oraz ile tooaccept odpowiedzi nie powiodło się przed oznaczeniem wystąpienia puli zaplecza hello swój stan jako niezdrowy.</span><span class="sxs-lookup"><span data-stu-id="75fe0-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="75fe0-167">dodano następujące dodatkowe właściwości Hello.</span><span class="sxs-lookup"><span data-stu-id="75fe0-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="75fe0-168">Właściwość sondy</span><span class="sxs-lookup"><span data-stu-id="75fe0-168">Probe property</span></span> | <span data-ttu-id="75fe0-169">Opis</span><span class="sxs-lookup"><span data-stu-id="75fe0-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75fe0-170">Nazwa</span><span class="sxs-lookup"><span data-stu-id="75fe0-170">Name</span></span> |<span data-ttu-id="75fe0-171">Nazwa sondy hello.</span><span class="sxs-lookup"><span data-stu-id="75fe0-171">Name of hello probe.</span></span> <span data-ttu-id="75fe0-172">Ta nazwa jest sonda toohello toorefer używane ustawienia HTTP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="75fe0-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="75fe0-173">Protokół</span><span class="sxs-lookup"><span data-stu-id="75fe0-173">Protocol</span></span> |<span data-ttu-id="75fe0-174">Protokół używany toosend hello sondowania.</span><span class="sxs-lookup"><span data-stu-id="75fe0-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="75fe0-175">Sonda Hello używa protokołu hello zdefiniowanego w ustawieniach protokołu HTTP zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="75fe0-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="75fe0-176">Host</span><span class="sxs-lookup"><span data-stu-id="75fe0-176">Host</span></span> |<span data-ttu-id="75fe0-177">Sonda hello toosend nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="75fe0-177">Host name toosend hello probe.</span></span> <span data-ttu-id="75fe0-178">Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75fe0-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="75fe0-179">To jest inna niż nazwa hosta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="75fe0-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="75fe0-180">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="75fe0-180">Path</span></span> |<span data-ttu-id="75fe0-181">Ścieżka względna hello sondy.</span><span class="sxs-lookup"><span data-stu-id="75fe0-181">Relative path of hello probe.</span></span> <span data-ttu-id="75fe0-182">prawidłowa ścieżka Hello rozpoczyna się od '/'.</span><span class="sxs-lookup"><span data-stu-id="75fe0-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="75fe0-183">Sonda Hello są wysyłane za\<protokołu\>://\<hosta\>:\<portu\>\<ścieżki\></span><span class="sxs-lookup"><span data-stu-id="75fe0-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="75fe0-184">Interwał</span><span class="sxs-lookup"><span data-stu-id="75fe0-184">Interval</span></span> |<span data-ttu-id="75fe0-185">Interwał sondy w sekundach.</span><span class="sxs-lookup"><span data-stu-id="75fe0-185">Probe interval in seconds.</span></span> <span data-ttu-id="75fe0-186">Jest to hello odstęp czasu między dwa kolejne sondy.</span><span class="sxs-lookup"><span data-stu-id="75fe0-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="75fe0-187">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="75fe0-187">Time-out</span></span> |<span data-ttu-id="75fe0-188">Badania limitu czasu w sekundach.</span><span class="sxs-lookup"><span data-stu-id="75fe0-188">Probe time-out in seconds.</span></span> <span data-ttu-id="75fe0-189">Jeśli w tym czasie limitu czasu nie odebrano prawidłowej odpowiedzi, hello sondowania jest oznaczony jako nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="75fe0-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="75fe0-190">Próg złej kondycji</span><span class="sxs-lookup"><span data-stu-id="75fe0-190">Unhealthy threshold</span></span> |<span data-ttu-id="75fe0-191">Badania liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="75fe0-191">Probe retry count.</span></span> <span data-ttu-id="75fe0-192">serwera zaplecza Hello jest oznaczony w dół po licznik awarii kolejnych sondowania hello osiągnie hello próg złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="75fe0-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="75fe0-193">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="75fe0-193">Solution</span></span>

<span data-ttu-id="75fe0-194">Sprawdź poprawność tego powitalne sondy kondycji niestandardowy jest poprawnie skonfigurowany jako hello powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="75fe0-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="75fe0-195">Ponadto toohello powyższych czynności, upewnij się również hello następujące:</span><span class="sxs-lookup"><span data-stu-id="75fe0-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="75fe0-196">Upewnij się, że sonda hello została poprawnie określona zgodnie z harmonogramem hello [przewodnik](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="75fe0-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="75fe0-197">Jeśli skonfigurowano brama aplikacji w jednej lokacji, przez domyślny hello hosta należy określać nazwy jako "127.0.0.1", chyba że w przeciwnym razie skonfigurowane w niestandardowych sondowania.</span><span class="sxs-lookup"><span data-stu-id="75fe0-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="75fe0-198">Upewnij się, że toohttp wywołania: / /\<hosta\>:\<portu\>\<ścieżki\> zwraca kod wyniku protokołu HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="75fe0-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="75fe0-199">Upewnij się, czy interwału limitu czasu i UnhealtyThreshold znajduje się w dopuszczalnych zakresach hello.</span><span class="sxs-lookup"><span data-stu-id="75fe0-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="75fe0-200">Jeśli sondowania przy użyciu protokołu HTTPS, upewnij się, że ten powitania serwera wewnętrznej bazy danych nie wymaga SNI przez skonfigurowanie certyfikat fallback na powitania serwera wewnętrznej bazy danych, sama.</span><span class="sxs-lookup"><span data-stu-id="75fe0-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="75fe0-201">Upewnij się, czy interwał limitu czasu i UnhealtyThreshold znajduje się w dopuszczalnych zakresach hello.</span><span class="sxs-lookup"><span data-stu-id="75fe0-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="75fe0-202">Upłynął limit czasu żądania</span><span class="sxs-lookup"><span data-stu-id="75fe0-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="75fe0-203">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="75fe0-203">Cause</span></span>

<span data-ttu-id="75fe0-204">Po odebraniu żądania użytkownika bramy aplikacji stosuje hello skonfigurowane reguły toohello żądania i kieruje je tooa puli zaplecza wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="75fe0-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="75fe0-205">Oczekuje na można skonfigurować interwał czasu odpowiedzi z hello zaplecza wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="75fe0-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="75fe0-206">Domyślnie jest to interwał **30 sekund**.</span><span class="sxs-lookup"><span data-stu-id="75fe0-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="75fe0-207">Jeśli bramy aplikacji nie otrzymują odpowiedź z zaplecza aplikacji w tym interwał, zobaczyć 502 Błąd żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75fe0-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="75fe0-208">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="75fe0-208">Solution</span></span>

<span data-ttu-id="75fe0-209">Brama aplikacji w umożliwia użytkownikom tooconfigure ustawienie BackendHttpSetting, który może być, a następnie zastosować toodifferent pule.</span><span class="sxs-lookup"><span data-stu-id="75fe0-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="75fe0-210">Różnych pul zaplecza może mieć różne BackendHttpSetting i skonfigurowany limit czasu dlatego innego żądania.</span><span class="sxs-lookup"><span data-stu-id="75fe0-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="75fe0-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="75fe0-211">Next steps</span></span>

<span data-ttu-id="75fe0-212">Jeśli hello powyższych kroków nie rozwiąże problemu hello, otwórz [obsługuje biletu](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="75fe0-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

