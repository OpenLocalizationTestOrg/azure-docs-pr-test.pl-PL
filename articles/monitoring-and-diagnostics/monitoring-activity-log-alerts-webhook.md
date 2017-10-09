---
title: "Schemat elementu webhook hello aaaUnderstand używane w alertach dziennika aktywności | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat schematu hello hello JSON publikowanego adresu URL elementu webhook tooa gdy aktywuje alert dziennika aktywności."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Elementów Webhook alertów dziennik aktywności platformy Azure
W ramach definicji hello grupę można skonfigurować elementu webhook punkty końcowe tooreceive działania dziennik powiadomień o alertach. Z elementów webhook można kierować te systemy tooother powiadomienia dla akcje przetwarzania końcowego lub niestandardowych. W tym artykule opisano, jakie ładunku hello hello HTTP POST tooa elementu webhook wygląda jak.

Aby uzyskać więcej informacji dotyczących alertów dziennika aktywności, zobacz jak zbyt[tworzyć działanie Azure alerty dziennika](monitoring-activity-log-alerts.md).

Informacji dotyczących grup akcji, zobacz temat jak zbyt[tworzenie grup akcji](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Uwierzytelnianie hello elementu webhook
Element webhook Hello można używać autoryzacji na podstawie tokenu uwierzytelniania. Witaj webhook identyfikatora URI jest zapisane przy użyciu Identyfikatora tokenu, na przykład `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Schemat ładunku
ładunek JSON Hello zawarte w hello operację POST różni się na podstawie w polu data.context.activityLog.eventSource hello ładunku.

###<a name="common"></a>Wspólne
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Administracyjne
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Szczegółowe schematu usługi kondycji powiadomień działania dziennika alertów, patrz [usługi powiadomień o kondycji](monitoring-service-notifications.md).

Dla określonego schematu informacji na temat wszystkich innych alertów dziennika aktywności, zobacz [omówienie dziennik aktywności platformy Azure hello](monitoring-overview-activity-logs.md).

| Nazwa elementu | Opis |
| --- | --- |
| status |Używany w przypadku alertów metryki. Zawsze ustawiona zbyt "aktywowanego" dla alertów dotyczących działań w dzienniku. |
| Kontekst |Kontekst hello zdarzeń. |
| resourceProviderName |Dostawca zasobów Hello hello wpływ na zasobów. |
| conditionType |Zawsze "Event". |
| name |Nazwa reguły alertów hello. |
| id |Identyfikator zasobu hello alertu. |
| description |Opis alertu ustawić po utworzeniu hello alertu. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |
| sygnatura czasowa |Czas, w którym hello zdarzeń został wygenerowany przez hello usługa Azure, która hello żądanie. |
| resourceId |Identyfikator zasobu hello wpływ na zasobów. |
| Grupy zasobów o nazwie |Nazwa grupy zasobów hello hello wpływ na zasobów. |
| properties |Zestaw `<Key, Value>` par (czyli `Dictionary<String, String>`) zawierającą szczegóły dotyczące zdarzenia hello. |
| Zdarzenia |Element zawierający metadane dotyczące zdarzenia hello. |
| Autoryzacji |właściwości kontroli dostępu opartej na rolach Hello hello zdarzenia. Te właściwości obejmują zazwyczaj hello akcji, hello roli i hello zakresu. |
| category |Kategoria zdarzenia hello. Obsługiwane wartości to administracyjne, Alert zabezpieczeń, ServiceHealth i zalecenia. |
| obiekt wywołujący |Adres e-mail użytkownika hello, który wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności. Może mieć wartości null dla niektórych wywołań systemowych. |
| correlationId |Zazwyczaj identyfikator GUID w postaci ciągu. Zdarzenia z correlationId należą toohello tę samą akcję większych i zwykle udostępnianie correlationId. |
| eventDescription |Opis zdarzenia hello tekst statyczny. |
| eventDataId |Unikatowy identyfikator dla hello zdarzenia. |
| Źródła zdarzeń |Nazwa hello infrastruktury i usługa Azure hello wygenerowane zdarzenie. |
| httpRequest |Witaj żądanie obejmuje zazwyczaj hello clientRequestId, clientIpAddress i metodę HTTP (na przykład umieścić). |
| poziom |Jeden z hello następujące wartości: krytyczny, błąd, ostrzeżenie, informacyjny i pełne. |
| operationId |Zazwyczaj identyfikator GUID współdzielenia zdarzenia hello odpowiadającego toosingle operacji. |
| operationName |Nazwa operacji hello. |
| properties |Właściwości zdarzenia hello. |
| status |Ciąg. Stan operacji hello. Typowe wartości to rozpoczęte, w toku, zakończyło się pomyślnie, nie powiodło się, aktywnych i rozwiązanych. |
| Podstan |Zwykle zawiera kod stanu HTTP hello hello odpowiedniego wywołania REST. Może również zawierać innych ciągów, które opisują podstanu. Typowe wartości podstanu obejmują OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (kod stanu HTTP: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503) i limit czasu bramy (kod stanu HTTP : 504). |

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o dziennik aktywności hello](monitoring-overview-activity-logs.md).
* [Wykonywanie skryptów automatyzacji Azure (elementów Runbook) Azure alerty](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Użyj toosend aplikacji logiki programu SMS za pośrednictwem usługi Twilio z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennika aktywności.
* [Użyj logiki aplikacji toosend Slack wiadomości z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennika aktywności.
* [Użyj toosend aplikacji logiki, kolejka wiadomości tooan Azure z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennika aktywności.
