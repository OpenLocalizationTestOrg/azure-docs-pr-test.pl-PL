---
title: "Monitoruj dzienniki dostęp, Dzienniki wydajności kondycji zaplecza i metryki bramy aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć i zarządzać Dzienniki wydajności i dzienników dostępu bramy aplikacji"
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="bb9a5-103">Kondycji zaplecza, dzienniki diagnostyczne i metryki bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="bb9a5-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="bb9a5-104">Korzystając z bramy aplikacji Azure, możesz monitorować zasobów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="bb9a5-105">[Kondycja zaplecza](#back-end-health): bramy aplikacji umożliwia monitorowanie kondycji serwerów w puli zaplecza za pośrednictwem portalu Azure i przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="bb9a5-106">Można również znaleźć kondycję pul zaplecza za pośrednictwem dzienników diagnostycznych wydajności.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="bb9a5-107">[Dzienniki](#diagnostic-logs): dzienniki umożliwiają wydajność, dostępu i innych danych, które mają być zapisywane lub używane z zasobu do celów monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="bb9a5-108">[Metryki](#metrics): jedna metryka ma obecnie Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="bb9a5-109">Ta metryka mierzy przepływność brama aplikacji w bajtach na sekundę.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="bb9a5-110">Kondycja zaplecza</span><span class="sxs-lookup"><span data-stu-id="bb9a5-110">Back-end health</span></span>

<span data-ttu-id="bb9a5-111">Brama aplikacji umożliwia monitorowanie kondycji poszczególnych członków pul zaplecza za pośrednictwem portalu, programu PowerShell i interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="bb9a5-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="bb9a5-112">Możesz również znaleźć zagregowane kondycji podsumowania pul zaplecza za pośrednictwem dzienników diagnostycznych wydajności.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="bb9a5-113">Raport o kondycji zaplecza odzwierciedla dane wyjściowe do wystąpień zaplecza sondy kondycji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="bb9a5-114">Podczas badania zakończy się pomyślnie i wewnętrznej mogą odbierać dane, jest on uznawany za dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="bb9a5-115">W przeciwnym razie jego jest określana jako zła.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb9a5-116">Jeśli istnieje grupa zabezpieczeń sieci (NSG) w podsieci bramy aplikacji, otwórz zakresy portów 65503 65534 podsieci bramy aplikacji dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="bb9a5-117">Te porty są wymagane dla kondycji zaplecza interfejsu API do pracy.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="bb9a5-118">Wyświetl kondycję zaplecza za pośrednictwem portalu</span><span class="sxs-lookup"><span data-stu-id="bb9a5-118">View back-end health through the portal</span></span>

<span data-ttu-id="bb9a5-119">W portalu wewnętrzną kondycji znajduje się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="bb9a5-120">Wybierz istniejącą bramę aplikacji **monitorowanie** > **kondycji zaplecza**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="bb9a5-121">Każdy element członkowski w puli zaplecza znajduje się na tej stronie (czy jest ona karty Sieciowej, adresu IP lub FQDN).</span><span class="sxs-lookup"><span data-stu-id="bb9a5-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="bb9a5-122">Nazwa puli zaplecza, portu, nazwy ustawienia HTTP zaplecza i stan kondycji są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="bb9a5-123">Prawidłowe wartości stanu kondycji to **dobra kondycja**, **niezdrowego**, i **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="bb9a5-124">Jeśli zostanie wyświetlony stan kondycji zaplecza **nieznany**, upewnij się, że dostęp do wewnętrznych nie jest blokowane przez reguły NSG, trasy zdefiniowane przez użytkownika (przez) lub niestandardowe DNS w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![Kondycja zaplecza][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="bb9a5-126">Wyświetl kondycję zaplecza za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb9a5-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="bb9a5-127">Poniższy kod programu PowerShell pokazano, jak wyświetlić kondycję zaplecza przy użyciu `Get-AzureRmApplicationGatewayBackendHealth` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="bb9a5-128">Wyświetl kondycję zaplecza za pośrednictwem 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a5-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="bb9a5-129">Wyniki</span><span class="sxs-lookup"><span data-stu-id="bb9a5-129">Results</span></span>

