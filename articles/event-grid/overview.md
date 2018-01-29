---
title: "Omówienie usługi Azure Event siatki"
description: "Opisuje Azure zdarzeń siatki i jego pojęcia."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 12/14/2017
ms.author: babanisa
ms.openlocfilehash: e6665b3b0c6e92ed462f18dbd41d62ccd9304928
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2017
---
# <a name="an-introduction-to-azure-event-grid"></a>Wprowadzenie do usługi Azure Event siatki

Azure siatki zdarzeń umożliwia łatwe tworzenie aplikacji za pomocą architektury oparty na zdarzeniach. Należy wybrać zasobów platformy Azure, które chcesz subskrybować i przypisz program obsługi zdarzeń lub wysłać zdarzenia do punktu końcowego elementu WebHook. Siatka zdarzeń ma wbudowaną obsługę zdarzenia pochodzące z usług Azure, takich jak magazynu obiektów blob i grup zasobów. Siatka zdarzeń ma również obsługę niestandardowych aplikacji i innych zdarzeń, przy użyciu niestandardowych tematów i niestandardowych elementów webhook. 

Filtry służy do kierowania określonych zdarzeń do różnych punktów końcowych, multiemisji do wielu punktów końcowych i upewnij się, że niezawodnie dostarczania zdarzeń. Siatki zdarzeń również ma wbudowaną obsługą dla firm i niestandardowych zdarzeń.

Siatka zdarzeń obsługuje obecnie następujących regionach:

* Środkowe stany USA
*   Wschodnie stany USA
*   Wschodnie stany USA 2
*   Środkowo-zachodnie stany USA
*   Zachodnie stany USA
*   Zachodnie stany USA 2

Zostanie dodany innych regionów.

Ten artykuł zawiera omówienie Azure zdarzeń siatki. Jeśli chcesz rozpocząć pracę z siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md). Na poniższej ilustracji przedstawiono, jak siatki zdarzeń łączy wydawcy i programy obsługi, ale nie zapewnia kompleksowe opcje są obsługiwane.

![Model funkcjonalności siatki zdarzeń](./media/overview/event-grid-functional-model.png)

## <a name="event-publishers"></a>Wydawcy zdarzeń

Obecnie następujących usług platformy Azure są wbudowane wydawcy obsługę zdarzeń siatki:

* Subskrypcje platformy Azure (operacje zarządzania)
* Niestandardowe — tematy
* Usługa Event Hubs
* Grupy zasobów (operacje zarządzania)
* Obiektu Blob magazynu

Innymi usługami Azure zostaną dodane tego roku.

## <a name="event-handlers"></a>Uchwyty zdarzeń

Obecnie następujących usług platformy Azure są wbudowana obsługa siatki zdarzeń: 

* Azure Automation
* Stan usługi Funkcje Azure
* Usługa Event Hubs
* Logic Apps
* Przepływ firmy Microsoft
* Elementy webhook

Innymi usługami Azure zostaną dodane tego roku.

## <a name="concepts"></a>Pojęcia

Istnieje pięć pojęcia w siatce zdarzeń platformy Azure, które umożliwiają zacząć:

* **Zdarzenia** -co się stało.
* **Wydawcy źródeł zdarzeń** — gdy zdarzenia miały miejsce.
* **Tematy** — gdy wydawców wysyłać zdarzenia.
* **Subskrypcja zdarzeń** — punktu końcowego lub wbudowany mechanizm zdarzenia trasy, czasami do wielu obsług. Subskrypcje są również używane przez obsługę inteligentnie filtrować zdarzenia przychodzące.
* **Programy obsługi zdarzeń** -aplikacji lub usługi reagowanie na zdarzenia.

Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [pojęcia w siatce zdarzeń Azure](concepts.md).

## <a name="capabilities"></a>Możliwości

Oto niektóre z kluczowych funkcji usługi Azure siatki zdarzeń:

* **Prostota** -wskaż i kliknij do osiągnięcia zdarzenia z zasobu platformy Azure do obsługi zdarzeń lub punktu końcowego.
* **Zaawansowane filtrowanie** -filtr na zdarzenie typu lub zdarzenia publikowania ścieżka do zapewnienia obsługi zdarzeń odbierać istotne zdarzenia.
* **Rozdysponowywania** -subskrypcji wiele punktów końcowych do tego samego zdarzenia wysłać kopie zdarzenia miejscach, w razie potrzeby.
* **Niezawodność** — korzystanie z 24-godzinnym ponownie za pomocą wykładniczego wycofywania w celu zapewnienia zdarzenia są dostarczane.
* **Płatności na zdarzenie** — płać tylko dla kwoty Użyj siatki zdarzeń.
* **Wysokiej przepływności** — Tworzenie dużych obciążeń w siatce zdarzeń z obsługą miliony zdarzeń na sekundę.
* **Wbudowane zdarzenia** — Uzyskaj i szybko uruchomić zdefiniowany zasób wbudowanych zdarzenia.
* **Niestandardowe zdarzenia** -Użyj siatki zdarzeń trasy, filtr i niezawodnie dostarczyć zdarzeń niestandardowych w aplikacji.

