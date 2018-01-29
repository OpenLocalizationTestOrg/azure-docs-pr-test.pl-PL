---
title: "Konfigurowanie źródeł danych w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Źródła danych do definiowania danych czy zbiera analizy dzienników z agentów i inne połączenie źródeł.  W tym artykule opisano pojęcia jak analizy dzienników korzysta ze źródeł danych, zawiera szczegółowe informacje o sposobach ich konfigurowania i zawiera podsumowanie dostępnych źródeł danych."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2017
ms.author: bwren
ms.openlocfilehash: 4237df0934d6191b77ff82c86a66585e72191ac9
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2017
---
# <a name="data-sources-in-log-analytics"></a>Źródła danych w analizy dzienników
Analiza dzienników zbiera dane z połączonych źródeł i zapisuje go w obszarze roboczym analizy dzienników.  Dane są zbierane z każdej jest zdefiniowany przez źródła danych, które można skonfigurować.  Dane analizy dziennika są przechowywane jako zestaw rekordów.  Dla każdego źródła danych tworzy rekordy określonego typu z każdym typem o własny zestaw właściwości.

![Zbierania danych analizy dzienników](./media/log-analytics-data-sources/overview.png)

Źródła danych są inne niż [rozwiązań do zarządzania](log-analytics-add-solutions.md), które również zbieranie danych z połączonych źródeł i tworzenie rekordów w analizy dzienników.  Oprócz zbierania danych, rozwiązań zwykle zawierają dziennik wyszukiwania i widoki, które ułatwiają analizowanie operacji określonej aplikacji lub usługi.


## <a name="summary-of-data-sources"></a>Podsumowanie źródeł danych
W poniższej tabeli wymieniono źródeł danych, które są aktualnie dostępne w analizy dzienników.  Każdy ma łącze do oddzielnym artykule podanie szczegółów dla tego źródła danych.

| Źródło danych | Typ zdarzenia | Opis |
|:--- |:--- |:--- |
| [Niestandardowe dzienniki](log-analytics-data-sources-custom-logs.md) |\<Nazwa_dziennika\>_CL |Pliki tekstowe agentów systemu Windows lub Linux, zawierające informacje w dzienniku. |
| [Dzienniki zdarzeń systemu Windows](log-analytics-data-sources-windows-events.md) |Wydarzenie |Zdarzenia zebrane z komputerów z systemem Windows logowania zdarzeń. |
| [Liczniki wydajności systemu Windows](log-analytics-data-sources-performance-counters.md) |Wydajności |Liczniki wydajności są zbierane z komputerów z systemem Windows. |
| [Liczniki wydajności systemu Linux](log-analytics-data-sources-performance-counters.md) |Wydajności |Liczniki wydajności zebrane z komputerów z systemem Linux. |
| [Dzienniki usług IIS](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Internetowe usługi informacyjne dzienniki w formacie W3C. |
| [Dziennik systemu](log-analytics-data-sources-syslog.md) |Dziennik systemu |Zdarzenia dziennika systemowego na komputerach z systemem Windows lub Linux. |

## <a name="configuring-data-sources"></a>Konfigurowanie źródeł danych
Konfigurowanie źródeł danych z **danych** menu analizy dzienników **Zaawansowane ustawienia**.  Żadnej konfiguracji są dostarczane do wszystkich połączonych źródeł w obszarze roboczym.  Nie można obecnie wykluczyć wszystkich agentów z tej konfiguracji.

![Skonfiguruj zdarzenia systemu Windows](./media/log-analytics-data-sources/configure-events.png)

1. W portalu Azure wybierz **analizy dzienników** > obszar roboczy > **Zaawansowane ustawienia**.
2. Wybierz **danych**.
3. Kliknij źródło danych, które chcesz skonfigurować.
4. Skorzystaj z linku do dokumentacji dla każdego źródła danych w tabeli powyżej, aby uzyskać szczegółowe informacje na ich konfiguracji.


## <a name="data-collection"></a>Zbieranie danych
Konfiguracje źródła danych są dostarczane do agentów, które są podłączone bezpośrednio do analizy dzienników w ciągu kilku minut.  Określony dane są zbierane z agenta i dostarczane bezpośrednio do analizy dzienników w odstępach czasu określonych dla każdego źródła danych.  Zobacz dokumentację dla każdego źródła danych dla tych szczegółowych informacji.

Agenci programu System Center Operations Manager w podłączonej grupie zarządzania konfiguracji źródła danych są przetłumaczyć pakietów administracyjnych i dostarczonych w grupie zarządzania co 5 minut domyślnie.  Agent pobiera pakiet administracyjny jak każdy inny i zbiera określone dane. W zależności od źródła danych dane będą się, że albo wysłane do serwera zarządzania, który przesyła dane do analizy dzienników lub agent będzie wysyłać dane do analizy dzienników bez przechodzenia przez serwer zarządzania. Zapoznaj się [szczegóły kolekcji danych](log-analytics-add-solutions.md#data-collection-details) szczegółowe informacje.  Możesz przeczytać o szczegółach połączenie programu Operations Manager i analizy dzienników i modyfikowanie częstotliwości tej konfiguracji jest dostarczany w [skonfigurować integrację z programem System Center Operations Manager](log-analytics-om-agents.md).

Jeśli agent nie może nawiązać połączenia analizy dzienników lub Operations Manager, będzie zbierać dane, które będzie dostarczać, podczas nawiązywania połączenia.  Dane mogą zostać utracone, jeśli ilość danych osiągnie maksymalny rozmiar pamięci podręcznej klienta, lub jeśli agent nie jest w stanie nawiązać połączenia w ciągu 24 godzin.

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Wszystkie dane zebrane przez analizy dzienników znajduje się w obszarze roboczym jako rekordy.  Rejestruje zebrane przez różnych źródeł danych będą mieć własny zestaw właściwości i zostać zidentyfikowane na podstawie ich **typu** właściwości.  Dla każdego typu rekordu, zobacz dokumentację dla każdego źródła danych i rozwiązania, aby uzyskać szczegółowe informacje.

## <a name="next-steps"></a>Kolejne kroki
* Dowiedz się więcej o [rozwiązań](log-analytics-add-solutions.md) czy dodać funkcje do analizy dzienników i również zbieranie danych do obszaru roboczego.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania.  
* Skonfiguruj [alerty](log-analytics-alerts.md) do aktywnego powiadomienia o krytyczne dane zebrane ze źródeł danych i rozwiązań.
