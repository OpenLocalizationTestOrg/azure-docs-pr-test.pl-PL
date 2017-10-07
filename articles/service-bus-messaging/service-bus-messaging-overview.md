---
title: "Omówienie komunikatów usługi Service Bus aaaAzure | Dokumentacja firmy Microsoft"
description: "Opis obsługi komunikatów w usłudze Service Bus oraz usługi Azure Relay"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Komunikatów usługi Service Bus: elastyczne dostarczanie danych w chmurze hello
Usługa Microsoft Azure Service Bus to niezawodna usługa dostarczania informacji. Witaj celem tej usługi jest komunikacja toomake łatwiejsze. Gdy dwie lub więcej stron przystępuje tooexchange informacji, muszą one pośrednik w przemieszczaniu komunikacji. Usługa Service Bus to mechanizm obsługiwany przez brokera lub mechanizm komunikacji innej firmy. Jest to podobne tooa usługi pocztowe w świecie hello. Usługi pocztowe stał się bardzo łatwo toosend różnych rodzajów listów i przesyłek z różną gwarancją dostarczania dowolne miejsce w hello world.

Podobne toohello za pomocą usług pocztowych, usługi Service Bus jest dostarczania informacji elastyczne z hello nadawcy i odbiorcy hello. usługę wiadomości powitania gwarantuje dostarczenie informacji hello, nawet jeśli Witaj dwie strony nigdy nie są w tryb online na powitania samym czasie lub jeśli nie są dostępne pod adresem hello dokładnie takie same czasu. W ten sposób obsługi wiadomości jest podobne toosending literą, podczas komunikacji z systemem innym niż obsługiwane przez brokera jest podobne tooplacing rozmowy telefonicznej (lub używania toobe — przed wywołania oczekującymi i Identyfikatorem dzwoniącego, które są bardziej przypominają komunikaty obsługiwane przez brokera połączeń telefonicznych).

nadawcy wiadomości powitania może również wymagać różnych właściwości dostarczania, w tym transakcji, wykrywania duplikatów, wygaśnięcia działającego i przetwarzanie wsadowe. Te wzorce również mają cechy wspólne z usługami pocztowymi: powtórne dostarczenie, wymagany podpis, zmiana adresu lub wycofanie.

Usługa Service Bus obsługuje dwa różne wzorce obsługi komunikatów: usługa *Azure Relay* i *obsługa komunikatów w usłudze Service Bus*.

## <a name="azure-relay"></a>Azure Relay
Witaj [przekazywania WCF](../service-bus-relay/relay-what-is-it.md) składnik Azure przekazywania jest scentralizowana (ale o wysokim stopniu równoważenia obciążenia) usługa, która obsługuje wiele różnych protokołów transportowych i standardów usług sieci Web. Obejmuje to usługi SOAP, WS-*, a nawet REST. Witaj [Usługa przekazywania](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) zapewnia różnorodność opcji łączności przekazywania i może pomóc podczas negocjowania bezpośrednich połączeń peer-to-peer, gdy jest możliwe. Usługi Service Bus jest zoptymalizowana pod kątem .NET deweloperzy, którzy używają hello Windows Communication Foundation (WCF), zarówno z uwzględnieniem tooperformance i użyteczność, i zapewnia pełny dostęp tooits usługą przekazywania za pomocą interfejsów SOAP i REST. Dzięki temu dla dowolnego programowania SOAP lub REST toointegrate środowisko z usługą Service Bus.

Hello usługa przekaźnika obsługuje tradycyjne jednokierunkowe komunikaty, komunikaty żądań/odpowiedzi, a wiadomości peer-to-peer. Obsługuje ona również dystrybucję zdarzeń w zakresie Internetu tooenable publikowania / subskrypcji scenariuszy i komunikacji poprzez gniazdo dwukierunkowe dla zwiększonej wydajności point-to-point. We wzorcu komunikatów obsługiwanych przez przekaźnik hello Usługa lokalna łączy toohello przekaźnika usługi za pomocą portu wychodzącego i tworzy gniazdo dwukierunkowe dla komunikacji powiązanej tooa konkretnym adresem spotkania. powitania klienta następnie może komunikować się z usługą lokalne powitania przez wysłanie wiadomości toohello usługi przekazywania kierującej hello adresu spotkania. Witaj usługi przekazywania następnie "przekazuje" komunikaty toohello lokalną usługą poprzez gniazdo dwukierunkowe hello już w miejscu. Hello klient nie potrzebuje bezpośredniego połączenia usługi lokalnej toohello ani tooknow it wymagane, w którym znajduje się usługa hello i hello Usługa lokalna nie wymaga żadnych portów przychodzących jest otwarty na zaporze hello.

