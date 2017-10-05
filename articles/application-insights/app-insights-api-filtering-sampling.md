---
title: "Filtrowanie i przetwarzania wstępnego w zestawie SDK Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Zapisywanie procesorów Telemetrii oraz inicjatory danych Telemetrycznych zestawu SDK, filtrowanie, lub dodać właściwości do danych przed wysłaniem danych telemetrycznych do portalu usługi Application Insights."
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
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="74328-103">Filtrowanie i przetwarzania wstępnego telemetrii w zestaw SDK usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="74328-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="74328-104">Możesz wpisać i skonfigurować wtyczek dla zestawu SDK usługi Application Insights do dostosowywania jak przechwycone dane telemetryczne i przetworzone przed wysłaniem ich do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="74328-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="74328-105">[Próbkowanie](app-insights-sampling.md) zmniejsza ilość danych telemetrycznych bez wpływu na statystyk.</span><span class="sxs-lookup"><span data-stu-id="74328-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="74328-106">Przechowuje się ze sobą powiązane punktów danych, dzięki czemu można przechodzić między nimi podczas diagnozowania problemu.</span><span class="sxs-lookup"><span data-stu-id="74328-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="74328-107">W portalu całkowitej liczby są mnożone odpowiednio do pobierania próbek.</span><span class="sxs-lookup"><span data-stu-id="74328-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="74328-108">Filtrowanie danych Telemetrycznych procesorów [dla platformy ASP.NET](#filtering) lub [Java](app-insights-java-filter-telemetry.md) pozwala wybrać lub zmodyfikować danych telemetrycznych w zestawie SDK przed wysłaniem do serwera.</span><span class="sxs-lookup"><span data-stu-id="74328-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="74328-109">Na przykład można zmniejszyć ilość danych telemetrycznych, wyłączając żądań z robotów.</span><span class="sxs-lookup"><span data-stu-id="74328-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="74328-110">Ale filtrowanie jest bardziej podstawową podejście do zmniejszenie ruchu niż próbkowanie.</span><span class="sxs-lookup"><span data-stu-id="74328-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="74328-111">Umożliwia większą kontrolę nad co to są przesyłane, ale masz należy pamiętać, że ma to wpływ na statystyk — na przykład, jeśli odfiltrowywania wszystkich pomyślnych żądań.</span><span class="sxs-lookup"><span data-stu-id="74328-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="74328-112">[Inicjatory telemetrii dodać właściwości](#add-properties) do żadnych danych telemetrycznych wysłanych z aplikacji, w tym dane telemetryczne z modułów standardowych.</span><span class="sxs-lookup"><span data-stu-id="74328-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="74328-113">Na przykład można dodać wartości obliczeniowej. lub numery wersji do filtrowania danych w portalu.</span><span class="sxs-lookup"><span data-stu-id="74328-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="74328-114">[Interfejs API zestawu SDK](app-insights-api-custom-events-metrics.md) służy do wysyłania zdarzeń niestandardowych i metryki.</span><span class="sxs-lookup"><span data-stu-id="74328-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="74328-115">Przed rozpoczęciem:</span><span class="sxs-lookup"><span data-stu-id="74328-115">Before you start:</span></span>

