---
title: "aaaWhat to Azure Event Hubs i dlaczego warto jej używać | Dokumentacja firmy Microsoft"
description: "Omówienie i wprowadzenie tooAzure usługi Event Hubs — wprowadzanie danych telemetrycznych skali chmury z witryn sieci Web, aplikacji i urządzeń"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>Co to jest usługa Event Hubs?

Azure Event Hubs to wysoce skalowalna platforma do pobierania zdarzeń i strumieniowego przesyłania danych, która umożliwia odbieranie i przetwarzanie milionów zdarzeń na sekundę. Usługa Event Hubs pozwala przetwarzać i przechowywać zdarzenia, dane lub dane telemetryczne generowane przez rozproszone oprogramowanie i urządzenia. Dane wysyłane tooan Centrum zdarzeń można je przekształcać i przechowywać za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub kart przetwarzania wsadowego i magazynowania. Z hello możliwości tooprovide [możliwości publikowania / subskrypcji](https://msdn.microsoft.com/library/aa560414.aspx) z małych opóźnień i bardzo dużej skali, usługa Event Hubs służy jako hello "na narastania" dla danych Big Data.

## <a name="why-use-event-hubs"></a>Dlaczego warto korzystać z usługi Event Hubs?

Możliwości obsługi zdarzeń i telemetrii w usłudze Event Hubs czynią ją szczególnie użyteczną do:

* instrumentacji aplikacji
* przetwarzania czynności użytkownika lub przepływów pracy
* scenariuszy Internetu rzeczy (IoT)

Usługa Event Hubs umożliwia na przykład śledzenie zachowania w aplikacjach mobilnych, gromadzenie informacji o ruchu z farmy serwerów w Internecie, przechwytywanie zdarzeń w grach na konsole i zbieranie danych telemetrycznych z maszyn przemysłowych, podłączonych pojazdów lub innych urządzeń.

## <a name="azure-event-hubs-overview"></a>Omówienie usługi Azure Event Hubs

Witaj typową rolą usługi Event hubs w architekturze rozwiązań jest hello "drzwi wejściowe" dla potoku zdarzeń, często nazywane *systemem zbierania zdarzeń*. Systemem zbierania zdarzeń to składnik lub usługa, która znajduje się między wydawcami zdarzeń, a zdarzenie konsumentów toodecouple hello Wytwarzanie strumienia zdarzeń od użycia tych zdarzeń hello. Witaj poniższym rysunku przedstawiono tej architektury:

![Usługa Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Usługa Event Hubs umożliwia obsługę strumienia komunikatów, ale jej właściwości różnią się od tradycyjnych metod przesyłania komunikatów w przedsiębiorstwie. Możliwości usługi Event Hubs są zbudowane wokół scenariuszy wysokiej przepływności i przetwarzania zdarzeń. W efekcie Usługa Event Hubs różni się od [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) wiadomości, a nie implementuje niektórych możliwości hello, które są dostępne dla [komunikatów usługi Service Bus](/azure/service-bus-messaging/) jednostki, na przykład tematów.

## <a name="event-hubs-features"></a>Funkcje usługi Event Hubs

Centra zdarzeń zawiera następujące kluczowe elementy hello:

- [**Wydawcy producentów zdarzeń**](event-hubs-features.md#event-publishers): jednostki, która wysyła Centrum zdarzeń tooan danych. Zdarzenia są publikowane za pośrednictwem protokołu AMQP 1.0 lub HTTPS.
- [**Przechwyć**](event-hubs-features.md#capture): umożliwia toocapture Event Hubs strumieniowego przesyłania danych i zapisze go na koncie magazynu obiektów Blob platformy Azure.
- [**Partycje**](event-hubs-features.md#partitions): włącza tooonly każdego konsumenta odczyt konkretny podzbiór, lub partycję, hello strumienia zdarzeń.
- [**Tokeny sygnatury dostępu Współdzielonego**](event-hubs-features.md#sas-tokens): identyfikuje i uwierzytelnia hello wydawca zdarzeń.
- [**Odbiorca zdarzenia**](event-hubs-features.md#event-consumers): jednostka, która odczytuje dane zdarzenia z centrum zdarzeń. Odbiorcy zdarzenia nawiązują połączenia za pomocą protokołu AMQP 1.0. 
- [**Grupy konsumentów**](event-hubs-features.md#consumer-groups): zapewnia każdego wielu korzystanie z aplikacji przy użyciu osobny widok strumienia zdarzeń hello, włączanie tych tooact konsumentów niezależnie.
- [**Jednostki przepływności**](event-hubs-features.md#capacity): zakupione wcześniej jednostki wydajności. Jedna partycja ma maksymalną skalę wynoszącą jedną jednostkę przepływności.

Aby uzyskać szczegółowe informacje techniczne na temat tych i innych funkcji usługi Event Hubs, zobacz hello [Przegląd funkcji usługi Event Hubs](event-hubs-features.md). 

## <a name="next-steps"></a>Następne kroki

Aby uzyskać szczegółowe informacje o cenach za korzystanie z usługi Event Hubs, zobacz [Usługa Event Hubs — cennik](https://azure.microsoft.com/pricing/details/event-hubs/).

Aby uzyskać więcej informacji na temat usługi Event Hubs odwiedź hello następującego łącza:

* Rozpocznij pracę od [samouczka dotyczącego usługi Event Hubs](event-hubs-dotnet-standard-getstarted-send.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)
* [Przykładowe aplikacje korzystające z usługi Event Hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

