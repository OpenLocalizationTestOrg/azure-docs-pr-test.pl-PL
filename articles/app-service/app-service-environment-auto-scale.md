---
title: "aaaAutoscaling i v1 środowiska usługi aplikacji"
description: "Skalowanie automatyczne i środowiska usługi aplikacji"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>V1 Skalowanie automatyczne i środowiska usługi aplikacji

> [!NOTE]
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji.  Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
> 

Środowiska usługi aplikacji Azure obsługuje *Skalowanie automatyczne*. Możesz pule poszczególnych procesów roboczych skalowania automatycznego na podstawie metryk lub harmonogram.

![Opcje automatycznego skalowania puli procesów roboczych.][intro]

Skalowanie automatyczne optymalizuje z wykorzystania zasobów przez automatycznie powiększania i zmniejszanie toofit środowiska usługi aplikacji profilu budżetu i/lub obciążenia.

## <a name="configure-worker-pool-autoscale"></a>Konfigurowanie automatycznego skalowania puli procesu roboczego
Dostęp do funkcji automatycznego skalowania hello z hello **ustawienia** kartę hello puli procesów roboczych.

![Karta Ustawienia hello puli procesów roboczych.][settings-scale]

Z tego miejsca interfejs hello powinna być dobrze znać, ponieważ jest hello planowanie tego samego środowiska, zobacz Kiedy skalować usługę aplikacji. 

![Ustawienia ręcznej skali.][scale-manual]

Można również skonfigurować profil skalowania automatycznego.

![Ustawienia skalowania automatycznego.][scale-profile]

Profile skalowania automatycznego są przydatne tooset limity na skalę. Dzięki temu można mieć wydajności spójne środowisko, ustawiając wartość skalowania dolna granica (1) i ograniczenie wydatków przewidywalną ustawiając górna granica (2).

![Ustawienia skalowania w profilu.][scale-profile2]

Po zdefiniowaniu profilu, można dodać tooscale reguły automatycznego skalowania w górę lub w dół hello liczba wystąpień w puli procesów roboczych hello w zakresie hello zdefiniowane przez profil hello. Reguły skalowania automatycznego są określane na podstawie.

![Reguły skalowania.][scale-rule]

 Wszystkie puli procesów roboczych ani frontonu metryki mogą być używane toodefine reguł skalowania automatycznego. Te metryki są hello, które same metryki, można monitorować na wykresach bloku zasobów hello lub Ustaw alerty dla.

## <a name="autoscale-example"></a>Przykład skalowania automatycznego
Funkcja automatycznego skalowania środowiska usługi aplikacji najlepiej można zilustrowane Instruktaż scenariusza.

W tym artykule opisano wszystkie niezbędne zagadnienia dotyczące powitania po ustawieniu skalowania automatycznego. Witaj artykule przedstawiono hello interakcji, które są dostarczane do odtwarzania po uwzględnieniu Skalowanie automatyczne środowiska usługi aplikacji, które znajdują się w środowisku usługi aplikacji.

### <a name="scenario-introduction"></a>Wprowadzenie do scenariusza
Piotr jest sysadmin w przedsiębiorstwie, który został zmigrowany część obciążenia hello czy zarządza tooan środowiska usługi aplikacji.

Hello jest środowiska usługi aplikacji skonfigurowany toomanual skali w następujący sposób:

* **Zakończenia przód:** 3
* **Proces roboczy puli 1**: 10
* **Proces roboczy puli 2**: 5
* **Proces roboczy puli 3**: 5

Puli procesów roboczych 1 jest używany w przypadku obciążeń produkcyjnych, podczas gdy puli procesów roboczych 2 i 3. puli procesów roboczych służą do zapewniania jakości (QA) i rozwoju obciążeń.

Witaj planów usługi App Service dla odpowiedzi na pytania i deweloperów są skonfigurowane toomanual skali. produkcji Hello planu usługi aplikacji jest ustawiana toodeal tooautoscale z zmian w obciążeń i ruchu.

