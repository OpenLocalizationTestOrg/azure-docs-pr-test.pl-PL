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
# <a name="event-grid-message-delivery-and-retry"></a>Dostarczanie komunikatów siatki zdarzeń i spróbuj ponownie 

W tym artykule opisano, jak siatki zdarzeń Azure obsługuje zdarzenia podczas dostarczania nie zostaje potwierdzony.

Zdarzenie siatki udostępnia trwałe dostarczania. Zapewnia każdy komunikat co najmniej raz dla każdej subskrypcji. Zdarzenia są wysyłane bezpośrednio webhook toohello zarejestrowany każdej subskrypcji. Elementu webhook nie otrzymanie zdarzenia w ciągu 60 sekund hello pierwszej dostawy podejmować, dostarczania zdarzeń hello ponowi próbę zdarzeń siatki.

## <a name="message-delivery-status"></a>Stan dostarczania wiadomości

Siatka zdarzeń używa potwierdzenie dostarczenia tooacknowledge kody odpowiedzi HTTP zdarzeń. 

### <a name="success-codes"></a>Kody operacji zakończonych powodzeniem

Hello następujące kody odpowiedzi HTTP wskazać, że zdarzenie została dostarczona pomyślnie tooyour elementu webhook. Zdarzenie siatki uwzględnia pełną dostarczania.

- 200 OK
- 202 zaakceptowane

### <a name="failure-codes"></a>Kod błędów

następujące kody odpowiedzi HTTP Hello wskazują, że próba dostarczania zdarzeń nie powiodła się. Siatka zdarzeń próbuje ponownie toosend hello zdarzeń. 

- 400 Niewłaściwe żądanie
- 401 nieautoryzowane
- 404 — Nie odnaleziono
- 408 Limit czasu żądania
- Identyfikator URI 414 zbyt długa
- 500 Wewnętrzny błąd serwera
- 503 Usługa jest niedostępna
- Limit czasu bramy 504

Każdy kod odpowiedzi lub brak odpowiedzi oznacza błąd. Zdarzenie siatki ponownych prób dostarczenia. 

## <a name="retry-intervals"></a>Interwały ponawiania

Siatka zdarzeń używa zasady ponawiania wykładniczego wycofywania w celu dostarczania zdarzeń. Jeśli Twoje elementu webhook nie odpowiada, zwraca kod błędu siatki zdarzeń ponownych prób dostarczenia na powitania według harmonogramu:

1. 10 sekund
2. 30 sekund
3. 1 minuta
4. 5 minut
5. 10 minut
6. 30 minut
7. 1 godzina

Siatka zdarzenie dodaje interwał ponawiania tooall małe losowe.

## <a name="retry-duration"></a>Spróbuj ponownie czas trwania

Witaj wersji zapoznawczej siatki zdarzeń Azure wygasa wszystkie zdarzenia, które nie zostały dostarczone w ciągu dwóch godzin. Przed ogólnej dostępności to zostanie zwiększona too24 godzin. 

## <a name="next-steps"></a>Następne kroki

* Aby tooEvent wprowadzenie siatki, zobacz [o siatki zdarzeń](overview.md).
* tooquickly rozpocząć korzystanie z siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).
