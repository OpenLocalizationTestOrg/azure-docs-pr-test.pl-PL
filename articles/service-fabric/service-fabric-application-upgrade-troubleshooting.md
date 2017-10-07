---
title: Uaktualnianie aplikacji aaaTroubleshooting | Dokumentacja firmy Microsoft
description: "W tym artykule opisano kilka typowych problemów wokół uaktualniania aplikacji usługi Service Fabric i w jaki sposób tooresolve je."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>Rozwiązywanie problemów z uaktualnieniami aplikacji
W tym artykule omówiono niektóre typowe problemy hello wokół uaktualniania aplikacji sieci szkieletowej usług Azure i w jaki sposób tooresolve je.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Rozwiązywanie problemów z uaktualniania aplikacji nie powiodło się
Jeśli uaktualnienie nie powiedzie się, dane wyjściowe hello hello **Get-ServiceFabricApplicationUpgrade** polecenia zawiera dodatkowe informacje dotyczące debugowania błędu hello.  Witaj poniżej określa używania hello dodatkowe informacje:

1. Określ typ awarii hello.
2. Zidentyfikuj hello Przyczyna niepowodzenia.
3. Określ co najmniej jednego składnika Niepowodzenie w celu dokładniejszego zbadania.

Te informacje są dostępne, gdy sieci szkieletowej usług wykryje błąd hello niezależnie od tego, czy hello **FailureAction** jest tooroll wstecz lub wstrzymać hello uaktualnienia.

### <a name="identify-hello-failure-type"></a>Określ typ awarii hello
W danych wyjściowych hello **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identyfikuje hello sygnatury (UTC) jaką błąd uaktualnienia został wykryty przez sieć szkieletowa usług i  **FailureAction** zostało wyzwolone. **Przyczyna błędu** identyfikuje jeden z trzech potencjalnych przyczyn wysokiego poziomu przez hello:

1. UpgradeDomainTimeout — wskazuje, że konkretnej domeny uaktualnienia trwało zbyt długo toocomplete i **UpgradeDomainTimeout** wygasł.
2. OverallUpgradeTimeout - wskazuje tego hello ogólne uaktualnienia trwało zbyt długo toocomplete i **UpgradeTimeout** wygasł.
3. Test kondycji — wskazuje, że po uaktualnieniu domeny aktualizacji aplikacji hello pozostała zła zgodnie z toohello określone zasady dotyczące kondycji i **HealthCheckRetryTimeout** wygasł.

Te wpisy tylko widoczne w danych wyjściowych hello podczas hello uaktualnienie nie powiedzie się i uruchamia wycofywanie. Dalsze informacje są wyświetlane w zależności od typu hello hello błędu.

### <a name="investigate-upgrade-timeouts"></a>Zbadaj uaktualnienia limitów czasu
Uaktualnij limit błędów są najczęściej spowodowane problemów dotyczących dostępności usługi. dane wyjściowe Hello dalej w tym temacie jest typowe dla uaktualnienia gdzie repliki usługi lub wystąpienia awarii toostart w nowej wersji kodu hello. Witaj **UpgradeDomainProgressAtFailure** pola przechwytuje migawkę oczekującego uaktualnienia pracę w czasie hello awarii.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

W tym przykładzie hello uaktualnienie nie powiodło się w domenie uaktualnienia *MYUD1* i dwóch partycji (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* i *4b43f4d8-b26b-424e-9307-7a7a62e79750*) zostały zatrzymane. partycje Hello zostały zatrzymane powodu środowiska uruchomieniowego hello replik podstawowych tooplace (*WaitForPrimaryPlacement*) na węzłach docelowych *Node1* i *Węzeł4*.

Witaj **Get-ServiceFabricNode** polecenie może być używane tooverify, że te dwa węzły znajdują się w domenie uaktualnienia *MYUD1*. Witaj *UpgradePhase* mówi *PostUpgradeSafetyCheck*, co oznacza, że występuje kontrole bezpieczeństwa po we wszystkich węzłach w domenie uaktualnienia hello zakończeniu uaktualniania. Te informacje punktów tooa potencjalny problem z nową wersję kodu aplikacji hello hello. najbardziej typowe problemy Hello są błędy usługi hello open lub ścieżki kodu tooprimary podwyższania poziomu.

*UpgradePhase* z *PreUpgradeSafetyCheck* oznacza, że wystąpiły problemy przygotowanie domeny uaktualnienia hello, przed jego została wykonana. w takim przypadku Hello najczęściej występujących problemów są błędy usługi Zamknij hello lub obniżania poziomu od ścieżki głównej kodu.

