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
# <a name="azure-monitoring-rest-api-walkthrough"></a>Monitorowanie wskazówki interfejsu API REST Azure
W tym artykule przedstawiono sposób uwierzytelniania, tak aby korzystać z kodu [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Monitor interfejsu API Azure umożliwia programowane pobieranie definicji metryk dostępnych domyślnych (typ metryki, takich jak czas procesora CPU, żądania, itp.), poziom szczegółowości i wartości metryki. Po pobraniu, dane można zapisać w magazynie oddzielnego danych, takie jak bazy danych SQL Azure, Azure DB rozwiązania Cosmos lub usługi Azure Data Lake. Z tego miejsca dodatkowe analizy mogą być wykonywane zgodnie z potrzebami.

Oprócz Praca z różnych punktów danych metryki, ponieważ w tym artykule przedstawiono, interfejsu API monitora umożliwia wyświetlić listę reguł alertów, widok Dzienniki aktywności i o wiele więcej. Aby uzyskać pełną listę dostępnych operacji, zobacz [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Uwierzytelniania Azure Monitor żądań
Pierwszym krokiem jest uwierzytelnić żądania.

Wszystkie zadania wykonywane monitora interfejsu API Azure używają modelu uwierzytelniania usługi Azure Resource Manager. W związku z tym wszystkie żądania musi zostać uwierzytelniony w usłudze Azure Active Directory (Azure AD). Jeden ze sposobów uwierzytelniania aplikacji klienckiej jest tworzenie nazwy głównej usługi Azure AD i pobrać tokenu uwierzytelniania (JWT). Poniższy przykładowy skrypt pokazuje tworzenie główną za pomocą programu PowerShell usługi Azure AD. Aby uzyskać bardziej szczegółowy przewodnik, zapoznaj się z dokumentacją na [Tworzenie nazwy głównej usługi dostępu do zasobów przy użyciu programu Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Istnieje również możliwość [Tworzenie nazwy głównej usługi za pośrednictwem portalu Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

Aby odpytać interfejsu API Azure monitora, aplikacja kliencka należy używać główną usługi utworzonej wcześniej do uwierzytelniania. W poniższym przykładzie skrypt programu PowerShell pokazano jedną podejścia, przy użyciu [biblioteki uwierzytelniania usługi Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL), aby pobrać tokenu uwierzytelniania tokenu JWT. JWT token jest przekazywany jako część parametrem autoryzacji HTTP w żądaniach do interfejsu API REST Azure monitora.

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

Po wykonaniu kroku konfiguracji uwierzytelniania następnie można wykonać zapytania do interfejsu API REST Monitor Azure. Istnieją dwa zapytania pomocne:

1. Lista definicje metryki dla zasobu
2. Pobieranie wartości metryki

## <a name="retrieve-metric-definitions"></a>Pobieranie definicji metryk
> [!NOTE]
> Aby pobrać definicji metryk przy użyciu interfejsu API REST Azure Monitor, należy użyć "2016-03-01" jako wersja interfejsu API.
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
Dla aplikacji logiki platformy Azure definicje metryk będzie wyglądać podobnie jak poniższy zrzut ekranu:

![ALT "Widok JSON odpowiedzi definicji metryk."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Aby uzyskać więcej informacji, zobacz [listy definicji metryk zasobu w interfejsie API REST Monitor Azure](https://msdn.microsoft.com/library/azure/mt743621.aspx) dokumentacji.

## <a name="retrieve-metric-values"></a>Pobieranie wartości metryki
Po definicji metryk dostępne są znane, następnie jest możliwe do pobierania wartości powiązane metryki. Nazwa metryki "wartość" (nie "localizedValue") na użytek żądań filtrowania (na przykład pobierania punktów danych metryki "CpuTime" i "Żądania"). Jeżeli nie określono żadnych filtrów, jest zwracana Metryka domyślnej.

> [!NOTE]
> Aby pobrać metryki wartości przy użyciu interfejsu API REST Azure Monitor, należy użyć "2016-06-01" jako wersja interfejsu API.
>
>

**Metoda**: GET

**Identyfikator URI żądania**: https://management.azure.com/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/*{ — — przestrzeń nazw dostawcy zasobów}*/*{typ zasobu}*/*{nazwa}*/providers/microsoft.insights/metrics?$filter= *{filtru}*& api-version =*{apiVersion}*

Na przykład pobierania punktów danych metryki RunsSucceeded dla danego okresie i ziarno czasu 1 godz, żądanie będzie następujące:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

Wynik pojawiały się podobny do następującego zrzutu ekranu:

![ALT "Odpowiedź w formacie JSON przedstawiający Średni czas odpowiedzi wartość metryki"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

Aby pobrać wiele punktów danych lub agregacji, Dodaj metryki definicji nazwy i typy agregacji do filtra, jak pokazano w poniższym przykładzie:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Użyj ARMClient
Zamiast przy użyciu programu PowerShell (jak pokazano powyżej), jest użycie [ARMClient](https://github.com/projectkudu/ARMClient) na komputerze z systemem Windows. ARMClient obsługuje automatycznie uwierzytelniania usługi Azure AD (i tokenu JWT). Poniższe kroki wchodzą w skład stosowania ARMClient pobierania danych metryki:

1. Zainstaluj [Chocolatey](https://chocolatey.org/) i [ARMClient](https://github.com/projectkudu/ARMClient).
2. W oknie terminalu, wpisz *logowania armclient.exe*. Monituje o logowanie do platformy Azure.
3. Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT "Using ARMClient do pracy z monitorowania Azure interfejsu API REST"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-the-resource-id"></a>Pobierz identyfikator zasobu
Dostępne metryki definicje, poziom szczegółowości i powiązane wartości naprawdę może pomóc przy użyciu interfejsu API REST. Informacje są pomocne przy użyciu [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Dla poprzedniego kodu identyfikator zasobu do użycia jest pełna ścieżka do żądanego zasobu platformy Azure. Na przykład wykonać zapytanie względem aplikacji sieci Web platformy Azure, będzie identyfikator zasobu:

*/Subscriptions/{Subscription-ID}/resourceGroups/{Resource-group-name}/providers/Microsoft.Web/Sites/{Site-Name}/*

Poniższa lista zawiera kilka przykładów formaty identyfikator zasobu dla różnych zasobów platformy Azure:

* **Centrum IoT** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Devices/IotHubs/*{iot hub nazwa-}*
* **Puli elastycznej SQL** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{puli db}*/elasticpools/*{nazwa sql puli}*
* **Baza danych SQL (v12)** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{nazwa serwera}* /databases/*{Nazwa bazy danych}*
* **Usługa Service Bus** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.ServiceBus/*{przestrzeń nazw}* / *{magistrali usług nazwa}*
* **Zestawy skalowania maszyny Wirtualnej** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ Nazwa maszyny wirtualnej}*
* **Maszyny wirtualne** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachines/*{Nazwa maszyny wirtualnej}*
* **Centra zdarzeń** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.EventHub/namespaces/*{ przestrzeń nazw eventhub}*

Istnieje kilka alternatywnych rozwiązań do pobierania identyfikator zasobu, w tym o korzystaniu z Eksploratora zasobów Azure, wyświetlanie żądanego zasobu w portalu Azure i przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure.

### <a name="azure-resource-explorer"></a>Eksplorator zasobów Azure
Aby znaleźć identyfikator zasobu dla żądanego zasobu, co przydatne rozwiązaniem jest użycie [Eksploratora zasobów Azure](https://resources.azure.com) narzędzia. Przejdź do żądanego zasobu, a następnie sprawdź identyfikator pokazano, jak na poniższym zrzucie ekranu:

![ALT "Eksploratora zasobów Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure Portal
Identyfikator zasobu można uzyskać w taki sposób, w portalu Azure. Aby to zrobić, przejdź do żądanego zasobu, a następnie wybierz polecenie Właściwości. Identyfikator zasobu jest wyświetlany w bloku właściwości, jak pokazano na poniższym zrzucie ekranu:

![ALT "identyfikator zasobu wyświetlane w bloku właściwości, w portalu Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Identyfikator zasobu można pobrać przy użyciu również polecenia cmdlet programu Azure PowerShell. Na przykład aby uzyskać identyfikator zasobu dla aplikacji sieci Web platformy Azure, wykonaj polecenie cmdlet Get-AzureRmWebApp, tak jak poniższy zrzut ekranu:

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Aby pobrać identyfikator zasobu przy użyciu wiersza polecenia platformy Azure, wykonaj polecenie "Pokaż aplikacji sieci Web platformy azure" określenie "--json" opcja, jak pokazano na poniższym zrzucie ekranu:

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Pobieranie danych dziennika aktywności
Oprócz pracę z definicji metryk i powiązanych wartości, jest również możliwe odbieranie interesujące szerszych informacji związanych z zasobów platformy Azure. Na przykład istnieje możliwość zapytania [dziennik aktywności](https://msdn.microsoft.com/library/azure/dn931934.aspx) danych. W poniższym przykładzie pokazano, przy użyciu interfejsu API REST Monitor Azure wykonać zapytania o dane dziennika aktywności w określonym zakresie dat. subskrypcji platformy Azure:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Następne kroki
* Przegląd [omówienie monitorowania](monitoring-overview.md).
* Widok [obsługiwane metryki z monitorem Azure](monitoring-supported-metrics.md).
* Przegląd [platformy Microsoft Azure monitorować dokumentacja interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Przegląd [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
