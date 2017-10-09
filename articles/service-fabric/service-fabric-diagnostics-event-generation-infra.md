---
title: "aaaAzure usługi sieci szkieletowej platformy poziom monitorowania | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat platformy poziomu zdarzeń i dzienniki używane toomonitor i diagnozowanie klastrów sieci szkieletowej usług Azure."
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
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Platforma poziomu generowania zdarzeń i dzienników

## <a name="monitoring-hello-cluster"></a>Monitorowanie hello klastra

Jest ważne toomonitor na powitania platformy poziomu toodetermine czy sprzęt i klastra są działa zgodnie z oczekiwaniami. Sieć szkieletowa usług można zachować aplikacje uruchomione podczas awarii sprzętu, ale nadal potrzebujesz toodiagnose czy błąd występuje w aplikacji lub hello podstawowej infrastruktury. Należy również monitorować planu toobetter klastrów pojemności, pomoc w podejmowaniu decyzji dotyczących dodawania i usuwania sprzętu.

Usługa Service Fabric realizuje pięć inny dziennik kanały out-of box generowany hello następujące zdarzenia:

* Kanał operacyjne: wysokiego poziomu operacje wykonywane przez sieć szkieletowa usług i hello klastra, w tym zdarzenia dotyczące węzła przygotowanie Nowa aplikacja jest wdrażana, lub rz, Uaktualnij wycofywania itp.
* Kanał operacyjne — szczegółowe: raportów o kondycji i decyzje dotyczące równoważenia obciążenia
* Kanał wiadomości & danych: dzienniki krytyczne i zdarzenia generowane w naszym wiadomości (obecnie tylko hello ReverseProxy) oraz ścieżki danych (modeli niezawodne usługi)
* Kanał wiadomości & danych - szczegółowe: pełne kanału, który zawiera wszystkie dzienniki niekrytyczne hello z danych i wiadomości powitania klastra (tego kanału ma bardzo duża liczba zdarzeń)   
* [Niezawodne zdarzenia usług](service-fabric-reliable-services-diagnostics.md): określonych zdarzeń modelu programowania
* [Niezawodne zdarzenia podmiotów](service-fabric-reliable-actors-diagnostics.md): Programowanie określonych zdarzeń modelu i liczniki wydajności
* Obsługiwać dzienniki: dzienniki systemu wygenerowany przez sieć szkieletowa usług toobe tylko używane przez nas podczas dostarczania pomocy technicznej

Te kanały różnych obejmują większość hello platformy poziomu rejestrowania jest zalecane. tooimprove platformy poziom rejestrowania, należy wziąć pod uwagę zainwestować w lepsze model kondycji hello zrozumienia i dodawanie raportów niestandardowych kondycji i dodawanie niestandardowych **liczniki wydajności** toobuild w czasie rzeczywistym zrozumienia hello wpływ usługi i aplikacje w klastrze hello.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Kondycji sieci szkieletowej usług platformy Azure i raportowania obciążenia

Sieć szkieletowa usług ma własną modelu kondycji, który opisano szczegółowo w następujących artykułach:
- [Monitorowanie kondycji sieci szkieletowej tooService wprowadzenie](service-fabric-health-introduction.md)
- [Tworzenie raportów i sprawdzanie kondycji usług](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Dodawanie niestandardowych raportów kondycji sieci szkieletowej usług](service-fabric-report-health.md)
- [Wyświetl raporty dotyczące kondycji sieci szkieletowej usług](service-fabric-view-entities-aggregated-health.md)

Monitorowanie kondycji jest aspektów toomultiple krytyczny działania usługi. Monitorowanie kondycji jest szczególnie ważne w przypadku, gdy usługa sieć szkieletowa przeprowadza uaktualnienie aplikacji o nazwie. Po każdej z domen usługi hello jest uaktualniany i jest dostępny tooyour klientów, hello domeny uaktualnień musi upłynąć kontroli kondycji wdrożenia hello przenosi toohello następnej domeny uaktualnienia. Jeśli nie może zostać osiągnięty stanu dobrej kondycji, hello wdrożenia zostanie wycofana, tak, aby aplikacja hello jest w stanie znane, dobrym. Mimo że niektórzy klienci mogą mieć wpływ przed usług hello są wycofywane, większość klientów nie będą zgłaszać problemy. Ponadto rozwiązanie występuje stosunkowo szybko i bez konieczności toowait dla akcji z osoby pełniącej rolę operatora. Witaj więcej kontroli kondycji, które są zawarte w kodzie hello bardziej odporne usługi jest toodeployment problemów.