<span data-ttu-id="bb9a5-130">Poniższy fragment kodu przedstawia przykład odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="bb9a5-131"><a name="diagnostic-logging"></a>Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="bb9a5-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="bb9a5-132">Różne typy dzienników Azure umożliwia zarządzanie i rozwiązywanie problemów z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="bb9a5-133">Niektóre z tych dzienników dostępne za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="bb9a5-134">Wszystkie dzienniki można wyodrębnić z magazynu obiektów Blob platformy Azure i wyświetlane w różnych narzędzi, takich jak [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md), Excel i Power BI.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="bb9a5-135">Użytkownik może więcej informacji na temat różnych typów dzienników z poniższej listy:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="bb9a5-136">**Dziennik aktywności**: można użyć [Dzienniki aktywności Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (wcześniej znane jako dzienniki inspekcji i operacyjne dzienniki) aby wyświetlić wszystkie operacje, które są przesyłane do Twojej subskrypcji platformy Azure i ich stan.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="bb9a5-137">Wpisy dziennika aktywności są zbierane domyślnie i można je wyświetlić w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="bb9a5-138">**Dziennik dostępu**: ten dziennik służy do wyświetlania wzorce dostępu bramy aplikacji i analizowania ważne informacje, w tym adresu IP, żądanego adresu URL wywołującego, czas oczekiwania na odpowiedź, kod powrotny i bajtów i wylogowanie. Dziennik dostępu są gromadzone co 300 sekund.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="bb9a5-139">Ten dziennik zawiera jeden rekord dla każdego wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="bb9a5-140">Wystąpienie bramy aplikacji mogą zostać zidentyfikowane na podstawie właściwość instanceId.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="bb9a5-141">**Dziennik wydajności**: ten dziennik służy do wyświetlania, jak działają wystąpieniach bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="bb9a5-142">Ten dziennik zawiera informacje o wydajności dla każdego wystąpienia, w tym całkowita liczba żądań obsłużonych, przepływność w bajtach, całkowita liczba żądań obsłużonych, liczba nieudanych żądań, a liczba wystąpień zaplecza dobrej kondycji i złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="bb9a5-143">Dziennik wydajności są zbierane co 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="bb9a5-144">**Dziennik zapory**: ten dziennik służy do wyświetlania żądań, które są rejestrowane za pomocą wykrywania i zapobiegania tryb bramę aplikacji, który jest skonfigurowany z zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="bb9a5-145">Dzienniki są dostępne tylko dla zasobów wdrożone w modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="bb9a5-146">Nie można używać dzienników zasobów w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="bb9a5-147">Aby lepiej zrozumieć dwa modele, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="bb9a5-148">Są trzy opcje do przechowywania dzienników:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="bb9a5-149">**Konto magazynu**: konta magazynu są najlepiej nadaje się do dzienników podczas dzienniki są przechowywane przez dłuższy czas i sprawdzić, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="bb9a5-150">**Centra zdarzeń**: Event hubs to doskonałe rozwiązanie dla integracji z innych informacji o zabezpieczeniach i narzędzi do zarządzania zdarzenia (SEIM) można pobrać alertów dotyczących zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="bb9a5-151">**Zaloguj się Analytics**: analizy dzienników najlepiej nadaje się do ogólnego monitorowania w czasie rzeczywistym aplikacji lub analizowania trendów.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="bb9a5-152">Włącz rejestrowanie za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb9a5-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="bb9a5-153">Rejestrowanie aktywności jest automatycznie włączona dla każdego zasobu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="bb9a5-154">Należy włączyć dostęp i rejestrowania w celu rozpoczęcia zbierania danych dostępne za pośrednictwem tych dzienników wydajności.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="bb9a5-155">Aby włączyć rejestrowanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="bb9a5-156">Należy zwrócić uwagę identyfikatorów zasobów konta magazynu, w którym są przechowywane dane dziennika.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="bb9a5-157">Ta wartość ma postać: /subscriptions/\<subscriptionId\>/resourceGroups/\<Nazwa grupy zasobów\>/providers/Microsoft.Storage/storageAccounts/\<nazwy konta magazynu\>.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="bb9a5-158">Można użyć dowolnego konta magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="bb9a5-159">Azure portal umożliwia znalezienie tych informacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-159">You can use the Azure portal to find this information.</span></span>

    ![Portalu: identyfikator zasobu dla konta magazynu](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="bb9a5-161">Należy pamiętać, dla którego włączono rejestrowanie identyfikator zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="bb9a5-162">Ta wartość ma postać: /subscriptions/\<subscriptionId\>/resourceGroups/\<Nazwa grupy zasobów\>/providers/Microsoft.Network/applicationGateways/\<nazwa bramy aplikacji \>.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="bb9a5-163">Portal umożliwia znalezienie tych informacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-163">You can use the portal to find this information.</span></span>

    ![Portalu: identyfikator zasobu bramy aplikacji](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="bb9a5-165">Za pomocą następującego polecenia cmdlet programu PowerShell, należy włączyć rejestrowanie diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="bb9a5-166">Dzienniki aktywności nie wymagają oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="bb9a5-167">Użycie magazynu dla dostępu do rejestrowania i wydajności wiąże opłaty za usługę.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="bb9a5-168">Włącz rejestrowanie za pośrednictwem portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a5-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="bb9a5-169">W portalu Azure Znajdź zasobu, a następnie kliknij przycisk **dzienniki diagnostyczne**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="bb9a5-170">Brama aplikacji dostępne są trzy dzienniki:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="bb9a5-171">Dziennik dostępu</span><span class="sxs-lookup"><span data-stu-id="bb9a5-171">Access log</span></span>
   * <span data-ttu-id="bb9a5-172">Dziennika wydajności</span><span class="sxs-lookup"><span data-stu-id="bb9a5-172">Performance log</span></span>
   * <span data-ttu-id="bb9a5-173">Dziennik zapory</span><span class="sxs-lookup"><span data-stu-id="bb9a5-173">Firewall log</span></span>

2. <span data-ttu-id="bb9a5-174">Aby rozpocząć, zbieranie danych, kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![Włączanie diagnostyki][1]

3. <span data-ttu-id="bb9a5-176">**Ustawień diagnostycznych** blok zawiera ustawienia dla dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="bb9a5-177">W tym przykładzie analizy dzienników są przechowywane dzienniki.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="bb9a5-178">Kliknij przycisk **Konfiguruj** w obszarze **analizy dzienników** do skonfigurowania swojego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="bb9a5-179">Aby zapisać dzienników diagnostycznych, można użyć centra zdarzeń i konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![Uruchamia proces konfiguracji][2]

4. <span data-ttu-id="bb9a5-181">Wybierz istniejący obszar roboczy Operations Management Suite (OMS) lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="bb9a5-182">W tym przykładzie użyto jednego z istniejących.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-182">This example uses an existing one.</span></span>

   ![Opcje dla obszarów roboczych OMS][3]

5. <span data-ttu-id="bb9a5-184">Potwierdź ustawienia, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-184">Confirm the settings and click **Save**.</span></span>

   ![Blok ustawień diagnostycznych z zaznaczenia][4]

### <a name="activity-log"></a><span data-ttu-id="bb9a5-186">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="bb9a5-186">Activity log</span></span>

<span data-ttu-id="bb9a5-187">Domyślnie Azure generuje dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="bb9a5-188">Dzienniki są zachowywane przez 90 dni w magazynie Azure dzienniki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="bb9a5-189">Dowiedz się więcej o tych dzienników, odczytując [wyświetlanie zdarzeń i dziennika aktywności](../monitoring-and-diagnostics/insights-debugging-with-events.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="bb9a5-190">Dziennik dostępu</span><span class="sxs-lookup"><span data-stu-id="bb9a5-190">Access log</span></span>

<span data-ttu-id="bb9a5-191">Dziennik dostępu jest generowany tylko wtedy, gdy włączono na każde wystąpienie bramy aplikacji, zgodnie z opisem w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="bb9a5-192">Dane są przechowywane w określonej po włączeniu rejestrowania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="bb9a5-193">Każdy dostęp brama aplikacji jest rejestrowany w formacie JSON, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="bb9a5-194">Wartość</span><span class="sxs-lookup"><span data-stu-id="bb9a5-194">Value</span></span>  |<span data-ttu-id="bb9a5-195">Opis</span><span class="sxs-lookup"><span data-stu-id="bb9a5-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="bb9a5-196">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="bb9a5-196">instanceId</span></span>     | <span data-ttu-id="bb9a5-197">Wystąpienie bramy aplikacji, który obsłużył żądanie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="bb9a5-198">ClientIP</span><span class="sxs-lookup"><span data-stu-id="bb9a5-198">clientIP</span></span>     | <span data-ttu-id="bb9a5-199">Źródłowy adres IP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="bb9a5-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="bb9a5-200">clientPort</span></span>     | <span data-ttu-id="bb9a5-201">Port źródłowy dla żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="bb9a5-202">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="bb9a5-202">httpMethod</span></span>     | <span data-ttu-id="bb9a5-203">Metoda HTTP używana przez żądanie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="bb9a5-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="bb9a5-204">requestUri</span></span>     | <span data-ttu-id="bb9a5-205">Identyfikator URI odebrane żądanie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-205">URI of the received request.</span></span>        |
|<span data-ttu-id="bb9a5-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="bb9a5-206">RequestQuery</span></span>     | <span data-ttu-id="bb9a5-207">**Serwer routingu**: wystąpienie puli zaplecza, którego wysłano żądanie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="bb9a5-208">**X-AzureApplicationGateway-dziennika-ID**: Identyfikator korelacji użytej w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="bb9a5-209">Może służyć do rozwiązywania problemów ruchu na serwerach wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="bb9a5-210">**Stan serwera**: kod odpowiedzi HTTP o bramy aplikacji otrzymanych od wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="bb9a5-211">Agent użytkownika</span><span class="sxs-lookup"><span data-stu-id="bb9a5-211">UserAgent</span></span>     | <span data-ttu-id="bb9a5-212">Agent użytkownika z nagłówka żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="bb9a5-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="bb9a5-213">httpStatus</span></span>     | <span data-ttu-id="bb9a5-214">Kod stanu HTTP zwrócona do klienta z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="bb9a5-215">Wersja_http</span><span class="sxs-lookup"><span data-stu-id="bb9a5-215">httpVersion</span></span>     | <span data-ttu-id="bb9a5-216">Wersja protokołu HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="bb9a5-217">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="bb9a5-217">receivedBytes</span></span>     | <span data-ttu-id="bb9a5-218">Rozmiar pakietów otrzymanych w bajtach.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="bb9a5-219">SentBytes</span><span class="sxs-lookup"><span data-stu-id="bb9a5-219">sentBytes</span></span>| <span data-ttu-id="bb9a5-220">Rozmiar pakietu wysłane w bajtach.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="bb9a5-221">Właściwość timeTaken</span><span class="sxs-lookup"><span data-stu-id="bb9a5-221">timeTaken</span></span>| <span data-ttu-id="bb9a5-222">Długość czas (w milisekundach) przetwarzania żądania i odpowiedzi mają być wysyłane.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="bb9a5-223">To jest obliczany jako wartość interwału od czasu, gdy brama aplikacji w odbiera pierwszy bajt żądania HTTP do czasu podczas wysyłania zakończenie operacji w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="bb9a5-224">Należy pamiętać, że pole Time-Taken zwykle zawiera godzinę, o której żądanie i odpowiedź pakiety są przesyłane przez sieć.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="bb9a5-225">SSL</span><span class="sxs-lookup"><span data-stu-id="bb9a5-225">sslEnabled</span></span>| <span data-ttu-id="bb9a5-226">Czy komunikacji z pul zaplecza używać protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="bb9a5-227">Prawidłowe wartości to on i off.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="bb9a5-228">Dziennika wydajności</span><span class="sxs-lookup"><span data-stu-id="bb9a5-228">Performance log</span></span>

<span data-ttu-id="bb9a5-229">Dziennik wydajności jest generowany tylko wtedy, gdy włączono na każde wystąpienie bramy aplikacji, zgodnie z opisem w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="bb9a5-230">Dane są przechowywane w określonej po włączeniu rejestrowania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="bb9a5-231">Dane dzienników wydajności jest generowana w 1-minutowych interwałach.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="bb9a5-232">Rejestrowane są następujące dane:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-232">The following data is logged:</span></span>


|<span data-ttu-id="bb9a5-233">Wartość</span><span class="sxs-lookup"><span data-stu-id="bb9a5-233">Value</span></span>  |<span data-ttu-id="bb9a5-234">Opis</span><span class="sxs-lookup"><span data-stu-id="bb9a5-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="bb9a5-235">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="bb9a5-235">instanceId</span></span>     |  <span data-ttu-id="bb9a5-236">Dla wydajności, które dane są generowane wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="bb9a5-237">Brama aplikacji w wielu wystąpień jest jeden wiersz dla każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="bb9a5-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="bb9a5-238">healthyHostCount</span></span>     | <span data-ttu-id="bb9a5-239">Liczba hostów dobrej kondycji w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="bb9a5-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="bb9a5-240">unHealthyHostCount</span></span>     | <span data-ttu-id="bb9a5-241">Liczba hostów złej kondycji w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="bb9a5-242">RequestCount</span><span class="sxs-lookup"><span data-stu-id="bb9a5-242">requestCount</span></span>     | <span data-ttu-id="bb9a5-243">Liczba żądań obsłużonych.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-243">Number of requests served.</span></span>        |
|<span data-ttu-id="bb9a5-244">Czas oczekiwania</span><span class="sxs-lookup"><span data-stu-id="bb9a5-244">latency</span></span> | <span data-ttu-id="bb9a5-245">Czas oczekiwania (w milisekundach) żądań z wystąpienia zaplecza, która służy do żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="bb9a5-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="bb9a5-246">failedRequestCount</span></span>| <span data-ttu-id="bb9a5-247">Liczba żądań zakończonych niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-247">Number of failed requests.</span></span>|
|<span data-ttu-id="bb9a5-248">Przepływność</span><span class="sxs-lookup"><span data-stu-id="bb9a5-248">throughput</span></span>| <span data-ttu-id="bb9a5-249">Średnia przepustowość od czasu ostatniego dziennika, mierzony w bajtach na sekundę.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="bb9a5-250">Czas oczekiwania jest obliczana na podstawie czasu, po odebraniu pierwszy bajt żądania HTTP do momentu wysłania ostatniego bajtu odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="bb9a5-251">Jest to suma czasu przetwarzania bramy aplikacji oraz koszty sieci wewnętrznej, a także czas, jaki wewnętrznej potrzebny do przetwarzania żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="bb9a5-252">Dziennik zapory</span><span class="sxs-lookup"><span data-stu-id="bb9a5-252">Firewall log</span></span>

<span data-ttu-id="bb9a5-253">Dziennik zapory jest generowany tylko wtedy, gdy włączono dla każdej bramy aplikacji, zgodnie z opisem w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="bb9a5-254">Ten dziennik wymaga również, czy Zapora aplikacji sieci web jest skonfigurowany dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="bb9a5-255">Dane są przechowywane w określonej po włączeniu rejestrowania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="bb9a5-256">Rejestrowane są następujące dane:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-256">The following data is logged:</span></span>


|<span data-ttu-id="bb9a5-257">Wartość</span><span class="sxs-lookup"><span data-stu-id="bb9a5-257">Value</span></span>  |<span data-ttu-id="bb9a5-258">Opis</span><span class="sxs-lookup"><span data-stu-id="bb9a5-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="bb9a5-259">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="bb9a5-259">instanceId</span></span>     | <span data-ttu-id="bb9a5-260">Zapory, które dane są generowane wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="bb9a5-261">Brama aplikacji w wielu wystąpień jest jeden wiersz dla każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="bb9a5-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="bb9a5-262">clientIp</span></span>     |   <span data-ttu-id="bb9a5-263">Źródłowy adres IP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="bb9a5-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="bb9a5-264">clientPort</span></span>     |  <span data-ttu-id="bb9a5-265">Port źródłowy dla żądania.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="bb9a5-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="bb9a5-266">requestUri</span></span>     | <span data-ttu-id="bb9a5-267">Adres URL odebrane żądanie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-267">URL of the received request.</span></span>       |
|<span data-ttu-id="bb9a5-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="bb9a5-268">ruleSetType</span></span>     | <span data-ttu-id="bb9a5-269">Typ zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-269">Rule set type.</span></span> <span data-ttu-id="bb9a5-270">Dostępne wartości to OWASP.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="bb9a5-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="bb9a5-271">ruleSetVersion</span></span>     | <span data-ttu-id="bb9a5-272">Wersja używanego zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-272">Rule set version used.</span></span> <span data-ttu-id="bb9a5-273">Dostępne wartości to 2.2.9 i 3.0.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="bb9a5-274">RuleId</span><span class="sxs-lookup"><span data-stu-id="bb9a5-274">ruleId</span></span>     | <span data-ttu-id="bb9a5-275">Identyfikator reguły wyzwalająca zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="bb9a5-276">Komunikat</span><span class="sxs-lookup"><span data-stu-id="bb9a5-276">message</span></span>     | <span data-ttu-id="bb9a5-277">Przyjazny komunikat wyzwalająca zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="bb9a5-278">Bardziej szczegółowe informacje znajdują się w sekcji szczegółów.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="bb9a5-279">Akcja</span><span class="sxs-lookup"><span data-stu-id="bb9a5-279">action</span></span>     |  <span data-ttu-id="bb9a5-280">Działania podjęte w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-280">Action taken on the request.</span></span> <span data-ttu-id="bb9a5-281">Dostępne wartości to zablokowany, a dozwolone.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="bb9a5-282">Lokacji</span><span class="sxs-lookup"><span data-stu-id="bb9a5-282">site</span></span>     | <span data-ttu-id="bb9a5-283">Witryna, dla którego wygenerowano dziennika.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-283">Site for which the log was generated.</span></span> <span data-ttu-id="bb9a5-284">Obecnie tylko Global jest na liście, ponieważ reguły są globalne.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="bb9a5-285">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="bb9a5-285">details</span></span>     | <span data-ttu-id="bb9a5-286">Szczegóły wyzwalająca zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="bb9a5-287">details.Message</span><span class="sxs-lookup"><span data-stu-id="bb9a5-287">details.message</span></span>     | <span data-ttu-id="bb9a5-288">Opis reguły.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-288">Description of the rule.</span></span>        |
|<span data-ttu-id="bb9a5-289">details.Data</span><span class="sxs-lookup"><span data-stu-id="bb9a5-289">details.data</span></span>     | <span data-ttu-id="bb9a5-290">Znaleziono żądania, które pasowało reguły określone dane.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="bb9a5-291">details.File</span><span class="sxs-lookup"><span data-stu-id="bb9a5-291">details.file</span></span>     | <span data-ttu-id="bb9a5-292">Plik konfiguracji zawiera reguły.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="bb9a5-293">details.Line</span><span class="sxs-lookup"><span data-stu-id="bb9a5-293">details.line</span></span>     | <span data-ttu-id="bb9a5-294">Numer wiersza w pliku konfiguracji, który wywołał zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="bb9a5-295">Wyświetlanie i analizowanie dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="bb9a5-295">View and analyze the activity log</span></span>

<span data-ttu-id="bb9a5-296">Można wyświetlać i analizować dane dzienników działania przy użyciu dowolnej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="bb9a5-297">**Narzędzia Azure**: pobieranie informacji z dziennika aktywności za pomocą programu Azure PowerShell, interfejsu wiersza polecenia Azure, interfejsu API REST Azure lub portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="bb9a5-298">Instrukcje krok po kroku dla każdej metody wyszczególnione w [operacji działania za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="bb9a5-299">**Power BI**: Jeśli nie masz jeszcze [usługi Power BI](https://powerbi.microsoft.com/pricing) konta, możesz spróbować ją bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="bb9a5-300">Za pomocą [Dzienniki aktywności Azure zawartości pakietu dla usługi Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), można analizować danych za pomocą wstępnie skonfigurowanych pulpity nawigacyjne, które można użyć jako jest lub dostosować je.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="bb9a5-301">Wyświetlanie i analizowanie dostępu, wydajności i dzienniki zapory</span><span class="sxs-lookup"><span data-stu-id="bb9a5-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="bb9a5-302">Azure [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md) może zbierać pliki dziennika zdarzeń i liczników z konta magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="bb9a5-303">Obejmuje on wizualizacji oraz możliwości wyszukiwania zaawansowanego do analizowania dzienników.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="bb9a5-304">Można również nawiązać połączenia z kontem magazynu i pobrać JSON wpisów dziennika dla dzienników dostępu i wydajności.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="bb9a5-305">Po pobraniu pliki w formacie JSON można przekonwertować je do pliku CSV i wyświetlić je w programie Excel, usłudze Power BI lub innych narzędzi wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="bb9a5-306">Jeśli znasz podstawowe koncepcje zmiany wartości stałych i zmiennych w języku C# i Visual Studio, możesz użyć [dziennika narzędzia konwertera](https://github.com/Azure-Samples/networking-dotnet-log-converter) dostępne w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="bb9a5-307">Metryki</span><span class="sxs-lookup"><span data-stu-id="bb9a5-307">Metrics</span></span>

<span data-ttu-id="bb9a5-308">Metryki są funkcją dla niektórych zasobów platformy Azure, w którym liczniki wydajności można przeglądać w portalu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="bb9a5-309">Bramy aplikacji jedna metryka jest teraz dostępna.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="bb9a5-310">Ta metryka jest przepływność i widoczny w portalu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="bb9a5-311">Przejdź do bramy aplikacji, a następnie kliknij przycisk **metryki**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="bb9a5-312">Aby wyświetlić wartości, wybierz przepływność w **dostępne metryki** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="bb9a5-313">Na poniższej ilustracji widać przykład filtry, które służą do wyświetlania danych w innym czasie zakresów.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![Widoku metryki z filtrami][5]

<span data-ttu-id="bb9a5-315">Aby wyświetlić bieżącą listę metryki, zobacz [obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bb9a5-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="bb9a5-316">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="bb9a5-316">Alert rules</span></span>

<span data-ttu-id="bb9a5-317">Można uruchomić reguły alertów w oparciu metryki dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="bb9a5-318">Na przykład alert można wywołać elementu webhook lub wiadomości e-mail administratora, jeśli przepływność bramy aplikacji jest powyżej, poniżej lub w wartości progowej przez określony czas.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="bb9a5-319">Poniższy przykład przeprowadzi Cię przez proces tworzenia reguły alertu, który wysyła wiadomość e-mail do administratora po naruszeń przepływność a próg:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="bb9a5-320">Kliknij przycisk **Dodaj alert metryki** otworzyć **Dodaj regułę** bloku.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="bb9a5-321">Zapewnia także łączność tego bloku z bloku metryki.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-321">You can also reach this blade from the metrics blade.</span></span>

   ![Przycisk "Dodaj metryki alert"][6]

2. <span data-ttu-id="bb9a5-323">Na **Dodaj regułę** bloku, wypełnij nazwę warunku, powiadom sekcje i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="bb9a5-324">W **warunku** selektora, wybierz jedną z czterech wartości: **większe**, **większy lub równy**, **mniej niż**, lub **Mniejsze niż lub równe**.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="bb9a5-325">W **okres** selektora, wybierz okres od 5 minut do 6 godzin.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="bb9a5-326">W przypadku wybrania **E-mail właściciele, współautorzy i czytelnicy**, wiadomości e-mail może być dynamiczny oparta na użytkownikach, którzy mają dostęp do tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="bb9a5-327">W przeciwnym razie możesz podać rozdzielana przecinkami lista użytkowników w **email(s) dodatkowe administratora** pole.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![Dodaj regułę bloku][7]

<span data-ttu-id="bb9a5-329">W przypadku naruszenia progu dociera do wiadomości e-mail, który jest podobny do przedstawionego na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="bb9a5-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![Wiadomości e-mail w przypadku naruszenia progu][8]

<span data-ttu-id="bb9a5-331">Po utworzeniu metryki alert zostanie wyświetlona lista alertów.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="bb9a5-332">Zapewnia przegląd wszystkich reguł alertów.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-332">It provides an overview of all the alert rules.</span></span>

![Lista alertów i reguł][9]

<span data-ttu-id="bb9a5-334">Aby dowiedzieć się więcej na temat powiadomień o alertach, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="bb9a5-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="bb9a5-335">Aby dowiedzieć się więcej o elementów webhook i sposobie ich użycia z alertami, odwiedź stronę [skonfigurować elementu webhook na alert metryki Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bb9a5-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb9a5-336">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bb9a5-336">Next steps</span></span>

* <span data-ttu-id="bb9a5-337">Wizualizuj w dziennikach zdarzeń i liczników przy użyciu [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="bb9a5-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="bb9a5-338">[Wizualizuj dziennik aktywności platformy Azure z usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="bb9a5-339">[Przeglądać i analizować Dzienniki aktywności platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="bb9a5-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
