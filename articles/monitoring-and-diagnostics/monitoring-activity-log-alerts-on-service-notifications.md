---
title: "aaaReceive działania dziennika alerty w przypadku powiadomień dotyczących usługi | Dokumentacja firmy Microsoft"
description: "Otrzymuj powiadomienia za pomocą programu SMS, wiadomości e-mail lub elementu webhook w przypadku wystąpienia usługi Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Utwórz działanie alertów dziennika na powiadomień usługi
## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooset dziennika aktywności alerty dla powiadomień o kondycji usługi za pomocą hello portalu Azure.  

Użytkownik otrzyma alert, gdy Azure wysyła tooyour powiadomienia o kondycji usługi subskrypcji platformy Azure. Można skonfigurować alerty hello na podstawie:

- Klasa Hello powiadomienia kondycji usługi (zdarzenia konserwacji, informacje, itp.).
- Hello usług, których to dotyczy.
- Witaj regionów, w których to dotyczy.
- Stan Hello hello powiadomienia (aktywny lub rozwiązany).
- poziom Hello hello powiadomienia (błąd informacyjny, ostrzeżenie,).

Można także skonfigurować kogo wysyłane hello alertu:

- Wybierz istniejącą grupę akcji.
- Utwórz nową grupę akcję (która może służyć do następnych alertów).

toolearn więcej informacji na temat grup akcji, zobacz [Utwórz i Zarządzaj grupami akcji](monitoring-action-groups.md).

Aby uzyskać informacji na temat sposobu powiadomienia kondycji usługi tooconfigure alerty przy użyciu szablonów usługi Azure Resource Manager, zobacz [szablonów Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Utwórz alert na powiadomienia kondycji usługi dla nowej grupy akcji przy użyciu hello portalu Azure
1. W hello [portal](https://portal.azure.com), wybierz pozycję **Monitor**.

    ![Witaj "Monitora" usługi](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. W hello **dziennik aktywności** zaznacz **alerty**.

    ![Karta "Alertów" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Wybierz **alert dziennika aktywności Dodaj**, a następnie wypełnij pola hello.

    ![Witaj polecenie "Dodaj alert dziennika aktywności"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Wprowadź nazwę w hello **nazwa alertu dziennika aktywności** polu i podaj **opis**.

    ![okno dialogowe "Dodaj alert dziennika aktywności" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Witaj **subskrypcji** polu autofills z Twojej bieżącej subskrypcji. Ta subskrypcja jest alert dziennika aktywności hello toosave używane. zasób alertu Hello jest wdrożone toothis subskrypcji i monitory zdarzeń w dzienniku aktywności hello dla niego.

6. Wybierz hello **grupy zasobów** w których hello alertu zasób został utworzony. Nie jest to hello grupy zasobów, które monitorują hello alertu. Zamiast tego jest hello grupy zasobów, gdzie znajduje się zasób alertu hello.

7. W hello **kategorii zdarzeń** wybierz opcję **kondycja usługi**. Opcjonalnie wybierz hello **usługi**, **Region**, **typu**, **stan**, i **poziom** usługi powiadomienia o kondycji, które mają tooreceive.

8. W obszarze **alertów za pośrednictwem**, wybierz pozycję hello **nowy** przycisku grupy akcji. Wprowadź nazwę w hello **nazwy grupy akcji** i wpisz nazwę w hello **krótką nazwę** pole. Krótka nazwa Hello odwołuje się do hello powiadomienia, które są wysyłane po zgłoszeniu tego alertu.

9. Zdefiniuj listy odbiorców zapewniając odbiornika hello:

    a. **Nazwa**: Wprowadź nazwę odbiornika hello, alias lub identyfikator.

    b. **Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.

    c. **Szczegóły**: oparte na wybrany typ akcji hello, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.

10. Wybierz **OK** toocreate hello alertu.

W ciągu kilku minut hello alert jest aktywny i rozpoczyna się tootrigger na podstawie hello warunków, które zostały określone podczas tworzenia.

Aby uzyskać informacje na powitania schematu elementu webhook dla alertów dotyczących działań w dzienniku, zobacz [elementów Webhook dla działania Azure rejestrowania alertów](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>Grupa akcji Hello zdefiniowane w tych kroków znajduje się do ponownego użycia istniejącej grupy akcji dla wszystkich przyszłych definicji alertu.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Utwórz alert na powiadomienia usługi kondycji dla istniejącej grupy akcji przy użyciu hello portalu Azure

1. Wykonaj kroki od 1 do 7 w hello poprzedniej sekcji toocreate powiadomienia usługi kondycji. 

2. W obszarze **alertów za pośrednictwem**, wybierz pozycję hello **istniejące** przycisku grupy akcji. Wybierz grupę odpowiednią akcję hello.

3. Wybierz **OK** toocreate hello alertu.

W ciągu kilku minut hello alert jest aktywny i rozpoczyna się tootrigger na podstawie hello warunków, które zostały określone podczas tworzenia.

## <a name="manage-your-alerts"></a>Zarządzanie alertami

Po utworzeniu alertu nie jest widoczna hello **alerty** sekcji hello **Monitor** bloku. Wybierz alert hello, który ma toomanage do:

* Czy chcesz go edytować.
* Usuń go.
* Wyłączone lub włączone, jeśli chcesz zatrzymać tootemporarily lub wznowić odbieranie powiadomień o alercie hello.

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [usługi powiadomień o kondycji](monitoring-service-notifications.md).
- Dowiedz się więcej o [limitów szybkości powiadomień](monitoring-alerts-rate-limiting.md).
- Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md).
- Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i Dowiedz się, jak tooreceive alertów. 
- Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).
