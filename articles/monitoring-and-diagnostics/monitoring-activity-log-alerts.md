---
title: "alerty dziennika aktywności aaaCreate | Dokumentacja firmy Microsoft"
description: "Otrzymasz powiadomienie w wiadomości SMS, webhook i wiadomości e-mail po wystąpieniu określonego zdarzenia w dzienniku aktywności hello."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Utwórz działanie alertów dziennika

## <a name="overview"></a>Omówienie
Alerty dziennika aktywności są alerty, które aktywować po wystąpieniu nowego zdarzenia dziennika działania, który spełnia warunki hello określone w hello alertu. Są one zasobów platformy Azure, dlatego mogą być tworzone za pomocą szablonu usługi Azure Resource Manager. One również może być utworzona, zaktualizowany lub usunięty hello portalu Azure. W tym artykule przedstawiono hello pojęć dotyczących alertów dotyczących działań w dzienniku. Następnie pokaże Ci, jak toouse hello Azure portalu tooset się alert na zdarzenia dziennika aktywności.

Zazwyczaj w celu utworzenia alertów dotyczących działań w dzienniku tooreceive powiadomienia po:

* Określone zmiany zostaną wprowadzone do zasobów w Twojej subskrypcji platformy Azure, często zakresie tooparticular grupy zasobów lub zasobów. Na przykład można toobe powiadomienia w przypadku maszyn wirtualnych w myProductionResourceGroup zostanie usunięty. Lub może być toobe powiadamiani, jeśli wszystkie nowe role są przypisywane tooa użytkownika w ramach subskrypcji.
* Usługa kondycji zdarzenie. Usługa kondycji zdarzenia zawierają zgłaszania zdarzeń i obsługi zdarzeń tooresources w ramach subskrypcji.

W obu przypadkach alert dziennika aktywności monitoruje tylko w przypadku zdarzeń w subskrypcji hello, w których hello tworzony jest alert.

Możesz skonfigurować alert dziennika działania na podstawie żadnych najwyższego poziomu właściwości w obiekcie JSON hello zdarzenia dziennika aktywności. Jednak portalu hello przedstawia najbardziej typowe opcje hello:

