---
title: "aaaSmart wykrywania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Usługa Application Insights odbywa się szczegółowa analiza automatycznego dotyczących telemetrii aplikacji i ostrzega o potencjalnych problemach."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Inteligentne wykrywanie w usłudze Application Insights
 Inteligentne wykrywanie automatycznie ostrzega o potencjalnych problemów z wydajnością w aplikacji sieci web. Wykonuje aktywnego analizy aplikacji zbyt wysyła dane telemetryczne hello[usługi Application Insights](app-insights-overview.md). Jeśli istnieje nagły wzrost awariami lub nietypowe wzorce wydajności serwera lub klienta, zostanie wyświetlony alert. Ta funkcja wymaga żadnej konfiguracji. Działa on tak, jeśli aplikacja wyśle za mało danych telemetrii.

Alerty o wykryciu inteligentne mogą dostęp zarówno z hello wiadomości e-mail, które otrzymujesz i za pomocą bloku inteligentne wykrywanie hello.

## <a name="review-your-smart-detections"></a>Zapoznaj się z zagrożeń wykrywanych przez usługę inteligentnego
Może odnajdować wykryć na dwa sposoby:

* **Otrzymasz wiadomość e-mail** z usługi Application Insights. Oto typowy przykład:
  
    ![Alerty e-mail](./media/app-insights-proactive-diagnostics/03.png)
  
    Kliknij przycisk tooopen duży przycisk hello bardziej szczegółowo w portalu hello.
* **Kafelek inteligentne wykrywanie Hello** na Omówienie aplikacji bloku pokazuje liczbę ostatnich alertów. Kliknij przycisk toosee kafelka hello listę ostatnich alertów.

![Wyświetl ostatnie wykryć](./media/app-insights-proactive-diagnostics/04.png)

Wybierz alert toosee jego szczegóły.

## <a name="what-problems-are-detected"></a>Jakie problemy zostaną wykryte?
Istnieją trzy typy wykrywania:

* [Inteligentne wykrywania — błąd anomalii](app-insights-proactive-failure-diagnostics.md). Używamy uczenia maszynowego tooset hello oczekiwano liczba nieudanych żądań dla aplikacji, dopasowywanie obciążenia i innych czynników. Jeśli częstość niepowodzeń hello odbędzie się poza oczekiwanym koperty hello, możemy wysyłać alert.
* [Inteligentne wykrywania - anomalii wydajności](app-insights-proactive-performance-diagnostics.md). Otrzymywać powiadomień, jeśli odpowiedź czas trwania operacji lub zależności jest spowolnieniem porównaniu toohistorical linii bazowej lub nazywamy nietypowych wzorca w czasie odpowiedzi lub czas ładowania strony.   
* [Inteligentne wykrywania — problemy z usługą w chmurze Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Uzyskiwanie alertów, jeśli aplikacja jest hostowana w usług Azure Cloud Services i wystąpienia roli ma uruchamianiem, często odtwarzania lub awarie środowiska wykonawczego.

(łącza pomocy hello Każde powiadomienie przejście odpowiednich artykułów toohello.)

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Następne kroki
Te narzędzia diagnostyczne pomóc sprawdzić telemetrii hello z aplikacji:

* [Eksplorator metryk](app-insights-metrics-explorer.md)
* [Eksplorator wyszukiwania](app-insights-diagnostic-search.md)
* [Analiza - język zaawansowanych zapytań](app-insights-analytics-tour.md)

Wykrywanie inteligentne jest całkowicie automatyczne. A może chcesz tooset niektóre alerty więcej?

* [Ręcznie skonfigurowanej metryki alertów](app-insights-alerts.md)
* [Dostępność testy sieci web](app-insights-monitor-web-app-availability.md) 

