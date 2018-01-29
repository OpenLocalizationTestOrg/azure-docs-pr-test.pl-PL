---
title: "Schemat zdarzenia dziennika aktywności platformy Azure | Dokumentacja firmy Microsoft"
description: "Zrozumienie schematu zdarzeń do dziennika aktywności danych"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2017
ms.author: johnkem
ms.openlocfilehash: 91129da9ef7791a506292d9e13e386a25ee341a8
ms.sourcegitcommit: 9c3150e91cc3075141dc2955a01f47040d76048a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/26/2017
---
# <a name="azure-activity-log-event-schema"></a>Schematu zdarzeń dziennika aktywności platformy Azure
**Dziennika aktywności platformy Azure** jest dziennika, który zapewnia wgląd w wszelkie zdarzenia poziomu subskrypcji, które wystąpiły na platformie Azure. W tym artykule opisano schematu zdarzeń na kategorię danych.

## <a name="administrative"></a>Administracyjne
Ta kategoria zawiera rekord wszystkich utworzyć, update, delete i akcji operacje wykonywane za pomocą Menedżera zasobów. Typy zdarzeń, które można zobaczyć w tej kategorii należą "Utwórz maszynę wirtualną" i "Usuń sieciową grupę zabezpieczeń" co akcję wykonywaną przez użytkownika lub aplikacji przy użyciu usługi Resource Manager ma formę operację określonego typu zasobu. W przypadku typu operacji zapisu, usuń lub działania, rekordy start i powodzenie lub niepowodzenie tej operacji są rejestrowane w kategorii administracyjnej. Kategoria administracyjna także wszystkie zmiany do kontroli dostępu opartej na rolach w ramach subskrypcji.

### <a name="sample-event"></a>Zdarzenie próbkowania
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Opisy właściwości
| Nazwa elementu | Opis |
| --- | --- |
| Autoryzacji |Obiekt typu blob RBAC właściwości zdarzenia. Zwykle zawiera właściwości "Akcja" i "rola" 'scope'. |
| obiekt wywołujący |Adres e-mail użytkownika, który wykonał operację, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności. |
| Kanały |Jedną z następujących wartości: "Administrator", "Operacji" |
| Oświadczenia |Token JWT używanych przez usługi Active Directory do uwierzytelniania użytkownika lub aplikacji do wykonania tej operacji w Menedżera zasobów. |
| correlationId |Zazwyczaj identyfikator GUID w postaci ciągu. Zdarzenia, które mają correlationId należą do tego samego działania pełny. |
| description |Statyczny tekst opisu zdarzenia. |
| eventDataId |Unikatowy identyfikator zdarzenia. |
| httpRequest |Obiekt typu blob opisujące żądania Http. Obejmuje zazwyczaj "clientRequestId", "clientIpAddress" i "method" (metoda HTTP. For example, PUT). |
| poziom |Poziom zdarzenia. Jedną z następujących wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| Grupy zasobów o nazwie |Nazwa grupy zasobów dla zasobu ryzyko. |
| resourceProviderName |Nazwa dostawcy zasobu dla zasobu wpływ na |
| resourceId |Identyfikator zasobu ryzyko zasobu. |
| operationId |Identyfikator GUID współdzielenia zdarzenia, które odpowiadają jednej operacji. |
| operationName |Nazwa operacji. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły zdarzenia. |
| status |Ciąg opisujący stan operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan |Zazwyczaj wywołań REST odpowiedni kod stanu HTTP, ale można również uwzględnić inne parametry opisujące podstanu, takich jak te wartości typowych: OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (kod stanu HTTP: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP : 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503), limit czasu bramy (kod stanu HTTP: 504). |
| eventTimestamp |Sygnatura czasowa po zdarzeniu został wygenerowany przez usługę Azure przetwarzania żądania odpowiednie zdarzenie. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

## <a name="service-health"></a>Kondycja usługi
Ta kategoria zawiera rekord określone zdarzenia kondycji usługi, które wystąpiły na platformie Azure. Przykładem typu zdarzenia, które widać w tej kategorii jest "Azure SQL w wschodnie stany USA występuje Przestój." Zdarzenia kondycji usługi są dostępne w pięciu odmian: wymagana akcja, wspierana odzyskiwania, zdarzenie, konserwacji, informacje lub zabezpieczeń i są wyświetlane tylko, jeśli zasób w subskrypcji, która może wpływać na zdarzenia.

