---
title: 'Uaktualnianie aplikacji: parametry uaktualnienia | Dokumentacja firmy Microsoft'
description: "W tym artykule opisano parametry tooupgrading powiązanych aplikacji usługi Service Fabric, w tym kondycji kontroli zasad i tooperform tooautomatically cofania hello uaktualnienia."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Parametry uaktualniania aplikacji
W tym artykule opisano hello różnych parametrów, które są stosowane podczas hello uaktualniania aplikacji sieci szkieletowej usług Azure. Parametry Hello zawierają hello nazwa i wersja aplikacji hello. Są one pokrętła określające hello limity czasu i kontroli kondycji, które są stosowane podczas uaktualniania hello i określają hello zasady, które należy zastosować w przypadku niepowodzenia uaktualnienia.

<br>

| Parametr | Opis |
| --- | --- |
| ApplicationName |Nazwa aplikacji hello, który jest uaktualniany. Przykłady: fabric: / VisualObjects, fabric: / ClusterMonitor |
| TargetApplicationTypeVersion |wersję Hello typu aplikacji hello hello cele uaktualniania. |
| FailureAction |Hello akcję wykonywaną przez sieć szkieletowa usług w przypadku nieudanego uaktualnienia hello. Aplikacja Hello może zostać przywrócona toohello wersji poprzedzającej wersję update (wycofywania) lub hello uaktualnienia może być zatrzymana na powitania bieżąca domena uaktualnienia. W drugim przypadku hello tryb uaktualniania hello jest również tooManual zmienione. Dozwolone wartości to wycofywania i ręczne. |
| HealthCheckWaitDurationSec |Witaj toowait czas (w sekundach) po uaktualnieniu hello zakończył w domenie uaktualnienia hello przed hello kondycji aplikacji hello ocenia sieci szkieletowej usług. Ten czas trwania mogą również być uważane hello razem, gdy aplikacja powinna być uruchomiona, zanim mogą zostać uwzględnione dobrej kondycji. Jeśli sprawdzenie kondycji hello zakończy się pomyślnie, proces uaktualniania hello przebieg toohello następnej domeny uaktualnienia.  W przypadku niepowodzenia sprawdzania kondycji hello sieci szkieletowej usług czeka na interwał (hello UpgradeHealthCheckInterval) przed ponowną próbą wykonania sprawdzenia kondycji hello ponownie do czasu hello osiągnięty HealthCheckRetryTimeout. Hello domyślną i zalecaną wartość wynosi 0 sekund. |
| HealthCheckRetryTimeoutSec |Witaj czas trwania (w sekundach) usługi sieć szkieletowa nadal oceny kondycji tooperform przed zadeklarowaniem hello uaktualnienia, ponieważ nie powiodło się. Domyślna Hello to 600 sekund. Ten czas trwania rozpoczyna się po osiągnięciu HealthCheckWaitDuration. W tym HealthCheckRetryTimeout sieci szkieletowej usług może być sprawdzana jest wiele kondycji o kondycji aplikacji hello. Hello wartość domyślna to 10 minut i należy odpowiednio dostosować aplikacji. |
| HealthCheckStableDurationSec |Witaj tooverify czas trwania (w sekundach), czy aplikacja hello jest stabilna przed przenoszenie toohello następnej domeny uaktualnienia lub zakończeniu hello uaktualnienia. Ten czas trwania oczekiwania jest używane tooprevent wykryte zmiany kondycji prawo po wykonaniu hello sprawdzania kondycji. Wartość domyślna Hello jest 120 sekund i należy odpowiednio dostosować aplikacji. |
| UpgradeDomainTimeoutSec |Maksymalny czas (w sekundach) dla uaktualnienia pojedynczej domeny uaktualnienia. Po osiągnięciu tego limitu czasu uaktualnienia hello zatrzymuje i będzie kontynuowana, oparte na powitania ustawienie UpgradeFailureAction. nigdy nie jest wartością domyślną Hello (Infinite) i należy odpowiednio dostosować aplikacji. |
| UpgradeTimeout |Limit (w sekundach), która ma zastosowanie do całego uaktualnienia hello. Po osiągnięciu tego limitu czasu hello uaktualnienia zatrzymuje i UpgradeFailureAction zostanie wywołany. nigdy nie jest wartością domyślną Hello (Infinite) i należy odpowiednio dostosować aplikacji. |
| UpgradeHealthCheckInterval |częstotliwość Hello zaznaczono hello stan kondycji. Ten parametr jest określony w hello ClusterManager części hello *klastra* *manifestu*i nie jest określony jako część polecenia cmdlet uaktualnienia hello. Witaj, wartość domyślna to 60 sekund. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Oceny kondycji usługi podczas uaktualniania aplikacji
<br>
kryteria oceny kondycji Hello są opcjonalne. Jeśli po uruchomieniu uaktualniania nie określono kryteriów oceny kondycji hello, sieć szkieletowa usług korzysta z zasad dotyczących kondycji aplikacji hello określone w hello ApplicationManifest.xml wystąpienia aplikacji hello.

<br>

