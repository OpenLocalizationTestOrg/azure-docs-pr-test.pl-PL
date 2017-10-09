---
title: "aaaMonitor dostęp do dzienników, Dzienniki wydajności kondycji zaplecza i metryki bramy aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable i zarządzanie nimi Dzienniki wydajności i dzienników dostępu bramy aplikacji"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="850bb-103">Kondycji zaplecza, dzienniki diagnostyczne i metryki bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="850bb-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="850bb-104">Korzystając z bramy aplikacji Azure, można monitorować zasobów w hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="850bb-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="850bb-105">[Kondycja zaplecza](#back-end-health): Application Gateway udostępnia hello możliwości toomonitor hello kondycji serwerów hello w hello pul zaplecza za pośrednictwem hello portalu Azure i przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="850bb-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="850bb-106">Można również znaleźć kondycji hello hello pul zaplecza za pośrednictwem dzienników diagnostycznych hello wydajności.</span><span class="sxs-lookup"><span data-stu-id="850bb-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="850bb-107">[Dzienniki](#diagnostic-logs): dzienniki umożliwić wydajności, dostęp, i inne toobe dane zapisane lub używane z zasobu do celów monitorowania.</span><span class="sxs-lookup"><span data-stu-id="850bb-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="850bb-108">[Metryki](#metrics): jedna metryka ma obecnie Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="850bb-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="850bb-109">Ta metryka mierzy hello przepływność bramy aplikacji hello w bajtach na sekundę.</span><span class="sxs-lookup"><span data-stu-id="850bb-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="850bb-110">Kondycja zaplecza</span><span class="sxs-lookup"><span data-stu-id="850bb-110">Back-end health</span></span>

<span data-ttu-id="850bb-111">Brama aplikacji w zapewnia hello możliwości toomonitor hello kondycji poszczególnych członków hello pul zaplecza za pośrednictwem portalu hello, programu PowerShell i hello interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="850bb-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="850bb-112">Możesz również znaleźć zagregowane kondycji podsumowania pul zaplecza za pośrednictwem dzienników diagnostycznych hello wydajności.</span><span class="sxs-lookup"><span data-stu-id="850bb-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="850bb-113">Raport o kondycji zaplecza Hello odzwierciedla dane wyjściowe hello wystąpień hello bramy aplikacji kondycji sondowania toohello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="850bb-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="850bb-114">Podczas badania zakończy się pomyślnie i Witaj ponownie zakończenia mogą odbierać dane, jest on uznawany za dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="850bb-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="850bb-115">W przeciwnym razie jego jest określana jako zła.</span><span class="sxs-lookup"><span data-stu-id="850bb-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="850bb-116">Jeśli istnieje grupa zabezpieczeń sieci (NSG) w podsieci bramy aplikacji, otwórz zakresy portów 65503 65534 podsieci bramy aplikacji hello dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="850bb-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="850bb-117">Te porty są wymagane dla hello kondycji zaplecza interfejsu API toowork.</span><span class="sxs-lookup"><span data-stu-id="850bb-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="850bb-118">Wyświetl kondycję zaplecza za pośrednictwem portalu hello</span><span class="sxs-lookup"><span data-stu-id="850bb-118">View back-end health through hello portal</span></span>

<span data-ttu-id="850bb-119">W portalu hello kondycji zaplecza podano automatycznie.</span><span class="sxs-lookup"><span data-stu-id="850bb-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="850bb-120">Wybierz istniejącą bramę aplikacji **monitorowanie** > **kondycji zaplecza**.</span><span class="sxs-lookup"><span data-stu-id="850bb-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="850bb-121">Każdy element członkowski w puli zaplecza hello jest wymieniona na tej stronie (czy jest ona karty Sieciowej, adresu IP lub FQDN).</span><span class="sxs-lookup"><span data-stu-id="850bb-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="850bb-122">Nazwa puli zaplecza, portu, nazwy ustawienia HTTP zaplecza i stan kondycji są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="850bb-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="850bb-123">Prawidłowe wartości stanu kondycji to **dobra kondycja**, **niezdrowego**, i **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="850bb-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="850bb-124">Jeśli zostanie wyświetlony stan kondycji zaplecza **nieznany**, upewnij się, że dostępu toohello wewnętrznej bazy nie jest blokowane przez reguły NSG, trasy zdefiniowane przez użytkownika (przez) lub niestandardowe DNS w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Kondycja zaplecza][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="850bb-126">Wyświetl kondycję zaplecza za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="850bb-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="850bb-127">Hello następującego kodu programu PowerShell pokazuje, jak hello tooview kondycji zaplecza przy użyciu `Get-AzureRmApplicationGatewayBackendHealth` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="850bb-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="850bb-128">Wyświetl kondycję zaplecza za pośrednictwem 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="850bb-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="850bb-129">Wyniki</span><span class="sxs-lookup"><span data-stu-id="850bb-129">Results</span></span>

<span data-ttu-id="850bb-130">powitania po fragment kodu przedstawia przykład hello odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="850bb-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="850bb-131"><a name="diagnostic-logging"></a>Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="850bb-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="850bb-132">Można użyć różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="850bb-133">Niektóre z tych dzienników dostępne za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="850bb-134">Wszystkie dzienniki można wyodrębnić z magazynu obiektów Blob platformy Azure i wyświetlane w różnych narzędzi, takich jak [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md), Excel i Power BI.</span><span class="sxs-lookup"><span data-stu-id="850bb-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="850bb-135">Użytkownik może dowiedzieć się więcej o hello różne typy dzienników z następującej listy hello:</span><span class="sxs-lookup"><span data-stu-id="850bb-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="850bb-136">**Dziennik aktywności**: można użyć [Dzienniki aktywności Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (wcześniej znane jako dzienniki inspekcji i operacyjne dzienniki) tooview wszystkie operacje, które są przesyłane tooyour subskrypcji platformy Azure i ich stan.</span><span class="sxs-lookup"><span data-stu-id="850bb-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="850bb-137">Wpisy dziennika aktywności są zbierane domyślnie i można je przeglądać w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="850bb-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="850bb-138">**Dziennik dostępu**: można użyć wzorce dostępu do tego dziennika tooview bramy aplikacji i analizować i wylogowywanie ważne informacje, takie jak wywołującego hello IP żądanego adresu URL, czas oczekiwania na odpowiedź, kod powrotny i bajtów. Dziennik dostępu są gromadzone co 300 sekund.</span><span class="sxs-lookup"><span data-stu-id="850bb-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="850bb-139">Ten dziennik zawiera jeden rekord dla każdego wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="850bb-140">wystąpienie bramy aplikacji Hello można zidentyfikować przez właściwość instanceId hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="850bb-141">**Dziennik wydajności**: można użyć tego tooview dziennika, jak działają wystąpieniach bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="850bb-142">Ten dziennik zawiera informacje o wydajności dla każdego wystąpienia, w tym całkowita liczba żądań obsłużonych, przepływność w bajtach, całkowita liczba żądań obsłużonych, liczba nieudanych żądań, a liczba wystąpień zaplecza dobrej kondycji i złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="850bb-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="850bb-143">Dziennik wydajności są zbierane co 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="850bb-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="850bb-144">**Dziennik zapory**: można użyć tego dziennika tooview hello żądań, które są rejestrowane za pośrednictwem bramy aplikacji skonfigurowanej z zapory aplikacji sieci web hello Tryb wykrywania i zapobiegania.</span><span class="sxs-lookup"><span data-stu-id="850bb-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="850bb-145">Dzienniki są dostępne tylko w przypadku wdrożono w modelu wdrażania usługi Azure Resource Manager hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="850bb-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="850bb-146">Nie można używać dzienników zasobów w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="850bb-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="850bb-147">Aby lepiej zrozumieć hello dwa modele, zobacz hello [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="850bb-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="850bb-148">Są trzy opcje do przechowywania dzienników:</span><span class="sxs-lookup"><span data-stu-id="850bb-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="850bb-149">**Konto magazynu**: konta magazynu są najlepiej nadaje się do dzienników podczas dzienniki są przechowywane przez dłuższy czas i sprawdzić, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="850bb-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="850bb-150">**Centra zdarzeń**: Event hubs to doskonałe rozwiązanie dla integracji z innych informacji o zabezpieczeniach i narzędzi do zarządzania zdarzenia (SEIM) tooget alertów dotyczących zasobów.</span><span class="sxs-lookup"><span data-stu-id="850bb-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="850bb-151">**Zaloguj się Analytics**: analizy dzienników najlepiej nadaje się do ogólnego monitorowania w czasie rzeczywistym aplikacji lub analizowania trendów.</span><span class="sxs-lookup"><span data-stu-id="850bb-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="850bb-152">Włącz rejestrowanie za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="850bb-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="850bb-153">Rejestrowanie aktywności jest automatycznie włączona dla każdego zasobu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="850bb-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="850bb-154">Należy włączyć dostęp i toostart rejestrowania wydajności zbierania danych hello dostępne za pośrednictwem tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="850bb-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="850bb-155">tooenable rejestrowanie użycia hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="850bb-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="850bb-156">Należy zwrócić uwagę identyfikatorów zasobów konta magazynu, w którym są przechowywane dane dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="850bb-157">Ta wartość ma formę hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<Nazwa grupy zasobów\>/providers/Microsoft.Storage/storageAccounts/\<nazwy konta magazynu\>.</span><span class="sxs-lookup"><span data-stu-id="850bb-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="850bb-158">Można użyć dowolnego konta magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="850bb-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="850bb-159">Witaj toofind portalu Azure można użyć tych informacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portalu: identyfikator zasobu dla konta magazynu](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="850bb-161">Należy pamiętać, dla którego włączono rejestrowanie identyfikator zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="850bb-162">Ta wartość ma formę hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<Nazwa grupy zasobów\>/providers/Microsoft.Network/applicationGateways/\<bramy aplikacji Nazwa\>.</span><span class="sxs-lookup"><span data-stu-id="850bb-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="850bb-163">Witaj toofind portalu można użyć tych informacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-163">You can use hello portal toofind this information.</span></span>

    ![Portalu: identyfikator zasobu bramy aplikacji](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="850bb-165">Włącz rejestrowanie diagnostyczne za pomocą następującego polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="850bb-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="850bb-166">Dzienniki aktywności nie wymagają oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="850bb-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="850bb-167">Użycie Hello magazynu do dostępu do rejestrowania i wydajności wiąże opłaty za usługę.</span><span class="sxs-lookup"><span data-stu-id="850bb-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="850bb-168">Włącz rejestrowanie za pośrednictwem hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="850bb-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="850bb-169">Witaj portalu Azure, Znajdź zasobu i kliknij przycisk **dzienniki diagnostyczne**.</span><span class="sxs-lookup"><span data-stu-id="850bb-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="850bb-170">Brama aplikacji dostępne są trzy dzienniki:</span><span class="sxs-lookup"><span data-stu-id="850bb-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="850bb-171">Dziennik dostępu</span><span class="sxs-lookup"><span data-stu-id="850bb-171">Access log</span></span>
   * <span data-ttu-id="850bb-172">Dziennika wydajności</span><span class="sxs-lookup"><span data-stu-id="850bb-172">Performance log</span></span>
   * <span data-ttu-id="850bb-173">Dziennik zapory</span><span class="sxs-lookup"><span data-stu-id="850bb-173">Firewall log</span></span>

2. <span data-ttu-id="850bb-174">toostart zbierania danych, kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="850bb-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Włączanie diagnostyki][1]

3. <span data-ttu-id="850bb-176">Witaj **ustawień diagnostycznych** blok zawiera ustawienia hello hello dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="850bb-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="850bb-177">W tym przykładzie analizy dzienników przechowuje hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="850bb-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="850bb-178">Kliknij przycisk **Konfiguruj** w obszarze **analizy dzienników** tooconfigure obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="850bb-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="850bb-179">Można również użyć centra zdarzeń i przechowywania konta toosave hello dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="850bb-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Uruchamia proces konfiguracji hello][2]

4. <span data-ttu-id="850bb-181">Wybierz istniejący obszar roboczy Operations Management Suite (OMS) lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="850bb-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="850bb-182">W tym przykładzie użyto jednego z istniejących.</span><span class="sxs-lookup"><span data-stu-id="850bb-182">This example uses an existing one.</span></span>

   ![Opcje dla obszarów roboczych OMS][3]

5. <span data-ttu-id="850bb-184">Potwierdź ustawienia hello, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="850bb-184">Confirm hello settings and click **Save**.</span></span>

   ![Blok ustawień diagnostycznych z zaznaczenia][4]

### <a name="activity-log"></a><span data-ttu-id="850bb-186">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="850bb-186">Activity log</span></span>

<span data-ttu-id="850bb-187">Platforma Azure generuje dziennik aktywności hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="850bb-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="850bb-188">Dzienniki Hello są zachowywane przez 90 dni w magazynie Azure dzienniki zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="850bb-189">Dowiedz się więcej o tych dzienników, odczytując hello [wyświetlanie zdarzeń i dziennika aktywności](../monitoring-and-diagnostics/insights-debugging-with-events.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="850bb-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="850bb-190">Dziennik dostępu</span><span class="sxs-lookup"><span data-stu-id="850bb-190">Access log</span></span>

<span data-ttu-id="850bb-191">Dziennik dostępu Hello jest generowany tylko wtedy, gdy włączono na każde wystąpienie bramy aplikacji, zgodnie z opisem w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="850bb-192">Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="850bb-193">Każdy dostęp brama aplikacji w jest rejestrowany w formacie JSON, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="850bb-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="850bb-194">Wartość</span><span class="sxs-lookup"><span data-stu-id="850bb-194">Value</span></span>  |<span data-ttu-id="850bb-195">Opis</span><span class="sxs-lookup"><span data-stu-id="850bb-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="850bb-196">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="850bb-196">instanceId</span></span>     | <span data-ttu-id="850bb-197">Brama aplikacji w wystąpienia tego żądania hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="850bb-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="850bb-198">ClientIP</span><span class="sxs-lookup"><span data-stu-id="850bb-198">clientIP</span></span>     | <span data-ttu-id="850bb-199">Źródłowy adres IP dla żądania hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="850bb-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="850bb-200">clientPort</span></span>     | <span data-ttu-id="850bb-201">Źródłowy port hello żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="850bb-202">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="850bb-202">httpMethod</span></span>     | <span data-ttu-id="850bb-203">Metoda HTTP używana przez hello żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="850bb-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="850bb-204">requestUri</span></span>     | <span data-ttu-id="850bb-205">Identyfikator URI hello odebrane żądanie.</span><span class="sxs-lookup"><span data-stu-id="850bb-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="850bb-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="850bb-206">RequestQuery</span></span>     | <span data-ttu-id="850bb-207">**Serwer routingu**: Wysłano żądanie hello wystąpienie puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="850bb-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="850bb-208">**X-AzureApplicationGateway-dziennika-ID**: Identyfikator korelacji jest używany dla hello żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="850bb-209">Może być używane tootroubleshoot problemy ruchu na serwerach wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="850bb-210">**Stan serwera**: kod odpowiedzi HTTP bramy aplikacji otrzymane z wewnętrznego hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="850bb-211">Agent użytkownika</span><span class="sxs-lookup"><span data-stu-id="850bb-211">UserAgent</span></span>     | <span data-ttu-id="850bb-212">Agent użytkownika z nagłówka żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="850bb-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="850bb-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="850bb-213">httpStatus</span></span>     | <span data-ttu-id="850bb-214">Kod stanu HTTP zwrócony toohello klienta z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="850bb-215">Wersja_http</span><span class="sxs-lookup"><span data-stu-id="850bb-215">httpVersion</span></span>     | <span data-ttu-id="850bb-216">Wersja hello żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="850bb-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="850bb-217">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="850bb-217">receivedBytes</span></span>     | <span data-ttu-id="850bb-218">Rozmiar pakietów otrzymanych w bajtach.</span><span class="sxs-lookup"><span data-stu-id="850bb-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="850bb-219">SentBytes</span><span class="sxs-lookup"><span data-stu-id="850bb-219">sentBytes</span></span>| <span data-ttu-id="850bb-220">Rozmiar pakietu wysłane w bajtach.</span><span class="sxs-lookup"><span data-stu-id="850bb-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="850bb-221">Właściwość timeTaken</span><span class="sxs-lookup"><span data-stu-id="850bb-221">timeTaken</span></span>| <span data-ttu-id="850bb-222">Długość czasu (w milisekundach), który zajmuje toobe żądania, przetwarzane i jego toobe odpowiedzi wysyłane.</span><span class="sxs-lookup"><span data-stu-id="850bb-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="850bb-223">Jest on obliczany jako interwał powitania od czasu powitania po bramy aplikacji odbiera pierwszy bajt hello czas toohello żądania HTTP podczas odpowiedź hello wysyłania zakończenie operacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="850bb-224">Jest ważne toonote, który zazwyczaj hello Time-Taken pole zawiera czas hello podróży za pośrednictwem sieci hello pakietów hello żądań i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="850bb-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="850bb-225">SSL</span><span class="sxs-lookup"><span data-stu-id="850bb-225">sslEnabled</span></span>| <span data-ttu-id="850bb-226">Określa, czy pule zaplecza toohello komunikacji używać protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="850bb-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="850bb-227">Prawidłowe wartości to on i off.</span><span class="sxs-lookup"><span data-stu-id="850bb-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="850bb-228">Dziennika wydajności</span><span class="sxs-lookup"><span data-stu-id="850bb-228">Performance log</span></span>

<span data-ttu-id="850bb-229">dziennik wydajności Hello jest generowany tylko wtedy, gdy włączono na każde wystąpienie bramy aplikacji, zgodnie z opisem w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="850bb-230">Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="850bb-231">dane dzienników wydajności Hello jest generowana w 1-minutowych interwałach.</span><span class="sxs-lookup"><span data-stu-id="850bb-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="850bb-232">rejestrowane są następujące dane Hello:</span><span class="sxs-lookup"><span data-stu-id="850bb-232">hello following data is logged:</span></span>


|<span data-ttu-id="850bb-233">Wartość</span><span class="sxs-lookup"><span data-stu-id="850bb-233">Value</span></span>  |<span data-ttu-id="850bb-234">Opis</span><span class="sxs-lookup"><span data-stu-id="850bb-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="850bb-235">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="850bb-235">instanceId</span></span>     |  <span data-ttu-id="850bb-236">Dla wydajności, które dane są generowane wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="850bb-237">Brama aplikacji w wielu wystąpień jest jeden wiersz dla każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="850bb-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="850bb-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="850bb-238">healthyHostCount</span></span>     | <span data-ttu-id="850bb-239">Liczba hostów dobrej kondycji w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="850bb-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="850bb-240">unHealthyHostCount</span></span>     | <span data-ttu-id="850bb-241">Liczba hostów złej kondycji w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="850bb-242">RequestCount</span><span class="sxs-lookup"><span data-stu-id="850bb-242">requestCount</span></span>     | <span data-ttu-id="850bb-243">Liczba żądań obsłużonych.</span><span class="sxs-lookup"><span data-stu-id="850bb-243">Number of requests served.</span></span>        |
|<span data-ttu-id="850bb-244">Czas oczekiwania</span><span class="sxs-lookup"><span data-stu-id="850bb-244">latency</span></span> | <span data-ttu-id="850bb-245">Czas oczekiwania (w milisekundach) żądań od toohello wystąpienia hello zaplecza pełniącą hello żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="850bb-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="850bb-246">failedRequestCount</span></span>| <span data-ttu-id="850bb-247">Liczba żądań zakończonych niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="850bb-247">Number of failed requests.</span></span>|
|<span data-ttu-id="850bb-248">Przepływność</span><span class="sxs-lookup"><span data-stu-id="850bb-248">throughput</span></span>| <span data-ttu-id="850bb-249">Średnia przepustowość od czasu ostatniego dziennika hello, mierzony w bajtach na sekundę.</span><span class="sxs-lookup"><span data-stu-id="850bb-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="850bb-250">Czas oczekiwania jest obliczana na podstawie hello godzinę hello pierwszy bajt żądania hello HTTP odebrane toohello czas wysłania ostatniego bajtu hello hello odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="850bb-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="850bb-251">Jego hello sumę hello brama aplikacji w czasie przetwarzania oraz hello ponownie toohello sieci koszt końca, oraz czas hello hello zaplecza przyjmuje tooprocess hello żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="850bb-252">Dziennik zapory</span><span class="sxs-lookup"><span data-stu-id="850bb-252">Firewall log</span></span>

<span data-ttu-id="850bb-253">dziennik zapory Hello jest generowany tylko wtedy, gdy włączono dla każdej bramy aplikacji, zgodnie z opisem w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="850bb-254">Ten dziennik wymaga również, że tej zapory aplikacji sieci web hello jest skonfigurowany dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="850bb-255">Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="850bb-256">rejestrowane są następujące dane Hello:</span><span class="sxs-lookup"><span data-stu-id="850bb-256">hello following data is logged:</span></span>


|<span data-ttu-id="850bb-257">Wartość</span><span class="sxs-lookup"><span data-stu-id="850bb-257">Value</span></span>  |<span data-ttu-id="850bb-258">Opis</span><span class="sxs-lookup"><span data-stu-id="850bb-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="850bb-259">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="850bb-259">instanceId</span></span>     | <span data-ttu-id="850bb-260">Zapory, które dane są generowane wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="850bb-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="850bb-261">Brama aplikacji w wielu wystąpień jest jeden wiersz dla każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="850bb-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="850bb-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="850bb-262">clientIp</span></span>     |   <span data-ttu-id="850bb-263">Źródłowy adres IP dla żądania hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="850bb-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="850bb-264">clientPort</span></span>     |  <span data-ttu-id="850bb-265">Źródłowy port hello żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="850bb-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="850bb-266">requestUri</span></span>     | <span data-ttu-id="850bb-267">Adres URL hello odebrane żądanie.</span><span class="sxs-lookup"><span data-stu-id="850bb-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="850bb-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="850bb-268">ruleSetType</span></span>     | <span data-ttu-id="850bb-269">Typ zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="850bb-269">Rule set type.</span></span> <span data-ttu-id="850bb-270">wartość dostępna Hello jest OWASP.</span><span class="sxs-lookup"><span data-stu-id="850bb-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="850bb-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="850bb-271">ruleSetVersion</span></span>     | <span data-ttu-id="850bb-272">Wersja używanego zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="850bb-272">Rule set version used.</span></span> <span data-ttu-id="850bb-273">Dostępne wartości to 2.2.9 i 3.0.</span><span class="sxs-lookup"><span data-stu-id="850bb-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="850bb-274">RuleId</span><span class="sxs-lookup"><span data-stu-id="850bb-274">ruleId</span></span>     | <span data-ttu-id="850bb-275">Identyfikator reguły hello wyzwolenie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="850bb-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="850bb-276">Komunikat</span><span class="sxs-lookup"><span data-stu-id="850bb-276">message</span></span>     | <span data-ttu-id="850bb-277">Przyjazna dla użytkownika komunikat dla hello wyzwolenie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="850bb-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="850bb-278">Bardziej szczegółowe informacje znajdują się w sekcji szczegółów hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="850bb-279">Akcja</span><span class="sxs-lookup"><span data-stu-id="850bb-279">action</span></span>     |  <span data-ttu-id="850bb-280">Nie wykonano akcji na powitania żądania.</span><span class="sxs-lookup"><span data-stu-id="850bb-280">Action taken on hello request.</span></span> <span data-ttu-id="850bb-281">Dostępne wartości to zablokowany, a dozwolone.</span><span class="sxs-lookup"><span data-stu-id="850bb-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="850bb-282">Lokacji</span><span class="sxs-lookup"><span data-stu-id="850bb-282">site</span></span>     | <span data-ttu-id="850bb-283">Witryna, dla których hello dziennika został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="850bb-283">Site for which hello log was generated.</span></span> <span data-ttu-id="850bb-284">Obecnie tylko Global jest na liście, ponieważ reguły są globalne.</span><span class="sxs-lookup"><span data-stu-id="850bb-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="850bb-285">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="850bb-285">details</span></span>     | <span data-ttu-id="850bb-286">Szczegóły hello wyzwolenie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="850bb-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="850bb-287">details.Message</span><span class="sxs-lookup"><span data-stu-id="850bb-287">details.message</span></span>     | <span data-ttu-id="850bb-288">Opis reguły hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="850bb-289">details.Data</span><span class="sxs-lookup"><span data-stu-id="850bb-289">details.data</span></span>     | <span data-ttu-id="850bb-290">Dane dotyczące określonego znaleziono w żądaniu reguły hello dopasowany.</span><span class="sxs-lookup"><span data-stu-id="850bb-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="850bb-291">details.File</span><span class="sxs-lookup"><span data-stu-id="850bb-291">details.file</span></span>     | <span data-ttu-id="850bb-292">Plik konfiguracji zawiera reguły hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="850bb-293">details.Line</span><span class="sxs-lookup"><span data-stu-id="850bb-293">details.line</span></span>     | <span data-ttu-id="850bb-294">Numer wiersza w pliku konfiguracyjnym hello, która wyzwoliła hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="850bb-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="850bb-295">Wyświetlanie i analizowanie hello dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="850bb-295">View and analyze hello activity log</span></span>

<span data-ttu-id="850bb-296">Można wyświetlać i analizować dane dzienników działania przy użyciu dowolnej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="850bb-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="850bb-297">**Narzędzia Azure**: pobieranie informacji z dziennika aktywności hello za pomocą programu Azure PowerShell, hello Azure CLI hello interfejsu API REST Azure lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="850bb-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="850bb-298">Instrukcje krok po kroku dla każdej metody wyszczególnione w hello [operacji działania za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="850bb-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="850bb-299">**Power BI**: Jeśli nie masz jeszcze [usługi Power BI](https://powerbi.microsoft.com/pricing) konta, możesz spróbować ją bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="850bb-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="850bb-300">Za pomocą hello [Dzienniki aktywności Azure zawartości pakietu dla usługi Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), można analizować danych za pomocą wstępnie skonfigurowanych pulpity nawigacyjne, które można użyć jako jest lub dostosować je.</span><span class="sxs-lookup"><span data-stu-id="850bb-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="850bb-301">Wyświetlanie i analizowanie hello dostępu, wydajności i dzienniki zapory</span><span class="sxs-lookup"><span data-stu-id="850bb-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="850bb-302">Azure [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md) może zbierać pliki dziennika zdarzeń i licznik hello z konta magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="850bb-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="850bb-303">Zawiera wizualizacje i tooanalyze możliwości wyszukiwania zaawansowanego dzienników.</span><span class="sxs-lookup"><span data-stu-id="850bb-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="850bb-304">Można także połączyć tooyour konta magazynu i pobrać wpisów dziennika JSON hello dzienników dostępu i wydajności.</span><span class="sxs-lookup"><span data-stu-id="850bb-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="850bb-305">Po pobraniu hello pliki w formacie JSON można przekonwertować tooCSV i wyświetlić je w programie Excel, usłudze Power BI lub innych narzędzi wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="850bb-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="850bb-306">Jeśli znasz podstawowe koncepcje zmiany wartości stałych i zmiennych w języku C# i Visual Studio, możesz użyć hello [dziennika narzędzia konwertera](https://github.com/Azure-Samples/networking-dotnet-log-converter) dostępne w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="850bb-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="850bb-307">Metryki</span><span class="sxs-lookup"><span data-stu-id="850bb-307">Metrics</span></span>

<span data-ttu-id="850bb-308">Metryki są funkcją dla niektórych zasobów platformy Azure, w którym liczniki wydajności można przeglądać w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="850bb-309">Bramy aplikacji jedna metryka jest teraz dostępna.</span><span class="sxs-lookup"><span data-stu-id="850bb-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="850bb-310">Ta metryka jest przepływność i widoczny w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="850bb-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="850bb-311">Przeglądaj tooan aplikacji bramy, a następnie kliknij przycisk **metryki**.</span><span class="sxs-lookup"><span data-stu-id="850bb-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="850bb-312">tooview hello wartości, wybierz opcję przepływność w hello **dostępne metryki** sekcji.</span><span class="sxs-lookup"><span data-stu-id="850bb-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="850bb-313">Hello po obrazu przedstawiono przykład z filtrami hello w innym czasie zakresów można toodisplay hello danych.</span><span class="sxs-lookup"><span data-stu-id="850bb-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Widoku metryki z filtrami][5]

<span data-ttu-id="850bb-315">Zobacz toosee bieżącą listę metryki, [obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="850bb-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="850bb-316">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="850bb-316">Alert rules</span></span>

<span data-ttu-id="850bb-317">Można uruchomić reguły alertów w oparciu metryki dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="850bb-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="850bb-318">Na przykład alert można wywołać elementu webhook lub wiadomości e-mail administratora, jeśli hello przepływność bramy aplikacji hello jest powyżej, poniżej lub w wartości progowej przez określony czas.</span><span class="sxs-lookup"><span data-stu-id="850bb-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="850bb-319">Poniższy przykład Hello przeprowadzi Cię przez proces tworzenia reguły alertu wysyłanej wiadomości e-mail administratora tooan po naruszeń przepływność a próg:</span><span class="sxs-lookup"><span data-stu-id="850bb-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="850bb-320">Kliknij przycisk **Dodaj alert metryki** tooopen hello **Dodaj regułę** bloku.</span><span class="sxs-lookup"><span data-stu-id="850bb-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="850bb-321">Zapewnia także łączność tego bloku z hello metryki bloku.</span><span class="sxs-lookup"><span data-stu-id="850bb-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Przycisk "Dodaj metryki alert"][6]

2. <span data-ttu-id="850bb-323">Na powitania **Dodaj regułę** bloku wypełniania hello nazwa warunku, powiadom sekcje i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="850bb-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="850bb-324">W hello **warunku** selektora, wybierz jedną z wartości hello czterech: **większe**, **większy lub równy**, **mniej niż**, lub  **Mniejsze niż lub równe**.</span><span class="sxs-lookup"><span data-stu-id="850bb-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="850bb-325">W hello **okres** selektora, wybierz okres od 5 minut too6 godzin.</span><span class="sxs-lookup"><span data-stu-id="850bb-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="850bb-326">W przypadku wybrania **E-mail właściciele, współautorzy i czytelnicy**, powitalne wiadomości e-mail może być dynamiczny na podstawie hello użytkowników, którzy mają dostęp do zasobów toothat.</span><span class="sxs-lookup"><span data-stu-id="850bb-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="850bb-327">W przeciwnym razie możesz podać rozdzielana przecinkami lista użytkowników w hello **email(s) dodatkowe administratora** pole.</span><span class="sxs-lookup"><span data-stu-id="850bb-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Dodaj regułę bloku][7]

<span data-ttu-id="850bb-329">W przypadku naruszenia progu hello dociera do wiadomości e-mail, która jest podobne toohello, co w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="850bb-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![Wiadomości e-mail w przypadku naruszenia progu][8]

<span data-ttu-id="850bb-331">Po utworzeniu metryki alert zostanie wyświetlona lista alertów.</span><span class="sxs-lookup"><span data-stu-id="850bb-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="850bb-332">Zapewnia przegląd wszystkich hello reguł alertów.</span><span class="sxs-lookup"><span data-stu-id="850bb-332">It provides an overview of all hello alert rules.</span></span>

![Lista alertów i reguł][9]

<span data-ttu-id="850bb-334">toolearn więcej informacji na temat powiadomień o alertach, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="850bb-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="850bb-335">toounderstand więcej informacji na temat elementów webhook i jak ich używać z alertami, odwiedź stronę [skonfigurować elementu webhook na alert metryki Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="850bb-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="850bb-336">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="850bb-336">Next steps</span></span>

* <span data-ttu-id="850bb-337">Wizualizuj w dziennikach zdarzeń i liczników przy użyciu [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="850bb-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="850bb-338">[Wizualizuj dziennik aktywności platformy Azure z usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="850bb-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="850bb-339">[Przeglądać i analizować Dzienniki aktywności platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="850bb-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
