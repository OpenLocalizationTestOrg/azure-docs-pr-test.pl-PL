---
title: "Usługa Azure sieci szkieletowej platformy poziom monitorowania | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat platformy poziomu zdarzeń i dzienników umożliwia monitorowanie i diagnozowanie klastrów sieci szkieletowej usług Azure."
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
ms.date: 11/20/2017
ms.author: dekapur
ms.openlocfilehash: 8452b5ae733b21254b0beecaec44a968897ae491
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/13/2017
---
# <a name="platform-level-event-and-log-generation"></a>Platforma poziomu generowania zdarzeń i dzienników

## <a name="monitoring-the-cluster"></a>Monitorowanie klastra

Należy monitorować na poziomie platformy, aby ustalić, czy sprzęt i klastra są działa zgodnie z oczekiwaniami. Sieć szkieletowa usług można zachować aplikacje uruchomione podczas awarii sprzętu, ale nadal konieczne zdiagnozować, czy błąd występuje w aplikacji lub podstawowej infrastruktury. Należy również monitorować klastrów lepiej planowania pojemności, pomoc w podejmowaniu decyzji dotyczących dodawania i usuwania sprzętu.

Usługa Service Fabric realizuje następujące dziennika kanały out-of box:
* Kanał operacyjne: wysokiego poziomu operacje wykonywane przez sieć szkieletowa usług i klastra, w tym zdarzenia dotyczące powtarzający się węzeł, nowej aplikacji wdrażany lub uaktualniania wycofywania itp.
* Kanał operacyjne — szczegółowe: raportów o kondycji i decyzje dotyczące równoważenia obciążenia
* Kanał wiadomości & danych: dzienniki krytyczne i zdarzenia generowane w wiadomości (obecnie tylko ReverseProxy) i ścieżki danych (modeli niezawodne usługi)
* Kanał wiadomości & danych - szczegółowe: pełne kanału, który zawiera wszystkie dzienniki niekrytyczne z danych i komunikatów w klastrze (ten kanał jest bardzo duża liczba zdarzeń)   

Oprócz tych istnieją dwa strukturalnych kanały źródła zdarzeń, a także dzienniki, które zbieramy do celów pomocy technicznej.
* [Niezawodne zdarzenia usług](service-fabric-reliable-services-diagnostics.md): określonych zdarzeń modelu programowania
* [Niezawodne zdarzenia podmiotów](service-fabric-reliable-actors-diagnostics.md): Programowanie określonych zdarzeń modelu i liczniki wydajności
* Obsługiwać dzienniki: dzienniki systemu wygenerowany przez sieć szkieletowa usług tylko do użycia przez nas podczas dostarczania pomocy technicznej

Te kanały różnych obejmują większość platform poziomu rejestrowania jest zalecane. Aby zwiększyć poziom rejestrowania platformy, należy wziąć pod uwagę zainwestować w lepsze zrozumienie model kondycji i dodawanie raportów niestandardowych kondycji i dodawanie niestandardowych **liczniki wydajności** do kompilacji w czasie rzeczywistym zrozumienia wpływu użytkownika usługi i aplikacje w klastrze.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Kondycji sieci szkieletowej usług platformy Azure i raportowania obciążenia

Sieć szkieletowa usług ma własną modelu kondycji, który opisano szczegółowo w następujących artykułach:
- [Wprowadzenie do monitorowania kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)
- [Tworzenie raportów i sprawdzanie kondycji usług](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Dodawanie niestandardowych raportów kondycji sieci szkieletowej usług](service-fabric-report-health.md)
- [Wyświetl raporty dotyczące kondycji sieci szkieletowej usług](service-fabric-view-entities-aggregated-health.md)

Monitorowanie kondycji jest kluczowa wiele aspektów pracy z usługą. Monitorowanie kondycji jest szczególnie ważne w przypadku, gdy usługa sieć szkieletowa przeprowadza uaktualnienie aplikacji o nazwie. Po każdej domeny uaktualnienia usługi jest uaktualniany i jest dostępny dla klientów, domeny uaktualnień musi upłynąć kontroli kondycji wdrożenia przechodzi do następnej domeny uaktualnienia. Jeśli stanu dobrej kondycji nie może zostać osiągnięty, wdrożenia zostanie wycofana, dzięki czemu aplikacja jest w stanie znane, dobrym. Mimo że niektórzy klienci mogą mieć wpływ przed usług są wycofywane, większość klientów nie będą zgłaszać problemy. Ponadto rozwiązanie występuje stosunkowo szybko i bez potrzeby czekania na akcję osoby pełniącej rolę operatora. Więcej kontroli kondycji, które są włączone do kodu, bardziej odporne usługi ma problemy z wdrażaniem.

