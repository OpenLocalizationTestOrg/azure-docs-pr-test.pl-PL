---
title: "aaaCollect i analizować dzienniki zdarzeń systemu Windows w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Dzienniki zdarzeń systemu Windows są jednym z hello najczęściej źródeł danych używanych przez analizy dzienników.  W tym artykule opisano, jak tooconfigure zbierania dzienników zdarzeń systemu Windows i szczegóły rekordów hello tworzą hello OMS repozytorium."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Źródła danych dziennika zdarzeń systemu Windows w analizy dzienników
Dzienniki zdarzeń systemu Windows są jednym z najbardziej typowych hello [źródeł danych](log-analytics-data-sources.md) do zbierania danych za pomocą agentów systemu Windows, ponieważ wiele aplikacji zapisu dziennika zdarzeń systemu Windows toohello.  Można zebrać zdarzenia z dzienników standardowe, takie jak systemu i aplikacji w toospecifying dodawania żadnych dzienników niestandardowych utworzone przez aplikacje należy toomonitor.

![Zdarzenia systemu Windows](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Dzienniki zdarzeń Konfigurowanie systemu Windows
Skonfiguruj dzienniki zdarzeń systemu Windows hello [danych menu Ustawienia usługi Analiza dzienników](log-analytics-data-sources.md#configuring-data-sources).

Analizy dzienników zbiera tylko zdarzenia z dzienników zdarzeń systemu Windows hello, które są określone w ustawieniach hello.  Można dodać dziennika zdarzeń, wpisując nazwę hello hello dziennika, a następnie klikając polecenie  **+** .  Dla każdego dziennika są zbierane tylko zdarzenia hello hello wybrane ważności.  Sprawdź hello wag dla hello dziennika, które mają toocollect.  Nie można podać wszelkie dodatkowe kryteria toofilter zdarzenia.

Podczas wpisywania nazwy hello dziennika zdarzeń analizy dzienników zawiera sugestie dotyczące typowych nazw w dzienniku zdarzeń. Jeśli dziennik hello ma tooadd nie ma na liście hello, należy go dodać wprowadzając pełną nazwę dziennika hello hello. Pełna nazwa hello hello dziennika można znaleźć za pomocą Podglądu zdarzeń. W Podglądzie zdarzeń, otwórz hello *właściwości* stronę hello dziennika i skopiuj ciąg hello z hello *imię i nazwisko* pola.

![Skonfiguruj zdarzenia systemu Windows](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Zbieranie danych
Analiza dzienników zbiera każdego zdarzenia odpowiadający wybranej ważności z monitorowanych dziennika zdarzeń jest tworzone zdarzenie hello.  Hello agent rejestruje jego miejsce w każdym dzienniku zdarzeń zbierane z.  Jeśli w danym okresie czasu hello agent przejdzie do trybu offline, następnie analizy dzienników zbiera dane zdarzeń z którym ostatnio przerwał, nawet jeśli te zdarzenia zostały utworzone podczas hello agent jest w trybie offline.  Istnieje możliwość dla tych toonot zdarzenia zebrane Jeśli dziennik zdarzeń hello opakowuje niepobranych zdarzenia zostaną zastąpione podczas hello agent jest w trybie offline.

>[!NOTE]
>Analiza dzienników nie są zbierane zdarzenia inspekcji utworzone przez program SQL Server ze źródła *MSSQLSERVER* o identyfikatorze zdarzenia 18453, który zawiera słowa kluczowe — *klasycznego* lub *Powodzenie inspekcji* i słowo kluczowe *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Właściwości rekordy zdarzeń systemu Windows
Rekordy zdarzeń systemu Windows mają typ **zdarzeń** i mają właściwości hello w hello w poniższej tabeli:

| Właściwość | Opis |
|:--- |:--- |
| Computer (Komputer) |Nazwę komputera hello hello zdarzeń zostały zebrane. |
| EventCategory |Kategoria zdarzenia hello. |
| EventData |Dane wszystkich zdarzeń w formacie nieprzetworzonym. |
| Identyfikator zdarzenia |Liczba zdarzeń hello. |
| eventLevel |Waga zdarzenia hello w liczbowe. |
| EventLevelName |Ważność hello zdarzenia w postaci tekstu. |
| Dziennik zdarzeń |Nazwa hello dziennika zdarzeń, które hello zdarzeń zostały zebrane. |
| ParameterXml |Wartości parametrów zdarzenia w formacie XML. |
| ManagementGroupName |Nazwa grupy zarządzania hello agenci programu System Center Operations Manager.  Dla innych agentów ta wartość jest AOI-<workspace ID> |
| RenderedDescription |Opis zdarzenia przy użyciu wartości parametrów |
| Element źródłowy |Źródło zdarzenia hello. |
| SourceSystem |Typ zdarzenia hello agenta zostały zebrane. <br> Połącz OpsManager — agent systemu Windows, bądź bezpośrednio lub zarządzanych w programie Operations Manager <br> Linux — wszystkich agentów systemu Linux  <br> AzureStorage — Diagnostyka Azure |
| TimeGenerated |Data i godzina zdarzenia hello został utworzony w systemie Windows. |
| Nazwa użytkownika |Nazwa użytkownika konta hello rejestrowane zdarzenia hello. |

## <a name="log-searches-with-windows-events"></a>Wyszukiwań dziennika zdarzeń systemu Windows
Witaj Poniższa tabela zawiera różne przykłady wyszukiwania dziennika, które pobierają rekordy zdarzeń systemu Windows.

| Zapytanie | Opis |
|:--- |:--- |
| Typ zdarzenia = |Wszystkie zdarzenia systemu Windows. |
| Typ = EventLevelName zdarzenie błędu = |Wszystkie zdarzenia systemu Windows z ważność błędu. |
| Typ = zdarzeń &#124; Miara count() przez źródło |Liczba systemu Windows zdarzenia według źródła. |
| Typ zdarzenia EventLevelName = = błąd &#124; Miara count() przez źródło |Liczba Windows Błąd źródła. |


>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.
>
>| Zapytanie | Opis |
|:---|:---|
| Wydarzenie |Wszystkie zdarzenia systemu Windows. |
| Zdarzenie &#124; gdzie EventLevelName == "error" |Wszystkie zdarzenia systemu Windows z ważność błędu. |
| Zdarzenie &#124; Podsumowanie funkcji count() przez źródło |Liczba systemu Windows zdarzenia według źródła. |
| Zdarzenie &#124; gdzie EventLevelName == "error" &#124; Podsumowanie funkcji count() przez źródło |Liczba Windows Błąd źródła. |


## <a name="next-steps"></a>Następne kroki
* Konfigurowanie analizy dzienników toocollect innych [źródeł danych](log-analytics-data-sources.md) do analizy.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.  
* Użyj [pola niestandardowe](log-analytics-custom-fields.md) rekordów zdarzeń hello tooparse do poszczególnych pól.
* Skonfiguruj [zbiór liczników wydajności](log-analytics-data-sources-performance-counters.md) z agentów systemu Windows.
