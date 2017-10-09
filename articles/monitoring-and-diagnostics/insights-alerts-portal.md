---
title: "alerty aaaCreate dla usług Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Gdy są spełnione warunki hello wyzwolenia wiadomości e-mail, powiadomienia, adresy URL witryny sieci Web wywołania (elementy webhook) lub automatyzacji."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>W monitorze Azure tworzyć alerty metryki dla usługi Azure - Azure portal
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [Program PowerShell](insights-alerts-powershell.md)
> * [Interfejs wiersza polecenia](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooset Azure metryki alerty za pomocą hello portalu Azure.   

Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.

* **Wartości metryki** — Witaj alertu wyzwalacze, jeśli wartość hello określonej metryki przecina próg przypisać w żadnym kierunku. Oznacza to, że oba wyzwala kiedy najpierw zostanie spełniony warunek hello i następnie później podczas warunku jest już spełniane.    
* **Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia. więcej informacji na temat alertów dotyczących działań w dzienniku toolearn [kliknij tutaj](monitoring-activity-log-alerts.md)

Można skonfigurować hello metryki toodo alertów po, wyzwala:

* Wyślij administratora usługi toohello powiadomienia e-mail i współadministratorzy
* Wyślij wiadomość e-mail tooadditional wiadomości e-mail, które określisz.
* Wywołanie elementu webhook
* Uruchamia wykonywanie elementów runbook platformy Azure (tylko z hello portalu Azure)

Można skonfigurować i uzyskać informacje na temat metryki reguły alertów za pomocą

* [Witryna Azure Portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [Interfejs wiersza polecenia (CLI)](insights-alerts-command-line-interface.md)
* [Interfejs API REST Azure monitora](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Tworzenie reguły alertu na Metryka z hello portalu Azure
1. W hello [portal](https://portal.azure.com/)planuje się monitorowanie zasobów hello Znajdź i zaznacz go.

2. Wybierz **alerty** lub **reguły alertów** w sekcji monitorowanie hello. Ikona i tekst Hello mogą się nieco różnić dla różnych zasobów.  

    ![Monitorowanie](./media/insights-alerts-portal/AlertRulesButton.png)

3. Wybierz hello **Dodaj alert** poleceń i wypełnij pola hello.

    ![Dodawanie alertu](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. **Nazwa** alertu reguły, a następnie wybierz pozycję **opis**, który pokazuje również w wiadomości e-mail z powiadomieniem.

5. Wybierz hello **Metryka** toomonitor, a następnie wybierz **warunku** i **próg** wartość metryki hello. Również wybrana hello **okres** hello metryki czasu reguły muszą zostać spełnione przed hello wyzwalaczy alertu. Tak na przykład jeśli używasz okres hello "PT5M" i alertu szuka procesora CPU przekracza 80%, hello alert jest wyzwalane po hello procesora CPU było stale powyżej 80% 5 minut. W momencie hello pierwszy wyzwalacz, ponownie uruchamia to, gdy hello Procesora pozostaje poniżej 80% 5 minut. Hello pomiaru Procesora występuje co minutę.   

6. Sprawdź **E-mail właścicieli...**  Jeśli chcesz, aby administratorzy i współadministratorzy toobe pocztą e-mail po hello uruchamiany alertu.

7. Jeśli chcesz, dodatkowe wiadomości e-mail tooreceive powiadomienie, gdy hello alertu, należy dodać je w hello **email(s) dodatkowe administratora** pola. Wiele wiadomości e-mail należy rozdzielić średnikami -  *email@contoso.com;email2@contoso.com*

8. Umieść w prawidłowym identyfikatorem URI w hello **Webhook** pole Jeśli ma ona wywoływana po hello uruchamiany alertu.

9. Jeśli używasz usługi Automatyzacja Azure, możesz wybrać toobe elementu Runbook, uruchom po zgłoszeniu alertu hello.

10. Wybierz **OK** po done toocreate hello alertu.   

W ciągu kilku minut hello alert jest aktywny i wyzwala w sposób opisany wcześniej.

## <a name="managing-your-alerts"></a>Zarządzanie alertami
Po utworzeniu alertu, zostanie ona wybrana oraz:

* Wyświetl wykres przedstawiający hello próg metryki i hello rzeczywistymi wartościami z hello poprzedniego dnia.
* Edytuj lub usuń go.
* **Wyłącz** lub **włączyć** go, jeśli chcesz zatrzymać tootemporarily lub wznowić odbieranie powiadomień dla tego alertu.

## <a name="next-steps"></a>Następne kroki
* [Omówienie monitorowania Azure](monitoring-overview.md) tym hello typy informacji, można zbierać i monitorowania.
* Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).
* Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).
* Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).
* Pobierz [Przegląd dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) i zbieranie szczegółowych metryki wysokiej częstotliwości w usłudze.
* Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.
