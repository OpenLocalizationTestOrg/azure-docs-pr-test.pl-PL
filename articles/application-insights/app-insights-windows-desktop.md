---
title: "aaaMonitoring użycia i wydajności dla aplikacji klasycznych systemu Windows"
description: "Analizowanie użycia i wydajności klasycznej aplikacji systemu Windows za pomocą usług HockeyApp i Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="3aeab-103">Monitorowanie użycia i wydajności klasycznych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3aeab-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="3aeab-104">Usługi [Azure Application Insights](app-insights-overview.md) i [HockeyApp](https://hockeyapp.net) umożliwiają monitorowanie wdrożonej aplikacji pod kątem użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="3aeab-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3aeab-105">Firma Microsoft zaleca [HockeyApp](https://hockeyapp.net) toodistribute i monitorowanie aplikacji pulpitu i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3aeab-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="3aeab-106">Za pomocą usługi HockeyApp można zarządzać dystrybucją, testowaniem na żywo i opiniami użytkowników oraz monitorować raporty użycia i awarii.</span><span class="sxs-lookup"><span data-stu-id="3aeab-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="3aeab-107">Możesz również [eksportować telemetrię i tworzyć zapytania do niej za pomocą funkcji analizy](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="3aeab-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="3aeab-108">Mimo że telemetrii można wysyłać tooApplication Insights z aplikacją, jest głównie przydatna do celów debugowania i eksperymentalne.</span><span class="sxs-lookup"><span data-stu-id="3aeab-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="3aeab-109">toosend telemetrii tooApplication szczegółowych informacji z aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3aeab-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="3aeab-110">W hello [portalu Azure](https://portal.azure.com), [utworzyć zasobu usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3aeab-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="3aeab-111">Jako typ aplikacji wybierz ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3aeab-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="3aeab-112">Należy wykonać kopię hello klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="3aeab-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="3aeab-113">Znajdź klucz hello w hello rozwijanej Essentials hello nowy zasób, który właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="3aeab-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="3aeab-114">W programie Visual Studio Edytuj hello pakietów NuGet projektu aplikacji, a następnie dodaj Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="3aeab-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="3aeab-115">(Lub wybierz Microsoft.ApplicationInsights, jeśli chcesz hello API systemu od zera, bez modułów kolekcji standardowych telemetrii hello.)</span><span class="sxs-lookup"><span data-stu-id="3aeab-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="3aeab-116">Ustaw hello klucza Instrumentacji w kodzie:</span><span class="sxs-lookup"><span data-stu-id="3aeab-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="3aeab-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *Twój klucz* `";`</span><span class="sxs-lookup"><span data-stu-id="3aeab-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="3aeab-118">lub ApplicationInsights.config (jeśli został zainstalowany jeden z pakietów standardowe telemetrii hello):</span><span class="sxs-lookup"><span data-stu-id="3aeab-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="3aeab-119">`<InstrumentationKey>`*Twój klucz*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="3aeab-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="3aeab-120">Jeśli używasz ApplicationInsights.config, upewnij się, jego właściwości w Eksploratorze rozwiązań są ustawiane za**Akcja kompilacji = zawartość, tooOutput kopiowania katalogu = kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="3aeab-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="3aeab-121">[Za pomocą interfejsu API hello](app-insights-api-custom-events-metrics.md) toosend telemetrii.</span><span class="sxs-lookup"><span data-stu-id="3aeab-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="3aeab-122">Uruchom aplikację i wyświetlić dane telemetryczne hello w zasobie hello, utworzony w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3aeab-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="3aeab-123"><a name="telemetry"></a>Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="3aeab-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a><span data-ttu-id="3aeab-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3aeab-124">Next steps</span></span>
* [<span data-ttu-id="3aeab-125">Tworzenie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="3aeab-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="3aeab-126">Wyszukiwanie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="3aeab-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="3aeab-127">Eksplorowanie metryk</span><span class="sxs-lookup"><span data-stu-id="3aeab-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="3aeab-128">Pisanie zapytań analitycznych</span><span class="sxs-lookup"><span data-stu-id="3aeab-128">Write Analytics queries</span></span>](app-insights-analytics.md)

