---
title: "Konserwacja aaaPredictive wstępnie skonfigurowane rozwiązanie | Dokumentacja firmy Microsoft"
description: "Opis konserwacji predykcyjnej pakiet IoT Azure hello wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Omówienie wstępnie skonfigurowanego rozwiązania konserwacji predykcyjnej

Witaj *konserwacji predykcyjnej* [wstępnie skonfigurowane rozwiązanie] [ lnk_preconfigured_solutions] jest jednym z hello [pakiet IoT Microsoft Azure] [ lnk_iot_suite] wstępnie rozwiązania. To rozwiązanie obejmuje zbieranie danych telemetrycznych z urządzeń w czasie rzeczywistym i model predykcyjny utworzony za pomocą usługi [Azure Machine Learning][lnk-machine-learning].

Z pakiet IoT Azure można szybko i łatwo połączyć tooand monitor zasobów i analizowania telemetrii w czasie rzeczywistym w pulpitach nawigacyjnych i wizualizacji. W rozwiązaniu konserwacji predykcyjnej hello hello pulpitów nawigacyjnych i wizualizacji umożliwiają nowe analizy, które można dysków wydajność i zwiększyć przychody strumieni.

## <a name="hello-scenario"></a>Witaj scenariusza

Fabrikam to regionalny przewoźnik lotniczy, ukierunkowany na zapewnienie doskonałej obsługi klientów przy zachowaniu konkurencyjnych cen. Jedną z przyczyn powodujących opóźnienia lotów są kwestie związane z obsługą techniczną samolotów. Dotyczy to w szczególności konserwacji silników. Firma Fabrikam należy unikać błąd aparatu w locie za wszelką cenę regularnie bada jego aparaty i harmonogramy konserwacji zgodnie z planem tooa. Jednak powietrznego przez aparaty nie zawsze nosić hello takie same. Zdarzają się przypadki wykonania prac konserwacyjnych, które nie były konieczne. Co więcej, pojawiają się problemy, które mogą prowadzić do uziemienia danego samolotu, dopóki nie zostanie przeprowadzona konserwacja. Jeśli samolotu znajduje się w lokalizacji gdzie hello techników prawo lub zamiennych nie są dostępne, te problemy mogą być szczególnie kosztowne.

aparaty Hello samolotów firmy są instrumentowane przy użyciu czujników, które monitorują aparat warunków w locie. Firma Fabrikam stosuje hello konserwacji predykcyjnej rozwiązania toocollect hello czujnik dane zebrane podczas transmitowane hello. Po kumulowanych lat aparatu operacyjne i dane awarii analityków danych w firmie Fabrikam mają modelowane hello toopredict sposób pozostała użytkowania (RUL) powietrznego aparatu. Hello model używa korelacji między danymi z czterech hello aparat czujników i zużycia aparatu, który prowadzi tooeventual awarii. Gdy firma Fabrikam nadal tooperform regularne inspekcje tooensure bezpieczeństwa, go teraz używać hello modele toocompute hello RUL dla każdego aparatu po każdym locie. Hello model używa hello dane telemetryczne zebrane z aparaty hello w locie hello. Pozwala to przewidywać przyszłe awarie i odpowiednio wcześniej zaplanować prace konserwacyjne i naprawcze.

> [!NOTE]
> model rozwiązania Hello używa aparatu rzeczywistego zużycia danych.

Przez punkt hello gdy wymagana jest obsługa, Fabrikam można optymalizować koszty tooreduce jego operacji.

Współpraca koordynatorów ds. konserwacji z personelem odpowiedzialnym za rozkład lotów ma na celu:

- Planowanie obsługi toocoincide z samolotu zatrzymywanie w określonej lokalizacji.
- Upewnij się, że czas wystarczający jest dostępna dla hello powietrznego toobe poza eksploatacją bez powodowania przerw w działaniu harmonogramu.
- tooensure techników tooschedule efektywną obsługę powietrznego bez czasu oczekiwania.

Menedżerowie odpowiedzialni za magazyny podzespołów mają dostęp do planów konserwacji, dzięki czemu mogą zoptymalizować zapasy części zamiennych i proces ich zamawiania.

