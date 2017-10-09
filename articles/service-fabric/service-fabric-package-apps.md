---
title: "aaaPackage aplikację usługi Azure Service Fabric | Dokumentacja firmy Microsoft"
description: "Jak toopackage aplikacji usługi Service Fabric, przed wdrożeniem tooa klastra."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a>Pakiet aplikacji
W tym artykule opisano sposób toopackage aplikacji usługi Service Fabric i przygotowania do wdrożenia.

## <a name="package-layout"></a>Układ pakietu
manifest aplikacji Hello, co najmniej jeden manifestów usługi i inne niezbędne pliki muszą być zorganizowane w układzie określonej dla wdrożenia do klastra usługi sieć szkieletowa pakiet. manifesty przykład Hello w tym artykule wymagałoby toobe podzielone na powitania po strukturę katalogów:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

foldery Hello są nazywane toomatch hello **nazwa** atrybuty każdego odpowiadającego mu elementu. Na przykład, jeśli hello manifestu usługi zawiera dwa pakiety kodu z nazwami hello **MyCodeA** i **MyCodeB**, a następnie dwa foldery z hello zawierałoby tych samych nazw hello niezbędne pliki binarne dla każdego kodu pakiet.

## <a name="use-setupentrypoint"></a>Użyj elementu SetupEntryPoint
Typowe scenariusze korzystania **SetupEntryPoint** są, gdy potrzebujesz toorun pliku wykonywalnego przed uruchomieniem usługi hello lub należy tooperform operacji z podwyższonym poziomem uprawnień. Na przykład:

* Konfigurowanie i Inicjowanie zmiennych środowiskowych, które hello potrzeb pliku wykonywalnego usługi. Nie jest ograniczona tooonly pliki wykonywalne napisane przez modele programowania hello sieci szkieletowej usług. Na przykład npm.exe musi niektóre zmienne środowiskowe skonfigurowane do wdrażania aplikacji node.js.
* Konfigurowanie kontroli dostępu, instalując certyfikaty zabezpieczeń.