### <a name="sample-event"></a>Zdarzenie próbkowania
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Opisy właściwości
Nazwa elementu | Opis
-------- | -----------
Kanały | Jest jednym z następujących wartości: "Administrator", "Operacji"
correlationId | Jest zazwyczaj identyfikator GUID w postaci ciągu. Zdarzenia z tym należy do tego samego działania pełny zwykle udostępnianie tego samego correlationId.
description | Opis zdarzenia.
eventDataId | Unikatowy identyfikator zdarzenia.
EventName | Nazwa zdarzenia.
poziom | Poziom zdarzenia. Jedną z następujących wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"
resourceProviderName | Nazwa dostawcy zasobów dla zasobu ryzyko. Jeśli nie jest znany, będzie to wartość null.
Typ zasobu| Typ zasobu ryzyko zasobu. Jeśli nie jest znany, będzie to wartość null.
Podstan | Zazwyczaj o wartości null dla zdarzenia kondycji usługi.
eventTimestamp | Znacznik czasu w momencie dziennik zdarzeń został wygenerowany i przesłane do dziennika aktywności.
submissionTimestamp |   Znacznik czasu w momencie zdarzenia stały się dostępne w dzienniku aktywności.
subscriptionId | Subskrypcja platformy Azure, w którym zarejestrowano to zdarzenie.
status | Ciąg opisujący stan operacji. Niektóre typowe wartości to: aktywne, rozwiązane.
operationName | Nazwa operacji. Zazwyczaj Microsoft.ServiceHealth/incident/action.
category | "ServiceHealth"
resourceId | Identyfikator zasobu ryzyko zasobu, jeśli znane. W przeciwnym razie podany identyfikator subskrypcji.
Properties.Title | Tytuł zlokalizowane dla tej komunikacji. Językiem domyślnym będzie angielski.
Properties.Communication | Szczegóły zlokalizowanych komunikacji z kodu znaczników HTML. Domyślnym będzie angielski.
Properties.incidentType | Możliwe wartości: AssistedRecovery, ActionRequired, informacje, zdarzenie, obsługi, zabezpieczeń
Properties.trackingId | Identyfikuje incydent, który jest skojarzony to zdarzenie. Umożliwia korelowanie zdarzeń związanych ze zdarzeniem.
Properties.impactedServices | Zmienionym obiektu blob JSON opisującą usług i regionów, które mają wpływ zdarzenia. Lista usług, z których każda ma elementy ServiceName i listę ImpactedRegions, z których każda ma RegionName.
Properties.defaultLanguageTitle | Komunikat w języku angielskim
Properties.defaultLanguageContent | Komunikat w języku angielskim jako kod znaczników html i zwykły tekst
Properties.Stage | Możliwe wartości AssistedRecovery, ActionRequired, informacje, zdarzenie, zabezpieczeń: są aktywne, rozwiązane. W konserwacji są: aktywny, planowane, w toku, anulowane, Rescheduled, rozwiązane, Zakończ
Properties.communicationId | Komunikacja to zdarzenie jest skojarzony.

## <a name="alert"></a>Alerty
Ta kategoria zawiera rekord wszystkich aktywacji Azure alertów. Przykładem typu zdarzenia, które widać w tej kategorii jest "procent użycia procesora CPU na myVM została ponad 80 dla ostatnich 5 minut." Z różnymi systemami Azure ma alertów koncepcji — można zdefiniować regułę jakiegoś i otrzymasz powiadomienie, gdy warunki reguły są zgodne. Zawsze Azure obsługiwanego typu alertu "aktywuje," lub warunki są spełnione, aby wygenerować powiadomienie, rekord aktywacji jest również przypisany do tej kategorii dziennik aktywności.

