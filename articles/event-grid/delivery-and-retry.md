---
title: "aaaAzure dostarczania zdarzeń siatki i spróbuj ponownie"
description: "Opisuje sposób siatki zdarzeń Azure zapewnia zdarzeń i sposób obsługi niedostarczone wiadomości."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="b387b-103">Dostarczanie komunikatów siatki zdarzeń i spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="b387b-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="b387b-104">W tym artykule opisano, jak siatki zdarzeń Azure obsługuje zdarzenia podczas dostarczania nie zostaje potwierdzony.</span><span class="sxs-lookup"><span data-stu-id="b387b-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="b387b-105">Zdarzenie siatki udostępnia trwałe dostarczania.</span><span class="sxs-lookup"><span data-stu-id="b387b-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="b387b-106">Zapewnia każdy komunikat co najmniej raz dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b387b-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="b387b-107">Zdarzenia są wysyłane bezpośrednio webhook toohello zarejestrowany każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b387b-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="b387b-108">Elementu webhook nie otrzymanie zdarzenia w ciągu 60 sekund hello pierwszej dostawy podejmować, dostarczania zdarzeń hello ponowi próbę zdarzeń siatki.</span><span class="sxs-lookup"><span data-stu-id="b387b-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="b387b-109">Stan dostarczania wiadomości</span><span class="sxs-lookup"><span data-stu-id="b387b-109">Message delivery status</span></span>

<span data-ttu-id="b387b-110">Siatka zdarzeń używa potwierdzenie dostarczenia tooacknowledge kody odpowiedzi HTTP zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b387b-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="b387b-111">Kody operacji zakończonych powodzeniem</span><span class="sxs-lookup"><span data-stu-id="b387b-111">Success codes</span></span>

<span data-ttu-id="b387b-112">Hello następujące kody odpowiedzi HTTP wskazać, że zdarzenie została dostarczona pomyślnie tooyour elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="b387b-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="b387b-113">Zdarzenie siatki uwzględnia pełną dostarczania.</span><span class="sxs-lookup"><span data-stu-id="b387b-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="b387b-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="b387b-114">200 OK</span></span>
- <span data-ttu-id="b387b-115">202 zaakceptowane</span><span class="sxs-lookup"><span data-stu-id="b387b-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="b387b-116">Kod błędów</span><span class="sxs-lookup"><span data-stu-id="b387b-116">Failure codes</span></span>

<span data-ttu-id="b387b-117">następujące kody odpowiedzi HTTP Hello wskazują, że próba dostarczania zdarzeń nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="b387b-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="b387b-118">Siatka zdarzeń próbuje ponownie toosend hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b387b-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="b387b-119">400 Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="b387b-119">400 Bad Request</span></span>
- <span data-ttu-id="b387b-120">401 nieautoryzowane</span><span class="sxs-lookup"><span data-stu-id="b387b-120">401 Unauthorized</span></span>
- <span data-ttu-id="b387b-121">404 — Nie odnaleziono</span><span class="sxs-lookup"><span data-stu-id="b387b-121">404 Not Found</span></span>
- <span data-ttu-id="b387b-122">408 Limit czasu żądania</span><span class="sxs-lookup"><span data-stu-id="b387b-122">408 Request timeout</span></span>
- <span data-ttu-id="b387b-123">Identyfikator URI 414 zbyt długa</span><span class="sxs-lookup"><span data-stu-id="b387b-123">414 URI Too Long</span></span>
- <span data-ttu-id="b387b-124">500 Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="b387b-124">500 Internal Server Error</span></span>
- <span data-ttu-id="b387b-125">503 Usługa jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="b387b-125">503 Service Unavailable</span></span>
- <span data-ttu-id="b387b-126">Limit czasu bramy 504</span><span class="sxs-lookup"><span data-stu-id="b387b-126">504 Gateway Timeout</span></span>

<span data-ttu-id="b387b-127">Każdy kod odpowiedzi lub brak odpowiedzi oznacza błąd.</span><span class="sxs-lookup"><span data-stu-id="b387b-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="b387b-128">Zdarzenie siatki ponownych prób dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="b387b-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="b387b-129">Interwały ponawiania</span><span class="sxs-lookup"><span data-stu-id="b387b-129">Retry intervals</span></span>

<span data-ttu-id="b387b-130">Siatka zdarzeń używa zasady ponawiania wykładniczego wycofywania w celu dostarczania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b387b-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="b387b-131">Jeśli Twoje elementu webhook nie odpowiada, zwraca kod błędu siatki zdarzeń ponownych prób dostarczenia na powitania według harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="b387b-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="b387b-132">10 sekund</span><span class="sxs-lookup"><span data-stu-id="b387b-132">10 seconds</span></span>
2. <span data-ttu-id="b387b-133">30 sekund</span><span class="sxs-lookup"><span data-stu-id="b387b-133">30 seconds</span></span>
3. <span data-ttu-id="b387b-134">1 minuta</span><span class="sxs-lookup"><span data-stu-id="b387b-134">1 minute</span></span>
4. <span data-ttu-id="b387b-135">5 minut</span><span class="sxs-lookup"><span data-stu-id="b387b-135">5 minutes</span></span>
5. <span data-ttu-id="b387b-136">10 minut</span><span class="sxs-lookup"><span data-stu-id="b387b-136">10 minutes</span></span>
6. <span data-ttu-id="b387b-137">30 minut</span><span class="sxs-lookup"><span data-stu-id="b387b-137">30 minutes</span></span>
7. <span data-ttu-id="b387b-138">1 godzina</span><span class="sxs-lookup"><span data-stu-id="b387b-138">1 hour</span></span>

<span data-ttu-id="b387b-139">Siatka zdarzenie dodaje interwał ponawiania tooall małe losowe.</span><span class="sxs-lookup"><span data-stu-id="b387b-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="b387b-140">Spróbuj ponownie czas trwania</span><span class="sxs-lookup"><span data-stu-id="b387b-140">Retry duration</span></span>

<span data-ttu-id="b387b-141">Witaj wersji zapoznawczej siatki zdarzeń Azure wygasa wszystkie zdarzenia, które nie zostały dostarczone w ciągu dwóch godzin.</span><span class="sxs-lookup"><span data-stu-id="b387b-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="b387b-142">Przed ogólnej dostępności to zostanie zwiększona too24 godzin.</span><span class="sxs-lookup"><span data-stu-id="b387b-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b387b-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b387b-143">Next steps</span></span>

* <span data-ttu-id="b387b-144">Aby tooEvent wprowadzenie siatki, zobacz [o siatki zdarzeń](overview.md).</span><span class="sxs-lookup"><span data-stu-id="b387b-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="b387b-145">tooquickly rozpocząć korzystanie z siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="b387b-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
