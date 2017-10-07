---
title: "Stan aaaCheck Konfigurowanie rejestrowania i uzyskiwanie alertów - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Stan Monitora wydajności dla usługi logic apps rejestrowanie danych diagnostycznych i Konfigurowanie alertów"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Monitorowanie stanu, konfigurowanie rejestrowania diagnostyki i Włącz alerty dla usługi Azure Logic Apps

Po [tworzenie i uruchamianie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md), można sprawdzić historię uruchomień, Historia wyzwalacza, stanu i wydajności. Monitorowanie zdarzeń w czasie rzeczywistym i debugowanie bardziej rozbudowane, skonfiguruj [rejestrowania diagnostyki](#azure-diagnostics) aplikacji logiki. W ten sposób można [Znajdowanie i wyświetlać zdarzenia](#find-events), takie jak zdarzenia wyzwalacza, uruchom zdarzeń i zdarzenia akcji. Możesz także użyć tej funkcji [danych diagnostycznych z innymi usługami](#extend-diagnostic-data), takie jak usługi Azure Storage i Azure Event Hubs. 

Konfigurowanie tooget powiadomienia o awarii lub innych możliwych problemów [alerty](#add-azure-alerts). Na przykład można utworzyć alertu wykrywa "więcej niż pięć uruchamia się niepowodzeniem w ciągu godziny." Można również skonfigurować monitorowanie, śledzenie i rejestrowanie programowo przy użyciu [ustawienia zdarzeń diagnostyki Azure i właściwości](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Uruchamia widok i historii wyzwalacza dla aplikacji logiki

1. toofind aplikację logiki w hello [portalu Azure](https://portal.azure.com)na temat hello Azure menu głównego, wybierz **więcej usług**. Pole wyszukiwania Witaj, "aplikacje logiki" Znajdź i wybierz polecenie **Logic apps**.

   ![Znajdź aplikację logiki](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   Hello portalu Azure zawiera wszystkie aplikacje logiki hello, które są skojarzone z subskrypcją platformy Azure. 

2. Wybierz aplikację logiki, a następnie wybierz **omówienie**.

   Hello portalu Azure zawiera historię uruchomień hello i historii wyzwalacza dla aplikacji logiki. Na przykład:

   ![Historia i wyzwalacza historii uruchomieniu aplikacji logiki](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Uruchamia historii** zawiera wszystkie elementy hello aplikacji logiki. 
   * **Wyzwalanie historii** pokazuje wszystkie działania wyzwalacza hello aplikacji logiki.

   Opis stanu, zobacz [rozwiązywania problemów z aplikacją logiki](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Jeśli nie możesz znaleźć hello dane, które należy oczekiwać na powitania narzędzi wybierz **Odśwież**.

3. Witaj tooview kroków z określonego działania, w obszarze **uruchamia historii**, wybierz opcję uruchomienia. 

   Widok monitora Hello zawiera każdego kroku w uruchomienia. Na przykład:

   ![Akcje dla określonego przebiegu](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. tooget więcej szczegółów na temat hello uruchomić, wybierz **Uruchom szczegóły**. Te informacje zawiera podsumowanie kroków hello, stan, dane wejściowe, a dane wyjściowe dla hello Uruchom. 

   ![Wybierz polecenie "Uruchom szczegóły"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Na przykład można uzyskać hello na uruchamianie **identyfikator korelacji**, który może być konieczne użycie hello [interfejsu API REST dla usługi Logic Apps](https://docs.microsoft.com/rest/api/logic).

5. tooget szczegółowe informacje o określonym kroku, można wybrać tego kroku. Teraz możesz przejrzeć szczegóły, takie jak wejść, wyjść i wszelkie błędy, które wystąpiły w tym kroku. Na przykład:

   ![Szczegółowe informacje krok](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Wszystkie szczegóły środowiska uruchomieniowego i zdarzenia są szyfrowane w hello usługi Logic Apps. Są one odszyfrowane tylko wtedy, gdy użytkownik zażąda tooview tych danych. Można też kontrolować dostęp toothese zdarzeń o [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md).

6. tooget szczegóły dotyczące zdarzenia określonego wyzwalacza, przejdź wstecz toohello **omówienie** okienka. W obszarze **wyzwolenia historii**, wybierz pozycję hello wyzwalacz zdarzenia. Teraz można przejrzeć szczegóły, takie jak wejściach i wyjściach, na przykład:

   ![Szczegóły danych wyjściowych zdarzenia wyzwalacza](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Włącz diagnostykę, rejestrowanie aplikacji logiki

Bardziej rozbudowane debugowanie z szczegóły środowiska uruchomieniowego i zdarzenia, można skonfigurować z funkcji rejestrowania diagnostyki [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Analiza dzienników jest usługą [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) który monitoruje chmurze i lokalnych środowiskach toohelp Obsługa ich dostępności i wydajności. 

Przed rozpoczęciem należy toohave obszarem roboczym pakietu OMS. Dowiedz się [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).

1. W hello [portalu Azure](https://portal.azure.com), Znajdź i wybierz aplikację logiki. 

2. Menu hello logiki aplikacji bloku w obszarze **monitorowanie**, wybierz **diagnostyki** > **ustawień diagnostycznych**.

   ![Przejdź do ustawień diagnostycznych tooMonitoring, diagnostyki](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. W obszarze **ustawień diagnostycznych**, wybierz **na**.

   ![Włączanie dzienników diagnostycznych](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. Teraz wybierz hello OMS obszaru roboczego i zdarzeń kategorii w celu rejestrowania, jak pokazano:

   1. Wybierz **wysyłania tooLog Analytics**. 
   2. W obszarze **analizy dzienników**, wybierz **Konfiguruj**. 
   3. W obszarze **obszarów roboczych OMS**, wybierz toouse obszar roboczy OMS hello logowania.
   4. W obszarze **dziennika**, wybierz pozycję hello **WorkflowRuntime** kategorii.
   5. Interwał hello metryki.
   6. Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.

   ![Wybierz obszar roboczy OMS i dane dotyczące rejestrowania](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

Teraz można znaleźć zdarzeń i inne dane dla zdarzenia wyzwalacza, uruchom zdarzenia i akcji.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Znajdź zdarzenia i dane aplikacji logiki

zdarzenia toofind i widok w aplikację logiki, takich jak zdarzenia wyzwalacza, uruchom zdarzenia i akcji, wykonaj następujące kroki.

1. W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**. Wyszukaj "analizy dzienników", a następnie wybierz **analizy dzienników** w sposób pokazany poniżej:

   ![Wybierz pozycję "Analizy dzienników"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS. 

   ![Wybierz obszar roboczy OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. W obszarze **zarządzania**, wybierz **portalu OMS**.

   ![Wybierz pozycję "Portalu OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. Na stronie głównej OMS wybierz **wyszukiwania dziennika**.

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   — lub —

   ![W menu OMS hello wybierz "Dziennik wyszukiwania"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. W polu wyszukiwania hello, określ pola, które mają toofind i naciśnij klawisz **Enter**. Po rozpoczęciu wprowadzania, OMS pokazuje, pasujących i operacje, które są dostępne. 

   Na przykład toofind hello 10 pierwszych zdarzenia, które wystąpiły, wprowadź i wybierz tego zapytania wyszukiwania: **kategorii = WorkflowRuntime | 10 pierwszych**

   ![Wprowadź ciąg wyszukiwania](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   Dowiedz się więcej o [jak toofind danych analizy dzienników](../log-analytics/log-analytics-log-searches.md).

6. Na stronie wyników hello hello pasku po lewej stronie, wybierz przedział czasu hello, które mają tooview.
Wybierz zapytanie, dodając filtr, toorefine **+ Dodaj**.

   ![Wybierz przedział czasu dla wyników zapytania](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. W obszarze **Dodaj filtry**, wprowadź nazwę filtru hello, aby umożliwić znalezienie hello filtr ma. Wybierz filtr hello, a następnie wybierz pozycję **+ Dodaj**.

   W tym przykładzie używa hello word toofind "status" nie powiodło się zdarzenia w obszarze **AzureDiagnostics**.
   W tym miejscu hello filtr dla **status_s** jest już wybrana.

   ![Wybierz filtr](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. Na pasku po lewej stronie powitania, wybierz wartość filtru hello mają toouse i wybierz polecenie **Zastosuj**.

   ![Wybierz wartości filtru, wybierz polecenie "Zastosuj"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Teraz wróć toohello zapytania, które tworzysz. Zapytanie jest aktualizowana z wybranego filtru i wartość. Poprzednie wyniki teraz są zbyt filtrowane.

   ![Zwraca tooyour filtrowane wyniki zapytania](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Wybierz zapytanie do użytku w przyszłości, toosave **zapisać**. Dowiedz się [jak toosave kwerendy](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Rozszerzanie, jak i gdzie używać danych diagnostycznych z innymi usługami

Wraz z Azure Log Analytics można rozszerzyć, jak używasz aplikacji logiki danych diagnostycznych z innymi usługami Azure, na przykład: 

* [Archiwum, które dzienniki diagnostyczne platformy Azure w magazynie Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Strumień tooAzure dzienników diagnostyki Azure Event Hubs](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Następnie monitorowanie za pomocą telemetrii i analiza z innych usług, takich jak get w czasie rzeczywistym [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) i [usługi Power BI](../log-analytics/log-analytics-powerbi.md). Na przykład:

* [Strumień danych z usługi Event Hubs tooStream analityka](../stream-analytics/stream-analytics-define-inputs.md)
* [Analizować dane przesyłane strumieniowo z usługi Stream Analytics i utworzyć pulpit nawigacyjny analiz w czasie rzeczywistym w usłudze Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Oparte na powitania opcje, które chcesz skonfigurować, upewnij się, że możesz pierwszy [utworzyć konto magazynu Azure](../storage/common/storage-create-storage-account.md) lub [tworzenia Centrum zdarzeń Azure](../event-hubs/event-hubs-create.md). Następnie wybierz opcje hello miejscu toosend danych diagnostycznych:

![Wysyłanie danych tooAzure magazynu konta lub zdarzenia Centrum](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Okresy przechowywania mają zastosowanie tylko wtedy, gdy wybierzesz toouse konta magazynu.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Ustawianie alertów dla aplikacji logiki

Przekroczono próg dla aplikacji logiki, lub określonych metryk toomonitor Konfigurowanie [alertów w usłudze Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md). Dowiedz się więcej o [metryki na platformie Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

tooset alerty bez [Azure Log Analytics](../log-analytics/log-analytics-overview.md), wykonaj następujące kroki. Bardziej zaawansowane kryteria alertów i akcji [Konfigurowanie analizy dzienników](#azure-diagnostics) zbyt.

1. Menu hello logiki aplikacji bloku w obszarze **monitorowanie**, wybierz **diagnostyki** > **reguły alertów** > **Dodaj alert**w sposób pokazany poniżej:

   ![Dodawanie alertu dla aplikacji logiki](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. Na powitania **dodać regułę alertu** bloku tworzenia alertu, jak pokazano:

   1. W obszarze **zasobów**, wybierz aplikację logiki, jeśli nie już wybrana. 
   2. Nadaj nazwę i opis alertu.
   3. Wybierz **Metryka** lub zdarzenie, które mają tootrack.
   4. Wybierz **warunku**, określ **próg** hello metryki i wybierz hello **okres** monitorowania ta metryka.
   5. Wybierz, czy toosend poczty hello alertu. 
   6. Określ inne adresy e-mail do wysyłania alertu hello. 
   Można również określić adres URL elementu webhook miejscu toosend hello alertu.

   Na przykład ta reguła wysyła alert, gdy jest pięć lub więcej uruchamia się niepowodzeniem w ciągu godziny:

   ![Utwórz metryki regułę alertu](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> toorun aplikacji logiki z poziomu alertu można uwzględnić hello [wyzwalacza żądania](../connectors/connectors-native-reqres.md) w przepływie pracy, który umożliwia wykonywanie zadań takich jak te przykłady:
> 
> * [Post tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Wyślij tekstu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Dodaj tooa kolejki komunikatów](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Ustawienia zdarzeń diagnostyki Azure i szczegóły

Każde zdarzenie diagnostyczne ma szczegółowe informacje o aplikacji logiki oraz czy zdarzenie, na przykład hello stan i godzina rozpoczęcia, godziny zakończenia, itp. Konfigurowanie monitorowania, śledzenie i rejestrowanie tooprogrammatically, jednostki organizacyjnej za pomocą te szczegóły hello [interfejsu API REST dla usługi Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) i hello [interfejsu API REST Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Na przykład Witaj `ActionCompleted` zdarzenie ma hello `clientTrackingId` i `trackedProperties` właściwości, które służą do monitorowania i śledzenia:

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Jeśli nie pod warunkiem Azure automatycznie generuje ten identyfikator i są powiązane zdarzenia na uruchamianie aplikacji logiki, w tym wszystkie zagnieżdżone przepływy pracy wywoływanych z hello logiki aplikacji. Można ręcznie określić ten identyfikator z wyzwalaczy przekazując `x-ms-client-tracking-id` nagłówek o niestandardowych wartość identyfikator w żądaniu wyzwalacza hello. Można użyć wyzwalacza żądania, wyzwalacz protokołu HTTP lub wyzwalacza elementu webhook.

* `trackedProperties`: tootrack wejściowych i wyjściowych danych diagnostycznych, możesz dodać tooactions śledzonych właściwości w definicji JSON aplikację logiki. Właściwości śledzonych można śledzić tylko jednej akcji wejściach i wyjściach, ale może użyć hello `correlation` właściwości zdarzenia toocorrelate przez akcje do uruchomienia.

  tootrack hello Dodaj co najmniej jednej właściwości `trackedProperties` sekcji i hello właściwości, które toohello definicji działania. Na przykład załóżmy, że chcesz tootrack dane, takie jak "Identyfikator zamówienia" w obrębie telemetrii:

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Następne kroki

* [Tworzenie szablonów dla wdrożenia aplikacji logiki i zarządzania zleceniami](../logic-apps/logic-apps-create-deploy-template.md)
* [Scenariusze B2B z pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Monitorowanie komunikatów B2B](../logic-apps/logic-apps-monitor-b2b-message.md)