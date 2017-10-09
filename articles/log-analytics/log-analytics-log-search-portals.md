---
title: "aaaPortals tworzenia i edytowania dziennika zapytań w programie Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano portali hello można użyć w toocreate Analiza dzienników Azure i edytować dziennik wyszukiwania."
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
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portale tworzenia i edytowania dziennika zapytań w programie Azure Log Analytics

> [!NOTE]
> W tym artykule opisano portali w przy użyciu hello nowego języka zapytań usługi Analiza dzienników Azure.  Możesz dowiedzieć się więcej o nowy język hello i uzyskać hello procedury tooupgrade obszaru roboczego na [uaktualnienia wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).  
>
> Jeśli obszar roboczy nie został uaktualniony toohello nowy język zapytań, należy zapoznać się zbyt[wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md) Aby uzyskać informacje o bieżącej wersji hello hello dziennik wyszukiwania portalu.

Możesz użyć dziennika wyszukiwania w różnych miejscach analizy dzienników tooretrieve danych z obszaru roboczego hello.  Faktycznie tworzenia i edytowania zapytania dodatkowo tooworking interakcyjnie z zwróciła dane jednak, dostępne są dwie opcje, które są opisane poniżej.  

## <a name="log-search-portal"></a>Dziennik wyszukiwania portalu
portal wyszukiwania dziennika Hello jest dostępny z hello portalu Azure lub hello portalu OMS.  Jest ona odpowiednia dla tworzenia podstawowych zapytań, które mogą zostać utworzone w jednym wierszu.  portal wyszukiwania dziennika Hello może być używany bez uruchamiania zewnętrznego portalu i umożliwia tooperform różne funkcje z tym tworzenie reguły alertu, tworzenie grup komputerów i eksportowanie wyników hello hello zapytania wyszukiwania dziennika.  

portal wyszukiwania dziennika Hello udostępnia wiele funkcji do edycji zapytania hello bez pełnej znajomości języka kwerend hello.  Można uzyskać podsumowanie informacji o tych funkcji w [Utwórz dziennik wyszukiwania przy użyciu hello dziennik wyszukiwania portalu usługi Analiza dzienników Azure](log-analytics-log-search-log-search-portal.md).


![Dziennik wyszukiwania portalu](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Zaawansowane portal analityka
portal zaawansowana analityka Hello jest dedykowany portal, który udostępnia zaawansowane funkcje, które nie jest dostępne w portalu wyszukiwania dziennika hello.  Funkcje obejmują hello możliwości tooedit zapytania w wielu wierszach, selektywnie wykonania kodu, kontekstowej Intellisense i analiza inteligentne.  portal analityka zaawansowane Hello jest najbardziej odpowiednie dla projektowania złożonych zapytań, które są albo zapisywane jako dziennik wyszukiwania lub kopiować i wklejać do innych elementów analizy dzienników.  Można uruchomić portal analityka zaawansowane hello z linku w portalu wyszukiwania dziennika hello.

![Zaawansowane portal analityka](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Ze względu na jego funkcje zaawansowane zwykle użyjesz hello zaawansowana analityka portalu jako podstawowy narzędzie tworzenia i edytowania zapytania.  Po określeniu, czy zapytanie hello działa zgodnie z oczekiwaniami, a następnie należy go skopiować i wkleić go w innym miejscu, takich jak hello dziennik wyszukiwania portalu lub Widok projektanta.  Ponieważ portal analityka zaawansowane hello obsługuje jednak zapytania z wielu wierszy, należy tootake hello następujące kwestie, kopiując zapytania z tego portalu.

- Komentarze należy usunąć z kwerendy hello przed skopiować i wkleić do innej lokalizacji.  Komentarz dotyczący wiersza poprzedzając ją dwa ukośniki (/ /).  Podczas wklejania wielu zapytań wiersza w jednym wierszu, podziały wiersza zostaną usunięte.  Jeśli są uwzględniane, wszystkie znaki od pierwszego komentarza hello są traktowane jako część hello komentarza.


## <a name="next-steps"></a>Następne kroki

- Zapoznaj się z artykułem samouczek na temat używania hello [dziennik wyszukiwania portalu](log-analytics-log-search-log-search-portal.md) lub hello [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587) toocreate zapytania.
- Zapoznaj się z [Samouczek o pisaniu zapytań](https://go.microsoft.com/fwlink/?linkid=856078) przy użyciu hello nowy język kwerendy.
