---
title: "aaaHow tooscale środowiska Azure czas serii Insights | Dokumentacja firmy Microsoft"
description: "W tym samouczku przedstawiono sposób tooscale środowiska Azure czas serii Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Jak tooscale środowisku Insights serii czasu

W tym samouczku przedstawiono sposób tooscale środowisku Insights serii czasu.

> [!NOTE]
> Skalowania w górę różnych typów jednostki sku nie jest dozwolone. Nie można przekonwertować w środowisku zawierającym S1 Sku środowisku S2.

## <a name="s1-sku-ingress-rates-and-capacities"></a>Szybkość wejściowych S1 SKU i pojemności

| S1 Pojemność jednostki SKU | Szybkość transferu | Maksymalna pojemność magazynu
| --- | --- | --- |
| 1 | 1 GB (1 mln zdarzeń) | 30 GB (30 milionów zdarzeń) na miesiąc |
| 10 | 10 GB (10 milionów zdarzeń) | 300 GB (300 milionów zdarzeń) na miesiąc |

## <a name="s2-sku-ingress-rates-and-capacities"></a>Szybkość wejściowych s2 jednostki SKU i pojemności

| S2 Pojemność jednostki SKU | Szybkość transferu | Maksymalna pojemność magazynu
| --- | --- | --- |
| 1 | 10 GB (10 milionów zdarzeń) | 300 GB (300 milionów zdarzeń) na miesiąc |
| 10 | 100 GB (100 milionów zdarzeń) | 3 TB (zdarzenia miliard 3) na miesiąc |

Możliwości skalowania liniowo, więc sku S1, o pojemności 2 obsługuje 2 GB (2 milionów) zdarzeń według dnia służąca szybkość i 60 GB (60 miliona zdarzeń) w miesiącu.

## <a name="changing-hello-capacity-of-your-environment"></a>Zmiana pojemności hello środowiska

1. W hello portalu Azure, wybierz hello środowiska której pojemność chcesz toochange.
1. W obszarze Ustawienia kliknij przycisk Konfiguruj.
1. Użyj systemu hello pojemności suwaka tooselect hello wydajności spełniający wymagania hello ceny wejściowych i pojemności magazynu.

## <a name="next-steps"></a>Następne kroki

* Sprawdź, czy hello nowego miejsca jest wystarczająca tooprevent ograniczania. Aby uzyskać więcej informacji, zobacz hello *środowisku może być pobieranie ograniczany* sekcji [tutaj](time-series-insights-diagnose-and-solve-problems.md).
