---
title: "elementów webhook aaaConfigure Azure alerty metryki | Dokumentacja firmy Microsoft"
description: "Przekieruj systemów innych niż Azure tooother Azure alerty."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Konfigurowanie elementu webhook na alert metryki Azure
Elementów Webhook pozwalają tooroute Azure alertów systemów tooother powiadomień dla akcje przetwarzania końcowego lub niestandardowy. Możesz użyć elementu webhook w alertu tooroute on tooservices wysyłających programu SMS, dziennika błędów, powiadamiania zespołu za pomocą usług wiadomości rozmów/lub czy dowolna liczba innych działań. W tym artykule opisano sposób tooset elementu webhook alert metryki Azure i jakie ładunek powitania dla elementu webhook tooa HTTP POST hello wygląda następująco. Informacje dotyczące instalacji hello i schematu dla alertu dziennika aktywności platformy Azure (alert zdarzeń) [wyświetlona następująca strona](insights-auditlog-to-webhook-email.md).

Azure alerty zawartość HTTP POST hello alertu w formacie JSON schematu zdefiniowana poniżej elementu webhook tooa identyfikator URI, który należy podać podczas tworzenia alertu hello. Ten identyfikator URI musi być prawidłowy punkt końcowy HTTP lub HTTPS. Azure wpisów jednego wpisu na żądanie, gdy alert jest aktywny.

## <a name="configuring-webhooks-via-hello-portal"></a>Konfigurowanie elementów webhook za pośrednictwem portalu hello
Można dodać lub zaktualizować elementu webhook hello identyfikatora URI na ekranie alerty Create/Update hello w hello [portal](https://portal.azure.com/).

![Dodaj regułę alertu](./media/insights-webhooks-alerts/Alertwebhook.png)

Można również skonfigurować element webhook tooa toopost alertu identyfikator URI przy użyciu hello [polecenia cmdlet programu PowerShell usługi Azure](insights-powershell-samples.md#create-metric-alerts), [interfejsu wiersza polecenia i Platform](insights-cli-samples.md#work-with-alerts), lub [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Uwierzytelnianie hello elementu webhook
Element webhook Hello uwierzytelniania z użyciem autoryzacji opartej na tokenach. Witaj zapisać elementu webhook identyfikatora URI jest identyfikatorem tokenu, np. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Schemat ładunku
Witaj operację POST zawiera hello ładunek JSON i schematu dla wszystkich metryki na podstawie alertów.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Pole | Obowiązkowy | Ustalony zbiór wartości | Uwagi |
|:--- |:--- |:--- |:--- |
| status |Tak |"Aktywna", "Rozwiązane" |Stan alertu hello na podstawie warunków hello się, że zostało ustawione. |
| Kontekst |Tak | |Witaj kontekst alertu. |
| sygnatura czasowa |Tak | |czas Hello, w których hello alert został uruchomiony. |
| id |Tak | |Każda reguła alertów ma unikatowy identyfikator. |
| name |Tak | |Nazwa alertu Hello. |
| description |Tak | |Opis alertu hello. |
| conditionType |Tak |"Metryki", "Event" |Obsługiwane są dwa typy alertów. Jeden na podstawie warunku metryki i hello inne na podstawie zdarzenia w hello dziennik aktywności. Użyj toocheck tej wartości, jeśli hello alert jest oparty na Metryka lub zdarzeń. |
| Warunek |Tak | |Witaj toocheck określonych pól dla oparte na powitania conditionType. |
| metricName |Metryki alertów | |monitoruje Hello Nazwa metryki hello, który definiuje, jakie reguły hello. |
| metricUnit |Metryki alertów |"B", "BytesPerSecond", "Count", "CountPerSecond", "%", "S" |Jednostka Hello dozwolone w hello metryki. [Dozwolone wartości są wyświetlane tutaj](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |Metryki alertów | |Wartość rzeczywista Hello metryki hello, który spowodował hello alert. |
| Próg |Metryki alertów | |wartość progowa Hello przy których hello jest uaktywniany alertu. |
| Rozmiar_okna |Metryki alertów | |Hello okres czasu, przez który toomonitor używane działanie alertów oparte na powitania próg. Musi należeć do zakresu od 5 minut do 1 dnia. Format czasu trwania ISO 8601. |
| timeAggregation |Metryki alertów |"Średnia", "Last", "Maksimum", "Minimalna", "None", "całkowita" |Jak można łączyć hello dane zbierane wraz z upływem czasu. Witaj domyślna wartość to średnia. [Dozwolone wartości są wyświetlane tutaj](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| Operator |Metryki alertów | |Hello operator używany toocompare hello bieżące dane toohello ustalonego progu. |
| subscriptionId |Tak | |Identyfikator subskrypcji platformy Azure. |
| Grupy zasobów o nazwie |Tak | |Nazwa grupy zasobów hello hello wpływ na zasobów. |
| resourceName |Tak | |Nazwa zasobu hello wpływ na zasobów. |
| Typ zasobu |Tak | |Typ zasobu hello wpływ na zasobów. |
| resourceId |Tak | |Identyfikator zasobu hello wpływ na zasobów. |
| resourceRegion |Tak | |Obszar lub lokalizacja hello wpływ na zasobów. |
| portalLink |Tak | |Toohello bezpośredniego łącza portalu zasobu strony podsumowania. |
| properties |N |Optional (Opcjonalność) |Zestaw `<Key, Value>` par (tj. `Dictionary<String, String>`) zawierającą szczegóły dotyczące zdarzenia hello. pole właściwości Hello jest opcjonalne. W przypadku niestandardowego interfejsu użytkownika lub logiki aplikacji na podstawie użytkownicy mogą wprowadzać klucza/wartości, które mogą zostać przekazane za pośrednictwem hello ładunku. Hello alternatywny sposób toopass właściwości niestandardowe wstecz toohello webhook odbywa się za pośrednictwem hello identyfikator uri elementu webhook sam (jako parametry kwerendy) |

> [!NOTE]
> pole właściwości Hello można ustawić tylko za pomocą hello [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o alertach Azure i elementów webhook wideo hello [integracji Azure alerty PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Wykonywanie skryptów automatyzacji Azure (elementów Runbook) Azure alertów](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Użyj aplikacji logiki toosend programu SMS za pośrednictwem usługi Twilio z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Użyj aplikacji logiki toosend Slack komunikat z Azure alertu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Użyj aplikacji logiki toosend tooan komunikatów kolejek platformy Azure z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
