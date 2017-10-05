---
title: "Oceń ograniczanie dla programu SMS, wiadomości e-mail i elementów webhook | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure ogranicza liczbę możliwe powiadomień programu SMS, wiadomości e-mail lub elementu webhook z grupy akcji."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="cb45f-103">Oceń ograniczenie dla elementu webhook, wiadomości e-mail i wiadomości SMS wpisów</span><span class="sxs-lookup"><span data-stu-id="cb45f-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="cb45f-104">Limitów szybkości jest zawieszenie powiadomienia, gdy zbyt wiele powiadomienia są wysyłane na adres telefonu komórkowego lub adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="cb45f-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="cb45f-105">Limitów szybkości zapewnia, że alerty są łatwe w zarządzaniu i możliwością wykonania akcji.</span><span class="sxs-lookup"><span data-stu-id="cb45f-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="cb45f-106">Zasady programu SMS i wiadomości e-mail są takie same.</span><span class="sxs-lookup"><span data-stu-id="cb45f-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="cb45f-107">Próg limitu szybkości jest:</span><span class="sxs-lookup"><span data-stu-id="cb45f-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="cb45f-108">**SMS**: 10 wiadomości w ciągu godziny.</span><span class="sxs-lookup"><span data-stu-id="cb45f-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="cb45f-109">**Wiadomości e-mail**: 100 wiadomości w ciągu godziny.</span><span class="sxs-lookup"><span data-stu-id="cb45f-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="cb45f-110">Reguły limit szybkości</span><span class="sxs-lookup"><span data-stu-id="cb45f-110">Rate limit rules</span></span>
- <span data-ttu-id="cb45f-111">Numer telefonu lub adres e-mail jest szybkość ograniczone, gdy odbiera komunikaty więcej niż próg.</span><span class="sxs-lookup"><span data-stu-id="cb45f-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="cb45f-112">Numer telefonu lub adres e-mail może być częścią grupy akcji na wiele subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cb45f-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="cb45f-113">Stosuje limitów szybkości dla wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cb45f-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="cb45f-114">Ma to zastosowanie zaraz po osiągnięciu progu, nawet jeśli komunikaty są wysyłane z wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="cb45f-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="cb45f-115">Jeśli numer telefonu lub adres e-mail jest szybkość ograniczone, dodatkowe powiadomienie jest wysyłane do komunikowania się limitów szybkości.</span><span class="sxs-lookup"><span data-stu-id="cb45f-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="cb45f-116">Stany powiadomienie po wygaśnięciu limitów szybkości.</span><span class="sxs-lookup"><span data-stu-id="cb45f-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="cb45f-117">Limit szybkości elementów webhook</span><span class="sxs-lookup"><span data-stu-id="cb45f-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="cb45f-118">Brak nie szybkość ograniczenia w przypadku elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="cb45f-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb45f-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb45f-119">Next steps</span></span> ##
* <span data-ttu-id="cb45f-120">Dowiedz się więcej o [SMS alertów zachowanie](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cb45f-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="cb45f-121">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i dowiedzieć się, jak otrzymywać alerty.</span><span class="sxs-lookup"><span data-stu-id="cb45f-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="cb45f-122">Dowiedz się, jak [skonfigurować alerty, gdy powiadomienie usługi kondycji jest przesyłana](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="cb45f-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
