---
title: "aaaAzure schemat zdarzenia dziennika aktywności | Dokumentacja firmy Microsoft"
description: "Zrozumienie schematu zdarzeń hello danych do hello dziennik aktywności"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Schematu zdarzeń dziennika aktywności platformy Azure
Witaj **dziennika aktywności platformy Azure** jest dziennika, który zapewnia wgląd w wszelkie zdarzenia poziomu subskrypcji, które wystąpiły na platformie Azure. W tym artykule opisano schematu zdarzeń hello na kategorię danych.

## <a name="administrative"></a>Administracyjne
Ta kategoria zawiera rekord hello wszystkich utworzyć, update, delete i akcji operacje wykonywane za pomocą Menedżera zasobów. Przykłady powitalne typy zdarzeń, które można zobaczyć w tej kategorii "Utwórz maszynę wirtualną" i "usunąć grupy zabezpieczeń sieci" każdej akcji podjętej przez użytkownika lub aplikacji przy użyciu usługi Resource Manager ma formę operację określonego typu zasobu. Jeśli typ operacji hello jest zapisu, usuwania lub działania, rekordy hello hello start i powodzenie lub niepowodzenie tej operacji są rejestrowane w hello kategorii administracyjnej. Kategoria administracyjna Hello także żadnych kontroli dostępu na podstawie toorole zmian w subskrypcji.

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
| Autoryzacji |Obiekt typu blob właściwości RBAC hello zdarzenia. Obejmuje zazwyczaj hello właściwości "Akcja", "rola" i "zakresu". |
| obiekt wywołujący |Adres e-mail użytkownika hello, który wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności. |
| Kanały |Jeden z hello następujące wartości: "Administrator", "Operacji" |
| Oświadczenia |Hello JWT token używane przez usługi Active Directory tooauthenticate hello użytkownik lub aplikacja tooperform tej operacji w Menedżera zasobów. |
| correlationId |Zazwyczaj identyfikator GUID w formacie ciągu hello. Zdarzenia, które mają correlationId należą toohello tę samą akcję pełny. |
| description |Statyczny tekst opisu zdarzenia. |
| eventDataId |Unikatowy identyfikator zdarzenia. |
| httpRequest |Obiekt blob opisujący hello żądania Http. Obejmuje zazwyczaj hello "clientRequestId", "clientIpAddress" i "method" (metoda HTTP. For example, PUT). |
| poziom |Poziom hello zdarzeń. Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| Grupy zasobów o nazwie |Nazwa grupy zasobów hello hello wpływ na zasobów. |
| resourceProviderName |Nazwa dostawcy zasobów hello hello wpływ na zasób |
| resourceId |Identyfikator zasobu hello wpływ na zasobów. |
| operationId |Identyfikator GUID współdzielenia hello zdarzenia, które odpowiadają tooa jednej operacji. |
| operationName |Nazwa operacji hello. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły hello hello zdarzenia. |
| status |Ciąg opisujący stan hello hello operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan |Zazwyczaj hello kod stanu HTTP hello odpowiadającego wywołania REST, ale można również uwzględnić inne parametry opisujące podstanu, takich jak te wartości typowych: OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (HTTP Kod stanu: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503), limit czasu bramy (kod stanu HTTP: 504). |
| eventTimestamp |Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

