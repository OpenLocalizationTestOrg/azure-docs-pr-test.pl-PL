---
title: "Przegląd zdarzeń siatki aaaAzure"
description: "Opisuje Azure zdarzeń siatki i jego pojęcia."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Wprowadzenie tooAzure siatki zdarzeń

Azure siatki zdarzeń umożliwia tooeasily kompilacji aplikacji za pomocą architektury oparty na zdarzeniach. Możesz wybrać hello zasobów platformy Azure chcesz toosubscribe do i program obsługi zdarzeń hello lub elementu WebHook punktu końcowego toosend hello zdarzenia. Siatka zdarzeń ma wbudowaną obsługę zdarzenia pochodzące z usług Azure, takich jak magazynu obiektów blob i grup zasobów. Siatka zdarzeń ma również obsługę niestandardowych aplikacji i innych zdarzeń, przy użyciu niestandardowych tematów i niestandardowych elementów webhook. 

Można użyć filtrów tooroute określonych zdarzeń toodifferent punkty końcowe multiemisji toomultiple punktów końcowych i upewnij się, że niezawodnie dostarczania zdarzeń. Siatki zdarzeń również ma wbudowaną obsługą dla firm i niestandardowych zdarzeń.

Dla wersji zapoznawczej hello obsługuje zdarzenia siatki **westus2** i **westcentralus** lokalizacji. Zostanie dodany innych regionów.

Ten artykuł zawiera omówienie Azure zdarzeń siatki. Tooget wprowadzenie siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).

![Model funkcjonalności siatki zdarzeń](./media/overview/event-grid-functional-model.png)

Magazyn obiektów Blob nie jest obecnie publicznie dostępna jako wydawca.

## <a name="concepts"></a>Pojęcia

Istnieje pięć pojęcia w siatce zdarzeń platformy Azure, które umożliwiają zacząć:

* **Zdarzenia** -co się stało.
* **Wydawcy źródeł zdarzeń** — w przypadku, gdy zdarzenie hello miało miejsce.
* **Tematy** — Witaj punktu końcowego, gdzie wydawców wysłać zdarzenia.
* **Subskrypcja zdarzeń** -hello punktu końcowego lub wbudowany mechanizm tooroute zdarzeń, a czasami toomultiple obsługi. Subskrypcje są również używane przez programy obsługi zdarzenia przychodzące filtru toointelligently.
* **Programy obsługi zdarzeń** — Witaj aplikacji lub usługi dające dodatnią reakcję toohello zdarzeń.

Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [pojęcia w siatce zdarzeń Azure](concepts.md).

## <a name="capabilities"></a>Możliwości

Oto niektóre najważniejsze funkcje hello Azure siatki zdarzeń:

* **Prostota** -zdarzenia tooaim punktu i kliknij przycisk z obsługi zdarzeń tooany zasobów platformy Azure lub punktu końcowego.
* **Zaawansowane filtrowanie** -filtr na zdarzenie typu lub zdarzenia publikowania tooensure ścieżka procedury obsługi zdarzeń odbierać istotne zdarzenia.
* **Rozdysponowywania** -wiele punktów końcowych toohello subskrypcji tego samego zdarzenia toosend kopie tooas zdarzeń hello wielu miejscach zgodnie z potrzebami.
* **Niezawodność** — korzystanie z 24-godzinnym ponownie za pomocą tooensure wykładniczego wycofywania zdarzenia są dostarczane.
* **Płatności na zdarzenie** — płać tylko dla kwoty hello Użyj siatki zdarzeń.
* **Wysokiej przepływności** — Tworzenie dużych obciążeń w siatce zdarzeń z obsługą miliony zdarzeń na sekundę.
* **Wbudowane zdarzenia** — Uzyskaj i szybko uruchomić zdefiniowany zasób wbudowanych zdarzenia.
* **Niestandardowe zdarzenia** -Użyj siatki zdarzeń trasy, filtr i niezawodnie dostarczyć zdarzeń niestandardowych w aplikacji.

## <a name="built-in-publisher-and-handler-integration"></a>Wbudowane funkcje integracji wydawcy i obsługi

Azure oferuje obsługę wbudowanych zdarzeń przy użyciu wielu usług, w tym zarówno i obsługi.

### <a name="publishers"></a>Wydawcy

Obecnie hello następujących usług platformy Azure są wbudowane wydawcy obsługę zdarzeń siatki:

* Grupy zasobów (operacje zarządzania)
* Subskrypcje platformy Azure (operacje zarządzania)
* Usługa Event Hubs
* Niestandardowe — tematy

Innymi usługami Azure zostaną dodane tego roku.

### <a name="handlers"></a>Programy obsługi

Obecnie hello następujących usług platformy Azure są wbudowana obsługa siatki zdarzeń: 