Bieżący Hello **UpgradeState** jest *RollingBackCompleted*, więc hello oryginalnego uaktualniania należy wykonać o wycofaniu **FailureAction**, która automatycznie wycofane hello uaktualnienia w przypadku awarii. W przypadku uaktualniania oryginalnego hello ręcznego **FailureAction**, a następnie Uaktualnianie hello zamiast tego będzie w stanie wstrzymanym tooallow na żywo, debugowania aplikacji hello.

### <a name="investigate-health-check-failures"></a>Zbadaj błędy sprawdzania kondycji
Błędy sprawdzania kondycji mogą być wyzwalane przez różne problemy, które mogą wystąpić po zakończeniu wszystkich węzłów w domenie uaktualnienia, uaktualniania i przekazywania wszystkich kontroli bezpieczeństwa. dane wyjściowe Hello dalej w tym temacie jest typowe dla niepowodzenia uaktualnienia powodu toofailed kontroli kondycji. Witaj **UnhealthyEvaluations** pola przechwytuje migawki kontroli kondycji, których nie powiodła się w czasie hello uaktualnienia hello zgodnie z toohello określony [zasad dotyczących kondycji](service-fabric-health-introduction.md).

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

Najpierw niepowodzeń sprawdzenia kondycji do badania wymaga zrozumienia model kondycji sieci szkieletowej usług hello. Ale nawet bez takich dobrej znajomości, możemy stwierdzić, czy dwie usługi są w złej kondycji: *sieci szkieletowej: / DemoApp/Svc3* i *fabric: / DemoApp/Svc2*, wraz z raportów o kondycji błąd hello ("InjectedFault "w tym przypadku). W tym przykładzie dwóch spośród czterech usługi jest w złej kondycji, która jest poniżej wartości docelowej domyślne hello 0% złej kondycji (*MaxPercentUnhealthyServices*).

Witaj uaktualnienie zostało zawieszone po niepowodzeniu określając **FailureAction** w przypadku ręcznego uruchamiania hello uaktualnienia. Ten tryb umożliwia tooinvestigate hello systemu na żywo w stanie hello nie powiodło się przed podjęciem dalszych działań.

### <a name="recover-from-a-suspended-upgrade"></a>Odzyskiwanie z wstrzymane uaktualnienia
O wycofaniu **FailureAction**, jest odzyskanie nie jest wymagane, ponieważ uaktualnienie hello automatycznie przywraca po niepowodzeniu. Ręcznego **FailureAction**, dostępnych jest kilka opcji odzyskiwania:

1.  wyzwalacz wycofywania
2. Postępuj zgodnie z instrukcjami hello pozostałej części uaktualnienia hello ręcznie
3. Wznów hello monitorowane uaktualnienia

Witaj **Start ServiceFabricApplicationRollback** polecenie może być używany w żadnych toostart czasu wycofywanie aplikacji hello. Po polecenie hello zwraca pomyślnie, żądanie wycofania hello został zarejestrowany w systemie hello i rozpoczyna się w krótkim czasie.

Witaj **polecenie Resume-ServiceFabricApplicationUpgrade** , można użyć polecenia tooproceed za pośrednictwem hello pozostałej części hello ręcznie uaktualnić domeny uaktualnienia pojedynczo. W tym trybie bezpieczeństwa tylko testy są wykonywane przez hello system. Brak kondycji są sprawdzane. To polecenie można użyć tylko, gdy hello *UpgradeState* pokazuje *RollingForwardPending*, co oznacza, że bieżąca domena uaktualnienia hello zakończył uaktualnianie, ale hello obok jedną nie została uruchomiona (oczekiwanie).

Witaj **ServiceFabricApplicationUpgrade aktualizacji** polecenia mogą być używane tooresume hello monitorowane uaktualnienia z kontroli zdrowia i bezpieczeństwa są wykonywane.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

uaktualnienie Hello kontynuuje działanie od hello domeny uaktualnień, których ostatnio został wstrzymany i hello Użyj takie same parametry i zasady dotyczące kondycji jako przed uaktualniania. W razie potrzeby, parametry uaktualniania hello i zasady dotyczące kondycji pokazano hello poprzedzający dane wyjściowe można zmienić w hello same polecenia po wznowieniu pracy uaktualniania hello. W tym przykładzie hello uaktualnienie zostało wznowione w trybie monitorowanej hello parametrów i zasady dotyczące kondycji hello bez zmian.

## <a name="further-troubleshooting"></a>Dodatkowe informacje o rozwiązywaniu
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Sieć szkieletowa usług nie jest po hello określone zasady dotyczące kondycji
Możliwa przyczyna 1:

