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
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>Oceń ograniczenie dla elementu webhook, wiadomości e-mail i wiadomości SMS wpisów
Limitów szybkości jest zawieszenie powiadomienia, gdy zbyt wiele powiadomienia są wysyłane tooa określonego numeru telefonu lub poczty e-mail adresu. Limitów szybkości zapewnia, że alerty są łatwe w zarządzaniu i możliwością wykonania akcji.

Hello reguł dla programu SMS i wiadomości e-mail są hello takie same. Próg limitu szybkości Hello jest:

 - **SMS**: 10 wiadomości w ciągu godziny.
 - **Wiadomości e-mail**: 100 wiadomości w ciągu godziny.

## <a name="rate-limit-rules"></a>Reguły limit szybkości
- Numer telefonu lub adres e-mail jest szybkość ograniczone, gdy odbiera komunikaty, niż pozwala program hello próg.
- Numer telefonu lub adres e-mail może być częścią grupy akcji na wiele subskrypcji. Stosuje limitów szybkości dla wszystkich subskrypcji. Ma to zastosowanie zaraz po osiągnięciu progu hello, nawet jeśli komunikaty są wysyłane z wieloma subskrypcjami.  
- Jeśli numer telefonu lub adres e-mail jest szybkość ograniczone, dodatkowe powiadomienie jest wysyłane toocommunicate hello limitów szybkości. Witaj powiadomienie o Państwa hello szybkości ogranicza wygasa.

## <a name="rate-limit-of-webhooks"></a>Limit szybkości elementów webhook ##
Brak nie szybkość ograniczenia w przypadku elementów webhook.

## <a name="next-steps"></a>Następne kroki ##
* Dowiedz się więcej o [SMS alertów zachowanie](monitoring-sms-alert-behavior.md).
* Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i Dowiedz się, jak tooreceive alertów.  
* Dowiedz się, jak za[skonfigurować alerty, gdy powiadomienie usługi kondycji jest przesyłana](monitoring-activity-log-alerts-on-service-notifications.md).
