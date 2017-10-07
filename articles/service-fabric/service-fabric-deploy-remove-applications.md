---
title: "aaaAzure wdrożenia aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Jak toodeploy i usunąć aplikacje w sieci szkieletowej usług za pomocą programu PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Wdrażanie i usunąć aplikacje przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Program Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [Interfejsy API FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Raz [typu aplikacji zostały opakowane][10], jest ono gotowe do wdrożenia do klastra usługi sieć szkieletowa usług Azure. Wdrożenie obejmuje hello następujące trzy kroki:

1. Przekaż magazynu obrazów toohello pakietu aplikacji hello
2. Rejestracja typu aplikacji hello
3. Tworzenie wystąpienia aplikacji hello

Po wdrożeniu aplikacji i wystąpienie jest uruchomione w klastrze hello, można usunąć wystąpienia aplikacji hello i typem aplikacji. Usuń toocompletely aplikacji z klastra hello obejmuje hello następujące kroki:

1. Usuń (lub usunąć) hello uruchomione wystąpienie aplikacji
2. Wyrejestrowywanie typu aplikacji hello, jeśli nie są już potrzebne
3. Usuwanie pakietu aplikacji hello z magazynu obrazów hello

Jeśli używasz [programu Visual Studio umożliwiające wdrażanie i debugowanie aplikacji](service-fabric-publish-app-remote-cluster.md) na klaster lokalny rozwój hello wszystkich powyższych kroków obsługi automatycznie za pomocą skryptu programu PowerShell.  Skrypt ten znajduje się w hello *skryptów* folderu projekt aplikacji hello. Ten artykuł zawiera tła na tego skryptu czynności, aby można było wykonać hello operacji poza Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Połącz toohello klastra
Przed uruchomieniem żadnych poleceń programu PowerShell w tym artykule należy uruchamiać przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) klastra sieci szkieletowej usług toohello tooconnect. tooconnect toohello lokalnego klastra projektowego, uruchom następujące hello:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Przykłady połączeniu tooa zdalnego klastra lub klastra zabezpieczone przy użyciu usługi Azure Active Directory, X509 certyfikatów lub usługi Active Directory systemu Windows, zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Przekaż pakiet aplikacji hello
Przekazywanie pakietu aplikacji hello umieszcza je w lokalizacji, który jest dostępny dla wewnętrznych składników usługi Service Fabric.
Pakiet aplikacji hello tooverify lokalnie, należy użyć hello [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia cmdlet.

Witaj [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenia przekazywania hello sklepu z aplikacjami pakietu toohello klastra obrazu.
Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.  tooimport hello zestawu SDK modułu, uruchom:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Załóżmy, że kompilacji i pakietu aplikacji o nazwie *MyApplication* w programie Visual Studio 2015. Domyślnie nazwa typu aplikacji hello wymienione w pliku ApplicationManifest.xml hello jest "MyApplicationType".  Witaj pakiet aplikacji, który zawiera manifest aplikacji konieczne hello, manifestów usługi i pakietów kodu/config/danych, znajduje się w *C:\Users\<username\>\Documents\Visual 2015\Projects\ w Studio MyApplication\MyApplication\pkg\Debug*. 

Witaj następujące polecenie wyświetla listę hello zawartości pakietu aplikacji hello:

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Jeśli pakiet aplikacji hello jest duży i/lub ma wiele plików, możesz [skompresować je](service-fabric-package-apps.md#compress-a-package). Witaj Kompresja zmniejsza rozmiar hello i hello liczbę plików.
Witaj efektem ubocznym jest tym hello rejestrowania i wyrejestrowywania typ aplikacji są szybsze. Czas przekazywania aktualnie może być mniejsza, zwłaszcza, Jeśli dołączysz hello czasu toocompress hello pakietu. 

toocompress pakiet, użyj hello sam [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenia. Kompresja może odbywać się oddzielne przesyłaniu, za pomocą hello `SkipCopy` flaga lub wraz z hello Przekaż operacji. Stosowanie kompresji na skompresowanym pakietem jest pusta.
toouncompress skompresowany pakiet, użyj hello sam [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) z hello `UncompressPackage` przełącznika.

Witaj następującego polecenia cmdlet kompresuje pakietu hello bez go kopiować toohello magazynu obrazów. Pakiet HELLO zawiera teraz pliki zip hello `Code` i `Config` pakietów. Witaj aplikacji i manifestów usługi hello są nie zip, ponieważ są potrzebne do wielu operacji wewnętrznych (takie jak udostępnianie aplikacji wyodrębniania nazwy i wersji typu dla niektórych operacji sprawdzania poprawności pakietu). Kompresja manifestów hello spowodowałoby te operacje, nieefektywne.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

Dla dużych pakietów aplikacji kompresji hello jest czasochłonne. Aby uzyskać najlepsze rezultaty należy użyć szybkiego dysk SSD. czasy kompresji Hello i rozmiar hello hello skompresowanym pakietem również się różnić w zależności na powitania zawartości pakietu.
Na przykład w tym miejscu jest statystyki kompresji niektórych pakietów, które Pokaż hello początkowej i hello rozmiar skompresowany pakiet z czasem kompresji hello.

|Początkowy rozmiar (MB)|Liczba plików|Czas kompresji|Skompresowany pakiet rozmiar (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Gdy pakiet jest skompresowana, może być przekazana tooone lub sieci szkieletowej usług wielu klastrów zgodnie z potrzebami. mechanizm wdrażania Hello jest takie samo skompresowanym i nieskompresowanym pakietów. Jeśli pakiet hello jest skompresowany, są przechowywane jako takie magazynu obrazu klastra hello i przed uruchomieniem aplikacji hello jest dekompresowane w węźle hello.


Witaj poniższy przykład przekazuje hello magazynu obrazów toohello pakietu, do folderu o nazwie "MyApplicationV1":

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.  tooimport hello zestawu SDK modułu, uruchom:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Jeśli nie określisz hello *- ApplicationPackagePathInImageStore* parametru, pakiet aplikacji hello jest kopiowany do folderu "Debug" hello w magazynie obraz powitania.

Hello czas tooupload pakiet zależy od wielu czynników. Niektóre z nich są hello liczba plików w hello pakietu, rozmiar pakietu hello i hello rozmiary plików. szybkość sieci Hello między maszyną źródłową hello i hello klastra sieci szkieletowej usług ma wpływ również na czas przekazywania hello. Witaj domyślny limit czasu dla [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) to 30 minut.
W zależności od hello opisane czynników, może być tooincrease hello przekroczenia limitu czasu. Jeśli są kompresowania hello pakietu w wywołaniu kopiowania hello, musisz tooalso należy wziąć pod uwagę czas kompresji hello.

Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.

## <a name="register-hello-application-package"></a>Pakiet aplikacji hello rejestru
Witaj typ i wersja aplikacji zadeklarowane w manifeście aplikacji hello staną się dostępne po zarejestrowaniu pakietu aplikacji hello. Hello system odczytuje przesłany w poprzednim kroku hello pakiet hello, sprawdza, czy pakiet hello przetwarza hello zawartość pakietu i kopiuje hello przetworzyć pakietu tooan wewnętrznego systemu lokalizacji.  

Uruchom hello [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister polecenia cmdlet hello typu aplikacji w klastrze hello i udostępnienie jej do wdrożenia:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

"MyApplicationV1" jest hello folder, w którym znajduje się pakiet aplikacji hello magazynu obrazów hello. Typ aplikacji Hello o nazwie "MyApplicationType" i wersji "1.0.0", (zarówno znajdują się w manifeście aplikacji hello) teraz jest zarejestrowany w klastrze hello.

Witaj [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) polecenie zwraca tylko wtedy, gdy hello system hello pomyślnie zarejestrowano pakiet aplikacji. Jak długo trwa rejestracji zależy od rozmiaru hello i zawartości pakietu aplikacji hello. W razie potrzeby hello **- TimeoutSec** parametr może być używane toosupply dłuższego limitu czasu (hello domyślny limit czasu wynosi 60 sekund).

Jeśli masz aplikację duży pakiet lub jeśli występują przekroczenia limitu czasu, użyj hello **- Async** parametru. polecenie Hello zwraca po klastra hello akceptuje polecenia register hello i hello przetwarzanie będzie kontynuowane zgodnie z potrzebami.
Witaj [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenie wyświetla listę wszystkich wersji typu pomyślnie zarejestrowano aplikacji i ich stan rejestracji. Po zakończeniu rejestracji hello, można użyć tego polecenia toodetermine.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
Można utworzyć wystąpienia aplikacji z dowolnej wersji typu aplikacji, który został pomyślnie zarejestrowany za pomocą hello [ServiceFabricApplication nowy](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet. nazwy poszczególnych aplikacji Hello musi rozpoczynać się od hello *"fabric:"* schemat i muszą być unikatowe dla każdego wystąpienia aplikacji. Wszystkie usługi domyślne zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello są również tworzone.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Dla dowolnej wersji danego typu zarejestrowanej aplikacji można tworzyć wiele wystąpień aplikacji. Każde wystąpienie aplikacji jest uruchamiany w izolacji z katalogu roboczego i procesu.

toosee, który o nazwie aplikacje i usługi są uruchomione w klastrze hello, uruchom hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) i [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) poleceń cmdlet:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>Usuwanie aplikacji
Gdy wystąpienie aplikacji nie jest już potrzebne, można trwale usunąć ją według nazwy przy użyciu hello [ServiceFabricApplication Usuń](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) polecenia cmdlet. [Usuń ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatycznie usuwa wszystkie usługi należące toohello aplikacji, jak również i stałe usunięcie wszystkich stan usługi. 

> [!WARNING]
> Ta operacja jest nieodwracalna i nie można odzyskać stan aplikacji.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Wyrejestrowywanie typu aplikacji
W przypadku konkretnej wersji typu aplikacji nie jest potrzebna, należy wyrejestrować typu aplikacji hello przy użyciu hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) polecenia cmdlet. Wyrejestrowanie nieużywane aplikacji typów wersjach miejsca do magazynowania używanych przez hello magazynu obrazów. Typ aplikacji można wyrejestrować tak długo, jak wystąpienia są tworzone na nim żadnych aplikacji, a nie do czasu aplikacji uaktualnień odwołuje się do niego.

Uruchom [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) typy aplikacji hello toosee obecnie zarejestrowany w klastrze hello:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Uruchom [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister określonych typów aplikacji:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Usuwanie pakietu aplikacji ze sklepu obraz powitania
Gdy pakiet aplikacji nie jest potrzebna, należy ją usunąć z toofree magazynu obrazu hello zasobów systemowych.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Element ImageStoreConnectionString wprowadza się ServiceFabricApplicationPackage kopiowania
środowisko zestawu SDK usług sieci szkieletowej Hello ma już hello jest poprawna, skonfigurować ustawienia domyślne. A w razie potrzeby hello element ImageStoreConnectionString dla wszystkich poleceń powinny być zgodne wartość hello tego hello klaster sieci szkieletowej usług. Hello element ImageStoreConnectionString można znaleźć w manifeście klastra hello pobrany przy użyciu hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) i polecenia Get-ImageStoreConnectionStringFromClusterManifest:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.  tooimport hello zestawu SDK modułu, uruchom:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Element ImageStoreConnectionString Hello zostanie znaleziony w manifeście klastra hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.

### <a name="deploy-large-application-package"></a>Wdrażanie pakietu dużych aplikacji
Problem: [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) upłynie limit czasu dla pakietu aplikacji duże (kolejność GB).
Wypróbuj:
- Określ większego limitu czasu dla [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) polecenie z `TimeoutSec` parametru. Domyślnie program hello limitu czasu wynosi 30 minut.
- Sprawdź hello połączenie sieciowe między maszyną źródłową a klastra. Jeśli hello połączenie jest powolne, rozważ użycie maszynę z lepszą połączenia sieciowego.
Jeśli komputer kliencki hello w regionie innym niż klaster hello, należy rozważyć użycie komputerze klienckim w regionie bliżej lub tego samego jako klaster hello.
- Sprawdź, czy osiągnięto ograniczania zewnętrznych. Na przykład gdy hello obrazu magazyn jest skonfigurowany toouse azure magazynu, można ograniczenie przekazywania.

Problem: Pakiet przekazywania została ukończona pomyślnie, ale [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) upłynie limit czasu. Wypróbuj:
- [Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów.
Hello Kompresja zmniejsza rozmiar hello i wykonaj hello liczba plików, który z kolei ogranicza hello ilość ruchu sieciowego i działają w tej sieci szkieletowej usług. Operacja przekazywania Hello może przebiegać wolniej, (zwłaszcza, Jeśli dołączysz hello kompresji czasu), ale rejestrowania i wyrejestrowania typ aplikacji hello są szybsze.
- Określ większego limitu czasu dla [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) z `TimeoutSec` parametru.
- Określ `Async` przełączać [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). polecenie Hello zwraca gdy klastra hello akceptuje polecenia hello i rejestracji hello typu aplikacji hello asynchronicznie. Z tego powodu jest toospecify nie konieczności wyższe przekroczenia limitu czasu w takim przypadku. Witaj [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenie wyświetla listę wszystkich wersji typu pomyślnie zarejestrowano aplikacji i ich stan rejestracji. Po zakończeniu rejestracji hello, można użyć tego polecenia toodetermine.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Wdrażanie pakietu aplikacji z wielu plików
Problem: [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) limitu czasu dla pakietu aplikacji z wielu plików (kolejność tysięcy).
Wypróbuj:
- [Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów. Kompresja Hello zmniejsza hello liczbę plików.
- Określ większego limitu czasu dla [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) z `TimeoutSec` parametru.
- Określ `Async` przełączać [ServiceFabricApplicationType rejestru](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). polecenie Hello zwraca gdy klastra hello akceptuje polecenia hello i rejestracji hello typu aplikacji hello asynchronicznie.
Z tego powodu jest toospecify nie konieczności wyższe przekroczenia limitu czasu w takim przypadku. Witaj [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) polecenie wyświetla listę wszystkich wersji typu pomyślnie zarejestrowano aplikacji i ich stan rejestracji. Po zakończeniu rejestracji hello, można użyć tego polecenia toodetermine.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)

[Wprowadzenie kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)

[Diagnozowanie i rozwiązywanie problemów z usługą sieci szkieletowej usług](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Model aplikacji w sieci szkieletowej usług](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
