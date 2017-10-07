---
title: "aaaCall elementu webhook alerty dziennika aktywności platformy Azure | Dokumentacja firmy Microsoft"
description: "Trasy działania dziennika zdarzeń tooother usługi akcji niestandardowych. Na przykład wysyłanie SMS dziennika błędów lub powiadomić zespołu za pomocą rozmowy/wiadomości usługi."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Wywołanie elementu webhook alerty dziennika aktywności platformy Azure
Elementów Webhook pozwalają tooroute Azure alertów systemów tooother powiadomień dla akcje przetwarzania końcowego lub niestandardowy. Możesz użyć elementu webhook w alertu tooroute on tooservices wysyłających programu SMS, dziennika błędów, powiadamiania zespołu za pomocą usług wiadomości rozmów/lub czy dowolna liczba innych działań. W tym artykule opisano, jak tooset webhook toobe wywoływane, gdy generowane alertu dziennika aktywności platformy Azure. Przedstawia on także jakie ładunku hello hello HTTP POST tooa elementu webhook wygląda jak. Informacje dotyczące instalacji hello i schematu dla alertu metryki Azure [wyświetlona następująca strona](insights-webhooks-alerts.md). Można również skonfigurować wiadomości e-mail alertów toosend dziennik aktywności po uaktywnieniu.

> [!NOTE]
> Ta funkcja jest obecnie w wersji zapoznawczej i zostanie usunięta w pewnym momencie w przyszłości hello.
>
>

Można skonfigurować przy użyciu hello alertu dziennik aktywności [poleceń cmdlet programu PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [interfejsu wiersza polecenia i Platform](insights-cli-samples.md#work-with-alerts), lub [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn933805.aspx). Obecnie nie można ustawić jedną przy użyciu hello portalu Azure.

## <a name="authenticating-hello-webhook"></a>Uwierzytelnianie hello elementu webhook
Element webhook Hello uwierzytelniania z użyciem jednej z tych metod:

1. **Autoryzacji opartej na tokenach** — Witaj identyfikatora URI jest na przykład zapisane przy użyciu Identyfikatora token elementu webhook`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Podstawowe autoryzacji** — Witaj identyfikatora URI jest zapisane przy użyciu nazwy użytkownika i hasła, na przykład elementu webhook`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Schemat ładunku
Witaj operację POST zawiera hello ładunek JSON i schematu dla wszystkich dziennik aktywności na podstawie alertów. Ten schemat jest podobne toohello co najmniej jedna używana przez alerty na podstawie metryki.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Nazwa elementu | Opis |
| --- | --- |
| status |Używany w przypadku alertów metryki. Zawsze ustawiona zbyt "aktywowanego" alertów dziennik aktywności. |
| Kontekst |Kontekst hello zdarzeń. |
| resourceProviderName |Dostawca zasobów Hello hello wpływ na zasobów. |
| conditionType |Zawsze "Event". |
| name |Nazwa reguły alertów hello. |
| id |Identyfikator zasobu hello alertu. |
| description |Opis alertu jako zestaw podczas tworzenia alertu hello. |
| subscriptionId |Identyfikator subskrypcji platformy Azure. |
| sygnatura czasowa |Czas, w którym hello zdarzeń został wygenerowany przez hello usługa Azure, która hello żądanie. |
| resourceId |Identyfikator zasobu hello wpływ na zasobów. |
| Grupy zasobów o nazwie |Nazwa grupy zasobów hello hello wpływ na zasób |
| properties |Zestaw `<Key, Value>` par (tj. `Dictionary<String, String>`) zawierającą szczegóły dotyczące zdarzenia hello. |
| Zdarzenia |Element zawierający metadane dotyczące zdarzenia hello. |
| Autoryzacji |właściwości RBAC Hello hello zdarzenia. Obejmują one zazwyczaj hello "Akcja" i "rola" hello "zakresu." |
| category |Kategoria zdarzenia hello. Obsługiwane wartości to: administracyjne, alertów zabezpieczeń, ServiceHealth, zalecenie. |
| obiekt wywołujący |Adres e-mail użytkownika hello, który wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności. Może mieć wartości null dla niektórych wywołań systemowych. |
| correlationId |Zazwyczaj identyfikator GUID w postaci ciągu. Zdarzenia z correlationId należą toohello tę samą akcję większych i zwykle udostępnianie correlationId. |
| eventDescription |Opis zdarzenia hello tekst statyczny. |
| eventDataId |Unikatowy identyfikator dla hello zdarzenia. |
| Źródła zdarzeń |Nazwa hello infrastruktury i usługa Azure hello wygenerowane zdarzenie. |
| httpRequest |Obejmuje zazwyczaj hello "clientRequestId", "clientIpAddress" i "method" (np. umieścić metoda HTTP). |
| poziom |Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne." |
| operationId |Zazwyczaj identyfikator GUID współdzielenia zdarzenia hello odpowiadającego toosingle operacji. |
| operationName |Nazwa operacji hello. |
| properties |Właściwości zdarzenia hello. |
| status |Ciąg. Stan operacji hello. Typowe wartości to: "Uruchomiona", "W toku", "Powiodło się", "Nie powiodło się", "Active", "Rozwiązany". |
| Podstan |Zwykle zawiera kod stanu HTTP hello hello odpowiedniego wywołania REST. Może również zawierać inne parametry opisujące podstanu. Obejmują wartości typowych podstanu: OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (kod stanu HTTP: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503), limit czasu bramy (kod stanu HTTP: 504) |

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello dziennik aktywności](monitoring-overview-activity-logs.md)
* [Wykonywanie skryptów automatyzacji Azure (elementów Runbook) Azure alertów](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Użyj aplikacji logiki toosend programu SMS za pośrednictwem usługi Twilio z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennik aktywności.
* [Użyj aplikacji logiki toosend Slack wiadomości z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennik aktywności.
* [Użyj aplikacji logiki toosend tooan komunikatów kolejek platformy Azure z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennik aktywności.
