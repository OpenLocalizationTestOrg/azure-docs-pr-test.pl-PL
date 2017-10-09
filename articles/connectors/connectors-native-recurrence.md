---
title: wyzwalacz cyklu hello aaaAdd w aplikacji logiki | Dokumentacja firmy Microsoft
description: "Omówienie hello cyklu wyzwalacza i w jaki sposób toouse go z aplikacji logiki platformy Azure."
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
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="f7594-103">Rozpoczynanie pracy z wyzwalaczem cyklu hello</span><span class="sxs-lookup"><span data-stu-id="f7594-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="f7594-104">Za pomocą wyzwalacza cyklu hello, mogą tworzyć zaawansowane przepływy pracy w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f7594-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="f7594-105">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="f7594-105">For example, you can:</span></span>

* <span data-ttu-id="f7594-106">Planowanie przepływu pracy toorun procedury składowane SQL każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="f7594-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="f7594-107">Wyślij wiadomość e-mail podsumowanie wszystkich tweetów w ciągu ostatniego tygodnia o niektórych hasztagiem hello.</span><span class="sxs-lookup"><span data-stu-id="f7594-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="f7594-108">tooget uruchomiony przy użyciu wyzwalacza cyklu hello w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7594-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="f7594-109">Użyj wyzwalacz cyklu</span><span class="sxs-lookup"><span data-stu-id="f7594-109">Use a recurrence trigger</span></span>
<span data-ttu-id="f7594-110">Wyzwalacz jest zdarzenie, które mogą być używane toostart przepływu pracy hello zdefiniowanej w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f7594-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="f7594-111">[Dowiedz się więcej o wyzwalaczy](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7594-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="f7594-112">Oto przykład sekwencji jak tooset się cykl wyzwalacz w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="f7594-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="f7594-113">Dodaj hello **cyklu** jako hello pierwszym etapem aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="f7594-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="f7594-114">Wprowadź parametry hello hello interwał cyklu.</span><span class="sxs-lookup"><span data-stu-id="f7594-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="f7594-115">Aplikacja logiki Hello uruchamia uruchamianie po każdym interwale czasu.</span><span class="sxs-lookup"><span data-stu-id="f7594-115">hello logic app now starts a run after each interval of time.</span></span>

![Wyzwalacz HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="f7594-117">Szczegóły wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="f7594-117">Trigger details</span></span>
<span data-ttu-id="f7594-118">wyzwalacz cyklu Hello ma następujące właściwości, które można skonfigurować hello.</span><span class="sxs-lookup"><span data-stu-id="f7594-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="f7594-119">Generowane aplikacji logiki, po upływie czasu określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="f7594-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="f7594-120">A * oznacza, że jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="f7594-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="f7594-121">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="f7594-121">Display name</span></span> | <span data-ttu-id="f7594-122">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="f7594-122">Property name</span></span> | <span data-ttu-id="f7594-123">Opis</span><span class="sxs-lookup"><span data-stu-id="f7594-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7594-124">Częstotliwość *</span><span class="sxs-lookup"><span data-stu-id="f7594-124">Frequency*</span></span> |<span data-ttu-id="f7594-125">frequency</span><span class="sxs-lookup"><span data-stu-id="f7594-125">frequency</span></span> |<span data-ttu-id="f7594-126">Jednostka czasu Hello: `Second`, `Minute`, `Hour`, `Day`, lub `Year`.</span><span class="sxs-lookup"><span data-stu-id="f7594-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="f7594-127">Interwał *</span><span class="sxs-lookup"><span data-stu-id="f7594-127">Interval*</span></span> |<span data-ttu-id="f7594-128">interval</span><span class="sxs-lookup"><span data-stu-id="f7594-128">interval</span></span> |<span data-ttu-id="f7594-129">Interwał powitania hello podana częstotliwość cyklu hello.</span><span class="sxs-lookup"><span data-stu-id="f7594-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="f7594-130">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="f7594-130">Time Zone</span></span> |<span data-ttu-id="f7594-131">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="f7594-131">timeZone</span></span> |<span data-ttu-id="f7594-132">Jeśli godzina rozpoczęcia jest dostarczany bez przesunięcie czasu UTC, będą używane tej strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="f7594-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="f7594-133">Godzina rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="f7594-133">Start time</span></span> |<span data-ttu-id="f7594-134">startTime</span><span class="sxs-lookup"><span data-stu-id="f7594-134">startTime</span></span> |<span data-ttu-id="f7594-135">Godzina rozpoczęcia Hello w [formacie ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="f7594-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="f7594-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7594-136">Next steps</span></span>
<span data-ttu-id="f7594-137">Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7594-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f7594-138">Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f7594-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