Te działania firmy Fabrikam toominimize powietrznego podstaw czas i zmniejszyć koszty operacyjne, przy równoczesnym zapewnieniu bezpieczeństwa hello osób i zespół ds..

toounderstand jak [pakiet IoT Azure] [ lnk_iot_suite] zapewnia hello możliwości klienci muszą potencjalne hello toorealize konserwacji predykcyjnej, przejrzyj to [infographic] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Jak jest wbudowane rozwiązanie do konserwacji predykcyjnej hello

rozwiązanie Hello używa istniejącego modelu uczenia maszynowego Azure dostępna jako tooshow szablonu te możliwości pracy z telemetrii urządzenia zbieranych za pośrednictwem usługi pakiet IoT. Microsoft opracowała [modelu regresji] [ lnk_regression_model] aparatu powietrznego na podstawie publicznie dostępnych danych<sup>\[1\]</sup>i krok po kroku wskazówki dotyczące sposobu toouse hello modelu.

Hello Azure IoT rozwiązanie do konserwacji predykcyjnej wykorzystuje model regresji hello utworzone na podstawie tego szablonu. Hello model jest wdrożonych w ramach subskrypcji platformy Azure i dostępne za pośrednictwem interfejsu API wygenerowanej automatycznie. rozwiązanie Hello zawiera podzbiór hello testowania dane reprezentujące 4 (całkowita liczba 100) aparaty oraz strumieni danych czujnika hello 4 (of 21 całkowita). Te dane są wystarczające tooprovide dokładne wyniku hello trenowanego modelu.

*\[1\] A. Saxena and K. Goebel (2008). „Turbofan Engine Degradation Simulation Data Set” (Zestaw danych dotyczących symulacji degradacji silnika turbowentylatorowego), repozytorium danych prognostycznych NASA w Ames (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), ośrodek badawczy NASA w Ames, Moffett Field, Kalifornia*

## <a name="get-started-with-predictive-maintenance"></a>Rozpoczynanie pracy z konserwacja predykcyjną

Ten samouczek pokazuje, jak tooprovision hello rozwiązanie do konserwacji predykcyjnej. On również przeprowadzi Cię przez hello podstawowych funkcji hello rozwiązanie do konserwacji predykcyjnej. Wiele z tych funkcji dostępne za pośrednictwem pulpitu nawigacyjnego rozwiązania hello, która wdraża wraz z hello wstępnie skonfigurowane rozwiązanie.

toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.

> [!NOTE]
> Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].

1. Zaloguj się za[azureiotsuite.com] [ lnk-azureiotsuite] poświadczenia konta przy użyciu platformy Azure i kliknij przycisk  **+**  toocreate rozwiązania.
1. Kliknij przycisk **wybierz** hello **konserwacji predykcyjnej** kafelka.
1. W polu **Nazwa rozwiązania** wprowadź nazwę wstępnie skonfigurowanego rozwiązania konserwacji predykcyjnej.
1. Wybierz hello **Region** i **subskrypcji** toouse tooprovision hello rozwiązanie.
1. Kliknij przycisk **Utwórz rozwiązanie** hello toobegin w procesie inicjowania obsługi. Ten proces zwykle trwa kilka minut toorun.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Poczekaj, aż hello inicjowania obsługi administracyjnej toocomplete procesu

1. Kliknij Kafelek hello rozwiązania z **inicjowania obsługi administracyjnej** stanu.
1. Powiadomienie hello **inicjowania obsługi administracyjnej stanów** podczas wdrażania usług platformy Azure w ramach subskrypcji platformy Azure.
1. Po ukończeniu inicjowania obsługi administracyjnej hello zmiany stanu zbyt**gotowe**.
1. Kliknij przycisk hello kafelka toosee hello szczegóły rozwiązania w okienku po prawej stronie powitania. W tym okienku możesz uruchomić hello rozwiązania dostępu i pulpit nawigacyjny hello obszaru roboczego uczenia maszynowego.

