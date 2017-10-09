---
title: "klastry Chaos w sieci szkieletowej usług aaaInduce | Dokumentacja firmy Microsoft"
description: "Przy użyciu iniekcji błędów i interfejsów API usługi analizy klastra toomanage Chaos hello klastra."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Wywołać kontrolowane Chaos w klastrach sieci szkieletowej usług
Dużych systemów rozproszonych jak infrastruktury chmury jest z założenia gwarantowane. Sieć szkieletowa usług Azure umożliwia toowrite deweloperzy niezawodnej usługi rozproszone zawodnych infrastrukturze. toowrite niezawodne usługi rozproszone zawodnych infrastrukturze, deweloperzy muszą toobe tootest stanie hello stabilności ich usług podczas hello podstawowej infrastruktury zawodnych przechodzi przez przejść stanu skomplikowane toofaults ukończenia.

Witaj [iniekcji błędów i usługi klastrowania analizy](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (znanej także jako hello błędów Analysis Service) umożliwia deweloperom hello tooinduce błędów tootest swoich usług. Tak samo, jak te docelowe symulowane błędów, [ponowne uruchomienie partycji](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), ułatwiają wykonywanie hello najczęściej przejścia stanu. Jednak docelowe symulowane błędów są ukierunkowane zgodnie z definicją i w związku z tym może nie usterek przedstawiające się tylko w twardych prognozowania, długich i skomplikowane sekwencji przejścia stanu. Nieobciążonej testowania, możesz użyć Chaos.

Chaos symuluje błędów okresowych, przeplotem (bezpieczne i nieprawidłowego) w całym klastrze hello przez dłuższy czas. Po skonfigurowaniu Chaos hello szybkość i hello rodzaju błędów, można uruchomić Chaos za pomocą języka C# lub interfejs API środowiska Powershell toostart generowanie błędów w klastrze hello i w usługach. Można skonfigurować Chaos toorun w określonym przedziale czasu (na przykład na godzinę), po którym Chaos automatycznie zatrzymywana, lub toostop API StopChaos (C# lub programu Powershell) można wywołać go w dowolnym momencie.

> [!NOTE]
> W postaci bieżącego Chaos wywołuje tylko bezpiecznych błędy, co oznacza, że w przypadku braku błędów zewnętrznych hello utrata kworum, lub utraty danych nigdy nie występuje.
>

Po uruchomieniu Chaos tworzy różne zdarzenia, które przechwytywania stanu hello hello Uruchom w chwili hello. Na przykład ExecutingFaultsEvent zawiera wszystkie błędy hello Chaos decyzję tooexecute w tym iteracji. ValidationFailedEvent zawiera szczegóły hello awarii sprawdzania poprawności (problemów kondycji lub stabilności), który został znaleziony podczas sprawdzania poprawności hello hello klastra. Można wywołać hello API GetChaosReport (C# lub programu Powershell) tooget hello raportu Chaos przebiegów. Te zdarzenia uzyskać utrwalone w [niezawodnej słownika](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), której obowiązują zasady obcięcie ustawieniem dwie konfiguracje: **MaxStoredChaosEventCount** (wartość domyślna to 25000) i **StoredActionCleanupIntervalInSeconds** (wartość domyślna to 3600). Każdy *StoredActionCleanupIntervalInSeconds* Chaos kontroli i wszystkie ale hello najnowszych *MaxStoredChaosEventCount* zdarzenia, zostaną usunięte ze słownika niezawodnej hello.

## <a name="faults-induced-in-chaos"></a>Błędy powstaniu w Chaos
Chaos generuje błędy między hello całego klastra sieci szkieletowej usług i kompresuje błędów, które są widoczne w miesięcy lub lat do kilku godzin. Kombinacja Hello przeplotem błędów ze stawką wysoką odporność hello znajduje sytuacjach wyjątkowych, które w przeciwnym razie mogą zostać pominięci. Tego ćwiczenia Chaos prowadzi tooa znaczne ulepszenia w jakości kodu hello hello usługi.

Chaos wywołuje usterek z hello następujące kategorie:

* Uruchom ponownie węzeł
* Ponowne uruchomienie wdrożonego pakietu kodu
* Usuwanie repliki
* Uruchom ponownie repliki
* Przenieś repliki podstawowej (można konfigurować)
* Przenieś repliki pomocniczej (można konfigurować)

Chaos działa w przejść przez wiele iteracji. Każdej iteracji składa się z usterek i sprawdzania poprawności klastra hello określonym okresie. Możesz skonfigurować czas hello hello toostabilize klastra i toosucceed sprawdzania poprawności. Jeśli błąd zostanie znaleziony w weryfikacji klastra, Chaos generuje i będzie się powtarzał ValidationFailedEvent sygnatury czasowej UTC hello oraz szczegóły dotyczące błędu hello. Rozważmy na przykład wystąpienie Chaos ustawionej toorun godzinę z maksymalnie trzech równoczesnych błędów. Chaos wywołuje trzy błędów, a następnie weryfikuje hello kondycji klastra. Go iterację hello poprzedniego kroku, dopóki nie zostanie jawnie zatrzymana za pośrednictwem interfejsu API StopChaosAsync hello lub jednogodzinnym przekazuje. Jeśli klaster hello staje się zła w dowolnym iteracji (to znaczy go nie stabilizacji w hello przekazany w MaxClusterStabilizationTimeout) Chaos generuje ValidationFailedEvent. To zdarzenie wskazuje, że coś niepowodzenia i może być konieczne dalsze badania.

tooget, który błędów Chaos powstaniu, możesz użyć GetChaosReport API (programu powershell lub C#). Witaj interfejsu API pobiera hello następny segment hello Chaos raportu na podstawie tokenu przekazanego kontynuacji hello lub hello przekazany w czasie range. Można określić hello ContinuationToken tooget hello następny segment hello Chaos raportu lub można określić zakres czasu hello za pośrednictwem StartTimeUtc i EndTimeUtc, ale nie można określić zarówno hello ContinuationToken, jak i zakres czasu hello w hello samo wywołanie. W przypadku więcej niż 100 zdarzeń Chaos hello Chaos raportu jest zwracana w segmentach gdy segment zawiera nie więcej niż 100 zdarzeń Chaos.

## <a name="important-configuration-options"></a>Opcje konfiguracji ważne
* **TimeToRun**: suma czasu uruchomionym programem Chaos przed zakończeniem pomyślnie. Można zatrzymać Chaos ma uruchomić hello TimeToRun okres za pośrednictwem hello StopChaos interfejsu API.

* **MaxClusterStabilizationTimeout**: hello maksymalną ilość czasu toowait dla toobecome klastra hello dobrej kondycji przed utworzeniem ValidationFailedEvent. Ten oczekiwania jest tooreduce hello obciążenie klastra hello podczas, gdy trwa jej odzyskiwanie. testy Hello wykonać to polecenie:
  * Jeśli kondycja klastra hello jest OK
  * Jeśli kondycja usługi hello jest OK
  * Jeśli rozmiar zestawu replik docelowy hello uzyskuje się hello partycji usługi
  * Czy istnieją nie replik w stanie InBuild
* **MaxConcurrentFaults**: hello maksymalną liczbę równoczesnych usterek, które są wywołane w każdej iteracji. większa liczba hello Hello, hello skuteczniejsze jest Chaos i hello operacji Failover i hello stan przejścia kombinacje, które hello klastra przesyłany przez także są bardziej złożone. 

> [!NOTE]
> Niezależnie od tego jak wysoka wartość *MaxConcurrentFaults* ma Chaos gwarantuje — w przypadku braku hello zewnętrznych usterek — nie utraty kworum lub utraty danych.
>

* **EnableMoveReplicaFaults**: Włącza lub wyłącza hello błędów, które powodują hello toomove repliki podstawowej lub dodatkowej. Te błędy są domyślnie wyłączone.
* **WaitTimeBetweenIterations**: hello ilość toowait czas między poszczególnymi iteracjami. Oznacza to, że hello czas Chaos zatrzyma się po wykonaniu round usterek i o zakończeniu hello odpowiedniego sprawdzania poprawności kondycji hello hello klastra. Witaj wyższa wartość hello, niższe hello jest wskaźnikiem iniekcji średnią usterek hello.
* **WaitTimeBetweenFaults**: hello ilość czasu toowait między dwa kolejne błędy w jednym iteracji. Witaj wyższa wartość hello, hello niższe hello współbieżności (lub hello nakładania się) błędów.
* **ClusterHealthPolicy**: zasady dotyczące kondycji klastra jest używane toovalidate hello kondycji klastra hello Between Chaos iteracji. Jeśli stan klastra hello jest wynikiem błędu lub sytuacji wystąpił nieoczekiwany wyjątek podczas wykonywania błąd Chaos będzie czekać przez 30 minut przed hello dalej — sprawdzenie kondycji - tooprovide hello klaster z niektórych toorecuperate czasu.
* **Kontekst**: pary klucz wartość typu kolekcji (ciąg). Mapa Hello mogą być używane toorecord informacje o hello Chaos Uruchom. Nie może być więcej niż 100 takie pary, a każdy ciąg (klucz lub wartość) może mieć maksymalnie 4095 znaków. Ta mapa jest ustawiana przez starter hello hello Chaos Uruchom toooptionally magazynu hello kontekstu o określonych hello Uruchom.

## <a name="how-toorun-chaos"></a>Jak toorun Chaos

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
