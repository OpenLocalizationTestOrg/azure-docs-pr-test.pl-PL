---
title: "aaaGet pracę z Skalowanie automatyczne według metryki niestandardowe na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale zasobu według metryki niestandardowe na platformie Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Rozpoczynanie pracy z Skalowanie automatyczne według metryki niestandardowe na platformie Azure
W tym artykule opisano sposób tooscale zasobu przez niestandardowa Metryka w portalu Azure.

Azure automatyczne skalowanie monitora dotyczy tylko tooVirtual zestawy skalowania maszyny (VMSS), usługi w chmurze, planów usługi aplikacji i środowiska usługi app service. 

# <a name="lets-get-started"></a>Umożliwia wprowadzenie
W tym artykule założono, że aplikacja sieci web z usługą application insights skonfigurowany. Jeśli nie masz już, możesz [skonfiguruj usługę Application Insights dla witryny sieci Web ASP.NET][1]

- Otwórz [portalu Azure][2]
- Kliknij ikonę monitora Azure w okienku nawigacji po lewej stronie powitania.
  ![Uruchom Azure Monitor][3]
- Ustawienie tooview wszystkie zasoby hello, dla których automatycznego skalowania ma zastosowanie, wraz z jego bieżącym stanie skalowania automatycznego skalowania automatycznego, kliknij polecenie ![odnajdywanie automatyczne skalowanie w Monitorze systemu Azure][4]
- Otwarcie bloku "Skalowania automatycznego" w monitorze Azure i wybierz zasób ma tooscale
> Uwaga: hello czynności użyć plan usługi aplikacji skojarzonych z aplikacji sieci web, który ma skonfigurowane insights aplikacji.
- W bloku Ustawienia skalowania hello hello zasobu należy zauważyć, że bieżąca liczba wystąpień hello jest 1. Kliknij pozycję "Włącz skalowania automatycznego".
  ![Ustawienia skalowania dla nowej aplikacji sieci web][5]
- Podaj nazwę dla ustawienia skalowania hello i hello kliknij "Dodaj regułę". Zwróć uwagę, hello skali reguł opcje, które Otwiera okienko kontekstu w powitania po prawej stronie. Domyślnie ustawia tooscale opcji hello wystąpienia liczba przez 1, jeśli percetage Procesora hello zasobu hello przekracza 70%. Zmień hello metryki źródło u góry hello zbyt "Usługi Application Insights", wybierz hello aplikacji zasobu wgląd w listy rozwijanej "Resource" hello i hello wybierz opcję Niestandardowa Metryka oparte na których ma być tooscale.
  ![Skalować według metryki niestandardowe][6]
- Podobne krok toohello powyżej, Dodaj regułę Skala będzie skalować w i zmniejszyć liczby skali hello, 1, jeśli niestandardowa Metryka hello jest poniżej wartości progowej.
  ![Oparte na procesorze skali][7]
- Ustaw hello wystąpienia limity. Na przykład, jeśli chcesz tooscale między wystąpieniami 2-5, w zależności od fluktuacji metryki niestandardowe hello, ustaw "minimalna" za "2", "maksymalna" za "5" i "default" zbyt 2
> Uwaga: W przypadku, gdy istnieje problem z odczytem hello zasobu metryki i jest obecna pojemność hello poniżej pojemności domyślnej hello, następnie tooensure hello dostępność zasobów hello automatycznego skalowania zostanie skalowanie w poziomie toohello wartości domyślnej. Jeśli obecna pojemność hello już jest wyższa niż pojemności domyślnej, skalowania automatycznego nie będzie skalować w.
- Kliknij przycisk "Zapisz"

Gratulacje. Możesz teraz został pomyślnie utworzony z tooauto ustawienie skali skalowanie aplikacji sieci web, w oparciu metryki niestandardowe.

> Uwaga: hello te same kroki są stosowane tooget uruchomiony w roli usługi VMSS lub w chmurze.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
