---
title: "Dodaj akcję zapytania w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie działania zapytania do wykonywania akcji, takich jak tablicy filtrów."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="b2121-103">Rozpoczynanie pracy z akcją zapytań</span><span class="sxs-lookup"><span data-stu-id="b2121-103">Get started with the query action</span></span>
<span data-ttu-id="b2121-104">Za pomocą akcji zapytania, możesz pracować z partii i tablic w celu przepływy pracy, aby:</span><span class="sxs-lookup"><span data-stu-id="b2121-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="b2121-105">Utwórz zadania dla wszystkich rekordów o wysokim priorytecie z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b2121-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="b2121-106">Zapisz wszystkie załączniki plików PDF do wiadomości e-mail do obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b2121-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="b2121-107">Aby rozpocząć, korzystając z akcji zapytania w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2121-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="b2121-108">Za pomocą akcji zapytania</span><span class="sxs-lookup"><span data-stu-id="b2121-108">Use the query action</span></span>
<span data-ttu-id="b2121-109">Akcja jest operacja odbywa się przez przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b2121-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="b2121-110">[Dowiedz się więcej o akcjach](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2121-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="b2121-111">Akcja zapytania ma obecnie jedną operację o nazwie tablicy filtrów, która jest widoczna w projektancie.</span><span class="sxs-lookup"><span data-stu-id="b2121-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="b2121-112">Umożliwia to zapytanie tablicy i zwraca zestawu wyników filtrowane.</span><span class="sxs-lookup"><span data-stu-id="b2121-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="b2121-113">Oto, jak można dodać go w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="b2121-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="b2121-114">Wybierz **nowy krok** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b2121-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="b2121-115">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="b2121-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b2121-116">W polu wyszukiwania akcji wpisz **filtru** do listy **tablicy filtrów** akcji.</span><span class="sxs-lookup"><span data-stu-id="b2121-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Wybierz akcję zapytania](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="b2121-118">Wybierz tablicę do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="b2121-118">Select an array to filter.</span></span> <span data-ttu-id="b2121-119">(Poniższy zrzut ekranu przedstawia tablicy wyniki wyszukiwania Twitter).</span><span class="sxs-lookup"><span data-stu-id="b2121-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="b2121-120">Warunku można oszacować na każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="b2121-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="b2121-121">(Poniższy zrzut ekranu filtry tweetów od użytkowników, którzy mają więcej niż 100 adherentami).</span><span class="sxs-lookup"><span data-stu-id="b2121-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Zakończenie akcji zapytania](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="b2121-123">Akcja dane wyjściowe obejmują nowe tablica, która zawiera tylko wyniki, które zostały spełnione wymagania dotyczące filtru.</span><span class="sxs-lookup"><span data-stu-id="b2121-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="b2121-124">Kliknij w lewym górnym rogu paska narzędzi, aby zapisać i aplikacji logiki będzie Zapisz i opublikuj (Aktywuj).</span><span class="sxs-lookup"><span data-stu-id="b2121-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="b2121-125">Akcja kwerendy</span><span class="sxs-lookup"><span data-stu-id="b2121-125">Query action</span></span>
<span data-ttu-id="b2121-126">Poniżej przedstawiono szczegóły akcję, która obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="b2121-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="b2121-127">Łącznik ma jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="b2121-127">The connector has one possible action.</span></span>

| <span data-ttu-id="b2121-128">Akcja</span><span class="sxs-lookup"><span data-stu-id="b2121-128">Action</span></span> | <span data-ttu-id="b2121-129">Opis</span><span class="sxs-lookup"><span data-stu-id="b2121-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2121-130">Macierz filtru</span><span class="sxs-lookup"><span data-stu-id="b2121-130">Filter array</span></span> |<span data-ttu-id="b2121-131">Sprawdza warunek dla każdego elementu w tablicy i zwraca wyniki</span><span class="sxs-lookup"><span data-stu-id="b2121-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="b2121-132">Szczegóły akcji</span><span class="sxs-lookup"><span data-stu-id="b2121-132">Action details</span></span>
<span data-ttu-id="b2121-133">Akcja kwerendy jest dostarczany z jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="b2121-133">The query action comes with one possible action.</span></span> <span data-ttu-id="b2121-134">Poniższe tabele zawierają opis wymaganych i opcjonalnych pól wejściowych dla akcji i odpowiednie szczegóły danych wyjściowych, które są skojarzone z przy użyciu akcji.</span><span class="sxs-lookup"><span data-stu-id="b2121-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="b2121-135">Macierz filtru</span><span class="sxs-lookup"><span data-stu-id="b2121-135">Filter array</span></span>
<span data-ttu-id="b2121-136">Poniżej przedstawiono pól wejściowych dla akcji, dzięki czemu wychodzące żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="b2121-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="b2121-137">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="b2121-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="b2121-138">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="b2121-138">Display name</span></span> | <span data-ttu-id="b2121-139">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="b2121-139">Property name</span></span> | <span data-ttu-id="b2121-140">Opis</span><span class="sxs-lookup"><span data-stu-id="b2121-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2121-141">Z *</span><span class="sxs-lookup"><span data-stu-id="b2121-141">From*</span></span> |<span data-ttu-id="b2121-142">Z</span><span class="sxs-lookup"><span data-stu-id="b2121-142">from</span></span> |<span data-ttu-id="b2121-143">Tablica do filtrowania</span><span class="sxs-lookup"><span data-stu-id="b2121-143">The array to filter</span></span> |
| <span data-ttu-id="b2121-144">Warunek *</span><span class="sxs-lookup"><span data-stu-id="b2121-144">Condition*</span></span> |<span data-ttu-id="b2121-145">gdzie</span><span class="sxs-lookup"><span data-stu-id="b2121-145">where</span></span> |<span data-ttu-id="b2121-146">Warunek, który ma zostać obliczone dla każdego elementu</span><span class="sxs-lookup"><span data-stu-id="b2121-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="b2121-147">Szczegóły danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="b2121-147">Output details</span></span>
<span data-ttu-id="b2121-148">Poniżej przedstawiono szczegóły danych wyjściowych dla odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="b2121-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="b2121-149">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="b2121-149">Property name</span></span> | <span data-ttu-id="b2121-150">Typ danych</span><span class="sxs-lookup"><span data-stu-id="b2121-150">Data type</span></span> | <span data-ttu-id="b2121-151">Opis</span><span class="sxs-lookup"><span data-stu-id="b2121-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2121-152">Filtrowane tablicy</span><span class="sxs-lookup"><span data-stu-id="b2121-152">Filtered array</span></span> |<span data-ttu-id="b2121-153">Tablica</span><span class="sxs-lookup"><span data-stu-id="b2121-153">array</span></span> |<span data-ttu-id="b2121-154">Tablica, która zawiera obiekt dla każdego wyniku filtrowane</span><span class="sxs-lookup"><span data-stu-id="b2121-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2121-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2121-155">Next steps</span></span>
<span data-ttu-id="b2121-156">Teraz, wypróbuj platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2121-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b2121-157">Dostępne łączniki w aplikacjach logiki można eksplorować analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b2121-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