## <a name="service-health"></a>Kondycja usługi
Ta kategoria zawiera rekord hello określone zdarzenia kondycji usługi, które wystąpiły na platformie Azure. Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "Azure SQL w wschodnie stany USA występuje Przestój." Zdarzenia kondycji usługi są dostępne w pięciu odmian: wymagana akcja, wspierana odzyskiwania, zdarzenie, konserwacji, informacje lub zabezpieczeń i są wyświetlane tylko, jeśli zasób hello subskrypcji, która może wpływać na powitania zdarzeń.

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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Opisy właściwości
Nazwa elementu | Opis
-------- | -----------
Kanały | Jest jednym z hello następujące wartości: "Administrator", "Operacji"
correlationId | Jest zazwyczaj identyfikator GUID w formacie ciągu hello. Zdarzenia z tym należy toohello zwykle udostępnić tę samą akcję pełny hello correlationId tego samego.
description | Opis zdarzenia hello.
eventDataId | Witaj Unikatowy identyfikator zdarzenia.
EventName | Tytuł Hello hello zdarzeń.
poziom | Poziom hello zdarzeń. Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"
resourceProviderName | Nazwa dostawcy zasobów hello hello wpływ na zasobów. Jeśli nie jest znany, będzie to wartość null.
Typ zasobu| Typ zasobu hello Hello wpływ na zasobów. Jeśli nie jest znany, będzie to wartość null.
Podstan | Zazwyczaj o wartości null dla zdarzenia kondycji usługi.
eventTimestamp | Znacznik czasu w momencie hello dziennik zdarzeń został wygenerowany i przesłać toohello dziennik aktywności.
submissionTimestamp |   Znacznik czasu w momencie zdarzenia hello stały się dostępne w hello dziennik aktywności.
subscriptionId | Witaj w trakcie którego zarejestrowano to zdarzenie subskrypcji platformy Azure.
status | Ciąg opisujący stan hello hello operacji. Niektóre typowe wartości to: aktywne, rozwiązane.
operationName | Nazwa operacji hello. Zazwyczaj Microsoft.ServiceHealth/incident/action.
category | "ServiceHealth"
resourceId | Identyfikator zasobu hello wpływ na zasobu, jeśli znane. W przeciwnym razie podany identyfikator subskrypcji.
Properties.Title | Tytuł Hello zlokalizowane dla tej komunikacji. Język domyślny hello jest angielski.
Properties.Communication | Szczegóły Hello zlokalizowane hello komunikacji z kodu znaczników HTML. Domyślne hello jest angielski.
Properties.incidentType | Możliwe wartości: AssistedRecovery, ActionRequired, informacje, zdarzenie, obsługi, zabezpieczeń
Properties.trackingId | Identyfikuje hello incydent, który jest skojarzony to zdarzenie. Użyj tego zdarzenia pokrewne tooan toocorrelate hello zdarzenia.
Properties.impactedServices | Zmienionym obiektu blob JSON opisującą hello usług i regionów, które mają wpływ zdarzenia hello. Lista usług, z których każda ma elementy ServiceName i listę ImpactedRegions, z których każda ma RegionName.
Properties.defaultLanguageTitle | Komunikacja Hello w języku angielskim
Properties.defaultLanguageContent | Komunikacja Hello w języku angielskim jako kod znaczników html i zwykły tekst
Properties.Stage | Możliwe wartości AssistedRecovery, ActionRequired, informacje, zdarzenie, zabezpieczeń: są aktywne, rozwiązane. W konserwacji są: aktywny, planowane, w toku, anulowane, Rescheduled, rozwiązane, Zakończ
Properties.communicationId | Komunikacja Hello to zdarzenie jest skojarzony.

## <a name="alert"></a>Alerty
Ta kategoria zawiera rekord hello aktywacji wszystkich alertów platformy Azure. Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "procent użycia procesora CPU na myVM została ponad 80 dla hello ostatnich 5 minut." Z różnymi systemami Azure ma alertów koncepcji — można zdefiniować regułę jakiegoś i otrzymasz powiadomienie, gdy warunki reguły są zgodne. Zawsze Azure obsługiwanego typu alertu "aktywuje," lub hello są warunki niespełnienia toogenerate powiadomienie, rekord aktywacji hello również spoczywa toothis kategorii hello dziennik aktywności.

### <a name="sample-event"></a>Zdarzenie próbkowania

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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
| Oświadczenia | Obiektu blob JSON hello głównej nazwy usługi (nazwy głównej usługi) lub zasób typu hello aparat alertów. |
| correlationId | Identyfikator GUID w formacie ciągu hello. |
| description |Opis tekst statyczny hello zdarzenia alertu. |
| eventDataId |Unikatowy identyfikator hello zdarzeń alertów. |
| poziom |Poziom hello zdarzeń. Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| Grupy zasobów o nazwie |Nazwę grupy zasobów hello hello wpływ na zasobu, jeśli jest to alert metryki. Inne typy alertów to hello nazwę grupy zasobów hello, która zawiera hello samego alertu. |
| resourceProviderName |Nazwa dostawcy zasobów hello hello wpływ na zasobu, jeśli jest to alert metryki. Inne typy alertów to hello nazwę dostawcy zasobów hello hello samego alertu. |
| resourceId | Nazwę identyfikatora zasobu hello hello wpływ na zasobu, jeśli jest to alert metryki. Inne typy alertów jest to identyfikator zasobu hello hello zasobu alertu sam. |
| operationId |Identyfikator GUID współdzielenia hello zdarzenia, które odpowiadają tooa jednej operacji. |
| operationName |Nazwa operacji hello. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły hello hello zdarzenia. |
| status |Ciąg opisujący stan hello hello operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan | Zazwyczaj o wartości null dla alertów. |
| eventTimestamp |Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

### <a name="properties-field-per-alert-type"></a>Pole właściwości typu alertu
pole właściwości Hello będzie zawierać różne wartości w zależności od źródła hello hello zdarzenia alertu. Dwóch dostawców typowych zdarzeń alertów są alerty dziennika aktywności i metryki alerty.

