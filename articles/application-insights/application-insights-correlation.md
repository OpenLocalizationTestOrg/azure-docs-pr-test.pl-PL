---
title: Application Insights Telemetrii korelacji aaaAzure | Dokumentacja firmy Microsoft
description: Application Insights telemetrii korelacji
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
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Korelacji telemetrii w usłudze Application Insights

Witaj świecie micro usług każda operacja logiczna wymaga pracować w różnych składników usługi hello. Każdy z tych składników mogą być oddzielnie monitorowane przez [usługi Application Insights](app-insights-overview.md). Składnik aplikacji sieci web Hello komunikuje się z poświadczeniami użytkownika toovalidate składnik dostawcy uwierzytelniania i danymi hello interfejsu API składnika tooget dla wizualizacji. Hello składnika interfejsu API z kolei może zapytania na danych z innych usług i użyj składników dostawcy pamięci podręcznej i powiadom hello składnika rozliczeń o tego wywołania. Aplikacji Insights obsługuje rozproszonej telemetrii korelacji. Pozwala ona toodetect, który składnik jest odpowiedzialny za błędy lub spadek wydajności.

W tym artykule opisano model danych hello używane przez usługi Application Insights toocorrelate telemetrii wysyłane przez kilka składników. Obejmuje ona hello kontekstu propagacji technik i protokołów. Obejmuje ona również implementacja hello hello korelacji pojęcia dotyczące różnych języków i platform.

## <a name="telemetry-correlation-data-model"></a>Model danych telemetrycznych korelacji

Definiuje usługi Application Insights [modelu danych](application-insights-data-model.md) dla rozproszonych telemetrii korelacji. telemetrii tooassociate operacja logiczna hello, każdy element telemetrii ma pole kontekstu o nazwie `operation_Id`. Ten identyfikator jest współużytkowany przez każdy element dane telemetryczne w śladzie hello rozproszonych. Dlatego nawet w przypadku utraty danych telemetrycznych z jedną warstwę nadal można skojarzyć dane telemetryczne zgłoszone przez inne składniki.

Operacja logiczna rozproszonej zazwyczaj składa się z zestaw operacji mniejsze - żądań przetwarzanych przez jeden ze składników hello. Te operacje są definiowane przez [żądanie telemetrii](application-insights-data-model-request-telemetry.md). Co dane telemetryczne żądania ma własną `id` identyfikującym jednoznacznie globalnie. Wszystkie dane telemetryczne - śladów, wyjątków, skojarzony z tym żądaniem itp. należy określić hello `operation_parentId` toohello wartości żądania hello `id`.

Każdej operacji wychodzących, takich jak składnika tooanother wywołanie http reprezentowany przez [dane telemetryczne zależności](application-insights-data-model-dependency-telemetry.md). Dane telemetryczne zależności definiuje również własną `id` jest globalnie unikatowa. Dane telemetryczne żądania, inicjowane przez wywołanie zależności, używa go jako `operation_parentId`.

Można utworzyć widoku hello przy użyciu operacji logicznych rozproszonej `operation_Id`, `operation_parentId`, i `request.id` z `dependency.id`. Te pola również definiować hello przyczynowości kolejność wywołań telemetrii.

W środowisku usług micro śladów ze składników przejść toohello różnych miejsc. Każda część może mieć własną klucza Instrumentacji w usłudze Application Insights. tooget telemetrii dla operacji logicznych hello, należy tooquery danych z każdego magazynu. W przypadku dużych liczbę miejsc o tym, gdzie należy toohave wskazówkę toolook dalej.

Model danych definiuje dwie usługi Application Insights pola toosolve ten problem: `request.source` i `dependency.target`. pierwsze pole Hello identyfikuje hello składnika, który zainicjował żądanie zależności hello i hello identyfikuje drugiego składnika, który zwrócił odpowiedź hello wywołania zależności hello.


## <a name="example"></a>Przykład

Spójrzmy na przykład cen GIEŁDOWYCH aplikacji przedstawiający hello bieżącego rynku ceny akcji przy użyciu zewnętrznego interfejsu API hello wywołuje interfejs API zasobów. CENY zasobów aplikacji Hello jest strona `Stock page` otworzyć za pomocą przeglądarki sieci web powitania klienta `GET /Home/Stock`. zapytania aplikacji Hello hello API zasobów przy użyciu wywołania HTTP `GET /api/stock/value`.

Można analizować wynikowy telemetrii kwerendy:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

Hello wynik widoku uwagi, że wszystkie elementy telemetrii udostępniać głównego hello `operation_Id`. Gdy wywołanie ajax wprowadzone na stronie powitania — nowy unikatowy identyfikator `qJSXU` jest przypisany toohello dane telemetryczne zależności i widok strony jego identyfikator jest używany jako `operation_ParentId`. Z kolei żądanie serwera używa identyfikatora w technologii ajax jako `operation_ParentId`itp.

