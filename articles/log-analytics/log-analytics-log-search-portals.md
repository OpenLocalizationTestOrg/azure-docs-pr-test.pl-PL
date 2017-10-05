---
title: "Portale tworzenia i edytowania dziennika zapytań w programie Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano portali, których można używać w Azure Log Analytics można tworzyć i edytować dziennika wyszukiwania."
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
ms.openlocfilehash: 29dfa31d38f85574f84ed351bc5c26224b1a7e16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portale tworzenia i edytowania dziennika zapytań w programie Azure Log Analytics

> [!NOTE]
> W tym artykule opisano portali w przy użyciu nowego języka zapytań usługi Analiza dzienników Azure.  Możesz dowiedzieć się więcej o nowy język i uzyskać Procedura uaktualniania obszaru roboczego na [uaktualnienia obszaru roboczego analizy dzienników Azure do nowego wyszukiwania dziennika](log-analytics-log-search-upgrade.md).  
>
> Jeśli nowy język kwerendy nie została ona uaktualniona obszaru roboczego, należy zapoznać się [wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md) Aby uzyskać informacje o bieżącej wersji portalu wyszukiwania dziennika.

Dziennik wyszukiwania w różnych miejscach analizy dzienników służy do pobierania danych z obszaru roboczego.  Faktycznie tworzenie i edytowanie zapytań oprócz pracy interakcyjnie z dane zwrotne jednak, masz dwie opcje, które są opisane poniżej.  

## <a name="log-search-portal"></a>Dziennik wyszukiwania portalu
Portal wyszukiwania dziennika jest dostępny w portalu Azure lub w portalu OMS.  Jest ona odpowiednia dla tworzenia podstawowych zapytań, które mogą zostać utworzone w jednym wierszu.  Portal dziennik wyszukiwania może być używany bez uruchamiania zewnętrznego portalu i służy do wykonywania różnych funkcji z dziennika wyszukiwania w tym tworzenie reguły alertu, tworzenie grup komputerów i eksportowanie wyników zapytania.  

Portal wyszukiwania dziennika zawiera wiele funkcji do edycji zapytanie bez pełnej znajomości języka kwerend.  Można uzyskać podsumowanie informacji o tych funkcji w [Utwórz dziennik wyszukiwania w Analiza dzienników Azure przy użyciu portalu wyszukiwania dziennika](log-analytics-log-search-log-search-portal.md).


![Dziennik wyszukiwania portalu](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Zaawansowane portal analityka
Portal zaawansowana analityka jest dedykowany portal, który udostępnia zaawansowane funkcje, które nie jest dostępne w portalu wyszukiwania dziennika.  Funkcje obejmują możliwość edytowania zapytania w wielu wierszach, selektywnie wykonania kodu, kontekstowej Intellisense i analiza inteligentne.  Portal analityka zaawansowane jest najbardziej odpowiednie dla projektowania złożonych zapytań, które są albo zapisywane jako dziennik wyszukiwania lub kopiować i wklejać do innych elementów analizy dzienników.  Można uruchomić portal analityka Zaawansowane z linku w portalu wyszukiwania dziennika.

![Zaawansowane portal analityka](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Ze względu na jego funkcje zaawansowane zwykle użyjesz portalu zaawansowana analityka jako narzędzia do głównej tworzenia i edytowania zapytania.  Po określeniu, czy zapytanie działa zgodnie z oczekiwaniami, a następnie należy go skopiować i wkleić go w innym miejscu takie jak dziennik wyszukiwania portalu lub Widok projektanta.  Ponieważ portal analityka zaawansowane obsługuje jednak zapytania z wielu wierszy, należy wziąć pod uwagę następujące pod uwagę podczas kopiowania zapytania z tego portalu.

- Komentarze należy usunąć z zapytania przed skopiować i wkleić do innej lokalizacji.  Komentarz dotyczący wiersza poprzedzając ją dwa ukośniki (/ /).  Podczas wklejania wielu zapytań wiersza w jednym wierszu, podziały wiersza zostaną usunięte.  Jeśli są uwzględniane, wszystkie znaki od pierwszego komentarza są traktowane jako część komentarza.


## <a name="next-steps"></a>Następne kroki

- Zapoznaj się z artykułem samouczek na temat używania [dziennik wyszukiwania portalu](log-analytics-log-search-log-search-portal.md) lub [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587) tworzenia zapytań.
- Zapoznaj się z [Samouczek o pisaniu zapytań](https://go.microsoft.com/fwlink/?linkid=856078) przy użyciu nowego języka zapytań.
