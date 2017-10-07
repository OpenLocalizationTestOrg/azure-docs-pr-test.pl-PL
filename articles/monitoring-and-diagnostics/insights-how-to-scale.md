---
title: "aaaScale wystąpienia licznika ręcznie lub automatycznie skalowana za pomocą portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale usług Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Skalowanie liczby wystąpień ręcznie lub automatycznie
W hello [Azure Portal](https://portal.azure.com/), możesz ręcznie ustawić hello liczba wystąpień usługi lub można ustawić parametry toohave automatycznie skalować na podstawie zapotrzebowania. Jest to zazwyczaj określonego tooas *skalowanie* lub *skalować w*.

Przed skalowanie na podstawie liczby wystąpień, należy rozważyć, czy skalowania dotyczy **warstwa cenowa** dodanie tooinstance liczba. Różnych warstw cenowych może mieć różne liczby rdzeni i ilości pamięci, a więc będą miały lepszą wydajność w przypadku hello samą liczbę wystąpień (czyli *skalowanie w górę* lub *dół*). W tym artykule szczegółowo omówiono *skalować w* i *limit*.

Możesz skalować w portalu hello i umożliwia także hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931953.aspx) lub [zestawu .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust skalować ręcznie lub automatycznie.

> [!NOTE]
> W tym artykule opisano sposób toocreate jako ustawienie hello Portal pod adresem skalowania automatycznego [http://portal.azure.com](http://portal.azure.com). Ustawienia skalowania automatycznego utworzonych w tym portalu nie może być edytowany hello klasyczny portal ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>Skalowanie ręcznie
1. W hello [Azure Portal](https://portal.azure.com/), kliknij przycisk **Przeglądaj**, następnie przejdź toohello zasobu tooscale, takich jak **planu usługi aplikacji**.
2. Kliknij przycisk **Ustawienia > skalowania w poziomie (plan usługi App Service).**
3. U góry hello hello **skali** bloku widać historii akcji skalowania automatycznego hello usługi.
   
    ![Blok skali](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > Tylko akcje, które są wykonywane przez skalowania automatycznego będą widoczne na tym wykresie. Ręcznie dopasować hello liczba wystąpień, hello zmiany nie zostaną odzwierciedlone na tym wykresie.
   > 
   > 
4. Można ręcznie dostosować numer hello **wystąpień** z suwaka.
5. Kliknij hello **zapisać** polecenie i można będzie skalowany toothat liczba wystąpień niemal natychmiast.

## <a name="scaling-based-on-a-pre-set-metric"></a>Skalowanie w oparciu metryki wstępnie ustawiona
Jeśli chcesz hello liczba wystąpień, Dostosuj tooautomatically w oparciu metryki, wybierz hello Metryka w hello **skalowanie przez** listy rozwijanej. Na przykład w przypadku **planu usługi aplikacji** można skalować przez **procent użycia procesora CPU**.

1. Po wybraniu metrykę otrzymasz suwaka i/lub, tekst pola tooenter hello liczbę wystąpień ma tooscale między:
   
    ![Blok skali z procent użycia procesora CPU](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Funkcja automatycznego skalowania potrwa nigdy nie usługi poniżej lub powyżej hello granice, które można ustawić, bez względu na obciążenie.
2. Po drugie można wybrać zakres docelowy hello hello metryki. Na przykład, jeśli została wybrana opcja **procent użycia procesora CPU**, można ustawić elementu docelowego dla hello średnie wykorzystanie Procesora we wszystkich wystąpieniach hello w usłudze. Skalowanie się stanie, gdy hello średnie wykorzystanie Procesora przekracza maksymalną hello, którą należy zdefiniować, podobnie skali w nastąpi przy każdym średnie wykorzystanie Procesora hello spadnie poniżej hello minimalna.
3. Kliknij przycisk hello **zapisać** polecenia. Skalowania automatycznego sprawdza co kilka toomake minut się, że w hello wystąpienia zakresu i obiekt docelowy dla Twojego metryki. Gdy usługa odbierze dodatkowy ruch, uzyskasz więcej wystąpień bez żadnego działania.

## <a name="scale-based-on-other-metrics"></a>Oparte na inne metryki skalowania
Można skalować na podstawie metryk inne niż ustawienia hello, które są widoczne w hello **skalowanie przez** listy rozwijanej i może nawet ma złożonego zestawu elementów skalowania w poziomie i Skaluj w regułach.

### <a name="adding-or-changing-a-rule"></a>Dodawanie lub zmienianie reguły
1. Wybierz hello **reguły wydajności i harmonogram** w hello **skalowanie przez** listy rozwijanej: ![reguły wydajności](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Jeśli poprzednio skalowania automatycznego na zobaczysz widok hello szczegółowe reguły, które były.
3. tooscale oparte na innym powitania kliknij metryki **Dodaj regułę** wiersza. Możesz również kliknąć jeden z hello istniejących toochange wierszy z Metryka hello poprzednio toohello metryka ma tooscale przez.
   ![Dodaj regułę](./media/insights-how-to-scale/Insights_AddRule.png)
4. Teraz należy tooselect metryki, które chcesz tooscale przez. W przypadku wybierania metrykę istnieje kilka rzeczy tooconsider:
   
   * Witaj *zasobów* Metryka hello pochodzi z. Zwykle to będzie można hello taki sam jak zasobów hello są skalowania. Jednak jeśli chcesz tooscale hello głębokość kolejki magazynu, hello zasób jest hello kolejki tooscale przez.
   * Witaj *Nazwa metryki* samej siebie.
   * Witaj *czasu agregacji* hello metryki. Jest to, jak dane hello jest łączenie za pośrednictwem hello *czas trwania*.
5. Po wybraniu Twoje metryki wybierzesz próg hello Metryka hello i hello operatora. Na przykład można powiedzieć **większe** **80%**.
6. Następnie wybierz pozycję hello akcji, które mają tootake. Istnieje kilka różnych rodzajów akcje:
   
   * Zwiększanie lub zmniejszanie przez — spowoduje to dodanie lub usunięcie hello **wartość** liczba wystąpień, należy zdefiniować
   * Zwiększanie lub zmniejszanie procent — spowoduje to zmianę liczby wystąpień hello przez wartość procentową. Na przykład możesz umieścić 25 w hello **wartość** pola, a jeśli masz obecnie wystąpień 8, 2 zostanie dodany.
   * Zwiększyć lub zmniejszyć za — spowoduje to ustawienie hello wystąpienia licznika toohello **wartość** należy zdefiniować.
7. Ponadto można wybrać chłodzenia — jak długo ta reguła ma czekać po hello poprzedniej skali akcji tooscale ponownie.
8. Po skonfigurowaniu reguły trafień **OK**.
9. Po skonfigurowaniu wszystkich reguł hello ma być czy hello toohit **zapisać** polecenia.

### <a name="scaling-with-multiple-steps"></a>Skalowanie za pomocą wielu kroków
Powyższe przykłady Hello są bardzo proste. Jednak jeśli toobe chcesz bardziej agresywną temat skalowania w górę (lub w dół), możesz nawet dodać skali wielu reguł dla hello takie same metryki. Na przykład można zdefiniować dwa reguł skalowania procent użycia procesora CPU:

1. Skalowanie przez wystąpienie 1, jeśli procent użycia procesora CPU przekracza 60%
2. Skalowanie przez 3 wystąpienia, jeśli procent użycia procesora CPU wynosi powyżej 85%

![Wiele reguł skalowania](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Z tą regułą dodatkowe jeśli obciążenie przekracza 85%, przed akcji skalowania, otrzymasz dwa dodatkowe wystąpienia zamiast jednego.

## <a name="scale-based-on-a-schedule"></a>Skala zgodnie z harmonogramem
Domyślnie podczas tworzenia reguły skalowania zostanie zawsze zastosowana. Można stwierdzić, że po kliknięciu nagłówka profilu hello:

![Profil](./media/insights-how-to-scale/Insights_Profile.png)

Jednak możesz toohave skuteczniejsze skalowanie podczas hello dnia lub tygodnia hello niż na powitania weekend. Można nawet zamknąć usługi całkowicie poza godzinami pracy.

1. toodo tego profilu hello masz, wybierz **cyklu** zamiast **zawsze,** i wybierz polecenie hello razy, które mają hello tooapply profilu.
2. Na przykład toohave profil, który ma zastosowanie w tygodniu hello, w hello **dni** Usuń zaznaczenie pola wyboru Lista rozwijana **sobota** i **niedziela**.
3. profil, który ma zastosowanie podczas hello hello dziennych, ustaw toohave **godzina rozpoczęcia** toohello porę dnia, który ma toostart w.
   
    ![Domyślne cyklu](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. Kliknij przycisk **OK**.
5. Następnie należy tooadd hello profilu mają tooapply w innym czasie. Kliknij przycisk hello **Dodaj profil** wiersza.
    ![Wolne od pracy](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Nazwa nowej, sekundy, profil, na przykład można go wywołać **wyłączone pracy**.
7. Następnie wybierz **cyklu** ponownie i wybierz zakres liczba wystąpień hello ma w tym czasie.
8. Jak hello profil domyślny, wybierz polecenie hello **dni** ma tooapply ten profil do, a hello **godzina rozpoczęcia** w dniu hello.
   
   > [!NOTE]
   > Skalowania automatycznego użyje hello letni reguł dla zależności **strefy czasowej** wybrania. Jednak podczas czasu letniego przesunięcie hello UTC wyświetli przesunięcia podstawowej strefy czasowej hello, nie przesunięcia hello UTC oszczędność czasu letniego.
   > 
   > 
9. Kliknij przycisk **OK**.
10. Teraz, konieczne będzie tooadd niezależnie od zasady można mają tooapply w drugim profilu. Kliknij przycisk **Dodaj regułę**, a następnie można skonstruować hello same reguły mają podczas hello profil domyślny.
    
    ![Dodawanie reguły toooff pracy](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Toocreate się, że oba regułę skalowania w poziomie i skali w, w przeciwnym razie podczas hello liczba wystąpień hello profil zostanie tylko wzrostu (ani zmniejszyć).
12. Na koniec kliknij **zapisać**.

## <a name="next-steps"></a>Następne kroki
* [Monitorowanie metryk usługi](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.
* [Włączanie monitorowania i diagnostyki](insights-how-to-use-diagnostics.md) toocollect szczegółowe metryki wysokiej częstotliwości w usłudze.
* [Odbieraj powiadomienia o alertach](insights-receive-alert-notifications.md) zawsze, gdy wystąpią zdarzenia operacyjne lub metryki przekroczą próg.
* [Monitorowanie wydajności aplikacji](../application-insights/app-insights-azure-web-apps.md) Jeśli toounderstand dokładnie, jak kod działa w chmurze hello.
* [Wyświetl zdarzenia i dziennik aktywności](insights-debugging-with-events.md) toolearn wszystkie czynności, które miało miejsce w usłudze.
* [Monitorowanie dostępności i czasu odpowiedzi dowolnej strony sieci web](../application-insights/app-insights-monitor-web-app-availability.md) z usługi Application Insights, można sprawdzić, czy strony nie działa.