Piotr jest bardzo zapoznać się z aplikacji hello. Zna, że są godzinach szczytu hello obciążenia między 9:00 i 18:00:00, ponieważ jest z biznesowych aplikacji (LOB), używanego przez pracowników, gdy są one w pakiecie office hello. Użycie spadnie po tym, gdy użytkownicy są wykonywane za ten dzień. Poza godzinami szczytu występuje nadal niektóre obciążenia, ponieważ użytkownicy mają dostęp do aplikacji hello zdalnie za pomocą ich urządzeń przenośnych lub komputerów domowych. do produkcji Hello planu usługi aplikacji jest już skonfigurowana tooautoscale oparte na użycie procesora CPU z hello następujące reguły:

![Ustawienia specyficzne dla aplikacji biznesowych.][asp-scale]

| **Profil skalowania automatycznego — dni tygodnia — plan usługi aplikacji** | **Profil skalowania automatycznego — weekendów — plan usługi aplikacji** |
| --- | --- |
| **Nazwa:** profilu dzień tygodnia |**Nazwa:** weekendowe profilu |
| **Skala przez:** reguły wydajności i harmonogramu |**Skala przez:** reguły wydajności i harmonogramu |
| **Profil:** dni tygodnia |**Profil:** weekendowe |
| **Typ:** cyklu |**Typ:** cyklu |
| **Zakres docelowy:** wystąpień too20 5 |**Zakres docelowy:** wystąpień too10 3 |
| **Liczba dni:** poniedziałek, Wtorek, środę, czwartek i piątek |**Liczba dni:** sobota, niedziela |
| **Czas rozpoczęcia:** 9:00 AM |**Czas rozpoczęcia:** 9:00 AM |
| **Strefa czasowa:** UTC-08 |**Strefa czasowa:** UTC-08 |
|  | |
| **Reguły automatycznego skalowania (Skaluj w górę)** |**Reguły automatycznego skalowania (Skaluj w górę)** |
| **Zasób:** produkcji (środowiska usługi aplikacji) |**Zasób:** produkcji (środowiska usługi aplikacji) |
| **Metryka:** procent użycia procesora CPU |**Metryka:** procent użycia procesora CPU |
| **Operacja:** przekracza 60% |**Operacja:** większe niż 80% |
| **Czas trwania:** 5 minut |**Czas trwania:** 10 minut |
| **Czas agregacji:** średni |**Czas agregacji:** średni |
| **Akcja:** zwiększyć liczbę przez 2 |**Akcja:** zwiększyć liczbę 1 |
| **Chłodny w dół (w minutach):** 15 |**Chłodny w dół (w minutach):** 20 |
|  | |
| **Reguły automatycznego skalowania (skali w dół)** |**Reguły automatycznego skalowania (skali w dół)** |
| **Zasób:** produkcji (środowiska usługi aplikacji) |**Zasób:** produkcji (środowiska usługi aplikacji) |
| **Metryka:** procent użycia procesora CPU |**Metryka:** procent użycia procesora CPU |
| **Operacja:** mniej niż 30% |**Operacja:** mniej niż 20% |
| **Czas trwania:** 10 minut |**Czas trwania:** 15 minut |
| **Czas agregacji:** średni |**Czas agregacji:** średni |
| **Akcja:** zmniejszyć liczbę 1 |**Akcja:** zmniejszyć liczbę 1 |
| **Chłodny w dół (w minutach):** 20 |**Chłodny w dół (w minutach):** 10 |

### <a name="app-service-plan-inflation-rate"></a>Szybkość inflacji planu usługi aplikacji
Planów usługi aplikacji, które są skonfigurowane tooautoscale zrobić maksymalna szybkość na godzinę. Ta stawka można jest obliczana na podstawie wartości hello określone w regule skalowania automatycznego hello.

Opis i obliczanie hello *stawka inflacji planu usługi aplikacji* jest ważne w przypadku automatycznego skalowania środowiska usługi aplikacji, ponieważ nie są natychmiastowe puli procesów roboczych tooa zmiany skali.

Hello stawka inflacji planu usługi aplikacji jest obliczana w następujący sposób:

![Obliczanie stawki inflacji planu usługi aplikacji.][ASP-Inflation]

Oparte na powitania skalowania automatycznego — Skaluj w górę reguły dla profilu dzień tygodnia hello produkcji hello planu usługi aplikacji:

