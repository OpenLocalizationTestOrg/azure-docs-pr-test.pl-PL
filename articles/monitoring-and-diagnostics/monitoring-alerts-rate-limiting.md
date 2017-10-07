---
title: "Ograniczanie aaaRate dla programu SMS, wiadomości e-mail i elementów webhook | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure ogranicza liczbę hello możliwe powiadomień programu SMS, wiadomości e-mail lub elementu webhook z grupy akcji."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="18370-103">Oceń ograniczenie dla elementu webhook, wiadomości e-mail i wiadomości SMS wpisów</span><span class="sxs-lookup"><span data-stu-id="18370-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="18370-104">Limitów szybkości jest zawieszenie powiadomienia, gdy zbyt wiele powiadomienia są wysyłane tooa określonego numeru telefonu lub poczty e-mail adresu.</span><span class="sxs-lookup"><span data-stu-id="18370-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="18370-105">Limitów szybkości zapewnia, że alerty są łatwe w zarządzaniu i możliwością wykonania akcji.</span><span class="sxs-lookup"><span data-stu-id="18370-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="18370-106">Hello reguł dla programu SMS i wiadomości e-mail są hello takie same.</span><span class="sxs-lookup"><span data-stu-id="18370-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="18370-107">Próg limitu szybkości Hello jest:</span><span class="sxs-lookup"><span data-stu-id="18370-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="18370-108">**SMS**: 10 wiadomości w ciągu godziny.</span><span class="sxs-lookup"><span data-stu-id="18370-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="18370-109">**Wiadomości e-mail**: 100 wiadomości w ciągu godziny.</span><span class="sxs-lookup"><span data-stu-id="18370-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="18370-110">Reguły limit szybkości</span><span class="sxs-lookup"><span data-stu-id="18370-110">Rate limit rules</span></span>
- <span data-ttu-id="18370-111">Numer telefonu lub adres e-mail jest szybkość ograniczone, gdy odbiera komunikaty, niż pozwala program hello próg.</span><span class="sxs-lookup"><span data-stu-id="18370-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="18370-112">Numer telefonu lub adres e-mail może być częścią grupy akcji na wiele subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="18370-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="18370-113">Stosuje limitów szybkości dla wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="18370-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="18370-114">Ma to zastosowanie zaraz po osiągnięciu progu hello, nawet jeśli komunikaty są wysyłane z wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="18370-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="18370-115">Jeśli numer telefonu lub adres e-mail jest szybkość ograniczone, dodatkowe powiadomienie jest wysyłane toocommunicate hello limitów szybkości.</span><span class="sxs-lookup"><span data-stu-id="18370-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="18370-116">Witaj powiadomienie o Państwa hello szybkości ogranicza wygasa.</span><span class="sxs-lookup"><span data-stu-id="18370-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="18370-117">Limit szybkości elementów webhook</span><span class="sxs-lookup"><span data-stu-id="18370-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="18370-118">Brak nie szybkość ograniczenia w przypadku elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="18370-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18370-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18370-119">Next steps</span></span> ##
* <span data-ttu-id="18370-120">Dowiedz się więcej o [SMS alertów zachowanie](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="18370-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="18370-121">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i Dowiedz się, jak tooreceive alertów.</span><span class="sxs-lookup"><span data-stu-id="18370-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="18370-122">Dowiedz się, jak za[skonfigurować alerty, gdy powiadomienie usługi kondycji jest przesyłana](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="18370-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
