---
title: "Strumienia Azure dzienników diagnostycznych do Centrum zdarzeń | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak strumienia Azure dzienników diagnostycznych do Centrum zdarzeń."
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
ms.date: 12/22/2017
ms.author: johnkem
ms.openlocfilehash: bcb9fcb2371217e7082d96ddbba4a095e6d9a00f
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/22/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hub"></a>Dzienniki diagnostyczne strumienia Azure do Centrum zdarzeń
**[Azure dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md)**  mogą być przesyłane strumieniowo w najbliższym czasie rzeczywistym do aplikacji przy użyciu wbudowanych opcji "Eksportuj do usługi Event Hubs", w portalu lub przez włączenie identyfikator reguły autoryzacji Centrum zdarzeń w ustawienie diagnostyczne za pośrednictwem platformy Azure Polecenia cmdlet programu PowerShell lub Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Co można zrobić z dzienników diagnostyki i usługi Event Hubs
Poniżej przedstawiono kilka sposobów można na przykład możliwość przesyłania strumieniowego dzienników diagnostycznych:

* **Strumienia dzienniki 3 systemów firm rejestrowania i dane telemetryczne** — przesyłania strumieniowego wszystkich dzienników diagnostycznych do koncentratora pojedyncze zdarzenie do potoku danych dziennika narzędzia analizy rozwiązania SIEM lub dziennika innej firmy.
* **Wyświetlić kondycję usługi przesyłania strumieniowego "aktywnej ścieżki" danych do usługi Power BI** — za pomocą usługi Event Hubs, Stream Analytics i usługi Power BI, łatwo można przekształcać dane diagnostyczne w prawie w czasie rzeczywistym rozeznanie usługami Azure. [Ten artykuł dokumentacja zawiera wszechstronne omówienie sposobu konfigurowania usługi Event Hubs, przetwarzania danych za pomocą usługi Stream Analytics i używać usługi Power BI jako dane wyjściowe](../stream-analytics/stream-analytics-power-bi-dashboard.md). Oto kilka porad dotyczących uzyskiwania skonfigurowany z dzienników diagnostycznych:
  
  * Centrum zdarzeń dla kategorii dzienników diagnostycznych jest tworzona automatycznie po zaznaczeniu opcji w portalu lub włączyć za pomocą programu PowerShell, tak aby wybrać Centrum zdarzeń w obszarze nazw o nazwie, która rozpoczyna się od **insights -**.
  * Następujący kod SQL jest przykładowe zapytanie Stream Analytics można przeanalizować wszystkie dane dziennika w tabeli usługi Power BI:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Tworzenie niestandardowych telemetrii i rejestrowanie platformy** — Jeśli masz już platformy telemetrii niestandardowej lub są tylko pomyśleć o jeden wysoce skalowalna tworzenia charakter publikowania / subskrypcji usługi Event hubs umożliwia elastyczne pozyskiwania dzienników diagnostycznych. [Zobacz Przewodnik Dan Rosanova przy użyciu usługi Event Hubs w skali globalnej platformy telemetrii tutaj](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Przesyłania strumieniowego dzienników diagnostycznych
Można włączyć przesyłania strumieniowego dzienników diagnostycznych programowo, w portalu lub przy użyciu [interfejsów API REST Monitor Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). W obu przypadkach należy utworzyć ustawienie diagnostyczne, w którym można określić przestrzeni nazw usługi Event Hubs i kategorie dziennika i metryk, które chcesz wysłać do przestrzeni nazw. Centrum zdarzeń jest tworzony w przestrzeni nazw dla każdej kategorii dziennika, który zostanie włączone. Diagnostyka **kategorii dziennika** jest typem dziennika, który może zbierać zasobu.

> [!WARNING]
> Włączanie i przesyłania strumieniowego dzienników diagnostycznych z zasobów obliczeniowych (na przykład maszyny wirtualne lub sieci szkieletowej usług) [wymaga innego zestawu kroków](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Centra zdarzeń w przestrzeni nazw nie ma w tej samej subskrypcji co zasób emitowanie dzienniki, dopóki użytkownik, który konfiguruje ustawienia ma odpowiedni dostęp RBAC do obu subskrypcji.

## <a name="stream-diagnostic-logs-using-the-portal"></a>Strumieniowe przesyłanie dzienników diagnostycznych przy użyciu portalu
1. W portalu przejdź do monitora Azure i kliknij na **ustawień diagnostycznych**

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Opcjonalnie Filtruj listę według grupy zasobów lub typ zasobu, a następnie kliknij na zasobie, dla której chcesz skonfigurować ustawienie diagnostyczne.

3. Jeśli nie istnieją żadne ustawienia zasobu wybrany, zostanie wyświetlony monit, aby utworzyć ustawienie. Kliknij pozycję "Włącz diagnostykę."

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   W przypadku istniejących ustawień na zasobie, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu. Kliknij przycisk "Dodaj ustawienie diagnostyczne".

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Nadaj nazwę ustawienia i pole wyboru dla **strumienia do Centrum zdarzeń**, następnie wybierz obszar nazw usługi Event Hubs.
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Przestrzeni nazw wybrane będzie gdzie (jeżeli jest to pierwszy przesyłania strumieniowego dzienników diagnostycznych czasu) lub przesyłane strumieniowo do Centrum zdarzeń (jeśli istnieje już zasobów, które są przesyłania strumieniowego tej kategorii dziennika do tej przestrzeni nazw), a zasada definiuje uprawnienia który przesyłanie strumieniowe mechanizmu ma. Obecnie przesyłania strumieniowego do Centrum zdarzeń wymaga uprawnienia Zarządzanie, wysyłania i nasłuchiwania. Można utworzyć lub zmodyfikować zasady dostępu przestrzeń nazw udostępnionych centra zdarzeń w portalu na karcie Konfiguracja przestrzeni nazw. Aby zaktualizować jednego z tych ustawień diagnostycznych, klient musi mieć uprawnienie ListKey dla reguły autoryzacji usługi Event Hubs. Opcjonalnie można określić nazwę Centrum zdarzeń. Jeśli określisz nazwy Centrum zdarzeń, dzienniki są kierowane do tego Centrum zdarzeń, a nie z koncentratorem nowo utworzonego zdarzenia według kategorii dziennika.

4. Kliknij pozycję **Zapisz**.

Po kilku chwilach nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu, a dzienników diagnostycznych są przesyłane strumieniowo do tego Centrum zdarzeń zaraz po wygenerowaniu nowych danych zdarzenia.

### <a name="via-powershell-cmdlets"></a>Za pomocą poleceń cmdlet programu PowerShell
Przesyłania strumieniowego za pośrednictwem [poleceń cmdlet programu PowerShell Azure](insights-powershell-samples.md), można użyć `Set-AzureRmDiagnosticSetting` polecenia cmdlet z następującymi parametrami:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Identyfikator reguły magistrali usług jest ciąg w formacie: `{Service Bus resource ID}/authorizationrules/{key name}`, na przykład `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`. Obecnie nie można wybrać nazwę koncentratora określonego zdarzenia przy użyciu programu PowerShell.

### <a name="via-azure-cli"></a>Za pomocą interfejsu wiersza polecenia platformy Azure
Do przesyłania strumieniowego za pośrednictwem [interfejsu wiersza polecenia Azure](insights-cli-samples.md), można użyć `insights diagnostic set` polecenia w następujący sposób:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Użyj tego samego formatu dla identyfikator reguły magistrali usług, zgodnie z objaśnieniem dla polecenia Cmdlet programu PowerShell. Obecnie nie można wybrać określonego zdarzenia nazwę Centrum z wiersza polecenia platformy Azure.

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a>Jak korzystać z danych dziennika z usługi Event Hubs?
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
| time |Czas, w którym wystąpiło zdarzenie. |
| category |Kategoria dziennika dla tego zdarzenia. |
| resourceId |Identyfikator zasobu zasobu, który wygenerował zdarzenie. |
| operationName |Nazwa operacji. |
| poziom |Opcjonalny. Wskazuje poziom dziennika zdarzeń. |
| properties |Właściwości zdarzenia. |

Można wyświetlić listę wszystkich dostawców zasobów, które obsługi przesyłania strumieniowego do usługi Event Hubs [tutaj](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Strumień danych z zasoby obliczeniowe
Można również przesyłania strumieniowego dzienników diagnostycznych z zasobów obliczeniowych, przy użyciu agenta Windows Azure Diagnostics. [Znajduje się w artykule](../event-hubs/event-hubs-streaming-azure-diags-data.md) jak to skonfigurować.

## <a name="next-steps"></a>Kolejne kroki
* [Więcej informacji na temat dzienników diagnostycznych platformy Azure](monitoring-overview-of-diagnostic-logs.md)
* [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

