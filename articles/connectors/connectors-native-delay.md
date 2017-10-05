---
title: "Dodaj opóźnienia w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Przegląd opóźnienia i opóźnienie — do działań i jak z nich korzystać z aplikacji logiki platformy Azure."
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="a6a9f-103">Rozpoczynanie pracy z opóźnieniem i opóźnienie — do działania</span><span class="sxs-lookup"><span data-stu-id="a6a9f-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="a6a9f-104">Za pomocą opóźnienie i "opóźnienie-dopóki" akcje, ukończeniem scenariuszy przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="a6a9f-105">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="a6a9f-105">For example, you can:</span></span>

* <span data-ttu-id="a6a9f-106">Poczekaj na dzień do wysyłania aktualizacji stanu za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="a6a9f-107">Opóźnienie przepływu pracy do czasu wywołania HTTP czasu, aby zakończyć działanie przed wznawianie i pobierania wynik.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="a6a9f-108">Aby rozpocząć, korzystając z akcji opóźnienia w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a6a9f-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="a6a9f-109">Akcje opóźnienia</span><span class="sxs-lookup"><span data-stu-id="a6a9f-109">Use the delay actions</span></span>
<span data-ttu-id="a6a9f-110">Akcja jest operacja odbywa się przez przepływ pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="a6a9f-111">[Dowiedz się więcej o akcjach](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6a9f-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="a6a9f-112">Oto przykład sekwencji sposób używania opóźnienia kroku w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="a6a9f-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="a6a9f-113">Po dodaniu wyzwalacza, kliknij przycisk **nowy krok** Aby dodać akcję.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="a6a9f-114">Wyszukaj **opóźnienie** można wyświetlić akcje opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="a6a9f-115">W tym przykładzie firma Microsoft będzie wybierać **opóźnienie**.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-115">In this example, we will select **Delay**.</span></span>
   
    ![Opóźnienie akcji](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="a6a9f-117">Ukończ wszelkie właściwości akcji, aby skonfigurować opóźnienie.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Opóźnienie konfiguracji](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="a6a9f-119">Kliknij przycisk **zapisać** do publikowania i aktywować aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="a6a9f-120">Szczegóły akcji</span><span class="sxs-lookup"><span data-stu-id="a6a9f-120">Action details</span></span>
<span data-ttu-id="a6a9f-121">Wyzwalacz cyklu ma następujące właściwości, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="a6a9f-122">Opóźnienie akcji</span><span class="sxs-lookup"><span data-stu-id="a6a9f-122">Delay action</span></span>
<span data-ttu-id="a6a9f-123">Ta akcja opóźnienia uruchomienia na określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="a6a9f-124">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="a6a9f-125">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="a6a9f-125">Display name</span></span> | <span data-ttu-id="a6a9f-126">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="a6a9f-126">Property name</span></span> | <span data-ttu-id="a6a9f-127">Opis</span><span class="sxs-lookup"><span data-stu-id="a6a9f-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6a9f-128">Liczba *</span><span class="sxs-lookup"><span data-stu-id="a6a9f-128">Count*</span></span> |<span data-ttu-id="a6a9f-129">Liczba</span><span class="sxs-lookup"><span data-stu-id="a6a9f-129">count</span></span> |<span data-ttu-id="a6a9f-130">Liczba jednostek czasu opóźnienia</span><span class="sxs-lookup"><span data-stu-id="a6a9f-130">The number of time units to delay</span></span> |
| <span data-ttu-id="a6a9f-131">Jednostka *</span><span class="sxs-lookup"><span data-stu-id="a6a9f-131">Unit*</span></span> |<span data-ttu-id="a6a9f-132">jednostki</span><span class="sxs-lookup"><span data-stu-id="a6a9f-132">unit</span></span> |<span data-ttu-id="a6a9f-133">Jednostka czasu: `Second`, `Minute`, `Hour`, lub`Day`</span><span class="sxs-lookup"><span data-stu-id="a6a9f-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="a6a9f-134">Opóźnienie — do akcji</span><span class="sxs-lookup"><span data-stu-id="a6a9f-134">Delay-until action</span></span>
<span data-ttu-id="a6a9f-135">Ta akcja opóźnienia uruchomienia aż do określonej daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="a6a9f-136">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="a6a9f-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="a6a9f-137">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="a6a9f-137">Display name</span></span> | <span data-ttu-id="a6a9f-138">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="a6a9f-138">Property name</span></span> | <span data-ttu-id="a6a9f-139">Opis</span><span class="sxs-lookup"><span data-stu-id="a6a9f-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6a9f-140">Rok *</span><span class="sxs-lookup"><span data-stu-id="a6a9f-140">Year*</span></span> |<span data-ttu-id="a6a9f-141">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="a6a9f-141">timestamp</span></span> |<span data-ttu-id="a6a9f-142">Roku, aby opóźnić do (GMT)</span><span class="sxs-lookup"><span data-stu-id="a6a9f-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="a6a9f-143">Miesiąc *</span><span class="sxs-lookup"><span data-stu-id="a6a9f-143">Month*</span></span> |<span data-ttu-id="a6a9f-144">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="a6a9f-144">timestamp</span></span> |<span data-ttu-id="a6a9f-145">Miesiąc opóźnienia do (GMT)</span><span class="sxs-lookup"><span data-stu-id="a6a9f-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="a6a9f-146">Dzień *</span><span class="sxs-lookup"><span data-stu-id="a6a9f-146">Day*</span></span> |<span data-ttu-id="a6a9f-147">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="a6a9f-147">timestamp</span></span> |<span data-ttu-id="a6a9f-148">Dzień opóźnienia do (GMT)</span><span class="sxs-lookup"><span data-stu-id="a6a9f-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="a6a9f-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6a9f-149">Next steps</span></span>
<span data-ttu-id="a6a9f-150">Teraz, wypróbuj platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a6a9f-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="a6a9f-151">Dostępne łączniki w aplikacjach logiki można eksplorować analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a6a9f-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

