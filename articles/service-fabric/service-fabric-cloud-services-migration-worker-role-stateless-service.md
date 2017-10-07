---
title: "Usługi w chmurze Azure aplikacje toomicroservices aaaConvert | Dokumentacja firmy Microsoft"
description: "W tym przewodniku porównuje chmury usług sieci Web i roli proces roboczy i usługi sieć szkieletowa usług bezstanowych toohelp migracji z usługi w chmurze tooService sieci szkieletowej."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Przewodnik dotyczący tooconverting usług sieci Web i roli proces roboczy tooService sieci szkieletowej bezstanowych
W tym artykule opisano sposób toomigrate chmury usług sieci Web i proces roboczy tooService sieci szkieletowej bezstanowych usług. Jest hello Najprostsza ścieżka migracji z usługi w chmurze tooService sieci szkieletowej dla aplikacji, których ogólna architektura będzie toostay około hello takie same.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Projekt aplikacji sieci szkieletowej tooService projektu usługi w chmurze
 Projektu usługi w chmurze i projektu aplikacji sieci szkieletowej usług mają podobną strukturę i jednostki zarówno reprezentują hello wdrożenia dla aplikacji — czyli każdy z nich określają hello pełny pakiet toorun wdrożonej aplikacji. Projekt usługi w chmurze zawiera co najmniej jednej sieci Web lub roli proces roboczy. Podobnie projektu aplikacji sieci szkieletowej usług zawiera co najmniej jedna usługa. 

Witaj różnica polega na tym pozamałżeńskie projektu usługi w chmurze hello hello wdrożenie aplikacji o wdrożeniu maszyny Wirtualnej w związku z tym zawiera ustawienia konfiguracji maszyny Wirtualnej w ramach tego projektu aplikacji sieci szkieletowej usług hello określa tylko aplikację, która zostanie wdrożona zestaw tooa istniejących maszyn wirtualnych w klastrze usługi sieć szkieletowa usług. samego klastra usługi sieć szkieletowa Hello jest wdrożona tylko raz, albo za pomocą szablonu usługi Resource Manager lub hello portalu Azure i wiele sieci szkieletowej usług aplikacje mogą być wdrożone tooit.

![Porównanie projektu usługi Service Fabric i usług w chmurze][3]

## <a name="worker-role-toostateless-service"></a>Usługa toostateless roli procesu roboczego
Koncepcyjnie rolę procesu roboczego reprezentuje bezstanowego obciążenia, co oznacza każde wystąpienie obciążenia hello jest identyczne i żądania mogą być kierowany tooany wystąpienia w dowolnym momencie. Każde wystąpienie nie jest oczekiwanym tooremember hello poprzedniego żądania. Stan, aby obciążenie hello działa z zarządzanych przez Magazyn stanów zewnętrzne, takie jak magazyn tabel Azure lub bazy danych dokumentów platformy Azure. W sieci szkieletowej usług tego rodzaju obciążenia jest reprezentowany przez usługę bezstanową. Hello najprostsza metoda toomigrating tooService roli procesu roboczego sieci szkieletowej można konwertowanie tooa kod roli proces roboczy usług bezstanowych.

![TooStateless roli procesu roboczego usługi][4]

## <a name="web-role-toostateless-service"></a>Rola toostateless usługi sieci Web
Podobne tooWorker roli roli sieci Web również reprezentuje bezstanowego obciążenia, a więc koncepcyjnie zbyt może być zmapowane tooa usługi bezstanowej sieci szkieletowej usług. Jednak w przeciwieństwie do ról sieci Web, usługi Service Fabric nie obsługuje usług IIS. toomigrate aplikacji sieci web z usługi bezstanowej tooa roli sieci Web wymaga pierwszego przenoszenie tooa platforma sieci web może być hostowana samodzielnie, który nie zależy od usług IIS lub System.Web, takich jak ASP.NET Core 1.

| **Aplikacji** | **Obsługiwane** | **Ścieżki migracji** |
| --- | --- | --- |
| Formularze sieci Web ASP.NET |Nie |Konwertuj tooASP.NET podstawowe 1 MVC |
| ASP.NET MVC |Z migracją |Uaktualnienia tooASP.NET podstawowe 1 MVC |
| Składnik Web API platformy ASP.NET |Z migracją |Użyj serwera siebie lub platformy ASP.NET Core 1 |
| Platformy ASP.NET Core 1 |Tak |Nie dotyczy |

## <a name="entry-point-api-and-lifecycle"></a>Interfejs API punktu wejścia i cykl życia
Rola proces roboczy i sieci szkieletowej usług usługi interfejsów API oferta podobne punkty wejścia: 

| **Punkt wejścia** | **Rola procesu roboczego** | **Usługa sieci szkieletowej usług** |
| --- | --- | --- |
| Przetwarzanie |`Run()` |`RunAsync()` |
| Początek maszyny Wirtualnej |`OnStart()` |Nie dotyczy |
| Zatrzymanie maszyny Wirtualnej |`OnStop()` |Nie dotyczy |
| Otwórz odbiornika dla żądań klientów |Nie dotyczy |<ul><li> `CreateServiceInstanceListener()`Aby uzyskać bezstanowych</li><li>`CreateServiceReplicaListener()`dla stateful</li></ul> |

