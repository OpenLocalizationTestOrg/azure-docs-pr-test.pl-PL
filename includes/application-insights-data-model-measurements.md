Kolekcja niestandardowych miar. Użyj tego tooreport kolekcji o nazwie miary skojarzone z elementem telemetrii hello. Typowe zastosowania to:
- Witaj rozmiar ładunku dane telemetryczne zależności
- Hello liczba elementów w kolejce przetworzone przez żądanie Telemetrii
- czas klienta trwało toocomplete hello krok w ukończenia kroku kreatora dane telemetryczne zdarzenia.

Można zbadać [niestandardowych miar](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) w analizy aplikacji:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Pomiary niestandardowe są skojarzone z elementem telemetrii hello, których należą. Są one podmiotu toosampling z elementem telemetrii hello zawierający pomiarów. tootrack miary niezależna od innych typów danych telemetrii, użyj wartości [dane telemetryczne metryki](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Maksymalna długość: 150
