---
title: "model aplikacji usługi sieć szkieletowa aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak toomodel i opisz aplikacji i usług w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>Model aplikacji w sieci szkieletowej usług
Ten artykuł zawiera omówienie modelu aplikacji hello sieć szkieletowa usług Azure oraz jak toodefine aplikacji i usług za pośrednictwem plików manifestu.

## <a name="understand-hello-application-model"></a>Zrozumienie modelu aplikacji hello
Aplikacja jest kolekcja składników usług, które wykonywać niektórych funkcji lub funkcji. Usługa działa pełny i autonomiczne i można uruchomić i uruchomić niezależnie od innych usług.  Usługa składa się z kodu, konfiguracji i danych. Dla każdej usługi kod składa się z plików binarnych wykonywalnego hello, konfiguracja obejmuje ustawienia usługi, które mogą zostać załadowane w czasie wykonywania i danych składa się z używane przez usługę hello toobe dowolne dane statyczne. Każdego składnika w tym modelu hierarchiczne aplikacji może być niezależnie określonej wersji, jak i uaktualnionych.

![model aplikacji Hello sieci szkieletowej usług][appmodel-diagram]

Typ aplikacji kategoryzacji aplikacji i składa się z pakietem typu usługi. Typ usługi jest kategoryzacji usługi. kategoryzacji Hello może mieć różne ustawienia i konfiguracje, ale pozostaje funkcje podstawowe hello hello takie same. Witaj wystąpień usługi są zmian konfiguracji usługi różnych hello z hello sam typ usługi.  

Klasy (lub "typów") aplikacji i usług opisanych za pomocą plików XML (manifestów aplikacji i manifestów usługi).  manifesty Hello są hello szablony, które można wdrożyć aplikacji z magazynu obrazu klastra hello. Witaj definicji schematu dla pliku ServiceManifest.xml i ApplicationManifest.xml hello jest instalowany z hello zestawu SDK sieci szkieletowej usług i narzędzi zbyt*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

Hello kodu dla różnych aplikacji wystąpień Uruchom jako osobne procesy nawet wtedy, gdy jest to obsługiwane przez hello tego samego węzła sieci szkieletowej usług. Ponadto hello cyklem życia każdego wystąpienia aplikacji mogą być zarządzane (na przykład uaktualnić) niezależnie. Witaj poniższym diagramie przedstawiono sposób typy aplikacji składają się z typów usług, które z kolei składają się z kodu, konfiguracji i danych. diagram hello toosimplify, tylko hello pakietów kodu/config/data dla `ServiceType4` są wyświetlane, że każdy typ usługi to niektórych lub wszystkich tych typów pakietów.

![Typy aplikacji usługi Service Fabric i usługi][cluster-imagestore-apptypes]

Dwa różne pliki manifestu są używane toodescribe aplikacji i usług: hello manifestu usługi i manifest aplikacji. Manifesty są tu szczegółowo hello następujące sekcje.

Może istnieć co najmniej jedno wystąpienie typu usługi active w klastrze hello. Na przykład wystąpienie usługi stanowej lub replik, osiągnąć wysoką niezawodnością poprzez replikację stanu między replikami znajdujących się w różnych węzłach w klastrze hello. Replikacji zasadniczo zapewnia nadmiarowość toobe usługi hello jest dostępne, nawet w przypadku awarii jednego węzła w klastrze. A [podzielona na partycje usługi](service-fabric-concepts-partitioning.md) dalsze bez reszty jego stan (i stanu toothat wzorce dostępu) na węzłach w klastrze hello.

Witaj Poniższy diagram przedstawia hello relacji między aplikacjami i wystąpień usług, partycji i replik.

![Partycji i replik w ramach usługi][cluster-application-instances]

> [!TIP]
> Układ aplikacji hello można wyświetlić w klastrze za pomocą narzędzia Service Fabric Explorer hello jest dostępne w http://&lt;yourclusteraddress&gt;: 19080/Explorer. Aby uzyskać więcej informacji, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Opis usługi
manifest usługi Hello deklaratywnie definiuje hello usługi typu i wersji. Określa usługę metadane, takie jak typ usługi, właściwości kondycji metryki równoważenia obciążenia, pliki binarne usługi i pliki konfiguracyjne.  Innymi słowy, opisuje pakiety kodu, konfiguracji i danych hello tworzące toosupport pakietu usługi co najmniej jeden typ usługi. Poniżej przedstawiono prosty przykład manifest usługi:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**Wersja** atrybuty są ciągami bez struktury i nie zostały przeanalizowane przez hello systemu. Wersja atrybuty są używane tooversion każdy składnik do uaktualnienia.

**Serivcetype** deklaruje, jakie typy usługi są obsługiwane przez **CodePackages** w tym manifeście. Usługa jest uruchomione na jednym z następujących typów usługi, wszystkie pakiety kodu zadeklarowany w tym manifeście zostaną aktywowane przez uruchomienie ich punktów wejścia. procesy wynikowy Hello są oczekiwanego tooregister hello obsługiwane usługi typów w czasie wykonywania. Typy usług są deklarowane jako hello manifestu poziomie i nie hello kod pakietu. Dlatego w przypadku wielu pakietów kodu ich wszystkich aktywacji zawsze, gdy hello system wyszukuje dowolny hello zadeklarowany typów usług.