### <a name="worker-role"></a>Rola procesu roboczego
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Usługa sieci szkieletowej usług bezstanowych
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

W których przetwarzanie toobegin mają zastąpienie podstawowego "Uruchom". Łączenie usługi sieć szkieletowa usług `Run`, `Start`, i `Stop` na jeden punkt wejścia, `RunAsync`. Podczas pracy z usługą powinny one zacząć `RunAsync` uruchamia i powinna zostać przerwana w pracy, gdy hello `RunAsync` zostanie zasygnalizowane metody CancellationToken. 

Istnieje kilka klucza różnic między hello cykl życia i okresem istnienia usług roli proces roboczy i sieci szkieletowej usług:

* **Cykl życia:** hello największych różnica polega na czy roli proces roboczy jest maszyny Wirtualnej i dlatego jego cyklem życia jest wiązanej toohello maszyny Wirtualnej, która obejmuje zdarzenia podczas uruchamiania i zatrzymywania w hello maszyny Wirtualnej. Usługa Service Fabric ma cykl życia, która jest oddzielona od hello wirtualna cykl życia, więc nie zawiera zdarzeń związanych z gdy hello host maszyny Wirtualnej lub uruchomieniu maszyny i zakończenie, ponieważ nie są powiązane.
* **Okres istnienia:** odtwarzana wystąpienia roli proces roboczy, jeśli hello `Run` wyjścia metody. Witaj `RunAsync` metody usługi sieci szkieletowej usług można uruchamiać toocompletion i wystąpienie usługi hello pozostaną w górę. 

Sieć szkieletowa usług udostępnia punkt wejścia instalacji komunikacji opcjonalne dla usług, które nasłuchuje żądań klienta. Zarówno hello RunAsync, jak i punktu wejścia komunikacji są opcjonalne zastąpień w usługach sieci szkieletowej usług - usługi może wybierz tooonly nasłuchiwania żądań tooclient lub uruchomić tylko w pętli przetwarzania i/lub -, które dlatego hello metodzie RunAsync jest dozwolone tooexit bez ponowne uruchamianie hello wystąpienie usługi, ponieważ może on nadal toolisten do obsługi żądań klientów.

## <a name="application-api-and-environment"></a>Interfejs API aplikacji i środowiska
Środowisko usługi w chmurze Hello interfejsu API zawiera informacje i funkcjonalność hello bieżące wystąpienie maszyny Wirtualnej, a także informacje o innych wystąpień roli maszyny Wirtualnej. Sieć szkieletowa usług zawiera informacje dotyczące środowiska uruchomieniowego tooits i niektóre informacje o węźle hello usługi jest obecnie uruchomiony w. 

| **Zadania środowiska** | **Cloud Services** | **Service Fabric** |
| --- | --- | --- |
| Ustawienia konfiguracji i powiadomienia o zmianie |`RoleEnvironment` |`CodePackageActivationContext` |
| Magazyn lokalny |`RoleEnvironment` |`CodePackageActivationContext` |
| Informacje o punkcie końcowym |`RoleInstance` <ul><li>Bieżące wystąpienie:`RoleEnvironment.CurrentRoleInstance`</li><li>Inne role i wystąpienie:`RoleEnvironment.Roles`</li> |<ul><li>`NodeContext`dla bieżącego adresu węzła</li><li>`FabricClient`i `ServicePartitionResolver` do odnajdywania punktu końcowego usługi</li> |
| Emulacja środowiska |`RoleEnvironment.IsEmulated` |Nie dotyczy |
| Zdarzenie zmiany jednoczesnych |`RoleEnvironment` |Nie dotyczy |

## <a name="configuration-settings"></a>Ustawienia konfiguracji
Ustawienia konfiguracji usług w chmurze są ustawiane dla roli maszyny Wirtualnej i zastosować tooall wystąpień tej roli maszyny Wirtualnej. Te ustawienia są pary klucz wartość ustawiona w plikach ServiceConfiguration.*.cscfg i jest dostępny bezpośrednio za pomocą RoleEnvironment. W sieci szkieletowej usług ustawienia mają zastosowanie indywidualnie tooeach usług i aplikacji tooeach, zamiast tooa maszyny Wirtualnej, ponieważ maszyna wirtualna może obsługiwać wiele usług i aplikacji. Usługa składa się z trzech pakietów:

* **Kod:** zawiera pliki wykonywalne usługi hello, plików binarnych biblioteki dll i inne pliki wymagane przez usługę toorun.
* **Config:** wszystkich plików konfiguracji i ustawień usługi.
* **Dane:** plików statycznych danych skojarzonych z usługą hello.

