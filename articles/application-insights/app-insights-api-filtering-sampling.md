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
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="c2beb-103">Filtrowanie i przetwarzania wstępnego telemetrii w hello zestaw SDK usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c2beb-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="c2beb-104">Możesz wpisać i skonfigurować dodatki hello zestaw SDK usługi Application Insights toocustomize jak przechwycone dane telemetryczne i przetworzone przed wysłaniem toohello usługa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c2beb-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="c2beb-105">[Próbkowanie](app-insights-sampling.md) zmniejsza hello ilość danych telemetrycznych bez wpływu na statystyk.</span><span class="sxs-lookup"><span data-stu-id="c2beb-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="c2beb-106">Przechowuje się ze sobą powiązane punktów danych, dzięki czemu można przechodzić między nimi podczas diagnozowania problemu.</span><span class="sxs-lookup"><span data-stu-id="c2beb-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="c2beb-107">W portalu hello całkowitej liczby hello są pomnożonych toocompensate do próbkowania hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="c2beb-108">Filtrowanie danych Telemetrycznych procesorów [dla platformy ASP.NET](#filtering) lub [Java](app-insights-java-filter-telemetry.md) pozwala wybrać lub zmodyfikować telemetrii w hello SDK przed wysłaniem toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c2beb-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="c2beb-109">Na przykład można zmniejszyć hello ilość danych telemetrycznych, wyłączając żądań z robotów.</span><span class="sxs-lookup"><span data-stu-id="c2beb-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="c2beb-110">Ale filtrowanie jest bardziej podstawową ruchu tooreducing podejście niż próbkowania.</span><span class="sxs-lookup"><span data-stu-id="c2beb-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="c2beb-111">Umożliwia większą kontrolę nad co to są przesyłane, ale masz toobe pamiętać, że ma to wpływ na statystyk — na przykład, jeśli odfiltrowywania wszystkich pomyślnych żądań.</span><span class="sxs-lookup"><span data-stu-id="c2beb-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="c2beb-112">[Inicjatory telemetrii dodać właściwości](#add-properties) tooany danych telemetrycznych wysłanych z aplikacji, w tym dane telemetryczne z hello standardowe moduły.</span><span class="sxs-lookup"><span data-stu-id="c2beb-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="c2beb-113">Na przykład można dodać wartości obliczeniowej. lub numery wersji, przez który dane hello toofilter w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="c2beb-114">[Witaj interfejsu API zestawu SDK](app-insights-api-custom-events-metrics.md) jest używane toosend niestandardowe zdarzenia i metryki.</span><span class="sxs-lookup"><span data-stu-id="c2beb-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="c2beb-115">Przed rozpoczęciem:</span><span class="sxs-lookup"><span data-stu-id="c2beb-115">Before you start:</span></span>

* <span data-ttu-id="c2beb-116">Zainstaluj usługi Application Insights hello [zestawu SDK dla platformy ASP.NET](app-insights-asp-net.md) lub [zestawu SDK dla języka Java](app-insights-java-get-started.md) w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2beb-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="c2beb-117">Filtrowanie: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="c2beb-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="c2beb-118">Ta metoda umożliwia bardziej bezpośrednią kontrolę nad co to jest dołączone lub wykluczone ze strumienia danych telemetrycznych hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="c2beb-119">Może być używany w połączeniu z włączonym próbkowaniem, lub oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="c2beb-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="c2beb-120">telemetrii toofilter zapisu procesora telemetrii i zarejestrowanie go za pomocą hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c2beb-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="c2beb-121">Wszystkie dane telemetryczne przechodzi przez procesor, a użytkownik może wybrać toodrop z hello strumienia lub dodać właściwości.</span><span class="sxs-lookup"><span data-stu-id="c2beb-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="c2beb-122">W tym dane telemetryczne z hello standardowe moduły, takich jak moduł zbierający żądania HTTP hello i hello zależności zbierający, a także dane telemetryczne zapisane samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="c2beb-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="c2beb-123">Na przykład można odfiltrować dane telemetryczne dotyczące żądań z robotów lub wywołania zależności powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c2beb-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="c2beb-124">Filtrowanie hello danych telemetrycznych wysłanych z hello SDK procesorów można pochylanie hello statystyk w portalu hello i stał się toofollow trudne powiązanych elementów.</span><span class="sxs-lookup"><span data-stu-id="c2beb-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="c2beb-125">Zamiast tego Rozważ użycie [próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c2beb-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="c2beb-126">Utwórz procesora telemetrii (C#)</span><span class="sxs-lookup"><span data-stu-id="c2beb-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="c2beb-127">Sprawdź, że hello zestaw SDK usługi Application Insights w projekcie jest w wersji 2.0.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c2beb-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="c2beb-128">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie Zarządzaj pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="c2beb-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="c2beb-129">W Menedżerze pakietów NuGet Sprawdź Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="c2beb-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="c2beb-130">toocreate filtru, zaimplementować ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="c2beb-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="c2beb-131">Jest to inny punkt rozszerzalności, takich jak moduł telemetrii, inicjatora telemetrii i kanału danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="c2beb-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="c2beb-132">Zwróć uwagę, że procesorów Telemetrii utworzyć łańcuch przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c2beb-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="c2beb-133">Można utworzyć wystąpienia procesora telemetrii, należy przekazać dalej procesor toohello łącze w łańcuchu hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="c2beb-134">Po upływie toohello proces metody punktu danych telemetrycznych jego działa i następnie wywołania hello dalej procesora Telemetrii w łańcuchu hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

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
1. <span data-ttu-id="c2beb-135">Wstaw ApplicationInsights.config to:</span><span class="sxs-lookup"><span data-stu-id="c2beb-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="c2beb-136">(Jest to hello tej samej sekcji, w którym zainicjować filtru próbkowania.)</span><span class="sxs-lookup"><span data-stu-id="c2beb-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="c2beb-137">Można przekazać wartości ciągu z pliku .config hello, zapewniając publicznej właściwości o nazwie w klasie.</span><span class="sxs-lookup"><span data-stu-id="c2beb-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="c2beb-138">Zajmie się nazwą typu hello toomatch oraz nazwy właściwości w klasie toohello pliku .config hello i nazwy właściwości w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="c2beb-139">Jeśli pliku .config hello odwołuje się do nieistniejącego typu lub właściwości, hello SDK może dyskretnie nie toosend żadnych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="c2beb-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="c2beb-140">**Alternatywnie** można zainicjować filtru hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c2beb-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="c2beb-141">W klasie inicjowania odpowiedniego — na przykład AppStart Global.asax.cs - Wstaw procesora do łańcucha hello:</span><span class="sxs-lookup"><span data-stu-id="c2beb-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="c2beb-142">TelemetryClients utworzone po tym punkcie będzie używać procesorów.</span><span class="sxs-lookup"><span data-stu-id="c2beb-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="c2beb-143">Przykładowe filtry</span><span class="sxs-lookup"><span data-stu-id="c2beb-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="c2beb-144">Syntetyczne żądań</span><span class="sxs-lookup"><span data-stu-id="c2beb-144">Synthetic requests</span></span>
<span data-ttu-id="c2beb-145">Filtrowanie testów robotów i sieci web.</span><span class="sxs-lookup"><span data-stu-id="c2beb-145">Filter out bots and web tests.</span></span> <span data-ttu-id="c2beb-146">Chociaż zapewnia Eksploratora metryk hello toofilter opcji limit syntetycznego źródła, tej opcji zmniejsza ruch przez filtrowanie ich na powitania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c2beb-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="c2beb-147">Uwierzytelnianie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="c2beb-147">Failed authentication</span></span>
<span data-ttu-id="c2beb-148">Filtrowanie żądań z odpowiedzi "401".</span><span class="sxs-lookup"><span data-stu-id="c2beb-148">Filter out requests with a "401" response.</span></span>

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

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="c2beb-149">Odfiltrować wywołania zależności fast zdalnego</span><span class="sxs-lookup"><span data-stu-id="c2beb-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="c2beb-150">Jeśli chcesz tylko wywołania toodiagnose, które są przetwarzane wolno, odfiltrować fast hello z nich.</span><span class="sxs-lookup"><span data-stu-id="c2beb-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="c2beb-151">Pochylanie przypadku statystyk hello, który zostanie wyświetlony w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="c2beb-152">wykres zależności Hello będzie wyglądać tak, jakby wywołania zależności hello są wszystkie błędy.</span><span class="sxs-lookup"><span data-stu-id="c2beb-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="c2beb-153">Diagnozowanie problemów z zależnością</span><span class="sxs-lookup"><span data-stu-id="c2beb-153">Diagnose dependency issues</span></span>
<span data-ttu-id="c2beb-154">[Ten blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) opisano problemy zależności toodiagnose projektu automatycznie wysyłając toodependencies regularne polecenia ping.</span><span class="sxs-lookup"><span data-stu-id="c2beb-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="c2beb-155">Dodaj właściwości: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="c2beb-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="c2beb-156">Dane telemetryczne inicjatory toodefine globalnych właściwości, które są wysyłane za pomocą wszystkie dane telemetryczne; i toooverride zachowanie hello telemetrii standardowe moduły.</span><span class="sxs-lookup"><span data-stu-id="c2beb-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="c2beb-157">Na przykład hello usługi Application Insights dla sieci Web pakietu zbiera dane telemetryczne dotyczące żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="c2beb-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="c2beb-158">Domyślnie flagi jako zakończony niepowodzeniem, wszystkie żądania z kodem odpowiedzi > = 400.</span><span class="sxs-lookup"><span data-stu-id="c2beb-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="c2beb-159">Ale jeśli chcesz tootreat 400 jako sukcesu, udostępniają inicjatora telemetrii, która ustawia właściwość Powodzenie hello.</span><span class="sxs-lookup"><span data-stu-id="c2beb-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="c2beb-160">Jeśli podasz inicjatora telemetrii, jest ona wywoływana przy każdym poszczególnych hello Track*() nosi nazwę metody.</span><span class="sxs-lookup"><span data-stu-id="c2beb-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="c2beb-161">Dotyczy to również metody wywołane przez hello telemetrii standardowe moduły.</span><span class="sxs-lookup"><span data-stu-id="c2beb-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="c2beb-162">Konwencja te moduły nie należy ustawiać dowolnej właściwości, która została już ustawiona przez inicjatora.</span><span class="sxs-lookup"><span data-stu-id="c2beb-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="c2beb-163">**Zdefiniuj z inicjatora**</span><span class="sxs-lookup"><span data-stu-id="c2beb-163">**Define your initializer**</span></span>

<span data-ttu-id="c2beb-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="c2beb-164">*C#*</span></span>

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

<span data-ttu-id="c2beb-165">**Ładowanie z inicjatora**</span><span class="sxs-lookup"><span data-stu-id="c2beb-165">**Load your initializer**</span></span>

<span data-ttu-id="c2beb-166">W ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="c2beb-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="c2beb-167">*Alternatywnie* można utworzyć wystąpienia inicjatora hello w kodzie, na przykład w pliku Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="c2beb-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="c2beb-168">Zobacz więcej w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c2beb-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="c2beb-169">Inicjatory telemetrii JavaScript</span><span class="sxs-lookup"><span data-stu-id="c2beb-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="c2beb-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c2beb-170">*JavaScript*</span></span>

<span data-ttu-id="c2beb-171">Wstaw inicjatora telemetrii natychmiast po kod inicjujący hello pochodzący z portalu hello:</span><span class="sxs-lookup"><span data-stu-id="c2beb-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

<span data-ttu-id="c2beb-172">Podsumowanie właściwości niestandardowych z systemem innym niż hello dostępnych na powitania telemetryItem, zobacz [Model danych eksportu Insights aplikacji](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="c2beb-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="c2beb-173">Możesz dodać dowolną liczbę inicjatory dowolnie.</span><span class="sxs-lookup"><span data-stu-id="c2beb-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="c2beb-174">ITelemetryProcessor i ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="c2beb-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="c2beb-175">Co to jest hello różnica między inicjatory telemetrii i danych telemetrycznych procesorów?</span><span class="sxs-lookup"><span data-stu-id="c2beb-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="c2beb-176">Istnieją pewne nakładania się w co można zrobić z nimi: zarówno mogą być używane tooadd tootelemetry właściwości.</span><span class="sxs-lookup"><span data-stu-id="c2beb-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="c2beb-177">TelemetryInitializers są zawsze uruchamiane przed TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="c2beb-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="c2beb-178">TelemetryProcessors pozwala zastąpić toocompletely lub odrzucić elementu telemetrii.</span><span class="sxs-lookup"><span data-stu-id="c2beb-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="c2beb-179">TelemetryProcessors nie Przetwarzaj telemetrii licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="c2beb-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="c2beb-180">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="c2beb-180">Reference docs</span></span>
* [<span data-ttu-id="c2beb-181">Przegląd interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c2beb-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="c2beb-182">Platformy ASP.NET — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="c2beb-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="c2beb-183">Kod zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="c2beb-183">SDK Code</span></span>
* [<span data-ttu-id="c2beb-184">Platformy ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="c2beb-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="c2beb-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="c2beb-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="c2beb-186">Zestaw SDK dla języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="c2beb-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="c2beb-187"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2beb-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="c2beb-188">Wyszukiwanie zdarzeń i dzienniki</span><span class="sxs-lookup"><span data-stu-id="c2beb-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="c2beb-189">Próbkowanie</span><span class="sxs-lookup"><span data-stu-id="c2beb-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="c2beb-190">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c2beb-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