**Element SetupEntryPoint** punkt wejścia uprzywilejowanych uruchamiane przy użyciu hello same poświadczenia jako sieci szkieletowej usług (zwykle hello *LocalSystem* konta) przed innymi punktu wejścia. plik wykonywalny Hello określony przez **punktu wejścia** jest zazwyczaj hello długotrwałe usługi hosta. obecności Hello osobnych ustawieniach punktu wejścia pozwala uniknąć konieczności hosta usługi hello toorun z wysokiego poziomu uprawnień przez dłuższy czas. plik wykonywalny Hello określony przez **punktu wejścia** po zakończeniu **SetupEntryPoint** kończy się pomyślnie. Jeśli kiedykolwiek hello proces kończy lub ulegnie awarii, monitorowania i ponowne uruchomienie procesu wynikowy hello (począwszy od ponownie **SetupEntryPoint**).  

Typowe scenariusze korzystania **SetupEntryPoint** są podczas uruchomienia pliku wykonywalnego przed uruchomieniem usługi hello lub wykonać operację z podwyższonym poziomem uprawnień. Na przykład:

* Konfigurowanie i Inicjowanie zmiennych środowiskowych, które hello potrzeb pliku wykonywalnego usługi. To nie jest ograniczona tooonly pliki wykonywalne napisane przez modele programowania hello sieci szkieletowej usług. Na przykład npm.exe musi niektóre zmienne środowiskowe skonfigurowane do wdrażania aplikacji node.js.
* Konfigurowanie kontroli dostępu, instalując certyfikaty zabezpieczeń.

Aby uzyskać więcej informacji na temat tooconfigure hello **SetupEntryPoint** zobacz [hello zasady dla punktu wejścia instalacji usługi](service-fabric-application-runas-security.md)

**EnvironmentVariables** zawiera listę zmiennych środowiskowych, które są ustawione dla tego pakietu kodu. Zmienne Environmentment może zostać zastąpiona w hello `ApplicationManifest.xml` tooprovide różne wartości dla wystąpień innej usługi. 

**DataPackage** deklaruje folder o nazwie hello **nazwa** atrybutu, zawierającego toobe dowolne dane statyczne, używane przez proces hello w czasie wykonywania.

**Lokalizacji ConfigPackage** deklaruje folder o nazwie hello **nazwa** atrybut, który zawiera *Settings.xml* pliku. Plik ustawień Hello zawiera sekcje ustawień pary klucz wartość, zdefiniowanych przez użytkownika, które odczytuje procesu hello Wstecz w czasie wykonywania. Podczas uaktualniania, jeśli tylko hello **lokalizacji ConfigPackage** **wersji** została zmieniona, a następnie hello uruchomiony proces nie zostanie ponownie uruchomiony. Zamiast tego wywołania zwrotnego powiadamia hello procesu, który zmieniono ustawienia konfiguracji, mogą być ładowane dynamicznie. Oto przykład *Settings.xml* pliku:

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Manifest usługi może zawierać wiele kodu, konfiguracji i danych. Każdy z tych może być kontrolą wersji niezależnie.
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Opis aplikacji
manifest aplikacji Hello deklaratywnie opisuje hello typ i wersja aplikacji. Określa usługę kompozycji metadane, takie jak nazwy stabilny oraz schemat partycji, współczynnik liczby/replikacji wystąpienia, zasady zabezpieczeń i izolacji, ograniczenia umieszczania, operacje zastępowania konfiguracji, typów usług składowych. opisano również Hello domen równoważenia obciążenia w których znajduje się aplikacja hello.

W związku z tym manifest aplikacji zawiera opis elementów na poziomie aplikacji hello i odwołuje się do jednego lub więcej usługi manifesty toocompose typu aplikacji. Poniżej przedstawiono prosty przykład manifestu aplikacji:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

Manifesty usługi, takich jak **wersji** atrybuty są ciągami bez struktury i nie są analizowane przez hello systemu. Atrybuty wersji są również używane tooversion każdy składnik do uaktualnienia.

**ServiceManifestImport** zawiera odwołania do tooservice manifestów, które tworzą ten typ aplikacji. Manifesty importowanych usługi określają, jakie typy usługi są prawidłowe w ramach tego typu aplikacji. W ramach hello ServiceManifestImport można zastąpić wartości konfiguracji w pliku Settings.xml i środowiska zmiennych w plikach pliku ServiceManifest.xml. 


**DefaultServices** deklaruje wystąpień usług, które są tworzone automatycznie, gdy aplikacja zostanie uruchomiony przed tego typu aplikacji. Domyślne usługi są po prostu udogodnienie i zachowywać się jak normalne usług w każdym względem po ich utworzeniu. One są uaktualniane wraz z innymi usługami w wystąpienia aplikacji hello i można również usunąć.

> [!NOTE]
> Manifest aplikacji może zawierać wiele importów manifestu usługi i usług domyślnych. Niezależnie może być wersjonowany każdego importu manifestu usługi.
> 
> 

jak wyświetlić toomaintain różnych aplikacji i parametrów usługi dla poszczególnych środowisk toolearn [Zarządzanie parametry aplikacji dla wielu środowiskach](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Następne kroki
[Pakiet aplikacji](service-fabric-package-apps.md) i zapewnić ich toodeploy gotowe.

[Wdrażanie i usunąć aplikacje] [ 10] w tym artykule opisano sposób toouse PowerShell toomanage aplikacji wystąpień.

[Zarządzanie parametry aplikacji dla wielu środowiskach] [ 11] w tym artykule opisano sposób tooconfigure parametrów i zmiennych środowiskowych dla wystąpień inną aplikację.

[Konfigurowania zasad zabezpieczeń dla aplikacji] [ 12] w tym artykule opisano, jak toorun usług pod dostępu toorestrict zasad zabezpieczeń.

[Hosting modeli aplikacji] [ 13] opis relacji między repliki (lub wystąpień) wdrożonej usługi i procesu hosta usługi.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
