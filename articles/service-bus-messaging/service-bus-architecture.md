---
title: "Przegląd architektury przetwarzania komunikatów usługi Service Bus aaaAzure | Dokumentacja firmy Microsoft"
description: "Zawiera opis architektury przetwarzania wiadomość hello Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Architektura usługi Service Bus
W tym artykule opisano architekturę przetwarzania komunikatu hello Azure Service Bus.

## <a name="service-bus-scale-units"></a>Jednostki skalowania usługi Service Bus
Usługa Service Bus jest zorganizowana według *jednostek skalowania*. Jednostką skalowania jest jednostką wdrożenia i zawiera wszystkie składniki wymagane hello Uruchom usługę. Każdy region wdraża co najmniej jedną jednostkę skalowania usługi Service Bus.

Przestrzeń nazw usługi Service Bus jest jednostką skalowania tooa mapowane. Witaj jednostka skalowania obsługuje wszystkie typy jednostek usługi Service Bus (kolejki, tematy, subskrypcje). Jednostki skalowania usługi Service Bus składa się z hello następujące składniki:

* **Zestaw węzłów bramy.** Węzły bramy uwierzytelniają żądania przychodzące. Każdy węzeł bramy ma publiczny adres IP.
* **Zestaw węzłów brokera komunikatów.** Węzły brokera komunikatów przetwarzają żądania dotyczące jednostek obsługi komunikatów.
* **Jeden magazyn bramy.** Witaj magazyn bramy przechowuje dane hello dla każdej jednostki, która jest zdefiniowana w tej jednostce skalowania. Magazyn bramy Hello jest wdrażany w oparciu o bazę danych SQL Azure.
* **Wiele magazynów obsługi komunikatów.** Usługa obsługi komunikatów przechowuje wiadomości powitania kolejki, tematy i subskrypcje, które są zdefiniowane w tej jednostce skalowania. Zawiera również wszystkie dane subskrypcji. O ile [partycjonowania jednostek obsługi komunikatów](service-bus-partitioning.md) jest włączona, kolejka lub temat jest mapowanych tooone magazynie obsługi komunikatów. Subskrypcje są przechowywane w hello samym magazynie obsługi komunikatów jako ich temat nadrzędny. Z wyjątkiem usługi Service Bus [Premium Messaging](service-bus-premium-messaging.md), magazyny obsługi komunikatów hello są wdrażane na podstawie baz danych SQL Azure.

## <a name="containers"></a>Kontenery
Każda jednostka obsługi komunikatów ma przypisany określony kontener. Kontener jest konstrukcją logiczną, który używa dokładnie jeden toostore magazynie obsługi komunikatów wszystkich odpowiednich danych dla tego kontenera. Każdy kontener jest przypisany tooa węzła brokera komunikatów. Zazwyczaj kontenerów jest więcej niż węzłów brokera obsługi komunikatów. W związku z tym każdy węzeł brokera obsługi komunikatów ładuje wiele kontenerów. Hello dystrybucja kontenerów węzeł brokera obsługi komunikatów tooa jest zorganizowana w taki sposób, że wszystkie węzły brokera obsługi komunikatów są równo obciążone. Jeśli hello hello obciążenia wzorzec zmiany (na przykład jeden z pobiera kontenery hello jest bardzo zajęty) lub jeśli węzeł brokera obsługi komunikatów staje się tymczasowo niedostępny, kontenery są redystrybuowane między hello węzłów brokera komunikatów.

## <a name="processing-of-incoming-messaging-requests"></a>Przetwarzanie przychodzących żądań obsługi komunikatów
Gdy klient wysyła żądanie tooService magistrali, hello Azure load balancer kieruje je tooany hello węzłów bramy. Witaj, węzeł bramy autoryzuje żądanie hello. Jeśli hello żądanie dotyczy jednostki obsługi komunikatów (kolejki, tematu, subskrypcji), hello węzeł bramy wyszukuje jednostkę hello w magazynie bramy hello i określa, w których wiadomości powitania magazynu znajduje się jednostki. Następnie wyszukuje które węzeł brokera obsługi komunikatów aktualnie obsługujący ten kontener i wysyła toothat żądania hello węzła brokera komunikatów. węzeł brokera wiadomości powitania przetwarza żądanie hello i aktualizuje stan jednostki hello hello kontenera magazynu. Hello wiadomości węzła brokera następnie wysyła hello odpowiedzi toohello wstecz bramy węzła, który wysyła klientowi wstecz toohello właściwą odpowiedź tego wystawione hello oryginalne żądanie.

![Przetwarzanie przychodzących żądań obsługi komunikatów](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Następne kroki
Teraz, gdy zostały przeczytane omówienie architektury usługi Service Bus, odwiedź hello następującego łącza Aby uzyskać więcej informacji:

* [Omówienie obsługi komunikatów w usłudze Service Bus](service-bus-messaging-overview.md)
* [Podstawy usługi Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Rozwiązanie do obsługi komunikatów kolejek korzystające z funkcji kolejek usługi Service Bus](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