| Parametr | Opis |
| --- | --- |
| Elementów ConsiderWarningAsError |Wartość domyślna to False. Traktuj hello kondycji ostrzeżenia dla aplikacji hello jako błędy podczas oceny kondycji hello aplikacji hello podczas uaktualniania. Domyślnie usługi sieć szkieletowa nie może oszacować ostrzeżenie kondycji zdarzenia toobe błędów (błędy), można kontynuować uaktualniania hello, nawet jeśli istnieją zdarzenia ostrzegawcze. |
| MaxPercentUnhealthyDeployedApplications |Domyślną i zalecaną wartością jest 0. Określ maksymalną liczbę wdrożonych aplikacji hello (zobacz hello [sekcji kondycji](service-fabric-health-introduction.md)) które może być nieprawidłowy, przed aplikacji hello jest określana jako zła i uaktualniania hello kończy się niepowodzeniem. Ten parametr określa kondycji aplikacji hello w węźle hello i pomaga wykrywać problemy podczas uaktualniania. Zazwyczaj hello replik aplikacji hello Pobierz równoważeniem obciążenia toohello innego węzła, dzięki czemu tooappear aplikacji hello dobrej kondycji, dzięki czemu hello tooproceed uaktualnienia. Określając strict kondycji MaxPercentUnhealthyDeployedApplications usługi sieć szkieletowa można wykrycie problem z pakietem aplikacji hello szybko i utworzyć błędu szybkiego uaktualnienia. |
| MaxPercentUnhealthyServices |Domyślną i zalecaną wartością jest 0. Określ maksymalną liczbę usług hello w hello wystąpienia aplikacji, która może być nieprawidłowy, zanim aplikacji hello jest określana jako zła, a nie uaktualnienie hello. |
| MaxPercentUnhealthyPartitionsPerService |Domyślną i zalecaną wartością jest 0. Określ maksymalną liczbę partycji hello usługi, który może być zła, zanim usługa hello jest określana jako zła. |
| MaxPercentUnhealthyReplicasPerPartition |Domyślną i zalecaną wartością jest 0. Określ maksymalną liczbę replik hello w partycji, która może być nieprawidłowy, zanim hello partycji jest określana jako zła. |
| UpgradeReplicaSetCheckTimeout |**Usługi bezstanowej**— w ramach pojedynczej domeny uaktualnienia sieci szkieletowej usług próbuje tooensure, że dostępne są dodatkowe wystąpienia usługi hello. Jeśli liczba wystąpień docelowych hello jest więcej niż jeden, Service Fabric czeka na więcej niż jednego wystąpienia toobe dostępne w górę tooa maksymalną wartość limitu czasu. Ten limit czasu został określony przy użyciu właściwości UpgradeReplicaSetCheckTimeout hello. Po przekroczeniu limitu czasu hello, Service Fabric kontynuuje hello uaktualnienia, niezależnie od hello liczbę wystąpień usługi. Jeśli liczba wystąpień docelowych hello, usługi sieć szkieletowa nie oczekuje i natychmiast kontynuuje hello uaktualnienia. **Usługi stanowej**— w ramach pojedynczej domeny uaktualnienia sieci szkieletowej usług próbuje tooensure, który hello repliki zestaw ma kworum. Sieć szkieletowa usług czeka toobe kworum dostępne w górę tooa maksymalną wartość limitu czasu (określonego przez właściwość UpgradeReplicaSetCheckTimeout hello). Po przekroczeniu limitu czasu hello, Service Fabric kontynuuje hello uaktualnienia, niezależnie od kworum. To ustawienie jest zestaw jak nigdy (infinite) stopniowych do przodu i 900 sekund po wycofanie. |
| ForceRestart |Po aktualizacji konfiguracji lub danych pakietu bez aktualizowania kodu usługi hello hello ponownego uruchomienia usługi tylko wtedy, gdy właściwość ForceRestart hello jest tootrue. Po zakończeniu aktualizacji hello sieci szkieletowej usług powiadamia usługi hello pakiet konfiguracji lub pakiet danych jest dostępna. Witaj usługa jest odpowiedzialna za stosowanie hello zmian. W razie potrzeby hello usługi można ponownie uruchomić się. |

<br>
<br>
kryteria MaxPercentUnhealthyServices, MaxPercentUnhealthyPartitionsPerService i MaxPercentUnhealthyReplicasPerPartition Hello może być określona dla typu usługi dla wystąpienia aplikacji. Ustawienie tych parametrów dla usługi umożliwia aplikacji toocontain różnych usług typów z różnych wersji ewaluacyjnej zasadami. Na przykład typ usługi bezstanowej bramy może mieć MaxPercentUnhealthyPartitionsPerService, który jest inny niż typ usługi stanowej aparat wystąpienie aplikacji.

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

[Uaktualnianie aplikacji w systemie Linux przy użyciu interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-application-lifecycle-sfctl.md#upgrade-application) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu interfejsu wiersza polecenia usługi sieci szkieletowej.

[Uaktualnianie aplikacji za pomocą wtyczki Eclipse sieci szkieletowej usług](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).

Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).
