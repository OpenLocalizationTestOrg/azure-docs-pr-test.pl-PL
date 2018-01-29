---
title: "Tworzenie zapytań względem indeksu (portal — usługa Azure Search) | Dokumentacja firmy Microsoft"
description: "Generowanie zapytań wyszukiwania w Eksploratorze wyszukiwania witryny Azure Portal."
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
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a>Tworzenie zapytań względem indeksu usługi Azure Search przy użyciu Eksploratora wyszukiwania w witrynie Azure Portal
> [!div class="op_single_selector"]
> * [Omówienie](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

W tym artykule opisano sposób tworzenia zapytań względem indeksu usługi Azure Search przy użyciu **Eksploratora wyszukiwania** w witrynie Azure Portal. Eksploratora wyszukiwania można użyć do przesyłania prostych lub pełnych ciągów zapytań Lucene do dowolnego istniejącego indeksu w usłudze.

## <a name="open-the-service-dashboard"></a>Otwórz pulpit nawigacyjny usługi
1. Na pasku dostępu po lewej stronie w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices) kliknij opcję **Wszystkie zasoby**.
2. Wybierz swoją usługę Azure Search.

## <a name="select-an-index"></a>Wybierz indeks

Z kafelka **Indeksy** wybierz indeks, który chcesz przeszukać.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Otwórz Eksplorator wyszukiwania

Kliknij kafelek Eksplorator wyszukiwania, aby wysunąć pasek wyszukiwania i okienko wyników.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Rozpocznij wyszukiwanie

Podczas używania Eksploratora wyszukiwania możesz określić dowolne [parametry zapytania](https://docs.microsoft.com/rest/api/searchservice/Search-Documents), aby sformułować zapytanie.

1. W polu **Ciąg zapytania** wpisz zapytanie, a następnie naciśnij klawisz **Wyszukaj**. 

   Ciąg zapytania jest automatycznie przekształcany do odpowiedniego adresu URL żądania w celu przesłania żądania HTTP do interfejsu API REST usługi Azure Search.   
   
   Do utworzenia żądania możesz użyć dowolnej poprawnej prostej lub pełnej składni zapytań Lucene. Znak `*` jest odpowiednikiem pustego lub nieokreślonego wyszukiwania, które zwraca wszystkie dokumenty w losowej kolejności.

2. Wyniki zapytania są prezentowane w obszarze **Wyniki** w niesformatowanej strukturze JSON, w taki sam sposób, jak ładunek zwracany w treści odpowiedzi HTTP podczas programowego wystawiania żądań.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Następne kroki

W następujących zasobach udostępniono dodatkowe informacje o składni oraz przykłady.

 + [Prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Składnia zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Przykłady składni zapytań Lucene](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [Składnia wyrażeń filtru OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 