* <span data-ttu-id="74328-116">Zainstaluj usługi Application Insights [zestawu SDK dla platformy ASP.NET](app-insights-asp-net.md) lub [zestawu SDK dla języka Java](app-insights-java-get-started.md) w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74328-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="74328-117">Filtrowanie: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="74328-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="74328-118">Ta metoda umożliwia bardziej bezpośrednią kontrolę nad co to jest dołączone lub wykluczone ze strumienia danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="74328-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="74328-119">Może być używany w połączeniu z włączonym próbkowaniem, lub oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="74328-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="74328-120">Aby filtrować dane telemetryczne, zapisać procesora telemetrii i zarejestrowanie go za pomocą zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="74328-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="74328-121">Wszystkie dane telemetryczne przechodzi przez procesor, a użytkownik może usunąć ją z strumienia lub dodać właściwości.</span><span class="sxs-lookup"><span data-stu-id="74328-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="74328-122">W tym dane telemetryczne z modułów standardowych, takich jak moduł zbierający żądania HTTP i zależności modułu zbierającego, a także dane telemetryczne zapisane samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="74328-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="74328-123">Na przykład można odfiltrować dane telemetryczne dotyczące żądań z robotów lub wywołania zależności powiodło się.</span><span class="sxs-lookup"><span data-stu-id="74328-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="74328-124">Filtrowanie telemetrycznych wysłanych z zestawu SDK procesorów można pochylanie statystyki, która zostanie wyświetlony w portalu i utrudnia wykonaj elementy powiązane.</span><span class="sxs-lookup"><span data-stu-id="74328-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="74328-125">Zamiast tego Rozważ użycie [próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="74328-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="74328-126">Utwórz procesora telemetrii (C#)</span><span class="sxs-lookup"><span data-stu-id="74328-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="74328-127">Sprawdź, czy zestaw SDK usługi Application Insights w projekcie wersji 2.0.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="74328-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="74328-128">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie Zarządzaj pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="74328-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="74328-129">W Menedżerze pakietów NuGet Sprawdź Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="74328-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="74328-130">Aby utworzyć filtr, zaimplementuj ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="74328-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="74328-131">Jest to inny punkt rozszerzalności, takich jak moduł telemetrii, inicjatora telemetrii i kanału danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="74328-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="74328-132">Zwróć uwagę, że procesorów Telemetrii utworzyć łańcuch przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="74328-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="74328-133">Można utworzyć wystąpienia procesora telemetrii, należy przekazać łącze do następnej procesora w łańcuchu.</span><span class="sxs-lookup"><span data-stu-id="74328-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="74328-134">Gdy punkt danych telemetrycznych jest przekazywany do metody procesu, nie jego pracy i następnie wywołuje dalej procesora Telemetrii w łańcuchu.</span><span class="sxs-lookup"><span data-stu-id="74328-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
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
1. <span data-ttu-id="74328-135">Wstaw ApplicationInsights.config to:</span><span class="sxs-lookup"><span data-stu-id="74328-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="74328-136">(Jest to tej samej sekcji, w którym zainicjować filtru próbkowania).</span><span class="sxs-lookup"><span data-stu-id="74328-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="74328-137">Można przekazać wartości ciągu z pliku .config, zapewniając publicznej właściwości o nazwie w klasie.</span><span class="sxs-lookup"><span data-stu-id="74328-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="74328-138">Należy zadbać, aby dopasować nazwy typu, a wszystkie nazwy właściwości w pliku .config do nazwy klasy i właściwości w kodzie.</span><span class="sxs-lookup"><span data-stu-id="74328-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="74328-139">Jeśli plik .config odwołuje się do nieistniejącego typu lub właściwości, dyskretnie może uniemożliwić Wyślij wszystkie dane telemetryczne zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="74328-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="74328-140">**Alternatywnie** można zainicjować filtru w kodzie.</span><span class="sxs-lookup"><span data-stu-id="74328-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="74328-141">W klasie inicjowania odpowiedniego — na przykład AppStart Global.asax.cs - Wstaw procesora w łańcuchu:</span><span class="sxs-lookup"><span data-stu-id="74328-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="74328-142">TelemetryClients utworzone po tym punkcie będzie używać procesorów.</span><span class="sxs-lookup"><span data-stu-id="74328-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="74328-143">Przykładowe filtry</span><span class="sxs-lookup"><span data-stu-id="74328-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="74328-144">Syntetyczne żądań</span><span class="sxs-lookup"><span data-stu-id="74328-144">Synthetic requests</span></span>
<span data-ttu-id="74328-145">Filtrowanie testów robotów i sieci web.</span><span class="sxs-lookup"><span data-stu-id="74328-145">Filter out bots and web tests.</span></span> <span data-ttu-id="74328-146">Mimo że Eksploratora metryk umożliwia filtrowanie syntetycznego źródła, tej opcji zmniejsza ruch przez filtrowanie ich na zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="74328-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="74328-147">Uwierzytelnianie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="74328-147">Failed authentication</span></span>
<span data-ttu-id="74328-148">Filtrowanie żądań z odpowiedzi "401".</span><span class="sxs-lookup"><span data-stu-id="74328-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="74328-149">Odfiltrować wywołania zależności fast zdalnego</span><span class="sxs-lookup"><span data-stu-id="74328-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="74328-150">Jeśli chcesz zdiagnozować wywołania, które są przetwarzane wolno, filtrować te fast.</span><span class="sxs-lookup"><span data-stu-id="74328-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="74328-151">Pochylanie przypadku statystyk, który zostanie wyświetlony w portalu.</span><span class="sxs-lookup"><span data-stu-id="74328-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="74328-152">Na wykresie zależności będzie wyglądać tak, jakby wywołania zależności są wszystkie błędy.</span><span class="sxs-lookup"><span data-stu-id="74328-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="74328-153">Diagnozowanie problemów z zależnością</span><span class="sxs-lookup"><span data-stu-id="74328-153">Diagnose dependency issues</span></span>
<span data-ttu-id="74328-154">[Ten blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) opisuje projektu do diagnozowania problemów zależności automatycznie przesyłając regularnego polecenia ping zależności.</span><span class="sxs-lookup"><span data-stu-id="74328-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="74328-155">Dodaj właściwości: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="74328-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="74328-156">Inicjatory telemetrii używany do definiowania właściwości globalne, które są wysyłane z wszystkie dane telemetryczne; i zastąpienie zachowania wybranych modułów standardowe telemetrii.</span><span class="sxs-lookup"><span data-stu-id="74328-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="74328-157">Na przykład pakiet sieci Web w usłudze Application Insights zbiera dane telemetryczne dotyczące żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="74328-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="74328-158">Domyślnie flagi jako zakończony niepowodzeniem, wszystkie żądania z kodem odpowiedzi > = 400.</span><span class="sxs-lookup"><span data-stu-id="74328-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="74328-159">Ale zaliczenie 400 sukcesu, możesz podać inicjatora telemetrii, która ustawia właściwość Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="74328-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="74328-160">Jeśli podasz inicjatora telemetrii jest wywoływana po każdej zmianie dowolnej z metod Track*() jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="74328-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="74328-161">Dotyczy to również metody wywołane przez moduły standardowe telemetrii.</span><span class="sxs-lookup"><span data-stu-id="74328-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="74328-162">Konwencja te moduły nie należy ustawiać dowolnej właściwości, która została już ustawiona przez inicjatora.</span><span class="sxs-lookup"><span data-stu-id="74328-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="74328-163">**Zdefiniuj z inicjatora**</span><span class="sxs-lookup"><span data-stu-id="74328-163">**Define your initializer**</span></span>

<span data-ttu-id="74328-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="74328-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
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
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="74328-165">**Ładowanie z inicjatora**</span><span class="sxs-lookup"><span data-stu-id="74328-165">**Load your initializer**</span></span>

<span data-ttu-id="74328-166">W ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="74328-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="74328-167">*Alternatywnie* można utworzyć wystąpienia inicjatora w kodzie, na przykład w pliku Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="74328-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="74328-168">Zobacz więcej w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="74328-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="74328-169">Inicjatory telemetrii JavaScript</span><span class="sxs-lookup"><span data-stu-id="74328-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="74328-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="74328-170">*JavaScript*</span></span>

<span data-ttu-id="74328-171">Wstaw inicjatora telemetrii bezpośrednio po kodzie inicjowania pochodzący z portalu:</span><span class="sxs-lookup"><span data-stu-id="74328-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

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

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="74328-172">Podsumowanie właściwości niestandardowych z systemem innym niż dostępna w telemetryItem, zobacz [Model danych eksportu Insights aplikacji](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="74328-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="74328-173">Możesz dodać dowolną liczbę inicjatory dowolnie.</span><span class="sxs-lookup"><span data-stu-id="74328-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="74328-174">ITelemetryProcessor i ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="74328-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="74328-175">Jaka jest różnica między procesorami telemetrii i danych telemetrycznych inicjatory?</span><span class="sxs-lookup"><span data-stu-id="74328-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="74328-176">Istnieją pewne nakładania się w co można zrobić z nimi: zarówno pozwala dodać właściwości do danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="74328-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="74328-177">TelemetryInitializers są zawsze uruchamiane przed TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="74328-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="74328-178">TelemetryProcessors umożliwiają całkowicie zastąpić lub odrzucić element telemetrii.</span><span class="sxs-lookup"><span data-stu-id="74328-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="74328-179">TelemetryProcessors nie Przetwarzaj telemetrii licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="74328-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="74328-180">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="74328-180">Reference docs</span></span>
* [<span data-ttu-id="74328-181">Przegląd interfejsu API</span><span class="sxs-lookup"><span data-stu-id="74328-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="74328-182">Platformy ASP.NET — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="74328-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="74328-183">Kod zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="74328-183">SDK Code</span></span>
* [<span data-ttu-id="74328-184">Platformy ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="74328-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="74328-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="74328-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="74328-186">Zestaw SDK dla języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="74328-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="74328-187"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74328-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="74328-188">Wyszukiwanie zdarzeń i dzienniki</span><span class="sxs-lookup"><span data-stu-id="74328-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="74328-189">Próbkowanie</span><span class="sxs-lookup"><span data-stu-id="74328-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="74328-190">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="74328-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
