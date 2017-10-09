---
title: "AAA \"Tworzenie zapytań względem indeksu (portal — usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Generowanie zapytań wyszukiwania w Eksploratorze wyszukiwania portalu Azure hello."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Zapytanie indeksu usługi Azure Search przy użyciu Eksploratora wyszukiwania w hello portalu Azure
> [!div class="op_single_selector"]
> * [Omówienie](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

W tym artykule opisano, jak tooquery usługi Azure Search index przy użyciu **Eksplorator wyszukiwania** w hello portalu Azure. Eksplorator wyszukiwania toosubmit prostą, jak i pełne Lucene zapytania ciągów tooany istniejącego indeksu można użyć w usłudze.

## <a name="open-hello-service-dashboard"></a>Witaj Otwórz pulpit nawigacyjny usługi
1. Kliknij przycisk **wszystkie zasoby** paska szybkiego dostępu hello na powitania po lewej stronie powitania [portalu Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Wybierz swoją usługę Azure Search.

## <a name="select-an-index"></a>Wybierz indeks

Wybierz hello indeks ma toosearch z hello **indeksów** kafelka.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Otwórz Eksplorator wyszukiwania

Kliknij na powitania pasek wyszukiwania hello Otwórz Eksplorator wyszukiwania kafelka tooslide i w okienku wyników.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Rozpocznij wyszukiwanie

Korzystając z hello Eksplorator wyszukiwania, możesz określić [parametry zapytania](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello zapytania.

1. W polu **Ciąg zapytania** wpisz zapytanie, a następnie naciśnij klawisz **Wyszukaj**. 

   Ciąg zapytania Hello jest automatycznie przekształcany do żądania prawidłowego hello toosubmit adres URL żądania HTTP hello interfejsu API REST wyszukiwanie Azure.   
   
   Można użyć dowolnego prawidłowy prostą, jak i pełne Lucene składni toocreate hello żądania kwerendy. Witaj `*` znak jest wyszukiwania pusta lub nieokreślona równoważne tooan, które zwraca wszystkie dokumenty w określonej kolejności.

2. W **wyniki**, wyniki zapytania są prezentowane w nieprzetworzone dane JSON, ładunek toohello identyczne zwracane w treści odpowiedzi HTTP podczas wystawiania żądania programowo.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Następne kroki

Hello następujące zasoby zawierają dodatkowe informacje o składni i przykłady.

 + [Prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Składnia zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Przykłady składni zapytań Lucene](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [Składnia wyrażeń filtru OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 