Aby uzyskać więcej informacji na temat tooconfigure hello **SetupEntryPoint**, zobacz [hello zasady dla punktu wejścia instalacji usługi](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Konfigurowanie
### <a name="build-a-package-by-using-visual-studio"></a>Tworzenie pakietu przy użyciu programu Visual Studio
Jeśli używasz programu Visual Studio 2015 toocreate aplikacji, można użyć hello pakietu tooautomatically polecenia utworzyć pakietu, który odpowiada układu hello opisane powyżej.

toocreate pakiet, kliknij prawym przyciskiem myszy projekt aplikacji hello w Eksploratorze rozwiązań i wybierz polecenie pakietu hello, jak pokazano poniżej:

![Pakowanie aplikacji przy użyciu programu Visual Studio][vs-package-command]

Po zakończeniu tworzenia pakietów można znaleźć lokalizacji hello hello pakietu w hello **dane wyjściowe** okna. krok pakietów Hello odbywa się automatycznie podczas wdrażania lub debugowania aplikacji w programie Visual Studio.

### <a name="build-a-package-by-command-line"></a>Tworzenie pakietu przy użyciu wiersza polecenia
Możliwe jest również możliwe tooprogrammatically pakietu przy użyciu aplikacji `msbuild.exe`. Pod maską hello Visual Studio jest uruchomiony, dane wyjściowe hello jest taka sama.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Pakiet hello testowy
Struktura pakietu hello lokalnie za pomocą programu PowerShell można sprawdzić za pomocą hello [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia.
To polecenie sprawdza dla manifest analizowania problemów i sprawdź wszystkie odwołania. To polecenie weryfikuje tylko hello poprawności strukturalnych hello katalogów i plików w pakiecie hello.
Nie Sprawdź dowolne hello zawartość pakietu kodu lub danych poza sprawdzanie, czy wszystkie niezbędne pliki są obecne.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Ten błąd pokazuje tego hello *MySetup.bat* pliku, do którego odwołuje się hello manifestu usługi **SetupEntryPoint** brakuje hello pakiet kodu. Po dodaniu hello brakujący plik przekazuje weryfikacji aplikacji hello:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

Jeśli aplikacja ma [parametry aplikacji](service-fabric-manage-multiple-environment-app-configuration.md) zdefiniowane, można przekazać je w [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) do właściwego weryfikacji.

Jeśli znasz klastra hello wdrożonym aplikacji hello, zalecane jest przekazywane w hello `ImageStoreConnectionString` parametru. W takim przypadku pakietów hello jest również weryfikacji względem poprzedniej wersji aplikacji hello już uruchomione w klastrze hello. Na przykład weryfikacji hello może wykryć, czy pakiet z hello tej samej wersji, ale inną zawartość została już wdrożona.  

Gdy aplikacja hello jest dostarczana poprawnie i pozytywnej weryfikacji, oceny na podstawie rozmiaru hello i hello liczbę plików, jeśli kompresji nie jest konieczne.

## <a name="compress-a-package"></a>Kompresuj pakietu
Gdy pakiet jest duży lub ma wiele plików, można skompresować je szybciej wdrożenia. Kompresja zmniejsza hello liczbę plików i hello rozmiar pakietu.
Dla pakietu aplikacji skompresowany [pakiet aplikacji hello przekazywanie](service-fabric-deploy-remove-applications.md#upload-the-application-package) może potrwać już porównaniu toouploading hello nieskompresowanych pakietu (Jeśli specjalnie czasu kompresji jest brana pod uwagę), ale [rejestrowanie](service-fabric-deploy-remove-applications.md#register-the-application-package) i [wyrejestrowanie typ aplikacji hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) są szybsze dla pakietu aplikacji skompresowane.

mechanizm wdrażania Hello jest takie samo skompresowanym i nieskompresowanym pakietów. Jeśli pakiet hello jest skompresowany, są przechowywane jako takie magazynu obrazu klastra hello i przed uruchomieniem aplikacji hello jest dekompresowane w węźle hello.
Kompresja Hello zastępuje hello skompresowanej wersji hello prawidłowy pakiet sieci szkieletowej usług. Hello folder muszą zezwalać na uprawnienia do zapisu. Systemem kompresji już skompresowanym pakietem daje żadnych zmian.

Pakiet można skompresować, uruchamiając polecenie programu Powershell hello [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) z `CompressPackage` przełącznika. Można zdekompresować hello pakiet o hello same polecenia przy użyciu `UncompressPackage` przełącznika.

Witaj następujące polecenie kompresuje pakietu hello bez go kopiować toohello magazynu obrazów. Możesz skopiować tooone skompresowany pakiet lub więcej klastrów sieci szkieletowej usług, zgodnie z potrzebami, za pomocą [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) bez hello `SkipCopy` flagi.
Pakiet HELLO zawiera teraz pliki zip hello `code`, `config`, i `data` pakietów. Witaj w manifeście aplikacji i manifestów usługi hello są nie zip, ponieważ są potrzebne do wielu operacji wewnętrznych (takie jak udostępnianie aplikacji wyodrębniania nazwy i wersji typu dla niektórych operacji sprawdzania poprawności pakietu).
Kompresja manifestów hello spowodowałoby te operacje, nieefektywne.

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

Alternatywnie można kompresować i skopiować hello pakietu z [ServiceFabricApplicationPackage kopiowania](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) w jednym kroku.
Jeśli hello pakiet jest duży, podaj wystarczająco wysoka, limit czasu czas tooallow hello pakietu kompresję i hello przekazywania toohello klastra.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Wewnętrznie Service Fabric oblicza sumy kontrolne dla pakietów aplikacji hello do weryfikacji. Korzystając z kompresji, sum kontrolnych hello są obliczane na powitania zip wersje każdego pakietu.
Jeśli skopiowane nieskompresowanych wersji pakietu aplikacji, i chcesz toouse kompresja hello tego samego pakietu, należy zmienić hello wersje hello `code`, `config`, i `data` pakiety tooavoid błąd sumy kontrolnej. Jeśli pakietów hello uległy zmianie, a zmiana wersji hello, możesz użyć [różnic inicjowania obsługi administracyjnej](service-fabric-application-upgrade-advanced.md). Po wybraniu tej opcji nie ma pakietu niezmienione hello zamiast niej odwołania z hello manifestu usługi.

Podobnie jeśli przekazać skompresowaną wersję pakietu hello i chcesz toouse nieskompresowanych pakietu, należy zaktualizować hello wersji tooavoid hello błąd sumy kontrolnej.

Hello pakietu jest teraz spakowane poprawnie zweryfikowane i skompresowane (w razie potrzeby), aby była gotowa do [wdrożenia](service-fabric-deploy-remove-applications.md) klastrów tooone lub więcej sieci szkieletowej usług.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Kompresuj pakiety, w przypadku wdrażania przy użyciu programu Visual Studio
Możesz wydać pakietów toocompress Visual Studio podczas wdrażania, dodając hello `CopyPackageParameters` tooyour elementu profilu publikowania i ustaw hello `CompressPackage` atrybutu zbyt`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Następne kroki
[Wdrażanie i usunąć aplikacje] [ 10] w tym artykule opisano sposób wystąpień aplikacji toomanage PowerShell toouse

[Zarządzanie parametry aplikacji dla wielu środowiskach] [ 11] w tym artykule opisano sposób tooconfigure parametrów i zmiennych środowiskowych dla wystąpień inną aplikację.

[Konfigurowania zasad zabezpieczeń dla aplikacji] [ 12] w tym artykule opisano, jak toorun usług pod dostępu toorestrict zasad zabezpieczeń.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
