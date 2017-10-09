---
title: aaaOverview metryk w Microsoft Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak monitorowanie toocustomize wykresy na platformie Azure."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Omówienie metryk w Microsoft Azure
Wszystkie usługi Azure śledzić kluczowych metryk, które pozwalają toomonitor hello kondycji, wydajności, dostępności i użyciu usług. Te metryki można wyświetlić w portalu Azure hello i umożliwia także hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931930.aspx) lub [zestawu .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello pełny zestaw metryki programowo.

W przypadku niektórych usług może być konieczne tooturn diagnostykę w kolejności toosee wszystkie metryki. Dla innych użytkowników, takich jak maszyny wirtualne otrzymasz podstawowego zestawu metryki, ale należy tooenable hello metryki wysokiej częstotliwości pełnego zestawu. Zobacz [włączania monitorowania i diagnostyki](insights-how-to-use-diagnostics.md) toolearn więcej.

## <a name="using-monitoring-charts"></a>Przy użyciu monitorowania wykresów
Można dowolną metryki hello wykresu je w dowolnym okresie możesz wybrać.

1. W hello [Azure Portal](https://portal.azure.com/), kliknij przycisk **Przeglądaj**, i następnie zasobu interesuje Cię monitorowania.
2. Witaj **monitorowanie** sekcja zawiera hello najważniejszych metryk dla każdego z zasobów platformy Azure. Na przykład aplikacja sieci web ma **żądań i błędów**, gdzie jako maszynę wirtualną, musi **procent użycia procesora CPU** i **odczytu i zapisu dysku**: ![obiektyw monitorowanie](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Kliknięcie dowolnego wykresu, zostaną wyświetlone zostanie hello **Metryka** bloku. W bloku hello wykres toohello jest ponadto jest tabela przedstawiająca agregacji metryki hello (na przykład średnią, minimalną i maksymalną, za pośrednictwem hello zakres czasu, którą wybrano). Poniżej są hello reguły alertów dla zasobu hello.
    ![Metryki bloku](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. toocustomize hello wierszy, które są wyświetlane, kliknij przycisk hello **Edytuj** znajdującego się na wykresie hello lub hello **Edytuj wykres** polecenia w bloku metryki hello.
5. W bloku Edytuj zapytanie hello należy wykonać trzy czynności:
   
   * Zmień zakres czasu hello
   * Przełącz wygląd hello między pasek i linia
   * Wybierz inną metics ![edytowanie zapytań](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Zmienić zakres czasowy hello jest tak proste, jak wybranie innego zakresu (takie jak **ostatniej godziny**) i kliknięcie **zapisać** u dołu hello hello bloku. Można również wybrać **niestandardowe**, co pozwala toochoose ka¿dy okres za pośrednictwem hello ostatnich 2 tygodni. Można na przykład zobacz hello całego dwa tygodnie lub po prostu 1 godziny od wczoraj. Wpisz tooenter pole tekstowe hello inną godzinę.
    ![Zakres czasu niestandardowych](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Poniżej hello zakres czasu kanał można wybrać dowolną liczbę tooshow metryki na wykresie hello.
8. Po kliknięciu przycisku Zapisz zmiany zostaną zapisane dla tego zasobu. Na przykład jeśli masz dwie maszyny wirtualne, a w przypadku zmiany wykresu w jednym, nie wpłynie ono hello innych.

## <a name="creating-side-by-side-charts"></a>Tworzenie wykresów side-by-side
Dostosowywanie zaawansowane hello w portalu hello można dodawać wykresy dowolną liczbę można dowolnie.

1. W hello **...**  menu u góry kliknij bloku hello hello **Dodaj Kafelki**:  
    ![Dodawanie Menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Następnie możesz wybierz wybrać wykres z hello **galerii** hello prawej strony ekranu: ![galerii](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Jeśli nie widzisz hello metryka ma, można dodać jeden z hello ustawienia metryki, i **Edytuj** hello wykresu tooshow hello metryki, które należy.

## <a name="monitoring-usage-quotas"></a>Monitorowanie wykorzystania przydziały
Większość metryki pokazują trendów w czasie, ale niektóre dane, takie jak przydziały do użycia, są w chwili informacji o progu.

Widoczny jest także użycie przydziały w bloku zasobów, które mają przydziały hello:

![Sposób użycia](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Tak jak w metryki, możesz użyć hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931963.aspx) lub [zestawu .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess pełny zestaw wykorzystania przydziały hello programowo.

## <a name="next-steps"></a>Następne kroki
* [Odbieranie powiadomień o alertach](insights-receive-alert-notifications.md) po każdej zmianie metryki przekracza próg.
* [Włączanie monitorowania i diagnostyki](insights-how-to-use-diagnostics.md) toocollect szczegółowe metryki wysokiej częstotliwości w usłudze.
* [Automatyczne skalowanie liczby wystąpień](insights-how-to-scale.md) toomake się, że usługa jest dostępna i elastyczny.
* [Monitorowanie wydajności aplikacji](../application-insights/app-insights-azure-web-apps.md) Jeśli toounderstand dokładnie, jak kod działa w chmurze hello.
* Użyj [usługi Application Insights dla aplikacji JavaScript i stron sieci web](../application-insights/app-insights-web-track-usage.md) tooget analytics klienta o hello przeglądarek, które strony sieci web.
* [Monitorowanie dostępności i czasu odpowiedzi dowolnej strony sieci web](../application-insights/app-insights-monitor-web-app-availability.md) z usługi Application Insights, można sprawdzić, czy strony nie działa.

