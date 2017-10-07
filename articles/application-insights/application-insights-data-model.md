---
title: Model danych Telemetrii Insights aplikacji aaaAzure | Dokumentacja firmy Microsoft
description: "Omówienie modelu danych usługi Insights aplikacji"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Model danych telemetrii Insights aplikacji

[Azure Application Insights](app-insights-overview.md) wysyła dane telemetryczne z toohello aplikacji sieci web portalu Azure, dzięki czemu można analizować hello wydajności i użycia aplikacji. model danych telemetrycznych Hello jest standardowym, aby była możliwa toocreate platformy i monitorowania niezależny od języka. 

Dane zebrane przez usługę Application Insights modele tego wzorca wykonywania typowych aplikacji:

![Model Application Insights aplikacji](./media/application-insights-data-model/application-insights-data-model.png)

Hello są następujące typy telemetrii wykonywania hello toomonitor używanych aplikacji. Hello następujące trzy typy są zazwyczaj automatycznie gromadzone przez zestaw SDK usługi Application Insights hello z platforma aplikacji sieci web hello:

* [**Żądanie** ](application-insights-data-model-request-telemetry.md) -generowane toolog żądanie odebrane przez aplikację. Na przykład sieci web usługi Application Insights hello SDK automatycznie generuje element dane telemetryczne żądania dla każdego żądania HTTP, odbierająca aplikacja sieci web. 

    **Operacji** to hello wątków wykonywania, który przetwarza żądania. Możesz również [napisać kod](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor inne rodzaje operacji, takich jak "wznawiania" w sieci web zadania lub funkcji, które okresowo przetwarza dane.  Każda operacja wymaga identyfikatora. Ten identyfikator, które mogą być używane too[group]((application-insights-correlation.md) wszystkie dane telemetryczne generowane podczas przetwarzania żądania hello aplikacji. Każdej operacji albo zakończy się pomyślnie lub nie powiedzie się i został czasu.
* [**Wyjątek** ](application-insights-data-model-exception-telemetry.md) — zazwyczaj reprezentuje wyjątek, który powoduje, że toofail operacji.
* [**Zależności** ](application-insights-data-model-dependency-telemetry.md) -reprezentuje wywołanie usługi zewnętrzne tooan aplikacji lub magazynu, takich jak interfejsu API REST lub SQL. W programie ASP.NET tooSQL wywołania zależności są definiowane przez `System.Data`. Punkty końcowe tooHTTP połączeń są definiowane przez `System.Net`. 

Telemetria niestandardowa usługi Application Insights zawiera trzy typy dodatkowe dane:

* [Śledzenia](application-insights-data-model-trace-telemetry.md) — używany bezpośrednio lub za pośrednictwem karty tooimplement diagnostyki rejestrowanie przy użyciu Instrumentacji strukturę znanych tooyou, takich jak `Log4Net` lub `System.Diagnostics`.
* [Zdarzenie](application-insights-data-model-event-telemetry.md) — zwykle używanych toocapture interakcji z usługą tooanalyze wzorców użycia.
* [Metryka](application-insights-data-model-metric-telemetry.md) — używane tooreport okresowe pomiary skalarne.

Każdy element danych telemetrycznych można zdefiniować hello [informacje o kontekście](application-insights-data-model-context.md) identyfikator sesji aplikacji w wersji lub użytkownika. Kontekst jest zestaw pól jednoznacznie odblokowuje niektórych scenariuszy. Wersja aplikacji został poprawnie zainicjowany, usługi Application Insights może sprawdzić wzorce nowe zachowanie aplikacji skorelowane z ponownego wdrażania. Identyfikator sesji może być używane toocalculate hello awarii lub problem wpływ na użytkowników. Dla niektórych obliczanie liczności unikatowych wartości wartości identyfikatora sesji nie może zależności, śledzenie błąd lub wyjątek krytyczny zapewnia dobrą znajomość wpływ.

Usługi Application Insights modelu telemetrii definiuje sposób zbyt[skorelowania](application-insights-correlation.md) telemetrii toohello operacji, który jest częścią. Na przykład żądanie może wywoływać bazy danych SQL i zarejestrowane informacje diagnostyczne. Można ustawić hello korelacji kontekst dla tych elementów dane telemetryczne, które powiązanie jej tyłu toohello dane telemetryczne żądania.

## <a name="schema-improvements"></a>Ulepszenia schematu

Model danych usługi Insights aplikacji jest proste i podstawowa, ale toomodel sposób dane telemetryczne aplikacji. Firma Microsoft dążyć tookeep hello modelu toosupport proste i obsługiwane podstawowe scenariusze i pozwolić tooextend hello schematu dla zaawansowanych użytkowników.

tooreport danych model lub schematu problemy i sugestie używają GitHub [ApplicationInsights głównej](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repozytorium.

## <a name="next-steps"></a>Następne kroki

- [Telemetria niestandardowa zapisu](app-insights-api-custom-events-metrics.md)
- Dowiedz się, jak za[rozszerzanie i filtrować dane telemetryczne](app-insights-api-filtering-sampling.md).
- Użyj [próbkowania](app-insights-sampling.md) toominimize ilość danych telemetrycznych oparte na modelu danych.
- Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.
