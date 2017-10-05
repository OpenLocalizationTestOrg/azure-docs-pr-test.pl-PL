---
title: "Monitorowanie wskazówki interfejsu API REST Azure | Dokumentacja firmy Microsoft"
description: "Jak do uwierzytelniania żądań i użyć interfejsu API REST monitorowania Azure."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: 454a85c4752ec9c7522ef147d5ce594ef5992c32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="a2092-103">Monitorowanie wskazówki interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="a2092-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="a2092-104">W tym artykule przedstawiono sposób uwierzytelniania, tak aby korzystać z kodu [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2092-104">This article shows you how to perform authentication so your code can use the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="a2092-105">Monitor interfejsu API Azure umożliwia programowane pobieranie definicji metryk dostępnych domyślnych (typ metryki, takich jak czas procesora CPU, żądania, itp.), poziom szczegółowości i wartości metryki.</span><span class="sxs-lookup"><span data-stu-id="a2092-105">The Azure Monitor API makes it possible to programmatically retrieve the available default metric definitions (the type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="a2092-106">Po pobraniu, dane można zapisać w magazynie oddzielnego danych, takie jak bazy danych SQL Azure, Azure DB rozwiązania Cosmos lub usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a2092-106">Once retrieved, the data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="a2092-107">Z tego miejsca dodatkowe analizy mogą być wykonywane zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a2092-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="a2092-108">Oprócz Praca z różnych punktów danych metryki, ponieważ w tym artykule przedstawiono, interfejsu API monitora umożliwia wyświetlić listę reguł alertów, widok Dzienniki aktywności i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="a2092-108">Besides working with various metric data points, as this article demonstrates, the Monitor API makes it possible to list alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="a2092-109">Aby uzyskać pełną listę dostępnych operacji, zobacz [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2092-109">For a full list of available operations, see the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="a2092-110">Uwierzytelniania Azure Monitor żądań</span><span class="sxs-lookup"><span data-stu-id="a2092-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="a2092-111">Pierwszym krokiem jest uwierzytelnić żądania.</span><span class="sxs-lookup"><span data-stu-id="a2092-111">The first step is to authenticate the request.</span></span>

<span data-ttu-id="a2092-112">Wszystkie zadania wykonywane monitora interfejsu API Azure używają modelu uwierzytelniania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a2092-112">All the tasks executed against the Azure Monitor API use the Azure Resource Manager authentication model.</span></span> <span data-ttu-id="a2092-113">W związku z tym wszystkie żądania musi zostać uwierzytelniony w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2092-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a2092-114">Jeden ze sposobów uwierzytelniania aplikacji klienckiej jest tworzenie nazwy głównej usługi Azure AD i pobrać tokenu uwierzytelniania (JWT).</span><span class="sxs-lookup"><span data-stu-id="a2092-114">One approach to authenticate the client application is to create an Azure AD service principal and retrieve the authentication (JWT) token.</span></span> <span data-ttu-id="a2092-115">Poniższy przykładowy skrypt pokazuje tworzenie główną za pomocą programu PowerShell usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2092-115">The following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="a2092-116">Aby uzyskać bardziej szczegółowy przewodnik, zapoznaj się z dokumentacją na [Tworzenie nazwy głównej usługi dostępu do zasobów przy użyciu programu Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="a2092-116">For a more detailed walk-through, refer to the documentation on [using Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="a2092-117">Istnieje również możliwość [Tworzenie nazwy głównej usługi za pośrednictwem portalu Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2092-117">It is also possible to [create a service principal via the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate to a specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for the service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with the designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role to the newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="a2092-118">Aby odpytać interfejsu API Azure monitora, aplikacja kliencka należy używać główną usługi utworzonej wcześniej do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a2092-118">To query the Azure Monitor API, the client application should use the previously created service principal to authenticate.</span></span> <span data-ttu-id="a2092-119">W poniższym przykładzie skrypt programu PowerShell pokazano jedną podejścia, przy użyciu [biblioteki uwierzytelniania usługi Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL), aby pobrać tokenu uwierzytelniania tokenu JWT.</span><span class="sxs-lookup"><span data-stu-id="a2092-119">The following example PowerShell script shows one approach, using the [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) to help get the JWT authentication token.</span></span> <span data-ttu-id="a2092-120">JWT token jest przekazywany jako część parametrem autoryzacji HTTP w żądaniach do interfejsu API REST Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="a2092-120">The JWT token is passed as part of an HTTP Authorization parameter in requests to the Azure Monitor REST API.</span></span>

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

<span data-ttu-id="a2092-121">Po wykonaniu kroku konfiguracji uwierzytelniania następnie można wykonać zapytania do interfejsu API REST Monitor Azure.</span><span class="sxs-lookup"><span data-stu-id="a2092-121">Once the authentication setup step is complete, queries can then be executed against the Azure Monitor REST API.</span></span> <span data-ttu-id="a2092-122">Istnieją dwa zapytania pomocne:</span><span class="sxs-lookup"><span data-stu-id="a2092-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="a2092-123">Lista definicje metryki dla zasobu</span><span class="sxs-lookup"><span data-stu-id="a2092-123">List the metric definitions for a resource</span></span>
2. <span data-ttu-id="a2092-124">Pobieranie wartości metryki</span><span class="sxs-lookup"><span data-stu-id="a2092-124">Retrieve the metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="a2092-125">Pobieranie definicji metryk</span><span class="sxs-lookup"><span data-stu-id="a2092-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="a2092-126">Aby pobrać definicji metryk przy użyciu interfejsu API REST Azure Monitor, należy użyć "2016-03-01" jako wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a2092-126">To retrieve metric definitions using the Azure Monitor REST API, use "2016-03-01" as the API version.</span></span>
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
<span data-ttu-id="a2092-127">Dla aplikacji logiki platformy Azure definicje metryk będzie wyglądać podobnie jak poniższy zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="a2092-127">For an Azure Logic App, the metric definitions would appear similar to the following screenshot:</span></span>

![ALT "Widok JSON odpowiedzi definicji metryk."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="a2092-129">Aby uzyskać więcej informacji, zobacz [listy definicji metryk zasobu w interfejsie API REST Monitor Azure](https://msdn.microsoft.com/library/azure/mt743621.aspx) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="a2092-129">For more information, see the [List the metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="a2092-130">Pobieranie wartości metryki</span><span class="sxs-lookup"><span data-stu-id="a2092-130">Retrieve Metric Values</span></span>
<span data-ttu-id="a2092-131">Po definicji metryk dostępne są znane, następnie jest możliwe do pobierania wartości powiązane metryki.</span><span class="sxs-lookup"><span data-stu-id="a2092-131">Once the available metric definitions are known, it is then possible to retrieve the related metric values.</span></span> <span data-ttu-id="a2092-132">Nazwa metryki "wartość" (nie "localizedValue") na użytek żądań filtrowania (na przykład pobierania punktów danych metryki "CpuTime" i "Żądania").</span><span class="sxs-lookup"><span data-stu-id="a2092-132">Use the metric’s name ‘value’ (not the ‘localizedValue’) for any filtering requests (for example, retrieve the ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="a2092-133">Jeżeli nie określono żadnych filtrów, jest zwracana Metryka domyślnej.</span><span class="sxs-lookup"><span data-stu-id="a2092-133">If no filters are specified, the default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="a2092-134">Aby pobrać metryki wartości przy użyciu interfejsu API REST Azure Monitor, należy użyć "2016-06-01" jako wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a2092-134">To retrieve metric values using the Azure Monitor REST API, use "2016-06-01" as the API version.</span></span>
>
>

<span data-ttu-id="a2092-135">**Metoda**: GET</span><span class="sxs-lookup"><span data-stu-id="a2092-135">**Method**: GET</span></span>

<span data-ttu-id="a2092-136">**Identyfikator URI żądania**: https://management.azure.com/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/*{ — — przestrzeń nazw dostawcy zasobów}*/*{typ zasobu}*/*{nazwa}*/providers/microsoft.insights/metrics?$filter= *{filtru}*& api-version =*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="a2092-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="a2092-137">Na przykład pobierania punktów danych metryki RunsSucceeded dla danego okresie i ziarno czasu 1 godz, żądanie będzie następujące:</span><span class="sxs-lookup"><span data-stu-id="a2092-137">For example, to retrieve the RunsSucceeded metric data points for the given time range and for a time grain of 1 hour, the request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="a2092-138">Wynik pojawiały się podobny do następującego zrzutu ekranu:</span><span class="sxs-lookup"><span data-stu-id="a2092-138">The result would appear similar to the example following screenshot:</span></span>

![ALT "Odpowiedź w formacie JSON przedstawiający Średni czas odpowiedzi wartość metryki"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="a2092-140">Aby pobrać wiele punktów danych lub agregacji, Dodaj metryki definicji nazwy i typy agregacji do filtra, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a2092-140">To retrieve multiple data or aggregation points, add the metric definition names and aggregation types to the filter, as seen in the following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="a2092-141">Użyj ARMClient</span><span class="sxs-lookup"><span data-stu-id="a2092-141">Use ARMClient</span></span>
<span data-ttu-id="a2092-142">Zamiast przy użyciu programu PowerShell (jak pokazano powyżej), jest użycie [ARMClient](https://github.com/projectkudu/ARMClient) na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="a2092-142">An alternative to using PowerShell (as shown above), is to use [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="a2092-143">ARMClient obsługuje automatycznie uwierzytelniania usługi Azure AD (i tokenu JWT).</span><span class="sxs-lookup"><span data-stu-id="a2092-143">ARMClient handles the Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="a2092-144">Poniższe kroki wchodzą w skład stosowania ARMClient pobierania danych metryki:</span><span class="sxs-lookup"><span data-stu-id="a2092-144">The following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="a2092-145">Zainstaluj [Chocolatey](https://chocolatey.org/) i [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="a2092-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="a2092-146">W oknie terminalu, wpisz *logowania armclient.exe*.</span><span class="sxs-lookup"><span data-stu-id="a2092-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="a2092-147">Monituje o logowanie do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2092-147">This prompts you to log in to Azure.</span></span>
3. <span data-ttu-id="a2092-148">Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="a2092-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="a2092-149">Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="a2092-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT "Using ARMClient do pracy z monitorowania Azure interfejsu API REST"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-the-resource-id"></a><span data-ttu-id="a2092-151">Pobierz identyfikator zasobu</span><span class="sxs-lookup"><span data-stu-id="a2092-151">Retrieve the Resource ID</span></span>
<span data-ttu-id="a2092-152">Dostępne metryki definicje, poziom szczegółowości i powiązane wartości naprawdę może pomóc przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a2092-152">Using the REST API can really help to understand the available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="a2092-153">Informacje są pomocne przy użyciu [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2092-153">That information is helpful when using the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="a2092-154">Dla poprzedniego kodu identyfikator zasobu do użycia jest pełna ścieżka do żądanego zasobu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2092-154">For the preceding code, the resource ID to use is the full path to the desired Azure resource.</span></span> <span data-ttu-id="a2092-155">Na przykład wykonać zapytanie względem aplikacji sieci Web platformy Azure, będzie identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="a2092-155">For example, to query against an Azure Web App, the resource ID would be:</span></span>

<span data-ttu-id="a2092-156">*/Subscriptions/{Subscription-ID}/resourceGroups/{Resource-group-name}/providers/Microsoft.Web/Sites/{Site-Name}/*</span><span class="sxs-lookup"><span data-stu-id="a2092-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="a2092-157">Poniższa lista zawiera kilka przykładów formaty identyfikator zasobu dla różnych zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a2092-157">The following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="a2092-158">**Centrum IoT** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Devices/IotHubs/*{iot hub nazwa-}*</span><span class="sxs-lookup"><span data-stu-id="a2092-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="a2092-159">**Puli elastycznej SQL** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{puli db}*/elasticpools/*{nazwa sql puli}*</span><span class="sxs-lookup"><span data-stu-id="a2092-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="a2092-160">**Baza danych SQL (v12)** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{nazwa serwera}* /databases/*{Nazwa bazy danych}*</span><span class="sxs-lookup"><span data-stu-id="a2092-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="a2092-161">**Usługa Service Bus** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.ServiceBus/*{przestrzeń nazw}* / *{magistrali usług nazwa}*</span><span class="sxs-lookup"><span data-stu-id="a2092-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="a2092-162">**Zestawy skalowania maszyny Wirtualnej** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ Nazwa maszyny wirtualnej}*</span><span class="sxs-lookup"><span data-stu-id="a2092-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="a2092-163">**Maszyny wirtualne** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachines/*{Nazwa maszyny wirtualnej}*</span><span class="sxs-lookup"><span data-stu-id="a2092-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="a2092-164">**Centra zdarzeń** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.EventHub/namespaces/*{ przestrzeń nazw eventhub}*</span><span class="sxs-lookup"><span data-stu-id="a2092-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="a2092-165">Istnieje kilka alternatywnych rozwiązań do pobierania identyfikator zasobu, w tym o korzystaniu z Eksploratora zasobów Azure, wyświetlanie żądanego zasobu w portalu Azure i przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="a2092-165">There are alternative approaches to retrieving the resource ID, including using Azure Resource Explorer, viewing the desired resource in the Azure portal, and via PowerShell or the Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="a2092-166">Eksplorator zasobów Azure</span><span class="sxs-lookup"><span data-stu-id="a2092-166">Azure Resource Explorer</span></span>
<span data-ttu-id="a2092-167">Aby znaleźć identyfikator zasobu dla żądanego zasobu, co przydatne rozwiązaniem jest użycie [Eksploratora zasobów Azure](https://resources.azure.com) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="a2092-167">To find the resource ID for a desired resource, one helpful approach is to use the [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="a2092-168">Przejdź do żądanego zasobu, a następnie sprawdź identyfikator pokazano, jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a2092-168">Navigate to the desired resource and then look at the ID shown, as in the following screenshot:</span></span>

![ALT "Eksploratora zasobów Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="a2092-170">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2092-170">Azure portal</span></span>
<span data-ttu-id="a2092-171">Identyfikator zasobu można uzyskać w taki sposób, w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a2092-171">The resource ID can also be obtained from the Azure portal.</span></span> <span data-ttu-id="a2092-172">Aby to zrobić, przejdź do żądanego zasobu, a następnie wybierz polecenie Właściwości.</span><span class="sxs-lookup"><span data-stu-id="a2092-172">To do so, navigate to the desired resource and then select Properties.</span></span> <span data-ttu-id="a2092-173">Identyfikator zasobu jest wyświetlany w bloku właściwości, jak pokazano na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a2092-173">The Resource ID is displayed in the Properties blade, as seen in the following screenshot:</span></span>

![ALT "identyfikator zasobu wyświetlane w bloku właściwości, w portalu Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="a2092-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2092-175">Azure PowerShell</span></span>
<span data-ttu-id="a2092-176">Identyfikator zasobu można pobrać przy użyciu również polecenia cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2092-176">The resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="a2092-177">Na przykład aby uzyskać identyfikator zasobu dla aplikacji sieci Web platformy Azure, wykonaj polecenie cmdlet Get-AzureRmWebApp, tak jak poniższy zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="a2092-177">For example, to obtain the resource ID for an Azure Web App, execute the Get-AzureRmWebApp cmdlet, as in the following screenshot:</span></span>

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="a2092-179">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a2092-179">Azure CLI</span></span>
<span data-ttu-id="a2092-180">Aby pobrać identyfikator zasobu przy użyciu wiersza polecenia platformy Azure, wykonaj polecenie "Pokaż aplikacji sieci Web platformy azure" określenie "--json" opcja, jak pokazano na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a2092-180">To retrieve the resource ID using the Azure CLI, execute the 'azure webapp show' command, specifying the '--json' option, as shown in the following screenshot:</span></span>

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="a2092-182">Pobieranie danych dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="a2092-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="a2092-183">Oprócz pracę z definicji metryk i powiązanych wartości, jest również możliwe odbieranie interesujące szerszych informacji związanych z zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2092-183">In addition to working with metric definitions and related values, it is also possible to retrieve additional interesting insights related to Azure resources.</span></span> <span data-ttu-id="a2092-184">Na przykład istnieje możliwość zapytania [dziennik aktywności](https://msdn.microsoft.com/library/azure/dn931934.aspx) danych.</span><span class="sxs-lookup"><span data-stu-id="a2092-184">As an example, it is possible to query [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="a2092-185">W poniższym przykładzie pokazano, przy użyciu interfejsu API REST Monitor Azure wykonać zapytania o dane dziennika aktywności w określonym zakresie dat. subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a2092-185">The following sample demonstrates using the Azure Monitor REST API to query activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="a2092-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2092-186">Next steps</span></span>
* <span data-ttu-id="a2092-187">Przegląd [omówienie monitorowania](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2092-187">Review the [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="a2092-188">Widok [obsługiwane metryki z monitorem Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a2092-188">View the [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="a2092-189">Przegląd [platformy Microsoft Azure monitorować dokumentacja interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2092-189">Review the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="a2092-190">Przegląd [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2092-190">Review the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
