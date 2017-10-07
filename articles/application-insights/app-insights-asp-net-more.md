---
title: "aaaGet więcej poza Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Po pierwsze kroki z usługą Application Insights, poniżej przedstawiono podsumowanie funkcji hello, które można eksplorować."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>Więcej danych telemetrycznych z usługi Application Insights
Po [dodać usługi Application Insights tooyour ASP.NET kodu](app-insights-asp-net.md), istnieje kilka sposobów tooget nawet więcej telemetrii. 

| Akcja | Efekty|
|---|---|
|(Serwery IIS) [Zainstaluj Monitor stanu](http://go.microsoft.com/fwlink/?LinkId=506648) na każdym komputerze z serwerem.<br/>(Aplikacje sieci web platformy azure) W Panelu sterowania Azure hello hello aplikacji sieci web Otwórz blok usługi Application Insights hello.| [**Liczniki wydajności**](app-insights-performance-counters.md)<br/>[**Wyjątki** ](app-insights-asp-net-exceptions.md) — szczegółowe dane śledzenia stosu<br/>[**Zależności**](app-insights-asp-net-dependencies.md)|
|[Dodawanie stron sieci web tooyour fragment kodu JavaScript hello](app-insights-javascript.md)|[Strona wydajności](app-insights-web-track-usage.md), wyjątki przeglądarki, wydajność AJAX. Telemetria niestandardowa po stronie klienta.|
|[Tworzenie testów sieci web dostępności](app-insights-monitor-web-app-availability.md)|Alerty, jeśli witryna jest niedostępny|
|[Upewnij się, buildinfo.config](https://msdn.microsoft.com/library/dn449058.aspx) jest generowany przez program MSBuild|[Tworzenie wykresów metryki annotationsin](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/)
|[Pisanie niestandardowych zdarzeń i metryk](app-insights-api-custom-events-metrics.md)|Liczba zdarzeń biznesowych i metryki, śledzić szczegółowe dane użycia i inne.|
|[Profil witryny na żywo](https://aka.ms/AIProfilerPreview)|Czasy szczegółowe funkcji z aplikacji sieci web na żywo|






