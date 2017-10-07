---
title: "aaaAzure wskazówki monitorowanie interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Jak tooauthenticate żądań tooand hello Użyj interfejsu API REST Azure monitorowania."
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
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="736fc-103">Monitorowanie wskazówki interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="736fc-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="736fc-104">W tym artykule opisano sposób uwierzytelniania tooperform dzięki kodu za pomocą hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="736fc-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="736fc-105">Hello interfejsu API Azure Monitor dzięki tooprogrammatically można pobrać hello dostępnych domyślnych definicji metryk (typ hello metryki, takich jak czas procesora CPU, żądania, itp.), poziom szczegółowości i wartości metryki.</span><span class="sxs-lookup"><span data-stu-id="736fc-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="736fc-106">Po pobraniu danych hello mogą zostać zapisane w magazynie oddzielnego danych, takie jak bazy danych SQL Azure, Azure DB rozwiązania Cosmos lub usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="736fc-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="736fc-107">Z tego miejsca dodatkowe analizy mogą być wykonywane zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="736fc-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="736fc-108">Oprócz Praca z różnych punktów danych metryki, ponieważ w tym artykule przedstawiono, hello API monitora ułatwia możliwe toolist reguły alertów, widok Dzienniki aktywności i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="736fc-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="736fc-109">Aby uzyskać pełną listę dostępnych operacji, zobacz hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="736fc-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="736fc-110">Uwierzytelniania Azure Monitor żądań</span><span class="sxs-lookup"><span data-stu-id="736fc-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="736fc-111">pierwszym krokiem Hello jest tooauthenticate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="736fc-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="736fc-112">Wszystkie zadania hello wykonywane hello interfejsu API Azure Monitor użycia hello Azure Resource Manager uwierzytelniania modelu.</span><span class="sxs-lookup"><span data-stu-id="736fc-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="736fc-113">W związku z tym wszystkie żądania musi zostać uwierzytelniony w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="736fc-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="736fc-114">Co aplikacja kliencka hello tooauthenticate podejście jest toocreate nazwy głównej usługi Azure AD i pobrać tokenu uwierzytelniania (JWT) hello.</span><span class="sxs-lookup"><span data-stu-id="736fc-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="736fc-115">Witaj Poniższy przykładowy skrypt pokazuje Tworzenie nazwy głównej usługi za pomocą programu PowerShell usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="736fc-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="736fc-116">Bardziej szczegółowy przewodnik, można znaleźć w dokumentacji toohello na [przy użyciu programu Azure PowerShell toocreate zasobów tooaccess główna usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="736fc-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="736fc-117">Możliwe jest również zbyt[Tworzenie nazwy głównej usługi za pośrednictwem portalu Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="736fc-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="736fc-118">tooquery hello Azure API monitora, powitania klienta aplikacji należy używać hello wcześniej utworzony tooauthenticate główną usługi.</span><span class="sxs-lookup"><span data-stu-id="736fc-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="736fc-119">powitania po przykładowy skrypt programu PowerShell pokazuje jednym z podejść, przy użyciu hello [biblioteki uwierzytelniania usługi Active Directory](../active-directory/active-directory-authentication-libraries.md) toohelp (ADAL) pobrania tokenu uwierzytelniania JWT hello.</span><span class="sxs-lookup"><span data-stu-id="736fc-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="736fc-120">Hello JWT token jest przekazywany jako część parametr autoryzacji HTTP w toohello żądania interfejsu API REST Monitor Azure.</span><span class="sxs-lookup"><span data-stu-id="736fc-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

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

<span data-ttu-id="736fc-121">Po wykonaniu kroku konfiguracji uwierzytelniania hello następnie można wykonać zapytania względem hello interfejsu API REST Monitor Azure.</span><span class="sxs-lookup"><span data-stu-id="736fc-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="736fc-122">Istnieją dwa zapytania pomocne:</span><span class="sxs-lookup"><span data-stu-id="736fc-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="736fc-123">Definicje list hello metryki dla zasobu</span><span class="sxs-lookup"><span data-stu-id="736fc-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="736fc-124">Pobieranie wartości metryki hello</span><span class="sxs-lookup"><span data-stu-id="736fc-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="736fc-125">Pobieranie definicji metryk</span><span class="sxs-lookup"><span data-stu-id="736fc-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="736fc-126">definicje metryk tooretrieve przy użyciu hello interfejsu API REST Monitor Azure, użyj "2016-03-01", zgodnie z hello wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="736fc-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
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
<span data-ttu-id="736fc-127">Dla aplikacji logiki platformy Azure definicje metryk hello pojawiały się podobne toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="736fc-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![ALT "Widok JSON odpowiedzi definicji metryk."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="736fc-129">Aby uzyskać więcej informacji, zobacz hello [listy hello definicje metryki dla zasobu w interfejsie API REST Monitor Azure](https://msdn.microsoft.com/library/azure/mt743621.aspx) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="736fc-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="736fc-130">Pobieranie wartości metryki</span><span class="sxs-lookup"><span data-stu-id="736fc-130">Retrieve Metric Values</span></span>
<span data-ttu-id="736fc-131">Po definicji metryk dostępnych hello są znane, jest następnie możliwe tooretrieve hello powiązanych wartości metryki.</span><span class="sxs-lookup"><span data-stu-id="736fc-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="736fc-132">Nazwa metryki Witaj "wartość" (nie hello "localizedValue") na użytek żądań filtrowania (na przykład pobranie hello "CpuTime" i "Żądania" metryki punktów danych).</span><span class="sxs-lookup"><span data-stu-id="736fc-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="736fc-133">Jeżeli nie określono żadnych filtrów, jest zwracana hello metrykę.</span><span class="sxs-lookup"><span data-stu-id="736fc-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="736fc-134">wartości metryk tooretrieve przy użyciu hello interfejsu API REST Monitor Azure, użyj "2016-06-01", zgodnie z hello wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="736fc-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="736fc-135">**Metoda**: GET</span><span class="sxs-lookup"><span data-stu-id="736fc-135">**Method**: GET</span></span>

<span data-ttu-id="736fc-136">**Identyfikator URI żądania**: https://management.azure.com/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/*{ — — przestrzeń nazw dostawcy zasobów}*/*{typ zasobu}*/*{nazwa}*/providers/microsoft.insights/metrics?$filter= *{filtru}*& api-version =*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="736fc-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="736fc-137">Na przykład tooretrieve hello RunsSucceeded metryki punktów danych dla hello podany zakres czasu i ziarno czasu 1 godziny, Żądanie hello będzie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="736fc-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="736fc-138">wynik Hello pojawiały się podobny przykład toohello po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="736fc-138">hello result would appear similar toohello example following screenshot:</span></span>

![ALT "Odpowiedź w formacie JSON przedstawiający Średni czas odpowiedzi wartość metryki"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="736fc-140">tooretrieve wielu danych lub agregacji punktów, Dodaj nazwy definicji metryk hello i filtra toohello typów agregacji, widziany hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="736fc-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="736fc-141">Użyj ARMClient</span><span class="sxs-lookup"><span data-stu-id="736fc-141">Use ARMClient</span></span>
<span data-ttu-id="736fc-142">Alternatywne toousing środowiska PowerShell (jak pokazano powyżej), jest toouse [ARMClient](https://github.com/projectkudu/ARMClient) na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="736fc-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="736fc-143">ARMClient obsługuje automatycznie uwierzytelniania hello Azure AD (i tokenu JWT).</span><span class="sxs-lookup"><span data-stu-id="736fc-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="736fc-144">Witaj poniższe kroki wchodzą w skład stosowania ARMClient pobierania danych metryki:</span><span class="sxs-lookup"><span data-stu-id="736fc-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="736fc-145">Zainstaluj [Chocolatey](https://chocolatey.org/) i [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="736fc-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="736fc-146">W oknie terminalu, wpisz *logowania armclient.exe*.</span><span class="sxs-lookup"><span data-stu-id="736fc-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="736fc-147">Monit toolog w tooAzure.</span><span class="sxs-lookup"><span data-stu-id="736fc-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="736fc-148">Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="736fc-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="736fc-149">Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="736fc-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT "Toowork ARMClient korzystanie z interfejsu API REST Azure monitorowanie hello"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="736fc-151">Pobrać hello identyfikator zasobu</span><span class="sxs-lookup"><span data-stu-id="736fc-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="736fc-152">Przy użyciu interfejsu API REST hello naprawdę może pomóc toounderstand hello dostępne metryki definicje, poziom szczegółowości oraz powiązanych wartości.</span><span class="sxs-lookup"><span data-stu-id="736fc-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="736fc-153">Te informacje są pomocne przy użyciu hello [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="736fc-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="736fc-154">Dla hello poprzedzających kodu toouse identyfikator zasobu hello jest toohello pełną ścieżkę hello potrzeby zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="736fc-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="736fc-155">Na przykład tooquery względem aplikacji sieci Web platformy Azure, identyfikator zasobu hello będzie:</span><span class="sxs-lookup"><span data-stu-id="736fc-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="736fc-156">*/Subscriptions/{Subscription-ID}/resourceGroups/{Resource-group-name}/providers/Microsoft.Web/Sites/{Site-Name}/*</span><span class="sxs-lookup"><span data-stu-id="736fc-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="736fc-157">Witaj Poniższa lista zawiera kilka przykładów formaty identyfikator zasobu dla różnych zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="736fc-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="736fc-158">**Centrum IoT** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Devices/IotHubs/*{iot hub nazwa-}*</span><span class="sxs-lookup"><span data-stu-id="736fc-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="736fc-159">**Puli elastycznej SQL** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{puli db}*/elasticpools/*{nazwa sql puli}*</span><span class="sxs-lookup"><span data-stu-id="736fc-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="736fc-160">**Baza danych SQL (v12)** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{nazwa serwera}* /databases/*{Nazwa bazy danych}*</span><span class="sxs-lookup"><span data-stu-id="736fc-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="736fc-161">**Usługa Service Bus** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.ServiceBus/*{przestrzeń nazw}* / *{magistrali usług nazwa}*</span><span class="sxs-lookup"><span data-stu-id="736fc-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="736fc-162">**Zestawy skalowania maszyny Wirtualnej** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ Nazwa maszyny wirtualnej}*</span><span class="sxs-lookup"><span data-stu-id="736fc-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="736fc-163">**Maszyny wirtualne** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachines/*{Nazwa maszyny wirtualnej}*</span><span class="sxs-lookup"><span data-stu-id="736fc-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="736fc-164">**Centra zdarzeń** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.EventHub/namespaces/*{ przestrzeń nazw eventhub}*</span><span class="sxs-lookup"><span data-stu-id="736fc-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="736fc-165">Brak alternatywnych metod tooretrieving hello zasobów Identyfikatora, w tym za pomocą Eksploratora zasobów Azure, wyświetlanie hello żądanego zasobu w hello portalu Azure i przy użyciu programu PowerShell lub hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="736fc-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="736fc-166">Eksplorator zasobów Azure</span><span class="sxs-lookup"><span data-stu-id="736fc-166">Azure Resource Explorer</span></span>
<span data-ttu-id="736fc-167">Identyfikator zasobu hello toofind dla żądanego zasobu, jednym z podejść pomocne jest toouse hello [Eksploratora zasobów Azure](https://resources.azure.com) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="736fc-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="736fc-168">Przejdź toohello żądanego zasobu, a następnie sprawdź identyfikator hello pokazano, jak powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="736fc-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![ALT "Eksploratora zasobów Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="736fc-170">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="736fc-170">Azure portal</span></span>
<span data-ttu-id="736fc-171">Identyfikator zasobu Hello również można uzyskać z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="736fc-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="736fc-172">toodo tak, przejdź toohello żądanego zasobu, a następnie wybierz właściwości.</span><span class="sxs-lookup"><span data-stu-id="736fc-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="736fc-173">Hello identyfikator zasobu jest wyświetlany w hello bloku właściwości, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="736fc-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT "identyfikator zasobu wyświetlane w bloku właściwości hello w portalu Azure hello"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="736fc-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="736fc-175">Azure PowerShell</span></span>
<span data-ttu-id="736fc-176">Identyfikator zasobu Hello można pobrać przy użyciu również polecenia cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="736fc-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="736fc-177">Na przykład identyfikator zasobu hello tooobtain dla aplikacji sieci Web platformy Azure, wykonaj polecenie cmdlet hello Get AzureRmWebApp, jak powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="736fc-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="736fc-179">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="736fc-179">Azure CLI</span></span>
<span data-ttu-id="736fc-180">tooretrieve hello Identyfikatora zasobów przy użyciu hello wiersza polecenia platformy Azure, wykonaj polecenie "Pokaż azure aplikacji sieci Web" hello, określając hello "--json" opcja, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="736fc-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="736fc-182">Pobieranie danych dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="736fc-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="736fc-183">W dodatku tooworking z definicji metryk i powiązanych wartości jest również możliwe tooretrieve dodatkowe interesujące insights tooAzure powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="736fc-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="736fc-184">Na przykład jest możliwe tooquery [dziennik aktywności](https://msdn.microsoft.com/library/azure/dn931934.aspx) danych.</span><span class="sxs-lookup"><span data-stu-id="736fc-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="736fc-185">Witaj poniższym przykładzie pokazano przy użyciu danych dziennika hello interfejsu API REST Monitor Azure tooquery działanie w określonym zakresie dat. subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="736fc-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="736fc-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="736fc-186">Next steps</span></span>
* <span data-ttu-id="736fc-187">Przejrzyj hello [omówienie monitorowania](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="736fc-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="736fc-188">Widok hello [obsługiwane metryki z monitorem Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="736fc-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="736fc-189">Przejrzyj hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="736fc-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="736fc-190">Przejrzyj hello [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="736fc-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
