---
title: "aaaQuery wiadomości B2B w Operations Management Suite — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie zapytań tootrack AS2, X 12 i EDIFACT wiadomości w hello Operations Management Suite"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Zapytanie o AS2, X 12 i EDIFACT wiadomości powitania programu Microsoft Operations Management Suite (OMS)

toofind hello AS2, X 12 i EDIFACT komunikaty śledzenia z [Azure Log Analytics](../log-analytics/log-analytics-overview.md) w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), można utworzyć kwerendy, które są oparte na określonych akcji filtrowania kryteria. Na przykład można znaleźć na podstawie różnych kontroli określonych wymiany wiadomości.

## <a name="requirements"></a>Wymagania

* Aplikację logiki, który został skonfigurowany z rejestrowania diagnostyki. Dowiedz się [jak toocreate aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) i [jak tooset rejestrowanie dla danej aplikacji logiki danych](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Konta integracji, które skonfigurowano przy użyciu rejestrowania i monitorowania. Dowiedz się [jak toocreate konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) i [jak tooset monitorowania i rejestrowania dla tego konta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Jeśli nie jest jeszcze, [publikowania danych diagnostycznych tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) i [Konfigurowanie śledzenia w OMS wiadomości](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Po zostały spełnione wymagania poprzedniej hello, powinien mieć obszar roboczy w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Należy używać tego samego pakietu OMS obszaru roboczego do śledzenia komunikacji B2B w OMS hello. 
>  
> Dowiedz się, jeśli nie masz obszar roboczy OMS [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Tworzenie kwerend komunikatów z filtrami w portalu usługi Operations Management Suite hello

Ten przykład przedstawia, jak można znaleźć na podstawie ich liczby kontroli wymiany wiadomości.

> [!TIP] 
> Jeśli znasz nazwę obszar roboczy OMS Przejdź strona główna obszaru roboczego tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) i uruchomić w kroku 4. W przeciwnym razie Rozpocznij w kroku 1.

1. W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**. Wyszukaj "analizy dzienników", a następnie wybierz pozycję **analizy dzienników** w sposób pokazany poniżej:

   ![Znajdź analizy dzienników](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS.

   ![Wybierz obszar roboczy OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. W obszarze **zarządzania**, wybierz **portalu OMS**.

   ![Wybierz portalu OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. Na stronie głównej OMS wybierz **wyszukiwania dziennika**.

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   — lub —

   ![W menu OMS hello wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. W polu wyszukiwania hello, wprowadź pola, które mają toofind i naciśnij klawisz **Enter**. Po rozpoczęciu wprowadzania, OMS pokazuje, pasujących i operacje, które są dostępne. Dowiedz się więcej o [jak toofind danych analizy dzienników](../log-analytics/log-analytics-log-searches.md).

   W tym przykładzie wyszukuje zdarzeń o **typu = AzureDiagnostics**.

   ![Wpisz ciąg zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. Na pasku po lewej stronie powitania, wybierz przedział czasu hello, które mają tooview. tooadd kwerendy tooyour filtru, wybierz **+ Dodaj**.

   ![Dodaj filtr tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. W obszarze **Dodaj filtry**, wprowadź nazwę filtru hello, aby umożliwić znalezienie hello filtr ma. Wybierz filtr hello, a następnie wybierz pozycję **+ Dodaj**.

   toofind numer formantu wymiany hello, w tym przykładzie wyszukuje hello word "wymiany" i wybiera **event_record_messageProperties_interchangeControlNumber_s** jako hello filtru.

   ![Wybierz filtr](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Na pasku po lewej stronie powitania, wybierz wartość filtru hello mają toouse i wybierz polecenie **Zastosuj**.

   W tym przykładzie wybiera numer kontroli hello wymiany wiadomości powitania, którą chcemy udostępnić.

   ![Wybierz wartości filtru](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Teraz wróć toohello zapytania, które tworzysz. Kwerenda została zaktualizowana wybrany filtr zdarzeń i wartość. Poprzednie wyniki teraz są zbyt filtrowane.

    ![Zwraca tooyour filtrowane wyniki zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Zapisz zapytanie do użytku w przyszłości

1. Z kwerendy na powitania **wyszukiwania dziennika** wybierz pozycję **zapisać**. Nadaj nazwę kwerendy, wybierz kategorię i wybierz **zapisać**.

   ![Nadaj zapytania, nazwę i kategorii](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview kwerendy, wybierz **ulubione**.

   ![Wybierz pozycję "Ulubione"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. W obszarze **zapisane wyszukiwania**, wybierz zapytanie, dzięki czemu można wyświetlić wyniki hello. tooupdate hello zapytania, aby umożliwić znalezienie różne wyniki, Edytuj hello zapytanie.

   ![Wybierz zapytanie](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Znajdź i uruchom zapisane kwerendy w portalu usługi Operations Management Suite hello

1. Otwórz stronę główną obszar roboczy OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) i wybierz polecenie **wyszukiwania dziennika**.

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   — lub —

   ![W menu OMS hello wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. Na powitania **wyszukiwania dziennika** strony głównej, wybierz **ulubione**.

   ![Wybierz pozycję "Ulubione"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. W obszarze **zapisane wyszukiwania**, wybierz zapytanie, dzięki czemu można wyświetlić wyniki hello. tooupdate hello zapytania, aby umożliwić znalezienie różne wyniki, Edytuj hello zapytanie.

   ![Wybierz zapytanie](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Następne kroki

* [Schematy śledzenia AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schematy śledzenia X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Śledzenie niestandardowych schematów](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)