Innym aspektem usługi kondycji jest raportowania metryki z hello usługi. Metryki są ważne w sieci szkieletowej usług, ponieważ są one używane toobalance użycia zasobów. Metryki można również wskaźnik kondycji systemu. Na przykład może być aplikacja, która ma wiele usług, a każde wystąpienie zgłasza żądania na drugi metryka (RPS). Jeśli jedna usługa używa więcej zasobów niż innej usługi, usługi Service Fabric przenosi wystąpień usługi wokół klastra hello wykorzystania zasobów nawet toomaintain tootry. Aby uzyskać bardziej szczegółowy opis działania wykorzystania zasobów, zobacz [Zarządzanie zużycia zasobów i obciążenia w sieci szkieletowej usług o metryki](service-fabric-cluster-resource-manager-metrics.md).

Metryki również może pomóc zapewniają wgląd w sposób działa usługa. Wraz z upływem czasu można użyć toocheck metryk, które usługa hello działa w ramach oczekiwanych parametrów. Na przykład jeśli trendów pokazują, że na 9 AM w poniedziałek rano hello średni RPS jest 1000, a następnie można skonfigurować ostrzega użytkownika o hello RPS znajduje się poniżej 500 lub ponad 1500 raport dotyczący kondycji. Wszystko, co może być całkowicie poprawnie, ale może być należy się upewnić, że klientom najwyższą doskonałego toobe wyglądu. Usługi można zdefiniować zestawu metryk, które mogą być zgłaszane do celów sprawdzania kondycji, ale które nie mają wpływu na powitania zasób równoważenia hello klastra. toodo toozero waga metryki hello tego zestawu. Zaleca się uruchomić wszystkie metryki o wadze zero i zwiększa wagi hello nie ma pewności, zrozumieć waga metryki hello wpływ zasób równoważenia dla klastra.

> [!TIP]
> Nie należy używać zbyt wiele ważoną metryki. Może być trudne toounderstand Dlaczego wystąpień usługi są przenoszone dla równoważenia. Kilka metryki można zdecydowanie!

Wszystkie informacje, które mogą wskazywać hello kondycji i wydajności aplikacji jest kandydatem do raportów metryki. Licznik wydajności procesora CPU pomagają stwierdzić, jak węzeł jest wykorzystywany, ale go nie informujące, czy określonej usługi jest w dobrej kondycji, ponieważ wiele usług może działać w jednym węźle. Ale metryk, takich jak RPS, elementów przetworzonych, i wszystkich opóźnienia żądania może wskazywać na powitania kondycji określonej usługi.

tooreport kondycji, toothis podobny kod użycia:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport metrykę, użyj toothis podobny kod:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Dzienniki pomocy technicznej w sieci szkieletowej usług

Jeśli potrzebujesz toocontact pomocy technicznej firmy Microsoft dla pomocy z klastrem usługi sieć szkieletowa usług Azure, dzienniki pomocy technicznej prawie zawsze są wymagane. Jeśli klaster jest hostowana na platformie Azure, dzienniki pomocy technicznej są automatycznie konfigurowane i zebrane w ramach tworzenia klastra. Witaj dzienniki są przechowywane na koncie dedykowanych dla magazynu w grupie zasobów klastra. Hello konta magazynu nie ma stałej nazwy, ale konto hello jest widoczny kontenerów obiektów blob i tabel o nazwach rozpoczynających się od *sieci szkieletowej*. Uzyskać informacji o konfigurowaniu kolekcje dziennika dla klastra autonomicznych, zobacz [tworzenie i zarządzanie nimi autonomicznej klastra sieci szkieletowej usług Azure](service-fabric-cluster-creation-for-windows-server.md) i [ustawienia konfiguracji dla autonomicznego Windows klastra](service-fabric-cluster-manifest.md). Wystąpień usługi sieć szkieletowa autonomicznych dzienniki hello powinny być przesyłane tooa udziału pliku lokalnego. Jesteś **wymagane** toohave te dzienniki dla pomocy technicznej, ale nie są zamierzone toobe można używać przez osobami poza zespół obsługi klienta firmy Microsoft hello.