### <a name="sample-event"></a>Zdarzenie próbkowania

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Opisy właściwości
| Nazwa elementu | Opis |
| --- | --- |
| obiekt wywołujący | Zawsze Microsoft.Insights/alertRules |
| Kanały | Zawsze "Admin, operację" |
| Oświadczenia | Obiektu blob JSON z typem głównej nazwy usługi (nazwy głównej usługi) lub zasób, aparat alertów. |
| correlationId | Identyfikator GUID w postaci ciągu. |
| description |Tekst statyczny opis alertu zdarzenia. |
| eventDataId |Unikatowy identyfikator zdarzenia alertu. |
| poziom |Poziom zdarzenia. Jedną z następujących wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| Grupy zasobów o nazwie |Nazwa grupy zasobów dla wpływ na zasobu, jeśli jest to alert metryki. Inne typy alertów jest to nazwa grupy zasobów, która zawiera samego alertu. |
| resourceProviderName |Nazwa dostawcy zasobów wpływ na zasobu, jeśli jest to alert metryki. Inne typy alertów jest to nazwa dostawcy zasobów dla samego alertu. |
| resourceId | Nazwa identyfikatora zasobu wpływ na zasobu, jeśli jest to alert metryki. Inne typy alertów jest to identyfikator zasobu alertu zasobu sam. |
| operationId |Identyfikator GUID współdzielenia zdarzenia, które odpowiadają jednej operacji. |
| operationName |Nazwa operacji. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły zdarzenia. |
| status |Ciąg opisujący stan operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan | Zazwyczaj o wartości null dla alertów. |
| eventTimestamp |Sygnatura czasowa po zdarzeniu został wygenerowany przez usługę Azure przetwarzania żądania odpowiednie zdarzenie. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

### <a name="properties-field-per-alert-type"></a>Pole właściwości typu alertu
Pole właściwości będzie zawierać różne wartości w zależności od źródła zdarzeń alertów. Dwóch dostawców typowych zdarzeń alertów są alerty dziennika aktywności i metryki alerty.

#### <a name="properties-for-activity-log-alerts"></a>Właściwości alertów dziennik aktywności
| Nazwa elementu | Opis |
| --- | --- |
| properties.subscriptionId | Identyfikator subskrypcji z dziennika zdarzeń działania, który spowodował tę regułę alertów dziennika aktywności do aktywacji. |
| properties.eventDataId | Identyfikator danych zdarzenia z dziennika zdarzeń działania, który spowodował tę regułę alertów dziennika aktywności do aktywacji. |
| properties.resourceGroup | Grupy zasobów z dziennika zdarzeń działania, który spowodował tę regułę alertów dziennika aktywności do aktywacji. |
| properties.resourceId | Identyfikator zasobu z dziennika zdarzeń działania, który spowodował tę regułę alertów dziennika aktywności do aktywacji. |
| properties.eventTimestamp | Sygnatura czasowa zdarzenia dziennika zdarzeń działania, który spowodował tę regułę alertów dziennika aktywności do aktywacji. |
| properties.operationName | Nazwa operacji z dziennika zdarzeń działania, który spowodował tę regułę alertów dziennika aktywności do aktywacji. |
| Properties.status | Stan działania dziennika zdarzeń, który spowodował tę regułę alertów dziennika aktywności do aktywacji.|

#### <a name="properties-for-metric-alerts"></a>Właściwości alertów metryki
| Nazwa elementu | Opis |
| --- | --- |
| właściwości. RuleUri | Identyfikator zasobu metryki reguły alertu samej siebie. |
| właściwości. RuleName | Nazwa metryki reguły alertów. |
| właściwości. RuleDescription | Opis metryki reguły alertu (zgodnie z definicją w regule alertu). |
| właściwości. Próg | Wartość progowa, używana podczas obliczania metryki reguły alertów. |
| właściwości. WindowSizeInMinutes | Rozmiar okna używana podczas obliczania metryki reguły alertów. |
| właściwości. Agregacji | Typ agregacji zdefiniowane w regule alertu metryki. |
| właściwości. Operator | Operator warunkowy używana podczas obliczania metryki reguły alertów. |
| właściwości. MetricName | Nazwa metryki metryki używana podczas obliczania metryki reguły alertów. |
| właściwości. MetricUnit | Metryki jednostka Metryka używana podczas obliczania metryki reguły alertów. |

