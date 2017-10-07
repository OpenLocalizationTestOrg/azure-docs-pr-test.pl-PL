---
title: "aaaDiagnose błędów i wyjątków w sieci web aplikacji za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przechwytywanie wyjątków w aplikacji ASP.NET oraz dane telemetryczne żądania."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnozowanie wyjątków w aplikacjach sieci web za pomocą usługi Application Insights
Wyjątki w aplikacji sieci web na żywo są zgłaszane przez [usługi Application Insights](app-insights-overview.md). Żądań zakończonych niepowodzeniem może być zgodne z wyjątków oraz inne zdarzenia na powitania klienta i serwera, dzięki czemu można szybko diagnozowania przyczyn hello.

## <a name="set-up-exception-reporting"></a>Konfigurowanie zgłoszenie wyjątku
* toohave wyjątki zgłaszane przez aplikację serwera:
  * Zainstaluj [zestaw SDK usługi Application Insights](app-insights-asp-net.md) w kodzie aplikacji lub
  * Serwery sieci web usług IIS: Uruchom [agenta Application Insights](app-insights-monitor-performance-live-website-now.md); lub
  * Aplikacje sieci web platformy Azure: Dodaj hello [rozszerzenie usługi Application Insights](app-insights-azure-web-apps.md)
  * Aplikacje sieci web Java: hello instalacji [agenta Java](app-insights-java-agent.md)
