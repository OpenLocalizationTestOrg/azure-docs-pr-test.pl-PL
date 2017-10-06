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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Monitorowanie użycia i wydajności klasycznych aplikacji systemu Windows


Usługi [Azure Application Insights](app-insights-overview.md) i [HockeyApp](https://hockeyapp.net) umożliwiają monitorowanie wdrożonej aplikacji pod kątem użycia i wydajności.

> [!IMPORTANT]
> Firma Microsoft zaleca [HockeyApp](https://hockeyapp.net) toodistribute i monitorowanie aplikacji pulpitu i urządzenia. Za pomocą usługi HockeyApp można zarządzać dystrybucją, testowaniem na żywo i opiniami użytkowników oraz monitorować raporty użycia i awarii. Możesz również [eksportować telemetrię i tworzyć zapytania do niej za pomocą funkcji analizy](app-insights-hockeyapp-bridge-app.md).
> 
> Mimo że telemetrii można wysyłać tooApplication Insights z aplikacją, jest głównie przydatna do celów debugowania i eksperymentalne.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend telemetrii tooApplication szczegółowych informacji z aplikacji systemu Windows
1. W hello [portalu Azure](https://portal.azure.com), [utworzyć zasobu usługi Application Insights](app-insights-create-new-resource.md). Jako typ aplikacji wybierz ASP.NET.
2. Należy wykonać kopię hello klucza instrumentacji. Znajdź klucz hello w hello rozwijanej Essentials hello nowy zasób, który właśnie utworzony. 
3. W programie Visual Studio Edytuj hello pakietów NuGet projektu aplikacji, a następnie dodaj Microsoft.ApplicationInsights.WindowsServer. (Lub wybierz Microsoft.ApplicationInsights, jeśli chcesz hello API systemu od zera, bez modułów kolekcji standardowych telemetrii hello.)
4. Ustaw hello klucza Instrumentacji w kodzie:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *Twój klucz* `";` 
   
    lub ApplicationInsights.config (jeśli został zainstalowany jeden z pakietów standardowe telemetrii hello):
   
    `<InstrumentationKey>`*Twój klucz*`</InstrumentationKey>` 
   
    Jeśli używasz ApplicationInsights.config, upewnij się, jego właściwości w Eksploratorze rozwiązań są ustawiane za**Akcja kompilacji = zawartość, tooOutput kopiowania katalogu = kopiowania**.
5. [Za pomocą interfejsu API hello](app-insights-api-custom-events-metrics.md) toosend telemetrii.
6. Uruchom aplikację i wyświetlić dane telemetryczne hello w zasobie hello, utworzony w hello portalu Azure.

## <a name="telemetry"></a>Przykładowy kod
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

## <a name="next-steps"></a>Następne kroki
* [Tworzenie pulpitu nawigacyjnego](app-insights-dashboards.md)
* [Wyszukiwanie diagnostyczne](app-insights-diagnostic-search.md)
* [Eksplorowanie metryk](app-insights-metrics-explorer.md)
* [Pisanie zapytań analitycznych](app-insights-analytics.md)

