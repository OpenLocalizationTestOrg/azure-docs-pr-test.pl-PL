---
title: "aaaFiltering i przetwarzania wstępnego w hello zestaw SDK usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Zapisać procesorów Telemetrii i danych Telemetrycznych Inicjatory dla hello SDK toofilter lub dodać właściwości toohello danych przed wysłaniem danych telemetrycznych hello toohello portalu Application Insights."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Filtrowanie i przetwarzania wstępnego telemetrii w hello zestaw SDK usługi Application Insights


Możesz wpisać i skonfigurować dodatki hello zestaw SDK usługi Application Insights toocustomize jak przechwycone dane telemetryczne i przetworzone przed wysłaniem toohello usługa Application Insights.

* [Próbkowanie](app-insights-sampling.md) zmniejsza hello ilość danych telemetrycznych bez wpływu na statystyk. Przechowuje się ze sobą powiązane punktów danych, dzięki czemu można przechodzić między nimi podczas diagnozowania problemu. W portalu hello całkowitej liczby hello są pomnożonych toocompensate do próbkowania hello.
* Filtrowanie danych Telemetrycznych procesorów [dla platformy ASP.NET](#filtering) lub [Java](app-insights-java-filter-telemetry.md) pozwala wybrać lub zmodyfikować telemetrii w hello SDK przed wysłaniem toohello serwera. Na przykład można zmniejszyć hello ilość danych telemetrycznych, wyłączając żądań z robotów. Ale filtrowanie jest bardziej podstawową ruchu tooreducing podejście niż próbkowania. Umożliwia większą kontrolę nad co to są przesyłane, ale masz toobe pamiętać, że ma to wpływ na statystyk — na przykład, jeśli odfiltrowywania wszystkich pomyślnych żądań.
* [Inicjatory telemetrii dodać właściwości](#add-properties) tooany danych telemetrycznych wysłanych z aplikacji, w tym dane telemetryczne z hello standardowe moduły. Na przykład można dodać wartości obliczeniowej. lub numery wersji, przez który dane hello toofilter w portalu hello.
* [Witaj interfejsu API zestawu SDK](app-insights-api-custom-events-metrics.md) jest używane toosend niestandardowe zdarzenia i metryki.

Przed rozpoczęciem:

* Zainstaluj usługi Application Insights hello [zestawu SDK dla platformy ASP.NET](app-insights-asp-net.md) lub [zestawu SDK dla języka Java](app-insights-java-get-started.md) w aplikacji.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filtrowanie: ITelemetryProcessor
Ta metoda umożliwia bardziej bezpośrednią kontrolę nad co to jest dołączone lub wykluczone ze strumienia danych telemetrycznych hello. Może być używany w połączeniu z włączonym próbkowaniem, lub oddzielnie.

telemetrii toofilter zapisu procesora telemetrii i zarejestrowanie go za pomocą hello zestawu SDK. Wszystkie dane telemetryczne przechodzi przez procesor, a użytkownik może wybrać toodrop z hello strumienia lub dodać właściwości. W tym dane telemetryczne z hello standardowe moduły, takich jak moduł zbierający żądania HTTP hello i hello zależności zbierający, a także dane telemetryczne zapisane samodzielnie. Na przykład można odfiltrować dane telemetryczne dotyczące żądań z robotów lub wywołania zależności powiodło się.

> [!WARNING]
> Filtrowanie hello danych telemetrycznych wysłanych z hello SDK procesorów można pochylanie hello statystyk w portalu hello i stał się toofollow trudne powiązanych elementów.
>
> Zamiast tego Rozważ użycie [próbkowania](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Utwórz procesora telemetrii (C#)
1. Sprawdź, że hello zestaw SDK usługi Application Insights w projekcie jest w wersji 2.0.0 lub nowszej. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie Zarządzaj pakietami NuGet. W Menedżerze pakietów NuGet Sprawdź Microsoft.ApplicationInsights.Web.
2. toocreate filtru, zaimplementować ITelemetryProcessor. Jest to inny punkt rozszerzalności, takich jak moduł telemetrii, inicjatora telemetrii i kanału danych telemetrycznych.

    Zwróć uwagę, że procesorów Telemetrii utworzyć łańcuch przetwarzania. Można utworzyć wystąpienia procesora telemetrii, należy przekazać dalej procesor toohello łącze w łańcuchu hello. Po upływie toohello proces metody punktu danych telemetrycznych jego działa i następnie wywołania hello dalej procesora Telemetrii w łańcuchu hello.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Wstaw ApplicationInsights.config to:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Jest to hello tej samej sekcji, w którym zainicjować filtru próbkowania.)

Można przekazać wartości ciągu z pliku .config hello, zapewniając publicznej właściwości o nazwie w klasie.

> [!WARNING]
> Zajmie się nazwą typu hello toomatch oraz nazwy właściwości w klasie toohello pliku .config hello i nazwy właściwości w kodzie hello. Jeśli pliku .config hello odwołuje się do nieistniejącego typu lub właściwości, hello SDK może dyskretnie nie toosend żadnych danych telemetrycznych.
>
>

**Alternatywnie** można zainicjować filtru hello w kodzie. W klasie inicjowania odpowiedniego — na przykład AppStart Global.asax.cs - Wstaw procesora do łańcucha hello:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

TelemetryClients utworzone po tym punkcie będzie używać procesorów.

### <a name="example-filters"></a>Przykładowe filtry
#### <a name="synthetic-requests"></a>Syntetyczne żądań
Filtrowanie testów robotów i sieci web. Chociaż zapewnia Eksploratora metryk hello toofilter opcji limit syntetycznego źródła, tej opcji zmniejsza ruch przez filtrowanie ich na powitania zestawu SDK.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Uwierzytelnianie nie powiodło się
Filtrowanie żądań z odpowiedzi "401".

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Odfiltrować wywołania zależności fast zdalnego
Jeśli chcesz tylko wywołania toodiagnose, które są przetwarzane wolno, odfiltrować fast hello z nich.

> [!NOTE]
> Pochylanie przypadku statystyk hello, który zostanie wyświetlony w portalu hello. wykres zależności Hello będzie wyglądać tak, jakby wywołania zależności hello są wszystkie błędy.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Diagnozowanie problemów z zależnością
[Ten blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) opisano problemy zależności toodiagnose projektu automatycznie wysyłając toodependencies regularne polecenia ping.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Dodaj właściwości: ITelemetryInitializer
Dane telemetryczne inicjatory toodefine globalnych właściwości, które są wysyłane za pomocą wszystkie dane telemetryczne; i toooverride zachowanie hello telemetrii standardowe moduły.

Na przykład hello usługi Application Insights dla sieci Web pakietu zbiera dane telemetryczne dotyczące żądania HTTP. Domyślnie flagi jako zakończony niepowodzeniem, wszystkie żądania z kodem odpowiedzi > = 400. Ale jeśli chcesz tootreat 400 jako sukcesu, udostępniają inicjatora telemetrii, która ustawia właściwość Powodzenie hello.

Jeśli podasz inicjatora telemetrii, jest ona wywoływana przy każdym poszczególnych hello Track*() nosi nazwę metody. Dotyczy to również metody wywołane przez hello telemetrii standardowe moduły. Konwencja te moduły nie należy ustawiać dowolnej właściwości, która została już ustawiona przez inicjatora.

**Zdefiniuj z inicjatora**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Ładowanie z inicjatora**

W ApplicationInsights.config:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*Alternatywnie* można utworzyć wystąpienia inicjatora hello w kodzie, na przykład w pliku Global.aspx.cs:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Zobacz więcej w tym przykładzie.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>Inicjatory telemetrii JavaScript
*JavaScript*

Wstaw inicjatora telemetrii natychmiast po kod inicjujący hello pochodzący z portalu hello:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Podsumowanie właściwości niestandardowych z systemem innym niż hello dostępnych na powitania telemetryItem, zobacz [Model danych eksportu Insights aplikacji](app-insights-export-data-model.md).

Możesz dodać dowolną liczbę inicjatory dowolnie.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor i ITelemetryInitializer
Co to jest hello różnica między inicjatory telemetrii i danych telemetrycznych procesorów?

* Istnieją pewne nakładania się w co można zrobić z nimi: zarówno mogą być używane tooadd tootelemetry właściwości.
* TelemetryInitializers są zawsze uruchamiane przed TelemetryProcessors.
* TelemetryProcessors pozwala zastąpić toocompletely lub odrzucić elementu telemetrii.
* TelemetryProcessors nie Przetwarzaj telemetrii licznika wydajności.


## <a name="reference-docs"></a>Dokumentacja
* [Przegląd interfejsu API](app-insights-api-custom-events-metrics.md)
* [Platformy ASP.NET — dokumentacja](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>Kod zestawu SDK
* [Platformy ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Zestaw SDK dla języka JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Następne kroki
* [Wyszukiwanie zdarzeń i dzienniki](app-insights-diagnostic-search.md)
* [Próbkowanie](app-insights-sampling.md)
* [Rozwiązywanie problemów](app-insights-troubleshoot-faq.md)
