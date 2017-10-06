---
title: "Łącznik programu Outlook pakietu Office 365 hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi Office 365 łącznika tooenable interakcji z usługą Office 365. Na przykład: tworzenie, edytowanie i aktualizowanie kontakty i elementy kalendarza."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Rozpoczynanie pracy z hello łącznika programu Outlook pakietu Office 365
Łącznik programu Outlook pakietu Office 365 Hello umożliwia interakcję z programu Outlook w usłudze Office 365. Użyj tego łącznika toocreate, edycji i kontakty aktualizacji i elementy kalendarza i również get, wysyłania i Odpowiedz tooemail.

W programie Outlook pakietu Office 365 możesz:

* Tworzenie przepływu pracy przy użyciu funkcji poczty e-mail i kalendarza hello w ramach usługi Office 365. 
* Użyj wyzwala toostart do przepływu pracy, gdy istnieje nową wiadomość e-mail po zaktualizowaniu elementu kalendarza i inne.
* Użyj akcji toosend wiadomości e-mail, Utwórz nowe zdarzenie kalendarza i inne. Na przykład, jeśli jest nowy obiekt w usłudze Salesforce (wyzwalacz), Wyślij wiadomość e-mail tooyour programu Outlook pakietu Office 365 (działanie). 

W tym temacie pokazano, jak toouse hello łącznika programu Outlook pakietu Office 365 w aplikacji logiki, a także list hello wyzwalacze i akcje.

> [!NOTE]
> Ta wersja artykułu hello ma zastosowanie tooLogic aplikacji ogólnodostępnej (GA).
> 
> 

toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Połącz tooOffice 365
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi. Połączenie stanowi połączenie między aplikacji logiki i innej usługi. Na przykład tooconnect tooOffice 365 programu Outlook, należy najpierw usługi Office 365 *połączenia*. toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, które mają tooconnect do zwykle jest używana. Dlatego w programie Outlook pakietu Office 365 należy wprowadzić hello poświadczenia tooyour połączenia hello toocreate konta usługi Office 365.

## <a name="create-hello-connection"></a>Utwórz połączenie hello
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Użyć wyzwalacza
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. Wyzwalacze "sondować" hello usługi interwału i częstotliwość. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. W aplikacji logiki hello wpisz "office 365" tooget listę hello wyzwalaczy:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Wybierz **Office 365 Outlook - wkrótce uruchamiając zdarzeń nadchodzących**. Jeśli połączenie już istnieje, wybierz kalendarz, z listy rozwijanej hello.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Jeśli zostanie wyświetlony monit o toosign w, wprowadź znak hello szczegóły toocreate hello połączenia. [Utwórz połączenie hello](connectors-create-api-office365-outlook.md#create-the-connection) w tym temacie przedstawiono kroki hello. 
   
   > [!NOTE]
   > W tym przykładzie aplikacji logiki hello jest uruchamiana po zaktualizowaniu zdarzenia kalendarza. wyniki hello toosee tego wyzwalacza, Dodaj inną akcję, która wysyła do Ciebie wiadomość SMS. Na przykład dodać hello usługi Twilio *wysyła komunikat* akcję, która teksty podczas hello kalendarza zdarzeń jest uruchamiana w ciągu 15 minut. 
   > 
   > 
3. Wybierz hello **Edytuj** przycisk i ustaw hello **częstotliwość** i **interwał** wartości. Na przykład, jeśli chcesz toopoll wyzwalacza hello co 15 minut, następnie ustawić hello **częstotliwość** za**minutę**i ustaw hello **interwał** zbyt**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Zapisz** zmiany (lewym górnym rogu paska narzędzi hello). Aplikację logiki jest zapisywana i automatycznie włączone.

## <a name="use-an-action"></a>Za pomocą akcji
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Wybierz znak plus hello. Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Wybierz **Dodaj akcję**.
3. W polu tekstowym hello wpisz "office 365" tooget listę wszystkich hello dostępne akcje.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. W tym przykładzie wybierz **Office 365 Outlook - Tworzenie kontaktu**. Jeśli połączenie już istnieje, a następnie wybierz hello **identyfikator folderu**, **imię**i inne właściwości:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia. [Utwórz połączenie hello](connectors-create-api-office365-outlook.md#create-the-connection) w tym temacie opisano te właściwości. 
   
   > [!NOTE]
   > W tym przykładzie utworzymy nowy kontakt w programie Outlook pakietu Office 365. Można użyć danych wyjściowych z innego kontaktu hello toocreate wyzwalacza. Na przykład dodać hello SalesForce *podczas tworzenia obiektu* wyzwalacza. Następnie dodaj hello Office 365 Outlook *utworzenie kontaktu* akcję, która używa hello SalesForce pola toocreate hello nowe miejsce nowego kontaktu w usłudze Office 365. 
   > 
   > 
5. **Zapisz** zmiany (lewym górnym rogu paska narzędzi hello). Aplikację logiki jest zapisywana i automatycznie włączone.

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/office365connector/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).