![Szybkość inflacji planu usługi aplikacji — dla dni tygodnia, w oparciu skalowania automatycznego — Skaluj w górę reguły.][Equation1]

W przypadku hello hello skalowania automatycznego — Skaluj w górę reguły dla profilu weekendowe hello produkcji hello planu usługi aplikacji hello formuły czy rozwiązania do:

![Usługi aplikacji szybkość inflacji planu weekendów oparte na skalowania automatycznego — Skaluj w górę reguły.][Equation2]

Ta wartość oblicza się do operacji w dół.

Oparte na powitania skalowania automatycznego — zasada skali w dół profilu dzień tygodnia hello produkcji hello planu usługi aplikacji to będzie wyglądać następująco:

![Szybkość inflacji planu usługi aplikacji — dla dni tygodnia, w oparciu skalowania automatycznego — reguły do skali w dół.][Equation3]

W przypadku hello hello skalowania automatycznego — zasada skali w dół profilu weekendowe hello produkcji hello planu usługi aplikacji hello formuły czy rozwiązania do:  

![Usługi aplikacji szybkość inflacji planu weekendów oparte na skalowania automatycznego — reguły do skali w dół.][Equation4]

produkcji Hello planu usługi aplikacji może zwiększyć maksymalną szybkość osiem wystąpień na godzinę w tygodniu hello i cztery godzinę wystąpienia weekend hello. Można go zwolnić wystąpień maksymalnie cztery godzinę wystąpienia w tygodniu hello i sześciu godzinę wystąpienia podczas weekendów.

Jeśli wiele planów usługi aplikacji są obsługiwane w puli procesów roboczych, masz toocalculate hello *całkowitej szybkości inflacji* jako suma hello szybkość inflacji hello hello wszystkich planów usługi App Service, które są w tej puli procesów roboczych.

