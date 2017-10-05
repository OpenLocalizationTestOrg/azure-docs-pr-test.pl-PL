---
title: "Azure dostarczania zdarzeń siatki i spróbuj ponownie"
description: "Opisuje sposób siatki zdarzeń Azure zapewnia zdarzeń i sposób obsługi niedostarczone wiadomości."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: e0f8afdfd84ea3c0c061459c27da285f6ae8957e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="d072a-103">Dostarczanie komunikatów siatki zdarzeń i spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="d072a-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="d072a-104">W tym artykule opisano, jak siatki zdarzeń Azure obsługuje zdarzenia podczas dostarczania nie zostaje potwierdzony.</span><span class="sxs-lookup"><span data-stu-id="d072a-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="d072a-105">Zdarzenie siatki udostępnia trwałe dostarczania.</span><span class="sxs-lookup"><span data-stu-id="d072a-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="d072a-106">Zapewnia każdy komunikat co najmniej raz dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d072a-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="d072a-107">Zdarzenia są wysyłane bezpośrednio do zarejestrowanych elementu webhook każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d072a-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="d072a-108">Jeśli elementu webhook nie otrzymanie zdarzenia w ciągu 60 sekund przy pierwszej próbie dostarczenia, siatki zdarzeń ponowi próbę dostarczania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d072a-108">If a webhook does not acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="d072a-109">Stan dostarczania wiadomości</span><span class="sxs-lookup"><span data-stu-id="d072a-109">Message delivery status</span></span>

<span data-ttu-id="d072a-110">Siatka zdarzeń używa kody odpowiedzi HTTP do otrzymanie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d072a-110">Event Grid uses HTTP response codes to acknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="d072a-111">Kody operacji zakończonych powodzeniem</span><span class="sxs-lookup"><span data-stu-id="d072a-111">Success codes</span></span>

<span data-ttu-id="d072a-112">Następujące kody odpowiedzi HTTP wskazują, że zdarzenia został pomyślnie dostarczony do Twojej elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="d072a-112">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span></span> <span data-ttu-id="d072a-113">Zdarzenie siatki uwzględnia pełną dostarczania.</span><span class="sxs-lookup"><span data-stu-id="d072a-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="d072a-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="d072a-114">200 OK</span></span>
- <span data-ttu-id="d072a-115">202 zaakceptowane</span><span class="sxs-lookup"><span data-stu-id="d072a-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="d072a-116">Kod błędów</span><span class="sxs-lookup"><span data-stu-id="d072a-116">Failure codes</span></span>

<span data-ttu-id="d072a-117">Następujące kody odpowiedzi HTTP wskazują, że próba dostarczania zdarzeń nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="d072a-117">The following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="d072a-118">Siatka zdarzeń próbuje ponownie wysłać zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d072a-118">Event Grid tries again to send the event.</span></span> 

- <span data-ttu-id="d072a-119">400 Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="d072a-119">400 Bad Request</span></span>
- <span data-ttu-id="d072a-120">401 nieautoryzowane</span><span class="sxs-lookup"><span data-stu-id="d072a-120">401 Unauthorized</span></span>
- <span data-ttu-id="d072a-121">404 — Nie odnaleziono</span><span class="sxs-lookup"><span data-stu-id="d072a-121">404 Not Found</span></span>
- <span data-ttu-id="d072a-122">408 Limit czasu żądania</span><span class="sxs-lookup"><span data-stu-id="d072a-122">408 Request timeout</span></span>
- <span data-ttu-id="d072a-123">Identyfikator URI 414 zbyt długa</span><span class="sxs-lookup"><span data-stu-id="d072a-123">414 URI Too Long</span></span>
- <span data-ttu-id="d072a-124">500 Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="d072a-124">500 Internal Server Error</span></span>
- <span data-ttu-id="d072a-125">503 Usługa jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="d072a-125">503 Service Unavailable</span></span>
- <span data-ttu-id="d072a-126">Limit czasu bramy 504</span><span class="sxs-lookup"><span data-stu-id="d072a-126">504 Gateway Timeout</span></span>

<span data-ttu-id="d072a-127">Każdy kod odpowiedzi lub brak odpowiedzi oznacza błąd.</span><span class="sxs-lookup"><span data-stu-id="d072a-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="d072a-128">Zdarzenie siatki ponownych prób dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="d072a-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="d072a-129">Interwały ponawiania</span><span class="sxs-lookup"><span data-stu-id="d072a-129">Retry intervals</span></span>

<span data-ttu-id="d072a-130">Siatka zdarzeń używa zasady ponawiania wykładniczego wycofywania w celu dostarczania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d072a-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="d072a-131">Jeśli Twoje elementu webhook nie odpowiada, zwraca kod błędu siatki zdarzeń ponowi próbę dostarczania zgodnie z harmonogramem następujące:</span><span class="sxs-lookup"><span data-stu-id="d072a-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on the following schedule:</span></span>

1. <span data-ttu-id="d072a-132">10 sekund</span><span class="sxs-lookup"><span data-stu-id="d072a-132">10 seconds</span></span>
2. <span data-ttu-id="d072a-133">30 sekund</span><span class="sxs-lookup"><span data-stu-id="d072a-133">30 seconds</span></span>
3. <span data-ttu-id="d072a-134">1 minuta</span><span class="sxs-lookup"><span data-stu-id="d072a-134">1 minute</span></span>
4. <span data-ttu-id="d072a-135">5 minut</span><span class="sxs-lookup"><span data-stu-id="d072a-135">5 minutes</span></span>
5. <span data-ttu-id="d072a-136">10 minut</span><span class="sxs-lookup"><span data-stu-id="d072a-136">10 minutes</span></span>
6. <span data-ttu-id="d072a-137">30 minut</span><span class="sxs-lookup"><span data-stu-id="d072a-137">30 minutes</span></span>
7. <span data-ttu-id="d072a-138">1 godzina</span><span class="sxs-lookup"><span data-stu-id="d072a-138">1 hour</span></span>

<span data-ttu-id="d072a-139">Siatka zdarzeń dodaje małe losowe do wszystkich interwałów ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="d072a-139">Event Grid adds a small randomization to all retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="d072a-140">Spróbuj ponownie czas trwania</span><span class="sxs-lookup"><span data-stu-id="d072a-140">Retry duration</span></span>

<span data-ttu-id="d072a-141">W wersji zapoznawczej siatki zdarzeń Azure wygasa wszystkie zdarzenia, które nie zostały dostarczone w ciągu dwóch godzin.</span><span class="sxs-lookup"><span data-stu-id="d072a-141">During the preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="d072a-142">Przed ogólnej dostępności tego czasu zostanie zwiększony do 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="d072a-142">Before General Availability, this time will be increased to 24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d072a-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d072a-143">Next steps</span></span>

* <span data-ttu-id="d072a-144">Aby obejrzeć wprowadzenie do siatki zdarzeń, zobacz [o siatki zdarzeń](overview.md).</span><span class="sxs-lookup"><span data-stu-id="d072a-144">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="d072a-145">Aby szybko rozpocząć korzystanie z siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="d072a-145">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>