* Zainstaluj hello [fragment kodu JavaScript](app-insights-javascript.md) w listy wyjątków przeglądarki toocatch stron sieci web.
* W niektórych struktur aplikacji lub z niektórymi ustawieniami, potrzebujesz tootake toocatch pewnych dodatkowych czynności więcej wyjątków:
  * [Formularze sieci Web](#web-forms)
  * [MVC](#mvc)
  * [1.* interfejsu API sieci Web](#web-api-1)
  * [2.* interfejsu API sieci Web](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnozowanie wyjątków przy użyciu programu Visual Studio
Otwórz rozwiązanie aplikacji hello w Visual Studio toohelp z debugowaniem.

Uruchamianie aplikacji hello na serwerze lub na komputerze deweloperskim za pomocą F5.

Otwórz okno wyszukiwania usługi Application Insights hello w programie Visual Studio i skonfigurować go toodisplay zdarzeń aplikacji. Podczas debugowania kodu, możesz to zrobić, klikając przycisk Application Insights hello.

![Kliknij prawym przyciskiem myszy projekt hello i wybierz polecenie usługi Application Insights, Otwórz.](./media/app-insights-asp-net-exceptions/34.png)

Zwróć uwagę, filtrować hello raport tooshow tylko wyjątki.

*Żadne wyjątki przedstawiający? Zobacz [przechwytywania wyjątków](#exceptions).*

Kliknij jego ślad stosu wyjątku tooshow raportu.
Kliknij przycisk informacje w wierszu w hello ślad stosu, tooopen hello odpowiedni kod pliku.  

W kodzie hello Zwróć uwagę, że CodeLens zawiera dane dotyczące wyjątków hello:

![Powiadomienie CodeLens wyjątków.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Diagnozowanie błędów przy użyciu hello portalu Azure
Z przeglądu usługi Application Insights hello aplikacji, hello błędów kafelka zawiera wykresy wyjątków i nieudanych żądań HTTP, wraz z listą hello adresów URL żądań powodujących hello najczęstsze błędy.

![Wybierz ustawienia, błędów](./media/app-insights-asp-net-exceptions/012-start.png)

Kliknij przycisk za pomocą jednego z hello nie typów wyjątków w hello listy tooget tooindividual wystąpień hello wyjątku, której można wyświetlić szczegóły hello i ślad stosu:

![Wybierz wystąpienie nieudanych żądań, a w obszarze szczegółów wyjątku, komunikat tooinstances hello wyjątek.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**Alternatywnie** można uruchomić z listy hello żądań i Znajdź tooit powiązanych wyjątków.

*Żadne wyjątki przedstawiający? Zobacz [przechwytywania wyjątków](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>I śledzenie niestandardowe dane dziennika
tooget danych diagnostycznych tooyour określonych aplikacji, można wstawić kodu toosend danych telemetrii. To wyświetlane w diagnostycznych wyszukiwania obok hello żądania, widok strony i inne dane zbierane automatycznie.

Istnieje kilka opcji:

* [Funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) jest zwykle używana do monitorowania wzorce użycia, ale hello dane wysyła również są wyświetlane w obszarze niestandardowe zdarzenia diagnostyczne wyszukiwania. Zdarzenia są nazywane i mogą przenosić właściwości ciągu lub liczbowego metryki, w których można [filtru wyszukiwania diagnostycznych](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) pozwala wysyłać dane dłużej, takie jak informacje POST.
* [Funkcji TrackException()](#exceptions) wysyła stos danych śledzenia. [Więcej informacji na temat wyjątki](#exceptions).
* Jeśli używasz już struktury rejestrowania, takich jak Log4Net lub NLog, możesz [przechwytywania tych dzienników](app-insights-asp-net-trace-logs.md) i wyświetlać je w diagnostycznych wyszukiwania obok danych żądania i wyjątków.

Otwórz te zdarzenia toosee [wyszukiwania](app-insights-diagnostic-search.md), otwórz filtru, a następnie wybierz Custom Event śledzenia i wyjątków.

![Drążenie wskroś](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Jeśli aplikacja generuje wiele telemetrii, hello adaptacyjną próbkowania modułu automatycznie zmniejsza hello wolumin, który jest wysyłany portalu toohello wysyłając reprezentatywny część zdarzeń. Zdarzenia, które są częścią hello tej samej operacji będzie być zaznaczany lub odznaczany jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń. [Więcej informacji na temat pobierania próbek.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Jak toosee żądania POST danych
Szczegóły żądania nie zawierają danych hello wysyłane tooyour aplikacji w wywołaniu POST. toohave zgłoszone dane:

* [Zainstaluj zestaw SDK hello](app-insights-asp-net.md) w projekcie aplikacji.
* Wstawianie kodu w Twojej aplikacji toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Wysyłanie danych POST hello w parametrze wiadomość hello. Brak Ogranicz rozmiar toohello dozwolone, należy spróbować toosend hello tylko istotne dane.
* Podczas badania, żądanie nie powiodło się, Znajdź hello skojarzone dane śledzenia.  

![Drążenie wskroś](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a>Przechwytywanie wyjątków i powiązane dane diagnostyczne
Na początku nie będą widzieć w portalu hello wszystkie wyjątki hello, których przyczyną błędów w aplikacji. Zobaczysz wszystkie wyjątki przeglądarki (Jeśli używasz hello [JavaScript SDK](app-insights-javascript.md) na stronach sieci web). Jednak większość serwera wyjątki są przechwytywane przez usługi IIS i masz toowrite nieco toosee kodu je.

Możesz:

* **Wyjątki rejestru jawnie** przez wstawienie kodu w wyjątkach hello tooreport programy obsługi wyjątków.
* **Przechwytywanie wyjątków automatycznie** przez skonfigurowanie struktury programu ASP.NET. dodatki niezbędne Hello są różne dla różnych typów framework.

## <a name="reporting-exceptions-explicitly"></a>Raportowanie jawnie wyjątków
Witaj Najprostszym sposobem jest tooinsert tooTrackException() wywołania programu obsługi wyjątków.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Witaj właściwości i pomiarów parametry są opcjonalne, ale są przydatne w przypadku [filtrowanie i dodawanie](app-insights-diagnostic-search.md) dodatkowe informacje. Na przykład jeśli aplikację można uruchomić kilka gier, można znaleźć wszystkie hello wyjątek raportów powiązanych tooa określonego gier. Możesz dodać dowolną liczbę elementów podczas jak tooeach słownika.

## <a name="browser-exceptions"></a>Wyjątki przeglądarki
Większość przeglądarki wyjątki są zgłaszane.

Jeśli strony sieci web zawiera pliki skryptów z sieci dostarczania zawartości lub inne domeny, upewnij się, Twoje tag skryptu ma atrybut hello ```crossorigin="anonymous"```, i wysyła ten serwer hello [nagłówki CORS](http://enable-cors.org/). Dzięki temu będzie można tooget ślad stosu i szczegóły dla nieobsłużonych wyjątków JavaScript z tych zasobów.

## <a name="web-forms"></a>Formularze sieci Web
W formularzach sieci web hello moduł HTTP będą mogli toocollect hello wyjątki podczas nie ma żadnych przekierowuje skonfigurowano CustomErrors.

Ale jeśli masz active przekierowuje dodać powitania po funkcji Application_Error toohello wiersze w Global.asax.cs. (Dodaj plik Global.asax, jeśli nie został wcześniej).

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Jeśli hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) konfiguracja jest `Off`, a następnie wyjątki będą dostępne dla hello [moduł HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Jednak jeśli jest `RemoteOnly` (ustawienie domyślne) lub `On`, hello wyjątek zostanie wyczyszczony i zbierać tooautomatically nie są dostępne dla usługi Application Insights. Możesz rozwiązać ten problem, zastępowanie hello [klasy System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)i stosowanie hello przesłonięcia klasy, jak pokazano na powitania MVC wersje poniżej ([źródła github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Zastąp atrybutu HandleError hello nowy atrybut w kontrolerach.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Próbki](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Zarejestruj `AiHandleErrorAttribute` jako filtr globalny w Global.asax.cs:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Próbki](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
AiHandleErrorAttribute rejestru jako filtr globalny w FilterConfig.cs:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Próbki](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Interfejs API sieci Web 1.x
Zastąp System.Web.Http.Filters.ExceptionFilterAttribute:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Możesz dodawania kontrolerów toospecific tego atrybutu przesłoniętej lub dodać toohello filtrów globalnych konfiguracji w klasa WebApiConfig hello:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Próbki](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Brak liczbę przypadków mogących hello filtry wyjątków nie może obsłużyć. Na przykład:

* Wyjątki generowane z konstruktorami kontrolera.
* Wyjątków zgłaszanych przez programy obsługi wiadomości.
* Wyjątki generowane podczas routingu.
* Wyjątki generowane podczas serializacji treści odpowiedzi.

## <a name="web-api-2x"></a>Interfejs API sieci Web 2.x
Dodaj implementacji interfejsu IExceptionLogger:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Dodaj ten usług toohello WebApiConfig:

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Próbki](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

Opis rozwiązań alternatywnych można:

1. Zastąp hello tylko ExceptionHandler niestandardowych implementacji IExceptionHandler. Jest to nazywane tylko, gdy hello framework jest nadal toochoose toosend (nie po hello połączenie zostało przerwane dla wystąpienia) komunikatu odpowiedzi, które
2. Filtry wyjątków (zgodnie z opisem w sekcji hello na kontrolerach 1.x interfejsu API sieci Web powyżej) — nie jest wywoływana we wszystkich przypadkach.

## <a name="wcf"></a>WCF
Dodaj klasę Attribute i implementującą interfejsy IErrorHandler i IServiceBehavior.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Dodaj implementacji usługi toohello atrybutu hello:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Próbki](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Liczniki wydajności wyjątku
Jeśli masz [zainstalowany Agent Insights aplikacji hello](app-insights-monitor-performance-live-website-now.md) na serwerze, można uzyskać wykresu hello wyjątki szybkości, mierząc .NET. Dotyczy to zarówno obsłużonych i nieobsłużonych wyjątków .NET.

Otwiera blok Explorer metryki, Dodaj nowy wykres i wybierz **szybkość wyjątek**, to wymienione w obszarze liczników wydajności.

Hello .NET framework szybkość hello jest obliczana przez zliczanie hello liczba wyjątków w interwale i podzielenie przez długość interwału powitania hello.

Należy pamiętać, że będzie się różnił od obliczana przez portal usługi Application Insights hello na podstawie raportów TrackException liczba wyjątków"hello". interwałami próbkowania Hello są różne, a hello zestawu SDK nie wysyłaj raportów TrackException wszystkich obsłużonych i nieobsłużonych wyjątków.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Następne kroki
* [Monitorowanie REST, SQL i innych toodependencies wywołania](app-insights-asp-net-dependencies.md)
* [Czas ładowania strony monitora, wyjątki przeglądarki i wywołania AJAX](app-insights-javascript.md)
* [Liczniki Monitora wydajności](app-insights-performance-counters.md)
