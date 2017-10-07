---
title: "aaaStream tooan dzienników diagnostycznych platformy Azure Event Hubs Namespace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostream Azure diagnostycznych dzienników tooan centra zdarzeń w przestrzeni nazw."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Strumień dzienników diagnostycznych platformy Azure tooan Namespace centra zdarzeń
**[Azure dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md)**  mogła być przesłana strumieniowo w pobliżu aplikacji tooany czasu rzeczywistego przy użyciu hello wbudowanych "Eksportuj koncentratory tooEvent" opcji w portalu hello lub przez włączenie hello identyfikator reguły magistrali usług w ustawienie diagnostyczne za pośrednictwem hello Azure PowerShell Polecenia cmdlet lub Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Co można zrobić z dzienników diagnostyki i usługi Event Hubs
Poniżej przedstawiono kilka sposobów może używać hello przesyłanie strumieniowe możliwości do dzienników diagnostycznych:

* **Strumień rejestruje systemów firm too3rd rejestrowania i dane telemetryczne** — wraz z upływem czasu przesyłania strumieniowego usługi Event Hubs ma zostać toopipe mechanizmu hello dzienników diagnostycznych w rozwiązań Siem toothird firm a dziennika rozwiązań analitycznych.
* **Wyświetlić kondycję usługi przesyłania strumieniowego "aktywnej ścieżki" tooPowerBI danych** — za pomocą usługi Event Hubs, Stream Analytics i usługi Power BI, dane diagnostyki toonear wgląd w czasie rzeczywistym mogą łatwo przekształcić na usługami Azure. [Ten artykuł dokumentacja zawiera wszechstronne omówienie sposobu przetwarzania danych za pomocą usługi Stream Analytics tooset się usługi Event Hubs i używać usługi Power BI jako dane wyjściowe](../stream-analytics/stream-analytics-power-bi-dashboard.md). Oto kilka porad dotyczących uzyskiwania skonfigurowany z dzienników diagnostycznych:
  
  * Centrum zdarzeń dla kategorii dzienników diagnostycznych jest tworzona automatycznie podczas sprawdzania hello opcji w portalu hello lub włączyć za pomocą programu PowerShell, więc chcesz Centrum zdarzeń hello tooselect w hello nazw o nazwie hello rozpoczyna się od **insights**.
  * Przykładowe Stream Analytics jest Hello następującego kodu SQL kwerendy, której można tooparse wszystkie dane dziennika hello tabeli tooa usługi Power BI:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Tworzenie niestandardowych telemetrii i rejestrowanie platformy** — Jeśli masz już platformy telemetrii niestandardowej lub są po prostu pomyśleć o budynku jedną hello skalowalnej publikowania / subskrypcji rodzaj usługi Event Hubs umożliwia tooflexibly pozyskiwania diagnostycznych dzienniki. [Zobacz Dan Rosanova przewodnik toousing centra zdarzeń w skali globalnej platformy telemetrii tutaj](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Przesyłania strumieniowego dzienników diagnostycznych
Można włączyć przesyłania strumieniowego dzienników diagnostycznych programowo, za pośrednictwem portalu hello, lub za pomocą hello [interfejsów API REST Monitor Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). W obu przypadkach należy utworzyć ustawienie diagnostyczne z określonymi przestrzeni nazw usługi Event Hubs i hello dziennika kategorii i metryki ma toosend w toohello przestrzeni nazw. Centrum zdarzeń jest tworzony w przestrzeni nazw powitania dla każdej kategorii dziennika, który zostanie włączone. Diagnostyka **kategorii dziennika** jest typem dziennika, który może zbierać zasobu.

> [!WARNING]
> Włączanie i przesyłania strumieniowego dzienników diagnostycznych z zasobów obliczeniowych (na przykład maszyny wirtualne lub sieci szkieletowej usług) [wymaga innego zestawu kroków](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Hello usługi Service Bus lub Event Hubs w przestrzeni nazw nie ma toobe hello tej samej subskrypcji co zasób hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Strumieniowe przesyłanie dzienników diagnostycznych za pomocą portalu hello
1. W portalu hello Przejdź tooAzure monitora, a następnie kliknij **ustawień diagnostycznych**

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Opcjonalnie Filtruj listę hello według grupy zasobów lub typ zasobu, a następnie kliknij na powitania zasobu, dla którego chcesz tooset ustawienie diagnostyczne.

3. Jeśli nie istnieją żadne ustawienia na powitania zasobów, wybrana przez Ciebie, jesteś toocreate zostanie wyświetlony monit o ustawienie. Kliknij pozycję "Włącz diagnostykę."

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   W przypadku ustawienia istniejące na powitania zasobów, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu. Kliknij przycisk "Dodaj ustawienie diagnostyczne".

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Nadaj nazwę ustawienia i sprawdź pole hello **Centrum zdarzeń tooan strumienia**, następnie wybierz obszar nazw usługi Event Hubs.
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Hello wybrane przestrzeni nazw będzie gdzie (jeżeli jest to pierwsza przesyłania strumieniowego dzienników diagnostycznych) lub zbyt strumieniowo hello Centrum zdarzeń (jeśli istnieje już zasobów, które są przesyłania strumieniowego tej przestrzeni nazw toothis kategorii dziennika), i hello zasady określają hello uprawnienia, które ma hello mechanizm przesyłania strumieniowego. Obecnie przesyłania strumieniowego tooan Centrum zdarzeń wymaga uprawnienia Zarządzanie, wysyłania i nasłuchiwania. Można utworzyć lub zmodyfikować zasady dostępu przestrzeń nazw udostępnionych centra zdarzeń w portalu hello karcie Konfigurowanie hello przestrzeni nazw. tooupdate, jeden z tych ustawień diagnostycznych powitania klienta musi mieć uprawnienie ListKey hello na reguły autoryzacji hello usługi Event Hubs.

4. Kliknij pozycję **Zapisz**.

Po kilku chwilach hello nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu, a dzienników diagnostycznych są przesyłane strumieniowo toothat konta magazynu, natychmiast po wygenerowaniu nowych danych zdarzenia.

### <a name="via-powershell-cmdlets"></a>Za pomocą poleceń cmdlet programu PowerShell
tooenable przesyłania strumieniowego za pośrednictwem hello [polecenia cmdlet programu PowerShell usługi Azure](insights-powershell-samples.md), można użyć hello `Set-AzureRmDiagnosticSetting` polecenia cmdlet z następującymi parametrami:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hello identyfikator reguły magistrali usług to ciąg w formacie: `{Service Bus resource ID}/authorizationrules/{key name}`, na przykład `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Za pomocą interfejsu wiersza polecenia platformy Azure
tooenable przesyłania strumieniowego za pośrednictwem hello [interfejsu wiersza polecenia Azure](insights-cli-samples.md), można użyć hello `insights diagnostic set` polecenia w następujący sposób:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Użyj hello sam format identyfikator reguły magistrali usługi zgodnie z objaśnieniem dla hello polecenia Cmdlet programu PowerShell.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Jak korzystać z hello danych dziennika z usługi Event Hubs?
Oto przykładowe dane wyjściowe dane z centrów zdarzeń:

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Nazwa elementu | Opis |
| --- | --- |
| rekordy |Tablica wszystkie zdarzenia dziennika, w tym ładunku. |
| time |Czas, jaką hello wystąpiło zdarzenie. |
| category |Kategoria dziennika dla tego zdarzenia. |
| resourceId |Identyfikator zasobu hello zasobu, który wygenerował zdarzenie. |
| operationName |Nazwa operacji hello. |
| poziom |Opcjonalny. Wskazuje poziom zdarzenia dziennika hello. |
| properties |Właściwości zdarzenia hello. |

Można wyświetlić listę wszystkich dostawców zasobów obsługujących przesyłania strumieniowego koncentratory tooEvent [tutaj](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Strumień danych z zasoby obliczeniowe
Można również przesyłania strumieniowego dzienników diagnostycznych z zasobów obliczeniowych, przy użyciu agenta Windows Azure Diagnostics hello. [Znajduje się w artykule](../event-hubs/event-hubs-streaming-azure-diags-data.md) jak tooset tego w górę.

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat dzienników diagnostycznych platformy Azure](monitoring-overview-of-diagnostic-logs.md)
* [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

