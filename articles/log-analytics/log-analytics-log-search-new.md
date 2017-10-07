---
title: aaaLog wyszukiwania OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Tooretrieve wyszukiwania dziennika jest wymagane żadne dane z analizy dzienników.  W tym artykule opisano sposób nowy dziennik wyszukiwania są używane w analizy dzienników i zapewnia koncepcje potrzebne toounderstand przed utworzeniem jeden."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Opis wyszukiwania dziennika analizy dzienników

> [!NOTE]
> W tym artykule opisano dziennik wyszukiwania przy użyciu hello nowego języka zapytań usługi Analiza dzienników Azure.  Możesz dowiedzieć się więcej o nowy język hello i uzyskać hello procedury tooupgrade obszaru roboczego na [uaktualnienia wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).  
>
> Jeśli obszar roboczy nie został uaktualniony toohello nowy język zapytań, należy zapoznać się zbyt[wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md).

Tooretrieve wyszukiwania dziennika jest wymagane żadne dane z analizy dzienników.  Czy w przypadku analizowania danych w portalu hello, konfigurowanie toobe reguły alertu powiadomienie określony warunek, lub podczas pobierania danych przy użyciu hello dziennika analizy interfejsu API, będzie używać danych hello toospecify wyszukiwania dziennika, który ma.  W tym artykule opisano sposób użycia dziennika wyszukiwania w analizy dzienników i zapewnia pojęcia, które należy zrozumieć przed utworzeniem jeden. Zobacz hello [następne kroki](#next-steps) sekcji, aby uzyskać więcej informacji na temat tworzenia i edytowania dziennik wyszukiwania i odwołań na powitania język zapytań.

## <a name="where-log-searches-are-used"></a>Gdzie są używane dziennik wyszukiwania

różne sposoby Hello, który będzie używany dziennik wyszukiwania w analizy dzienników Uwzględnij hello następujące elementy:

- **Portale.** Można wykonywać analizy interakcyjnej danych w repozytorium hello i hello [dziennik wyszukiwania portalu](log-analytics-log-search-log-search-portal.md) lub hello [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587).  Dzięki temu można tooedit Twojego zapytania i Analizuj wyniki hello w różnych formatach i wizualizacji.  Większość zapytań, które możesz utworzyć zostanie uruchomiony w jednym z portali hello i następnie skopiowana po zweryfikowaniu, że działa zgodnie z oczekiwaniami.
- **Reguły alertów.** [Reguły alertów](log-analytics-alerts.md) aktywne identyfikowanie problemów z danych w obszarze roboczym.  Każdej reguły alertu jest oparta na wyszukiwania dziennika, który jest automatycznie uruchamiany w regularnych odstępach czasu.  wyniki Hello są toodetermine kontrolowanego, jeśli alert powinien zostać utworzony.
- **Widoki.**  Możesz utworzyć wizualizacje toobe dane zawarte w pulpity nawigacyjne użytkownika z [Widok projektanta](log-analytics-view-designer.md).  Wyszukiwanie dziennika zawierają dane hello używane przez [Kafelki](log-analytics-view-designer-tiles.md) i [części wizualizacji](log-analytics-view-designer-parts.md) w każdym widoku.  Możesz można przejść z części wizualizacji do hello dziennik wyszukiwania portalu tooperform dalszą analizę danych hello.
- **Eksportowanie.**  Podczas eksportowania danych z tooExcel obszaru roboczego analizy dzienników hello lub [usługi Power BI](log-analytics-powerbi.md), Utwórz tooexport dziennik wyszukiwania toodefine hello danych.
- **Środowiska PowerShell.** Należy uruchomić skrypt programu PowerShell z wiersza polecenia lub element runbook usługi Automatyzacja Azure, która używa [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve dane z analizy dzienników.  To polecenie cmdlet wymaga kwerendy toodetermine hello danych tooretrieve.
- **Interfejs API analizy dziennika.**  Witaj [analizy dzienników dziennika wyszukiwania interfejsu API](log-analytics-log-search-api.md) umożliwia tooretrieve danych z obszaru roboczego hello dowolnego klienta interfejsu API REST.  żądanie interfejsu API Hello zawiera zapytanie, które jest wykonywane na tooretrieve danych hello toodetermine analizy dzienników.

![Dziennik wyszukiwania](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Sposób organizowania danych analizy dzienników
Podczas tworzenia zapytania należy rozpocząć od określania tabel, które znajdują się dane hello, którego szukasz. Każdy [źródła danych](log-analytics-data-sources.md) i [rozwiązania](../operations-management-suite/operations-management-suite-solutions.md) przechowuje dane w tabelach dedykowanych w obszarze roboczym analizy dzienników hello.  Dokumentacja dla każdego źródła danych i rozwiązanie zawiera nazwę hello hello typu danych, które tworzy i opis każdego z jego właściwości.     Wiele zapytań będzie wymagać tylko dane z jednej tabeli, ale inne osoby mogą używać różnych opcji tooinclude danych z wielu tabel.

![Tabele](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Pisanie zapytań
W podstawowej hello dziennika jest wyszukiwanie w analizy dzienników [język zapytań szeroką gamę](https://docs.loganalytics.io/) umożliwia pobieranie i analizowanie danych z repozytorium hello na różne sposoby.  Tym samym języku zapytania jest używana do [usługi Application Insights](../application-insights/app-insights-analytics.md).  Learning, jak toowrite zapytania jest krytyczne toocreating wyszukiwania dziennika analizy dzienników.  Będzie zazwyczaj rozpoczyna się z zapytaniami podstawowa, a następnie toouse postępu bardziej zaawansowane funkcje zgodnie z wymaganiami staną się bardziej złożonych.

Hello podstawową strukturę zapytania jest tabela źródłowa następuje szereg operatory oddzielone znakiem potoku `|`.  Możesz łańcuch wielu operatorów toorefine hello danych i wykonywanie zaawansowanych funkcji.

Na przykład załóżmy, że chce toofind hello top dziesięć komputerów z hello większość zdarzeń błędów za pośrednictwem hello dnia.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

A może warto toofind komputerów, które nie mam pulsu w hello ostatni dzień.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

Jak wykres liniowy z hello użycie procesora dla każdego komputera w ostatnim tygodniu?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Z tych szybkie przykłady, które niezależnie od hello rodzaj danych, które użytkownik pracuje, hello można zauważyć, że przypomina strukturę hello zapytania.  Można podzielić je w dół na różne czynności wysyłania hello danych wynikowych polecenia za pomocą potoku hello toohello następnego polecenia.

Pełna dokumentacja języka zapytań usługi Analiza dzienników Azure hello tym samouczki i materiały referencyjne dotyczące języka, zobacz hello [dokumentację dotyczącą języka zapytań usługi Analiza dzienników Azure](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o hello [portali Użyj toocreate, a następnie edytować dziennik wyszukiwania](log-analytics-log-search-portals.md).
- Zapoznaj się z [Samouczek o pisaniu zapytań](https://go.microsoft.com/fwlink/?linkid=856078) przy użyciu hello nowy język kwerendy.
