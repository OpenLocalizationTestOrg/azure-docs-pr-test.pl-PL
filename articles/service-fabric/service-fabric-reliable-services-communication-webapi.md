---
title: Komunikacja aaaService z hello interfejsu API sieci Web programu ASP.NET | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak krok po kroku przy użyciu komunikacji usługi tooimplement hello interfejsu API sieci Web platformy ASP.NET z OWIN hostingu samodzielnego w hello niezawodnej usługi interfejsu API."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Wprowadzenie: usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN
Sieć szkieletowa usług Azure umieszcza hello zasilania w dłoni podczas wybierania jest sposób toocommunicate Twojego usług z użytkownikami i ze sobą. Ten samouczek koncentruje się na implementacji komunikacji usług za pomocą interfejsu API sieci Web platformy ASP.NET z interfejsu Open Web dla interfejsu API usługi Service Fabric niezawodnej usługi hostingu samodzielnego .NET (OWIN). Firma Microsoft będzie poznaj dok³adniejsze opisy wybranych głęboko do hello podłączany komunikacji niezawodnej usługi interfejsu API. Użyjemy interfejsu API sieci Web w tooshow krok po kroku przykładu możesz jak tooset się odbiornik komunikacji niestandardowych.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Wprowadzenie tooWeb interfejsu API w sieci szkieletowej usług
Interfejs API sieci Web platformy ASP.NET to platforma popularnych i wydajne do tworzenia interfejsów API HTTP na powitania .NET Framework. Jeśli nie masz już znasz hello framework, zobacz [wprowadzenie do korzystania z programu ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn więcej.

Interfejs API sieci Web w sieci szkieletowej usług jest hello tej samej sieci Web interfejsu API platformy ASP.NET znają i lubią. Witaj różnicą jest sposób możesz *hosta* aplikacji interfejsu API sieci Web. Microsoft Internet Information Services (IIS) nie będzie używany. toobetter zrozumieć różnicę hello, możemy podzielić je na dwie części:

1. Witaj aplikacji interfejsu API sieci Web (w tym kontrolerów i modeli)
2. Witaj hosta (powitania serwera sieci web, zazwyczaj usług IIS)

Nie zmienia samej aplikacji interfejsu API sieci Web. Go nie różni się od aplikacji interfejsu API sieci Web, które zostały zapisane w przeszłości hello i Przenieś stanie toosimply powinien być w większości kod aplikacji. Ale jeśli już zostało hosting w usługach IIS, w których host aplikacji hello może być nieco inne niż czego umożliwia. Przed uzyskujemy toohello hosting części Zacznijmy coś więcej dobrze znany: hello aplikacji interfejsu API sieci Web.

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
Rozpocznij od utworzenia nowej aplikacji platformy Service Fabric przy użyciu jednej usługi bezstanowej w programie Visual Studio 2015.

Szablon programu Visual Studio dla usługi bezstanowej przy użyciu interfejsu API sieci Web jest dostępna tooyou. W tym samouczku firma Microsoft będzie zbudować projekt interfejsu API sieci Web od podstaw, którego wynikiem co otrzyma, w przypadku wybrania tego szablonu.

Wybierz puste toolearn projektu usługi bezstanowej jak toobuild projekt interfejsu API sieci Web od podstaw, lub można rozpoczynać się od usługi bezstanowej hello szablonu interfejsu API sieci Web i po prostu odbiorze.  

pierwszym krokiem Hello jest toopull w niektórych pakietów NuGet dla interfejsu API sieci Web. chcemy toouse pakietów Hello jest Microsoft.AspNet.WebApi.OwinSelfHost. Ten pakiet zawiera wszystkie hello wymaganych pakietów interfejsu API sieci Web i hello *hosta* pakietów. Jest to ważne później.

Po zainstalowaniu pakietów hello można rozpocząć zbudowaniu hello podstawowej struktury projektu interfejsu API sieci Web. Jeśli używano interfejsu API sieci Web, hello struktury projektu powinna wyglądać bardzo znajomo. Rozpocznij od dodania `Controllers` katalogu i kontrolera proste wartości:

**ValuesController.cs**

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

Następnie Dodaj klasę uruchamiania routingu hello projektu głównego tooregister hello, elementy formatujące i inne ustawienia konfiguracji. Dotyczy to również gdzie interfejsu API sieci Web podłącza toohello *hosta*, który będzie można uruchomić ponownie później. 

**Startup.CS**

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

To wszystko dla części aplikacji hello. W tym momencie skonfigurowaliśmy tylko hello podstawowy interfejs API sieci Web projektu układ. Do tej pory nie powinien wyglądać wiele różnych z projektów interfejsu API sieci Web, które zostały zapisane w przeszłości hello lub hello podstawowy szablon interfejsu API sieci Web. Logiki biznesowej przechodzi w kontrolerach hello i modeli w zwykły sposób.

Teraz możemy czego o hostingu, aby firma Microsoft może faktycznie uruchomić?

## <a name="service-hosting"></a>Usługa hostingu
W sieci szkieletowej usług, usługa jest uruchomiona *procesu hosta usługi*, plik wykonywalny, który uruchamia kodu usługi. Podczas pisania usługi za pomocą hello niezawodnej usługi interfejsu API projekt usługi właśnie kompiluje tooan plik wykonywalny, który rejestruje danego typu usługi i uruchamia kod. Dotyczy to w większości przypadków podczas pisania usługi w sieci szkieletowej usług w programie .NET. Po otwarciu pliku Program.cs w projekcie usługi bezstanowej hello powinien zostać wyświetlony:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Jeśli to wygląda podejrzanie aplikacji konsoli tooa punktu wejścia hello, który jest ponieważ jest on.

Szczegółowe informacje na temat hello procesu hosta usługi i usługi rejestracji wykraczają poza zakres tego artykułu hello. Jednak jest ważne tooknow dla teraz, gdy *kodu usługi działa we własnym procesie*.

## <a name="self-host-web-api-with-an-owin-host"></a>Host samodzielny interfejsu API sieci Web z hostem OWIN
Biorąc pod uwagę, że kod aplikacji interfejsu API sieci Web znajduje się w swoim własnym procesie, jak możesz Podłączanie go tooa serwera sieci web? Wprowadź [OWIN](http://owin.org/). OWIN jest po prostu Umowa między serwerami sieci web i aplikacji sieci web platformy .NET. Tradycyjnie użycie programu ASP.NET (w górę tooMVC 5), aplikacji sieci web hello jest silnie sprzężonego tooIIS za pośrednictwem System.Web. Jednak interfejsu API sieci Web implementuje OWIN, więc pisania aplikacji sieci web, która jest całkowicie niezależna od hello serwera sieci web, który go obsługuje. W związku z tym można użyć *hosta samodzielnego* OWIN serwera sieci web można uruchomić w własnego procesu. To jest dopasowany hello sieci szkieletowej usług hostingu model firma opisana.

W tym artykule użyjemy Katana jako hello OWIN hosta dla hello aplikacji interfejsu API sieci Web. Katana jest implementacją hosta OWIN open source oparty na [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) i hello Windows [interfejsu API serwera HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> więcej informacji na temat Katana, przejdź toohello toolearn [lokacji Katana](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Aby uzyskać szybki przegląd jak toouse Katana tooself hosta sieci Web interfejsu API, zobacz [OWIN Użyj hosta tooSelf ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Konfigurowanie serwera sieci web hello
Hello niezawodnej usługi interfejsu API zapewnia punkt wejścia komunikacji, gdzie można podłączyć stosach komunikacji, które umożliwiają użytkownikom i klientów tooconnect toohello usługi:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

powitania serwera sieci web (i innych stosu komunikacji używanych w przyszłych, takie jak protokół WebSockets hello) należy używać hello ICommunicationListener interfejsu toointegrate poprawnie hello systemu. Witaj przyczyn tej staną się bardziej widoczne w hello następujące kroki.

Najpierw Utwórz klasę o nazwie OwinCommunicationListener, który implementuje ICommunicationListener:

**OwinCommunicationListener.cs**

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

Interfejs ICommunicationListener Hello udostępnia trzy metody toomanage odbiornik komunikacji usługi:

* *OpenAsync*. Rozpocznij nasłuchiwanie żądań.
* *CloseAsync*. Zatrzymaj nasłuchiwanie żądań, Zakończ wszystkie żądania locie i bezpiecznie zamknąć.
* *Przerwij*. Anulować wszystkie i zatrzymać natychmiast.

tooget pracę, dodawanie członków prywatnych klasy, do odbiornika hello rzeczy, należy toofunction. Te zostanie zainicjowany przez Konstruktor hello i będzie używana później podczas konfigurowania hello nasłuchiwania adresu URL.

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a>Implementowanie OpenAsync
tooset powitania serwera sieci web, potrzebne informacje:

* *Prefiks adresu URL ścieżki*. Mimo że jest to opcjonalne, jest dobra dla tooset możesz tego teraz up, dzięki czemu można bezpiecznie obsługiwać wiele usług sieci web w aplikacji.
* *Port*.

Przed uzyskanie portu dla serwera sieci web hello jest ważne, że rozumiesz, że Usługa Service Fabric realizuje warstwa aplikacji, która pełni rolę bufora między aplikacji i hello podstawowego systemu operacyjnego, który jest uruchamiany na. W efekcie Usługa Service Fabric realizuje tooconfigure sposób *punkty końcowe* dla usług. Sieci szkieletowej usług gwarantuje, że punkty końcowe są dostępne dla Twojej toouse usługi. Dzięki temu masz tooconfigure je samodzielnie w hello podstawowego środowiska systemu operacyjnego. Można łatwo hostowania aplikacji usługi Service Fabric w różnych środowiskach bez konieczności toomake aplikacji tooyour żadnych zmian. (Na przykład można obsługiwać hello tej samej aplikacji na platformie Azure lub we własnym centrum danych.)

Skonfiguruj punkt końcowy HTTP w PackageRoot\ServiceManifest.xml:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Ten krok jest ważne, ponieważ proces hosta usługi hello jest uruchamiany w ograniczonym poświadczeń (Usługa sieciowa w systemie Windows). Oznacza to, z usługą nie będziesz mieć dostępu tooset się punkt końcowy HTTP samodzielnie. Przy użyciu konfiguracji punktu końcowego hello, usługi Service Fabric wie tooset się hello odpowiednią listę kontroli dostępu (ACL) dla adresu URL, który hello usługi będzie nasłuchiwać powitalne. Sieć szkieletowa usług również miejsce na standardowej tooconfigure punktów końcowych.

W OwinCommunicationListener.cs można uruchomić implementacji OpenAsync. Jest to, gdzie uruchomić powitania serwera sieci web. Najpierw Pobierz informacje o punkcie końcowym hello i Utwórz hello adres URL, który będzie nasłuchiwać hello usługi. adres URL Hello może się różnić w zależności od tego, czy odbiornik hello jest używany w usługi bezstanowej lub usługi stanowej. Dla usługi stanowej hello odbiornika musi toocreate unikatowy adres dla każdej repliki usługi stanowej go wykrywa w. W przypadku usług bezstanowych adresów hello może być znacznie prostsze. 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

Należy pamiętać, że "http://+" jest używana w tym miejscu. Jest to toomake się, że tego serwera sieci web hello nasłuchuje na wszystkich dostępnych adresów, w tym localhost, nazwy FQDN i hello IP komputera.

Witaj OpenAsync implementacja jest najważniejsze przyczyny hello, dlaczego powitania serwera sieci web (lub dowolnego stosu komunikacji) została wdrożona jako ICommunicationListener, a nie tylko go otworzyć go bezpośrednio z `RunAsync()` hello usługi. Witaj wartość zwrotną z elementu OpenAsync jest nasłuchuje adres hello hello serwera sieci web. Gdy ten adres jest zwracany toohello systemu, rejestruje hello adresu z usługą hello. Usługa sieci szkieletowej udostępnia interfejs API umożliwiający klientów i innych usług toothen poprosić dla tego adresu według nazwy usługi. Jest to ważne, ponieważ adres usługi hello nie jest statyczne. Usługi są przenoszone w klastrze hello do celów dostępności i równoważenia zasobów. Jest to mechanizm hello, który umożliwia klientom Witaj tooresolve nasłuchiwania adresów dla usługi.

Ten fakt OpenAsync uruchamia serwer sieci web hello i zwraca hello adres, który jest nasłuchiwanie. Należy pamiętać, że nasłuchuje "http://+", ale przed OpenAsync zwraca adres hello, Witaj "+" jest zastępowany hello adres IP lub nazwa FQDN węzła hello, który jest obecnie na. Hello adres, który jest zwracany przez tę metodę jest, co jest zarejestrowany w systemie hello. Istnieje również jakie klientów i innych usług, wyświetlać, gdy został poproszony o adresu usługi. Dla klientów toocorrectly połączenia tooit, potrzebują rzeczywisty adres IP lub nazwę FQDN adresu hello.

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

Należy pamiętać, że to odwołuje się do klasy uruchamiania hello, która została przekazana toohello OwinCommunicationListener w Konstruktorze hello. To wystąpienie uruchamiania jest używany przez hello powitania toobootstrap serwera sieci web aplikacji interfejsu API sieci Web.

Witaj `ServiceEventSource.Current.Message()` wiersza zostaną wyświetlone w oknie zdarzeń diagnostycznych hello później, po uruchomieniu tooconfirm aplikacji hello tego serwera sieci web hello została uruchomiona pomyślnie.

## <a name="implement-closeasync-and-abort"></a>Implementowanie CloseAsync i przerwania
Ponadto wdrożenie zarówno CloseAsync i Abort serwera sieci web hello toostop. serwer sieci web Hello może zostać zatrzymana przez usuwanie hello dojścia serwera, który został utworzony podczas OpenAsync.

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

W tym przykładzie implementacji zarówno CloseAsync, jak i przerwania po prostu Zatrzymaj powitania serwera sieci web. Można wybrać opcję tooperform bardziej bezpiecznie skoordynowany sposób wyłączania powitania serwera sieci web w CloseAsync. Na przykład zamykania hello można poczekaj zakończona, zanim zwracać hello toobe locie żądań.

## <a name="start-hello-web-server"></a>Uruchamianie powitania serwera sieci web
Jest teraz gotowy toocreate i zwrócić wystąpienia serwera sieci web hello toostart OwinCommunicationListener. Po powrocie do hello klasy usługi (WebService.cs), należy zastąpić hello `CreateServiceInstanceListeners()` metody:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

Gdzie jest to hello interfejsu API sieci Web *aplikacji* i hello OWIN *hosta* spełnia finally. Witaj hosta (OwinCommunicationListener) znajduje się wystąpienie hello *aplikacji* (interfejs API sieci Web) za pośrednictwem hello klasy początkowej. Usługa Service Fabric zarządza następnie cykl życia. Tego samego wzorca zwykle można wykonać z dowolnego stosu komunikacji.

## <a name="put-it-all-together"></a>Zebranie wszystkich elementów
W tym przykładzie, nie potrzebujesz toodo cokolwiek w hello `RunAsync()` metody, więc po prostu można usunąć tego zastąpienia.

implementacji usługi końcowego Hello powinny być bardzo proste. Wymaga tylko odbiornik komunikacji hello toocreate:

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

Witaj pełną `OwinCommunicationListener` klasy:

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

Teraz, gdy wszystkie elementy hello zostało umieszczone w miejscu, projektu powinna wyglądać Typowa aplikacja interfejsu API sieci Web z punktów wejścia niezawodnej usługi interfejsu API i OWIN hosta.

## <a name="run-and-connect-through-a-web-browser"></a>Uruchom i łączenie się za pośrednictwem przeglądarki sieci web
Jeśli nie zostało to jeszcze zrobione, [Konfigurowanie środowiska deweloperskiego](service-fabric-get-started.md).

Teraz możesz skompilować i wdrożyć usługę. Naciśnij klawisz **F5** w toobuild programu Visual Studio i wdrażanie aplikacji hello. W oknie zdarzeń diagnostycznych hello, powinien zostać wyświetlony komunikat wskazujący tego serwera sieci web hello otwarte na http://localhost:8281 /.

> [!NOTE]
> Jeśli hello port został już otwarty przez inny proces na komputerze, może zostać wyświetlony błąd. Oznacza to, że nie można otworzyć tego odbiornika hello. Jeśli jest przypadek hello, spróbuj użyć innego portu dla konfiguracji punktu końcowego hello w pliku ServiceManifest.xml.
> 
> 

Po uruchomieniu usługi hello, otwórz przeglądarkę i przejdź zbyt[http://localhost:8281/api/wartości](http://localhost:8281/api/values) tootest go.

## <a name="scale-it-out"></a>Skalowanie go
Skalowania aplikacji sieci web bezstanowych zwykle oznacza dodanie więcej maszyn i kręci się hello aplikacje sieci web na nich. Aparat aranżacji usługi sieć szkieletowa można to zrobić dla Ciebie zawsze, gdy tooa klastra zostaną dodane nowe węzły. Podczas tworzenia wystąpienia usługi bezstanowej, można określić numer hello wystąpień ma toocreate. Sieć szkieletowa usług umieszcza tej liczby wystąpień na węzłach w klastrze hello. I pozwala sprawdzić toocreate nie więcej niż jednego wystąpienia na dowolnego pojedynczego węzła. Można także skonfigurować usługi sieć szkieletowa tooalways Utwórz wystąpienie w każdym węźle, określając **-1** hello wystąpienia licznika. Gwarantuje to, że po dodaniu tooscale węzłów poza klastrem, wystąpienie usługi bezstanowej zostanie utworzony na powitania nowe węzły. Ta wartość jest właściwością wystąpienia usługi hello, więc jest ustawiana podczas tworzenia wystąpienia usługi. Można to zrobić za pomocą programu PowerShell:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

Ponadto można to zrobić, po zdefiniowaniu domyślnej usługi w projekcie usługi bezstanowej programu Visual Studio:

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Aby uzyskać więcej informacji na temat sposobu toocreate aplikacji i wystąpienie usługi, zobacz [wdrażania aplikacji](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Następne kroki
[Debugowanie aplikacji sieci szkieletowej usług za pomocą programu Visual Studio](service-fabric-debugging-your-application.md)