| ItemType   | name                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| Widok strony   | Strona standardowych                |              | STYz               | STYz         |
| zależności | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| Żądanie    | Strona główna GET/Stock            | KqKwlrSt9PA = | qJSXU              | STYz         |
| zależności | Pobierz /api/stock/value      | bBrf2L7mm2g = | KqKwlrSt9PA =       | STYz         |

Teraz po hello wywołania `GET /api/stock/value` wprowadzone tooan zewnętrzna usługa ma tożsamość hello tooknow tego serwera. Można ustawić `dependency.target` odpowiednio do pola. Gdy hello zewnętrzna usługa nie obsługuje monitorowania - `target` jest ustawiona na nazwę hosta toohello hello usługi, takiej jak `stock-prices-api.com`. Jednak jeśli czy usługa identyfikuje zwracając wstępnie zdefiniowanej nagłówka HTTP - `target` zawiera tożsamość usługi hello umożliwiający śledzenia toobuild rozproszonego usługi Application Insights, badając dane telemetryczne z tej usługi. 

## <a name="correlation-headers"></a>Nagłówki korelacji

Pracujemy nad RFC propozycję hello [korelacji protokołu HTTP](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Propozycja ta definiuje dwa nagłówki:

- `Request-Id`globalnie unikatowy identyfikator hello wywołania hello przenoszenia
- `Correlation-Context`-przenoszenia hello nazwa wartość pary kolekcję właściwości śledzenia hello rozproszonych

Standardowa Hello definiuje również dwa schematy `Request-Id` generowania - płaskiego i hierarchicznego. Ze schematem płaskiej hello, jest dobrze znanym `Id` klucz zdefiniowany dla hello `Correlation-Context` kolekcji.

Usługa Application Insights definiuje hello [rozszerzenia](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) dla korelacji hello protokołu HTTP. Używa `Request-Context` nazwa pary wartości toopropagate hello zbiór właściwości używanych przez hello natychmiastowego wywołujący lub wywoływany. Zestaw SDK usługi Application Insights używa tego nagłówka tooset `dependency.target` i `request.source` pól.

## <a name="open-tracing-and-application-insights"></a>Otwórz śledzenie i usługi Application Insights

[Otwórz śledzenie](http://opentracing.io/) i wygląda modeli danych usługi Application Insights 

- `request`, `pageView` mapy zbyt**zakres** z`span.kind = server`
- `dependency`mapuje zbyt**zakres** z`span.kind = client`
- `id`z `request` i `dependency` mapy zbyt**Span.Id**
- `operation_Id`mapuje zbyt**TraceId**
- `operation_ParentId`mapuje zbyt**odwołania** typu`ChileOf`

Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.

Zobacz [specyfikacji](https://github.com/opentracing/specification/blob/master/specification.md) i [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md) definicji śledzenia Otwórz pojęcia.


## <a name="telemetry-correlation-in-net"></a>Korelacja telemetrii w .NET

Wraz z upływem czasu .NET zdefiniowanych wiele sposobów toocorrelate telemetrii i informacji diagnostycznych dzienników. Brak `System.Diagnostics.CorrelationManager` stosowanie tootrack [LogicalOperationStack i ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`i Windows ETW zdefiniować metody hello [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger`używa [zakresy dziennika](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). Usługi WCF i Http podczas transmisji się "bieżący" propagacji kontekstu.

Jednak tych metod nie umożliwia automatycznego śledzenia rozproszonych. `DiagnosticsSource`toosupport sposób odbywa się automatycznie cross korelacji maszyny. Biblioteki .NET obsługuje źródła diagnostyki i Zezwalaj na automatyczne maszyny krzyżowego propagacji hello korelacji kontekstu za pomocą transportu hello, takich jak http.

Witaj [przewodnik tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) w źródle diagnostyki opisano podstawy hello śledzenie działań. 

Wyodrębniania nagłówków Http obsługuje podstawowe ASP.NET 2.0 i uruchamianie hello nowe działanie. 

`System.Net.HttpClient`wersję początkową `<fill in>` obsługuje automatyczne uruchomienie korelacji hello nagłówków Http i śledzenia hello wywołanie http jako działania.

Moduł Http jest nowy [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) dla hello ASP.NET Classic. Ten moduł stanowi wdrożenie przy użyciu DiagnosticsSource korelacji telemetrii. Rozpoczyna działania od nagłówków żądań przychodzących. Są również powiązane dane telemetryczne z różnych etapów hello przetwarzania żądania. Nawet w przypadku przypadków powitania po uruchomieniu każdego etapu przetwarzania usług IIS w wątkach różnych zarządzanie.

Wersję początkową aplikacji zestawu SDK Insights `2.4.0-beta1` używa telemetrii toocollect DiagnosticsSource i działania i powiązać ją z hello bieżącego działania. 

## <a name="next-steps"></a>Następne kroki

- [Telemetria niestandardowa zapisu](app-insights-api-custom-events-metrics.md)
- Dołączyć wszystkie składniki usługi micro na usługi Application Insights. Zapoznaj się z [obsługiwanych platform](app-insights-platforms.md).
- Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- Dowiedz się, jak za[rozszerzanie i filtrować dane telemetryczne](app-insights-api-filtering-sampling.md).