## <a name="enabling-diagnostics-for-a-cluster"></a>Włączanie diagnostyki dla klastra

W kolejności tootake zaletą te dzienniki zaleca się, że podczas tworzenia klastra "diagnostyki" jest włączona. Przez włączenie diagnostyki, po wdrożeniu klastra hello Windows Azure Diagnostics jest możliwe tooacknowledge hello Operational, Reliable Services i Reliable actors kanałów i przechowywania danych hello jak wyjaśniono dalej w [agregacji zdarzeń z Diagnostyka Azure](service-fabric-diagnostics-event-aggregation-wad.md).

Jak pokazano powyżej, dostępna jest również tooadd pole opcjonalne klucza Instrumentacji Application Insights (AI). Jeśli wybierzesz toouse AI do analizy wszystkie zdarzenia (Dowiedz się więcej na temat [analiza zdarzeń z usługi Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), w tym miejscu zawierają hello AppInsights zasobów instrumentationKey (GUID).


Jeśli zamierzasz toodeploy kontenery tooyour klastra należy włączyć toopick WAD zapasowej Statystyka docker przez dodanie tego tooyour "WadCfg > DiagnosticMonitorConfiguration":

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Pomiaru wydajności

Miara wydajności klastra ułatwią zrozumienie, jak jest możliwe toohandle obciążenia i dysku decyzje wokół skalowanie klastra (Zobacz więcej informacji na temat skalowania klastra [na platformie Azure](service-fabric-cluster-scale-up-down.md), lub [lokalnymi](service-fabric-cluster-windows-server-add-remove-nodes.md)). Dane dotyczące wydajności jest również przydatne w przypadku gdy w porównaniu tooactions możesz lub aplikacji i usług może posiadać pobrane podczas analizowania dzienników w hello przyszłych. 

Aby uzyskać listę toocollect liczniki wydajności, korzystając z usługi Service Fabric, zobacz [liczników wydajności w sieci szkieletowej usług](service-fabric-diagnostics-event-generation-perf.md)

Istnieją dwa sposoby typowych, w których można skonfigurować zbieranie danych wydajności dla klastra:

* Przy użyciu agenta: jest hello preferowany sposób zbierania wydajności z komputera, ponieważ agenci mają zwykle listę metryki wydajności możliwości, które mogą być zbierane i jest stosunkowo łatwa procesu toochoose hello metryki mają toocollect lub je zmienić . Przeczytaj informacje o [jak tooconfigure hello OMS dla sieci szkieletowej usług](service-fabric-diagnostics-event-analysis-oms.md) i [Konfigurowanie agenta pakietu OMS Windows hello](../log-analytics/log-analytics-windows-agents.md) toolearn artykuły więcej informacji na temat agent pakietu OMS hello, czyli jednego takiego agenta monitorowania, czy jest możliwe toopick uruchomiona dane wydajności dla maszyn wirtualnych klastra i wdrożone kontenery.

* Konfigurowanie wydajności diagnostyki toowrite liczników tabeli tooa: w przypadku klastrów w systemie Azure, oznacza to, zmiana hello Azure Diagnostics konfiguracji toopick się liczniki wydajności odpowiednie hello hello maszyn wirtualnych w klastrze i włączenie go toopick w górę Statystyka docker, jeśli będziesz wdrażać żadnych kontenerów. Przeczytaj informacje o konfigurowaniu [liczniki wydajności w WAD](service-fabric-diagnostics-event-aggregation-wad.md) w sieci szkieletowej usług tooset się zbieranie danych licznika wydajności.

## <a name="next-steps"></a>Następne kroki

Dzienniki, a zdarzenia muszą toobe zagregowane, zanim będzie można wysłać tooany analizy platformy. Przeczytaj informacje o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) i [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter zrozumieniu hello zalecane opcje.
