---
title: Dodaj wyzwalacza cyklu w aplikacjach logiki | Dokumentacja firmy Microsoft
description: "Przegląd cyklu wyzwalacza i jak z niego korzystać z aplikacji logiki platformy Azure."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="28e04-103">Rozpoczynanie pracy z wyzwalaczem cyklu</span><span class="sxs-lookup"><span data-stu-id="28e04-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="28e04-104">Przy użyciu wyzwalacza cyklu, można tworzyć rozbudowane przepływy pracy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="28e04-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="28e04-105">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="28e04-105">For example, you can:</span></span>

* <span data-ttu-id="28e04-106">Planowanie przepływu pracy do uruchomienia codziennie procedury składowane SQL.</span><span class="sxs-lookup"><span data-stu-id="28e04-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="28e04-107">Wyślij wiadomość e-mail podsumowanie wszystkich tweetów w ostatnim tygodniu o niektórych hasztagiem.</span><span class="sxs-lookup"><span data-stu-id="28e04-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="28e04-108">Aby rozpocząć korzystanie z wyzwalacza cyklu w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="28e04-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="28e04-109">Użyj wyzwalacz cyklu</span><span class="sxs-lookup"><span data-stu-id="28e04-109">Use a recurrence trigger</span></span>
<span data-ttu-id="28e04-110">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy, który jest zdefiniowany w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="28e04-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="28e04-111">[Dowiedz się więcej o wyzwalaczy](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28e04-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="28e04-112">Oto przykład sekwencji sposobu konfigurowania wyzwalacz cyklu w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="28e04-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="28e04-113">Dodaj **cyklu** wyzwalacza jako pierwszy krok w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="28e04-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="28e04-114">Wprowadź interwał cyklu w parametrach.</span><span class="sxs-lookup"><span data-stu-id="28e04-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="28e04-115">Uruchomieniu aplikacji logiki teraz uruchamianie po każdym interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="28e04-115">The logic app now starts a run after each interval of time.</span></span>

![Wyzwalacz HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="28e04-117">Szczegóły wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="28e04-117">Trigger details</span></span>
<span data-ttu-id="28e04-118">Wyzwalacz cyklu ma następujące właściwości, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="28e04-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="28e04-119">Generowane aplikacji logiki, po upływie czasu określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="28e04-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="28e04-120">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="28e04-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="28e04-121">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="28e04-121">Display name</span></span> | <span data-ttu-id="28e04-122">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="28e04-122">Property name</span></span> | <span data-ttu-id="28e04-123">Opis</span><span class="sxs-lookup"><span data-stu-id="28e04-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28e04-124">Częstotliwość *</span><span class="sxs-lookup"><span data-stu-id="28e04-124">Frequency*</span></span> |<span data-ttu-id="28e04-125">częstotliwość</span><span class="sxs-lookup"><span data-stu-id="28e04-125">frequency</span></span> |<span data-ttu-id="28e04-126">Jednostka czasu: `Second`, `Minute`, `Hour`, `Day`, lub `Year`.</span><span class="sxs-lookup"><span data-stu-id="28e04-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="28e04-127">Interwał *</span><span class="sxs-lookup"><span data-stu-id="28e04-127">Interval*</span></span> |<span data-ttu-id="28e04-128">Interwał</span><span class="sxs-lookup"><span data-stu-id="28e04-128">interval</span></span> |<span data-ttu-id="28e04-129">Interwał częstotliwości danego cyklu.</span><span class="sxs-lookup"><span data-stu-id="28e04-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="28e04-130">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="28e04-130">Time Zone</span></span> |<span data-ttu-id="28e04-131">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="28e04-131">timeZone</span></span> |<span data-ttu-id="28e04-132">Jeśli godzina rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, będą używane tej strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="28e04-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="28e04-133">Godzina rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="28e04-133">Start time</span></span> |<span data-ttu-id="28e04-134">startTime</span><span class="sxs-lookup"><span data-stu-id="28e04-134">startTime</span></span> |<span data-ttu-id="28e04-135">Czas rozpoczęcia w [formacie ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="28e04-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="28e04-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28e04-136">Next steps</span></span>
<span data-ttu-id="28e04-137">Teraz, wypróbuj platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="28e04-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="28e04-138">Dostępne łączniki w aplikacjach logiki można eksplorować analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="28e04-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

