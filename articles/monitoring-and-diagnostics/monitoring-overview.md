---
title: aaaMonitoring na platformie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Opcje można toomonitor z jakąkolwiek platformie Microsoft Azure. Azure Monitor, analizy dzienników Application Insights"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Omówienie monitorowania na platformie Microsoft Azure
Ten artykuł zawiera omówienie narzędzia dostępne dla monitorowania programu Microsoft Azure. Ma to zastosowanie zbyt
- monitorowanie aplikacji działających na platformie Microsoft Azure 
- narzędzia/usługi działające poza platformą Azure, które można monitorować obiekty należące do platformy Azure. 

Zawarto informacje hello różnych produktów i usług dostępnych i ich współpracę. Mogą pomagać Ci toodetermine narzędzia, które są najbardziej odpowiednie dla Ciebie w jakich przypadkach.  

## <a name="why-use-monitoring-and-diagnostics"></a>Dlaczego warto używać monitorowania i diagnostyki?

Problemy z wydajnością w Twojej aplikacji w chmurze może wpłynąć na Twojej firmy. Z wielu powiązanych elementów i częste wersjach degradations może nastąpić w dowolnej chwili. I w przypadku tworzenia aplikacji, użytkowników, zazwyczaj odnajdywanie problemy, które nie udało się znaleźć podczas testowania. Należy od razu wiedzieć o tych problemów i narzędzia do diagnozowania i rozwiązywania problemów hello. Microsoft Azure ma szeroką gamę narzędzi do identyfikacji tych problemów.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Jak monitorować Moje aplikacje w chmurze Azure?

Istnieje szereg narzędzia do monitorowania usługi i aplikacje platformy Azure. Niektóre z ich funkcji nakładają się. To jest częściowo ze względów historycznych i częściowo powodu toohello rozmycia między rozwoju i działania aplikacji. 

Poniżej przedstawiono hello Narzędzia główne:

-   **Azure Monitor** jest podstawowym narzędziem do monitorowania usługi działające na platformie Azure. Udostępnia poziomie infrastruktury danych o przepływności hello usługi i hello otaczającego środowiska. W przypadku zarządzania aplikacjami w usłudze Azure podejmowaniu decyzji, czy tooscale w górę lub w dół zasobów, Azure Monitor daje służą toostart.

-   **Usługa Application Insights** mogą być używane do tworzenia aplikacji oraz jako rozwiązanie monitorujące produkcji. Działa, instalując pakiet w swojej aplikacji, a więc zapewnia bardziej wewnętrzny widok co się dzieje. Jego danych obejmuje czas reakcji zależności i śladów wyjątek, debugowanie migawki, profile wykonywania. Zapewnia on zaawansowanych narzędzi inteligentne analizowanie danych to dane telemetryczne zarówno toohelp debugowania aplikacji i toohelp zrozumieć, co robią użytkownicy z nim. Można określić, czy kolekcji w czas reakcji przypada toosomething w aplikacji lub niektóre zewnętrznego problemem resourcing. Jeśli używasz programu Visual Studio i aplikacji hello jest uszkodzone, użytkownik może zostać pobrany prawo toohello problem wiersze kodu, można go naprawić.  

-   **Zaloguj się Analytics** jest potrzebują tootune wydajności i plan konserwacji na aplikacje uruchomione w środowisku produkcyjnym. Jest on oparty na platformie Azure. On zbiera i agregują dane z wielu źródeł, chociaż z opóźnieniem 10 minut too15. Przewiduje całościowe rozwiązanie zarządzania Azure, lokalne i innych firm oparte na chmurze infrastruktury (na przykład usług Amazon Web Services). Zawiera bardziej zaawansowane funkcje narzędzi tooanalyze danych między źródłami więcej, umożliwia złożonych zapytań przez wszystkie dzienniki i może aktywnie alert po wystąpieniu określonego warunku.  Można nawet zebrać dane niestandardowe w jego centralnym repozytorium, dzięki czemu może zapytania i wizualizacji go. 

-   **System Center Operations Manager (SCOM)** jest do zarządzania i monitorowania instalacji dużych chmury. Może być już znasz go jako narzędzia do zarządzania lokalnymi chmury na podstawie funkcji Hyper-V i Windows Server, ale można również zintegrować z i zarządzanie aplikacjami platformy Azure. Między innymi może instalować usługi Application Insights na istniejące aplikacje na żywo.  Jeśli aplikacja przestanie działać, określa w sekundach. Należy pamiętać, że analizy dzienników nie zastępuje SCOM. Działa w połączeniu z nim.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>Uzyskiwanie dostępu do monitorowania w hello portalu Azure
Wszystkie usługi monitorowania Azure są teraz dostępne w jednym okienku interfejsu użytkownika. Aby uzyskać więcej informacji na temat tooaccess ten obszar, zobacz [Rozpoczynanie pracy z monitorem Azure](monitoring-get-started.md). 

Funkcje monitorowania dla określonych zasobów można także przejść przez wyróżnianie tych zasobów i przechodzenie od ich opcje monitorowania. 

## <a name="examples-of-when-toouse-which-tool"></a>Przykłady sytuacji, w których toouse, w którym narzędzie 

