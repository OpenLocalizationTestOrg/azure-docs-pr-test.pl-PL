---
title: "Przeglądanie Azure komunikatów usługi Service Bus | Dokumentacja firmy Microsoft"
description: "Przeglądanie i wybieranie komunikatów usługi Service Bus"
services: service-bus-messaging
documentationcenter: 
author: clemensv
manager: timlt
editor: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2017
ms.author: sethm
ms.openlocfilehash: b0bc1ef7570ccac07975e2560a1d0501d3cde2b3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="message-browsing"></a>Przeglądanie wiadomości

Komunikat przeglądanie ("wybierania") umożliwia klientowi wyliczyć wszystkie komunikaty znajdującej się w kolejce lub subskrypcji, zazwyczaj diagnostycznych i debugowania.

Operacje wglądu zwraca wszystkie wiadomości znajdujące się w dzienniku komunikat kolejki lub subskrypcji, nie tylko te dostępne do powstania natychmiastowego z *Receive()* lub *OnMessage()* pętli. *Stanu* właściwości każdy komunikat informuje, czy wiadomość jest aktywny (dostępne do odebrania), odroczone (patrz odroczenia [łącze do ustalenia]) lub zaplanowane (patrz wiadomości zaplanowane [łącze do ustalenia]).

Zużywa i wygasłe komunikaty są czyszczone przez asynchronicznego Uruchom "wyrzucanie elementów bezużytecznych" musi dokładnie wiadomości wygaśnięcia i w związku z tym wglądu w rzeczywistości może zwrócić wiadomości, które już wygasł i zostanie usunięte ani wiadomości lettered podczas odbierania Operacja obok została wywołana, kolejka lub subskrypcji.

Jest to szczególnie ważne, należy wziąć pod uwagę podczas próby odzyskania odroczonego wiadomości z kolejki. Komunikat, dla którego [ExpiresAtUtc](/dotnet/api/microsoft.azure.servicebus.message.expiresatutc#Microsoft_Azure_ServiceBus_Message_ExpiresAtUtc) przeszło błyskawicznych nie jest już kwalifikuje się do pobierania regularne w inny sposób, nawet wtedy, gdy zostały zwrócone przez podglądu. Zwracanie te komunikaty jest zamierzone, ponieważ Peek to narzędzie Diagnostyka aktualnym stanie dziennika.

Peek również zwraca wiadomości, które zostały zablokowane i są przetwarzane aktualnie przez innych odbiorców, ale nie zostało jeszcze zakończone. Jednak ponieważ Peek zwraca odłączonego migawki, stan blokady wiadomości nie mogą być obserwowane przybywającej komunikatów i [LockedUntilUtc](/dotnet/api/microsoft.azure.servicebus.core.messagereceiver.lockeduntilutc#Microsoft_Azure_ServiceBus_Core_MessageReceiver_LockedUntilUtc) i [LockToken](/dotnet/api/microsoft.azure.servicebus.message.systempropertiescollection.locktoken#Microsoft_Azure_ServiceBus_Message_SystemPropertiesCollection_LockToken) throw właściwości [ InvalidOperationException](/dotnet/api/system.invalidoperationexception) gdy aplikacja próbuje odczytać je.

## <a name="peek-apis"></a>Wybieranie interfejsów API

[Wglądu/PeekAsync](/dotnet/api/microsoft.azure.servicebus.core.messagereceiver.peekasync#Microsoft_Azure_ServiceBus_Core_MessageReceiver_PeekAsync) i [PeekBatch/PeekBatchAsync](/dotnet/api/microsoft.servicebus.messaging.queueclient.peekbatchasync#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatchAsync_System_Int64_System_Int32_) metody istnieją w wszystkich usług .NET i Java bibliotek klienckich i na wszystkich obiektach odbiornik: **MessageReceiver**, **MessageSession**, **QueueClient**, i **SubscriptionClient**. Wybieranie działania na wszystkich kolejek i subskrypcje oraz ich odpowiednich kolejki utraconych wiadomości.

Gdy wywołuje się wielokrotnie, metody Peek wylicza wszystkie komunikaty, które istnieją w dzienniku kolejki lub subskrypcji, w kolejności sekwencji, z najniższą dostępny numer porządkowy jako najwyższe. Jest to kolejność, w którym wiadomości były umieszczonych w kolejce; nie jest kolejność, w którym wiadomości po pewnym czasie może być pobierane.

[PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient.peekbatch#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) pobiera wiele komunikatów i zwraca je jako wyliczenie. Jeśli nie ma wiadomości, obiekt wyliczenie jest pusta, nie jest pusty.

Można również inicjatora przeciążenia metody z [SequenceNumber](/dotnet/api/microsoft.azure.servicebus.message.systempropertiescollection.sequencenumber#Microsoft_Azure_ServiceBus_Message_SystemPropertiesCollection_SequenceNumber) w którym należy uruchomić, a następnie wywołać przeciążenie metody bez parametrów, dalsze wyliczyć. **PeekBatch** ekwiwalentnie działa, ale jednocześnie pobiera zestaw komunikatów.

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej o komunikatów usługi Service Bus, zobacz następujące tematy:

* [Podstawy usługi Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Kolejki, tematy i subskrypcje usługi Service Bus](service-bus-queues-topics-subscriptions.md)
* [Wprowadzenie do kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Jak używać tematów i subskrypcji usługi Service Bus](service-bus-dotnet-how-to-use-topics-subscriptions.md)