Sieć szkieletowa usług tłumaczy wszystkie wartości procentowe na rzeczywistą liczbę jednostek (na przykład replik, partycji i usług) do oceny kondycji i zawsze zaokrągla liczbę w górę toowhole jednostek. Na przykład, jeśli hello maksymalna *MaxPercentUnhealthyReplicasPerPartition* % 21 i istnieją pięciu replik, a następnie umożliwia sieci szkieletowej usług zapasową replik zła tootwo (czyli`Math.Ceiling (5*0.21)`). W związku z tym zasady dotyczące kondycji powinien być odpowiednio ustawiony.

Możliwe przyczyny 2:

Zasady dotyczące kondycji są określane w przeliczeniu na wartości procentowe całkowita usługi i wystąpień nie określonej usługi. Na przykład przed uaktualnieniem, jeśli aplikacja ma cztery usługi wystąpień A "," B "," C "i" D, w przypadku, gdy usługa D jest zła, ale mały wpływ toohello aplikacji. Chcemy hello tooignore znane usługi w złej kondycji D podczas hello uaktualnienia i ustawić parametr *MaxPercentUnhealthyServices* toobe 25%, przy założeniu, A, B i C muszą toobe dobrej kondycji.

Jednak podczas uaktualniania hello D mogą stać się dobra podczas C staje się nieprawidłowy. uaktualnienie Hello może nadal się powieść, ponieważ tylko 25% hello usługi jest w złej kondycji. Jednak może to spowodować nieprzewidziane błędy powodu tooC jest nieoczekiwanie zła zamiast D. W takiej sytuacji należy należy modelować D jako typ innej usługi, a, B i C. Ponieważ zasady dotyczące kondycji są określone dla typów usług, progi różnych Zła wartość procentowa może być zastosowane toodifferent usług. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Nie określono zasadę dla aplikacji, ale uaktualnienia hello nadal nie powiedzie się niektóre błędy przekroczenia limitu czasu, które nigdy nie została określona
Zasady dotyczące kondycji nie są udostępniane toohello żądanie uaktualnienia, będą pobierane z hello *ApplicationManifest.xml* hello bieżącej wersji aplikacji. Na przykład jeśli w przypadku uaktualniania z wersji 1.0 tooversion 2.0 X aplikacji, są używane zasady dotyczące kondycji aplikacji określone dla w wersji 1.0. Jeśli zasadę różnych powinny być używane do uaktualnienia hello hello zasad musi toobe określony jako część aplikacji hello uaktualnienia wywołanie interfejsu API. Witaj zasady określony jako część wywołania interfejsu API hello miały zastosowanie tylko podczas uaktualniania hello. Po ukończeniu uaktualniania hello hello zasad określonych w hello *ApplicationManifest.xml* są używane.

### <a name="incorrect-time-outs-are-specified"></a>Podano niepoprawny limity czasu
Może mieć zastanawiasz się o co się dzieje, gdy niespójnie przekroczeń limitu czasu. Na przykład może być *UpgradeTimeout* jest mniejsza niż hello *UpgradeDomainTimeout*. Witaj odpowiedzi jest zwracany jest błąd. Błędy są zwracane, jeśli hello *UpgradeDomainTimeout* jest mniejsza niż suma hello *HealthCheckWaitDuration* i *HealthCheckRetryTimeout*, lub jeśli  *UpgradeDomainTimeout* jest mniejsza niż suma hello *HealthCheckWaitDuration* i *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Moje uaktualnień trwa zbyt długo
Hello czas uaktualniania toocomplete zależy od hello kontroli kondycji i określić limity czasu. Sprawdzanie kondycji i limity czasu są zależne od czasu wykonywania toocopy, wdrażanie i ustabilizowania aplikacji hello. Trwa zbyt agresywnie z limitów czasu może to oznaczać więcej uaktualnienia nie powiodło się, dlatego zalecamy konserwatywnie począwszy od dłuższego limitu czasu.

Oto szybkie odświeżacz na interakcję hello przekroczeń limitu czasu z hello uaktualnienia razy:

Uaktualnia dla domeny uaktualnienia nie można ukończyć szybciej niż *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

Niepowodzenie uaktualniania nie może być szybsza niż *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

Witaj czas uaktualniania dla domeny uaktualnienia jest ograniczona przez *UpgradeDomainTimeout*.  Jeśli *HealthCheckRetryTimeout* i *HealthCheckStableDuration* są zarówno niezerowy i hello kondycji aplikacji hello śledzi przełączania i z powrotem, następnie uaktualnienie hello ostatecznie upłynie limit czasu na  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* rozpoczyna zliczanie raz hello uaktualnienia dla rozpoczyna hello bieżąca domena uaktualnienia.

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).

Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).
