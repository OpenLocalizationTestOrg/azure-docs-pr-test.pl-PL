---
title: "Monitorowanie dostarczanie komunikatów Azure zdarzeń siatki"
description: "Opisuje sposób monitorowania dostarczenia komunikatów Azure zdarzeń siatki."
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 01/10/2018
ms.author: tomfitz
ms.openlocfilehash: 1552174589e91c370c3b85a9af7b5cc1106cbb90
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2018
---
# <a name="monitor-event-grid-message-delivery"></a>Monitorowanie zdarzeń siatki dostarczanie komunikatów 

W tym artykule opisano, jak korzystać z portalu, aby wyświetlić stan dostawy zdarzeń.

Zdarzenie siatki udostępnia trwałe dostarczania. Zapewnia każdy komunikat co najmniej raz dla każdej subskrypcji. Zdarzenia są wysyłane bezpośrednio do zarejestrowanych elementu webhook każdej subskrypcji. Jeśli elementu webhook nie otrzymanie zdarzenia w ciągu 60 sekund przy pierwszej próbie dostarczenia, siatki zdarzeń ponowi próbę dostarczania zdarzenia.

Informacje dotyczące dostarczania zdarzeń i ponownych prób [dostarczanie komunikatów zdarzeń siatki i ponów próbę](delivery-and-retry.md).

## <a name="delivery-metrics"></a>Metryki dostarczania

Portal zawiera wskaźniki stanu dostarczania komunikaty o zdarzeniach.

Tematy metryki są:

* **Publikowanie zakończyło się pomyślnie**: zdarzenie pomyślnie wysłane do tematu i przetwarzane przy użyciu 2xx odpowiedzi.
* **Publikowanie nie powiodło się**: zdarzeń wysyłanych do tematu, ale odrzucone z kodem błędu.
* **Niedopasowane**: zdarzenie pomyślnie opublikowane do tematu, ale nie pasuje do subskrypcji zdarzeń. Zdarzenie zostało porzucone.

W przypadku subskrypcji metryki są:

* **Powodzenie dostarczania**: zdarzenie pomyślnie dostarczone do punktu końcowego subskrypcji i odebrał odpowiedź 2xx.
* **Niepowodzenie dostarczania**: zdarzenia wysyłane do punktu końcowego dla tej subskrypcji, ale otrzymano 4xx lub 5xx odpowiedzi.
* **Ważność zdarzenia**: zdarzenie nie zostało dostarczone i zostały wysłane wszystkie ponownych prób. Zdarzenie zostało porzucone.
* **Dopasowano zdarzenia**: zdarzeń zawiera temat został uwzględniony przez subskrypcji zdarzeń.

## <a name="event-subscription-status"></a>Stan subskrypcji zdarzeń

Aby widzieć metryki dla subskrypcji zdarzeń, wyszukaj **subskrypcji siatki zdarzeń** dostępnych usług i zaznacz je.

![Wyszukaj subskrypcji zdarzeń](./media/monitor-event-delivery/select-event-subscriptions.png)

Filtruj według typu zdarzenia, subskrypcji i lokalizacji. Wybierz **metryki** subskrypcji do wyświetlenia.

![Filtr subskrypcji zdarzeń](./media/monitor-event-delivery/filter-events.png)

Wyświetl metryki zdarzenia tematu i subskrypcji.

![Wyświetlaj metryki zdarzenia](./media/monitor-event-delivery/subscription-metrics.png)

## <a name="custom-event-status"></a>Stan zdarzenia niestandardowe

Po opublikowaniu niestandardowego tematu, można wyświetlić dla niej metryki. Wybierz grupę zasobów, zawierającą tematu, a następnie wybierz temat.

![Wybierz niestandardowego tematu](./media/monitor-event-delivery/select-custom-topic.png)

Wyświetl metryki dla tematu zdarzenie niestandardowe.

![Wyświetlaj metryki zdarzenia](./media/monitor-event-delivery/custom-topic-metrics.png)

## <a name="next-steps"></a>Kolejne kroki

* Informacje dotyczące dostarczania zdarzeń i ponownych prób [dostarczanie komunikatów zdarzeń siatki i ponów próbę](delivery-and-retry.md).
* Aby obejrzeć wprowadzenie do siatki zdarzeń, zobacz [o siatki zdarzeń](overview.md).
* Aby szybko rozpocząć korzystanie z siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).
