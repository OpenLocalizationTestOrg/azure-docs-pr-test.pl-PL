---
title: aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne zdarzenia | Dokumentacja firmy Microsoft
description: "Model danych usługi Insights aplikacji dla dane telemetryczne zdarzenia"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>Dane telemetryczne zdarzenia: model danych usługi Application Insights

Można utworzyć zdarzenia telemetrii elementów (w [usługi Application Insights](app-insights-overview.md)) toorepresent zdarzenie w aplikacji. Zwykle jest on interakcji z użytkownikiem, takich jak przycisk kliknij lub kolejność wyewidencjonowania. Można także zdarzeń cyklu życia aplikacji, takich jak inicjowanie lub konfiguracji aktualizacji. 

Semantycznie zdarzenia może lub nie może być skorelowane toorequests. Jednak jeśli prawidłowo używana, dane telemetryczne zdarzenia jest ważniejsze niż żądań i śladów. Zdarzenia reprezentują telemetrii biznesowych i powinna być tooseparate podmiotu, mniej aktywnego [próbkowania](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Nazwa

Nazwa zdarzenia. Grupowanie prawidłowego tooallow i przydatne metryki, należy ograniczyć aplikacji tak, aby generuje niewielką liczbę nazw oddzielne zdarzenie. Na przykład nie używaj osobnej nazwy dla każdego wystąpienia wygenerowane zdarzenia.

Maksymalna długość: 512 znaków

## <a name="custom-properties"></a>Właściwości niestandardowe

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Miar niestandardowych

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Następne kroki

- Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- [Pisanie niestandardowych zdarzeń telemetrii](app-insights-api-custom-events-metrics.md#trackevent)
- Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.
