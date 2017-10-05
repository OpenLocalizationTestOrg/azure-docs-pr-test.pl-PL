---
title: "Automatyczne zarządzanie aplikacji sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: fb3c2a77ea887289eebf343e223c190781d0e4c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automate-the-application-lifecycle-using-powershell"></a>Automatyzowanie cyklem życia aplikacji przy użyciu programu PowerShell
Wiele aspektów [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md) można zautomatyzować.  W tym artykule pokazano, jak za pomocą programu PowerShell do automatyzacji typowych zadań związanych z wdrażanie, uaktualnianie, usuwanie i testowanie aplikacji sieci szkieletowej usług Azure.  Zarządzane i dostępne są również interfejsy API protokołu HTTP do zarządzania aplikacjami. Zobacz [cykl życia aplikacji](service-fabric-application-lifecycle.md) Aby uzyskać więcej informacji.  

## <a name="prerequisites"></a>Wymagania wstępne
Przed przeniesieniem do zadań w artykule należy koniecznie:

* Zapoznaj się z sieci szkieletowej usług pojęcia opisane w [techniczne omówienie sieci szkieletowej usług](service-fabric-technical-overview.md).
* [Instalowanie środowiska uruchomieniowego, zestawu SDK i narzędzia](service-fabric-get-started.md), co spowoduje również zainstalowanie **ServiceFabric** modułu programu PowerShell.
* [Włączanie wykonywania skryptów programu PowerShell](service-fabric-get-started.md#enable-powershell-script-execution).
* Uruchom klaster lokalny.  Uruchom nowe okno programu PowerShell jako administrator, a następnie uruchom skrypt instalacji klastra z folderu zestawu SDK:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Przed uruchomieniem żadnych poleceń programu PowerShell w tym artykule, najpierw połączyć się z lokalnym klastrem usługi sieć szkieletowa usług za pomocą [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Następujące zadania wymagają v1 pakiet aplikacji do wdrożenia i pakiet aplikacji w wersji 2 do uaktualnienia. Pobierz [ **WordCount** Przykładowa aplikacja](http://aka.ms/servicefabricsamples) (znajdujący się w przykładach wprowadzenie). Tworzenie i pakietu aplikacji w programie Visual Studio (kliknij prawym przyciskiem myszy **WordCount** w Eksploratorze rozwiązań i wybierz **pakietu**). Skopiuj pakiet v1 w `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` do `C:\Temp\WordCount`. Kopiuj `C:\Temp\WordCount` do `C:\Temp\WordCountV2`, tworzenia pakietu aplikacji w wersji 2 do uaktualnienia. Otwórz `C:\Temp\WordCountV2\ApplicationManifest.xml` w edytorze tekstów. W **ApplicationManifest** elementu, zmień **ApplicationTypeVersion** atrybut z "1.0.0" do "2.0.0", aby zaktualizować numer wersji aplikacji. Zapisać zmienionego pliku ApplicationManifest.xml.

## <a name="task-deploy-a-service-fabric-application"></a>Zadanie: Wdrażanie aplikacji sieci szkieletowej usług
Po wbudowane i spakowanej aplikacji (lub pobrany pakiet aplikacji), możesz wdrożyć aplikację do lokalnego klastra usługi sieć szkieletowa usług. Wdrożenie obejmuje przekazywanie pakietu aplikacji, rejestrowania typu aplikacji i utworzenia wystąpienia aplikacji. Aby wdrożyć nową aplikację do klastra, wykonaj instrukcje w tej sekcji.

### <a name="step-1-upload-the-application-package"></a>Krok 1: Przekaż pakiet aplikacji
Przekazywanie pakietu aplikacji do magazynu w obrazie umieszcza je w lokalizacji dostęp do wewnętrznych składników usługi Service Fabric.  Pakiet aplikacji zawiera niezbędną konfigurację manifest aplikacji, usługi deklaracje oraz kod, a pakiety danych do tworzenia aplikacji i wystąpień usługi. Jeśli chcesz sprawdzić lokalnie pakietu aplikacji, użyj [ServiceFabricApplicationPackage testu](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) polecenia cmdlet.  [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenia zostanie przesłany pakiet. Na przykład:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-the-application-type"></a>Krok 2: Rejestracja typu aplikacji
Rejestracja pakietu aplikacji sprawia, że typ aplikacji i wersji zadeklarowane w manifeście aplikacji dostępne do użycia. Odczyty systemu przekazany pakiet w kroku 1, sprawdź pakiet (odpowiednikiem uruchomiona [ServiceFabricApplicationPackage testu](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) lokalnie), przetwarzają zawartość pakietu i skopiuj przetworzonych pakiet do wewnętrznego systemowego Lokalizacja.  Uruchom [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
Aby wyświetlić wszystkie typy aplikacji zarejestrowany w klastrze, uruchom [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-the-application-instance"></a>Krok 3: Tworzenie instancji aplikacji
Aplikację można wdrożyć przy użyciu dowolnej wersji typu aplikacji, który został pomyślnie zarejestrowany za pomocą [ServiceFabricApplication nowy](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) polecenia. Nazwy poszczególnych aplikacji jest zadeklarowane na czas wdrażania i musi zaczynać się od **sieci szkieletowej:** schemat i być unikatowe dla każdego wystąpienia aplikacji. Nazwa typu aplikacji i wersja typu aplikacji, które są zadeklarowane w **ApplicationManifest.xml** pliku pakietu aplikacji. Jeśli wszystkie domyślne usługi zostały zdefiniowane w manifeście aplikacji typu aplikacji docelowej, te są tworzone w tym momencie.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

[Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) polecenie wyświetla listę wszystkich wystąpień aplikacji, które zostały pomyślnie utworzone, wraz z ich ogólny stan. [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) polecenie wyświetla listę wszystkich wystąpień usługi, które zostały pomyślnie utworzone w ramach wystąpienia danej aplikacji. Domyślne usługi (jeśli istnieje) są wyświetlane.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Zadanie: Uaktualnienie aplikacji sieci szkieletowej usług
Można uaktualnić wdrożonej wcześniej aplikacji sieci szkieletowej usług z pakietu aplikacji zaktualizowane. To zadanie uaktualnienie aplikacji WordCount, który został wdrożony w "zadań: Wdrażanie aplikacji sieci szkieletowej usług." Zapoznaj się z artykułem [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md) Aby uzyskać więcej informacji.

Aby zachować proste, w tym przykładzie rzeczy, numer wersji aplikacji został zaktualizowany w pakiecie aplikacji WordCountV2 utworzone w wymaganiach wstępnych. Bardziej realistyczne scenariuszu jest stosowane aktualizowanie usługi plików kodu, konfiguracji lub danych, a następnie ponownie skompilować i pakowania aplikacji z numerami zaktualizowanej wersji.  

### <a name="step-1-upload-the-updated-application-package"></a>Krok 1: Przekaż pakiet aplikacji zaktualizowane
Aplikacja WordCount v1 jest gotowy do uaktualnienia. Jeśli Otwórz okno programu PowerShell jako administrator i wpisz [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), zostanie wyświetlony tej wersji 1.0.0 typu aplikacja WordCount jest wdrażana.  

Teraz Skopiuj pakiet zaktualizowaną aplikację do magazynu obrazów platformy Service Fabric (gdzie pakiety aplikacji są przechowywane przez usługi sieć szkieletowa). Parametr **ApplicationPackagePathInImageStore** informuje o tym, gdzie można znaleźć pakietu aplikacji sieci szkieletowej usług. Polecenie kopiuje pakiet aplikacji do **WordCountV2** w magazynie obrazu:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-the-updated-application-type"></a>Krok 2: Rejestracja typu aplikacji zaktualizowane
Następnym krokiem jest można zarejestrować nowej wersji aplikacji w sieci szkieletowej usług, które można wykonać za pomocą [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-the-upgrade"></a>Krok 3: Uruchom operację uaktualniania
Różne parametry uaktualnienia, limity czasu i kryteria kondycji mogą być stosowane do uaktualniania aplikacji. Zapoznaj się z artykułem [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) i [procesu uaktualniania](service-fabric-application-upgrade.md) dokumentów, aby dowiedzieć się więcej. Wszystkie usługi i wystąpień powinna być *dobrej kondycji* po uaktualnieniu.  Ustaw **HealthCheckStableDuration** do 60 sekund (tak, aby co najmniej 20 sekund przed uaktualnienia przechodzi do następnej domeny uaktualnienia usługi są w dobrej kondycji).  Również ustawić **UpgradeDomainTimeout** 1200 sekund i **UpgradeTimeout** 3000 sekund. Wreszcie, ustaw **UpgradeFailureAction** do **wycofywania**, który żąda czy sieci szkieletowej usług wycofuje aplikacji do poprzedniej wersji występują błędy podczas uaktualniania.

Można teraz uruchomić uaktualnienie aplikacji przy użyciu [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Należy pamiętać, że nazwa aplikacji jest taka sama jak nazwa aplikacji wdrożonej wcześniej v1.0.0 (fabric: / WordCount). Sieć szkieletowa usług używa tej nazwy do identyfikowania, która aplikacja jest wprowadzenie uaktualniony. Jeśli ustawisz limity czasu się zbyt krótki, może wystąpić komunikat o błędzie limitu czasu, stwierdzający problem. Zapoznaj się [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md), lub zwiększ wartość limitu czasu.

### <a name="step-4-check-upgrade-progress"></a>Krok 4: Postęp uaktualniania wyboru
Możesz monitorować postęp uaktualniania aplikacji przy użyciu [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), lub za pomocą [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

W ciągu kilku minut [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia cmdlet pokazuje, że wszystkie domeny uaktualnienia zostały uaktualnione (ukończone).

## <a name="task-test-a-service-fabric-application"></a>Zadanie: Testów aplikacji sieci szkieletowej usług
Aby napisać wysokiej jakości usług, deweloperzy muszą móc wywoływać błędy zawodnych infrastruktury do testowania stabilność swoich usług. Sieć szkieletowa usług zapewnia deweloperom możliwość wywoływać akcje usterek i przetestować usługi w razie awarii za pomocą scenariuszy testowania chaos i pracy awaryjnej.  Zapoznaj się z artykułem [wprowadzenie do usługi analiza błędów](service-fabric-testability-overview.md) Aby uzyskać dodatkowe informacje.

### <a name="step-1-run-the-chaos-test-scenario"></a>Krok 1: Uruchom chaos scenariusza testów
Scenariusz testów chaos generuje błędy w ramach całego klastra sieci szkieletowej usług. Scenariusz kompresuje błędów zwykle widoczne za pośrednictwem miesięcy lub lat do kilku godzin. Kombinacja przeplotem błędów z wartością wysoką odporność znajduje sytuacjach wyjątkowych, które w przeciwnym razie być pominięte. W poniższym przykładzie uruchamiane scenariusza testów chaos przez 60 minut.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-the-failover-test-scenario"></a>Krok 2: Uruchom scenariusz test trybu failover
Przejście w tryb failover przetestuj cele scenariusz partycji określonej usługi, zamiast całego klastra i innych usług pozostawia nie mają wpływu. Scenariusz iterację sekwencję symulowane błędy podczas weryfikowania usługi podczas wykonywania logiki biznesowej. Błąd podczas weryfikowania usługi wskazuje problem, który wymaga dalszego badania. Test pracy awaryjnej wywołuje tylko jeden błąd w czasie, w przeciwieństwie do scenariusza testów chaos, które może wywołać wiele błędów. W poniższym przykładzie uruchamiane test pracy awaryjnej przez 60 minut przed sieci szkieletowej: / WordCount/usługi WordCountService usługi.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Zadanie: Usuwanie aplikacji sieci szkieletowej usług
Można usunąć wystąpienia wdrożonej aplikacji, Usuń typ elastycznie aplikacji z klastra i usuwanie pakietu aplikacji w składniku ImageStore.

### <a name="step-1-remove-an-application-instance"></a>Krok 1: Usuwanie wystąpienia aplikacji
Wystąpienie aplikacji nie jest już potrzebne, możesz trwale usunąć go za pomocą [ServiceFabricApplication Usuń](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet. To również automatycznie usuwa wszystkie usługi należące do aplikacji, trwałe usunięcie wszystkich stan usługi. Ta operacja jest nieodwracalna i nie można odzyskać stan aplikacji.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-the-application-type"></a>Krok 2: Wyrejestruj typ aplikacji
W przypadku konkretnej wersji typu aplikacji nie są już potrzebne, wyrejestrować go za pomocą [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet. Wyrejestrowywanie typy nieużywane wersje miejsca używanego przez pakiet aplikacji w sklepie obrazu. Typ aplikacji można wyrejestrować tak długo, jak żadne aplikacje nie wystąpienia na nim lub do czasu uaktualnienia aplikacji odwołuje.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-the-application-package"></a>Krok 3: Usunięcie pakietu aplikacji
Po typem aplikacji jest zarejestrowany, pakiet aplikacji można usunąć z magazynu obrazów za pomocą [ServiceFabricApplicationPackage Usuń](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) polecenia cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Następne kroki
[Cykl życia aplikacji w sieci szkieletowej usług](service-fabric-application-lifecycle.md)

[Wdrażanie aplikacji](service-fabric-deploy-remove-applications.md)

[Uaktualnianie aplikacji](service-fabric-application-upgrade.md)

[Polecenia cmdlet systemu Azure sieci szkieletowej usług](/powershell/azure/overview?view=azureservicefabricps)

