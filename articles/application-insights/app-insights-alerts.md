---
title: "aaaSet alertów w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Bądź na bieżąco o wydłużają czas odpowiedzi, wyjątków i innych wydajności lub zmiany użycia w aplikacji sieci web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Ustawianie alertów w usłudze Application Insights
[Azure Application Insights] [ start] może generować alerty toochanges w metryki wydajności i użycia w aplikacji sieci web. 

Usługa Application Insights monitoruje aplikację na żywo na [różnymi platformami] [ platforms] toohelp diagnozowanie problemów z wydajnością i poznania wzorców użycia.

Istnieją trzy typy alertów:

* **Alerty metryki** informujące o tym, kiedy metrykę przecina wartość progową dla niektórych okres — takie jak czas reakcji, liczby wyjątków, użycie procesora CPU lub wyświetleń strony. 
* [**Testów sieci Web** ] [ availability] informujące o tym, w których witryna cieszy niedostępna na powitania internet lub wolno odpowiadać. [Dowiedz się więcej][availability].
* [**Proaktywna Diagnostyka** ](app-insights-proactive-diagnostics.md) zostaną skonfigurowane automatycznie toonotify o wydajności nietypowe wzorce.

Możemy skupić się na metryki alertów w tym artykule.

## <a name="set-a-metric-alert"></a>Ustaw metryki alertu
Otwórz hello reguły alertów bloku, a następnie użyj hello przycisk Dodaj. 

![W bloku reguły alertów hello wybierz opcję Dodaj alertu. Ustaw aplikacji hello toomeasure zasobów, podaj nazwę dla alertu hello i wybierz metrykę.](./media/app-insights-alerts/01-set-metric.png)

* Ustaw zasób hello przed hello inne właściwości. **Wybierz zasób hello "(składniki)"** Jeśli chcesz otrzymywać alerty tooset metryki wydajności i użycia.
* Nazwa Hello nadawana toohello alert musi być unikatowa w ramach grupy zasobów hello (nie tylko aplikacji).
* Być dokładne toonote hello jednostki, w których użytkownik jest proszony wartość progowa hello tooenter.
* Po zaznaczeniu pola hello "E-mail właścicieli...", alerty są wysyłane przez tooeveryone poczty e-mail, kto ma dostęp toothis zasobów grupy. tooexpand to zbiór osoby, dodaj je toohello [grupy zasobów lub subskrypcji](app-insights-resources-roles-access-control.md) (nie hello zasobów).
* Jeśli określisz "Dodatkowe wiadomości e-mail" alerty są wysyłane toothose konkretnych osób lub grup (czy zaznaczono pole "e-mail właścicieli..." hello). 
* Ustaw [adresu elementu webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) Jeśli zdefiniowano aplikacji sieci web, który odpowiada tooalerts. Jest to zarówno po aktywowaniu hello alert i po jej usunięciu. (Ale należy pamiętać, że w chwili obecnej, parametry zapytania nie są przekazywane jako właściwości elementu webhook).
* Można wyłączyć lub włączyć hello alertu: wyświetlanie przycisków hello u góry bloku hello hello.

*Nie widzę Alert przycisku Dodaj hello.* 

* Używasz konta organizacyjnego? Można ustawić alerty, właścicielem lub współautorem zasobu aplikacji toothis dostępu. Spójrz na powitania bloku kontroli dostępu. [Więcej informacji na temat kontroli dostępu][roles].

> [!NOTE]
> W bloku alerty hello, widać, że istnieje już zestaw alertu: [proaktywna Diagnostyka](app-insights-proactive-failure-diagnostics.md). alert automatycznego Hello monitoruje jednego określonego metryki, częstość niepowodzeń. O ile zdecydujesz toodisable hello aktywnego alertu nie jest potrzebny tooset alertu na częstość niepowodzeń żądań. 
> 
> 

## <a name="see-your-alerts"></a>Zobacz alerty
Otrzymasz wiadomość e-mail, gdy stan alertu zmiany między stanem nieaktywnym i aktywnym. 

bieżący stan każdego alertu Hello jest wyświetlany w bloku reguły alertów hello.

Brak podsumowanie ostatnią aktywność w alertach hello listy rozwijanej:

![Alerty z listy rozwijanej](./media/app-insights-alerts/010-alert-drop.png)

Witaj historię zmian stanu znajduje się w hello dziennik aktywności:

