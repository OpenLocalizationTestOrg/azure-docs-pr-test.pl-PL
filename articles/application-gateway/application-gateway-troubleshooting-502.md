---
title: "Rozwiązywanie problemów zły brama bramy aplikacji Azure (502) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązać problemy z błędami 502 bramy aplikacji"
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="bd735-103">Rozwiązywanie problemów z błędami Zła brama bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="bd735-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="bd735-104">Dowiedz się, jak rozwiązywać problemy z błędów zły bramy (502) podczas używania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd735-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="bd735-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bd735-105">Overview</span></span>

<span data-ttu-id="bd735-106">Po skonfigurowaniu bramy aplikacji, jest jeden z błędów, które użytkownicy mogą wystąpić "Błąd serwera: 502 — Serwer sieci Web odebrał nieprawidłową odpowiedź działając jako brama lub serwer proxy".</span><span class="sxs-lookup"><span data-stu-id="bd735-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="bd735-107">Ten błąd może się zdarzyć z powodu następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="bd735-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="bd735-108">Azure bramy aplikacji [puli zaplecza nie jest skonfigurowany lub pusty](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="bd735-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="bd735-109">Żadna z maszyn wirtualnych i wystąpień w [zestawu skali maszyny Wirtualnej są w dobrej kondycji](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="bd735-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="bd735-110">Maszyny wirtualne zaplecza lub wystąpienia zestawu skali maszyny Wirtualnej są [nie odpowiada na domyślnej sondy kondycji](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="bd735-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="bd735-111">Nieprawidłowy lub niewłaściwego [konfiguracji sondy kondycji niestandardowych](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="bd735-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="bd735-112">[Żądania limitu czasu lub problemów z łącznością](#request-time-out) z żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd735-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="bd735-113">Pusty BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="bd735-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="bd735-114">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="bd735-114">Cause</span></span>

<span data-ttu-id="bd735-115">Jeśli bramy aplikacji nie ma maszyn wirtualnych ani skonfigurowana w puli adresów zaplecza zestawu skali maszyny Wirtualnej, nie można przekierować wszystkie żądania klienta i zgłasza błąd zły bramy.</span><span class="sxs-lookup"><span data-stu-id="bd735-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="bd735-116">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="bd735-116">Solution</span></span>

<span data-ttu-id="bd735-117">Upewnij się, że pula adresów zaplecza nie jest pusty.</span><span class="sxs-lookup"><span data-stu-id="bd735-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="bd735-118">Można to zrobić za pośrednictwem programu PowerShell, interfejsu wiersza polecenia lub portalu.</span><span class="sxs-lookup"><span data-stu-id="bd735-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="bd735-119">Dane wyjściowe z poprzedniego polecenia cmdlet powinny zawierać puli adresów zaplecza niepusta.</span><span class="sxs-lookup"><span data-stu-id="bd735-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="bd735-120">Poniżej przedstawiono przykładowy, w których dwie pule są zwracane które są skonfigurowane przy użyciu nazwy FQDN lub adresów IP dla maszyn wirtualnych w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bd735-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="bd735-121">Stan inicjowania obsługi administracyjnej BackendAddressPool musi mieć wartość "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="bd735-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="bd735-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="bd735-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="bd735-123">Zła wystąpień w BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="bd735-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="bd735-124">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="bd735-124">Cause</span></span>

<span data-ttu-id="bd735-125">Jeśli wszystkie wystąpienia BackendAddressPool jest zła, następnie bramy aplikacji nie będzie zawierało dowolnego zaplecza na żądanie użytkownika trasy.</span><span class="sxs-lookup"><span data-stu-id="bd735-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="bd735-126">Przyczyną może być również wielkość liter podczas wystąpień zaplecza są w dobrej kondycji, ale nie ma wymaganej aplikacji, które są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="bd735-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="bd735-127">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="bd735-127">Solution</span></span>

<span data-ttu-id="bd735-128">Upewnij się, że wystąpienia są w dobrej kondycji i aplikacja jest poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="bd735-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="bd735-129">Sprawdź, czy wystąpienia zaplecza są odpowiada na polecenia ping z innej maszyny Wirtualnej w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd735-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="bd735-130">Jeśli skonfigurowano publiczny punkt końcowy, upewnij się, że żądanie przeglądarki do aplikacji sieci web jest obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="bd735-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="bd735-131">Problemy z domyślnej funkcji badania kondycji</span><span class="sxs-lookup"><span data-stu-id="bd735-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="bd735-132">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="bd735-132">Cause</span></span>

<span data-ttu-id="bd735-133">błędy 502 można także częste wskaźniki domyślnej funkcji badania kondycji nie jest możliwe nawiązanie łączności zaplecza maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="bd735-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="bd735-134">Po zainicjowaniu obsługi wystąpienia bramy aplikacji, automatycznie konfiguruje domyślne badanie kondycji do każdego BackendAddressPool przy użyciu właściwości BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="bd735-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="bd735-135">Dane wejściowe użytkownika nie jest wymagane do ustawienia tej sondy.</span><span class="sxs-lookup"><span data-stu-id="bd735-135">No user input is required to set this probe.</span></span> <span data-ttu-id="bd735-136">W szczególności w przypadku skonfigurowania reguły równoważenia obciążenia, skojarzenie jest nawiązywane pomiędzy BackendHttpSetting i BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="bd735-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="bd735-137">Domyślne badanie jest skonfigurowany dla każdego skojarzenia i brama aplikacji w inicjuje połączenie wyboru okresowego do każdego wystąpienia w BackendAddressPool na port określony w elemencie BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="bd735-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="bd735-138">Poniższa tabela zawiera listę wartości skojarzone z domyślnej funkcji badania kondycji.</span><span class="sxs-lookup"><span data-stu-id="bd735-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="bd735-139">Właściwość sondy</span><span class="sxs-lookup"><span data-stu-id="bd735-139">Probe property</span></span> | <span data-ttu-id="bd735-140">Wartość</span><span class="sxs-lookup"><span data-stu-id="bd735-140">Value</span></span> | <span data-ttu-id="bd735-141">Opis</span><span class="sxs-lookup"><span data-stu-id="bd735-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd735-142">Sonda adresu URL</span><span class="sxs-lookup"><span data-stu-id="bd735-142">Probe URL</span></span> |<span data-ttu-id="bd735-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="bd735-143">http://127.0.0.1/</span></span> |<span data-ttu-id="bd735-144">Ścieżka adresu URL</span><span class="sxs-lookup"><span data-stu-id="bd735-144">URL path</span></span> |
| <span data-ttu-id="bd735-145">Interwał</span><span class="sxs-lookup"><span data-stu-id="bd735-145">Interval</span></span> |<span data-ttu-id="bd735-146">30</span><span class="sxs-lookup"><span data-stu-id="bd735-146">30</span></span> |<span data-ttu-id="bd735-147">Interwał sondowania w sekundach</span><span class="sxs-lookup"><span data-stu-id="bd735-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="bd735-148">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="bd735-148">Time-out</span></span> |<span data-ttu-id="bd735-149">30</span><span class="sxs-lookup"><span data-stu-id="bd735-149">30</span></span> |<span data-ttu-id="bd735-150">Sonda limitu czasu w sekundach</span><span class="sxs-lookup"><span data-stu-id="bd735-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="bd735-151">Próg złej kondycji</span><span class="sxs-lookup"><span data-stu-id="bd735-151">Unhealthy threshold</span></span> |<span data-ttu-id="bd735-152">3</span><span class="sxs-lookup"><span data-stu-id="bd735-152">3</span></span> |<span data-ttu-id="bd735-153">Badania liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="bd735-153">Probe retry count.</span></span> <span data-ttu-id="bd735-154">Po kolejnych sondowania liczby awarii osiągnie próg złej kondycji serwera zaplecza jest oznaczony jako w dół.</span><span class="sxs-lookup"><span data-stu-id="bd735-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="bd735-155">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="bd735-155">Solution</span></span>

* <span data-ttu-id="bd735-156">Upewnij się, że domyślna witryna jest skonfigurowana i prowadzi nasłuchiwanie na 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="bd735-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="bd735-157">Jeśli BackendHttpSetting Określa port inny niż 80, należy skonfigurować domyślną witrynę do nasłuchiwania na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="bd735-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="bd735-158">Wywołanie http://127.0.0.1:port powinien zwrócić 200 kod wyniku HTTP.</span><span class="sxs-lookup"><span data-stu-id="bd735-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="bd735-159">Powinna to być zwrócona w ciągu 30 sekund limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="bd735-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="bd735-160">Upewnij się, że skonfigurowany port jest otwarty i czy nie ma żadnych reguł zapory lub grup zabezpieczeń sieci Azure, która zablokować ruch przychodzący lub wychodzący na porcie skonfigurowanym.</span><span class="sxs-lookup"><span data-stu-id="bd735-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="bd735-161">Jeśli klasyczne maszyny wirtualne platformy Azure lub usługi w chmurze jest używana nazwa FQDN lub publicznego adresu IP, upewnij się, że odpowiednie [punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="bd735-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="bd735-162">Jeśli maszyna wirtualna jest skonfigurowana za pośrednictwem usługi Azure Resource Manager i jest spoza sieci wirtualnej, w której wdrażana jest aplikacja bramy, [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) musi być skonfigurowane i umożliwiają dostęp do wybranego portu.</span><span class="sxs-lookup"><span data-stu-id="bd735-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="bd735-163">Problemy z sondy kondycji niestandardowych</span><span class="sxs-lookup"><span data-stu-id="bd735-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="bd735-164">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="bd735-164">Cause</span></span>

<span data-ttu-id="bd735-165">Sondy kondycji niestandardowe umożliwiają dodatkowa elastyczność sondowanie zachowanie domyślne.</span><span class="sxs-lookup"><span data-stu-id="bd735-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="bd735-166">Podczas korzystania z niestandardowego sond, użytkownicy mogą skonfigurować interwał sondowania, adres URL i ścieżki do testowania i ile odpowiedzi nie powiodło się do akceptowania przed oznaczeniem wystąpienia puli zaplecza swój stan jako niezdrowy.</span><span class="sxs-lookup"><span data-stu-id="bd735-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="bd735-167">Zostaną dodane następujące dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="bd735-167">The following additional properties are added.</span></span>

| <span data-ttu-id="bd735-168">Właściwość sondy</span><span class="sxs-lookup"><span data-stu-id="bd735-168">Probe property</span></span> | <span data-ttu-id="bd735-169">Opis</span><span class="sxs-lookup"><span data-stu-id="bd735-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bd735-170">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bd735-170">Name</span></span> |<span data-ttu-id="bd735-171">Nazwa sondy.</span><span class="sxs-lookup"><span data-stu-id="bd735-171">Name of the probe.</span></span> <span data-ttu-id="bd735-172">Ta nazwa jest używana do odwoływania się do sondowania w ustawieniach protokołu HTTP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bd735-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="bd735-173">Protokół</span><span class="sxs-lookup"><span data-stu-id="bd735-173">Protocol</span></span> |<span data-ttu-id="bd735-174">Protokół używany do wysyłania sondy.</span><span class="sxs-lookup"><span data-stu-id="bd735-174">Protocol used to send the probe.</span></span> <span data-ttu-id="bd735-175">Sonda korzysta z protokołu zdefiniowanego w ustawieniach protokołu HTTP zaplecza</span><span class="sxs-lookup"><span data-stu-id="bd735-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="bd735-176">Host</span><span class="sxs-lookup"><span data-stu-id="bd735-176">Host</span></span> |<span data-ttu-id="bd735-177">Nazwa hosta, aby wysłać sondy.</span><span class="sxs-lookup"><span data-stu-id="bd735-177">Host name to send the probe.</span></span> <span data-ttu-id="bd735-178">Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd735-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="bd735-179">To jest inna niż nazwa hosta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd735-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="bd735-180">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="bd735-180">Path</span></span> |<span data-ttu-id="bd735-181">Ścieżka względna sondy.</span><span class="sxs-lookup"><span data-stu-id="bd735-181">Relative path of the probe.</span></span> <span data-ttu-id="bd735-182">Nieprawidłowa ścieżka rozpoczyna się od '/'.</span><span class="sxs-lookup"><span data-stu-id="bd735-182">The valid path starts from '/'.</span></span> <span data-ttu-id="bd735-183">Sonda są wysyłane do \<protokołu\>://\<hosta\>:\<portu\>\<ścieżki\></span><span class="sxs-lookup"><span data-stu-id="bd735-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="bd735-184">Interwał</span><span class="sxs-lookup"><span data-stu-id="bd735-184">Interval</span></span> |<span data-ttu-id="bd735-185">Interwał sondy w sekundach.</span><span class="sxs-lookup"><span data-stu-id="bd735-185">Probe interval in seconds.</span></span> <span data-ttu-id="bd735-186">Jest to odstęp czasu między dwa kolejne sondy.</span><span class="sxs-lookup"><span data-stu-id="bd735-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="bd735-187">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="bd735-187">Time-out</span></span> |<span data-ttu-id="bd735-188">Badania limitu czasu w sekundach.</span><span class="sxs-lookup"><span data-stu-id="bd735-188">Probe time-out in seconds.</span></span> <span data-ttu-id="bd735-189">Jeśli w tym czasie limitu czasu nie odebrano prawidłowej odpowiedzi, sondy jest oznaczony jako nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="bd735-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="bd735-190">Próg złej kondycji</span><span class="sxs-lookup"><span data-stu-id="bd735-190">Unhealthy threshold</span></span> |<span data-ttu-id="bd735-191">Badania liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="bd735-191">Probe retry count.</span></span> <span data-ttu-id="bd735-192">Po kolejnych sondowania liczby awarii osiągnie próg złej kondycji serwera zaplecza jest oznaczony jako w dół.</span><span class="sxs-lookup"><span data-stu-id="bd735-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="bd735-193">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="bd735-193">Solution</span></span>

<span data-ttu-id="bd735-194">Zweryfikuj, że sondy kondycji niestandardowy jest skonfigurowana jako powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="bd735-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="bd735-195">Oprócz powyższych kroków upewnij się również następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd735-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="bd735-196">Upewnij się, że sondy została poprawnie określona w [przewodnik](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bd735-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="bd735-197">Jeśli skonfigurowano brama aplikacji w jednej lokacji, domyślnie hosta należy określać nazwy jako "127.0.0.1", chyba że w przeciwnym razie skonfigurowane w niestandardowych sondowania.</span><span class="sxs-lookup"><span data-stu-id="bd735-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="bd735-198">Upewnij się, że wywołanie http://\<hosta\>:\<portu\>\<ścieżki\> zwraca kod wyniku protokołu HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="bd735-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="bd735-199">Upewnij się, że interwału limitu czasu i UnhealtyThreshold są dopuszczalne zakresy.</span><span class="sxs-lookup"><span data-stu-id="bd735-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="bd735-200">Jeśli przy użyciu sondy protokołu HTTPS, upewnij się, że serwer wewnętrznej bazy danych nie wymaga SNI przez skonfigurowanie rezerwowy certyfikatu na serwerze wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bd735-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="bd735-201">Upewnij się, czy interwał limitu czasu i UnhealtyThreshold znajduje się w dopuszczalnych zakresach.</span><span class="sxs-lookup"><span data-stu-id="bd735-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="bd735-202">Upłynął limit czasu żądania</span><span class="sxs-lookup"><span data-stu-id="bd735-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="bd735-203">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="bd735-203">Cause</span></span>

<span data-ttu-id="bd735-204">Po odebraniu żądania użytkownika bramy aplikacji stosuje skonfigurowanych reguł do żądania i kieruje je do wystąpienia puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bd735-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="bd735-205">Oczekuje na można skonfigurować interwał czasu odpowiedzi z wystąpienia zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bd735-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="bd735-206">Domyślnie jest to interwał **30 sekund**.</span><span class="sxs-lookup"><span data-stu-id="bd735-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="bd735-207">Jeśli bramy aplikacji nie otrzymują odpowiedź z zaplecza aplikacji w tym interwał, zobaczyć 502 Błąd żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd735-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="bd735-208">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="bd735-208">Solution</span></span>

<span data-ttu-id="bd735-209">Brama aplikacji umożliwia użytkownikom tego ustawienia za pomocą BackendHttpSetting, które mogą być następnie stosowane do różnych pul.</span><span class="sxs-lookup"><span data-stu-id="bd735-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="bd735-210">Różnych pul zaplecza może mieć różne BackendHttpSetting i skonfigurowany limit czasu dlatego innego żądania.</span><span class="sxs-lookup"><span data-stu-id="bd735-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="bd735-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd735-211">Next steps</span></span>

<span data-ttu-id="bd735-212">Jeśli powyższe czynności nie rozwiązać ten problem, otwórz [obsługuje biletu](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="bd735-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