Inicjuje hello połączenie między usługą lokalną i usługi przekazywania hello, przy użyciu zestawu powiązań "przekazuje" usługi WCF. Tle hello hello powiązania przekaźników są mapowane tootransport powiązania elementy toocreate składników kanału WCF integrujące się z magistralą usług w chmurze hello.

Przekaźnik WCF oferuje wiele korzyści, ale wymaga powitania serwera i klienta tooboth być w trybie online na powitania sam czas w kolejności toosend i odbierania wiadomości. To nie jest optymalna dla komunikacji typu HTTP, w których hello żądania nie mogą mieć typowo długiego okresu życia, ani dla klientów łączących się tylko okazjonalnie, takich jak przeglądarki, aplikacji dla urządzeń przenośnych i tak dalej. Komunikaty obsługiwane przez brokera obsługują komunikację odłączoną i mają wiele zalet. Klienci i serwery mogą łączyć się w zależności od potrzeb i wykonywać operacje w sposób asynchroniczny.

## <a name="brokered-messaging"></a>Komunikaty obsługiwane przez brokera
Z kolei toohello przekazywania schematu, usługi Service Bus wiadomości, lub [komunikatów obsługiwanych przez brokera](service-bus-queues-topics-subscriptions.md) mogą być traktowane jako asynchroniczne lub "czasowo odłączone". Producenci (nadawcy) i konsumenci (odbiorcy) nie jest toobe w trybie online na powitania tym samym czasie. infrastruktury obsługi wiadomości powitania niezawodny sposób przechowuje komunikaty w "brokerze" (np. w kolejce) do momentu hello odbierająca jest gotowa tooreceive je. Dzięki temu składniki hello toobe aplikacji hello rozproszonych rozłączone zarówno dobrowolnie; na przykład w celu przeprowadzenia konserwacji lub powodu tooa awarii składników, bez wywierania wpływu na cały system hello. Ponadto aplikacja odbierająca hello może mieć tylko toocome online pewnych porach dnia hello, jak w przypadku systemu zarządzania spisem tylko jest wymagana toorun hello końca dnia roboczego hello.

podstawowe składniki infrastruktury komunikatów obsługiwanych przez brokera usługi Service Bus hello Hello są kolejki, tematy i subskrypcje.  Witaj podstawowa różnica polega na tym, że tematy obsługują możliwości publikowania/subskrybowania, które mogą być używane dla zaawansowane opartej na zawartości logiki routingu i dostarczania, w tym wysyłania toomultiple adresatów. Te składniki umożliwiają nowe asynchroniczne scenariusze obsługi komunikatów, takie jak czasowe oddzielenie, publikowanie/subskrypcja i równoważenie obciążenia. Aby uzyskać więcej informacji na temat tych jednostek obsługi komunikatów, zobacz sekcję [Kolejki, tematy i subskrypcje usługi Magistrala usług](service-bus-queues-topics-subscriptions.md).

Zgodnie z infrastrukturą przekazywania WCF hello, hello komunikatów obsługiwanych przez brokera możliwości podano dla programistów WCF i .NET Framework, a także za pośrednictwem interfejsu REST.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat komunikatów usługi Service Bus, zobacz następujące tematy hello.

* [Podstawy usługi Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Kolejki, tematy i subskrypcje usługi Service Bus](service-bus-queues-topics-subscriptions.md)
* [Jak toouse kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Jak toouse usługi Service Bus tematów i subskrypcji](service-bus-dotnet-how-to-use-topics-subscriptions.md)

