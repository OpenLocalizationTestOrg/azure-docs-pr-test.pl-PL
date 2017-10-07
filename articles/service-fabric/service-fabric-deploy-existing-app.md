---
title: "aaaDeploy istniejącego pliku wykonywalnego tooAzure sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Przewodnik dotyczący jak toopackage istniejącej aplikacji jako pliku wykonywalnego gościa, dlatego można ją wdrożyć tooa klastra sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Wdrażanie gościa tooService wykonywalnego sieci szkieletowej
Możesz uruchomić dowolnego typu kodu, np. Node.js, Java lub C++ w sieci szkieletowej usług Azure, jako usługa. Sieć szkieletowa usług odnosi się toothese typów usług jako pliki wykonywalne gościa.

Pliki wykonywalne gościa są traktowane przez sieć szkieletowa usług takich jak usług bezstanowych. W związku z tym są umieszczane w węzłach w klastrze, w oparciu o dostępności i inne metryki. W tym artykule opisano sposób toopackage i wdrażanie klastra usługi sieć szkieletowa tooa pliku wykonywalnego gościa za pomocą programu Visual Studio lub narzędzia wiersza polecenia.

W tym artykule firma Microsoft obejmuje hello kroki toopackage pliku wykonywalnego gościa i wdrożyć ją tooService sieci szkieletowej.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Zalety uruchamiania Gość pliku wykonywalnego w sieci szkieletowej usług
Istnieje kilka toorunning zalety Gość pliku wykonywalnego w klastrze usługi sieć szkieletowa usług:

* Wysoka dostępność. Aplikacje uruchamiane w sieci szkieletowej usług są zyskuje dużą dostępność. Sieć szkieletowa usług zapewnia uruchomionych wystąpień aplikacji.
* Monitorowanie kondycji. Monitorowanie kondycji sieci szkieletowej usług wykrywa, czy aplikacja działa i udostępnia informacje diagnostyczne, w przypadku awarii.   
* Zarządzanie cyklem życia aplikacji. Oprócz zapewnienia uaktualnienia bez przestojów, usługi Service Fabric zawiera automatycznego wycofania toohello poprzedniej wersji, jeśli istnieje zdarzenie kondycji zły zgłoszone podczas uaktualniania.    
* Gęstości. Wiele aplikacji można uruchomić w klastrze, która eliminuje potrzebę hello toorun każdej aplikacji na własnych sprzętu.
* Odnajdowanie: Za pomocą usługi REST można wywołać toofind Usługa nazewnictwa sieci szkieletowej usług hello innych usług w klastrze hello. 

