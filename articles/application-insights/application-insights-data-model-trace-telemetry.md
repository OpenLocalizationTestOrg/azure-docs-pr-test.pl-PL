---
title: "aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne śledzenia | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne śledzenia"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a>Dane telemetryczne śledzenia: model danych usługi Application Insights

Dane telemetryczne śledzenia (w [usługi Application Insights](app-insights-overview.md)) reprezentuje `printf` styl instrukcji śledzenia, które są przeszukiwane tekstu. `Log4Net`, `NLog`, i inne wpisy w pliku tekstowym dziennika są przetłumaczyć wystąpień tego typu. Witaj śledzenia nie ma pomiarów jako rozszerzalności.

## <a name="message"></a>Komunikat

Komunikat śledzenia.

Maksymalna długość: 32768 znaków

## <a name="severity-level"></a>Poziom ważności

Poziom ważności śledzenia. Wartość może być `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="custom-properties"></a>Właściwości niestandardowe

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Następne kroki

- [Eksploruj dzienniki śledzenia platformy .NET w usłudze Application Insights](app-insights-asp-net-trace-logs.md).
- [Eksploruj dzienniki śledzenia w usłudze Application Insights Java](app-insights-java-trace-logs.md).
- Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- [Zapisać dane telemetryczne śledzenia niestandardowych](app-insights-api-custom-events-metrics.md#tracktrace)
- Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.
