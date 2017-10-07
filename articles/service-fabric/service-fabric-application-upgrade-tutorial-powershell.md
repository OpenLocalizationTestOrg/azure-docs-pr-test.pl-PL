---
title: "Uaktualnianie aplikacji Fabric aaaService przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono hello środowisko wdrażania aplikacji usługi Service Fabric, zmiana kodu hello i wprowadza uaktualnienia przy użyciu programu PowerShell."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Uaktualnianie aplikacji sieci szkieletowej usług za pomocą programu PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Program Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Hello najczęściej używane i zalecane podejście uaktualnienia uaktualnienia stopniowego hello monitorowane.  Sieć szkieletowa usług Azure monitoruje kondycję hello aplikacji hello uaktualniany na podstawie zestawu zasad dotyczących kondycji. Po uaktualnieniu domeny aktualizacji (UD) usługi sieć szkieletowa ocenia kondycji aplikacji hello i przechodzi dalej domeny aktualizacji toohello lub nie powiedzie się uaktualnienie hello w zależności od zasad dotyczących kondycji hello.

Uaktualnienie monitorowanej aplikacji można przeprowadzić przy użyciu hello zarządzane lub macierzystych interfejsów API, programu PowerShell lub REST. Aby uzyskać instrukcje dotyczące wykonywania uaktualnienia przy użyciu programu Visual Studio, zobacz [uaktualniania aplikacji przy użyciu programu Visual Studio](service-fabric-application-upgrade-tutorial.md).

Stopniowe monitorowania sieci szkieletowej usług administrator aplikacji hello umożliwiają konfigurowanie zasad oceny kondycji hello sieci szkieletowej usług używa toodetermine, jeśli aplikacja hello jest w dobrej kondycji. Ponadto hello administrator można skonfigurować hello toobe działania podejmowane podczas oceny kondycji hello zakończy się niepowodzeniem (na przykład podczas automatycznego wycofania.) Ta sekcja przeprowadzi Cię przez monitorowanych uaktualnienia dla jednego z hello SDK przykłady, które korzysta z programu PowerShell. Witaj poniższe wideo Microsoft Virtual Academy również przeprowadzi Cię przez kolejne uaktualnienia aplikacji:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Krok 1: Tworzenie i wdrażanie hello obiektów Visual próbki
Tworzenie i publikowanie aplikacji hello, klikając prawym przyciskiem myszy projekt aplikacji hello, **VisualObjectsApplication,** i wybierając hello **publikowania** polecenia.  Aby uzyskać więcej informacji, zobacz [samouczek uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade-tutorial.md).  Alternatywnie można użyć programu PowerShell toodeploy aplikacji.

> [!NOTE]
> Przed jakichkolwiek poleceń usługi sieć szkieletowa hello mogą być używane w programu PowerShell, należy najpierw tooconnect toohello klastra przy użyciu hello `Connect-ServiceFabricCluster` polecenia cmdlet. Podobnie założono, że powitalne klastra nie został już skonfigurowany na komputerze lokalnym. Zobacz artykuł hello na [konfigurowania środowiska deweloperskiego sieci szkieletowej usług](service-fabric-get-started.md).
> 
> 