## <a name="autoscale"></a>Automatyczne skalowanie
Ta kategoria zawiera rekord wszystkie zdarzenia związane z operacji skalowania automatycznego aparatu oparte na ustawienia skalowania automatycznego zdefiniowanych w ramach subskrypcji. Przykładem typu zdarzenia, które widać w tej kategorii jest "Skalowania automatycznego skalowania w górę akcja nie powiodła się". Przy użyciu automatycznego skalowania, można automatycznie skalować w poziomie lub skalowanie liczby wystąpień w typie zasobów obsługiwanych na podstawie czasu dnia i/lub obciążenia () dane przy użyciu ustawienia skalowania automatycznego. Jeśli warunki są spełnione, aby skalowania w górę lub w dół, uruchamiania i zakończyło się pomyślnie lub niepowodzeniem zdarzenia będą rejestrowane w tej kategorii.

### <a name="sample-event"></a>Zdarzenie próbkowania
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Opisy właściwości
| Nazwa elementu | Opis |
| --- | --- |
| obiekt wywołujący | Zawsze Microsoft.Insights/autoscaleSettings |
| Kanały | Zawsze "Admin, operację" |
| Oświadczenia | Obiektu blob JSON z typem głównej nazwy usługi (nazwy głównej usługi) lub zasobów, aparatu skalowania automatycznego. |
| correlationId | Identyfikator GUID w postaci ciągu. |
| description |Opis zdarzenia skalowania automatycznego tekst statyczny. |
| eventDataId |Unikatowy identyfikator zdarzenia automatycznego skalowania. |
| poziom |Poziom zdarzenia. Jedną z następujących wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| Grupy zasobów o nazwie |Nazwa grupy zasobów w ustawieniu skalowania automatycznego. |
| resourceProviderName |Nazwa dostawcy zasobów w ustawieniu skalowania automatycznego. |
| resourceId |Identyfikator zasobu w ustawieniu skalowania automatycznego. |
| operationId |Identyfikator GUID współdzielenia zdarzenia, które odpowiadają jednej operacji. |
| operationName |Nazwa operacji. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły zdarzenia. |
| właściwości. Opis elementu | Szczegółowy opis wykonywanych czynności został aparat skalowania automatycznego. |
| właściwości. ResourceName | Identyfikator zasobu ryzyko zasobu (zasobu, na którym wykonywana akcji skalowania) |
| właściwości. OldInstancesCount | Liczba wystąpień przed akcji skalowania automatycznego weszły w życie. |
| właściwości. NewInstancesCount | Liczba wystąpień po akcji skalowania automatycznego weszły w życie. |
| właściwości. LastScaleActionTime | Sygnatura czasowa wystąpienia akcji skalowania automatycznego. |
| status |Ciąg opisujący stan operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan | Zazwyczaj o wartości null dla automatycznego skalowania. |
| eventTimestamp |Sygnatura czasowa po zdarzeniu został wygenerowany przez usługę Azure przetwarzania żądania odpowiednie zdarzenie. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

## <a name="security"></a>Bezpieczeństwo
Ta kategoria zawiera rekord wszystkie alerty wygenerowane przez Centrum zabezpieczeń Azure. Przykładem typu zdarzenia, które widać w tej kategorii jest "podejrzane podwójne rozszerzenie pliku wykonywane".

