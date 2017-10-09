---
title: "aaaAzure omówienie Diagnostyka i monitorowanie sieci szkieletowej usługi | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat monitorowania i diagnostyki dla klastrów, aplikacje i usługi sieć szkieletowa usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Monitorowania i diagnostyki dla sieci szkieletowej usług Azure

Monitorowania i diagnostyki są krytyczne toodeveloping, testowania i wdrażania aplikacji i usług w każdym środowisku. Rozwiązania sieci szkieletowej usług najlepiej podczas planowanie i implementowanie monitorowania i diagnostyki, które pomagają upewnij się, aplikacji i usług działają zgodnie z oczekiwaniami w środowisku projektowym lokalnej lub w środowisku produkcyjnym.

Witaj główne cele monitorowania i diagnostyki są:
* Wykrywanie i diagnozowanie problemów dotyczących sprzętu i infrastruktury
* Wykrywaj problemy związane z oprogramowania i aplikacji, skrócić przestoje związane z usługi
* Podejmowanie świadomych zasobów i zmniejsza zużycie dysku operacje decyzji
* Optymalizowanie aplikacji, usług i infrastruktury
* Generuj informacje biznesowe i zidentyfikuj obszary wymagające poprawy


Witaj ogólnego przepływu pracy, monitorowania i diagnostyki obejmuje trzy kroki:

1. **Generowanie zdarzeń**: zdarzenia (dzienników, śledzenie zdarzeń niestandardowych) w tym infrastruktury hello (klaster), platformy i poziom aplikacji / usługi
2. **Zdarzenie agregacji**: generowanych zdarzeń muszą toobe zbierane i agregowane przed mogą być wyświetlane
3. **Analiza**: zdarzeń muszą toobe wizualizowanego i jest dostępna w niektórych formatu, tooallow analizy i wyświetlania w razie potrzeby

Wiele produktów są dostępne, który obejmuje te trzy obszary i są wolne toochoose różnych technologii dla każdego. Jest ważne toomake się upewnić, że hello różnych elementów roboczych razem toodeliver end-to-end rozwiązanie monitorowania dla klastra.

## <a name="event-generation"></a>Generowanie zdarzeń

Hello pierwszym krokiem w przepływie pracy monitorowania i diagnostyki hello jest tworzenie hello i generowania zdarzeń i dzienniki. Te zdarzenia, dzienników i danych śledzenia są generowane na dwa poziomy: hello warstwy platformy (w tym hello klastra, hello maszyny lub usługi sieć szkieletowa akcji) lub warstwy aplikacji hello (Instrumentacji żadnych dodany do usługi i tooapps wdrożone toohello klastra). Zdarzenia na każdym z tych poziomów są można dostosowywać, chociaż sieci szkieletowej usług zapewniają niektóre Instrumentacji domyślnie.

Przeczytaj więcej na temat [zdarzenia na poziomie platformy](service-fabric-diagnostics-event-generation-infra.md) i [zdarzenia na poziomie aplikacji](service-fabric-diagnostics-event-generation-app.md) toounderstand jaka jest dostępna i jak tooadd dalsze instrumentacji.

Po podejmowania decyzji w sprawie hello rejestrowanie dostawcy, które chcesz toouse, należy toomake się, że dzienniki są agregowane i przechowywane poprawnie.

## <a name="event-aggregation"></a>Agregacja zdarzeń