#### <a name="properties-for-activity-log-alerts"></a>Właściwości alertów dziennik aktywności
| Nazwa elementu | Opis |
| --- | --- |
| properties.subscriptionId | Identyfikator subskrypcji Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany. |
| properties.eventDataId | Identyfikator danych zdarzenia Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany. |
| properties.resourceGroup | Grupa zasobów Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany. |
| properties.resourceId | Identyfikator zasobu Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany. |
| properties.eventTimestamp | Witaj zdarzeń sygnatura czasowa hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany. |
| properties.operationName | Nazwa operacji Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany. |
| Properties.status | Stan Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.|

#### <a name="properties-for-metric-alerts"></a>Właściwości alertów metryki
| Nazwa elementu | Opis |
| --- | --- |
| właściwości. RuleUri | Identyfikator zasobu hello metryki reguły alertu samej siebie. |
| właściwości. RuleName | Nazwa Hello hello metryki reguły alertów. |
| właściwości. RuleDescription | Opis Hello hello metryki reguły alertu (zgodnie z definicją w regule alertu hello). |
| właściwości. Próg | wartość progowa Hello przy ocenie hello hello metryki reguły alertów. |
| właściwości. WindowSizeInMinutes | rozmiar okna Hello przy ocenie hello hello metryki reguły alertów. |
| właściwości. Agregacji | Typ agregacji Hello zdefiniowane w regule alertu metryki hello. |
| właściwości. Operator | operator warunkowy Hello przy ocenie hello hello metryki reguły alertów. |
| właściwości. MetricName | Nazwa metryki Hello metryki hello przy ocenie hello hello metryki reguły alertów. |
| właściwości. MetricUnit | Jednostka metryki Hello metryki hello przy ocenie hello hello metryki reguły alertów. |

## <a name="autoscale"></a>Automatyczne skalowanie
Ta kategoria zawiera rekord hello żadnych operacji toohello powiązane zdarzenia aparatu skalowania automatycznego hello oparte na ustawienia skalowania automatycznego zdefiniowanych w ramach subskrypcji. Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "Skalowania automatycznego skalowania w górę akcja nie powiodła się". Przy użyciu automatycznego skalowania, można automatycznie skalować w poziomie lub skalować w hello liczbę wystąpień w typie zasobów obsługiwanych na podstawie czasu dnia i/lub obciążenia () dane przy użyciu ustawienia skalowania automatycznego. Po spełnieniu warunków hello tooscale w górę i w dół hello start i zakończyło się pomyślnie lub niepowodzeniem zdarzenia będą rejestrowane w tej kategorii.

### <a name="sample-event"></a>Zdarzenie próbkowania
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
| Oświadczenia | Obiektu blob JSON z hello głównej nazwy usługi (nazwy głównej usługi) lub zasobu typu, hello skalowania automatycznego aparatu. |
| correlationId | Identyfikator GUID w formacie ciągu hello. |
| description |Opis tekst statyczny hello skalowania automatycznego zdarzenia. |
| eventDataId |Unikatowy identyfikator zdarzenia skalowania automatycznego hello. |
| poziom |Poziom hello zdarzeń. Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| Grupy zasobów o nazwie |Nazwa grupy zasobów hello hello ustawieniu skalowania automatycznego. |
| resourceProviderName |Nazwa dostawcy zasobów hello hello ustawieniu skalowania automatycznego. |
| resourceId |Identyfikator zasobu hello ustawieniu skalowania automatycznego. |
| operationId |Identyfikator GUID współdzielenia hello zdarzenia, które odpowiadają tooa jednej operacji. |
| operationName |Nazwa operacji hello. |
| properties |Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły hello hello zdarzenia. |
| właściwości. Opis elementu | Szczegółowy opis wykonywanych jakie hello skalowania automatycznego aparatu. |
| właściwości. ResourceName | Identyfikator zasobu hello wpływ na zasobów (hello zasobu, na które hello wykonywania akcji skalowania) |
| właściwości. OldInstancesCount | Hello liczbę wystąpień przed akcji skalowania automatycznego hello weszły w życie. |
| właściwości. NewInstancesCount | Witaj liczba wystąpień po akcji skalowania automatycznego hello weszły w życie. |
| właściwości. LastScaleActionTime | Witaj sygnatura czasowa wystąpienia hello akcji skalowania automatycznego. |
| status |Ciąg opisujący stan hello hello operacji. Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane. |
| Podstan | Zazwyczaj o wartości null dla automatycznego skalowania. |
| eventTimestamp |Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello. |
| submissionTimestamp |Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello dziennik aktywności (dawniej dzienników inspekcji)](monitoring-overview-activity-logs.md)
* [Strumienia tooEvent dziennika aktywności platformy Azure hello koncentratory](monitoring-stream-activity-logs-event-hubs.md)