* Stan usługi Funkcje Azure
* Logic Apps
* Azure Automation
* Elementów Webhook

Innymi usługami Azure zostaną dodane tego roku.

## <a name="what-can-i-do-with-event-grid"></a>Co można zrobić siatki zdarzenia?

Siatki zdarzeń Azure oferuje kilka możliwości, które znacząco poprawić niekorzystającą, ops automatyzacji i pracy integracji: 

### <a name="serverless-application-architectures"></a>Architektury aplikacji bez użycia serwera

![Aplikację niekorzystającą](./media/overview/serverless_web_app.png)

Usługa Event Grid łączy źródła danych i programy obsługi zdarzeń. Na przykład użyć wyzwalacza tooinstantly siatki zdarzeń niekorzystającą funkcja analizy obrazu toorun każdym razem, gdy jest nowe zdjęcie dodać kontener magazynu obiektów blob tooa. 

### <a name="ops-automation"></a>Automatyzacja OPS

![Automatyzacja operacji](./media/overview/Ops_automation.png)

Siatka zdarzeń umożliwia automatyzację toospeed i uprościć wymuszanie zasad. Przykładowo usługa Event Grid może powiadamiać usługę Azure Automation, gdy maszyna wirtualna zostanie utworzona lub usługa SQL Database zostanie rozszerzona. Zdarzenia te mogą służyć tooautomatically Sprawdź, czy konfiguracja usługi są zgodne, poddane metadanych narzędzia operacje, tag maszyn wirtualnych lub pliku elementów roboczych.

### <a name="application-integration"></a>Integracja aplikacji

![Integracja aplikacji](./media/overview/app_integration.png)

Usługa Event Grid łączy aplikację z innymi usługami. Na przykład utworzyć toosend niestandardowego tematu tooEvent danych zdarzeń aplikacji siatki i wykorzystać jej wiarygodnych dostarczania zaawansowane routingu i bezpośrednia Integracja z platformą Azure. Alternatywnie można użyć siatki zdarzeń z dane tooprocess Logic Apps w dowolnym miejscu, bez pisania kodu. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Czym różni się siatki zdarzeń od innych usług integracji Azure?

Siatka zdarzeń jest płyty montażowej obsługi zdarzeń, która umożliwia programowanie sterowane zdarzeniami, reaktywne. Jest ściśle zintegrowana z usługami Azure, a może być zintegrowana z usługami innych firm. wiadomości powitania zdarzenia zawiera informacje hello potrzebne toochanges tooreact w usług i aplikacji. Siatka zdarzeń nie jest potoku danych i nie dostarcza hello rzeczywistego obiektu, który został zaktualizowany.

Usługa Service Bus jest odpowiednia dla przedsiębiorstwa tradycyjnej aplikacji, które wymagają transakcji, porządkowanie, wykrywania duplikatów i natychmiastowe spójności. Siatka zdarzeń jest pod kątem szybkości, skala, szerokość i niedrogiej reaktywne modelu. Należy dobrze nadają się tooserverless architektury.

Zdarzenie siatki uzupełnia innymi usługami Azure, takich jak aplikacje logiki i usługi Event Hubs. Wyzwalacze zdarzeń siatki hello toobegin aplikacji logiki jego przepływu pracy. Centra zdarzeń współpracuje z siatki zdarzeń włączając tooevents tooreact przechwytywania centra zdarzeń i potoki przychodzące i przekształcania danych kompilacji.

## <a name="how-much-does-event-grid-cost"></a>Ile kosztuje siatki zdarzeń

Azure siatki zdarzeń używa modelu cenowego płatności na zdarzenie, więc płacisz tylko za można użyć.

Zdarzenia siatki koszty: 0,60 $ operacje milionów ($0.30 wersji zapoznawczej) i mogą hello pierwszych 100 000 operacji w ciągu miesiąca. Operacje są definiowane jako zdarzeń wejściowych, zaawansowane dopasowania, próba dostarczania i zarządzania wywołania.  Więcej informacji można znaleźć na powitania [cennikiem](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Następne kroki

* [Tworzyć i subskrybować zdarzenia toocustom](custom-event-quickstart.md) od razu i Rozpocznij wysyłanie własnych punktu końcowego tooany zdarzeń niestandardowych za pomocą hello Azure zdarzeń siatki — Szybki Start.
* [Przy użyciu logiki aplikacji jako program obsługi zdarzeń](monitor-virtual-machine-changes-event-grid-logic-app.md) samouczek dotyczący tworzenia aplikacji za pomocą tooevents tooreact Logic Apps wypychana przez zdarzenie siatki.
* [Dokumentacja interfejsu API REST siatki zdarzeń](/rest/api/eventgrid)  
  Zawiera więcej informacji technicznych dotyczących hello Azure zdarzeń siatki i odwołanie zarządzania subskrypcji zdarzeń routingu i filtrowania.
