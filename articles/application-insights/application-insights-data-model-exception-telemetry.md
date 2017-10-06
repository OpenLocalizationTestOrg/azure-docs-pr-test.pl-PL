---
title: "aaaAzure aplikacji modelu danych Telemetrii Insights - dane telemetryczne dotyczące wyjątków | Dokumentacja firmy Microsoft"
description: "Model danych usługi Insights aplikacji dla dane telemetryczne dotyczące wyjątków"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a>Dane telemetryczne wyjątku: model danych usługi Application Insights

W [usługi Application Insights](app-insights-overview.md), obsługiwany lub nieobsługiwany wyjątek, który wystąpił podczas wykonywania aplikacji hello monitorowane reprezentuje wystąpienie wyjątku.

## <a name="problem-id"></a>Identyfikator problemu

Identyfikator której hello Wystąpił wyjątek w kodzie. Używane do grupowania wyjątków. Zwykle połączenie typ wyjątku i funkcję hello stosu wywołań.

Maksymalna długość: 1024 znaki

## <a name="severity-level"></a>Poziom ważności

Poziom ważności śledzenia. Wartość może być `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Szczegóły wyjątku

(toobe rozszerzony)

## <a name="custom-properties"></a>Właściwości niestandardowe

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Miar niestandardowych

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Następne kroki

- Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.
- Dowiedz się, jak za[diagnozowanie wyjątków w aplikacjach sieci web za pomocą usługi Application Insights](app-insights-asp-net-exceptions.md).
- Zapoznaj się z [platform](app-insights-platforms.md) obsługiwane przez usługę Application Insights.