- **Kategoria**: administracyjne, usługa kondycji, skalowania automatycznego i zalecenia. Aby uzyskać więcej informacji, zobacz [omówienie dziennik aktywności platformy Azure hello](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn więcej informacji na temat zdarzenia kondycji usługi, zobacz [odbierzesz alerty dziennika działania dotyczące powiadomień dotyczących usługi](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Grupa zasobów**
- **Zasób**
- **Typ zasobu**
- **Nazwa operacji**: Nazwa operacji hello kontroli dostępu opartej na roli Menedżera zasobów.
- **Poziom**: hello poziom ważności zdarzenia hello (pełne, informacyjny, ostrzeżenie, błąd lub krytyczny).
- **Stan**: hello stan hello zdarzeń, zwykle uruchomiona, nie powiodło się lub zakończyło się pomyślnie.
- **Zdarzenie inicjowane przez**: hello znanej także jako "wywołującego." adres e-mail Hello lub identyfikator hello użytkownika, który wykonał operację hello Azure Active Directory.

>[!NOTE]
>Należy określić co najmniej dwóch hello poprzedzające kryteria alertu o jeden jest hello kategorii. Nie można utworzyć alertu, który uaktywnia każdorazowego zdarzenie jest tworzone w dziennikach działania hello.
>
>

Po aktywowaniu alert dziennika aktywności używa akcji grupy toogenerate akcje lub powiadomienia. Grupy akcji jest zestawem wielokrotnego użytku odbiorców powiadomień, takie jak adresy e-mail, numerów telefonów adresy URL elementu webhook lub wiadomości SMS. odbiorniki Hello mogą być przywoływane z wielu toocentralize alertów i grupy kanałów powiadomień. Podczas definiowania alertu dziennika aktywności, dostępne są dwie opcje. Możesz:

* Użyj istniejącej grupy działań w alertu dziennika aktywności. 
* Utwórz nową grupę akcji. 

toolearn więcej informacji na temat grup akcji, zobacz [Utwórz i Zarządzaj grupami akcji w portalu Azure hello](monitoring-action-groups.md).

toolearn więcej informacji na temat powiadomień o kondycji usługi, zobacz [odbierzesz alerty dziennika działania dotyczące powiadomień o kondycji usługi](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Utwórz alert na zdarzenie dziennika działania z nową grupą akcji przy użyciu hello portalu Azure
1. W hello [portal](https://portal.azure.com), wybierz pozycję **Monitor**.

    ![Witaj "Monitora" usługi](./media/monitoring-activity-log-alerts/home-monitor.png)
2. W hello **dziennik aktywności** zaznacz **alerty**.

    ![Karta "Alertów" Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Wybierz **alert dziennika aktywności Dodaj**, a następnie wypełnij pola hello.

4. Wprowadź nazwę w hello **nazwa alertu dziennika aktywności** i wybierz **opis**.

    ![Witaj polecenie "Dodaj alert dziennika aktywności"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Witaj **subskrypcji** polu autofills z Twojej bieżącej subskrypcji. Ta subskrypcja jest hello jedną grupy akcji hello, do której jest zapisywany. zasób alertu Hello jest wdrożony toothis subskrypcji i monitory działania zdarzenia dziennika z niego.

    ![okno dialogowe "Dodaj alert dziennika aktywności" Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Wybierz hello **grupy zasobów** w których hello alertu zasób został utworzony. To nie jest hello grupy zasobów, które monitorują hello alertu. Zamiast tego jest hello grupy zasobów, gdzie znajduje się zasób alertu hello.

7. Opcjonalnie wybierz **kategorii zdarzeń** toomodify hello dodatkowe filtry, które są wyświetlane. Zdarzenia administracyjne są następujące filtry hello **grupy zasobów**, **zasobów**, **typu zasobu**, **nazwy operacji**, **Poziom**, **stan**, i **zdarzenie inicjowane przez**. Identyfikuje te zdarzenia, które należy monitorować ten alert.

    >[!NOTE]
    >Należy określić co najmniej jeden z hello poprzedzające kryteria alertu. Nie można utworzyć alertu, który uaktywnia każdorazowego zdarzenie jest tworzone w dziennikach działania hello.
    >
    >

8. Wprowadź nazwę w hello **nazwy grupy akcji** i wpisz nazwę w hello **krótką nazwę** pole. Krótka nazwa Hello jest używany zamiast akcji pełną nazwę grupy, podczas powiadomienia są wysyłane przy użyciu tej grupy.

9.  Zdefiniuj listę działań przez zapewnienie hello akcji:

    a. **Nazwa**: Wprowadź nazwę, alias lub identyfikator akcji hello.

    b. **Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.

    c. **Szczegóły**: oparte na typ akcji hello, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.

10. Wybierz **OK** toocreate hello alertu.

Hello alert zajmuje kilka minut toofully propagacji i stanie się aktywne. Uruchamia go, gdy nowe zdarzenia spełniających kryteria alertu hello.

Aby uzyskać więcej informacji, zobacz [schematu elementu webhook hello omówienie używane w alertach dziennika aktywności](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>Grupa akcji Hello zdefiniowane w tych kroków znajduje się do ponownego użycia istniejącej grupy akcji dla wszystkich przyszłych definicji alertu.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Utwórz alert na działania dziennika zdarzeń dla istniejącej grupy akcji przy użyciu hello portalu Azure
1. Wykonaj kroki od 1 do 7 w hello poprzedniej sekcji toocreate alertu dziennika aktywności.

2. W obszarze **powiadomienia za pośrednictwem**, wybierz pozycję hello **istniejące** przycisku grupy akcji. Wybierz istniejącą grupę akcji z listy hello.

3. Wybierz **OK** toocreate hello alertu.

Hello alert zajmuje kilka minut toofully propagacji i stanie się aktywne. Uruchamia go, gdy nowe zdarzenia spełniających kryteria alertu hello.

## <a name="manage-your-alerts"></a>Zarządzanie alertami

Po utworzeniu alertu jest widoczna w sekcji alerty hello hello Monitor bloku. Wybierz alert hello, który ma toomanage do:

* Czy chcesz go edytować.
* Usuń go.
* Wyłączone lub włączone, jeśli chcesz zatrzymać tootemporarily lub wznowić odbieranie powiadomień o alercie hello.

## <a name="next-steps"></a>Następne kroki
- Pobierz [Przegląd alertów](monitoring-overview-alerts.md).
- Dowiedz się więcej o [limitów szybkości powiadomień](monitoring-alerts-rate-limiting.md).
- Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md).
- Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).  
- Dowiedz się więcej o [usługi powiadomień o kondycji](monitoring-service-notifications.md).
- Utwórz [działania logowania alertu toomonitor wszystkie operacje aparat skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Utwórz [aktywności logowania alertu toomonitor wszystkie operacje w/skali skalowalnych w poziomie skalowania automatycznego nie powiodło się w ramach subskrypcji](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
