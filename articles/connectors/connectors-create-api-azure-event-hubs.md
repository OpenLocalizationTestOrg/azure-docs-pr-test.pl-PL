---
title: "aaaSet Monitor zdarzeń w usłudze Azure Event Hubs dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Monitorowanie zdarzeń tooreceive strumieni danych i wysyłania zdarzeń dla usługi Azure Logic Apps w usłudze Azure Event Hubs"
services: logic-apps
keywords: "strumień danych, monitor zdarzeń, usługa event hubs"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Monitorowanie, odbierania i wysyłania zdarzeń z łącznikiem usługi Event Hubs hello

tooset Monitor zdarzeń, aby aplikację logiki można wykrywać zdarzenia, zdarzenia są rejestrowane i wysyłać zdarzenia, Połącz tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) z aplikacji logiki. Dowiedz się więcej o [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Wymagania

* Masz toohave [centra zdarzeń w przestrzeni nazw i Centrum zdarzeń](../event-hubs/event-hubs-create.md) na platformie Azure. Dowiedz się [jak toocreate centra zdarzeń w przestrzeni nazw i Centrum zdarzeń](../event-hubs/event-hubs-create.md). 

* toouse [każdy łącznik](https://docs.microsoft.com/azure/connectors/apis-list) w aplikacji logiki, masz toocreate aplikacji logiki najpierw. Dowiedz się [jak toocreate aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Sprawdź uprawnienia przestrzeni nazw usługi Event Hubs i Znajdź parametry połączenia hello

Dla Twojego tooaccess aplikacji logiki dowolnej usługi, masz toocreate [ *połączenia* ](./connectors-overview.md) między logiki aplikacji i hello usługi, jeśli nie jest jeszcze. To połączenie autoryzuje danych tooaccess aplikacji logiki.
Dla Twojego tooaccess aplikacji logiki Centrum zdarzeń, masz toohave **Zarządzaj** uprawnienia i hello parametry połączenia dla przestrzeni nazw usługi Event Hubs.

toocheck swoje uprawnienia i get hello parametrów połączenia, wykonaj następujące kroki.

1.  Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure"). 

2.  Przejdź do usługi Event Hubs tooyour *przestrzeni nazw*, nie hello określonym Centrum zdarzeń. W bloku przestrzeni nazw hello w obszarze **ustawienia**, wybierz **zasady dostępu współużytkowanego**. W obszarze **oświadczeń**, sprawdź, czy masz **Zarządzaj** uprawnienia dla tej przestrzeni nazw.

    ![Zarządzaj uprawnieniami dla przestrzeni nazw Centrum zdarzeń](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  Wybierz parametry połączenia hello toocopy dla przestrzeni nazw usługi Event Hubs hello **RootManageSharedAccessKey**. Następny tooyour podstawowego klucza parametry połączenia, kliknij przycisk Kopiuj hello.

    ![Skopiuj parametry połączenia w przestrzeni nazw usługi Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm czy ciąg połączenia jest skojarzony z przestrzeni nazw usługi Event Hubs lub z określonym Centrum zdarzeń, sprawdź ciąg połączenia hello hello `EntityPath` parametru. Możesz znaleźć tego parametru, ciąg połączenia hello jest przeznaczony dla określonego Centrum zdarzeń "entity" i nie jest toouse poprawny ciąg hello z aplikacji logiki.

4.  Teraz po wyświetleniu monitu o poświadczenia, po dodaniu usługi Event Hubs wyzwalacza lub akcji tooyour logikę aplikacji, możesz połączyć tooyour centra zdarzeń w przestrzeni nazw. Nadaj nazwę połączenia, wprowadź parametry połączenia hello, który został skopiowany, a wybierz **Utwórz**.

    ![Wprowadź parametry połączenia dla przestrzeni nazw usługi Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Po utworzeniu połączenia, nazwa połączenia hello powinna pojawić się w wyzwalacza usługi Event Hubs hello lub akcji. 
    Następnie możesz nadal z hello inne czynności w aplikacji logiki.

    ![Połączenia nazw centra zdarzeń utworzony](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Uruchamianie przepływu pracy w Centrum zdarzeń odebrania nowych zdarzeń

A [ *wyzwalacza* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) jest zdarzeniem, która uruchamia przepływ pracy w aplikacji logiki. Aby uruchomić przepływ pracy, gdy nowe zdarzenia są wysyłane tooyour Centrum zdarzeń, wykonaj następujące kroki dodawania hello wyzwalacz, który wykryje to zdarzenie.

1.  W hello [portalu Azure](https://portal.azure.com "portalu Azure"), przejdź do istniejących aplikacji logiki tooyour lub tworzenie aplikacji logiki puste.

2.  W polu wyszukiwania hello na powitania projektanta aplikacji logiki, wprowadź `event hubs` filtru. Wybierz ten wyzwalacz: **podczas zdarzenia są dostępne w Centrum zdarzeń**

    ![Wybierz wyzwalacz po odbiera nowych zdarzeń w Centrum zdarzeń](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Jeśli nie masz już przestrzeń nazw usługi Event Hubs tooyour połączenie, zostanie wyświetlony monit toocreate teraz tego połączenia. Nadaj nazwę połączenia, a następnie wprowadź hello parametry połączenia dla przestrzeni nazw usługi Event Hubs. 
    Dowiedz się, jeśli to konieczne, [jak toofind parametrów połączenia](#permissions-connection-string).

    ![Wprowadź parametry połączenia dla przestrzeni nazw usługi Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Po utworzeniu połączenia hello hello ustawienia hello **podczas zdarzenia w dostępnych w Centrum zdarzeń** wyzwalacza są wyświetlane.

    ![Ustawienia wyzwalacza po odbiera nowych zdarzeń w Centrum zdarzeń](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Wprowadź lub wybierz nazwę hello hello Centrum zdarzeń, które mają toomonitor. Wybierz hello częstotliwość i interwał częstotliwość hello toocheck Centrum zdarzeń.

    > [!TIP]
    > toooptionally zaznacz grupy odbiorców do odczytywania zdarzeń, wybierz polecenie **Pokaż zaawansowane opcje**. 

    ![Określ Centrum zdarzeń lub grupy odbiorców](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Teraz skonfigurowaniu toostart wyzwalacz przepływu pracy aplikacji logiki. 
    Aplikację logiki sprawdza, czy hello określony na podstawie harmonogramu hello, które można ustawić Centrum zdarzeń. 
    Jeśli aplikacji znajdzie nowe zdarzenia w hello Centrum zdarzeń, wyzwalacz hello wykonuje inne operacje i wyzwalaczy aplikacji logiki.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Wysyłanie zdarzeń tooyour Centrum zdarzeń z aplikacji logiki

[*Akcja*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) to zadanie wykonywane przez przepływ pracy aplikacji logiki. Po dodaniu aplikacji logiki wyzwalacza tooyour, można dodać operacji tooperform akcji z danych wygenerowanych przez tego wyzwalacza. toosend tooyour zdarzeń Centrum zdarzeń z aplikacji logiki, wykonaj następujące kroki.

1.  W Projektancie aplikacji logiki, zgodnie z wyzwalaczem aplikacji logiki, wybierz **nowy krok** > **Dodaj akcję**.

    ![Wybierz pozycję "Nowy krok", następnie "Dodaj akcję"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Teraz można znaleźć i wybrać tooperform akcji. 
    Chociaż można wybrać żadnych akcji, na przykład chcemy hello centra zdarzeń w akcji toosend zdarzenia.

2.  W polu wyszukiwania hello, wprowadź `event hubs` filtru.
Wybierz tę akcję: **wysyłania zdarzeń**

    ![Wybierz opcję "Event Hubs — wysyłanie zdarzeń" akcji](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Wprowadź szczegóły hello wymagane dla hello zdarzenia, takie jak nazwa hello hello Centrum zdarzeń, w którym ma toosend hello zdarzeń. Wprowadź inne opcjonalne szczegóły dotyczące zdarzenia hello, takie jak zawartość dla tego zdarzenia.

    > [!TIP]
    > toooptionally Określ hello partycji Centrum zdarzeń, gdy toosend hello zdarzenia, wybierz **Pokaż zaawansowane opcje**. 

    ![Wprowadź nazwę Centrum zdarzeń i szczegóły zdarzenia opcjonalne](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Zapisz zmiany.

    ![Zapisywanie aplikacji logiki](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    Teraz skonfigurowaniu zdarzenia toosend akcji z aplikacji logiki. 

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/eventhubs/). 

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask, odpowiadanie na pytania i robią innych użytkowników usługi Azure Logic Apps, zobacz odwiedź hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

*  [Znajdź inne łączniki dla usługi Azure Logic apps](./apis-list.md)