Po utworzeniu hello projektu programu Visual Studio, możesz użyć polecenia środowiska PowerShell hello [ServiceFabricApplicationPackage kopiowania](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy hello aplikacji pakietu toohello magazynu ImageStore. Pakiet aplikacji hello tooverify lokalnie, należy użyć hello [ServiceFabricApplicationPackage testu](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) polecenia cmdlet. Witaj następnym krokiem jest tooregister hello toohello sieci szkieletowej usług plik wykonywalny aplikacji przy użyciu hello [ServiceFabricApplicationPackage rejestru](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) polecenia cmdlet. Witaj ostatnim krokiem jest toostart wystąpienie aplikacji hello przy użyciu hello [ServiceFabricApplication nowy](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet.  Te trzy kroki są podobne toousing hello **Wdróż** element menu w programie Visual Studio.

Teraz, można użyć [Service Fabric Explorer tooview hello klastra i hello aplikacji](service-fabric-visualizing-your-cluster.md). Witaj aplikacja ma usługi sieci web, którą można nawigować tooin programu Internet Explorer, wpisując [http://localhost: 8081/visualobjects](http://localhost:8081/visualobjects) na pasku adresu hello.  Niektóre obiekty visual przestawne przenoszenia na ekranie powitania powinna zostać wyświetlona.  Ponadto można użyć [Get ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) stanu aplikacji hello toocheck.

## <a name="step-2-update-hello-visual-objects-sample"></a>Krok 2: Aktualizacja hello obiektów Visual próbki
Można zauważyć, że z wersją hello, który został wdrożony w kroku 1, obiektów visual hello nie Obróć. Uaktualnij teraz tooone tej aplikacji, gdzie obiektów visual hello również Obróć.

Wybierz hello VisualObjects.ActorService projektu w ramach hello VisualObjects rozwiązania, a następnie otwórz plik StatefulVisualObjectActor.cs hello. W tym pliku Przejdź metody toohello `MoveObject`, komentarz `this.State.Move()`i Usuń komentarz `this.State.Move(true)`. Ta zmiana obraca obiekty powitania po uaktualnieniu hello usługi.

Potrzebujemy tooupdate hello *ServiceManifest.xml* pliku (w ramach elementu PackageRoot) projektu hello **VisualObjects.ActorService**. Aktualizacja hello *elementu CodePackage* hello too2.0 wersji usługi i hello odpowiednich wierszy w hello *ServiceManifest.xml* pliku.
Można użyć programu Visual Studio hello *edytować pliki manifestu* opcję po kliknięciu prawym przyciskiem myszy na zmiany hello toomake hello rozwiązania w pliku manifestu.

Po dokonaniu zmiany hello hello manifest powinna wyglądać następujące hello (wyróżniony części Pokaż zmiany hello):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Teraz hello *ApplicationManifest.xml* pliku (w obszarze hello **VisualObjects** projektu w obszarze hello **VisualObjects** rozwiązania) jest zaktualizowane tooversion 2.0 z hello  **VisualObjects.ActorService** projektu. Ponadto wersja aplikacji hello jest zaktualizowane too2.0.0.0 z 1.0.0.0. Witaj *ApplicationManifest.xml* powinien wyglądać podobnie jak hello po fragment kodu:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


Teraz, kompilacji projektu hello, wybierając tylko hello **ActorService** projektu, a następnie prawym przyciskiem myszy i wybierając hello **kompilacji** w programie Visual Studio. W przypadku wybrania **odbudowanie wszystkiego**, należy zaktualizować hello wersji dla wszystkich projektów, ponieważ kod hello może zostać zmieniona. Następnie Załóżmy zaktualizowana aplikacja hello pakietu przez kliknięcie prawym przyciskiem myszy ***VisualObjectsApplication***, wybierając hello usługi sieć szkieletowa Menu i wybierając **pakietu**. Ta akcja powoduje utworzenie pakietu aplikacji, które można wdrożyć.  Zaktualizowano aplikacja jest gotowa toobe wdrożone.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Krok 3: Wybierz zasady dotyczące kondycji i parametry uaktualnienia
Zapoznaj się z hello [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) i hello [procesu uaktualniania](service-fabric-application-upgrade.md) tooget dobrą znajomość hello uaktualniania różnych parametrów, limity czasu i zastosować kryterium kondycji . W ramach tego przewodnika kryterium oceny kondycji usługi hello jest ustawienie domyślne toohello (i zalecana) wartości, które oznacza, że wszystkie usługi i wystąpień powinny być *dobrej kondycji* po uaktualnieniu hello.  

Jednak ta funkcja pozwala zwiększyć hello *HealthCheckStableDuration* too60 sekund (tak, aby hello usługi są w dobrej kondycji dla co najmniej 20 sekund przed hello uaktualnianie będzie kontynuowane toohello Następna aktualizacja domeny).  Umożliwia również ustawić hello *UpgradeDomainTimeout* toobe 1200 sekund i hello *UpgradeTimeout* toobe 3000 sekund.

Ponadto umożliwia także ustawić hello *UpgradeFailureAction* toorollback. Ta opcja wymaga sieci szkieletowej usług tooroll wstecz hello aplikacji toohello poprzedniej wersji, w przypadku napotkania problemów podczas uaktualniania hello. W związku z tym podczas rozpoczynania uaktualniania hello (w kroku 4), hello określić następujące parametry są:

FailureAction = wycofywania

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Krok 4: Przygotowywanie aplikacji do uaktualnienia
Teraz aplikacji hello jest wbudowana i uaktualnić toobe gotowe. Jeśli Otwórz okno programu PowerShell jako administrator, a typ [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), powinien pozwalają wiedzieli, że jest on typ aplikacji 1.0.0.0 **VisualObjects** który jest wdrażany.  

Witaj pakiet aplikacji są przechowywane w następujących hello ścieżki względnej, gdzie jako nieskompresowane hello zestawu SDK usług sieci szkieletowej — *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. Folder "Pakietu" powinien znajdować się w tym katalogu, w którym przechowywana jest pakiet aplikacji hello. Sprawdź tooensure sygnatury czasowe hello jest hello ostatniej kompilacji (może być także odpowiednio toomodify hello ścieżki).

Teraz załóżmy hello kopiowania zaktualizować toohello pakietu aplikacji magazynu ImageStore sieci szkieletowej usług (gdzie hello pakiety aplikacji są przechowywane przez sieć szkieletowa usług). Witaj parametru *ApplicationPackagePathInImageStore* informuje o tym, gdzie można znaleźć pakietu aplikacji hello sieci szkieletowej usług. Testujemy aplikacji hello zaktualizowane "VisualObjects\_V2" z hello następujące polecenie (czasem ścieżki toomodify ponownie odpowiednio).

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

Witaj, następnym krokiem jest tooregister tej aplikacji z sieci szkieletowej usług, które mogą być wykonywane przy użyciu hello [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenia:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Jeśli hello poprzednie polecenie nie powiedzie się, prawdopodobnie konieczność ponownej kompilacji wszystkich usług. Jak wspomniano w kroku 2, konieczne może być tooupdate w używanej wersji usługi sieci Web.

## <a name="step-5-start-hello-application-upgrade"></a>Krok 5: Uruchom uaktualniania aplikacji hello
Teraz, jesteśmy wszystkich aplikacji hello toostart zestaw uaktualnienia przy użyciu hello [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Witaj Nazwa aplikacji jest hello sam opisane w hello *ApplicationManifest.xml* pliku. Sieć szkieletowa usług używa tego tooidentify nazwę, która aplikacja jest wprowadzenie uaktualniony. Jeśli ustawisz toobe limity czasu hello jest zbyt krótki, możesz napotkać komunikat o błędzie, że stanów hello problem. Zobacz toohello Rozwiązywanie problemów z sekcji, lub zwiększ hello przekroczeń limitu czasu.

Teraz, jak hello kontynuowane uaktualniania aplikacji, można monitorować za pomocą Eksploratora usługi sieć szkieletowa, lub za pomocą hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) polecenia programu PowerShell: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

W ciągu kilku minut hello stan, który uzyskano przy użyciu hello poprzedzających polecenia programu PowerShell powinny prezentować uaktualniono wszystkie domeny aktualizacji (ukończone). I powinien znajdować się, że uruchomiony obracanie hello obiekty widoczne w oknie przeglądarki!

Możesz spróbować uaktualniania z wersji 2 tooversion 3 lub w wersji 2 tooversion 1, ponieważ wykonywanie. Przenoszenie z wersji 2 tooversion 1 jest traktowana jako uaktualnienia. Odtwarzanie z limitów czasu i toomake zasady kondycji samodzielnie z nich korzystać. W przypadku wdrażania klastra Azure tooan hello zestawu toobe potrzeby parametrów odpowiednio. Konserwatywnie jest dobrym tooset hello przekroczeń limitu czasu.

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą programu Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [parametry uaktualnienia](service-fabric-application-upgrade-parameters.md).

Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).

Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).

