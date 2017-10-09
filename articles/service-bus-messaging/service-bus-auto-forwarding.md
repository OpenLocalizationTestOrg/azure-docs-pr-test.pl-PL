---
title: "przekazywanie aaaAuto jednostki do obsługi komunikatów usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Jak toochain usługi Service Bus kolejki lub kolejka tooanother subskrypcji lub temat."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Tworzenie łańcuchów jednostek usługi Service Bus z automatyczne przekazywanie

Witaj usługi Service Bus *automatyczne przekazywanie* pozwala toochain kolejkę lub kolejki tooanother subskrypcji lub temat, który jest częścią hello tego samego obszaru nazw. Gdy włączone jest automatyczne przekazywanie, usługi Service Bus automatycznie usuwa wiadomości, które są umieszczane w pierwszej kolejki hello lub subskrypcji (źródło) i umieszcza je w hello drugi kolejka lub temat (docelowy). Należy pamiętać, że nadal możliwe toosend do jednostki docelowej toohello komunikat bezpośrednio. Ponadto nie jest możliwe toochain podkolejki, takich jak kolejki utraconych wiadomości, tooanother kolejka lub temat.

## <a name="using-auto-forwarding"></a>Przy użyciu automatycznego przekazywania
Możesz włączyć automatyczne przekazywanie przez ustawienie hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] lub [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] właściwości na powitania [QueueDescription] [ QueueDescription] lub [SubscriptionDescription] [ SubscriptionDescription] obiekty źródła hello, tak jak hello Poniższy przykład.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

Witaj jednostki docelowej musi istnieć w czasie hello jednostki źródłowej hello jest tworzony. Jeśli hello jednostki docelowej nie istnieje, usługi Service Bus zwraca wyjątek podczas zadawane toocreate hello jednostki źródłowej.

Umożliwia automatyczne przekazywanie tooscale limit poszczególne tematy. Usługi Service Bus limity hello [liczba subskrypcji danego tematu](service-bus-quotas.md) too2, 000. Może obsłużyć dodatkowe subskrypcji, tworząc tematy drugiego poziomu. Należy pamiętać, że nawet jeśli nie są powiązane przez hello usługi Service Bus ograniczenia hello liczbę subskrypcji, dodawanie drugiego poziomu tematów można zwiększyć hello ogólną przepustowość tematu.

![Automatyczne przekazywanie scenariusza][0]

Umożliwia także automatyczne przekazywanie nadawcy wiadomości toodecouple z odbiorcy. Rozważmy na przykład system ERP, który składa się z trzech modułów: kolejność przetwarzania, Zarządzanie zapasami i zarządzania relacjami z klientami. Każdy z tych modułów generuje wiadomości, które są umieszczonych w kolejce do odpowiedniego tematu. Alicja i Robert są przedstawicieli handlowych, którzy chcą wszystkie komunikaty dotyczące tootheir klientów. tooreceive tych wiadomości, Alicja, jak i Robert Utwórz kolejkę osobistych i subskrypcji na każdym hello ERP tematów, które automatycznie przekazywać wszystkie kolejki tootheir wiadomości.

![Automatyczne przekazywanie scenariusza][1]

Jeśli Alicja odbędzie się na urlop, swoje osobiste kolejki, a nie hello ERP tematu, wypełnia. W tym scenariuszu ponieważ przedstawiciel handlowy nie odebrał żadnych wiadomości Brak tematów ERP hello kiedykolwiek łączność przydziału.

## <a name="auto-forwarding-considerations"></a>Zagadnienia dotyczące automatyczne przekazywanie

Jeśli jednostki docelowej hello akumuluje zbyt wiele komunikatów i przekracza przydział hello lub hello jednostki docelowej jest wyłączona, jednostki źródłowej hello dodaje tooits wiadomości powitania [kolejki utraconych wiadomości](service-bus-dead-letter-queues.md) do momentu w docelowym hello jest miejsca lub hello jednostki zostanie ponownie włączony. Te komunikaty będą nadal toolive kolejki utraconych wiadomości powitania, musisz jawnie odbierania i ich przetwarzania z kolejki utraconych wiadomości powitania.

Podczas łączenia ze sobą tooobtain tematy złożonego temat o wielu subskrypcji, zaleca się, że masz umiarkowanej liczbie subskrypcje tematu pierwszego stopnia hello i wiele subskrypcji na powitania tematy drugiego poziomu. Na przykład pierwszego stopnia tematu z subskrypcjami 20, każdego z nich łańcuchowej tooa drugiego poziomu tematu z subskrypcjami 200 umożliwia wyższej przepustowości niż tematu pierwszego stopnia z subskrypcjami 200 każdego łańcuchowej tooa drugiego poziomu tematu z subskrypcjami 20 .

Usługa Service Bus rachunków jedna operacja dla każdej przekazany dalej komunikat. Na przykład wysyłanie temat tooa wiadomość z subskrypcjami 20, każde z nich skonfigurowany komunikatów do przodu tooauto tooanother kolejka lub temat, jest użyta jako 21 operacje, jeśli wszystkie subskrypcje pierwszego stopnia otrzymać kopię wiadomości powitania.

toocreate subskrypcji, która jest tooanother łańcuchowa kolejka lub temat hello twórca subskrypcji hello musi mieć **Zarządzaj** uprawnienia na powitania źródła i hello jednostki docelowej. Wysyłanie wiadomości toohello źródła tematu wymaga tylko **wysyłania** uprawnienia na powitania źródła tematu.

## <a name="next-steps"></a>Następne kroki

Szczegółowe informacje dotyczące automatycznego przekazywania zobacz następujące tematy dokumentacji hello:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn więcej informacji na temat ulepszenia wydajności usługi Service Bus, zobacz 

* [Najlepsze rozwiązania dotyczące poprawy wydajności przy użyciu usługi magistrali komunikatów](service-bus-performance-improvements.md)
* [Partycjonowane jednostki do obsługi komunikatów][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
