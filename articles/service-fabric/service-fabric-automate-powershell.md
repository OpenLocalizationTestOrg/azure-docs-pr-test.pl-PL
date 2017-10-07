---
title: "Zarządzanie aplikacjami sieć szkieletowa usług Azure aaaAutomate | Dokumentacja firmy Microsoft"
description: "Wdrażanie, uaktualniania, przetestować i usuwanie aplikacji usługi Service Fabric przy użyciu programu PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>Automatyzowanie cyklem życia aplikacji hello przy użyciu programu PowerShell
Wiele aspektów hello [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md) można zautomatyzować.  W tym artykule opisano, jak toouse PowerShell tooautomate typowe zadania dla wdrażanie, uaktualnianie, usuwanie i testowanie aplikacji sieci szkieletowej usług Azure.  Zarządzane i dostępne są również interfejsy API protokołu HTTP do zarządzania aplikacjami. Zobacz [cykl życia aplikacji](service-fabric-application-lifecycle.md) Aby uzyskać więcej informacji.  

## <a name="prerequisites"></a>Wymagania wstępne
Przed przeniesieniem toohello zadań w artykule hello, należy koniecznie:

* Zapoznaj się z hello sieci szkieletowej usług pojęcia opisane w [techniczne omówienie sieci szkieletowej usług](service-fabric-technical-overview.md).
* [Instalowanie środowiska uruchomieniowego hello, zestawu SDK i narzędzia](service-fabric-get-started.md), co spowoduje również zainstalowanie hello **ServiceFabric** modułu programu PowerShell.
* [Włączanie wykonywania skryptów programu PowerShell](service-fabric-get-started.md#enable-powershell-script-execution).
* Uruchom klaster lokalny.  Uruchom nowe okno programu PowerShell jako administrator, a następnie uruchom skrypt instalacji klastra hello z folderu zestawu SDK hello:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Przed uruchomieniem żadnych poleceń programu PowerShell w tym artykule, za pomocą pierwszego połączenia lokalnego klastra usługi sieć szkieletowa toohello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* następujące zadania Hello wymagają toodeploy pakietu aplikacji v1 i v2 pakietu aplikacji do uaktualnienia. Pobierz hello [ **WordCount** Przykładowa aplikacja](http://aka.ms/servicefabricsamples) (znajdujący się w hello przykłady wprowadzenie). Tworzenie i pakietu aplikacji hello w programie Visual Studio (kliknij prawym przyciskiem myszy **WordCount** w Eksploratorze rozwiązań i wybierz **pakietu**). Kopiuj hello v1 pakiet w `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` zbyt`C:\Temp\WordCount`. Kopiuj `C:\Temp\WordCount` zbyt`C:\Temp\WordCountV2`, tworzenia pakietu aplikacji v2 hello do uaktualnienia. Otwórz `C:\Temp\WordCountV2\ApplicationManifest.xml` w edytorze tekstów. W hello **ApplicationManifest** element, zmień hello **ApplicationTypeVersion** atrybutu z "1.0.0" za "2.0.0" hello tooupdate numer wersji aplikacji. Zapisywanie pliku ApplicationManifest.xml hello zmienione.

## <a name="task-deploy-a-service-fabric-application"></a>Zadanie: Wdrażanie aplikacji sieci szkieletowej usług
Po wbudowane i spakowanej aplikacji hello (lub pobrany pakiet aplikacji hello), można wdrożyć aplikacji hello do lokalnego klastra usługi sieć szkieletowa usług. Wdrożenie obejmuje przekazywanie pakietu aplikacji hello, rejestrowania typu aplikacji hello i utworzenia wystąpienia aplikacji hello. Użyj instrukcji hello w tej sekcji toodeploy nowy klaster tooa aplikacji.

### <a name="step-1-upload-hello-application-package"></a>Krok 1: Przekaż pakiet aplikacji hello
Przekazywanie toohello pakietu aplikacji hello składnika image store umieszczane w składniki sieci szkieletowej usług toointernal dostępnych lokalizacji.  pakiet aplikacji Hello zawiera hello niezbędne manifest aplikacji, usługi manifesty i kodu, konfiguracji i aplikacja hello toocreate pakiety danych i wystąpień usługi. Pakiet aplikacji hello tooverify lokalnie, należy użyć hello [ServiceFabricApplicationPackage testu](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) polecenia cmdlet.  Witaj [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenia przekazywania hello pakietu. Na przykład:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Krok 2: Rejestracja typu aplikacji hello
Pakiet aplikacji hello rejestrowania sprawia, że hello typ i wersja aplikacji zadeklarowane w manifeście aplikacji hello dostępne do użycia. Hello system odczytuje pakietu hello przekazany w hello w kroku 1, sprawdź hello pakietu (równoważne toorunning [ServiceFabricApplicationPackage testu](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) lokalnie), przetworzyć zawartość pakietu hello i skopiować hello przetworzyć pakietu tooan Lokalizacja wewnętrznego systemu.  Uruchom hello [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
wszystkie typy aplikacji hello zarejestrowany w klastrze hello, uruchom hello toosee [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Krok 3: Tworzenie wystąpienia aplikacji hello
Aplikację można wdrożyć przy użyciu dowolnej wersji typu aplikacji, który został pomyślnie zarejestrowany za pomocą hello [ServiceFabricApplication nowy](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) polecenia. nazwy poszczególnych aplikacji Hello jest zadeklarowane na czas wdrażania i musi zaczynać się od hello **sieci szkieletowej:** schemat i być unikatowe dla każdego wystąpienia aplikacji. Witaj nazwy typu aplikacji, a wersja typu aplikacji są zadeklarowane w hello **ApplicationManifest.xml** pliku pakietu aplikacji hello. Jeśli wszystkie domyślne usługi zostały zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello, te są tworzone w tym momencie.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Witaj [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) polecenie wyświetla listę wszystkich wystąpień aplikacji, które zostały pomyślnie utworzone, wraz z ich ogólny stan. Witaj [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) polecenie wyświetla listę wszystkich wystąpień usługi hello, które zostały pomyślnie utworzone w ramach wystąpienia danej aplikacji. Domyślne usługi (jeśli istnieje) są wyświetlane.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Zadanie: Uaktualnienie aplikacji sieci szkieletowej usług
Można uaktualnić wdrożonej wcześniej aplikacji sieci szkieletowej usług z pakietu aplikacji zaktualizowane. To zadanie uaktualnienie aplikacji WordCount hello, który został wdrożony w "zadań: Wdrażanie aplikacji sieci szkieletowej usług." Zapoznaj się z artykułem [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md) Aby uzyskać więcej informacji.

prosty rzeczy tookeep, na przykład tylko hello numer wersji aplikacji został zaktualizowany w pakiecie aplikacji hello WordCountV2 utworzone hello wymagań wstępnych. Bardziej realistyczne scenariuszu jest stosowane aktualizowanie usługi plików kodu, konfiguracji lub danych, a następnie ponownie skompilować i pakowania aplikacji hello numerami zaktualizowanej wersji.  

### <a name="step-1-upload-hello-updated-application-package"></a>Krok 1: Hello Przekaż zaktualizowany pakiet aplikacji
WordCount v1 aplikacji Hello jest gotowy toobe uaktualniony. Jeśli Otwórz okno programu PowerShell jako administrator i wpisz [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), zobaczysz, że ta wersja 1.0.0 hello typ aplikacji WordCount jest wdrożony.  

Kopia hello zaktualizowania aplikacji pakietu toohello sieci szkieletowej usług magazynu w obrazie (gdzie hello pakiety aplikacji są przechowywane przez sieć szkieletowa usług). Witaj parametru **ApplicationPackagePathInImageStore** informuje o tym, gdzie można znaleźć pakietu aplikacji hello sieci szkieletowej usług. Witaj, następujące polecenia kopie hello pakiet aplikacji za**WordCountV2** w magazynie obrazu hello:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Krok 2: Hello rejestru zaktualizowany typ aplikacji
Witaj następnym krokiem jest tooregister hello nowej wersji aplikacji hello z sieci szkieletowej usług, które mogą być wykonywane przy użyciu hello [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Krok 3: Uruchom hello uaktualniania
Różnych parametrów uaktualnienia, limity czasu i kryteria kondycji mogą być zastosowane tooapplication uaktualnienia. Zapoznaj się z artykułem hello [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) i [procesu uaktualniania](service-fabric-application-upgrade.md) toolearn więcej dokumentów. Wszystkie usługi i wystąpień powinna być *dobrej kondycji* po uaktualnieniu hello.  Zestaw hello **HealthCheckStableDuration** too60 sekund (tak, aby hello usługi są w dobrej kondycji, co najmniej 20 sekund przed hello uaktualnianie będzie kontynuowane toohello uaktualnić obok domeny).  Także zestaw hello **UpgradeDomainTimeout** too1200 sekund i hello **UpgradeTimeout** too3000 sekund. Wreszcie, ustaw hello **UpgradeFailureAction** za**wycofywania**, która żądań, które przywraca sieci szkieletowej usług hello aplikacji toohello poprzedniej wersji, jeśli nie zostaną napotkane błędy podczas uaktualniania.

Można teraz uruchomić uaktualniania aplikacji hello przy użyciu hello [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Uwaga tej nazwy aplikacji hello jest hello takie same jak hello wcześniej wdrożona v1.0.0 nazwy aplikacji (fabric: / WordCount). Sieć szkieletowa usług używa tego tooidentify nazwę, która aplikacja jest wprowadzenie uaktualniony. Jeśli ustawisz toobe limity czasu hello jest zbyt krótki, może wystąpić komunikat o błędzie limitu czasu czy stanów hello problem. Odwołuje się zbyt[Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md), lub zwiększ hello przekroczeń limitu czasu.

### <a name="step-4-check-upgrade-progress"></a>Krok 4: Postęp uaktualniania wyboru
Możesz monitorować postęp uaktualniania aplikacji przy użyciu [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), lub za pomocą hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

W ciągu kilku minut hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia cmdlet pokazuje, że wszystkie domeny uaktualnienia zostały uaktualnione (ukończone).

## <a name="task-test-a-service-fabric-application"></a>Zadanie: Testów aplikacji sieci szkieletowej usług
toowrite wysokiej jakości usług, deweloperzy muszą toobe tooinduce stanie zawodnych infrastruktury błędów tootest hello stabilność swoich usług. Sieć szkieletowa usług zapewnia deweloperom hello możliwości tooinduce błędów akcje i usług testu w hello występowania błędów przy użyciu hello scenariuszy testowania chaos i trybu failover.  Zapoznaj się z artykułem [toohello wprowadzenie błędów Analysis Service](service-fabric-testability-overview.md) Aby uzyskać dodatkowe informacje.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Krok 1: Uruchom Scenariusz testów chaos hello
Scenariusz testów chaos Hello generuje błędy między hello całego klastra sieci szkieletowej usług. Scenariusz Hello kompresuje błędów zwykle widoczne za pośrednictwem tooa miesięcy lub lat. kilka godzin. Kombinacja Hello przeplotem błędów z wartością wysoką odporność znajduje sytuacjach wyjątkowych, które w przeciwnym razie być pominięte. Witaj poniższym przykładzie uruchamiane są scenariusza testów chaos hello przez 60 minut.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Krok 2: Uruchom scenariusz test pracy awaryjnej hello
Hello trybu failover przetestuj cele scenariusz partycji określonej usługi, zamiast całego klastra hello i innych usług pozostawia nie dotyczy. Scenariusz Hello iterację sekwencję symulowane błędy podczas weryfikowania usługi podczas wykonywania logiki biznesowej. Błąd podczas weryfikowania usługi wskazuje problem, który wymaga dalszego badania. test pracy awaryjnej Hello wywołuje tylko jeden błąd w czasie, jako min. toohello chaos testu scenariusza, który można wywołać wiele błędów. Witaj poniższy przykład jest uruchamiana test pracy awaryjnej hello przez 60 minut dla sieci szkieletowej hello: / WordCount/usługi WordCountService usługi.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Zadanie: Usuwanie aplikacji sieci szkieletowej usług
Można usunąć wystąpienia wdrożonej aplikacji, Usuń typ aplikacji hello udostępnione z klastra hello i usuwanie pakietu aplikacji hello z hello magazynu ImageStore.

### <a name="step-1-remove-an-application-instance"></a>Krok 1: Usuwanie wystąpienia aplikacji
Wystąpienie aplikacji nie jest już potrzebne, możesz trwale usunąć go przy użyciu hello [ServiceFabricApplication Usuń](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet. Automatycznie spowoduje to usunięcie wszystkich usług należących toohello aplikacji, trwałe usunięcie wszystkich stan usługi. Ta operacja jest nieodwracalna i nie można odzyskać stan aplikacji.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Krok 2: Wyrejestruj typ aplikacji hello
W przypadku konkretnej wersji typu aplikacji nie są już potrzebne, wyrejestrować go za pomocą hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet. Wyrejestrowywanie typy nieużywane wersje miejsca do magazynowania używanych przez pakiet aplikacji hello w magazynie obraz powitania. Typ aplikacji można wyrejestrować tak długo, jak żadne aplikacje nie wystąpienia na nim lub do czasu uaktualnienia aplikacji odwołuje.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Krok 3: Usunięcie pakietu aplikacji hello
Po typ aplikacji hello jest zarejestrowany, pakiet aplikacji hello można usunąć z magazynu obrazów hello przy użyciu hello [ServiceFabricApplicationPackage Usuń](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) polecenia cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Następne kroki
[Cykl życia aplikacji w sieci szkieletowej usług](service-fabric-application-lifecycle.md)

[Wdrażanie aplikacji](service-fabric-deploy-remove-applications.md)

[Uaktualnianie aplikacji](service-fabric-application-upgrade.md)

[Polecenia cmdlet systemu Azure sieci szkieletowej usług](/powershell/azure/overview?view=azureservicefabricps)

