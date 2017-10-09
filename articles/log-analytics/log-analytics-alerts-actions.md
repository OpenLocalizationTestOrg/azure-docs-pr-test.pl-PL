---
title: tooalerts aaaResponses w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Alerty w analizy dzienników zidentyfikować ważne informacje zawarte w repozytorium OMS i aktywne powiadamia użytkownika o problemy lub wywołanie akcji tooattempt toocorrect je.  W tym artykule opisano, jak toocreate regułę alertu i szczegóły hello różne akcje mogą przyjmować."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Dodaj reguły tooalert akcje w analizy dzienników
Gdy [alert jest tworzony w analizy dzienników](log-analytics-alerts.md), dostępna opcja hello [konfigurowania reguły alertu hello](log-analytics-alerts.md) tooperform co najmniej jednej akcji.  W tym artykule opisano hello różne akcje, które są dostępne i szczegółowe informacje na temat konfigurowania każdego rodzaju.

| Akcja | Opis |
|:--|:--|
| [Adres e-mail](#email-actions) | Wyślij wiadomość e-mail ze szczegółami hello hello tooone alertu lub więcej adresatów. |
| [Element Webhook](#webhook-actions) | Wywołaj procesu zewnętrznego przez pojedyncze żądanie HTTP POST. |
| [Element Runbook](#runbook-actions) | Uruchom element runbook automatyzacji Azure. |


## <a name="email-actions"></a>Akcje poczty e-mail
Akcje e-mail Wyślij wiadomość e-mail ze szczegółami hello hello tooone alertu lub więcej adresatów.  Można określić podmiotu hello hello poczty, ale jego zawartość jest standardowym formacie tworzony przez analizy dzienników.  Zawiera informacje podsumowania, takie jak nazwa hello alertu hello toodetails dodanie z tooten rekordów zwróconych hello dziennik wyszukiwania.  Zawiera również link tooa dziennik wyszukiwania w analizy dzienników, która zwróci hello cały zestaw rekordów z tej kwerendy.   nadawca Hello poczty hello jest *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* . 

Akcje poczty e-mail wymaga właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Temat |Podmiotu w hello wiadomości e-mail.  Nie można zmodyfikować hello treści wiadomości powitania. |
| Adresaci |Adresy wszystkich adresatów wiadomości e-mail.  Jeśli określono więcej niż jeden adres, a następnie hello oddzielne adresy średnikiem (;). |


## <a name="webhook-actions"></a>Akcje elementu Webhook

Akcje elementu Webhook pozwalają tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP POST.  Usługa Hello wywoływana powinien obsługuje elementów webhook i określić, jak używać żadnych ładunku odbiera.  Można także wywołać interfejs API REST w szczególności nie obsługuje elementów webhook, jak długo Żądanie hello jest w formacie tego powitalne rozumie interfejsu API.  Przykłady użycia elementu webhook w odpowiedzi tooan alert wysyłania wiadomości [Slack](http://slack.com) lub Tworzenie zdarzenia w [PagerDuty](http://pagerduty.com/).  Pełny Przewodnik tworzenia reguły alertu z elementu webhook toocall zapas czasu jest dostępna na [elementów Webhook w alertach analizy dzienników](log-analytics-alerts-webhooks.md).

Akcje elementu Webhook wymagają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Adres URL elementu Webhook |adres URL Hello hello elementu webhook. |
| Niestandardowy ładunek JSON |Niestandardowy ładunek toosend z hello elementu webhook.  Aby uzyskać więcej informacji, zobacz poniżej. |


Elementów Webhook zawierały adres URL i zapisany w formacie JSON, ilości danych hello ładunku wysyłane toohello zewnętrznej usługi.  Domyślnie ładunku hello będzie zawierać wartości hello w hello w poniższej tabeli.  Możesz wybrać tooreplace tego ładunku z niestandardowych jeden własny.  W takim przypadku można używać hello zmiennych w tabeli powitania dla każdego tooinclude parametry hello ich wartości w niestandardowy ładunek.

| Parametr | Zmienna | Opis |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Nazwa reguły alertów hello. |
| AlertThresholdOperator |#thresholdoperator |Operator próg hello reguły alertów.  *Większa niż* lub *mniej niż*. |
| AlertThresholdValue |#thresholdvalue |Wartość progowa hello reguły alertów. |
| LinkToSearchResults |#linktosearchresults |Łącze tooLog analizy dziennika wyszukiwania, które zwraca hello rekordów w kwerendzie hello utworzony hello alert. |
| ResultCount |#searchresultcount |Liczba rekordów w wynikach wyszukiwania hello. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Godzina zakończenia hello zapytania w formacie UTC. |
| SearchIntervalInSeconds |#searchinterval |Przedział czasu dla hello reguły alertów. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Godzina rozpoczęcia dla zapytania hello w formacie UTC. |
| SearchQuery |#searchquery |Używane przez reguły alertu hello zapytania wyszukiwania dziennika. |
| Wynikówwyszukiwania |Zobacz poniżej |Rekordów zwróconych przez zapytanie hello w formacie JSON.  Ograniczone toohello najpierw 5000 rekordów. |
| WorkspaceID |#workspaceid |Identyfikator obszaru roboczego OMS. |

Na przykład można określić następujące niestandardowy ładunek, który zawiera jeden parametr o nazwie hello *tekstu*.  Usługa Hello, który odwołuje się ten element webhook czy oczekiwano tego parametru.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Ten przykładowy ładunek rozwiąże toosomething jak powitania po kiedy wysłanych toohello elementu webhook.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

wyniki wyszukiwania tooinclude w ładunku niestandardowego, Dodaj powitania po wierszu jako właściwość najwyższego poziomu w ładunku json hello.  

    "IncludeSearchResults":true

Na przykład toocreate niestandardowy ładunek, zawierający tylko nazwę alertu hello i hello wyniki wyszukiwania można powitania po. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Można przeprowadzić za pomocą pełny przykład tworzenie reguły alertu z toostart elementu webhook zewnętrznej usługi na [utworzenie alertu elementu webhook w tooSlack komunikat toosend analizy dzienników OMS](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Działania elementu Runbook
Działania elementu Runbook uruchamiania elementu runbook automatyzacji Azure.  W celu toouse tego typu akcji, musisz mieć hello [rozwiązania automatyzacja](log-analytics-add-solutions.md) zainstalowany i skonfigurowany w obszarze roboczym pakietu OMS.  Możesz wybrać elementów runbook hello na koncie automatyzacji hello, skonfigurowanego w hello rozwiązanie Automatyzacja.

Działania elementu Runbook wymagają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:---|
| Element Runbook | Element Runbook ma toostart, podczas tworzenia alertu. |
| Uruchom na | Określ **Azure** toorun runbook hello w chmurze hello.  Określ **hybrydowy proces roboczy** toorun runbook hello na agenta o [hybrydowy proces roboczy elementu Runbook](../automation/automation-hybrid-runbook-worker.md ) zainstalowane.  |

Działania elementu Runbook start hello runbook za pomocą [webhook](../automation/automation-webhooks.md).  Podczas tworzenia reguły alertu hello automatycznie zostanie utworzony nowy element webhook dla elementu runbook hello o nazwie hello **OMS Alert korygowania** następuje identyfikator GUID.  

Nie można bezpośrednio wypełnić żadnych parametrów elementu hello runbook ale hello [parametru $WebhookData](../automation/automation-webhooks.md) będzie zawierał hello szczegółów alertu hello, w tym hello wyniki wyszukiwania hello dziennika, który go utworzył.  Witaj runbook należy toodefine **$WebhookData** jako parametru dla niego tooaccess hello właściwości hello alertu.  Witaj dane alertów jest dostępny w formacie json w jedną właściwość o nazwie **wynikówwyszukiwania** w hello **RequestBody** właściwość **$WebhookData**.  Będzie to mieć z właściwościami hello w hello w poniższej tabeli.

| Węzeł | Opis |
|:--- |:--- |
| id |Ścieżka i identyfikator GUID hello wyszukiwania. |
| __metadata |Informacje o hello alertu łącznie hello liczba rekordów i stanie hello wyników wyszukiwania. |
| wartość |Oddzielny wpis dla każdego rekordu w wynikach wyszukiwania hello.  Szczegóły Hello hello wpis będzie zgodny hello właściwości i wartości rekordu hello. |

Na przykład hello następujący element runbook będzie wyodrębnienie hello rekordów zwróconych przez hello dziennik wyszukiwania i przypisać różne właściwości na podstawie typu hello każdego rekordu.  Należy zwrócić uwagę hello elementu runbook rozpoczyna się od konwertowanie **RequestBody** z formatu json, którego nie można pracować z jako obiekt w programie PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Następne kroki
- Zakończenie wskazówki dla [Konfigurowanie webook](log-analytics-alerts-webhooks.md) z reguły alertu.  
- Dowiedz się, jak toowrite [elementy runbook automatyzacji Azure](https://azure.microsoft.com/documentation/services/automation) problemów tooremediate identyfikowana na podstawie alertów.
