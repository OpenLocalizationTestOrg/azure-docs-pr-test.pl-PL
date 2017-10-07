---
title: Komunikacja aaaService z hello platformy ASP.NET Core | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse platformy ASP.NET Core w bezstanowe i stanowe niezawodne usługi."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>Platformy ASP.NET Core w niezawodnej usługi sieci szkieletowej usług

Platformy ASP.NET Core to nowa open source i międzyplatformowa struktura do tworzenia nowoczesnych aplikacji działających w chmurze podłączonej do Internetu, takich jak aplikacje sieci web, aplikacji IoT i przenośnych zapleczy. 

W tym artykule jest toohosting szczegółowy przewodnik platformy ASP.NET Core services w sieci szkieletowej niezawodnej usługi za pomocą hello **Microsoft.ServiceFabric.AspNetCore.** * zestaw pakietów NuGet.

Samouczek wprowadzający platformy ASP.NET Core w sieci szkieletowej usług i instrukcje dotyczące konfigurowania środowiska deweloperskiego, konfigurowanie, zobacz [tworzenie frontonu aplikacji przy użyciu platformy ASP.NET Core sieci web](service-fabric-add-a-web-frontend.md).

pozostałe Hello w tym artykule przyjęto założenie, że już znasz platformy ASP.NET Core. Jeśli nie, firma Microsoft zaleca odczytywania za pośrednictwem hello [podstawowe informacje na temat platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>Platformy ASP.NET Core w środowisku sieci szkieletowej usług hello

Gdy aplikacji platformy ASP.NET Core można uruchomić na .NET Core lub powitalne pełnego środowiska .NET Framework, obecnie usługi sieć szkieletowa usług można uruchomić tylko na hello pełna platformy .NET. Oznacza to, podczas tworzenia usługi platformy ASP.NET Core Service Fabric, należy nadal wskazać hello pełna platformy .NET.

Platformy ASP.NET Core mogą być używane w sieci szkieletowej usług na dwa sposoby:
 - **Hostowany jako pliku wykonywalnego gościa**. To jest głównie używane toorun platformy ASP.NET Core aplikacji w sieci szkieletowej usług bez zmian kodu.
 - **Uruchom wewnątrz niezawodnej usługi**. Umożliwia lepszą integrację ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello i umożliwia stanowe platformy ASP.NET Core services.

Hello dalszej części tego artykułu opisano, jak hello toouse platformy ASP.NET Core wewnątrz niezawodnej usługi za pomocą platformy ASP.NET Core składniki integracji, które są dostarczane z hello zestawu SDK usług sieci szkieletowej. 

## <a name="service-fabric-service-hosting"></a>Hosting usług sieci szkieletowej usług

W sieci szkieletowej usług, jeden lub więcej wystąpień i/lub repliki usługi uruchamiane w *procesu hosta usługi*, plik wykonywalny, który uruchamia kodu usługi. Jako autor usługi, własnej procesu hosta usługi hello i sieci szkieletowej usług aktywuje i monitorowanie go dla Ciebie.

Tradycyjny ASP.NET (w górę tooMVC 5) jest silnie sprzężonego tooIIS za pośrednictwem System.Web.dll. Platformy ASP.NET Core rozdzielenie między powitania serwera sieci web i aplikacji sieci web. Umożliwia przenośny między serwerami sieci web inną toobe aplikacji sieci web i pozwala również toobe serwerów sieci web *hosta samodzielnego*, co oznacza można uruchomić serwera sieci web w własnego procesu jako procesu min. tooa, którego właścicielem jest dedykowanych sieci web oprogramowanie serwera, takich jak usługi IIS. 

W kolejności toocombine usługi Service Fabric i ASP.NET, jako pliku wykonywalnego gościa lub w niezawodnej usługi, musi być możliwe toostart ASP.NET wewnątrz procesu hosta usługi. Platformy ASP.NET Core hostingu samodzielnego umożliwia toodo to.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Hosting platformy ASP.NET Core w niezawodnej usługi
Zazwyczaj własnym obsługiwanych aplikacji platformy ASP.NET Core utworzyć WebHost w punkcie wejścia aplikacji, takich jak hello `static void Main()` metoda `Program.cs`. W takim przypadku hello cyklem życia hello WebHost jest cyklu życia związanych toohello hello procesu.

![Hosting platformy ASP.NET Core w procesie][0]

Jednak punkt wejścia aplikacji hello nie jest toocreate odpowiednim miejscu hello WebHost w niezawodnej usługi, ponieważ punkt wejścia aplikacji hello jest używany tylko tooregister usługi wpisz ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello, dzięki czemu może tworzyć wystąpienia tej usługi Typ. Witaj WebHost powinny zostać utworzone w niezawodnej usługi samej siebie. W ramach procesu hosta usługi hello wystąpień usługi i/lub repliki można przejść przez wiele cyklów. 

Wystąpienie usługi niezawodnego jest reprezentowana przez usługi klasy wywodzące się z `StatelessService` lub `StatefulService`. Witaj stosu komunikacji usługi znajduje się w `ICommunicationListener` wdrażania w klasie usługi. Witaj `Microsoft.ServiceFabric.Services.AspNetCore.*` pakietów NuGet zawiera implementacje `ICommunicationListener` czy start i zarządzanie hello hosta sieci Web platformy ASP.NET Core dla Kestrel lub WebListener w niezawodnej usługi.

![Hosting platformy ASP.NET Core w niezawodnej usługi][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ICommunicationListeners platformy ASP.NET Core
Witaj `ICommunicationListener` implementacje Kestrel i WebListener w hello `Microsoft.ServiceFabric.Services.AspNetCore.*` pakietów NuGet mają podobne wzorce użycia, ale serwer sieci web określonego tooeach nieco inne akcje do wykonania. 

Zarówno odbiorników komunikacji zawierają konstruktora przyjmującego hello następujące argumenty:
 - **`ServiceContext serviceContext`**: hello `ServiceContext` obiekt, który zawiera informacje o hello usługi.
 - **`string endpointName`**: Nazwa hello `Endpoint` konfiguracji w pliku ServiceManifest.xml. To przede wszystkim których różnią się odbiorników komunikacji hello dwa: WebListener **wymaga** `Endpoint` konfiguracji, a nie Kestrel.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: lambda, który implementuje, w którym można utworzyć i zwracany `IWebHost`. Dzięki temu można tooconfigure `IWebHost` sposób hello zwykle w aplikacji platformy ASP.NET Core. Witaj lambda zawiera adres URL, który jest generowany dla można w zależności od hello sieci szkieletowej usług integracji opcje użycia i hello `Endpoint` konfiguracji należy podać. Adres URL następnie można zmodyfikować lub używane jako — serwer sieci web hello toostart.

## <a name="service-fabric-integration-middleware"></a>Oprogramowanie pośredniczące integracji sieci szkieletowej usług
Witaj `Microsoft.ServiceFabric.Services.AspNetCore` pakiet NuGet zawiera hello `UseServiceFabricIntegration` — metoda rozszerzenia na `IWebHostBuilder` dodaje oprogramowanie pośredniczące obsługujący usługi sieci szkieletowej. To oprogramowanie pośredniczące konfiguruje hello Kestrel lub WebListener `ICommunicationListener` tooregister usługi unikatowy adres URL z hello Usługa nazewnictwa sieci szkieletowej, a następnie weryfikuje łączą usługowy toohello klienci tooensure żądań klienta. Jest to konieczne w środowisku udostępnionych hosta, na przykład sieci szkieletowej usług, gdy wiele aplikacji sieci web mogą być uruchamiane na powitania same fizyczne lub maszyny wirtualnej, ale nie należy używać nazw unikatowy hosta, klienci tooprevent przez pomyłkę łączenie toohello niewłaściwej usługi. Ten scenariusz jest opisany bardziej szczegółowo w następnej sekcji hello.

### <a name="a-case-of-mistaken-identity"></a>Przypadek omyłkowo wystąpiła tożsamości
Repliki usługi, niezależnie od protokołu, nasłuchiwania IP:port unikatowych kombinacji. Po repliki usługi rozpoczął nasłuchiwanie na punkt końcowy IP:port, raporty toohello adres tego punktu końcowego usługi nazewnictwa sieci szkieletowej usług gdzie mogły być odnajdowane przez klientów lub innych usług. Jeśli używany przez usługi używanych aplikacji dynamicznie przypisywane porty, repliki usługi mogą przypadkowo hello samego IP:port punktu końcowego innej usługi, który został wcześniej na hello same fizyczne lub maszyny wirtualnej. To może spowodować, że klient toomistakely połączyć toohello niewłaściwej usługi. To może nastąpić, jeśli występują powitania po sekwencja zdarzeń:

 1. Usługa A nasłuchuje 10.0.0.1:30000 za pośrednictwem protokołu HTTP. 
 2. Klient rozpoznaje Service A i pobiera adres 10.0.0.1:30000
 3. Usługi przenosi tooa inny węzeł.
 4. Usługi B znajduje się na 10.0.0.1 i przypadkowo używa hello tego samego portu 30000.
 5. Klient próbuje wykonać tooconnect tooservice A z 10.0.0.1:30000 adres pamięci podręcznej.
 6. Klient jest teraz pomyślnie połączono tooservice B wiedzy nie jest podłączony toohello niewłaściwej usługi.

Może to powodować błędy w czasie losowych, które mogą być trudne toodiagnose. 

### <a name="using-unique-service-urls"></a>Przy użyciu usługi unikatowe adresy URL
tooprevent, usług post toohello punktu końcowego usługi nazw z unikatowym identyfikatorem, a następnie zweryfikować Unikatowy identyfikator podczas żądania klienta. To jest akcją współpracy między usługami w zaufanym środowisku — dzierżawy szkodliwy. Zapewnia to usługa bezpiecznego uwierzytelniania w środowisku szkodliwy dzierżawy.

W zaufanym środowisku hello oprogramowanie pośredniczące, który jest dodawany przez hello `UseServiceFabricIntegration` metody dołącza automatycznie adres toohello Unikatowy identyfikator, który jest przesyłana toohello nazw usługi i sprawdza poprawność identyfikator dla każdego żądania. Jeśli identyfikator hello nie jest zgodny, oprogramowanie pośredniczące hello natychmiast zwraca odpowiedź HTTP 410 — Przeniesiono.

Usługi używające należy się upewnić, port przypisywane dynamicznie używać tego oprogramowania pośredniczącego.

W środowisku współpracy usług korzystających z stały port unikatowy nie mają ten problem. Stały port unikatowy jest zwykle używany dla usługi uwzględniającym zewnętrznie, które wymagają dobrze znanego portu dla tooconnect aplikacji klienta do. Na przykład większość aplikacji sieci web skierowane do Internetu będzie używać portu 80 i 443 dla połączeń przeglądarki sieci web. W takim przypadku hello Unikatowy identyfikator nie powinna być włączona.

Witaj Poniższy diagram przedstawia przepływ żądania hello z oprogramowania pośredniczącego hello włączone:

![Integracja usługi sieci szkieletowej platformy ASP.NET Core][2]

Zarówno Kestrel i WebListener `ICommunicationListener` implementacje użycie tego mechanizmu hello dokładnie tak samo. Mimo że WebListener wewnętrznie pozwala odróżnić żądań oparte na unikatowych ścieżki adresu URL przy użyciu podstawowego hello *http.sys* funkcji, które są funkcji współużytkowania portów *nie* używane przez hello WebListener `ICommunicationListener` implementacji ponieważ skutkiem będzie HTTP 503 i HTTP 404 kodów stanu błędu w scenariuszu hello opisany wcześniej. Które z kolei utrudnia bardzo klientów toodetermine hello celem błąd hello, ponieważ HTTP 503 i 404 protokołu HTTP są już tooindicate często używane inne błędy. W związku z tym zarówno Kestrel i WebListener `ICommunicationListener` implementacje normalizacji na oprogramowanie pośredniczące hello podał hello `UseServiceFabricIntegration` — metoda rozszerzenia, dzięki czemu klienci muszą tylko tooperform punkt końcowy usługi ponownie rozwiązać akcji na odpowiedzi HTTP 410.

## <a name="weblistener-in-reliable-services"></a>WebListener w niezawodne usługi
WebListener mogą być używane w niezawodnej usługi przez importowanie hello **Microsoft.ServiceFabric.AspNetCore.WebListener** pakietu NuGet. Ten pakiet zawiera `WebListenerCommunicationListener`, implementacja `ICommunicationListener`, które pozwala toocreate WebHost Core ASP.NET wewnątrz niezawodnej usługi za pomocą WebListener jako serwera sieci web hello.

WebListener jest zbudowany na powitania [interfejsu API serwera HTTP systemu Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Ta metoda korzysta hello *http.sys* sterownik jądra używane przez usługi IIS tooprocess HTTP żądania i kierowania ich tooprocesses uruchamiania aplikacji sieci web. Dzięki temu wiele procesów na powitania tej samej maszynie fizycznej lub wirtualnej aplikacji toohost w sieci web na powitania tego samego portu rozróżniane unikatowej ścieżki adresu URL lub nazwa hosta. Funkcje te są przydatne w sieci szkieletowej usług do obsługi wielu witryn sieci Web w hello tego samego klastra.

Witaj poniższym diagramie przedstawiono sposób WebListener używa hello *http.sys* sterownik jądra w systemie Windows Udostępnianie portów:

![Sterownik HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener usługi bezstanowej
toouse `WebListener` za pośrednictwem usługi bezstanowej, Zastąp hello `CreateServiceInstanceListeners` — metoda i przywracać `WebListenerCommunicationListener` wystąpienie:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>WebListener w usługi stanowej

`WebListenerCommunicationListener`obecnie nie jest przeznaczony do użytku w usługach stanowych z powodu toocomplications z podstawowej hello *http.sys* funkcji współużytkowania portów. Aby uzyskać więcej informacji zobacz powitania po sekcji alokacją portów dynamicznych z WebListener. Dla stanowych usług Kestrel jest hello zalecane serwera sieci web.

### <a name="endpoint-configuration"></a>Konfiguracja punktu końcowego

`Endpoint` Konfiguracja jest wymagana dla serwerów sieci web, które używają hello API serwera HTTP systemu Windows, w tym WebListener. Serwery sieci Web, które używają interfejsu API serwera HTTP systemu Windows hello musi najpierw zarezerwować swojego adresu URL z *http.sys* (zwykle jest to realizowane przy użyciu hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) narzędzia). Ta akcja wymaga podniesione uprawnienia, które nie mają domyślnie usług. Witaj opcje "http" lub "https" hello `Protocol` właściwości hello `Endpoint` konfiguracji w *ServiceManifest.xml* są używane w szczególności tooinstruct hello tooregister środowiska uruchomieniowego platformy Service Fabric adresu URL za *http.sys* w Twoim imieniu przy użyciu hello [ *silne symbolu wieloznacznego* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) prefiksu adresu URL.

Na przykład tooreserve `http://+:80` dla usługi, hello następującej konfiguracji powinny być używane w pliku ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

I nazwa punktu końcowego hello muszą być przekazywane toohello `WebListenerCommunicationListener` konstruktora:

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>WebListener za pomocą portu statycznego
toouse portu statycznego z WebListener, podaj numer portu hello w hello `Endpoint` konfiguracji:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Użyj WebListener z portów dynamicznych
toouse dynamicznie przypisywanego port o WebListener, Pomiń hello `Port` właściwości w hello `Endpoint` konfiguracji:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Należy pamiętać, że port dynamiczny przydzielonej przez `Endpoint` konfiguracji zawiera tylko jeden port *na proces hosta*. Witaj bieżącej sieci szkieletowej usług hostingu modelu umożliwia wielu usługi wystąpień i/lub replik toobe hostowanych w hello tego samego procesu, co oznacza, że każdej z nich będzie udostępniać hello sam portu podczas przydzielane za pośrednictwem hello `Endpoint` konfiguracji. Wiele wystąpień WebListener można współużytkować port przy użyciu podstawowego hello *http.sys* portu udostępniania funkcji, ale nie jest obsługiwana przez `WebListenerCommunicationListener` powodu komplikacji toohello wprowadza się ona do obsługi żądań klientów. W przypadku użycia portów dynamicznych Kestrel jest hello zalecane serwera sieci web.

## <a name="kestrel-in-reliable-services"></a>Kestrel w niezawodne usługi
Kestrel mogą być używane w niezawodnej usługi przez importowanie hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** pakietu NuGet. Ten pakiet zawiera `KestrelCommunicationListener`, implementacja `ICommunicationListener`, które pozwala toocreate WebHost Core ASP.NET wewnątrz niezawodnej usługi za pomocą Kestrel jako serwera sieci web hello.

Kestrel to serwer sieci web i platform dla platformy ASP.NET Core oparta na libuv, biblioteki i platform asynchroniczne We/Wy. W odróżnieniu od WebListener, Kestrel nie używa Menedżera scentralizowane punktu końcowego takich jak *http.sys*. I w przeciwieństwie do WebListener, Kestrel nie obsługuje udostępniania portów między wiele procesów. Każde wystąpienie Kestrel musi używać portu unikatowy.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel usługi bezstanowej
toouse `Kestrel` za pośrednictwem usługi bezstanowej, Zastąp hello `CreateServiceInstanceListeners` — metoda i przywracać `KestrelCommunicationListener` wystąpienie:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>Kestrel w usługi stanowej
toouse `Kestrel` w usługi stanowej, Zastąp hello `CreateServiceReplicaListeners` — metoda i przywracać `KestrelCommunicationListener` wystąpienie:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

W tym przykładzie pojedyncze wystąpienie `IReliableStateManager` podano kontenera iniekcji zależności WebHost toohello. To nie jest to niezbędne, ale pozwala toouse `IReliableStateManager` i niezawodne kolekcji w metody akcji kontrolera MVC.

Należy pamiętać, że `Endpoint` Nazwa konfiguracji jest **nie** podano zbyt`KestrelCommunicationListener` w usługi stanowej. Jest to wyjaśnić bardziej szczegółowo w hello następujących sekcji.

### <a name="endpoint-configuration"></a>Konfiguracja punktu końcowego
`Endpoint` Konfiguracja nie jest wymagane toouse Kestrel. 

Kestrel jest prosty autonomiczny serwer sieci web; w odróżnieniu od WebListener (lub HttpListener), nie musi `Endpoint` konfiguracji w *ServiceManifest.xml* , ponieważ nie jest konieczne wcześniejsze toostarting rejestracji adresu URL. 

#### <a name="use-kestrel-with-a-static-port"></a>Kestrel za pomocą portu statycznego
Można skonfigurować port statyczny w hello `Endpoint` konfiguracji ServiceManifest.xml do użytku z Kestrel. Chociaż nie jest to niezbędne, zawiera dwa potencjalnych korzyści:
 1. Jeśli hello port nie należy do zakresu portów aplikacji hello, plik jest otwarty przez zaporę systemu operacyjnego hello przez sieć szkieletowa usług.
 2. Witaj tooyou podanego adresu URL za pośrednictwem `KestrelCommunicationListener` użyje tego portu.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Jeśli `Endpoint` jest skonfigurowany, jego nazwa muszą być przekazywane do hello `KestrelCommunicationListener` konstruktora: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Jeśli `Endpoint` konfiguracji nie jest używany, Pomiń nazwę hello w hello `KestrelCommunicationListener` konstruktora. W takim przypadku będzie używany port dynamiczny. Zobacz następną sekcję hello, aby uzyskać więcej informacji.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Użyj Kestrel z portów dynamicznych
Kestrel nie można użyć przypisania portów automatyczne hello hello `Endpoint` konfiguracji w pliku ServiceManifest.xml, ponieważ port automatyczne przypisanie z `Endpoint` konfiguracji przypisuje unikatowy portu na *proces hosta* , i procesem jednego hosta może zawierać wiele wystąpień Kestrel. Ponieważ Kestrel nie obsługuje udostępniania portów, to nie działa jako każde wystąpienie Kestrel muszą być otwarte na porcie unikatowy.

toouse dynamiczne przypisywanie portów z Kestrel, po prostu pominąć hello `Endpoint` konfiguracji w pliku ServiceManifest.xml całkowicie i nie są przekazywane toohello Nazwa punktu końcowego `KestrelCommunicationListener` konstruktora:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

W tej konfiguracji `KestrelCommunicationListener` będzie automatycznie wybierać nieużywanego portu z zakresu portów aplikacji hello.

## <a name="scenarios-and-configurations"></a>Scenariusze i konfiguracje
W tej sekcji opisano hello następujące scenariusze i zapewnia hello zalecane kombinację serwera sieci web, konfiguracji portów sieci szkieletowej usług integracji opcje i tooachieve różne ustawienia usługi działa prawidłowo:
 - Zewnętrznie udostępnione usługi bezstanowej platformy ASP.NET Core
 - Tylko wewnętrznie usługi bezstanowej platformy ASP.NET Core
 - Tylko wewnętrznie usługi stanowej platformy ASP.NET Core

**Zewnętrznie udostępnione** usługi jest taki, który udostępnia punkt końcowy dostępny spoza klastra hello, zwykle za pomocą modułu równoważenia obciążenia.

**Wyłącznie wewnętrznym** usługi jest jednym tylko jest dostępny w ramach klastra hello których punkt końcowy.

> [!NOTE]
> Usługi stanowej, które punkty końcowe zazwyczaj nie powinna być widoczne toohello Internet. Klastry, które znajdują się za usługi równoważenia obciążenia, które znają rozpoznawania usługi sieć szkieletowa usług, takich jak hello Azure Load Balancer będzie tooexpose stanowych usług, ponieważ usługi równoważenia obciążenia hello zostanie nie mogli toolocate i kierowania ruchu toohello odpowiednie usługi stanowej repliki. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Zewnętrznie udostępnione usług bezstanowych platformy ASP.NET Core
WebListener jest zalecane, serwer sieci web dla usług frontonu, które udostępniają zewnętrznych, internetowy punktów końcowych HTTP w systemie Windows hello. Zapewnia lepszą ochronę przed atakami, a obsługuje funkcje, które nie Kestrel, na przykład uwierzytelnianie systemu Windows i udostępnianie portów. 

Kestrel nie jest obsługiwany jako serwer graniczny (internetowy) w tej chwili. Należy użyć zwrotnego serwera proxy, takich jak IIS lub Nginx toohandle ruch z hello publicznej sieci Internet.
 
Gdy narażonych toohello Internet, usługi bezstanowej należy używać punktu końcowego dobrze znanych i stabilny, który jest dostępny za pośrednictwem usługi równoważenia obciążenia. Jest to adres URL hello zapewni toousers aplikacji. Zaleca się Hello następującej konfiguracji:

|  |  | **Uwagi** |
| --- | --- | --- |
| Serwer sieci Web | WebListener | Jeśli usługa hello jest tylko narażonych tooa zaufanej sieci, intranet, Kestrel może być używany. W przeciwnym razie WebListener jest opcją hello preferowany. |
| Konfiguracja portów | Statyczne | Dobrze znanego portu statycznego powinna być skonfigurowana w hello `Endpoints` konfiguracji ServiceManifest.xml, takie jak 80 dla protokołu HTTP i 443 dla protokołu HTTPS. |
| ServiceFabricIntegrationOptions | Brak | Witaj `ServiceFabricIntegrationOptions.None` opcja powinna być używana podczas konfigurowania sieci szkieletowej usług integracji w oprogramowaniu pośredniczącym, aby usługa hello zrezygnować z przychodzącego żądania toovalidate Unikatowy identyfikator. Użytkownicy zewnętrzni aplikacji nie będzie wiedzieć, hello unikatowe informacje identyfikacyjne używane przez oprogramowanie pośredniczące hello. |
| Liczba wystąpień | -1 | W typowych przypadkach ustawiania liczby wystąpień hello powinna być ustawiona zbyt-"1", aby wystąpienie jest dostępna we wszystkich węzłach, które odbierać dane z usługi równoważenia obciążenia. |

Jeśli wiele usług zewnętrznie narażonych udostępniać hello sam zestaw węzłów, należy używać unikalny, ale stabilna ścieżki adresu URL. Można to zrobić przez zmodyfikowanie hello adres URL podany podczas konfigurowania IWebHost. Należy pamiętać, że ma to zastosowanie tylko tooWebListener.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>Tylko wewnętrznie usługi bezstanowej platformy ASP.NET Core
Usługi bezstanowej, wywoływane tylko z wewnątrz klastra hello należy używać unikatowe adresy URL i dynamicznie przypisywane porty tooensure współpracy między wieloma usługami. Zaleca się Hello następującej konfiguracji:

|  |  | **Uwagi** |
| --- | --- | --- |
| Serwer sieci Web | kestrel | Mimo że WebListener może służyć do wewnętrznych usług bezstanowych, Kestrel jest hello zalecane tooallow serwera wielu tooshare wystąpień usługi hosta.  |
| Konfiguracja portów | przypisywane dynamicznie | Wiele replik usługi stanowej może udostępnić procesu hosta lub systemu operacyjnego hosta i w związku z tym należy unikatowych portów. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Z dynamiczne przypisywanie portów to ustawienie zapobiega hello pomylone tożsamości problem opisany wcześniej. |
| Wartość InstanceCount | wszystkie | Liczba wystąpień Hello ustawienie można skonfigurować tooany wartość niezbędne toooperate hello usługi. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Tylko wewnętrznie usługi stanowej platformy ASP.NET Core
Stanowe usług, które są wywoływać tylko z wewnątrz klastra hello należy używać portów przypisywany dynamicznie tooensure współpracy między wieloma usługami. Zaleca się Hello następującej konfiguracji:

|  |  | **Uwagi** |
| --- | --- | --- |
| Serwer sieci Web | kestrel | Witaj `WebListenerCommunicationListener` nie jest przeznaczony do użytku przez usługi stanowej w których replik udziału procesu hosta. |
| Konfiguracja portów | przypisywane dynamicznie | Wiele replik usługi stanowej może udostępnić procesu hosta lub systemu operacyjnego hosta i w związku z tym należy unikatowych portów. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Z dynamiczne przypisywanie portów to ustawienie zapobiega hello pomylone tożsamości problem opisany wcześniej. |

## <a name="next-steps"></a>Następne kroki
[Debugowanie aplikacji sieci szkieletowej usług za pomocą programu Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
