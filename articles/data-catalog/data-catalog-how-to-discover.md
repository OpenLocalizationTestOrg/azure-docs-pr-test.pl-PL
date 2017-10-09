---
title: "źródła danych toodiscover aaaHow w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule prezentuje sposób toodiscover zarejestrowanych zasobów danych z usługi Azure Data Catalog, w tym wyszukiwania i filtrowania i przy użyciu hello trafień wyróżnienia możliwości hello portalu wykazu danych Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Jak źródła danych toodiscover w wykazie danych Azure
## <a name="introduction"></a>Wprowadzenie
Wykaz danych Azure to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i odnajdywania źródeł danych przedsiębiorstwa. Innymi słowy Data Catalog pomaga użytkownikom odnajdywania, zrozumienia i używania źródeł danych, a także pomaga organizacjom osiąganie większych zysków z ich istniejących danych. Po zarejestrowaniu źródła danych z wykazu danych metadanych jest indeksowany przez usługę hello, dzięki czemu można łatwo wyszukiwanie potrzebnych danych hello toodiscover.

## <a name="searching-and-filtering"></a>Wyszukiwanie i filtrowanie
Odnajdywania w wykazie danych używa dwóch mechanizmów podstawowego: wyszukiwanie i filtrowanie.

Wyszukiwanie jest zaprojektowana toobe intuicyjny i wydajne. Domyślnie terminy wyszukiwania są dopasowywane do żadnej właściwości w katalogu hello, łącznie z adnotacjami dostarczane przez użytkownika.

Filtrowanie zaprojektowano toocomplement wyszukiwania. Można wybrać określone właściwości, takie jak ekspertów, typ źródła danych typu obiektu i tagów. Wyświetlanie tylko pasujących zasobów danych i ograniczyć zasoby toomatching wyników wyszukiwania.

Przy użyciu kombinacji wyszukiwania i filtrowania, można szybko przejść hello źródeł danych, które zostały zarejestrowane ze źródłami danych hello toodiscover wykazu danych, które są potrzebne.

## <a name="search-syntax"></a>Wyszukiwanie w składni
Mimo że hello domyślne niezależnych wyszukiwanie jest proste i intuicyjne, umożliwia także składni wyszukiwania w wykazie danych uzyskać większą kontrolę nad hello wyniki wyszukiwania. Dane katalogu wyszukiwania obsługuje hello następujące techniki:

| Technika | Użycie | Przykład |
| --- | --- | --- |
| Wyszukiwanie podstawowe |Wyszukiwania podstawowego, który korzysta z jednego lub większej liczby terminów wyszukiwania. Wyniki są dowolny zbiór, który pasuje do żadnej właściwości z co najmniej jednego z warunków hello określony. |`sales data` |
| Wyznaczanie zakresu właściwości |Zwracany tylko źródeł danych, w którym hello wyszukiwany termin jest zgodny z hello określona wartość właściwości. |`name:finance` |
| Operatory logiczne |Poszerzają lub zawężają wyszukiwanie przy użyciu operacji logicznych. |`finance NOT corporate` |
| Grupowanie za pomocą nawiasów |Użyj nawiasów toogroup części hello zapytania tooachieve izolacji logicznej, szczególnie w połączeniu z operatorami logicznymi. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Operatory porównania |Użyj porównań innych niż równość dla właściwości, które mają numeryczne i datowe typy danych. |`modifiedTime > "11/05/2014"` |

Aby uzyskać więcej informacji na temat wyszukiwania w wykazie danych, zobacz hello [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) artykułu.

## <a name="hit-highlighting"></a>Wyróżnianie trafień
Podczas wyświetlania wyników wyszukiwania wyświetlone dowolne właściwości spełniających określone hello terminy wyszukiwania (takich jak nazwa zasobów danych hello, opisie i tagach) są wyróżnione toomake go łatwiejsze tooidentify Dlaczego zasobów podanych danych został zwrócony przez podanym wyszukiwaniem.

> [!NOTE]
> tooturn poza trafień wyróżnianie hello użyj **zaznacz** przełącznika w hello portalu wykazu danych.
>
>

Podczas wyświetlania wyników wyszukiwania, może nie zawsze być oczywista Dlaczego zasobu danych są uwzględnione, nawet w przypadku wyróżnianie trafień włączone. Ponieważ wszystkie właściwości są przeszukiwane domyślnie, zasobu danych może być zwrócony z powodu dopasowania właściwości na poziomie kolumny. I ponieważ wielu użytkowników może dodawać adnotacje do zarejestrowanych zasobów danych z tagami i opisy, nie wszystkie metadane mogą być wyświetlane w hello listy wyników wyszukiwania.

W widoku tile domyślne hello, zawiera każdego kafelka wyświetlane w wynikach wyszukiwania hello **widoku wyszukiwany termin jest zgodny** ikony, dzięki czemu można szybko wyświetlić hello liczbę dopasowań i ich lokalizacji oraz toojump toothem, jeśli chcesz.

 ![Wyróżnianie trafień i wyszukiwanie ma uwzględniać w portalu Azure Data Catalog hello](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Podsumowanie
Ponieważ rejestrowanie źródła danych z kopiami wykazu danych strukturalnych i opisowy metadanych z danych hello źródło toohello katalogu usług, hello źródła danych staje się łatwiejsze toodiscover i zrozumieć. Po źródła danych został zarejestrowany, można go odnaleźć za pomocą filtrowania i wyszukiwanie z poziomu portalu wykazu danych hello.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe informacje krok po kroku na temat toodiscover źródeł danych, zobacz [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md).
