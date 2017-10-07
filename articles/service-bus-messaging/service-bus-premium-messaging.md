---
title: "aaaAzure usługi Service Bus w warstwie Premium i standardowa komunikatów cenową omówienie warstw | Dokumentacja firmy Microsoft"
description: "Warstwy Premium i Standardowa komunikatów usługi Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Warstwy Premium i Standardowa komunikatów usługi Service Bus

Komunikaty usługi Service Bus, w tym jednostki, takie jak kolejki i tematy, stanowią połączenie możliwości obsługi komunikatów dla przedsiębiorstw oraz zaawansowanej semantyki publikowania/subskrybowania w skali chmury. Komunikatów magistrali usług jest używany jako hello szkieletu komunikacyjnego dla wielu zaawansowanych rozwiązań w chmurze.

Witaj *Premium* warstwy usługi magistrali komunikatów adresów częste żądania klientów dotyczące skali, wydajności i dostępności dla aplikacji o krytycznym znaczeniu. Mimo że hello zestawy funkcji są niemal identyczne, te dwie warstwy komunikatów magistrali usług są zaprojektowane tooserve innych przypadków użycia.

Pewne ogólne różnice są wyróżnione na powitania w poniższej tabeli.

| Premium | Standardowa (Standard) |
| --- | --- |
| Wysoka przepływność |Zmienna przepływność |
| Przewidywalna wydajność |Zmienne opóźnienie |
| Stałe ceny |Zmienne ceny i płatność zgodnie z rzeczywistym użyciem |
| Możliwość tooscale obciążenia w górę i w dół |Nie dotyczy |
| Rozmiar komunikatu too1 MB |Rozmiar wiadomości w górę too256 KB |

**Usługa Bus Premium Messaging** zapewniają izolację zasobów na poziomie hello Procesora i pamięci, dzięki czemu obciążenia poszczególnych klientów uruchamia się w izolacji. Ten kontener zasobów jest nazywany *jednostką obsługi komunikatów*. Każda przestrzeń nazw w warstwie Premium ma przydzieloną co najmniej jedną jednostkę obsługi komunikatów. Możesz kupić 1, 2 lub 4 jednostki obsługi komunikatów dla każdej przestrzeni nazw usługi Service Bus w warstwie Premium. Pojedyncze obciążenie lub jednostka może obejmować wiele jednostek obsługi komunikatów, a hello liczbę jednostek obsługi komunikatów można dowolnie zmieniać, chociaż są w 24-godzinnym lub codziennie opłaty. wynik Hello jest przewidywalną i powtarzalną wydajność dla rozwiązania na podstawie usługi Service Bus.

Poprawa dotyczy nie tylko przewidywalności i dostępności, ale również szybkości działania. Usługa Bus Premium Messaging opiera się na aparacie magazynu hello wprowadzone w systemie [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/). Z obsługą wiadomości — wersja Premium maksymalna szybkość działania jest znacznie wyższa niż w przypadku warstwy standardowa hello.

## <a name="premium-messaging-technical-differences"></a>Różnice techniczne dotyczące komunikatów w warstwie Premium

Witaj poniższych sekcjach omówiono niektóre różnice między Premium i standardowa warstwy obsługi wiadomości.

### <a name="partitioned-queues-and-topics"></a>Partycjonowane kolejki i tematy

Partycjonowane kolejki i tematy są obsługiwane przez komunikaty w warstwie Premium; w rzeczywistości te jednostki są zawsze partycjonowane (i nie można ich wyłączyć). Jednak Premium podzielona na partycje, kolejek i tematów nie działa hello tak samo jak w hello warstwy standardowa i podstawowa komunikatów usługi Service Bus. Premium obsługi wiadomości nie używa SQL jako magazynu danych i nie ma hello konkurencji zasobów powiązanych z platformą udostępnionego. W związku z tym partycjonowanie nie jest konieczne tooimprove wydajności. Ponadto liczba partycji hello została zmieniona z 16 partycji w przypadku komunikatów w warstwie standardowa too2 partycji w warstwie Premium. Po dwóch partycji gwarantuje dostępność i jest bardziej odpowiednia liczba dla środowiska uruchomieniowego hello Premium. 

Z obsługą wiadomości — wersja Premium, po określeniu hello rozmiar jednostki z [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), czy rozmiar jest podzielone równo między hello 2 partycji, w odróżnieniu od [Standard partycjonowane jednostki](service-bus-partitioning.md#standard) w których hello Całkowity rozmiar jest 16 godzin hello określony rozmiar. 

Aby uzyskać więcej informacji na temat partycjonowania, zobacz [Partitioned queues and topics](service-bus-partitioning.md) (Partycjonowane kolejki i tematy).

### <a name="express-entities"></a>Jednostki ekspresowe

Ze względu na fakt, że obsługa komunikatów Premium działa w całkowicie odizolowanym środowisku uruchomieniowym, jednostki ekspresowe nie są obsługiwane w przestrzeniach nazw w warstwie Premium. Aby uzyskać więcej informacji o funkcji express hello, zobacz hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) właściwości.

Jeśli masz kod do uruchamiania standardowe tooport obsługi wiadomości i chcesz ją toohello warstwy Premium, upewnij się, że hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) właściwość jest ustawiona zbyt**false** (hello wartość domyślna).

## <a name="get-started-with-premium-messaging"></a>Wprowadzenie do obsługi komunikatów Premium

Wprowadzenie do obsługi komunikatów w warstwie Premium jest proste i hello proces jest podobny toothat Standard obsługi komunikatów. Rozpocznij od [utworzenia przestrzeni nazw](service-bus-create-namespace-portal.md). W obszarze **Warstwa cenowa** wybierz pozycję **Premium**.

![create-premium-namespace][create-premium-namespace]

Możesz również tworzyć [przestrzenie nazw Premium za pomocą szablonów usługi Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat usługi magistrali komunikatów, zobacz następujące tematy hello.

* [Introducing Azure Service Bus Premium messaging](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/) (Wprowadzenie do komunikatów usługi Service Bus w warstwie Premium) — wpis w blogu
* [Introducing Azure Service Bus Premium messaging](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging) (Wprowadzenie do komunikatów usługi Service Bus w warstwie Premium) — Channel9
* [Omówienie obsługi komunikatów w usłudze Service Bus](service-bus-messaging-overview.md)
* [Jak toouse kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
