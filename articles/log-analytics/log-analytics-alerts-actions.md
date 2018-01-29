---
title: Odpowiedzi na alerty w Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Alerty w analizy dzienników zidentyfikować ważne informacje w obszarze roboczym Azure i aktywne powiadamia użytkownika o problemy lub akcji, aby je poprawić.  W tym artykule opisano sposób tworzenia reguły alertu i szczegóły dla różnych działań podejmowanych przez nich."
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
ms.date: 01/08/2018
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e80481f074bc196caae7c03f54134eaef0fb46d5
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a>Dodawanie akcji do reguły alertów w analizy dzienników
Gdy [alert jest tworzony w analizy dzienników](log-analytics-alerts.md), masz możliwość [konfigurowanie reguły alertu](log-analytics-alerts.md) przeprowadzenie jedną lub więcej akcji.  W tym artykule opisano różne akcje, które są dostępne i szczegółowe informacje na temat konfigurowania każdego rodzaju.

| Akcja | Opis |
|:--|:--|
| [Wiadomość e-mail](#email-actions) | Wyślij wiadomość e-mail ze szczegółami alertu do co najmniej jednego adresata. |
| [Element Webhook](#webhook-actions) | Wywołaj procesu zewnętrznego przez pojedyncze żądanie HTTP POST. |
| [Element Runbook](#runbook-actions) | Uruchom element runbook automatyzacji Azure. |


## <a name="email-actions"></a>Akcje poczty e-mail
Akcje e-mail Wyślij wiadomość e-mail ze szczegółami alertu do co najmniej jednego adresata.  Można określić temat wiadomości e-mail, ale jego zawartość jest standardowym formacie tworzony przez analizy dzienników.  Zawiera informacje podsumowania, takie jak nazwa alertu oprócz szczegółów do dziesięciu rekordów zwróconych przez wyszukiwanie dziennika.  Zawiera również link do wyszukiwania dziennika w analizy dzienników, która zwróci cały zestaw rekordów z tej kwerendy.   Nadawcą wiadomości jest *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* . 

Akcje poczty e-mail wymaga właściwości w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Temat |Podmiotu w wiadomości e-mail.  Nie można zmodyfikować treści wiadomości. |
| Adresaci |Adresy wszystkich adresatów wiadomości e-mail.  Jeśli określono więcej niż jeden adres, oddziel adresy średnikiem (;). |


## <a name="webhook-actions"></a>Akcje elementu Webhook

Akcje elementu Webhook umożliwiają wywołanie procesu zewnętrznego przez pojedyncze żądanie HTTP POST.  Usługa wywoływana powinien obsługuje elementów webhook i określić, jak używać żadnych ładunku odbiera.  Można także wywołać interfejsu API REST, które w szczególności nie obsługuje elementów webhook, jak długo żądanie znajduje się w formacie, który obsługuje usługę interfejsu API.  Przykłady użycia elementu webhook w odpowiedzi na alert wysyłania wiadomości [Slack](http://slack.com) lub Tworzenie zdarzenia w [PagerDuty](http://pagerduty.com/).  Pełny Przewodnik tworzenia reguły alertu z elementu webhook do wywołania zapas czasu jest dostępna na [elementów Webhook w alertach analizy dzienników](log-analytics-alerts-webhooks.md).

Akcje elementu Webhook wymagają właściwości w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Adres URL elementu Webhook |Adres URL elementu webhook. |
| Niestandardowy ładunek JSON |Niestandardowy ładunek do wysłania z elementu webhook.  Aby uzyskać więcej informacji, zobacz poniżej. |


Elementów Webhook obejmują adres URL i zapisany w formacie JSON, które to dane wysyłane do zewnętrznych usługi ładunku.  Domyślnie ładunek zawiera wartości w tabeli poniżej.  Można zastąpić to ładunku niestandardowego własny.  W takim przypadku służy zmiennych w tabeli dla każdego z parametrów do uwzględnienia w niestandardowy ładunek ich wartości.

>[!NOTE]
> Jeśli Twój obszar roboczy został uaktualniony do [nowego języka zapytań usługi Log Analytics](log-analytics-log-search-upgrade.md), ładunek elementu webhook uległ zmianie.  Szczegółowe informacje na temat tego formatu zawiera artykuł [Azure Log Analytics REST API (Interfejs API REST usługi Azure Log Analytics)](https://aka.ms/loganalyticsapiresponse).  Można zobaczyć przykład w [przykłady](#sample-payload) poniżej.

| Parametr | Zmienna | Opis |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Nazwa reguły alertów. |
| AlertThresholdOperator |#thresholdoperator |Operator próg dla reguł alertów.  *Większa niż* lub *mniej niż*. |
| AlertThresholdValue |#thresholdvalue |Wartość progowa reguły alertów. |
| LinkToSearchResults |#linktosearchresults |Link do wyszukiwania dziennika analizy dzienników, która zwraca odpowiednie rekordy z kwerendy utworzony alert. |
| ResultCount |#searchresultcount |Liczba rekordów w wynikach wyszukiwania. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Godzina zakończenia dla zapytania w formacie UTC. |
| SearchIntervalInSeconds |#searchinterval |Przedział czasu dla reguły alertów. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Godzina rozpoczęcia dla zapytania w formacie UTC. |
| SearchQuery |#searchquery |Dziennik wyszukiwania używane przez reguły alertów. |
| Wynikówwyszukiwania |Zobacz poniżej |Rekordów zwróconych przez zapytanie w formacie JSON.  Ograniczone do pierwszych 5000 rekordów. |
| WorkspaceID |#workspaceid |Identyfikator obszaru roboczego analizy dzienników. |

Można na przykład określić następujące niestandardowy ładunek, który zawiera jeden parametr o nazwie *tekstu*.  Usługa, która wywołuje ten element webhook czy oczekiwano tego parametru.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Ten przykładowy ładunek może rozpoznać przypominać następujące przy wysyłaniu do elementu webhook.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

Aby dołączyć wyniki wyszukiwania niestandardowy ładunek, Dodaj następujący wiersz jako właściwość najwyższego poziomu w ładunku json.  

    "IncludeSearchResults":true

Na przykład aby utworzyć niestandardowy ładunek, zawierający tylko nazwę alertu i wyniki wyszukiwania, można poniżej. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Można przeprowadzić za pomocą pełny przykład tworzenie reguły alertu z elementu webhook można uruchomić usługi zewnętrzne w [utworzenie alertu elementu webhook w analizy dzienników do wysyłania wiadomości zapas czasu](log-analytics-alerts-webhooks.md).


## <a name="runbook-actions"></a>Działania elementu Runbook
Działania elementu Runbook uruchamiania elementu runbook automatyzacji Azure.  Aby użyć tego typu akcji, należy skonfigurować [rozwiązania automatyzacja](log-analytics-add-solutions.md) zainstalowany i skonfigurowany w obszarze roboczym analizy dzienników.  Możesz wybrać elementów runbook w ramach konta automatyzacji, skonfigurowanego w rozwiązaniu automatyzacji.

Działania elementu Runbook wymagają właściwości w poniższej tabeli.

| Właściwość | Opis |
|:--- |:---|
| Element Runbook | Element Runbook, który ma być uruchamiany podczas tworzenia alertu. |
| Uruchom na | Określ **Azure** do uruchomienia elementu runbook w chmurze.  Określ **hybrydowy proces roboczy** do uruchomienia elementu runbook na agenta o [hybrydowy proces roboczy elementu Runbook](../automation/automation-hybrid-runbook-worker.md ) zainstalowane.  |

Uruchom działania elementu Runbook przy użyciu elementu runbook [webhook](../automation/automation-webhooks.md).  Podczas tworzenia reguły alertu, automatycznie zostanie utworzony nowy element webhook dla elementu runbook o nazwie **OMS Alert korygowania** następuje identyfikator GUID.  

Nie można bezpośrednio wypełnić wszystkie parametry elementu runbook, ale [parametru $WebhookData](../automation/automation-webhooks.md) będzie zawierać szczegóły alertu, w tym wyniki wyszukiwania dziennika, który go utworzył.  Element runbook, należy zdefiniować **$WebhookData** jako parametr, aby uzyskać dostęp do właściwości alertu.  Dane alertu jest dostępny w formacie json w jedną właściwość o nazwie **właściwości SearchResult** (dla działania elementu runbook i Akcje elementu webhook z ładunku standardowe) lub **wynikówwyszukiwania** (Akcje elementu webhook z niestandardowych w tym ładunku **IncludeSearchResults ": true**) w **RequestBody** właściwość **$WebhookData**.  Będzie to mieć z właściwościami w poniższej tabeli.

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony do [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie ładunku element runbook został zmieniony.  Szczegółowe informacje na temat tego formatu zawiera artykuł [Azure Log Analytics REST API (Interfejs API REST usługi Azure Log Analytics)](https://aka.ms/loganalyticsapiresponse).  Można zobaczyć przykład w [przykłady](#sample-payload) poniżej.  

| Węzeł | Opis |
|:--- |:--- |
| id |Ścieżka i identyfikator GUID wyszukiwania. |
| __metadata |Informacje dotyczące alertu, w tym liczbę rekordów i stan wyników wyszukiwania. |
| wartość |Oddzielny wpis dla każdego rekordu w wynikach wyszukiwania.  Szczegóły wpis będzie zgodny właściwości i wartości rekordu. |

Na przykład następujące elementy runbook wyodrębnić rekordów zwróconych przez dziennik wyszukiwania i przypisać różne właściwości na podstawie typu każdego rekordu.  Należy pamiętać, że element runbook zostanie uruchomiony za pomocą konwersji **RequestBody** z formatu json, którego nie można pracować z jako obiekt w programie PowerShell.

>[!NOTE]
> Użyj obu tych elementów runbook **właściwości SearchResult** właściwość zawiera wyniki działania elementu runbook i Akcje elementu webhook z standardowe ładunku.  Jeśli element runbook były nazywane z elementu webhook odpowiedź przy użyciu niestandardowy ładunek, czy trzeba będzie zmienić tę właściwość, aby **wynikówwyszukiwania**.

Następujący element runbook będzie działać z ładunku z [starszej wersji obszaru roboczego analizy dzienników](log-analytics-log-search-upgrade.md).

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResult.value

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

Następujący element runbook będzie działać z ładunku z [uaktualnione obszaru roboczego analizy dzienników](log-analytics-log-search-upgrade.md).

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody

    # Get all metadata properties    
    $AlertRuleName = $RequestBody.AlertRuleName
    $AlertThresholdOperator = $RequestBody.AlertThresholdOperator
    $AlertThresholdValue = $RequestBody.AlertThresholdValue
    $AlertDescription = $RequestBody.Description
    $LinktoSearchResults =$RequestBody.LinkToSearchResults
    $ResultCount =$RequestBody.ResultCount
    $Severity = $RequestBody.Severity
    $SearchQuery = $RequestBody.SearchQuery
    $WorkspaceID = $RequestBody.WorkspaceId
    $SearchWindowStartTime = $RequestBody.SearchIntervalStartTimeUtc
    $SearchWindowEndTime = $RequestBody.SearchIntervalEndtimeUtc
    $SearchWindowInterval = $RequestBody.SearchIntervalInSeconds

    # Get detailed search results
    if($RequestBody.SearchResult -ne $null)
    {
        $SearchResultRows    = $RequestBody.SearchResult.tables[0].rows 
        $SearchResultColumns = $RequestBody.SearchResult.tables[0].columns;

        foreach ($SearchResultRow in $SearchResultRows)
        {   
            $Column = 0
            $Record = New-Object –TypeName PSObject 
        
            foreach ($SearchResultColumn in $SearchResultColumns)
            {
                $Name = $SearchResultColumn.name
                $ColumnValue = $SearchResultRow[$Column]
                $Record | Add-Member –MemberType NoteProperty –Name $name –Value $ColumnValue -Force
                        
                $Column++
            }

            # Include code to work with the record. 
            # For example $Record.Computer to get the computer property from the record.
            
        }
    }



## <a name="sample-payload"></a>Przykładowy ładunek
W tej sekcji przedstawiono przykładowy ładunek dla Akcje elementu webhook i elementu runbook w obu starszych i [uaktualnione obszaru roboczego analizy dzienników](log-analytics-log-search-upgrade.md).

### <a name="webhook-actions"></a>Akcje elementu Webhook
Oba te przykłady użycia **właściwości SearchResult** właściwość zawiera wyniki dla akcji elementu webhook z standardowe ładunku.  W przypadku elementu webhook jest używany niestandardowy ładunek, zawierającego wyniki wyszukiwania, ta właściwość będzie **wynikówwyszukiwania**.

#### <a name="legacy-workspace"></a>Obszar roboczy starszej wersji.
Poniżej przedstawiono przykładowe ładunku dla akcji elementu webhook w starszej wersji obszaru roboczego.

    {
    "WorkspaceId": "workspaceID",
    "AlertRuleName": "WebhookAlert",
    "SearchQuery": "Type=Usage",
    "SearchResult": {
        "id": "subscriptions/subscriptionID/resourceGroups/ResourceGroupName/providers/Microsoft.OperationalInsights/workspaces/workspace-workspaceID/search/SearchGUID|10.1.0.7|2017-09-27T10-30-38Z",
        "__metadata": {
        "resultType": "raw",
        "total": 1,
        "top": 2147483647,
        "RequestId": "SearchID|10.1.0.7|2017-09-27T10-30-38Z",
        "CoreSummaries": [
            {
            "Status": "Successful",
            "NumberOfDocuments": 135000000
            }
        ],
        "Status": "Successful",
        "NumberOfDocuments": 135000000,
        "StartTime": "2017-09-27T10:30:38.9453282Z",
        "LastUpdated": "2017-09-27T10:30:44.0907473Z",
        "ETag": "636421050440907473",
        "sort": [
            {
            "name": "TimeGenerated",
            "order": "desc"
            }
        ],
        "requestTime": 361
        },
        "value": [
        {
            "Computer": "-",
            "SourceSystem": "OMS",
            "TimeGenerated": "2017-09-26T13:59:59Z",
            "ResourceUri": "/subscriptions/df1ec963-d784-4d11-a779-1b3eeb9ecb78/resourcegroups/mms-eus/providers/microsoft.operationalinsights/workspaces/workspace-861bd466-5400-44be-9552-5ba40823c3aa",
            "DataType": "Operation",
            "StartTime": "2017-09-26T13:00:00Z",
            "EndTime": "2017-09-26T13:59:59Z",
            "Solution": "LogManagement",
            "BatchesWithinSla": 8,
            "BatchesOutsideSla": 0,
            "BatchesCapped": 0,
            "TotalBatches": 8,
            "AvgLatencyInSeconds": 0.0,
            "Quantity": 0.002502,
            "QuantityUnit": "MBytes",
            "IsBillable": false,
            "MeterId": "a4e29a95-5b4c-408b-80e3-113f9410566e",
            "LinkedMeterId": "00000000-0000-0000-0000-000000000000",
            "id": "954f7083-cd55-3f0a-72cb-3d78cd6444a3",
            "Type": "Usage",
            "MG": "00000000-0000-0000-0000-000000000000",
            "__metadata": {
            "Type": "Usage",
            "TimeGenerated": "2017-09-26T13:59:59Z"
            }
        }
        ]
    },
    "SearchIntervalStartTimeUtc": "2017-09-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2017-09-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 1,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://workspaceID.portal.mms.microsoft.com/#Workspace/search/index?_timeInterval.intervalEnd=2017-09-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Type%3DUsage",
    "Description": null,
    "Severity": "Low"
    }


#### <a name="upgraded-workspace"></a>Obszar roboczy uaktualniony.
Poniżej przedstawiono przykładowe ładunku dla akcji elementu webhook w obszarze roboczym uaktualniony.

    {
    "WorkspaceId": "workspaceID",
    "AlertRuleName": "WebhookAlert",
    "SearchQuery": "Usage",
    "SearchResult": {
        "tables": [
        {
            "name": "PrimaryResult",
            "columns": [
            {
                "name": "TenantId",
                "type": "string"
            },
            {
                "name": "Computer",
                "type": "string"
            },
            {
                "name": "TimeGenerated",
                "type": "datetime"
            },
            {
                "name": "SourceSystem",
                "type": "string"
            },
            {
                "name": "StartTime",
                "type": "datetime"
            },
            {
                "name": "EndTime",
                "type": "datetime"
            },
            {
                "name": "ResourceUri",
                "type": "string"
            },
            {
                "name": "LinkedResourceUri",
                "type": "string"
            },
            {
                "name": "DataType",
                "type": "string"
            },
            {
                "name": "Solution",
                "type": "string"
            },
            {
                "name": "BatchesWithinSla",
                "type": "long"
            },
            {
                "name": "BatchesOutsideSla",
                "type": "long"
            },
            {
                "name": "BatchesCapped",
                "type": "long"
            },
            {
                "name": "TotalBatches",
                "type": "long"
            },
            {
                "name": "AvgLatencyInSeconds",
                "type": "real"
            },
            {
                "name": "Quantity",
                "type": "real"
            },
            {
                "name": "QuantityUnit",
                "type": "string"
            },
            {
                "name": "IsBillable",
                "type": "bool"
            },
            {
                "name": "MeterId",
                "type": "string"
            },
            {
                "name": "LinkedMeterId",
                "type": "string"
            },
            {
                "name": "Type",
                "type": "string"
            }
            ],
            "rows": [
            [
                "workspaceID",
                "-",
                "2017-09-26T13:59:59Z",
                "OMS",
                "2017-09-26T13:00:00Z",
                "2017-09-26T13:59:59Z",
                "/subscriptions/SubscriptionID/resourcegroups/ResourceGroupName/providers/microsoft.operationalinsights/workspaces/workspace-workspaceID",
                null,
                "Operation",
                "LogManagement",
                8,
                0,
                0,
                8,
                0,
                0.002502,
                "MBytes",
                false,
                "a4e29a95-5b4c-408b-80e3-113f9410566e",
                "00000000-0000-0000-0000-000000000000",
                "Usage"
            ]
            ]
        }
        ]
    },
    "SearchIntervalStartTimeUtc": "2017-09-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2017-09-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 1,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://workspaceID.portal.mms.microsoft.com/#Workspace/search/index?_timeInterval.intervalEnd=2017-09-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Usage",
    "Description": null,
    "Severity": "Low"
    }


### <a name="runbooks"></a>Elementy Runbook

#### <a name="legacy-workspace"></a>Starszej wersji obszaru roboczego
Poniżej przedstawiono przykładowe ładunku dla działania elementu runbook w starszej wersji obszaru roboczego.

    {
        "SearchResult": {
            "id": "subscriptions/subscriptionID/resourceGroups/ResourceGroupName/providers/Microsoft.OperationalInsights/workspaces/workspace-workspaceID/search/searchGUID|10.1.0.7|TimeStamp",
            "__metadata": {
                "resultType": "raw",
                "total": 1,
                "top": 2147483647,
                "RequestId": "searchGUID|10.1.0.7|2017-09-27T10-51-43Z",
                "CoreSummaries": [{
                    "Status": "Successful",
                    "NumberOfDocuments": 135000000
                }],
                "Status": "Successful",
                "NumberOfDocuments": 135000000,
                "StartTime": "2017-09-27T10:51:43.3075124Z",
                "LastUpdated": "2017-09-27T10:51:51.1002092Z",
                "ETag": "636421063111002092",
                "sort": [{
                    "name": "TimeGenerated",
                    "order": "desc"
                }],
                "requestTime": 511
            },
            "value": [{
                "Computer": "-",
                "SourceSystem": "OMS",
                "TimeGenerated": "2017-09-26T13:59:59Z",
                "ResourceUri": "/subscriptions/AnotherSubscriptionID/resourcegroups/SampleResourceGroup/providers/microsoft.operationalinsights/workspaces/workspace-workspaceID",
                "DataType": "Operation",
                "StartTime": "2017-09-26T13:00:00Z",
                "EndTime": "2017-09-26T13:59:59Z",
                "Solution": "LogManagement",
                "BatchesWithinSla": 8,
                "BatchesOutsideSla": 0,
                "BatchesCapped": 0,
                "TotalBatches": 8,
                "AvgLatencyInSeconds": 0.0,
                "Quantity": 0.002502,
                "QuantityUnit": "MBytes",
                "IsBillable": false,
                "MeterId": "a4e29a95-5b4c-408b-80e3-113f9410566e",
                "LinkedMeterId": "00000000-0000-0000-0000-000000000000",
                "id": "954f7083-cd55-3f0a-72cb-3d78cd6444a3",
                "Type": "Usage",
                "MG": "00000000-0000-0000-0000-000000000000",
                "__metadata": {
                    "Type": "Usage",
                    "TimeGenerated": "2017-09-26T13:59:59Z"
                }
            }]
        }
    }

#### <a name="upgraded-workspace"></a>Uaktualniony obszaru roboczego
Poniżej przedstawiono przykładowe ładunku dla działania elementu runbook w obszarze roboczym uaktualniony.

    {
    "WorkspaceId": "workspaceID",
    "AlertRuleName": "AutomationAlert",
    "SearchQuery": "Usage",
    "SearchResult": {
        "tables": [
        {
            "name": "PrimaryResult",
            "columns": [
            {
                "name": "TenantId",
                "type": "string"
            },
            {
                "name": "Computer",
                "type": "string"
            },
            {
                "name": "TimeGenerated",
                "type": "datetime"
            },
            {
                "name": "SourceSystem",
                "type": "string"
            },
            {
                "name": "StartTime",
                "type": "datetime"
            },
            {
                "name": "EndTime",
                "type": "datetime"
            },
            {
                "name": "ResourceUri",
                "type": "string"
            },
            {
                "name": "LinkedResourceUri",
                "type": "string"
            },
            {
                "name": "DataType",
                "type": "string"
            },
            {
                "name": "Solution",
                "type": "string"
            },
            {
                "name": "BatchesWithinSla",
                "type": "long"
            },
            {
                "name": "BatchesOutsideSla",
                "type": "long"
            },
            {
                "name": "BatchesCapped",
                "type": "long"
            },
            {
                "name": "TotalBatches",
                "type": "long"
            },
            {
                "name": "AvgLatencyInSeconds",
                "type": "real"
            },
            {
                "name": "Quantity",
                "type": "real"
            },
            {
                "name": "QuantityUnit",
                "type": "string"
            },
            {
                "name": "IsBillable",
                "type": "bool"
            },
            {
                "name": "MeterId",
                "type": "string"
            },
            {
                "name": "LinkedMeterId",
                "type": "string"
            },
            {
                "name": "Type",
                "type": "string"
            }
            ],
            "rows": [
            [
                "861bd466-5400-44be-9552-5ba40823c3aa",
                "-",
                "2017-09-26T13:59:59Z",
                "OMS",
                "2017-09-26T13:00:00Z",
                "2017-09-26T13:59:59Z",
            "/subscriptions/SubscriptionID/resourcegroups/ResourceGroupName/providers/microsoft.operationalinsights/workspaces/workspace-861bd466-5400-44be-9552-5ba40823c3aa",
                null,
                "Operation",
                "LogManagement",
                8,
                0,
                0,
                8,
                0,
                0.002502,
                "MBytes",
                false,
                "a4e29a95-5b4c-408b-80e3-113f9410566e",
                "00000000-0000-0000-0000-000000000000",
                "Usage"
            ]
        }
        ]
    },
    "SearchIntervalStartTimeUtc": "2017-09-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2017-09-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 1,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://workspaceID.portal.mms.microsoft.com/#Workspace/search/index?_timeInterval.intervalEnd=2017-09-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Usage",
    "Description": null,
    "Severity": "Critical"
    }



## <a name="next-steps"></a>Kolejne kroki
- Zakończenie wskazówki dla [Konfigurowanie webook](log-analytics-alerts-webhooks.md) z reguły alertu.  
- Dowiedz się, jak napisać [elementy runbook automatyzacji Azure](https://azure.microsoft.com/documentation/services/automation) skorygować problemy zidentyfikowane przez alertów.