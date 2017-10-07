---
title: aaaUsing OMS dziennika analizy alertu interfejsu API REST
description: "Witaj interfejsu API REST alertu dziennika analizy pozwala toocreate alerty i zarządzaj nimi w analizy dzienników, która jest częścią z Operations Management Suite (OMS).  Ten artykuł zawiera szczegółowe informacje o hello interfejsu API i kilka przykładów do wykonywania różnych operacji."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Tworzenie i zarządzanie nimi reguły alertów w analizy dzienników z interfejsu API REST
Witaj interfejsu API REST alertu dziennika analizy pozwala toocreate alerty i zarządzaj nimi w Operations Management Suite (OMS).  Ten artykuł zawiera szczegółowe informacje o hello interfejsu API i kilka przykładów do wykonywania różnych operacji.

Witaj interfejsu API REST Search analizy dziennika jest RESTful i jest możliwy za pośrednictwem hello Azure Resource Manager REST API. W tym dokumencie można znaleźć przykłady gdzie hello interfejsu API jest dostępny z wiersza polecenia programu PowerShell przy użyciu [ARMClient](https://github.com/projectkudu/ARMClient), narzędzie wiersza polecenia typu open source, który upraszcza wywoływania hello interfejsu API usługi Azure Resource Manager. Użycie Hello ARMClient i programu PowerShell jest jedną z wielu opcji hello tooaccess interfejsu API Search analizy dziennika. Z tych narzędzi można wykorzystywać hello wywołania interfejsu API RESTful Menedżera zasobów Azure toomake obszarów roboczych o tooOMS i wykonywać polecenia wyszukiwania w nich. Witaj interfejsu API dane wyjściowe obejmują tooyou wyników wyszukiwania w formacie JSON, umożliwiając wyniki wyszukiwania hello toouse na wiele różnych sposobów programowo.

## <a name="prerequisites"></a>Wymagania wstępne
Obecnie usługa alertów można tworzyć tylko z zapisanej operacji wyszukiwania w analizy dzienników.  Może się odwoływać toohello [interfejsu API REST wyszukiwania dziennika](log-analytics-log-search-api.md) Aby uzyskać więcej informacji.

## <a name="schedules"></a>Harmonogramy
Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram. Hello harmonogram Określa, jak często hello wyszukiwania jest uruchamiany i interwał czasu hello za pośrednictwem których kryteria hello jest identyfikowany.
Harmonogramy mają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Interwał |Jak często hello wyszukiwania jest uruchamiany. (W minutach). |
| QueryTimeSpan |Interwał czasu Hello za pośrednictwem których hello oceny kryteriów. Musi być większy niż interwał równy tooor. (W minutach). |
| Wersja |Witaj używana wersja interfejsu API.  Obecnie ta powinna być zawsze ustawiony too1. |

Rozważmy na przykład kwerendy zdarzeń z interwałem 15 minut i zakres czasu 30 minut. W takim przypadku hello będzie uruchamiane zapytanie co 15 minut, a alert będzie uruchomiony, jeśli kryteria hello nadal tooresolve tootrue w danym okresie 30 minut.

### <a name="retrieving-schedules"></a>Trwa pobieranie harmonogramów
Użyj hello Pobierz tooretrieve — metoda wszystkie harmonogramy dla zapisanego kryterium wyszukiwania.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Użyj hello Get, metoda z tooretrieve identyfikator harmonogramu konkretny harmonogram dla zapisanego kryterium wyszukiwania.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Poniżej znajduje się przykładowa odpowiedź dla harmonogramu.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Tworzenie harmonogramu
Za pomocą metody Put hello harmonogram Unikatowy identyfikator toocreate nowy harmonogram.  Należy pamiętać, że dwa harmonogramy nie może mieć hello takim samym identyfikatorze nawet, jeśli są one powiązane z różnymi, zapisane wyszukiwania.  Po utworzeniu harmonogramu w konsoli OMS hello identyfikator GUID jest tworzony dla identyfikatora hello harmonogramu.

> [!NOTE]
> Nazwa Hello wszystkie zapisane wyszukiwania, harmonogramów i działania utworzone za pomocą hello API analizy dziennika musi być pisane małymi literami.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Edytowanie harmonogramu
Za pomocą metody Put hello identyfikator hello sam zapisane wyszukiwanie toomodify, który zaplanować istniejącego harmonogramu.  Hello treści żądania hello musi zawierać element etag hello hello harmonogramu.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Usuwanie harmonogramów
Za pomocą metody Delete hello toodelete identyfikator harmonogramu zgodnie z harmonogramem.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Akcje
Harmonogram może mieć wiele akcji. Akcja może zdefiniować co najmniej jeden tooperform procesy, takie jak wysyłanie wiadomości e-mail lub uruchamianie elementu runbook lub mogą określić próg, określająca, kiedy hello wyniki wyszukiwania kryteriom niektórych.  Niektóre akcje definiują zarówno tak, aby procesy hello są wykonywane po spełnieniu hello próg.

Wszystkie działania mają właściwości hello w hello w poniższej tabeli.  Różne typy alertów mają różne dodatkowe właściwości, które są opisane poniżej.

| Właściwość | Opis |
|:--- |:--- |
| Typ |Typ akcji hello.  Obecnie hello możliwe wartości to Alert i elementu Webhook. |
| Nazwa |Nazwa wyświetlana hello alertu. |
| Wersja |Witaj używana wersja interfejsu API.  Obecnie ta powinna być zawsze ustawiony too1. |

### <a name="retrieving-actions"></a>Pobieranie akcji
Użyj hello Pobierz tooretrieve — metoda wszystkie akcje dla harmonogramu.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Użyj hello Get, metoda z tooretrieve identyfikator akcji hello określonej akcji dla harmonogramu.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Tworzenie lub edytowanie akcji
Użyj metody Put hello o identyfikatorze akcji, który jest unikatowy toohello harmonogram toocreate nową akcję.  Po utworzeniu akcji w konsoli OMS hello identyfikator GUID jest identyfikatora hello akcji.

> [!NOTE]
> Nazwa Hello wszystkie zapisane wyszukiwania, harmonogramów i działania utworzone za pomocą hello API analizy dziennika musi być pisane małymi literami.

Użyj metody Put hello z akcją istniejący identyfikator hello sam zapisane wyszukiwanie toomodify, który harmonogramu.  Hello treści żądania hello musi zawierać element etag hello hello harmonogramu.

format żądania Hello do tworzenia nowych akcji zależy od typu akcji, te przykłady znajdują się w poniższych sekcjach hello.

### <a name="deleting-actions"></a>Usuwanie akcji
Za pomocą metody Delete hello toodelete identyfikator akcji hello akcji.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Akcje alertu
Harmonogram ma jeden i tylko jeden Alert akcji.  Akcje alertu występuje jeden lub kilka z sekcji hello hello w poniższej tabeli.  Każdy jest opisany bardziej szczegółowo poniżej.

| Sekcja | Opis |
|:--- |:--- |
| Próg |Po uruchomieniu akcji hello kryteria. |
| EmailNotification |Wysyłanie poczty toomultiple adresatów. |
| Korygowania |Uruchom element runbook w automatyzacji Azure tooattempt toocorrect zidentyfikować problem. |

#### <a name="thresholds"></a>Progi
Akcja alertu powinna mieć jeden i tylko jeden próg.  Jeśli wyniki hello zapisanego kryterium wyszukiwania zgodne próg hello w akcji skojarzonej z tym wyszukiwania, są uruchamiane żadnych innych procesów w tej akcji.  Akcja może również zawierać tylko wartości progowej, aby mogą być używane z akcjami innych typów, które nie zawierają wartości progowe.

Progi mają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Operator |Operator porównania próg hello. <br> gt = większe niż <br> lt = mniej niż |
| Wartość |Wartość progu hello. |

Rozważmy na przykład kwerendy interwał 15 minut, Timespan 30 minut, a próg większym niż 10. W takim przypadku hello będzie uruchamiane zapytanie co 15 minut, a alert będzie uruchomiony, jeśli zwróceniem 10 zdarzeń, które zostały utworzone w danym okresie 30 minut.

Poniżej znajduje się przykładowa odpowiedź dla akcji z tylko wartości progowej.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nową akcję próg dla harmonogramu.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Za pomocą metody Put hello istniejących toomodify identyfikator akcji akcji próg dla harmonogramu.  Witaj treści żądania hello musi zawierać etag hello hello akcji.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Powiadomienia e-mail
Powiadomienia e-mail wysyłanie poczty tooone lub więcej adresatów.  Obejmują one właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Adresaci |Lista adresów e-mail. |
| Temat |temat Hello hello poczty. |
| Załącznika |Załączniki nie są obecnie obsługiwane, dlatego to zawsze będzie mieć wartość "None". |

Poniżej znajduje się przykładowa odpowiedź dla akcji powiadomienia e-mail o progu.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nową akcję poczty e-mail dla harmonogramu.  Witaj poniższy przykład tworzy wiadomość e-mail z powiadomieniem o progu tak poczty hello jest wysyłany, gdy wyniki hello hello zapisanego wyszukiwania przekracza próg hello.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Za pomocą metody Put hello istniejących toomodify identyfikator akcji akcji poczty e-mail dla harmonogramu.  Witaj treści żądania hello musi zawierać etag hello hello akcji.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Akcji korygowania
Korygowaniami uruchomienia elementu runbook w automatyzacji Azure, która próbuje problem hello toocorrect identyfikowane przez hello alert.  Należy utworzyć elementu webhook dla elementu runbook hello używany w Akcja korygowania, a następnie określ hello identyfikatora URI w hello WebhookUri właściwości.  Podczas tworzenia tej akcji, używając konsoli OMS hello nowego elementu webhook jest tworzony automatycznie hello elementu runbook.

Korygowaniami dołączyć właściwości hello hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| RunbookName |Nazwa elementu hello runbook. To musi być zgodna opublikowanego elementu runbook na koncie automatyzacji hello skonfigurowane w hello rozwiązanie do automatyzacji w obszarze roboczym pakietu OMS. |
| WebhookUri |Identyfikator URI elementu webhook hello. |
| Wygaśnięcia |Witaj datę i godzinę wygaśnięcia elementu hello webhook.  Jeśli hello elementu webhook nie ma wygaśnięcia, może to być wszystkie prawidłową datą przyszłą. |

Poniżej znajduje się przykładowa odpowiedź dla akcji korygowania o progu.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nowa akcja korygowania harmonogramu.  Witaj poniższy przykład tworzy korygowania o progu tak hello elementu runbook została uruchomiona, wyniki hello hello zapisanego wyszukiwania przekracza próg hello.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Za pomocą metody Put hello istniejących toomodify identyfikator akcji Akcja korygowania harmonogramu.  Witaj treści żądania hello musi zawierać etag hello hello akcji.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Przykład
Poniżej znajduje się pełny przykład toocreate nowy alert e-mail.  Spowoduje to utworzenie nowego harmonogramu wraz z akcji zawierający próg i poczty e-mail.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Akcje elementu Webhook
Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając toobe ładunku, wysyłane.  Są one podobne akcje tooRemediation, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesów innych niż element runbook usługi Automatyzacja Azure.  Zapewniają także hello dodatkowa opcja udostępniania procesu zdalnego toohello toobe dostarczyć ładunku.

Akcje elementu Webhook nie ma wartości progowej, ale zamiast tego należy dodać tooa harmonogram, który ma akcję alertu o progu.  Można dodawać wiele akcji elementu Webhook, które zostaną wszystkie uruchomione po spełnieniu hello próg.

Akcje elementu Webhook dołączyć właściwości hello hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| WebhookUri |temat Hello hello poczty. |
| CustomPayload |Niestandardowy ładunek toobe wysyłane toohello elementu webhook.  Hello format będzie zależeć od elementu webhook jakie hello jest oczekiwany. |

Poniżej znajduje się przykładowa odpowiedź dla elementu webhook akcji i skojarzonych alertach o progu.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Utwórz lub Edytuj akcji elementu webhook
Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nową akcję elementu webhook dla harmonogramu.  Witaj poniższy przykład tworzy akcji elementu Webhook i alertów o progu tak, aby wyniki hello hello zapisanego wyszukiwania przekracza próg hello zostanie wywołane hello elementu webhook.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Za pomocą metody Put hello istniejących toomodify identyfikator akcji akcji elementu webhook dla harmonogramu.  Witaj treści żądania hello musi zawierać etag hello hello akcji.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Następne kroki
* Użyj hello [interfejsu API REST tooperform dziennik wyszukiwania](log-analytics-log-search-api.md) w analizy dzienników.

