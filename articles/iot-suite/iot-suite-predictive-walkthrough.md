---
title: "Przewodnik obsługi aaaPredictive | Dokumentacja firmy Microsoft"
description: "Przewodnik hello Azure IoT — konserwacja predykcyjna wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Przewodnik po wstępnie skonfigurowanym rozwiązaniu konserwacji predykcyjnej

Witaj konserwacji predykcyjnej wstępnie skonfigurowane rozwiązanie to rozwiązanie na trasie dla scenariusza biznesowego, który prognozuje punktu hello jaką awarii jest prawdopodobnie toooccur. To wstępnie skonfigurowane rozwiązanie można aktywnie wykorzystać w celu zoptymalizowania konserwacji. rozwiązanie Hello łączy klucza usług pakiet IoT Azure, takich jak Centrum IoT, Stream analytics i [usługi Azure Machine Learning] [ lnk-machine-learning] obszaru roboczego. Ten obszar roboczy zawiera model, na podstawie zestawu danych przykładowych publiczny, hello toopredict pozostała użytkowania (RUL) aparatu powietrznego. rozwiązanie Hello pełni implementuje scenariusza biznesowego IoT hello jako punkt początkowy dla tooplan możesz i wdrożyć rozwiązanie, który spełnia wymagania firmy.

## <a name="logical-architecture"></a>Architektura logiczna

powitania po diagram przedstawia hello logiczne składniki hello wstępnie skonfigurowane rozwiązanie:

![][img-architecture]

elementy Hello niebieski są udostępniane w regionie hello wdrożonym hello wstępnie skonfigurowane rozwiązanie usług platformy Azure. Wyświetla Hello listę regionów, w którym można wdrożyć hello wstępnie skonfigurowane rozwiązanie na powitania [inicjowania obsługi administracyjnej strony][lnk-azureiotsuite].

Element zielony Hello jest symulowane urządzenie, które reprezentuje aparat powietrznego. Możesz dodatkowe informacje na temat tych urządzeń symulowane w hello następujących sekcji.

Witaj szarego elementy reprezentują składników, które implementują *zarządzania urządzeniami* możliwości. Witaj bieżącej wersji usługi hello konserwacji predykcyjnej wstępnie skonfigurowane rozwiązanie nie udostępniania tych zasobów. toolearn więcej informacji na temat zarządzania urządzeniami można znaleźć toohello [zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Symulowane urządzenia

W rozwiązaniu hello wstępnie symulowane urządzenie reprezentuje aparat powietrznego. rozwiązanie Hello jest administracyjnie dwa aparaty mapowane powietrznego pojedynczego tooa. Każdy aparat emituje cztery typy telemetrii: 9 czujnika, 11 czujnik czujnik 14 i 15 czujnik Podaj hello dane niezbędne do hello Machine Learning model toocalculate hello RUL hello przez aparat. Każde symulowane urządzenie wysyła hello następujące dane telemetryczne wiadomości tooIoT Centrum:

*Liczba cykli*. Cykl reprezentuje ukończony lot o długości od 2 do 10 godzin. W locie hello dane telemetryczne są przechwytywane co pół godziny.

*Dane telemetryczne*. Są cztery czujniki, które reprezentują parametry silnika. czujniki Hello objęty są oznaczone czujnik 9, 11 czujnik czujnik 14 i czujnik 15. Te cztery czujników reprezentują telemetrii wystarczające tooobtain przydatne wyniki z hello RUL modelu. Witaj modelu używanego w hello wstępnie skonfigurowane rozwiązanie jest tworzona na podstawie publicznego zestawu danych, który zawiera dane czujników rzeczywistych aparatu. Aby uzyskać więcej informacji dotyczących sposobu hello model został utworzony na podstawie hello oryginalnego zestawu danych, zobacz hello [Cortana Intelligence galerii predykcyjnej konserwacji szablonu][lnk-cortana-analytics].

urządzenia Hello symulowane może obsłużyć hello następujące polecenia wysyłane z Centrum IoT hello w rozwiązaniu hello:

| Polecenie | Opis |
| --- | --- |
| StartTelemetry |Formanty hello stanu hello symulacji.<br/>Urządzenie hello rozpoczyna wysyłanie danych telemetrycznych |
| StopTelemetry |Formanty hello stanu hello symulacji.<br/>Zatrzymuje hello urządzenia wysyłania danych telemetrycznych |

Usługa IoT Hub udostępnia potwierdzenia poleceń wysyłanych do urządzeń.

## <a name="azure-stream-analytics-job"></a>Zadanie usługi Azure Stream Analytics

**Zadanie: Telemetrii** działa na powitania urządzenia telemetrii strumienia przychodzącego dwie instrukcje using:

* Hello najpierw wybiera wszystkie dane telemetryczne z urządzeń hello i wysyła ten tooblob pamięci masowej. W tym miejscu jest wizualizowane w hello aplikacji sieci web.
* Hello drugi oblicza średnią czujnik wartości na metodzie przesuwanego okna dwuminutowego i wysyła te dane za pośrednictwem tooan Centrum zdarzeń hello **procesora zdarzeń**.

## <a name="event-processor"></a>Procesor zdarzeń
Witaj **hosta procesora zdarzeń** uruchamia zadanie sieci Web platformy Azure. Witaj **procesora zdarzeń** przyjmuje wartości średnia czujnik hello cykl ukończone. Następnie przekazuje te wartości tooan interfejsu API, który udostępnia uczonego modelu toocalculate hello RUL przez aparat. Witaj interfejsu API jest udostępniany przez obszaru roboczego uczenia maszynowego, który jest udostępniony w ramach rozwiązania hello.

## <a name="machine-learning"></a>Usługa Machine Learning
składnik uczenia maszynowego Hello używa modelu pochodzi od danych zbieranych z aparaty powietrznego rzeczywistych. Można przejść obszaru roboczego uczenia maszynowego toohello z kafelka hello na powitania [azureiotsuite.com] [ lnk-azureiotsuite] strony elastycznie rozwiązania. Witaj kafelka jest dostępna, gdy rozwiązanie hello jest hello **gotowe** stanu.


## <a name="next-steps"></a>Następne kroki
Skoro już znasz hello najważniejsze składniki hello konserwacji predykcyjnej wstępnie rozwiązania, może być toocustomize go. Zobacz [Przewodnik dostosowywania wstępnie skonfigurowanych rozwiązań][lnk-customize].

Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]
* [Zabezpieczenia IoT z hello tła w][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/