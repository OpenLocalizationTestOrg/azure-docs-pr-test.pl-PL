<span data-ttu-id="20cac-101">Kolekcja niestandardowych miar.</span><span class="sxs-lookup"><span data-stu-id="20cac-101">Collection of custom measurements.</span></span> <span data-ttu-id="20cac-102">Użyj tej kolekcji do raportu o nazwie miary skojarzone z elementem telemetrii.</span><span class="sxs-lookup"><span data-stu-id="20cac-102">Use this collection to report named measurement associated with the telemetry item.</span></span> <span data-ttu-id="20cac-103">Typowe zastosowania to:</span><span class="sxs-lookup"><span data-stu-id="20cac-103">Typical use cases are:</span></span>
- <span data-ttu-id="20cac-104">Rozmiar ładunku dane telemetryczne zależności</span><span class="sxs-lookup"><span data-stu-id="20cac-104">the size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="20cac-105">Liczba elementów w kolejce przetworzone przez żądanie Telemetrii</span><span class="sxs-lookup"><span data-stu-id="20cac-105">the number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="20cac-106">czas klienta trwało wykonanie czynności w ukończenia kroku kreatora dane telemetryczne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="20cac-106">time that customer took to complete the step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="20cac-107">Można zbadać [niestandardowych miar](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) w analizy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="20cac-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="20cac-108">Pomiary niestandardowe są skojarzone z elementem telemetrii, do których należą.</span><span class="sxs-lookup"><span data-stu-id="20cac-108">Custom measurements are associated with the telemetry item they belong to.</span></span> <span data-ttu-id="20cac-109">Podlegają próbkowania z elementem telemetrii zawierający pomiarów.</span><span class="sxs-lookup"><span data-stu-id="20cac-109">They are subject to sampling with the telemetry item containing those measurements.</span></span> <span data-ttu-id="20cac-110">Aby śledzić miary niezależna od innych typów danych telemetrycznych wartości, należy użyć [dane telemetryczne metryki](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="20cac-110">To track a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="20cac-111">Maksymalna długość: 150</span><span class="sxs-lookup"><span data-stu-id="20cac-111">Max key length: 150</span></span>
