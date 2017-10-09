<span data-ttu-id="f0d4a-101">Kolekcja niestandardowych miar.</span><span class="sxs-lookup"><span data-stu-id="f0d4a-101">Collection of custom measurements.</span></span> <span data-ttu-id="f0d4a-102">Użyj tego tooreport kolekcji o nazwie miary skojarzone z elementem telemetrii hello.</span><span class="sxs-lookup"><span data-stu-id="f0d4a-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="f0d4a-103">Typowe zastosowania to:</span><span class="sxs-lookup"><span data-stu-id="f0d4a-103">Typical use cases are:</span></span>
- <span data-ttu-id="f0d4a-104">Witaj rozmiar ładunku dane telemetryczne zależności</span><span class="sxs-lookup"><span data-stu-id="f0d4a-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="f0d4a-105">Hello liczba elementów w kolejce przetworzone przez żądanie Telemetrii</span><span class="sxs-lookup"><span data-stu-id="f0d4a-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="f0d4a-106">czas klienta trwało toocomplete hello krok w ukończenia kroku kreatora dane telemetryczne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f0d4a-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="f0d4a-107">Można zbadać [niestandardowych miar](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) w analizy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f0d4a-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="f0d4a-108">Pomiary niestandardowe są skojarzone z elementem telemetrii hello, których należą.</span><span class="sxs-lookup"><span data-stu-id="f0d4a-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="f0d4a-109">Są one podmiotu toosampling z elementem telemetrii hello zawierający pomiarów.</span><span class="sxs-lookup"><span data-stu-id="f0d4a-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="f0d4a-110">tootrack miary niezależna od innych typów danych telemetrii, użyj wartości [dane telemetryczne metryki](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f0d4a-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="f0d4a-111">Maksymalna długość: 150</span><span class="sxs-lookup"><span data-stu-id="f0d4a-111">Max key length: 150</span></span>