Do zbierania dzienników hello i zdarzenia generowane przez aplikacje i klastra, zwykle zaleca się używanie [diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md) (zbieranie danych dziennika na podstawie tooagent więcej podobne) lub [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(w procesie zbierania dzienników).

Zbieranie dzienników aplikacji przy użyciu rozszerzenia Azure Diagnostics jest dobra opcja w przypadku usług sieci szkieletowej usług, jeśli hello źródeł dziennika miejsc docelowych nie zmienia się często i istnieje bezpośrednie mapowanie między hello źródeł i ich miejsc docelowych. Przyczyna Hello dla diagnostyki Azure to konfiguruje odbywa się w warstwie usługi Resource Manager hello, więc wymaga wprowadzania istotnych zmian toohello konfiguracji klastra hello ponownego aktualizowania/wdrażania. Ponadto, najlepiej jest wykorzystywany w upewnieniu się, czy dzienniki są przechowywane w innym nieco bardziej trwałego, z którym są one dostępne na różnych platformach analizy. Oznacza to, że kończy się ono są mniej wydajne potoku niż korzystanie z opcji, takich jak EventFlow.

Przy użyciu [EventFlow](https://github.com/Azure/diagnostics-eventflow) umożliwia usług toohave wysyłania dzienników bezpośrednio tooan analizy i wizualizacji platformy i/lub toostorage. Inne biblioteki (ILogger, Serilog itp.) mogą być używane dla hello sam cel, ale EventFlow ma zaletą hello o został zaprojektowany specjalnie z myślą w trakcie dziennika kolekcji i toosupport usługi sieć szkieletowa usług. Jest to prawdopodobnie toohave wiele potencjalnych korzyści:

* Łatwe konfigurowanie i wdrażanie
    * Konfiguracja Hello zbierania danych diagnostycznych jest tylko część hello konfiguracji usługi. Należy zachować łatwe tooalways go "zsynchronizowane" z hello pozostałej części aplikacji hello
    * Dla każdej aplikacji lub na usługi konfiguracji jest łatwo osiągalne
    * Wystarczy dodanie hello odpowiedniego pakietu NuGet i zmianę hello jest skonfigurowanie miejsca docelowe danych za pośrednictwem EventFlow *eventFlowConfig.json* pliku
* Elastyczność
    * Aplikacja Hello może wysyłać dane hello wszędzie tam, gdzie musi toogo, tak długo, jak istnieje biblioteki klienckiej, która obsługuje system przechowywania danych hello docelowe. Można dodać nowych miejsc docelowych pożądane
    * Złożone zasady przechwytywania, filtrowania i agregacja danych może być zaimplementowany.
* Uzyskiwanie dostępu do danych aplikacji toointernal i kontekstu
    * Podsystem diagnostycznych Hello uruchomiony proces aplikacji/usługi hello można łatwo rozszerzyć hello śladów z informacje kontekstowe

Jeden element toonote jest te dwie opcje nie wykluczają oraz podczas tooget możliwe podobne zadania wykonane przy użyciu jednej lub drugiej hello, można również rozsądne okazać dla Ciebie tooset się. W większości sytuacji należy połączenie agenta z kolekcji w trakcie może spowodować tooa bardziej niezawodne, monitorowania przepływu pracy. Hello rozszerzenie Azure Diagnostics (agent) może być ścieżki wybranego poziomu dzienników platformy podczas można używać EventFlow (w trakcie kolekcji) dla poziomu dzienników aplikacji. Po przypadku znalezienia co najlepiej będzie działać dla Ciebie, jest czas toothink o Twojej toobe dane wyświetlane i analizowane.

## <a name="event-analysis"></a>Analiza zdarzeń

Istnieje kilka dużą platformy, które istnieją w rynku powitania po przejściu do analizy toohello i wizualizacja danych monitorowania i diagnostyki. Witaj dwie zalecany to [OMS](service-fabric-diagnostics-event-analysis-oms.md) i [usługi Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) powodu tootheir lepszą integrację z sieci szkieletowej usług, ale również powinien wyglądać na powitania [stosu elastycznych](https://www.elastic.co/products) (szczególnie, gdy rozważane jest uruchomiony klaster w środowisku w trybie offline), [Splunk](https://www.splunk.com/), lub inne platformy swoich preferencji.

Hello najważniejszych dla dowolnej platformy należy wybrać powinna zawierać jak doświadczenia są hello interfejsu użytkownika i badania opcje hello możliwości toovisualize danych i utworzyć czytelny pulpitów nawigacyjnych i hello dodatkowe narzędzia zapewniają tooenhance Twojego Monitorowanie, takie jak automatyczne alerty.

Ponadto platforma toohello wybranej podczas konfigurowania klastra sieci szkieletowej usług jako zasobów platformy Azure, umożliwia również wyświetlenie tooAzure dostępu poza pole monitorowanie dla maszyn, które mogą być przydatne w przypadku dotyczące wydajności i monitorowanie metryki.

### <a name="azure-monitor"></a>Azure Monitor

Można użyć [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor hello wielu zasobów platformy Azure, na których jest zbudowany klastra sieci szkieletowej usług. Zestaw metryki dla hello [zestaw skali maszyny wirtualnej](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) i indywidualnych [maszyn wirtualnych](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) automatycznie są zbierane i wyświetlane w portalu Azure hello. tooview hello zbierane informacje w hello portalu Azure, hello wybierz grupę zasobów, która zawiera hello klastra sieci szkieletowej usług. Następnie zestawu skalowania maszyny wirtualnej wybierz hello, które mają tooview. W hello **monitorowanie** zaznacz **metryki** tooview wykres hello wartości.

![Widok portalu Azure zebranych informacji metryki](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

Wykresy hello toocustomize, wykonaj te instrukcje hello [metryk w Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). Można również tworzyć alerty oparte na tych metryk, zgodnie z opisem w [w monitorze Azure tworzyć alerty dla usług Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Można wysyłać alerty usługi powiadamiania o tooa przy użyciu punkty zaczepienia sieci web, zgodnie z opisem w [skonfigurować haku sieci web na alert metryki Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure Monitor obsługuje tylko jedną subskrypcję. Jeśli potrzebujesz toomonitor wiele subskrypcji, lub jeśli potrzebujesz dodatkowych funkcji [analizy dzienników](https://azure.microsoft.com/documentation/services/log-analytics/), część programu Microsoft Operations Management Suite, przewiduje całościowe rozwiązanie zarządzania zarówno lokalnych i oparte na chmurze infrastruktura. Można przekierować danych z monitora Azure bezpośrednio tooLog Analytics, dzięki czemu metryki i dzienniki dla całego środowiska w jednym miejscu.

## <a name="next-steps"></a>Następne kroki

### <a name="watchdogs"></a>Watchdogs

Programu alarmowego jest oddzielny usługa można obejrzeć kondycji i obciążenie usługi i raportu kondycji dla wszystkich elementów w hierarchii modelu kondycji hello. Może to pomóc zapobiec wystąpieniu błędów, których nie można wykryć na podstawie widoku hello jednej usługi. Watchdogs są również kod toohost dobrym miejscem, który wykonuje czynności zaradczych bez interakcji z użytkownikiem (na przykład czyszczenie plików dziennika w magazynie, co pewien czas). Można znaleźć implementacji usługi programu alarmowego próbki [tutaj](https://github.com/Azure-Samples/service-fabric-watchdog-service).

Wprowadzenie do zrozumienia, jak pobrać generowany zdarzeń i dzienniki na powitania [poziom platformy](service-fabric-diagnostics-event-generation-infra.md) i hello [poziomie aplikacji](service-fabric-diagnostics-event-generation-app.md).
