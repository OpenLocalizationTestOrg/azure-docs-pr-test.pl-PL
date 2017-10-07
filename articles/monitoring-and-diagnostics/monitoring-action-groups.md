---
title: "aaaCreate i Zarządzaj grupami akcji w hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate grup działań w hello portalu Azure i zarządzanie nimi."
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Utwórz i Zarządzaj grupami akcji w hello portalu Azure
## <a name="overview"></a>Omówienie ##
W tym artykule opisano sposób toocreate grup działań w hello portalu Azure i zarządzanie nimi.

Można skonfigurować listę akcji przy użyciu grup działań. Te grupy następnie mogą być używane podczas definiowania alertów dotyczących działań w dzienniku. Następnie te grupy mogą być ponownie używane przez każdy alert dziennika aktywności, zdefiniowane przez użytkownika, zapewnienie, że powitalne same akcje podejmowane są zawsze, gdy zostanie wyzwolony alert dziennika aktywności hello.

Grupy akcji może zawierać maksymalnie too10 każdego typu akcji. Każda akcja składa się z hello następujące właściwości:

* **Nazwa**: Unikatowy identyfikator grupy hello akcji.  
* **Typ akcji**: Wyślij wiadomość SMS, Wyślij wiadomość e-mail lub wywołanie elementu webhook.  
* **Szczegóły**: hello odpowiedni numer telefonu, adres e-mail lub identyfikator URI elementu webhook.

Aby uzyskać informacje na temat toouse usługi Azure Resource Manager szablony tooconfigure akcji grupy, zobacz [szablony Menedżera zasobów grupy akcji](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Utwórz grupy akcji, używając hello portalu Azure ##
1. W hello [portal](https://portal.azure.com), wybierz pozycję **Monitor**. Witaj **Monitor** bloku konsoliduje wszystkich monitorowania ustawień i danych w jednym widoku.

    ![Witaj "Monitora" usługi](./media/monitoring-action-groups/home-monitor.png)
2. W hello **dziennik aktywności** zaznacz **grupy akcji**.

    ![Witaj "Akcji grupy" karta](./media/monitoring-action-groups/action-groups-blade.png)
3. Wybierz **Dodaj grupę akcji**i wypełnij pola hello.

    ![Witaj polecenie "Dodaj grupę akcji"](./media/monitoring-action-groups/add-action-group.png)
4. Wprowadź nazwę w hello **nazwy grupy akcji** i wpisz nazwę w hello **krótką nazwę** pole. Krótka nazwa Hello jest używany zamiast akcji pełną nazwę grupy, podczas powiadomienia są wysyłane przy użyciu tej grupy.

      ![okno dialogowe Hello Dodawanie grupy akcji"](./media/monitoring-action-groups/action-group-define.png)

5. Witaj **subskrypcji** polu autofills z Twojej bieżącej subskrypcji. Ta subskrypcja jest hello jedną grupy akcji hello, do której jest zapisywany.

6. Wybierz hello **grupy zasobów** w akcję hello jest zapisywana grupy.

7. Zdefiniuj listę działań, zapewniając każdej akcji:

    a. **Nazwa**: wprowadź unikatowy identyfikator dla tej akcji.

    b. **Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.

    c. **Szczegóły**: oparte na typ akcji hello, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.

8. Wybierz **OK** toocreate hello akcji grupy.

## <a name="manage-your-action-groups"></a>Zarządzanie grupami akcji ##
Po utworzeniu grupy akcji nie jest widoczna hello **grupy akcji** sekcji hello **Monitor** bloku. Wybierz grupę akcji hello, który ma toomanage do:

* Dodawanie, edytowanie lub usuwanie akcji.
* Usuwanie grupy akcji hello.

## <a name="next-steps"></a>Następne kroki ##
* Dowiedz się więcej o [SMS alertów zachowanie](monitoring-sms-alert-behavior.md).  
* Uzyskaj [zrozumienia schemat alertu elementu webhook dziennika aktywności hello](monitoring-activity-log-alerts-webhook.md).  
* Dowiedz się więcej o [limitów szybkości](monitoring-alerts-rate-limiting.md) alertów. 
* Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i Dowiedz się, jak tooreceive alertów.  
* Dowiedz się, jak za[skonfigurować alerty, gdy powiadomienie usługi kondycji jest przesyłana](monitoring-activity-log-alerts-on-service-notifications.md).