> [!NOTE]
> Jeśli wystąpią problemy dotyczące wdrażania rozwiązania hello wstępnie skonfigurowane, przejrzyj [uprawnienia w witrynie azureiotsuite.com hello] [ lnk-permissions] i hello [— często zadawane pytania] [ lnk-faq]. Jeśli hello problemy będą się powtarzać, Utwórz biletu usługi na powitania [portal][lnk-portal].

Czy istnieją szczegółowe informacje można oczekiwać toosee, które nie są wyświetlane dla rozwiązania? Prześlij nam swoje propozycje dotyczące funkcji, korzystając ze strony [User Voice](https://feedback.azure.com/forums/321918-azure-iot) (Opinie użytkowników).

## <a name="view-hello-solution"></a>Wyświetl hello rozwiązanie

Ta sekcja przeprowadzi Cię przez rozwiązanie hello interfejsu użytkownika.

### <a name="predictive-maintenance-dashboard"></a>Pulpit nawigacyjny konserwacji predykcyjnej

Ta strona w aplikacji sieci web hello używa kontrolek JavaScript usługi Power BI (zobacz hello [repozytorium elementów wizualnych usługi Power BI][lnk-powerbi]) toovisualize:

* Witaj danych wyjściowych z zadania usługi analiza strumienia hello w magazynie obiektów blob.
* Witaj RUL i cyklu liczba na powietrznego aparatu.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Obserwowania zachowanie hello hello rozwiązania chmury

W portalu Azure Witaj, przejdź toohello grupy zasobów o nazwie rozwiązania hello wybrano tooview udostępnione zasoby.

![][img-resource-group]

Podczas obsługi administracyjnej hello wstępnie skonfigurowane rozwiązanie otrzymasz wiadomość e-mail z obszaru roboczego uczenia maszynowego toohello łącza. Można także przechodzić obszaru roboczego uczenia maszynowego toohello z hello [azureiotsuite.com] [ lnk-azureiotsuite] strony elastycznie rozwiązania. Kafelek jest dostępne na tej stronie, gdy rozwiązanie hello jest hello **gotowe** stanu.

![][img-machine-learning]

W portalu rozwiązania hello można zauważyć, że z próbką hello jest udostępniane z dwóch powietrznego toorepresent cztery symulowanego urządzenia dwa aparaty na lotniczych, każdy z czterech czujników. Podczas pierwszego przechodzenia toohello rozwiązanie portalu, symulacji hello jest zatrzymana.

![][img-simulation-stopped]

Kliknij przycisk **Start symulacji** toobegin hello symulacji. Witaj historii czujnika, RUL cykle i RUL historii wypełnić hello pulpitu nawigacyjnego.

![][img-simulation-running]

Gdy RUL jest mniejsza niż 160 (dowolnego próg wybrany dla celów demonstracyjnych), portalu rozwiązania hello wyświetla ostrzeżenie symbol toohello dalej, wyświetlić RUL. portal rozwiązania Hello również wyodrębnić hello powietrznego aparat kolorem żółtym. Zwróć uwagę, jak hello RUL wartości mają ogólne trend pobieranej ogólnej, ale mają tendencję toobounce w górę i w dół. To zachowanie jest wynikiem hello różne długości cyklu i hello dokładności modelu.

![][img-simulation-warning]

Pełna symulacji Hello trwa około 35 toocomplete minut 148 cykle. Hello 160 RUL osiągnięty jest próg dla powitania po raz pierwszy po około 5 minut, a oba aparaty trafienie próg hello około 8 minut.

Symulacja Hello jest uruchomiony za pośrednictwem hello pełen zestaw 148 cykle i reguluje na wartości końcowe RUL i cyklu.

Można zatrzymać symulacji hello w dowolnym punkt, ale kliknięcie **Start symulacji** odtworzenie hello symulacji od początku hello hello zestawu danych.

## <a name="next-steps"></a>Następne kroki

więcej informacji na temat sposobu Azure IoT umożliwia scenariuszy konserwacji predykcyjnej, przeczytaj toolearn [przechwytywania wartość z Internetu rzeczy hello][lnk_capture_value].

Podejmij [wskazówki] [ lnk-predictive-walkthrough] hello konserwacji predykcyjnej rozwiązania.

Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]
* [Zabezpieczenia IoT z hello tła w][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/