![Całkowita liczba inflacji Obliczanie dla wielu planów usługi aplikacji hostowanej w puli procesów roboczych.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Użyj hello usługi aplikacji — planowanie szybkość inflacji toodefine procesu roboczego puli skalowania automatycznego reguły
Proces roboczy puli hostujących planów usługi aplikacji, które są skonfigurowane tooautoscale konieczne można przydzielić bufora pojemności. Bufor Hello umożliwia toogrow operacji skalowania automatycznego hello i zmniejszenie plan usługi aplikacji. Minimalna buforu Hello byłoby hello obliczany całkowitej aplikacji szybkości inflacji Plan usługi.

Ponieważ niektóre tooapply czas operacji skalowania środowiska usługi aplikacji, należy uwzględnić wszelkie zmiany dalszych zmian zapotrzebowania, które może się zdarzyć, gdy trwa operacja skalowania. tooaccommodate tego opóźnienia, firma Microsoft zaleca użycie hello obliczany całkowitej aplikacji szybkości inflacji Plan usługi jako hello minimalna liczba wystąpień, które są dodawane do każdej operacji skalowania automatycznego.

Dzięki tym informacjom Paweł można zdefiniować hello profilów skalowania automatycznego i reguł:

![Reguły profilów skalowania automatycznego na przykład LOB.][Worker-Pool-Scale]

| **Profil skalowania automatycznego — dni tygodnia** | **Profil skalowania automatycznego — weekendów** |
| --- | --- |
| **Nazwa:** profilu dzień tygodnia |**Nazwa:** weekendowe profilu |
| **Skala przez:** reguły wydajności i harmonogramu |**Skala przez:** reguły wydajności i harmonogramu |
| **Profil:** dni tygodnia |**Profil:** weekendowe |
| **Typ:** cyklu |**Typ:** cyklu |
| **Zakres docelowy:** 13 too25 wystąpień |**Zakres docelowy:** wystąpień too15 6 |
| **Liczba dni:** poniedziałek, Wtorek, środę, czwartek i piątek |**Liczba dni:** sobota, niedziela |
| **Czas rozpoczęcia:** 7:00:00 |**Czas rozpoczęcia:** 9:00 AM |
| **Strefa czasowa:** UTC-08 |**Strefa czasowa:** UTC-08 |
|  | |
| **Reguły automatycznego skalowania (Skaluj w górę)** |**Reguły automatycznego skalowania (Skaluj w górę)** |
| **Zasób:** puli procesów roboczych 1 |**Zasób:** puli procesów roboczych 1 |
| **Metryka:** WorkersAvailable |**Metryka:** WorkersAvailable |
| **Operacja:** mniej niż 8 |**Operacja:** mniej niż 3 |
| **Czas trwania:** 20 minut |**Czas trwania:** 30 minut |
| **Czas agregacji:** średni |**Czas agregacji:** średni |
| **Akcja:** zwiększyć liczbę 8 |**Akcja:** zwiększyć liczbę przez 3 |
| **Chłodny w dół (w minutach):** 180 |**Chłodny w dół (w minutach):** 180 |
|  | |
| **Reguły automatycznego skalowania (skali w dół)** |**Reguły automatycznego skalowania (skali w dół)** |
| **Zasób:** puli procesów roboczych 1 |**Zasób:** puli procesów roboczych 1 |
| **Metryka:** WorkersAvailable |**Metryka:** WorkersAvailable |
| **Operacja:** większa niż 8 |**Operacja:** wyższej niż 3 |
| **Czas trwania:** 20 minut |**Czas trwania:** 15 minut |
| **Czas agregacji:** średni |**Czas agregacji:** średni |
| **Akcja:** zmniejszyć liczbę o 2 |**Akcja:** zmniejszyć liczbę 3 |
| **Chłodny w dół (w minutach):** 120 |**Chłodny w dół (w minutach):** 120 |

Hello zakres docelowy zdefiniowaną w profilu hello jest obliczana na podstawie wystąpień minimalna hello zdefiniowany w profilu dla planu usługi aplikacji hello + buforu.

Witaj maksymalny zakres będzie hello sumę wszystkich zakresów maksymalną powitania dla wszystkich planów usługi aplikacji hostowanej w puli procesów roboczych hello.

Hello wzrost liczby hello skali reguł powinien być zestaw tooat przynajmniej 1 X aplikacji usługi planu inflacji stopa skali się.

Zmniejszenie liczby może być dostosowane toosomething między 1/2 X lub 1 X hello szybkość inflacji Plan usługi aplikacji do skalowania w dół.

### <a name="autoscale-for-front-end-pool"></a>Funkcja automatycznego skalowania puli frontonu
Zasady automatycznego skalowania frontonu są prostsze niż dla pule procesów roboczych. Przede wszystkim należy  
Upewnij się, że czas trwania pomiaru hello i czasomierze cooldown hello należy wziąć pod uwagę operacji skalowania dla planu usługi aplikacji nie są natychmiastowe.

W tym scenariuszu Paweł zna tego współczynnik błędów hello zwiększa po interfejsy do 80% wykorzystania Procesora i ustawia wystąpień tooincrease reguły automatycznego skalowania hello w następujący sposób:

![Ustawienia automatycznego skalowania puli frontonu.][Front-End-Scale]

| **Profil skalowania automatycznego — zakończenia przód** |
| --- |
| **Nazwa:** skalowania automatycznego — przodu kończy się |
| **Skala przez:** reguły wydajności i harmonogramu |
| **Profil:** codzienne |
| **Typ:** cyklu |
| **Zakres docelowy:** wystąpień too10 3 |
| **Liczba dni:** codzienne |
| **Czas rozpoczęcia:** 9:00 AM |
| **Strefa czasowa:** UTC-08 |
|  |
| **Reguły automatycznego skalowania (Skaluj w górę)** |
| **Zasób:** puli frontonu |
| **Metryka:** procent użycia procesora CPU |
| **Operacja:** przekracza 60% |
| **Czas trwania:** 20 minut |
| **Czas agregacji:** średni |
| **Akcja:** zwiększyć liczbę przez 3 |
| **Chłodny w dół (w minutach):** 120 |
|  |
| **Reguły automatycznego skalowania (skali w dół)** |
| **Zasób:** puli procesów roboczych 1 |
| **Metryka:** procent użycia procesora CPU |
| **Operacja:** mniej niż 30% |
| **Czas trwania:** 20 minut |
| **Czas agregacji:** średni |
| **Akcja:** zmniejszyć liczbę 3 |
| **Chłodny w dół (w minutach):** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
