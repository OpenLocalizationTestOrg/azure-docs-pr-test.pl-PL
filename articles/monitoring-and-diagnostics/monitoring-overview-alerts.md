---
title: "aaaOverview alertów w monitorze Azure i Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Alerty pozwalają toomonitor metryki zasobów platformy Azure, zdarzenia lub dzienniki i otrzymać powiadomienie, gdy spełniony jest warunek, który określisz."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Co to są alerty na platformie Microsoft Azure?
W tym artykule opisano hello różnych źródeł alertów na platformie Microsoft Azure, jakie są hello celów alertów, ich zalety i jak tooget wprowadzenie do korzystania z nich. Go w szczególności dotyczy tooAzure Monitor, ale udostępnia usługi tooother wskaźniki z alertami, a także. Alerty oferują metodą monitorowania w platformie Azure, które pozwalają warunki tooconfigure nad danymi i stają się powiadomienie, gdy hello warunki są zgodne hello najnowszych danych monitorowania.

## <a name="taxonomy-of-azure-alerts"></a>Taksonomii Azure alertów
Platforma Azure hello następujące warunki toodescribe alertów i ich funkcje:
* **Alert** -definicję kryteria (jeden lub więcej reguł lub warunków), która zostanie aktywowany, gdy spełnione.
* **Aktywne** — Witaj stanu, gdy hello są spełnione kryteria zdefiniowane przez alert.
* **Rozwiązane** — Witaj stanu, gdy hello kryteria zdefiniowane przez alert nie jest już spełniany po wcześniej spełnione.
* **Powiadomienie** — Witaj akcję wykonywaną na podstawie wylogowuje alert aktywację.
* **Akcja** -odbiornik tooa wywołań wysyłane powiadomienia (na przykład wysyłanie wiadomości e-mail adres lub publikowanie adresu URL elementu webhook tooa). Powiadomienia zwykle można wyzwolić wiele akcji.

## <a name="alerts-in-different-azure-services"></a>Alerty w różnych usług platformy Azure
Alerty są dostępne przez kilka Azure monitorowanie usług. Aby uzyskać informacje dotyczące sposobu i czasu toouse tych usług [znajduje się w artykule](./monitoring-overview.md). W tym miejscu jest podział typów alertów hello dostępna na Azure:

| Usługa | Typ alertu | Obsługiwane usługi | Opis |
|---|---|---|---|
| Azure Monitor | [Metryki alertów](./insights-alerts-portal.md) | [Obsługiwane metryki z monitora Azure](./monitoring-supported-metrics.md) | Otrzymasz powiadomienie, gdy wszystkie metryki platformy poziomu spełnia określony warunek (na przykład procesora CPU Wynoszące % na maszynie Wirtualnej jest większa niż 90 dla hello ostatnich 5 minut). |
| Azure Monitor | [Alerty dziennika aktywności](./monitoring-activity-log-alerts.md) | Wszystkie typy zasobów dostępnych w usłudze Azure Resource Manager | Otrzymasz powiadomienie, gdy dowolne nowe zdarzenie w hello [dziennika aktywności platformy Azure](./monitoring-overview-activity-logs.md) pasuje do określonych warunków (na przykład podczas operacji "Usuwanie maszyny Wirtualnej" występuje w myProductionResourceGroup lub nowe zdarzenie kondycji usługi z "Active", jako Stan Hello jest wyświetlany). |
| Application Insights | [Metryki alertów](../application-insights/app-insights-alerts.md) | Toosend tooApplication danych usługi Insights Instrumentacji żadnych aplikacji | Otrzymasz powiadomienie, gdy wszystkie metryki poziomu aplikacji spełnia określony warunek (na przykład czas odpowiedzi serwera jest większa niż 2 sekundy). |
| Application Insights | [Alerty testu sieci Web](../application-insights/app-insights-monitor-web-app-availability.md) | Wszystkie witryny sieci Web zinstrumentowane toosend tooApplication danych usługi Insights | Otrzymasz powiadomienie, gdy dostępność lub czasu odpowiedzi witryny sieci Web jest poniżej oczekiwań. |
| Log Analytics | [Alerty analizy dzienników](../log-analytics/log-analytics-alerts.md) | Wszystkie usługi skonfigurowane toosend danych do analizy dzienników | Otrzymasz powiadomienie, gdy analiza dzienników zapytania wyszukiwania danych metryki i/lub zdarzeń spełnia określone kryteria. |

