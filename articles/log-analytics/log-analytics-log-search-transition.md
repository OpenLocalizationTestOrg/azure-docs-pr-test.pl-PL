---
title: "aaaAzure analizy dzienników zapytania języka ściągawka | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera pomoc na przechodzenie toohello nowy język kwerendy dla analizy dzienników, jeśli już znasz hello starszej wersji języka."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Przechodzenie nowy język kwerendy tooAzure analizy dzienników

> [!NOTE]
> Możesz przeczytać więcej informacji na temat hello analizy dzienników nowego języka zapytań i uzyskać hello tooupgrade procedury obszaru roboczego na uaktualnienie z [wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).

Ten artykuł zawiera pomoc na przechodzenie toohello nowy język kwerendy dla analizy dzienników, jeśli już znasz hello starszej wersji języka.

## <a name="language-converter"></a>Konwerter języka

Jeśli znasz język zapytań usługi Analiza dzienników starszej wersji hello, hello Najprostszym sposobem toocreate hello tego samego zapytania w nowym języku hello jest hello toouse konwerter języka, który jest zainstalowany w portalu wyszukiwania dziennika powitania po przekonwertowaniu obszaru roboczego.  Za pomocą konwertera hello jest tak proste, jak wpisywanie w starszej wersji zapytanie w polu tekstowym top hello, a następnie klikając pozycję **przekonwertować**.  Możesz kliknij hello wyszukiwania przycisk toorun hello zapytania lub kopiowania i wkleić go toouse go w innym miejscu.

![Konwerter języka](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Ściągawka

Witaj Poniższa tabela zawiera porównanie różnych typowych kwerend polecenia tooequivalent między język zapytań nowych i starszych hello w Analiza dzienników Azure.

| Opis | Starsza wersja | Nowy |
|:--|:--|:--|
| Wszystkie tabele wyszukiwania      | error | Wyszukaj "error" (bez rozróżniania wielkości liter) |
| Wybierz dane z tabeli | Typ zdarzenia = |  Wydarzenie |
|                        | Typ = zdarzeń &#124; Wybierz źródło dziennika zdarzeń, identyfikator zdarzenia | Zdarzenie &#124; Źródło dziennika zdarzeń, EventID projektu |
|                        | Typ = zdarzeń &#124; 100 najpopularniejszych | Zdarzenie &#124; podejmij 100 |
| Porównanie ciągów      | Typ = Computer=srv01.contoso.com zdarzeń   | Zdarzenie &#124; gdy komputer == "srv01.contoso.com" |
|                        | Typ = Computer=contains("contoso") zdarzeń | Zdarzenie &#124; gdy komputer zawiera "contoso" (bez rozróżniania wielkości liter)<br>Zdarzenie &#124; gdy komputer contains_cs "Contoso" (z uwzględnieniem wielkości liter) |
|                        | Typ = komputer zdarzenia = wyrażenie regularne ("@contoso@")  | Zdarzenie &#124; gdy komputer zgodny z wyrażeniem regularnym ". *contoso*" |
| Porównanie dat        | Typ zdarzenia TimeGenerated = > 1DAYS teraz | Zdarzenie &#124; gdzie TimeGenerated > ago(1d) |
|                        | Typ zdarzenia TimeGenerated = > TimeGenerated 2017-05-01 < 2017-05-31 | Zdarzenie &#124; gdzie TimeGenerated między (datetime(2017-05-01)... DATETIME(2017-05-31)) |
| Wartość logiczna porównania     | Typ = IsGatewayInstalled pulsu = false  | Pulsu | gdzie IsGatewayInstalled == false |
| Sortuj                   | Typ = zdarzeń &#124; Sortowanie asc komputera, desc dziennika zdarzeń, EventLevelName asc | Zdarzenie \| Sortuj według komputera asc, desc dziennika zdarzeń, EventLevelName asc |
| Różne               | Typ = zdarzeń &#124; Funkcja deduplikacji komputera \| Wybierz komputer | Zdarzenie &#124; Podsumuj według komputera, dziennika zdarzeń |
| Rozszerzenie kolumny         | Typ = CounterName wydajności = "% czasu procesora" &#124; ROZSZERZ if(map(CounterValue,0,50,0,1),"HIGH","LOW") jako wykorzystania | Wydajności &#124; w przypadku, gdy CounterName == "% czasu procesora" \| Rozszerzanie wykorzystania = Jeśli ("Od" równowartości > 50, "HIGH") |
| Agregacji            | Typ = zdarzeń &#124; Miara count() jako liczność według komputera | Zdarzenie &#124; Podsumuj Count = count() przez komputer |
|                                | Typ = wydajności ObjectName = CounterName procesora = "% czasu procesora" &#124; Miara avg(CounterValue) interwał komputera 5 minut | Wydajności &#124; Gdzie ObjectName == "Procesor" i CounterName == "% czasu procesora" &#124; Podsumuj avg(CounterValue) przez komputer, bin (TimeGenerated, 5 minut) |
| Agregacja limit | Typ = zdarzeń &#124; Miara count() przez komputer &#124; 10 pierwszych | Zdarzenie &#124; Podsumuj AggregatedValue = count() przez komputer &#124; limit 10 |
| Unii                  | Typ = zdarzeń lub typ = Syslog | Unia zdarzenia dziennika systemowego |
| Join                   | Typ = NetworkMonitoring &#124; Dołącz AgentIP wewnętrzny (typ = pulsu) ComputerIP | NetworkMonitoring &#124; Dołącz rodzaj = wewnętrzny (wyszukiwania typu == "Pulsu") na $left. AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Następne kroki
- Zapoznaj się z [Samouczek o pisaniu zapytań](https://go.microsoft.com/fwlink/?linkid=856078) przy użyciu hello nowy język kwerendy.
- Zobacz toohello [Query Language Reference](https://go.microsoft.com/fwlink/?linkid=856079) szczegółowe informacje dotyczące polecenia, Operatorzy i funkcje dla hello nowy język kwerendy.  
