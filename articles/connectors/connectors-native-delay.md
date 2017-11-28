---
title: "aaaAdd opóźnienia w aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Omówienie hello opóźnienia i opóźnienie — do akcji i w jaki sposób toouse z aplikacji logiki platformy Azure."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="5f797-103">Rozpoczynanie pracy z hello opóźnienia i opóźnienie — do działania</span><span class="sxs-lookup"><span data-stu-id="5f797-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="5f797-104">Za pomocą hello opóźnienia i "opóźnienie — do momentu" akcje, ukończeniem scenariuszy przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5f797-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="5f797-105">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="5f797-105">For example, you can:</span></span>

* <span data-ttu-id="5f797-106">Poczekaj, aż toosend dzień tygodnia, stan aktualizacji za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="5f797-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="5f797-107">Przepływ pracy hello opóźnienie do wywołania HTTP ma toofinish czasu przed wznowieniem i pobierania wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="5f797-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="5f797-108">tooget pracy z hello opóźnienie akcji w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5f797-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="5f797-109">Używanie hello opóźnienie akcji</span><span class="sxs-lookup"><span data-stu-id="5f797-109">Use hello delay actions</span></span>
<span data-ttu-id="5f797-110">Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="5f797-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="5f797-111">[Dowiedz się więcej o akcjach](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f797-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="5f797-112">Oto przykład sekwencji jak toouse opóźnienia kroku w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="5f797-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="5f797-113">Po dodaniu wyzwalacza, kliknij przycisk **nowy krok** tooadd akcji.</span><span class="sxs-lookup"><span data-stu-id="5f797-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="5f797-114">Wyszukaj **opóźnienie** toobring się hello opóźnienie akcji.</span><span class="sxs-lookup"><span data-stu-id="5f797-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="5f797-115">W tym przykładzie firma Microsoft będzie wybierać **opóźnienie**.</span><span class="sxs-lookup"><span data-stu-id="5f797-115">In this example, we will select **Delay**.</span></span>
   
    ![Opóźnienie akcji](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="5f797-117">Ukończ wszelkie hello akcji właściwości tooconfigure hello opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="5f797-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Opóźnienie konfiguracji](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="5f797-119">Kliknij przycisk **zapisać** toopublish i aktywować aplikację logiki hello.</span><span class="sxs-lookup"><span data-stu-id="5f797-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="5f797-120">Szczegóły akcji</span><span class="sxs-lookup"><span data-stu-id="5f797-120">Action details</span></span>
<span data-ttu-id="5f797-121">wyzwalacz cyklu Hello ma następujące właściwości, które można skonfigurować hello.</span><span class="sxs-lookup"><span data-stu-id="5f797-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="5f797-122">Opóźnienie akcji</span><span class="sxs-lookup"><span data-stu-id="5f797-122">Delay action</span></span>
<span data-ttu-id="5f797-123">Ta akcja opóźnienia hello Uruchom określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="5f797-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="5f797-124">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="5f797-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="5f797-125">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="5f797-125">Display name</span></span> | <span data-ttu-id="5f797-126">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="5f797-126">Property name</span></span> | <span data-ttu-id="5f797-127">Opis</span><span class="sxs-lookup"><span data-stu-id="5f797-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f797-128">Liczba *</span><span class="sxs-lookup"><span data-stu-id="5f797-128">Count*</span></span> |<span data-ttu-id="5f797-129">Liczba</span><span class="sxs-lookup"><span data-stu-id="5f797-129">count</span></span> |<span data-ttu-id="5f797-130">Liczba Hello toodelay jednostki czasu</span><span class="sxs-lookup"><span data-stu-id="5f797-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="5f797-131">Jednostka *</span><span class="sxs-lookup"><span data-stu-id="5f797-131">Unit*</span></span> |<span data-ttu-id="5f797-132">jednostki</span><span class="sxs-lookup"><span data-stu-id="5f797-132">unit</span></span> |<span data-ttu-id="5f797-133">Jednostka czasu Hello: `Second`, `Minute`, `Hour`, lub`Day`</span><span class="sxs-lookup"><span data-stu-id="5f797-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="5f797-134">Opóźnienie — do akcji</span><span class="sxs-lookup"><span data-stu-id="5f797-134">Delay-until action</span></span>
<span data-ttu-id="5f797-135">Ta akcja opóźnia hello uruchomić do określonej daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="5f797-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="5f797-136">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="5f797-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="5f797-137">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="5f797-137">Display name</span></span> | <span data-ttu-id="5f797-138">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="5f797-138">Property name</span></span> | <span data-ttu-id="5f797-139">Opis</span><span class="sxs-lookup"><span data-stu-id="5f797-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f797-140">Rok *</span><span class="sxs-lookup"><span data-stu-id="5f797-140">Year*</span></span> |<span data-ttu-id="5f797-141">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="5f797-141">timestamp</span></span> |<span data-ttu-id="5f797-142">Witaj toodelay roku do (GMT)</span><span class="sxs-lookup"><span data-stu-id="5f797-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="5f797-143">Miesiąc *</span><span class="sxs-lookup"><span data-stu-id="5f797-143">Month*</span></span> |<span data-ttu-id="5f797-144">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="5f797-144">timestamp</span></span> |<span data-ttu-id="5f797-145">Witaj toodelay miesiąc aż do (GMT)</span><span class="sxs-lookup"><span data-stu-id="5f797-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="5f797-146">Dzień *</span><span class="sxs-lookup"><span data-stu-id="5f797-146">Day*</span></span> |<span data-ttu-id="5f797-147">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="5f797-147">timestamp</span></span> |<span data-ttu-id="5f797-148">Witaj toodelay dzień do (GMT)</span><span class="sxs-lookup"><span data-stu-id="5f797-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="5f797-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f797-149">Next steps</span></span>
<span data-ttu-id="5f797-150">Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5f797-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5f797-151">Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5f797-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