## <a name="samples"></a>Przykłady
* [Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Omówienie aplikacji i pliki manifestu usługi
W ramach wdrażania pliku wykonywalnego gościa, jest przydatne toounderstand hello sieci szkieletowej usług pakowania i wdrażania modelu zgodnie z opisem w [model aplikacji](service-fabric-application-model.md). Hello sieci szkieletowej usług pakowania modelu opiera się na dwa pliki XML: hello manifestów aplikacji i usług. Witaj definicji schematu dla hello pliki ApplicationManifest.xml i ServiceManifest.xml jest instalowany z hello zestawu SDK sieci szkieletowej usług do *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Manifest aplikacji** manifest aplikacji hello jest używany toodescribe aplikacji hello. Przedstawia on hello usług, które go tworzą i innych parametrów, które są używane toodefine jak co najmniej jednej usługi powinny zostać wdrożone, takich jak hello liczba wystąpień.

  W sieci szkieletowej usług aplikacji jest jednostką wdrożenia i uaktualnienia. Aplikację można aktualizować jako pojedyncza jednostka, w której zarządzane potencjalnych awarii i wycofywanie potencjalne zmian. Sieć szkieletowa usług gwarantuje, że proces uaktualniania hello jest pomyślnie, lub jeśli hello uaktualnienie nie powiedzie się, nie pozostawi aplikacji hello w stan nieznany lub niestabilny.
* **Manifest usługi** manifestu usługi hello w tym artykule opisano składniki hello usługi. Zawiera dane, takie jak nazwa hello i typ usługi, a jego kod i konfiguracji. Witaj manifestu usługi zawiera również pewne dodatkowe parametry, które mogą być używane tooconfigure hello usługi po jej wdrożeniu.

## <a name="application-package-file-structure"></a>Struktura pliku pakietu aplikacji
toodeploy tooService aplikacji sieci szkieletowej aplikacji hello należy stosować struktury katalogów wstępnie zdefiniowane. Witaj poniżej znajduje się przykład tej struktury.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Witaj ApplicationPackageRoot zawiera pliku ApplicationManifest.xml hello, który definiuje aplikacji hello. Podkatalog dla poszczególnych usług zawartych w aplikacji hello jest używany toocontain hello wszystkie artefakty, które usługa hello wymaga. Te podkatalogi są hello ServiceManifest.xml i zazwyczaj hello następujące:

* *Kod*. Ten katalog zawiera hello kodu usługi.
* *Config*. Ten katalog zawiera pliku Settings.xml (i innych plików, jeśli to konieczne) czy hello usługa może uzyskać dostęp w środowiska uruchomieniowego tooretrieve określonych ustawień konfiguracji.
* *Dane*. To dodatkowe toostore dodatkowe lokalne dane katalogu hello usługi może być konieczne. Dane powinny być używane toostore tylko tymczasowych danych. Sieć szkieletowa usług pojawia się kopiuje lub replicate katalog danych toohello zmiany Usługa hello musi toobe przeniesiony (na przykład w trybie failover).

> [!NOTE]
> Nie masz toocreate hello `config` i `data` katalogów, jeśli nie są potrzebne.
>
>

## <a name="package-an-existing-executable"></a>Pakiet istniejącego pliku wykonywalnego
Podczas pakowania pliku wykonywalnego gościa, można wybrać obu toouse szablon projektu Visual Studio lub zbyt[ręcznie utworzyć pakiet aplikacji hello](#manually). Za pomocą programu Visual Studio, hello struktury pakietu aplikacji i pliki manifestu zostają utworzone przez hello nowego szablonu projektu.

> [!TIP]
> Witaj Najprostszym sposobem toopackage Windows istniejącego pliku wykonywalnego do usługi jest toouse programu Visual Studio i w systemie Linux toouse narzędzia Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Korzystając z programu Visual Studio toopackage oraz wdrożyć istniejącego pliku wykonywalnego
Program Visual Studio udostępnia usługi sieć szkieletowa toohelp szablonu usługi, w przypadku wdrażania klastra usługi sieć szkieletowa tooa pliku wykonywalnego gościa.

1. Wybierz **pliku** > **nowy projekt**i tworzenie aplikacji sieci szkieletowej usług.
2. Wybierz **pliku wykonywalnego gościa** jako hello szablonu usługi.
3. Kliknij przycisk **Przeglądaj** tooselect hello folder, plik wykonywalny i wypełnij rest hello hello parametry toocreate hello usługi.
   * *Zachowanie pakietu kodu*. Może być toocopy zestaw wszystkich zawartość hello toohello Twojego folderu projektu programu Visual Studio, co jest przydatne, jeśli hello pliku wykonywalnego nie ulega zmianie. Jeśli oczekiwać hello toochange pliku wykonywalnego i chcesz dynamicznie hello możliwości toopick się nowych kompilacji, zamiast tego można wybrać toolink toohello folder. Podczas tworzenia projektu aplikacji hello w programie Visual Studio, można użyć połączonego folderów. W ten sposób toohello lokalizacji źródła z projektu hello, umożliwiając możesz tooupdate hello gościa pliku wykonywalnego w jego miejsce docelowe źródło. Aktualizacje mogące spowodować staną się częścią pakietu aplikacji hello podczas kompilacji.
   * *Program* Określa plik wykonywalny hello, która powinna być uruchomiona usługa hello toostart.
   * *Argumenty* Określa argumenty hello, które powinny być przekazywane wykonywalnego toohello. Może być lista parametrów z argumentami.
   * *WorkingFolder* Określa katalog roboczy hello hello procesu, który będzie toobe uruchomiona. Można określić trzy wartości:
     * `CodeBase`Określa, że katalog roboczy hello będzie toobe Ustaw katalog kodów toohello w pakiecie aplikacji hello (`Code` katalogu pokazano hello poprzedzających struktury plików).
     * `CodePackage`Określa, że katalog roboczy hello przechodzi toobe ustawić głównego toohello pakietu aplikacji hello (`GuestService1Pkg` pokazano hello poprzedzających struktury plików).
     * `Work`Określa, że pliki hello są umieszczane w podkatalogu o nazwie pracy.
4. Nadaj nazwę usłudze i kliknij przycisk **OK**.
5. Jeśli usługa wymaga punktu końcowego do komunikacji, można teraz dodawać hello protokół, port i plik ServiceManifest.xml toohello typu. Na przykład: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Można teraz używać pakietu hello i opublikować akcji względem klastra lokalnego przez debugowanie rozwiązania hello w programie Visual Studio. Po wykonaniu tych czynności można publikować klastra zdalnego tooa aplikacji hello lub zaewidencjonować hello rozwiązania toosource formantu.
7. Jak przejść toohello na końcu tego artykułu toosee tooview Twojego usługa wykonywalna gościa w narzędziu Service Fabric Explorer.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Użyj Yoeman toopackage i wdrażanie istniejącego pliku wykonywalnego w systemie Linux

Witaj procedura tworzenia i wdrażania Gość pliku wykonywalnego w systemie Linux jest hello taki sam jak wdrażanie aplikacji csharp lub java.

1. Na terminalu wpisz `yo azuresfguest`.
2. Nadaj nazwę aplikacji.
3. Nazwę usługi i podaj szczegóły hello, w tym ścieżki hello pliku wykonywalnego i parametrów hello, które muszą być wywoływane z.

Narzędzia yeoman tworzy pakiet aplikacji z odpowiedniej aplikacji hello i pliki manifestu wraz z instalowania i odinstalowywania skryptów.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Ręcznie pakietów i wdrożyć istniejącego pliku wykonywalnego
proces Hello ręcznie pakowania pliku wykonywalnego gościa jest oparta na powitania następujące ogólne kroki:

1. Utwórz strukturę katalogów hello pakietu.
2. Dodawanie aplikacji hello kodu i plików konfiguracji.
3. Edytuj hello pliku manifestu usługi.
4. Edytuj plik manifestu aplikacji hello.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Utwórz strukturę katalogów hello pakietu
Możesz uruchomić tworzenie hello struktury katalogów, zgodnie z opisem w powyższej sekcji hello "Struktura pliku pakietu aplikacji".

### <a name="add-hello-applications-code-and-configuration-files"></a>Dodawanie plików kodu i konfiguracji aplikacji hello
Po utworzeniu hello struktury katalogów, możesz dodać pliki kodu i konfiguracji aplikacji hello w obszarze hello katalogów kodu i konfiguracji. Można również utworzyć dodatkowe katalogi lub podkatalogi w obszarze hello kodu lub config katalogów.

Sieć szkieletowa usług jest `xcopy` hello zawartości hello katalogu, więc nie ma żadnych toouse struktury wstępnie zdefiniowanych innych niż tworzenie dwa katalogi top, kodu i ustawienia. (Można wybrać różne nazwy elementu, jeśli chcesz. Bardziej szczegółowe informacje znajdują się w następnej sekcji hello.)

> [!NOTE]
> Upewnij się, czy zawiera wszystkie pliki hello i zależności, które hello potrzeb aplikacji. Sieć szkieletowa usług kopiuje hello zawartości pakietu aplikacji hello we wszystkich węzłach w klastrze hello, gdzie usługi aplikacji hello są wdrożone toobe będzie. Witaj pakiet powinien zawierać wszystkie kodu hello, że aplikacja hello musi toorun. Zakłada się, że zależności hello są już zainstalowane.
>
>

### <a name="edit-hello-service-manifest-file"></a>Zmodyfikuj plik manifestu usługi hello
Witaj następnym krokiem jest tooedit hello usługi pliku manifestu tooinclude hello następujących informacji:

* Nazwa Hello hello typu usługi. To jest identyfikator używany tooidentify usługi sieć szkieletowa usług.
* Witaj polecenia toouse toolaunch hello aplikacji (w elemencie ExeHost).
* Dowolny skrypt, który wymaga toobe Uruchom tooset zapasowej aplikacji hello (SetupEntrypoint).

Witaj poniżej przedstawiono przykład `ServiceManifest.xml` pliku:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Witaj następujące sekcje zapoznać się z różnych części pliku hello konieczność tooupdate hello.

#### <a name="update-servicetypes"></a>Serivcetype aktualizacji
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Można wybrać dowolną nazwę, która ma `ServiceTypeName`. wartość Hello jest używany w hello `ApplicationManifest.xml` tooidentify hello usługa plików.
* Określ `UseImplicitHost="true"`. Ten atrybut informuje usługi Service Fabric, że usługa hello opiera się na autonomiczną aplikację, więc wszystkie usługi sieć szkieletowa usług musi toodo toolaunch go jako proces i monitorowanie jej kondycji.

#### <a name="update-codepackage"></a>Aktualizowanie elementu CodePackage
element elementu CodePackage Hello Określa lokalizację, hello (i wersji) hello usługi kodu.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Witaj `Name` element jest używany toospecify hello nazwę katalogu hello w pakiecie aplikacji hello, który zawiera kod hello usługi. `CodePackage`ma również hello `version` atrybutu. To może być używane toospecify hello wersja hello kodu i może też być używany kod tooupgrade hello usługi przy użyciu infrastruktury zarządzania cyklem życia aplikacji hello w sieci szkieletowej usług.

#### <a name="optional-update-setupentrypoint"></a>Opcjonalnie: SetupEntrypoint aktualizacji
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
Hello SetupEntryPoint element jest używany toospecify żadnych plik wykonywalny lub plik wsadowy który ma być wykonany przed uruchomieniem kodu usługi hello. Krok opcjonalny, jest więc nie musi toobe włączone, jeśli nie wymagają inicjalizacji nie istnieje. Witaj SetupEntryPoint jest wykonywane przy każdym uruchomieniu usługi hello.

Nie tylko jeden element SetupEntryPoint, więc skrypty instalacyjne wymagają toobe zgrupowane w pliku wsadowym pojedynczego, jeśli wiele skryptów wymaga ustawienia aplikacji hello. Witaj SetupEntryPoint można wykonywać dowolny typ pliku: pliki wykonywalne, pliki wsadowe i poleceń cmdlet programu PowerShell. Aby uzyskać więcej informacji, zobacz [skonfigurować SetupEntryPoint](service-fabric-application-runas-security.md).

W hello poprzedzających przykład, hello SetupEntryPoint uruchamia plik wsadowy o nazwie `LaunchConfig.cmd` czyli znajduje się w hello `scripts` podkatalogu w katalogu kodu hello (przy założeniu, hello WorkingFolder element jest ustawiony tooCodeBase).

#### <a name="update-entrypoint"></a>Aktualizowanie punktu wejścia
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Witaj `EntryPoint` elementu w pliku manifestu usługi hello jest używany toospecify jak toolaunch hello usługi. Witaj `ExeHost` element określa hello pliku wykonywalnego (i argumenty) powinny być używane toolaunch hello usługi.

* `Program`Określa nazwę pliku wykonywalnego hello, który należy uruchomić usługę hello hello.
* `Arguments`Określa argumenty hello, które powinny być przekazywane wykonywalnego toohello. Może być lista parametrów z argumentami.
* `WorkingFolder`Określa katalog roboczy hello hello procesu, który będzie toobe uruchomiona. Można określić trzy wartości:
  * `CodeBase`Określa, że katalog roboczy hello będzie toobe Ustaw katalog kodów toohello w pakiecie aplikacji hello (`Code` katalogu w hello poprzedzających struktury plików).
  * `CodePackage`Określa, że katalog roboczy hello przechodzi toobe ustawić głównego toohello pakietu aplikacji hello (`GuestService1Pkg` w hello poprzedzających struktury plików).
    * `Work`Określa, że pliki hello są umieszczane w podkatalogu o nazwie pracy.

Witaj WorkingFolder jest przydatne tooset hello poprawny katalog roboczy, aby ścieżek względnych mogą być używane przez skrypty albo hello aplikacji lub inicjowania.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Zaktualizuj punktów końcowych i zarejestrować w usłudze nazewnictwa do komunikacji
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
W hello poprzedzających przykład, hello `Endpoint` element określa hello punkty końcowe, które można nasłuchiwać aplikacji hello. W tym przykładzie hello aplikacji Node.js nasłuchuje http na porcie 3000.

Ponadto można zadawać toopublish sieci szkieletowej usług toohello tego punktu końcowego usługi nazewnictwa, inne usługi umożliwia odnalezienie usługi toothis adresu punktu końcowego hello. Dzięki temu toobe toocommunicate stanie między usługami, które są pliki wykonywalne gościa.
Witaj adres punktu końcowego opublikowanych ma formę hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme`i `PathSuffix` są opcjonalne atrybuty. `IPAddressOrFQDN`jest hello adresu IP lub nazwy FQDN węzła hello dotyczącymi pobiera tego pliku wykonywalnego i jest obliczana automatycznie.

W hello poniższy przykład, jeden raz hello usługi jest wdrażana, w narzędziu Service Fabric Explorer wyświetlone podobne punktu końcowego za`http://10.1.4.92:3000/myapp/` opublikowane hello wystąpienia usługi. Lub jeśli jest to komputer lokalny, zobacz `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Korzystając z tych adresów z [odwrotny serwer proxy](service-fabric-reverseproxy.md) toocommunicate między usługami.

### <a name="edit-hello-application-manifest-file"></a>Edytowanie pliku manifestu aplikacji hello
Po skonfigurowaniu hello `Servicemanifest.xml` pliku, należy toomake toohello niektóre zmiany `ApplicationManifest.xml` pliku tooensure, który hello poprawny typ usługi i nazwy są używane.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
W hello `ServiceManifestImport` elementu, można określić jedną lub kilka usług, które mają tooinclude w aplikacji hello. Usługi są przywoływane z `ServiceManifestName`, który określa nazwę hello hello katalogu, gdzie hello `ServiceManifest.xml` znajduje się plik.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Konfigurowanie rejestrowania
Pliki wykonywalne gościa jest przydatne toobe stanie toosee konsoli Dzienniki toofind limit Jeśli skryptów aplikacji i konfiguracji hello wyświetlać żadnych błędów.
Przekierowywanie konsoli można skonfigurować w hello `ServiceManifest.xml` plik przy użyciu hello `ConsoleRedirection` elementu.

> [!WARNING]
> Nigdy nie używaj zasad przekierowania konsoli hello w aplikacji, która jest wdrożony w środowisku produkcyjnym, ponieważ może to mieć wpływ na powitania aplikacji w tryb failover. *Tylko* użyć tej funkcji dla rozwoju lokalnych i debugowania.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`może to być katalog roboczy tooa tooredirect używane Konsola danych wyjściowych (stdout i stderr). Udostępnia hello możliwości tooverify, że nie ma żadnych błędów podczas instalacji hello lub wykonywanie aplikacji hello w klastrze usługi sieć szkieletowa hello.

`FileRetentionCount`Określa, ile plików są zapisywane w katalogu roboczym hello. Na przykład wartość 5, oznacza, że hello pliki dziennika poprzedniego wykonaniami pięć hello są przechowywane w katalogu roboczym hello.

`FileMaxSizeInKb`Określa maksymalny rozmiar plików dziennika hello hello.

Pliki dziennika są zapisywane w jednym z katalogów roboczych usługi hello. toodetermine, w którym znajdują się, hello pliki za pomocą Eksploratora usługi sieć szkieletowa toodetermine usługi hello węzła, która jest uruchomiona na i katalog roboczy, który jest używany. Ten proces jest uwzględnione w dalszej części tego artykułu.

## <a name="deployment"></a>Wdrożenie
ostatni krok Hello jest zbyt[wdrożyć aplikację](service-fabric-deploy-remove-applications.md). Witaj, jak po pokazuje skrypt programu PowerShell toodeploy Twojej aplikacji toohello lokalnego klastra projektowego i rozpocząć nową usługę sieci szkieletowej usług.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów, jeśli pakietów hello jest długa lub zawiera wiele plików. Dowiedz się więcej [tutaj](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Usługa sieci szkieletowej usług można wdrożyć w różnych "konfiguracji." Na przykład można wdrożyć jako jednego lub wielu wystąpień lub mogą być wdrażane w taki sposób, że istnieje jedno wystąpienie usługi hello w każdym węźle klastra sieci szkieletowej usług hello.

Witaj `InstanceCount` parametru hello `New-ServiceFabricService` polecenia cmdlet jest używane toospecify jak wiele wystąpień usługi hello powinna być uruchamiana w klastrze usługi sieć szkieletowa hello. Można ustawić hello `InstanceCount` wartość, w zależności od typu hello aplikacji, która jest wdrażana. Witaj dwie najczęstsze scenariusze są następujące:

* `InstanceCount = "1"`. W takim przypadku tylko jedno wystąpienie usługi hello jest wdrażane w klastrze hello. Harmonogram usługi sieć szkieletowa określa usługi hello węzła, która będzie toobe wdrożone na.
* `InstanceCount ="-1"`. W takim przypadku jednego wystąpienia usługi hello jest wdrażana na każdym węźle w klastrze usługi sieć szkieletowa hello. wynik Hello ma jeden (i tylko jeden) wystąpienia usługi powitania dla każdego węzła w klastrze hello.

Jest to przydatne w konfiguracji dla aplikacji frontonu (na przykład punkt końcowy REST), ponieważ aplikacje klienckie wymagają zbyt "connect" tooany hello węzłów hello punktu końcowego hello toouse dla klastra. Tę konfigurację można również w przypadku, na przykład wszystkie węzły klastra sieci szkieletowej usług hello tooa podłączonej usługi równoważenia obciążenia. Ruch klientów następnie mogą być rozproszone na powitania usługa, która jest uruchomiona na wszystkich węzłach w klastrze hello.

## <a name="check-your-running-application"></a>Sprawdź uruchomionej aplikacji
W narzędziu Service Fabric Explorer Zidentyfikuj węzła hello, w którym jest uruchomiona usługa hello. W tym przykładzie jest uruchamiany na Node1:

![Węzeł, na którym jest uruchomiona usługa](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Jeśli przejdź do węzła toohello i Przeglądaj toohello aplikacji, zobaczysz hello węzła istotne informacje, w tym lokalizacji na dysku.

![Miejsce na dysku](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Przeglądaj katalog toohello za pomocą Eksploratora serwera można znaleźć folderu dziennika hello usługi i katalog roboczy hello, zgodnie z powitania po zrzut ekranu: 

![Lokalizacja dziennika](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Następne kroki
W tym artykule wiesz już, jak toopackage pliku wykonywalnego gościa i wdróż je tooService sieci szkieletowej. Zobacz następujące artykuły powiązane informacje i zadań hello.

* [Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), łącznie z łącza toohello wstępnej wersji narzędzia do tworzenia pakietów hello
* [Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Wdrażanie wielu aplikacji wykonywalnych gości](service-fabric-deploy-multiple-apps.md)
* [Tworzenie pierwszej aplikacji sieci szkieletowej usług za pomocą programu Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
