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
# <a name="azure-monitoring-rest-api-walkthrough"></a>Monitorowanie wskazówki interfejsu API REST Azure
W tym artykule opisano sposób uwierzytelniania tooperform dzięki kodu za pomocą hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hello interfejsu API Azure Monitor dzięki tooprogrammatically można pobrać hello dostępnych domyślnych definicji metryk (typ hello metryki, takich jak czas procesora CPU, żądania, itp.), poziom szczegółowości i wartości metryki. Po pobraniu danych hello mogą zostać zapisane w magazynie oddzielnego danych, takie jak bazy danych SQL Azure, Azure DB rozwiązania Cosmos lub usługi Azure Data Lake. Z tego miejsca dodatkowe analizy mogą być wykonywane zgodnie z potrzebami.

Oprócz Praca z różnych punktów danych metryki, ponieważ w tym artykule przedstawiono, hello API monitora ułatwia możliwe toolist reguły alertów, widok Dzienniki aktywności i o wiele więcej. Aby uzyskać pełną listę dostępnych operacji, zobacz hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Uwierzytelniania Azure Monitor żądań
pierwszym krokiem Hello jest tooauthenticate hello żądania.

Wszystkie zadania hello wykonywane hello interfejsu API Azure Monitor użycia hello Azure Resource Manager uwierzytelniania modelu. W związku z tym wszystkie żądania musi zostać uwierzytelniony w usłudze Azure Active Directory (Azure AD). Co aplikacja kliencka hello tooauthenticate podejście jest toocreate nazwy głównej usługi Azure AD i pobrać tokenu uwierzytelniania (JWT) hello. Witaj Poniższy przykładowy skrypt pokazuje Tworzenie nazwy głównej usługi za pomocą programu PowerShell usługi Azure AD. Bardziej szczegółowy przewodnik, można znaleźć w dokumentacji toohello na [przy użyciu programu Azure PowerShell toocreate zasobów tooaccess główna usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Możliwe jest również zbyt[Tworzenie nazwy głównej usługi za pośrednictwem portalu Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

tooquery hello Azure API monitora, powitania klienta aplikacji należy używać hello wcześniej utworzony tooauthenticate główną usługi. powitania po przykładowy skrypt programu PowerShell pokazuje jednym z podejść, przy użyciu hello [biblioteki uwierzytelniania usługi Active Directory](../active-directory/active-directory-authentication-libraries.md) toohelp (ADAL) pobrania tokenu uwierzytelniania JWT hello. Hello JWT token jest przekazywany jako część parametr autoryzacji HTTP w toohello żądania interfejsu API REST Monitor Azure.

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

Po wykonaniu kroku konfiguracji uwierzytelniania hello następnie można wykonać zapytania względem hello interfejsu API REST Monitor Azure. Istnieją dwa zapytania pomocne:

1. Definicje list hello metryki dla zasobu
2. Pobieranie wartości metryki hello

## <a name="retrieve-metric-definitions"></a>Pobieranie definicji metryk
> [!NOTE]
> definicje metryk tooretrieve przy użyciu hello interfejsu API REST Monitor Azure, użyj "2016-03-01", zgodnie z hello wersja interfejsu API.
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
Dla aplikacji logiki platformy Azure definicje metryk hello pojawiały się podobne toohello po zrzut ekranu:

![ALT "Widok JSON odpowiedzi definicji metryk."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Aby uzyskać więcej informacji, zobacz hello [listy hello definicje metryki dla zasobu w interfejsie API REST Monitor Azure](https://msdn.microsoft.com/library/azure/mt743621.aspx) dokumentacji.

## <a name="retrieve-metric-values"></a>Pobieranie wartości metryki
Po definicji metryk dostępnych hello są znane, jest następnie możliwe tooretrieve hello powiązanych wartości metryki. Nazwa metryki Witaj "wartość" (nie hello "localizedValue") na użytek żądań filtrowania (na przykład pobranie hello "CpuTime" i "Żądania" metryki punktów danych). Jeżeli nie określono żadnych filtrów, jest zwracana hello metrykę.

> [!NOTE]
> wartości metryk tooretrieve przy użyciu hello interfejsu API REST Monitor Azure, użyj "2016-06-01", zgodnie z hello wersja interfejsu API.
>
>

**Metoda**: GET

**Identyfikator URI żądania**: https://management.azure.com/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/*{ — — przestrzeń nazw dostawcy zasobów}*/*{typ zasobu}*/*{nazwa}*/providers/microsoft.insights/metrics?$filter= *{filtru}*& api-version =*{apiVersion}*

Na przykład tooretrieve hello RunsSucceeded metryki punktów danych dla hello podany zakres czasu i ziarno czasu 1 godziny, Żądanie hello będzie w następujący sposób:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

wynik Hello pojawiały się podobny przykład toohello po zrzut ekranu:

![ALT "Odpowiedź w formacie JSON przedstawiający Średni czas odpowiedzi wartość metryki"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve wielu danych lub agregacji punktów, Dodaj nazwy definicji metryk hello i filtra toohello typów agregacji, widziany hello poniższy przykład:

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
Alternatywne toousing środowiska PowerShell (jak pokazano powyżej), jest toouse [ARMClient](https://github.com/projectkudu/ARMClient) na komputerze z systemem Windows. ARMClient obsługuje automatycznie uwierzytelniania hello Azure AD (i tokenu JWT). Witaj poniższe kroki wchodzą w skład stosowania ARMClient pobierania danych metryki:

1. Zainstaluj [Chocolatey](https://chocolatey.org/) i [ARMClient](https://github.com/projectkudu/ARMClient).
2. W oknie terminalu, wpisz *logowania armclient.exe*. Monit toolog w tooAzure.
3. Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Typ *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT "Toowork ARMClient korzystanie z interfejsu API REST Azure monitorowanie hello"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Pobrać hello identyfikator zasobu
Przy użyciu interfejsu API REST hello naprawdę może pomóc toounderstand hello dostępne metryki definicje, poziom szczegółowości oraz powiązanych wartości. Te informacje są pomocne przy użyciu hello [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Dla hello poprzedzających kodu toouse identyfikator zasobu hello jest toohello pełną ścieżkę hello potrzeby zasobów platformy Azure. Na przykład tooquery względem aplikacji sieci Web platformy Azure, identyfikator zasobu hello będzie:

*/Subscriptions/{Subscription-ID}/resourceGroups/{Resource-group-name}/providers/Microsoft.Web/Sites/{Site-Name}/*

Witaj Poniższa lista zawiera kilka przykładów formaty identyfikator zasobu dla różnych zasobów platformy Azure:

* **Centrum IoT** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Devices/IotHubs/*{iot hub nazwa-}*
* **Puli elastycznej SQL** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{puli db}*/elasticpools/*{nazwa sql puli}*
* **Baza danych SQL (v12)** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Sql/servers/*{nazwa serwera}* /databases/*{Nazwa bazy danych}*
* **Usługa Service Bus** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.ServiceBus/*{przestrzeń nazw}* / *{magistrali usług nazwa}*
* **Zestawy skalowania maszyny Wirtualnej** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{ Nazwa maszyny wirtualnej}*
* **Maszyny wirtualne** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.Compute/virtualMachines/*{Nazwa maszyny wirtualnej}*
* **Centra zdarzeń** -/subscriptions/*{identyfikator subskrypcji}*/resourceGroups/*{— Nazwa grupy zasobów-}*/providers/Microsoft.EventHub/namespaces/*{ przestrzeń nazw eventhub}*

Brak alternatywnych metod tooretrieving hello zasobów Identyfikatora, w tym za pomocą Eksploratora zasobów Azure, wyświetlanie hello żądanego zasobu w hello portalu Azure i przy użyciu programu PowerShell lub hello wiersza polecenia platformy Azure.

### <a name="azure-resource-explorer"></a>Eksplorator zasobów Azure
Identyfikator zasobu hello toofind dla żądanego zasobu, jednym z podejść pomocne jest toouse hello [Eksploratora zasobów Azure](https://resources.azure.com) narzędzia. Przejdź toohello żądanego zasobu, a następnie sprawdź identyfikator hello pokazano, jak powitania po zrzut ekranu:

![ALT "Eksploratora zasobów Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure Portal
Identyfikator zasobu Hello również można uzyskać z hello portalu Azure. toodo tak, przejdź toohello żądanego zasobu, a następnie wybierz właściwości. Hello identyfikator zasobu jest wyświetlany w hello bloku właściwości, jak pokazano w powitania po zrzut ekranu:

![ALT "identyfikator zasobu wyświetlane w bloku właściwości hello w portalu Azure hello"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Identyfikator zasobu Hello można pobrać przy użyciu również polecenia cmdlet programu Azure PowerShell. Na przykład identyfikator zasobu hello tooobtain dla aplikacji sieci Web platformy Azure, wykonaj polecenie cmdlet hello Get AzureRmWebApp, jak powitania po zrzut ekranu:

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
tooretrieve hello Identyfikatora zasobów przy użyciu hello wiersza polecenia platformy Azure, wykonaj polecenie "Pokaż azure aplikacji sieci Web" hello, określając hello "--json" opcja, jak pokazano w powitania po zrzut ekranu:

![ALT "identyfikator zasobu uzyskany za pomocą programu PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Pobieranie danych dziennika aktywności
W dodatku tooworking z definicji metryk i powiązanych wartości jest również możliwe tooretrieve dodatkowe interesujące insights tooAzure powiązane zasoby. Na przykład jest możliwe tooquery [dziennik aktywności](https://msdn.microsoft.com/library/azure/dn931934.aspx) danych. Witaj poniższym przykładzie pokazano przy użyciu danych dziennika hello interfejsu API REST Monitor Azure tooquery działanie w określonym zakresie dat. subskrypcji platformy Azure:

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
* Przejrzyj hello [omówienie monitorowania](monitoring-overview.md).
* Widok hello [obsługiwane metryki z monitorem Azure](monitoring-supported-metrics.md).
* Przejrzyj hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Przejrzyj hello [Biblioteka zarządzania Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
