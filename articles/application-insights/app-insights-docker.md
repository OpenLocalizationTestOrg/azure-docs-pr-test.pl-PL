---
title: "aaaMonitor Docker aplikacji w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Docker liczników wydajności, zdarzeń i wyjątków mogą być wyświetlane w usłudze Application Insights wraz z telemetrii hello z aplikacji hello konteneryzowanych."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Monitorowanie aplikacji Docker w usłudze Application Insights
Zdarzenia cyklu życia i wydajności liczników z [Docker](https://www.docker.com/) kontenerów może być na wykresie na usługi Application Insights. Zainstaluj hello [usługi Application Insights](app-insights-overview.md) obrazu w kontenerze w hoście, a wyświetli liczniki wydajności dla hosta hello oraz jak w przypadku hello inne obrazy.

Z rozwiązaniem Docker, z dystrybucji w kontenerach lekkie ukończone wszystkie zależności aplikacji. By działały na dowolnym komputerze hosta z systemem aparatem platformy Docker.

Po uruchomieniu hello [obrazu usługi Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) na hoście Docker, możesz uzyskać następujące korzyści:

* Cykl życia telemetrii dotyczące wszystkich kontenerów hello uruchomiona na hoście hello — uruchamianie, zatrzymywanie i tak dalej.
* Liczniki wydajności dla wszystkich kontenerów hello. Procesor CPU, pamięci, użycie sieci i inne.
* Jeśli użytkownik [zainstalowany zestaw SDK usługi Application Insights dla języka Java](app-insights-java-live.md) w aplikacji hello w kontenerach hello, wszystkie telemetrii hello tych aplikacji będą miały dodatkowe właściwości hello kontenera i komputera-hosta. Tak na przykład jeśli masz wystąpienie aplikacji uruchomionej w więcej niż jednego hosta, łatwo filtrować telemetrii aplikacji przez hosta.

![Przykład](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Ustawianie zasobu usługi Application Insights
1. Zaloguj się do [portalu Microsoft Azure](https://azure.com) , a następnie otwórz hello zasobu usługi Application Insights dla aplikacji; lub [Utwórz nową](app-insights-create-new-resource.md). 
   
    *Którego zasobu należy użyć?* Jeśli hello aplikacje, które są uruchomione na hoście zostały opracowane przez innego użytkownika, a następnie należy zbyt[utworzyć nowy zasób usługi Application Insights](app-insights-create-new-resource.md). Jest to, gdzie przeglądać i analizować dane telemetryczne hello. (Wybierz Ogólne, dla typu aplikacji hello).
   
    Ale jeśli hello Deweloper aplikacji hello, następnie mamy nadzieję, że możesz [dodaje zestaw SDK usługi Application Insights](app-insights-java-live.md) tooeach z nich. Jeśli są one wszystkich naprawdę składników aplikacji biznesowej, a następnie można skonfigurować ich wszystkich zasobów tooone telemetrii toosend i będzie używać tego samego zasobu toodisplay hello Docker cykl życia i wydajności danych. 
   
    Trzeci scenariusz jest opracowany większość aplikacji hello, że używasz toodisplay oddzielne zasoby ich telemetrii. W takim przypadku należy prawdopodobnie również chcesz toocreate oddzielne zasobu hello danych Docker. 
2. Dodaj hello Docker kafelka: Wybierz **dodać Kafelek**, przeciągnij Kafelek Docker hello z galerii hello, a następnie kliknij przycisk **gotowe**. 
   
    ![Przykład](./media/app-insights-docker/03.png)
3. Kliknij przycisk hello **Essentials** listy rozwijanej i skopiuj hello klucza instrumentacji. Użyj tego hello tootell SDK gdzie toosend jego telemetrii.

    ![Przykład](./media/app-insights-docker/02-props.png)

Zachowanie tego okna przeglądarki przydatną, jak będzie powrocie tooit wkrótce toolook na telemetrii.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Uruchom monitor usługi Application Insights hello na hoście
Skoro masz gdzieś toodisplay hello telemetrii, można skonfigurować hello konteneryzowanych aplikację, która będzie gromadzić i wysłać go.

1. Połącz tooyour Docker hosta. 
2. Edytuj klucz Instrumentacji do tego polecenia, a następnie uruchom go:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Tylko jeden obraz usługi Application Insights jest wymagany na hoście Docker. Jeśli aplikacja jest wdrażana na wielu hostach Docker, następnie powtórz polecenie hello na każdym hoście.

## <a name="update-your-app"></a>Aktualizowanie aplikacji
Jeśli aplikacja jest instrumentowane przy użyciu hello [zestaw SDK usługi Application Insights dla języka Java](app-insights-java-get-started.md), Dodaj powitania po wierszu do pliku ApplicationInsights.xml hello w projekcie, w obszarze hello `<TelemetryInitializers>` elementu:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Spowoduje to dodanie Docker informacje, takie jak kontener i hosta tooevery telemetrii elementu identyfikatora wysyłane z aplikacji.

## <a name="view-your-telemetry"></a>Wyświetlanie telemetrii
Przejdź wstecz tooyour zasobu usługi Application Insights w hello portalu Azure.

Kliknij Kafelek Docker hello.

Wkrótce zobaczysz danych otrzymywanych z aplikacji Docker hello, zwłaszcza, jeśli masz inne kontenery zasilany z aparatem platformy Docker.

Poniżej przedstawiono niektóre hello widoków, które można pobrać.

### <a name="perf-counters-by-host-activity-by-image"></a>Liczniki wydajności przez hosta, działania przez obraz
![Przykład](./media/app-insights-docker/10.png)

![Przykład](./media/app-insights-docker/11.png)

Kliknij dowolną nazwę hosta lub obraz, aby uzyskać więcej szczegółów.

toocustomize hello widok, kliknij dowolnego wykresu, nagłówek siatki hello, lub użyj Dodawanie wykresu. 

[Dowiedz się więcej o Eksploratora metryk](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Zdarzenia kontenera docker
![Przykład](./media/app-insights-docker/13.png)

tooinvestigate poszczególne zdarzenia, kliknij [wyszukiwania](app-insights-diagnostic-search.md). Wyszukaj i Filtruj toofind hello zdarzenia. Kliknij przycisk tooget żadnych zdarzeń więcej szczegółów.

### <a name="exceptions-by-container-name"></a>Wyjątki według nazwy kontenera
![Przykład](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Kontekst docker dodane tooapp telemetrii
Dane telemetryczne żądania wysyłane z aplikacji hello Instrumentacji z zestawem SDK AI, wzbogaconych Docker kontekstu:

![Przykład](./media/app-insights-docker/16.png)

Liczniki wydajności dostępnej pamięci i czasu procesora wzbogacone i pogrupowane według nazwy kontenera Docker:

![Przykład](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Pytania i odpowiedzi
*Co to oznacza usługi Application Insights udzielenia mnie, który nie może odczytać Docker?*

* Szczegółowy podział liczniki wydajności przez kontener i obrazów.
* Integrowanie aplikacji i kontenera danych na jednym pulpicie nawigacyjnym.
* [Eksportuj dane telemetryczne](app-insights-export-telemetry.md) dla dalszego analizy tooa bazy danych usługi Power BI lub innymi pulpitu nawigacyjnego.

*Jak uzyskać dane telemetryczne z aplikacji hello?*

* Zainstaluj zestaw SDK usługi Application Insights hello w aplikacji hello. Dowiedz się, jak dla: [aplikacje sieci web Java](app-insights-java-get-started.md), [aplikacji sieci web systemu Windows](app-insights-asp-net.md).

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki

* [Application Insights dla języka Java](app-insights-java-get-started.md)
* [Usługa Application Insights dla środowiska Node.js](app-insights-nodejs.md)
* [Application Insights dla platformy ASP.NET](app-insights-asp-net.md)