Innym aspektem usługi kondycji jest raportowania metryki z usługi. Metryki są ważne w sieci szkieletowej usług, ponieważ są one używane do równoważyć obciążenie zasobów. Metryki można również wskaźnik kondycji systemu. Na przykład może być aplikacja, która ma wiele usług, a każde wystąpienie zgłasza żądania na drugi metryka (RPS). Jeśli jedna usługa używa więcej zasobów niż innej usługi, usługi Service Fabric przenosi wystąpień usługi wokół klastra, aby spróbować Obsługa wykorzystania zasobów nawet. Aby uzyskać bardziej szczegółowy opis działania wykorzystania zasobów, zobacz [Zarządzanie zużycia zasobów i obciążenia w sieci szkieletowej usług o metryki](service-fabric-cluster-resource-manager-metrics.md).

Metryki również może pomóc zapewniają wgląd w sposób działa usługa. Wraz z upływem czasu metryki służy do sprawdzenia, czy usługa działa w ramach oczekiwanych parametrów. Na przykład jeśli trendy wskazują na 9 AM w poniedziałek rano średnią RPS jest 1000, następnie może skonfigurowaniu ostrzega użytkownika o RPS znajduje się poniżej 500 lub ponad 1500 raport dotyczący kondycji. Wszystko, co może być całkowicie poprawnie, ale może być warto wygląd należy upewnić się, że klientom najwyższą maksymalnego komfortu obsługi. Usługi można zdefiniować zestawu metryk, które mogą być zgłaszane do celów sprawdzania kondycji, ale które nie mają wpływu na równoważenia zasobów klastra. Aby to zrobić, należy ustawić na zero waga metryki. Zaleca się uruchomić wszystkie metryki o wadze zero i zwiększa wagę nie ma pewności, zrozumieć wpływ waga metryki równoważenia dla klastra zasobów.

> [!TIP]
> Nie należy używać zbyt wiele ważoną metryki. Może być trudne do zrozumienia, dlaczego wystąpień usługi są przenoszone dla równoważenia. Kilka metryki można zdecydowanie!

Wszystkie informacje, które mogą wskazywać kondycję i wydajność aplikacji jest kandydatem do raportów metryki. Licznik wydajności procesora CPU pomagają stwierdzić, jak węzeł jest wykorzystywany, ale go nie informujące, czy określonej usługi jest w dobrej kondycji, ponieważ wiele usług może działać w jednym węźle. Ale metryk, takich jak RPS, elementów przetworzonych, i wszystkich opóźnienia żądania można wskazać kondycji określonej usługi.

Raport kondycji, należy użyć kodu podobny do poniższego:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

Aby zgłosić metrykę, należy użyć kodu podobny do poniższego:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Dzienniki pomocy technicznej w sieci szkieletowej usług

Należy się z pomocą techniczną firmy Microsoft, aby uzyskać pomoc dotyczącą klastra usługi sieć szkieletowa usług Azure, dzienniki pomocy technicznej są prawie zawsze wymagane. Jeśli klaster jest hostowana na platformie Azure, dzienniki pomocy technicznej są automatycznie konfigurowane i zebrane w ramach tworzenia klastra. Dzienniki są przechowywane na koncie dedykowanych dla magazynu w grupie zasobów klastra. Konto magazynu nie ma stałej nazwy, ale w ramach konta, zobacz kontenerów obiektów blob i tabel o nazwach rozpoczynających się od *sieci szkieletowej*. Uzyskać informacji o konfigurowaniu kolekcje dziennika dla klastra autonomicznych, zobacz [tworzenie i zarządzanie nimi autonomicznej klastra sieci szkieletowej usług Azure](service-fabric-cluster-creation-for-windows-server.md) i [ustawienia konfiguracji dla autonomicznego Windows klastra](service-fabric-cluster-manifest.md). Dla wystąpień usługi sieć szkieletowa autonomicznych dzienniki powinny być przesyłane do udziału pliku lokalnego. Jesteś **wymagane** mają te dzienniki dla pomocy technicznej, ale nie są przeznaczone do można korzystać przez osobami poza zespół obsługi klienta firmy Microsoft.