![W bloku omówienie hello kliknij pozycję Ustawienia, dzienniki inspekcji](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Jak działają alerty
* Alert ma trzy stany: "Nigdy aktywowany", "Aktywny" i "Rozwiązany". Oznacza, że aktywowanego hello została wartość true, gdy ostatniej oceny określony warunek.
* Powiadomienie jest generowany, gdy alert zmieni stan. (Jeśli hello warunku alertu został już wartość true, podczas tworzenia alertu hello, mogą różnić się powiadomienie do momentu warunku hello przechodzi false.)
* Każde powiadomienie generuje wiadomość e-mail, zaznaczone pole wiadomości powitania, czy podany adres e-mail. Można również sprawdzić w listy rozwijanej hello powiadomienia.
* Alert jest obliczane zawsze, gdy dociera metrykę, ale nie w inny sposób.
* Ocena Hello agreguje Metryka hello za pośrednictwem hello poprzedzający okres i porównuje go po toohello próg toodetermine hello nowy stan.
* Możesz wybrać okres Hello Określa interwał powitania, w którym są agregowane metryki. Nie wpływa na częstotliwość hello alertu jest obliczane: to zależy od częstotliwości hello odbioru metryki.
* Jeśli żadne dane dla określonej metryki przez pewien czas, hello przerwa ma efekty różnych na ocenę alertów i na wykresach hello w Eksploratorze metryk. W Eksploratorze metryk Jeśli występuje bez danych przez czas dłuższy niż interwał próbkowania hello wykresu, wykres hello pokazuje wartość 0. Ale alertu opartego na powitania tego samego Metryka to nie jest ponownie oceniane i hello jego stan pozostaje niezmieniona. 
  
    Po odebraniu ostatecznie danych, wykresu hello Przechodzi wstecz tooa wartość inną niż zero. oblicza Hello alertu na podstawie danych hello dostępne dla określonego okresu hello. Hello nowego punktu danych w przypadku hello tylko jeden dostępny w okresie hello, hello agregacji jest oparty tylko na punktu danych.
* Alert można często migotać między Stanami alertów i działa prawidłowo, nawet w przypadku ustawienia długiego okresu. Może to nastąpić, jeśli wartość metryki hello jest przesuwany wokół hello próg. Próg hello jest nie histerezy: hello przejścia tooalert odbywa się na powitania samą wartość jak hello toohealthy przejścia.

## <a name="what-are-good-alerts-tooset"></a>Co to są dobrym alerty tooset?
To zależy od aplikacji. toostart, ma ona najlepszych nie tooset zbyt wiele miar. Należy poświęcić trochę czasu spojrzenie na wykresach metryki uruchomionej aplikacji tooget działanie dla jak działa normalnie. Takie rozwiązanie pomaga znaleźć tooimprove sposobów jego wydajności. Następnie skonfiguruj tootell alerty można po przejściu metryki hello poza strefą normalne hello. 

Alerty popularnych obejmują:

* [Metryki przeglądarki][client], szczególnie przeglądarki **czas ładowania strony**, są odpowiednie dla aplikacji sieci web. Jeśli Twoja strona zawiera wiele skryptów, należy szukać **wyjątki przeglądarki**. W kolejności tooget te metryki i alerty, masz tooset [monitorowania strony sieci web][client].
* **Czas odpowiedzi serwera** po stronie serwera na powitania aplikacji sieci web. A także Konfigurowanie alertów, śledzić tej metryki toosee Jeśli nieproporcjonalnie zależy to żądanie wysokiej szybkości przetwarzania: odmiany może wskazywać, że aplikacja działa poza zasobów. 
* **Wyjątki serwera** -toosee ich niektóre masz toodo [dodatkowe ustawienia](app-insights-asp-net-exceptions.md).

Pamiętaj, że [diagnostyki szybkość niepowodzenia aktywnego](app-insights-proactive-failure-diagnostics.md) automatycznie hello monitor współczynnika jaką aplikacji odpowiada toorequests z kodami awarii. 

## <a name="automation"></a>Automatyzacja
* [Użyj programu PowerShell tooautomate Konfigurowanie alertów](app-insights-powershell-alerts.md)
* [Użyj tooalerts odpowiada tooautomate elementów webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Zobacz też
* [Dostępność testy sieci web](app-insights-monitor-web-app-availability.md)
* [Zautomatyzować konfigurowanie alertów](app-insights-powershell-alerts.md)
* [Proaktywna Diagnostyka](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