### <a name="sample-event"></a>Zdarzenie próbkowania
```json
{
    "channels": "Operation",
    "correlationId": "965d6c6a-a790-4a7e-8e9a-41771b3fbc38",
    "description": "Suspicious double extension file executed. Machine logs indicate an execution of a process with a suspicious double extension.\r\nThis extension may trick users into thinking files are safe to be opened and might indicate the presence of malware on the system.",
    "eventDataId": "965d6c6a-a790-4a7e-8e9a-41771b3fbc38",
    "eventName": {
        "value": "Suspicious double extension file executed",
        "localizedValue": "Suspicious double extension file executed"
    },
    "category": {
        "value": "Security",
        "localizedValue": "Security"
    },
    "eventTimestamp": "2017-10-18T06:02:18.6179339Z",
    "id": "/subscriptions/d4742bb8-c279-4903-9653-9858b17d0c2e/providers/Microsoft.Security/locations/centralus/alerts/965d6c6a-a790-4a7e-8e9a-41771b3fbc38/events/965d6c6a-a790-4a7e-8e9a-41771b3fbc38/ticks/636439033386179339",
    "level": "Informational",
    "operationId": "965d6c6a-a790-4a7e-8e9a-41771b3fbc38",
    "operationName": {
        "value": "Microsoft.Security/locations/alerts/activate/action",
        "localizedValue": "Microsoft.Security/locations/alerts/activate/action"
    },
    "resourceGroupName": "myResourceGroup",
    "resourceProviderName": {
        "value": "Microsoft.Security",
        "localizedValue": "Microsoft.Security"
    },
    "resourceType": {
        "value": "Microsoft.Security/locations/alerts",
        "localizedValue": "Microsoft.Security/locations/alerts"
    },
    "resourceId": "/subscriptions/d4742bb8-c279-4903-9653-9858b17d0c2e/providers/Microsoft.Security/locations/centralus/alerts/2518939942613820660_a48f8653-3fc6-4166-9f19-914f030a13d3",
    "status": {
        "value": "Active",
        "localizedValue": "Active"
    },
    "subStatus": {
        "value": null
    },
    "submissionTimestamp": "2017-10-18T06:02:52.2176969Z",
    "subscriptionId": "d4742bb8-c279-4903-9653-9858b17d0c2e",
    "properties": {
        "accountLogonId": "0x2r4",
        "commandLine": "c:\\mydirectory\\doubleetension.pdf.exe",
        "domainName": "hpc",
        "parentProcess": "unknown",
        "parentProcess id": "0",
        "processId": "6988",
        "processName": "c:\\mydirectory\\doubleetension.pdf.exe",
        "userName": "myUser",
        "UserSID": "S-3-2-12",
        "ActionTaken": "Detected",
        "Severity": "High"
    },
    "relatedEvents": []
}

```

### <a name="property-descriptions"></a>Opisy właściwości
| Nazwa elementu | Opis |
| --- | --- |
| Kanały | Zawsze "operacji" |
| correlationId | Identyfikator GUID w postaci ciągu. |
| description |Statyczny tekst opisu zdarzenia zabezpieczeń. |
| eventDataId |Unikatowy identyfikator zdarzenia zabezpieczeń. |
| EventName |Przyjazna nazwa zdarzeń zabezpieczeń. |
| id |Identyfikator unikatowy zasób zdarzeń zabezpieczeń. |
| poziom |Poziom zdarzenia. Jedną z następujących wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" lub "Pełne" |
| Grupy zasobów o nazwie |Nazwa grupy zasobów dla zasobu. |
| resourceProviderName |Nazwa dostawcy zasobów Centrum zabezpieczeń Azure. Zawsze "Microsoft.Security". |
| Typ zasobu |Typ zasobu, który wygenerował zdarzenie zabezpieczeń, takich jak "Microsoft.Security/locations/alerts" |
| resourceId |Identyfikator zasobu alertu zabezpieczeń. |
| operationId |Identyfikator GUID współdzielenia zdarzenia, które odpowiadają jednej operacji. |
| operationName |Nazwa operacji. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły zdarzenia. Te właściwości będą się różnić w zależności od rodzaju alertu zabezpieczeń. Zobacz [tej strony](../security-center/security-center-alerts-type.md) opis typów alertów, które pochodzą z Centrum zabezpieczeń. |
| właściwości. Ważność |Poziom ważności. Możliwe wartości to "High", "Średni" lub "Low". |
| status |Ciąg opisujący stan operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan | Zazwyczaj o wartości null dla zdarzeń zabezpieczeń. |
| eventTimestamp |Sygnatura czasowa po zdarzeniu został wygenerowany przez usługę Azure przetwarzania żądania odpowiednie zdarzenie. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o dziennik aktywności (dawniej dzienników inspekcji)](monitoring-overview-activity-logs.md)
* [Strumień dziennika aktywności platformy Azure do usługi Event Hubs](monitoring-stream-activity-logs-event-hubs.md)