Porównanie siatki zdarzenia, usługi Event Hubs i Service Bus, zobacz [wybór między usługami Azure, których dostarczania komunikatów](compare-messaging-services.md).

## <a name="what-can-i-do-with-event-grid"></a>Co można zrobić siatki zdarzenia?

Siatki zdarzeń Azure oferuje kilka możliwości, które znacząco poprawić niekorzystającą, ops automatyzacji i pracy integracji: 

### <a name="serverless-application-architectures"></a>Architektury aplikacji bez użycia serwera

![Aplikację niekorzystającą](./media/overview/serverless_web_app.png)

Usługa Event Grid łączy źródła danych i programy obsługi zdarzeń. Przykładowo możesz użyć usługi Event Grid, aby natychmiast wyzwalać funkcję bezserwerową i uruchamiać analizę obrazu za każdym razem, gdy do kontenera magazynu obiektów blob zostanie dodane nowe zdjęcie. 

### <a name="ops-automation"></a>Automatyzacja OPS

![Automatyzacja operacji](./media/overview/Ops_automation.png)

Usługa Event Grid umożliwia przyspieszenie automatyzacji i uproszczenie wymuszania zasad. Przykładowo usługa Event Grid może powiadamiać usługę Azure Automation, gdy maszyna wirtualna zostanie utworzona lub usługa SQL Database zostanie rozszerzona. Te zdarzenia mogą być wykorzystane do automatycznego sprawdzania, czy konfiguracje usługi są zgodne, umieszczania metadanych w narzędziach do obsługi operacji, tagowania maszyn wirtualnych lub zachowywania elementów roboczych.

### <a name="application-integration"></a>Integracja aplikacji

![Integracja aplikacji](./media/overview/app_integration.png)

Usługa Event Grid łączy aplikację z innymi usługami. Na przykład utworzyć niestandardowy temat wysyłać dane zdarzeń aplikacji siatki zdarzeń i wykorzystać jej wiarygodnych dostarczania zaawansowane routingu i bezpośrednia Integracja z platformą Azure. Ewentualnie możesz użyć usługi Event Grid oraz usługi Logic Apps, aby przetwarzać dane w dowolnym miejscu, bez pisania kodu. 

## <a name="how-much-does-event-grid-cost"></a>Ile kosztuje siatki zdarzeń

Azure siatki zdarzeń używa modelu cenowego płatności na zdarzenie, więc płacisz tylko za można użyć.

Zdarzenia siatki koszty: 0,60 $ operacje milionów ($0.30 wersji zapoznawczej) i mogą pierwszych 100 000 operacji w ciągu miesiąca. Operacje są definiowane jako zdarzeń wejściowych, zaawansowane dopasowania, próba dostarczania i zarządzania wywołania.  Więcej informacji można znaleźć w [cennikiem](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Następne kroki

* [Trasy zdarzenia obiektu Blob magazynu](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)  
  Odpowiadanie na zdarzenia magazynu obiektów blob przy użyciu siatki zdarzeń.
* [Tworzenie i subskrybowanie zdarzeń niestandardowych](custom-event-quickstart.md)  
  Przejście bezpośrednio w i rozpocząć wysyłanie zdarzeń niestandardowych do dowolnego punktu końcowego za pomocą Szybki Start Azure zdarzeń siatki.
* [Przy użyciu logiki aplikacji jako program obsługi zdarzeń](monitor-virtual-machine-changes-event-grid-logic-app.md)  
  Samouczek dotyczący tworzenia aplikacji za pomocą aplikacji logiki do reagowania na zdarzenia wypychana siatki zdarzeń.
* [Przesyłanie strumieniowe danych Big Data do magazynu danych](event-grid-event-hubs-integration.md)  
  Samouczek, który używa usługi Azure Functions do strumienia danych z usługi Event Hubs SQL Data Warehouse.
* [Dokumentacja interfejsu API REST siatki zdarzeń](/rest/api/eventgrid)  
  Zawiera więcej informacji technicznych dotyczących siatki zdarzeń platformy Azure i odwołanie do zarządzania subskrypcjami zdarzeń routingu i filtrowania.