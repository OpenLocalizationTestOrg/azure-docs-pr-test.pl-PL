---
title: Akcja kwerendy hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft
description: "Przegląd hello zapytania akcji do wykonania akcji, takich jak tablicy filtrów."
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
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="55c0f-103">Rozpoczynanie pracy z akcją zapytań hello</span><span class="sxs-lookup"><span data-stu-id="55c0f-103">Get started with hello query action</span></span>
<span data-ttu-id="55c0f-104">Za pomocą akcji zapytania hello, możesz pracować z partii tablice tooaccomplish przepływy pracy i do:</span><span class="sxs-lookup"><span data-stu-id="55c0f-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="55c0f-105">Utwórz zadania dla wszystkich rekordów o wysokim priorytecie z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="55c0f-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="55c0f-106">Zapisz wszystkie załączniki plików PDF do wiadomości e-mail do obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="55c0f-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="55c0f-107">tooget uruchomiony przy użyciu akcji zapytania hello w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="55c0f-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="55c0f-108">Za pomocą akcji zapytania hello</span><span class="sxs-lookup"><span data-stu-id="55c0f-108">Use hello query action</span></span>
<span data-ttu-id="55c0f-109">Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="55c0f-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="55c0f-110">[Dowiedz się więcej o akcjach](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55c0f-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="55c0f-111">Akcja kwerendy Hello aktualnie ma jedną operację o nazwie tablicy filtrów hello, która jest widoczna w Projektancie hello.</span><span class="sxs-lookup"><span data-stu-id="55c0f-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="55c0f-112">To pozwala tooquery tablicy i zwraca zestawu wyników filtrowane.</span><span class="sxs-lookup"><span data-stu-id="55c0f-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="55c0f-113">Oto, jak można dodać go w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="55c0f-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="55c0f-114">Wybierz hello **nowy krok** przycisku.</span><span class="sxs-lookup"><span data-stu-id="55c0f-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="55c0f-115">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="55c0f-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="55c0f-116">W polu wyszukiwania akcji hello wpisz **filtru** toolist hello **tablicy filtrów** akcji.</span><span class="sxs-lookup"><span data-stu-id="55c0f-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Wybierz akcję zapytania hello](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="55c0f-118">Wybierz toofilter tablicy.</span><span class="sxs-lookup"><span data-stu-id="55c0f-118">Select an array toofilter.</span></span> <span data-ttu-id="55c0f-119">(hello Poniższy zrzut ekranu przedstawia hello tablicę wyniki wyszukiwania usługi Twitter.)</span><span class="sxs-lookup"><span data-stu-id="55c0f-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="55c0f-120">Utwórz tooevaluate warunku w każdym elemencie.</span><span class="sxs-lookup"><span data-stu-id="55c0f-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="55c0f-121">(hello następującego zrzutu ekranu filtry tweetów od użytkowników, którzy mają więcej niż 100 adherentami).</span><span class="sxs-lookup"><span data-stu-id="55c0f-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Akcja kwerendy hello ukończone](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="55c0f-123">Akcja Hello dane wyjściowe obejmują nowe tablica, która zawiera tylko wyniki, które spełniają wymagań filtru hello.</span><span class="sxs-lookup"><span data-stu-id="55c0f-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="55c0f-124">Kliknij przycisk hello lewego górnego rogu hello toosave narzędzi i Twoje logiki aplikacji zapisze zarówno i publikowanie (Aktywuj).</span><span class="sxs-lookup"><span data-stu-id="55c0f-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="55c0f-125">Akcja kwerendy</span><span class="sxs-lookup"><span data-stu-id="55c0f-125">Query action</span></span>
<span data-ttu-id="55c0f-126">Poniżej przedstawiono szczegóły hello hello akcję, która obsługuje ten łącznik.</span><span class="sxs-lookup"><span data-stu-id="55c0f-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="55c0f-127">Łącznik Hello ma jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="55c0f-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="55c0f-128">Akcja</span><span class="sxs-lookup"><span data-stu-id="55c0f-128">Action</span></span> | <span data-ttu-id="55c0f-129">Opis</span><span class="sxs-lookup"><span data-stu-id="55c0f-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55c0f-130">Macierz filtru</span><span class="sxs-lookup"><span data-stu-id="55c0f-130">Filter array</span></span> |<span data-ttu-id="55c0f-131">Sprawdza warunek dla każdego elementu w tablicy i zwraca wyniki hello</span><span class="sxs-lookup"><span data-stu-id="55c0f-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="55c0f-132">Szczegóły akcji</span><span class="sxs-lookup"><span data-stu-id="55c0f-132">Action details</span></span>
<span data-ttu-id="55c0f-133">Akcja kwerendy Hello jest dostarczany z jedną akcję możliwe.</span><span class="sxs-lookup"><span data-stu-id="55c0f-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="55c0f-134">Witaj poniższych tabelach opisano hello wymagane i opcjonalne pola wejściowego dla akcji hello i hello odpowiednie dane wyjściowe szczegóły, które są skojarzone z przy użyciu akcji hello.</span><span class="sxs-lookup"><span data-stu-id="55c0f-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="55c0f-135">Macierz filtru</span><span class="sxs-lookup"><span data-stu-id="55c0f-135">Filter array</span></span>
<span data-ttu-id="55c0f-136">Oto Hello pól wejściowych dla akcji hello, dzięki czemu żądania wychodzącego HTTP.</span><span class="sxs-lookup"><span data-stu-id="55c0f-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="55c0f-137">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="55c0f-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="55c0f-138">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="55c0f-138">Display name</span></span> | <span data-ttu-id="55c0f-139">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="55c0f-139">Property name</span></span> | <span data-ttu-id="55c0f-140">Opis</span><span class="sxs-lookup"><span data-stu-id="55c0f-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55c0f-141">Z *</span><span class="sxs-lookup"><span data-stu-id="55c0f-141">From*</span></span> |<span data-ttu-id="55c0f-142">Z</span><span class="sxs-lookup"><span data-stu-id="55c0f-142">from</span></span> |<span data-ttu-id="55c0f-143">Witaj toofilter tablicy</span><span class="sxs-lookup"><span data-stu-id="55c0f-143">hello array toofilter</span></span> |
| <span data-ttu-id="55c0f-144">Warunek *</span><span class="sxs-lookup"><span data-stu-id="55c0f-144">Condition*</span></span> |<span data-ttu-id="55c0f-145">gdzie</span><span class="sxs-lookup"><span data-stu-id="55c0f-145">where</span></span> |<span data-ttu-id="55c0f-146">Witaj tooevaluate warunek dla każdego elementu</span><span class="sxs-lookup"><span data-stu-id="55c0f-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="55c0f-147">Szczegóły danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="55c0f-147">Output details</span></span>
<span data-ttu-id="55c0f-148">Witaj poniżej przedstawiono szczegóły danych wyjściowych dla hello odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="55c0f-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="55c0f-149">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="55c0f-149">Property name</span></span> | <span data-ttu-id="55c0f-150">Typ danych</span><span class="sxs-lookup"><span data-stu-id="55c0f-150">Data type</span></span> | <span data-ttu-id="55c0f-151">Opis</span><span class="sxs-lookup"><span data-stu-id="55c0f-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55c0f-152">Filtrowane tablicy</span><span class="sxs-lookup"><span data-stu-id="55c0f-152">Filtered array</span></span> |<span data-ttu-id="55c0f-153">Tablica</span><span class="sxs-lookup"><span data-stu-id="55c0f-153">array</span></span> |<span data-ttu-id="55c0f-154">Tablica, która zawiera obiekt dla każdego wyniku filtrowane</span><span class="sxs-lookup"><span data-stu-id="55c0f-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55c0f-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55c0f-155">Next steps</span></span>
<span data-ttu-id="55c0f-156">Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="55c0f-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="55c0f-157">Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="55c0f-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