Każdy z tych pakietów można niezależnie określonej wersji, jak i uaktualnionych. Podobne usługi tooCloud, pakietu konfiguracji można uzyskać programistycznie przy użyciu interfejsu API i zdarzenia są dostępne toonotify hello usługi o zmianie konfiguracji pakietu. Pliku Settings.xml może służyć do konfiguracji klucz wartość, a dostęp programistyczny podobne toohello aplikacji ustawienia sekcji pliku App.config. Jednak w przeciwieństwie do usługi w chmurze, pakiet konfiguracji sieci szkieletowej usług może zawierać pliki konfiguracji w dowolnym formacie XML, JSON, yaml programu lub niestandardowy format binarny. 

### <a name="accessing-configuration"></a>Uzyskiwanie dostępu do konfiguracji
#### <a name="cloud-services"></a>Cloud Services
Ustawienia konfiguracji z ServiceConfiguration.*.cscfg jest możliwy za pośrednictwem `RoleEnvironment`. Te ustawienia są globalnie dostępną tooall wystąpień roli w hello tego samego wdrożenia usługi w chmurze.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Każda usługa ma własny pakiet konfiguracji poszczególnych. Nie istnieje wbudowany mechanizm dla globalne ustawienia konfiguracji dostępne przez wszystkie aplikacje w klastrze. Podczas korzystania z usługi Service Fabric specjalne Settings.xml konfiguracji pliku w ramach pakietu konfiguracji wartości w pliku Settings.xml można zastąpić na poziomie aplikacji hello, umożliwiając ustawień konfiguracji na poziomie aplikacji.

Ustawienia konfiguracji są dostępu w ramach każdego wystąpienia usługi za pośrednictwem usługi hello `CodePackageActivationContext`.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>Zdarzenia aktualizacji konfiguracji
#### <a name="cloud-services"></a>Cloud Services
Witaj `RoleEnvironment.Changed` zdarzenie jest używane toonotify występuje wszystkich wystąpień roli wprowadzania zmian w środowisku hello, np. o zmianie konfiguracji. Jest to używane tooconsume konfiguracji aktualizacji bez odtwarzania wystąpień roli lub ponowne uruchomienie procesu roboczego.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Każdy z trzech typów pakietów hello w usłudze - kodu, konfiguracji i danych — mieć zdarzenia, które powiadamiają o wystąpieniu usługi, gdy pakiet zostanie zaktualizowany, dodany lub usunięty. Usługa może zawierać wielu pakietów każdego typu. Na przykład usługa może mieć wielu pakietów konfiguracji każdego indywidualnie numerów wersji i możliwej. 

Te zdarzenia są dostępne tooconsume zmiany pakietów usług bez konieczności ponownego uruchamiania wystąpienie usługi hello.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Zadania uruchamiania
Uruchamianie zadania są działaniach wykonywanych przed uruchomieniem aplikacji. Zadanie uruchamiania jest najczęściej używanymi toorun skryptów instalacji przy użyciu podniesionych przywilejów. Usługa Service Fabric i usług w chmurze obsługuje zadania uruchamiania. Witaj podstawowa różnica polega na tym w usługi w chmurze, zadanie uruchamiania jest wiązana tooa maszyny Wirtualnej, ponieważ jest częścią wystąpienia roli, w sieci szkieletowej usług zadanie uruchamiania jest wiązana tooa usługi, która nie jest związany tooany określonej maszyny Wirtualnej.

| Cloud Services | Service Fabric |
| --- | --- | --- |
| Lokalizacja konfiguracji |ServiceDefinition.csdef |
| Uprawnienia |"ograniczony" lub "z podwyższonym poziomem uprawnień" |
| Sekwencjonowanie |"prosty", "tła", "narzędzia" |

### <a name="cloud-services"></a>Cloud Services
Usług w chmurze punktu wejścia uruchamiania jest skonfigurowany dla każdej roli w ServiceDefinition.csdef. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
W sieci szkieletowej usług punktu wejścia uruchamiania jest skonfigurowany dla usługi w pliku ServiceManifest.xml:

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>Uwagi dotyczące środowiska deweloperskiego
Usługi Service Fabric i usług w chmurze są zintegrowane z programem Visual Studio z szablonów projektu i obsługę debugowania, konfigurowanie i wdrażanie zarówno lokalnie i tooAzure. Usługa Service Fabric i usług w chmurze udostępniają rozwoju lokalnego środowiska uruchomieniowego. Witaj różnicą jest to, że podczas hello emuluje programowanie środowiska uruchomieniowego usługi w chmurze hello środowiska platformy Azure, na którym jest uruchomiony, Service Fabric nie korzysta z emulatora — używa środowiska uruchomieniowego platformy Service Fabric pełną hello. Hello jest środowiska, które należy uruchomić na komputerze deweloperskim lokalnej sieci szkieletowej usług hello tym samym środowisku, który jest uruchamiany w środowisku produkcyjnym.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o usługach niezawodnej usługi sieci szkieletowej i hello podstawowych różnic między usługami w chmurze i architektura toounderstand aplikacji sieci szkieletowej usług, jak tootake zaletą hello pełny zestaw funkcji sieci szkieletowej usług.

* [Wprowadzenie do korzystania z usługi sieć szkieletowa niezawodne usługi](service-fabric-reliable-services-quick-start.md)
* [Przewodnik koncepcyjny toohello różnice między usługami w chmurze i sieci szkieletowej usług](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
