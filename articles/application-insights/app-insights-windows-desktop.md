---
title: "Monitorowanie użycia i wydajności klasycznych aplikacji systemu Windows"
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
ms.openlocfilehash: 9d7e2a390adf10cbf5d88dd0084ce09136987309
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="bead9-103">Monitorowanie użycia i wydajności klasycznych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bead9-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="bead9-104">Usługi [Azure Application Insights](app-insights-overview.md) i [HockeyApp](https://hockeyapp.net) umożliwiają monitorowanie wdrożonej aplikacji pod kątem użycia i wydajności.</span><span class="sxs-lookup"><span data-stu-id="bead9-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bead9-105">Zalecamy użycie usługi [HockeyApp](https://hockeyapp.net) do dystrybucji i monitorowania aplikacji klasycznych i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bead9-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="bead9-106">Za pomocą usługi HockeyApp można zarządzać dystrybucją, testowaniem na żywo i opiniami użytkowników oraz monitorować raporty użycia i awarii.</span><span class="sxs-lookup"><span data-stu-id="bead9-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="bead9-107">Możesz również [eksportować telemetrię i tworzyć zapytania do niej za pomocą funkcji analizy](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="bead9-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="bead9-108">Chociaż telemetria może być wysyłana do usługi Application Insights z klasycznej aplikacji, jest to głównie przydatne podczas debugowania i do celów doświadczalnych.</span><span class="sxs-lookup"><span data-stu-id="bead9-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="bead9-109">Aby wysłać dane telemetryczne do usługi Application Insights z aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bead9-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="bead9-110">W witrynie [Azure Portal](https://portal.azure.com) [utwórz zasób usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bead9-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="bead9-111">Jako typ aplikacji wybierz ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bead9-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="bead9-112">Wykonaj kopię klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="bead9-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="bead9-113">Klucz można znaleźć na liście rozwijanej Podstawy dla nowego zasobu, który właśnie został utworzony.</span><span class="sxs-lookup"><span data-stu-id="bead9-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="bead9-114">W programie Visual Studio edytuj pakiety NuGet projektu aplikacji, a następnie dodaj interfejs Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="bead9-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="bead9-115">(Lub wybierz interfejs Microsoft.ApplicationInsights, jeśli potrzebny jest tylko podstawowy interfejs API bez standardowych modułów gromadzenia telemetrii).</span><span class="sxs-lookup"><span data-stu-id="bead9-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="bead9-116">Ustaw klucz instrumentacji w kodzie:</span><span class="sxs-lookup"><span data-stu-id="bead9-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="bead9-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *Twój klucz* `";`</span><span class="sxs-lookup"><span data-stu-id="bead9-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="bead9-118">albo w pliku ApplicationInsights.config (jeśli został zainstalowany jeden ze standardowych pakietów telemetrii):</span><span class="sxs-lookup"><span data-stu-id="bead9-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="bead9-119">`<InstrumentationKey>`*Twój klucz*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="bead9-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="bead9-120">Jeśli używasz pliku ApplicationInsights.config, upewnij się, że jego właściwości w Eksploratorze rozwiązań zostały ustawione na **Akcja kompilacji = Zawartość, Kopiuj do katalogu wyjściowego = Kopiuj**.</span><span class="sxs-lookup"><span data-stu-id="bead9-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="bead9-121">[Użyj interfejsu API](app-insights-api-custom-events-metrics.md), aby wysłać telemetrię.</span><span class="sxs-lookup"><span data-stu-id="bead9-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="bead9-122">Uruchom aplikację i wyświetl dane telemetryczne w zasobie utworzonym w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bead9-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <span data-ttu-id="bead9-123"><a name="telemetry"></a>Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="bead9-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
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

## <a name="next-steps"></a><span data-ttu-id="bead9-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bead9-124">Next steps</span></span>
* [<span data-ttu-id="bead9-125">Tworzenie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="bead9-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="bead9-126">Wyszukiwanie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="bead9-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="bead9-127">Eksplorowanie metryk</span><span class="sxs-lookup"><span data-stu-id="bead9-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="bead9-128">Pisanie zapytań analitycznych</span><span class="sxs-lookup"><span data-stu-id="bead9-128">Write Analytics queries</span></span>](app-insights-analytics.md)