## <a name="enabling-diagnostics-for-a-cluster"></a>Włączanie diagnostyki dla klastra

Aby można było korzystać z tych dzienników, zaleca się, czy podczas tworzenia klastra "diagnostyki" jest włączona. Przez włączenie diagnostyki, po wdrożeniu klastra systemu Windows Azure Diagnostics jest w stanie potwierdzić Operational, Reliable Services i Reliable actors kanałów i przechowywać dane, jak wyjaśniono dalej w [agregacji zdarzenia z platformy Azure Diagnostyka](service-fabric-diagnostics-event-aggregation-wad.md).

Jak pokazano powyżej, dostępna jest również pole opcjonalne, aby dodać klucz Instrumentacji Application Insights (AI). Jeśli chcesz użyć AI do analizy wszystkie zdarzenia (Dowiedz się więcej na temat [analiza zdarzeń z usługi Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), w tym miejscu zawierają instrumentationKey zasobów AppInsights (GUID).


Jeśli zamierzasz wdrażanie kontenerów do klastra, należy włączyć WAD podnieść Statystyka docker, dodając to Twoje "WadCfg > DiagnosticMonitorConfiguration":

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Pomiaru wydajności

Miara wydajności klastra ułatwią zrozumienie, jak jest w stanie obsłużyć obciążenia i dysku decyzje wokół skalowanie klastra (Zobacz więcej informacji na temat skalowania klastra [na platformie Azure](service-fabric-cluster-scale-up-down.md), lub [lokalnymi](service-fabric-cluster-windows-server-add-remove-nodes.md)). Dane dotyczące wydajności jest również przydatne w porównaniu do akcji, które można lub aplikacje i usługi mogą posiadać pobrane podczas analizowania dzienników w przyszłości. 

Aby uzyskać listę liczników wydajności do zebrania po przy użyciu usługi Service Fabric, zobacz [liczników wydajności w sieci szkieletowej usług](service-fabric-diagnostics-event-generation-perf.md)

Istnieją dwa sposoby typowych, w których można skonfigurować zbieranie danych wydajności dla klastra:

* Przy użyciu agenta: jest to preferowany sposób zbierania wydajności z komputera, ponieważ agenci mają zwykle listę metryki wydajności możliwości, które mogą być zbierane i jest stosunkowo łatwa procesu, aby wybrać metryki, aby zbierać lub je zmienić. Przeczytaj informacje o [sposobu konfigurowania sieci szkieletowej usług OMS](service-fabric-diagnostics-event-analysis-oms.md) i [konfigurowania agenta systemu Windows OMS](../log-analytics/log-analytics-windows-agent.md) artykuły, aby dowiedzieć się więcej o agenta pakietu OMS to jeden taki agent monitorowania, który może podnieść wydajność dane dla maszyn wirtualnych klastra i wdrożone kontenery.

* Konfigurowanie diagnostykę, aby zapisać liczniki wydajności do tabeli: w przypadku klastrów w systemie Azure, oznacza to, zmienianie konfiguracji diagnostyki Azure do odebrania liczniki wydajności odpowiednie z maszyn wirtualnych w klastrze, a następnie włączenie go do odebrania Statystyka docker, jeśli wdrażania żadnych kontenerów. Przeczytaj informacje o konfigurowaniu [liczniki wydajności w WAD](service-fabric-diagnostics-event-aggregation-wad.md) w sieci szkieletowej usług, aby skonfigurować zbieranie danych licznika wydajności.

## <a name="next-steps"></a>Następne kroki

Dzienniki, a zdarzenia konieczne zagregowane, zanim będzie można wysłać do dowolnej platformie analizy. Przeczytaj informacje o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) i [WAD](service-fabric-diagnostics-event-aggregation-wad.md) aby lepiej zrozumieć niektóre zalecane opcje.