## <a name="alerts-on-azure-monitor-data"></a>Alerty dotyczące danych monitora Azure
Istnieją dwa typy alertów znajdujące się na nich danych, dostępnej w sklepie Azure Monitor — alerty metryki i alerty dziennik aktywności.

* **Alerty metryki** — ten alert jest wyzwalane po wartości progowej, którą należy przypisać przecina hello wartość określonej metryki. Hello alert generuje powiadomienie, gdy hello alert jest "aktywny" (po przekroczeniu progu hello i spełnieniu warunku alertu hello), a także gdy "Problemu" (po przekroczeniu progu hello ponownie i nie jest spełniony warunek hello). Rosnącym listę dostępne metryki obsługiwane przez Azure monitor, zobacz [listy metryki obsługiwane na monitorze Azure](monitoring-supported-metrics.md).
* **Alerty dziennika aktywności** -przesyłania strumieniowego alertu dziennika, który uaktywnia jest generowane zdarzenie dziennika aktywności, że dopasowań filtrować kryteria, które zostały przypisane. Te alerty mają tylko jeden stan "Aktywować", ponieważ aparat alertów powitania po prostu stosuje hello filtru kryteria tooany nowe zdarzenie. Te alerty mogą być używane toobecome powiadomienie po wystąpieniu nowego zdarzenia kondycji usługi lub gdy użytkownik lub aplikacja wykonuje operację w ramach subskrypcji, na przykład "Usuń maszynę wirtualną".

W przypadku dzienników diagnostycznych danych dostępne za pośrednictwem Monitora Azure zalecamy routingu hello danych do analizy dziennika i przy użyciu alertu analizy dzienników. Witaj Poniższy diagram przedstawia źródeł danych w Azure monitora i, koncepcyjnym, jak może generować alerty znajdujące się na nich danych.

![Opis alertów](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Sposób otrzymywania powiadomień na alert monitora Azure?
W przeszłości Azure alertów z różnych usług używać metod wbudowanych powiadomień. Idąc dalej, Azure Monitor oferuje grupowanie wielokrotnego użytku powiadomienia o nazwie grupy akcji. Grupy akcji określ zestaw odbiorcy powiadomienia — dowolną liczbę adresów e-mail, numerów (SMS) lub adresów URL elementu webhook — uprawnia do zawsze, gdy alert jest aktywny, że odwołania hello grupy akcji, wszystkie odbiorcy powiadomienia. Dzięki temu można tooreuse Grupa odbiorców (na przykład na wywołania odtwarzania listy) przez wiele obiektów alertu. Obecnie tylko alerty dziennik aktywności wykorzystać grupy akcji, ale pracy przy użyciu grup akcji, jak również kilka inne Azure typy alertów.

Grupy akcji powiadomienia są obsługiwane przez firmę tooa adresu URL elementu webhook w dodanie tooemail adresy i numery programu SMS. Dzięki temu automatyzacji i korygowania, na przykład przy użyciu:
    - Element Runbook usługi Azure Automation
    - Azure — funkcja
    - Aplikacja logiki platformy Azure
    - usługi innej firmy

Alerty metryki jeszcze nie należy używać grup akcji. Na poszczególnych metryki alertu można skonfigurować powiadomienia do:
* Wyślij wiadomość e-mail powiadomienia toohello usługi administratora, Administratorzy tooco lub tooadditional adresów e-mail, które określisz.
* Wywołaj element webhook, co pozwala toolaunch automatyzacji dodatkowe akcje.

## <a name="next-steps"></a>Następne kroki
Uzyskaj informacje o regułach alertów i konfigurowanie ich za pomocą:

* Dowiedz się więcej o [metryk](monitoring-overview-metrics.md)
* Skonfiguruj [Metryka alertów za pośrednictwem portalu Azure](insights-alerts-portal.md)
* Skonfiguruj [Metryka alerty programu PowerShell](insights-alerts-powershell.md)
* Skonfiguruj [interfejsu Metryka alerty z wiersza polecenia (CLI)](insights-alerts-command-line-interface.md)
* Skonfiguruj [Metryka alerty monitora Azure interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Dowiedz się więcej o [dziennik aktywności](monitoring-overview-activity-logs.md)
* Skonfiguruj [alerty dziennika aktywności za pośrednictwem portalu Azure](monitoring-activity-log-alerts.md)
* Skonfiguruj [alerty dziennika aktywności za pomocą Menedżera zasobów](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md)
* Dowiedz się więcej o [powiadomień usługi](monitoring-service-notifications.md)
* Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md)