Hello następujące sekcje zawierają niektóre podstawowe scenariusze i narzędzia, które powinny być używane razem. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Scenariusz 1 — poprawki błędów w tworzonej aplikacji Azure   

**Witaj najlepszym rozwiązaniem jest razem toouse Application Insights, Azure Monitor i programu Visual Studio**

Platforma Azure udostępnia teraz pełną moc hello debuger programu Visual Studio w chmurze hello hello. Skonfiguruj Azure Monitor toosend telemetrii tooApplication szczegółowych informacji. Włącz program Visual Studio tooinclude hello zestaw SDK usługi Application Insights w aplikacji. Po w usłudze Application Insights, można użyć toodiscover mapowanie aplikacji hello wizualnie części uruchomionych aplikacji, które jest w złej kondycji lub też nie. Dla tych elementów, które nie są w dobrej kondycji błędy i wyjątki są już dostępne dla eksploracji. Można użyć hello różnych analityka w bardziej toogo usługi Application Insights. Jeśli nie masz pewności o błędzie hello, można użyć tootrace debugera programu Visual Studio hello punkt kodu i numer pin dalsze problem. 

Aby uzyskać więcej informacji, zobacz [monitorowania aplikacji sieci Web](../application-insights/app-insights-azure-web-apps.md) i odwoływać się toohello spis treści po lewej stronie powitania instrukcje dotyczące różnych typów aplikacji i języków.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Scenariusz 2 — debugowania aplikacji sieci web Azure .NET błędów, które zawierają tylko w środowisku produkcyjnym 

> [!NOTE]
> Te funkcje są w wersji zapoznawczej. 

**Witaj najlepszych opcji jest toouse Application Insights i jeśli to możliwe Visual Studio dla hello pełnej obsługi debugowania.**

Użyj aplikacji hello toodebug Application Insights migawki debugera. W przypadku pewnej wartości progowej błędu ze składnikami produkcji, hello system automatycznie przechwytuje dane telemetryczne w systemie windows w czasie o nazwie "migawki." Hello kwota przechwycone jest bezpieczne dla chmury produkcji ponieważ jest za mały za mało nie tooaffect wydajność, ale wystarczająco znaczące tooallow śledzenia.  Hello systemie może przechwytywać wiele migawek. Można przyjrzeć się punktu w czasie w portalu Azure hello lub użyć programu Visual Studio dla hello pełne środowisko. Z programem Visual Studio deweloperzy mogą Przeprowadź przez tej migawki tak, jakby były one debugowanie w czasie rzeczywistym. Zmienne lokalne, parametry, pamięci i ramki będą dostępne. Deweloperzy muszą mieć uprawnienie dostępu do danych produkcyjnych toothis za pomocą roli RBAC.  

Aby uzyskać więcej informacji, zobacz [debugowania migawki](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Scenariusz 3 — debugowania aplikacji Azure, która używa kontenerów lub mikrousług 

**Taka sama jak Scenariusz 1. Jednocześnie używać usługi Application Insights, Azure Monitor i programu Visual Studio** usługi Application Insights obsługuje również zbieranie telemetrii z procesów uruchomionych wewnątrz kontenerów i mikrousług (Kubernetes, Docker, sieć szkieletowa usług Azure). Aby uzyskać więcej informacji [zobacz ten film na debugowanie kontenerów i mikrousług](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Scenariusz 4 — wydajności napraw problemy w aplikacji Azure

Witaj [profilera usługi Application Insights](../application-insights/app-insights-profiler.md) jest zaprojektowana toohelp rozwiązywanie tego typu problemów. Identyfikowanie i rozwiązywanie problemów z wydajnością aplikacji uruchomionych w usługach aplikacji (aplikacje sieci Web, Logic Apps, Mobile Apps, aplikacje interfejsu API) i innych zasobów obliczeniowych, takich jak maszyny wirtualne, maszyny wirtualnej zestawy skalowania (VMSS), usługi w chmurze i sieci szkieletowej usług . 

> [!NOTE]
> Tooprofile możliwości maszyn wirtualnych, zestawy skalowania maszyny wirtualnej (VMSS), usługi w chmurze i sieci szkieletowej usług jest w wersji zapoznawczej.   

Ponadto aktywne wyświetla powiadomienie pocztą e-mail o niektórych typów błędów, takich jak czas ładowania strony powoli, narzędzie do wykrywania inteligentne hello.  Nie trzeba toodo żadnej konfiguracji dotyczących tego narzędzia. Aby uzyskać więcej informacji, zobacz [inteligentne wykrywanie - anomalii wydajności](../application-insights/app-insights-proactive-performance-diagnostics.md) i [inteligentne wykrywanie - anomalii wydajności](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o

* [Azure Monitor wideo z Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Wprowadzenie do platformy Azure monitora](monitoring-get-started.md)
* [Diagnostyka Azure](../azure-diagnostics.md) Jeśli próbujesz toodiagnose problemów w usłudze chmury maszyny wirtualnej maszyny wirtualnej skalowanie aplikacji sieci szkieletowej ustawiona lub usługi.
* [Usługa Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) Jeśli próbujesz toodiagnostic problemy w aplikacji sieci Web usługi aplikacji.
* [Zaloguj się Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) i hello [Operations Management Suite](https://www.microsoft.com/oms/) produkcji rozwiązanie monitorujące,