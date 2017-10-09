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
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="89091-103">Zapytanie indeksu usługi Azure Search przy użyciu Eksploratora wyszukiwania w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="89091-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89091-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="89091-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="89091-105">Portal</span><span class="sxs-lookup"><span data-stu-id="89091-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="89091-106">.NET</span><span class="sxs-lookup"><span data-stu-id="89091-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="89091-107">REST</span><span class="sxs-lookup"><span data-stu-id="89091-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="89091-108">W tym artykule opisano, jak tooquery usługi Azure Search index przy użyciu **Eksplorator wyszukiwania** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="89091-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="89091-109">Eksplorator wyszukiwania toosubmit prostą, jak i pełne Lucene zapytania ciągów tooany istniejącego indeksu można użyć w usłudze.</span><span class="sxs-lookup"><span data-stu-id="89091-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="89091-110">Witaj Otwórz pulpit nawigacyjny usługi</span><span class="sxs-lookup"><span data-stu-id="89091-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="89091-111">Kliknij przycisk **wszystkie zasoby** paska szybkiego dostępu hello na powitania po lewej stronie powitania [portalu Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="89091-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="89091-112">Wybierz swoją usługę Azure Search.</span><span class="sxs-lookup"><span data-stu-id="89091-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="89091-113">Wybierz indeks</span><span class="sxs-lookup"><span data-stu-id="89091-113">Select an index</span></span>

<span data-ttu-id="89091-114">Wybierz hello indeks ma toosearch z hello **indeksów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="89091-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="89091-115">Otwórz Eksplorator wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="89091-115">Open Search Explorer</span></span>

<span data-ttu-id="89091-116">Kliknij na powitania pasek wyszukiwania hello Otwórz Eksplorator wyszukiwania kafelka tooslide i w okienku wyników.</span><span class="sxs-lookup"><span data-stu-id="89091-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="89091-117">Rozpocznij wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="89091-117">Start searching</span></span>

<span data-ttu-id="89091-118">Korzystając z hello Eksplorator wyszukiwania, możesz określić [parametry zapytania](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="89091-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="89091-119">W polu **Ciąg zapytania** wpisz zapytanie, a następnie naciśnij klawisz **Wyszukaj**.</span><span class="sxs-lookup"><span data-stu-id="89091-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="89091-120">Ciąg zapytania Hello jest automatycznie przekształcany do żądania prawidłowego hello toosubmit adres URL żądania HTTP hello interfejsu API REST wyszukiwanie Azure.</span><span class="sxs-lookup"><span data-stu-id="89091-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="89091-121">Można użyć dowolnego prawidłowy prostą, jak i pełne Lucene składni toocreate hello żądania kwerendy.</span><span class="sxs-lookup"><span data-stu-id="89091-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="89091-122">Witaj `*` znak jest wyszukiwania pusta lub nieokreślona równoważne tooan, które zwraca wszystkie dokumenty w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="89091-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="89091-123">W **wyniki**, wyniki zapytania są prezentowane w nieprzetworzone dane JSON, ładunek toohello identyczne zwracane w treści odpowiedzi HTTP podczas wystawiania żądania programowo.</span><span class="sxs-lookup"><span data-stu-id="89091-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="89091-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89091-124">Next steps</span></span>

<span data-ttu-id="89091-125">Hello następujące zasoby zawierają dodatkowe informacje o składni i przykłady.</span><span class="sxs-lookup"><span data-stu-id="89091-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="89091-126">Prosta składnia zapytań</span><span class="sxs-lookup"><span data-stu-id="89091-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="89091-127">Składnia zapytań Lucene</span><span class="sxs-lookup"><span data-stu-id="89091-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="89091-128">Przykłady składni zapytań Lucene</span><span class="sxs-lookup"><span data-stu-id="89091-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="89091-129">Składnia wyrażeń filtru OData</span><span class="sxs-lookup"><span data-stu-id="89091-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 