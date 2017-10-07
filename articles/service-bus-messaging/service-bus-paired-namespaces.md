---
title: "przestrzenie nazw łączyć aaaAzure usługi Service Bus | Dokumentacja firmy Microsoft"
description: "Szczegóły implementacji par nazw i kosztów"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Skojarzone szczegóły implementacji przestrzeni nazw i kosztów efekty
Witaj [PairNamespaceAsync] [ PairNamespaceAsync] — metoda, za pomocą [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] wystąpienia, wykonuje zadania widoczne w Twoim imieniu. Ponieważ są koszt zagadnienia, podczas używania funkcji hello, jest przydatne toounderstand tych zadań, aby oczekiwać hello zachowanie, gdy nastąpi. Witaj interfejsu API angażujący hello następujące zachowanie automatyczne w Twoim imieniu:

* Tworzenie zaległości kolejki.
* Tworzenie [MessageSender] [ MessageSender] obiekt, który zawiera tooqueues lub tematów.
* Gdy jednostka obsługi komunikatów staje się niedostępny, wysyła komunikaty ping toohello jednostki w toodetect próba podczas jednostkę znowu dostępne.
* Opcjonalnie tworzy zestawu pomp"komunikat" czy przenoszenia wiadomości z hello zaległości kolejki toohello głównej kolejek.
* Współrzędne zamknięcia/spowodowaniem błędu z hello podstawowych i pomocniczych [MessagingFactory] [ MessagingFactory] wystąpień.

Na wysokim poziomie, funkcja hello działa w następujący sposób: obiekt podstawowy hello jest w dobrej kondycji, żadne zmiany zachowania nastąpić. Gdy hello [FailoverInterval] [ FailoverInterval] upłynie czas trwania, a obiekt podstawowy hello zobaczy nie powiodło się wysyła po z systemem innym niż przejściowy [MessagingException] [ MessagingException] lub [TimeoutException][TimeoutException], występuje hello następujące zachowanie:

1. Wyślij toohello operacji podstawowej jednostki są wyłączone i pakietów systemu hello hello podstawowej jednostki, aż pomyślnie dostarczony polecenia ping.
2. Wybrano losowe zaległości kolejki.
3. [BrokeredMessage] [ BrokeredMessage] obiekty są routingiem toohello wybrany zaległości kolejki.
4. W przypadku niepowodzenia toohello operacji wysyłania, wybierany zaległości kolejki tej kolejki są pobierane z obrotu hello i Nowa kolejka jest zaznaczone. Wszystkich nadawców na powitania [MessagingFactory] [ MessagingFactory] wystąpienia Dowiedz się hello awarii.

Witaj następującej liczby przedstawiać hello sekwencji. Po pierwsze hello Nadawca wysyła wiadomości.

![Sparowanego przestrzenie nazw][0]

Po awarii toosend toohello podstawowej kolejki hello nadawca zaczyna, wysyłania wiadomości tooa losowo wybrany zaległości kolejki. Rozpoczyna się jednocześnie, zadanie ping.

![Sparowanego przestrzenie nazw][1]

W tym momencie wiadomości powitania są nadal w hello kolejki dodatkowej, a nie została dostarczona toohello kolejki głównej. Po kolejki głównej hello jest w dobrej kondycji ponownie, co najmniej jednego procesu powinna działać hello syphon. Hello syphon dostarcza wiadomości powitania z wszystkich powitalne różnych zaległości kolejki toohello właściwe miejsce docelowe jednostek (kolejki i tematy).

![Sparowanego przestrzenie nazw][2]

Hello pozostałej części tematu opisano hello konkretne szczegółowe informacje, jak te elementy pracy.

## <a name="creation-of-backlog-queues"></a>Tworzenie zaległości kolejki
Witaj [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] obiekt przekazany toohello [PairNamespaceAsync] [ PairNamespaceAsync] hello wskazuje — metoda Liczba zaległości kolejki możesz mają toouse. Każdej kolejki zaległości zostanie utworzona z hello następujące właściwości jawnie ustaw (wszystkie inne wartości są ustawiane toohello [QueueDescription] [ QueueDescription] ustawień domyślnych):

| Ścieżka | [głównej przestrzeni nazw] / x magistrali usług transferu / [Indeks] [Indeks] w przypadku wartości [0, BacklogQueueCount) |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| maxDeliveryCount |int. MaxValue |
| DefaultMessageTimeToLive |Wartość TimeSpan.MaxValue |
| AutoDeleteOnIdle |Wartość TimeSpan.MaxValue |
| LockDuration |1 minuta |
| EnableDeadLetteringOnMessageExpiration |Wartość true |
| EnableBatchedOperations |Wartość true |

Na przykład hello pierwszej zaległości kolejki utworzone dla przestrzeni nazw **contoso** nosi nazwę `contoso/x-servicebus-transfer/0`.

Podczas tworzenia kolejki hello, kod hello najpierw sprawdza toosee, jeśli istnieje takiej kolejki. Jeśli hello kolejka nie istnieje, kolejka hello jest tworzona. nie ma kodu Hello oczyszczania "dodatkowe" zaległości kolejki. W szczególności, jeśli hello aplikacji hello głównej przestrzeni nazw **contoso** żądań w pięciu kolejkach zaległości, ale zaległości kolejki ze ścieżką hello `contoso/x-servicebus-transfer/7` istnieje, jest nadal znajdują się dodatkowe zaległości kolejki, ale nie są używane. Hello system jawnie zezwala na dodatkowe zaległości kolejki tooexist, który nie jest używany. Właściciel przestrzeni nazw hello jest odpowiedzialny za czyszczenie wszystkie nieużywane/niechciane zaległości kolejki. Witaj tej decyzji są usługi Service Bus nie wiadomo, jakich celów istnieje dla wszystkich kolejek hello w przestrzeni nazw. Ponadto jeśli kolejka o hello podanej nazwie istnieje, ale nie spełnia hello zakłada, że [QueueDescription][QueueDescription], nie można używać z powodów własne do zmieniających się hello domyślne zachowanie. Żadnych gwarancji są wykonywane dla kolejki zaległości toohello zmian w kodzie. Wprowadź zmiany tootest się dokładnie.

## <a name="custom-messagesender"></a>Niestandardowe MessageSender
Podczas wysyłania, wszystkie komunikaty go za pośrednictwem wewnętrznego [MessageSender] [ MessageSender] obiekt, który działa normalnie, kiedy wszystko działa i przekierowuje toohello zaległości kolejki, gdy elementy "break." Po odebraniu Błąd przejściowy z systemem innym niż, uruchamia czasomierz. Po [TimeSpan] [ TimeSpan] okres składające się z hello [FailoverInterval] [ FailoverInterval] wartość właściwości, w którym nie wysłano żadnych komunikatów powiodło się , pracy awaryjnej hello jest włączone. W tym momencie hello następujących czynności stanie dla każdego obiektu:

* Wykonuje zadanie ping co [PingPrimaryInterval] [ PingPrimaryInterval] toocheck, jeśli jednostka hello jest dostępna. Gdy to zadanie zakończy się powodzeniem, żadnego kodu klienta, który używa jednostki hello natychmiast rozpoczyna wysyłanie nowej wiadomości toohello głównej przestrzeni nazw.
* Tej samej jednostki z innych nadawców spowoduje hello toothat toosend przyszłych żądań [BrokeredMessage] [ BrokeredMessage] wysyłane toobe zmodyfikować toosit hello zaległości kolejki. Modyfikacja Hello usuwa hello niektóre właściwości [BrokeredMessage] [ BrokeredMessage] obiektu i przechowuje je w innym miejscu. Witaj następujące właściwości są wyczyszczone i dodany w obszarze Nowy alias, umożliwiając usługi Service Bus i hello wiadomości tooprocess SDK jednolicie:

| Stara nazwa właściwości | Nowa nazwa właściwości |
| --- | --- |
| Identyfikator sesji |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path. |

Oryginalna ścieżka docelowa Hello jest również przechowywane w wiadomości powitania jako właściwość o nazwie x-ms-path. Ten projekt umożliwia komunikatów dla wielu toocoexist jednostek w jednym zaległości kolejki. właściwości Hello są tłumaczone przez hello syphon.

niestandardowe Hello [MessageSender] [ MessageSender] obiektu można napotkania problemów podczas wiadomości podejścia limit 256 KB hello i pracy awaryjnej jest włączone. niestandardowe Hello [MessageSender] [ MessageSender] obiekt przechowuje komunikaty wszystkich kolejek i tematów w hello zaległości kolejki. Ten obiekt łączy komunikaty z wielu kolory podstawowe w ramach hello zaległości kolejki. obciążenia toohandle zrównoważyć wielu klientów, których nie wiadomo, każdy inny, hello SDK losowo wybiera jeden zaległości kolejki dla każdego [QueueClient] [ QueueClient] lub [TopicClient] [ TopicClient] tworzenie w kodzie.

## <a name="pings"></a>Polecenia ping
Wiadomość ping jest pusta [BrokeredMessage] [ BrokeredMessage] z jego [ContentType] [ ContentType] tooapplication/vnd.ms-magistrali usług ping ustawić właściwości i [TimeToLive] [ TimeToLive] wartość 1 sekundę. To polecenie ping ma jeden właściwości specjalne w usłudze Service Bus: serwer hello nigdy nie zapewnia polecenia ping, gdy zażąda każdego obiektu wywołującego [BrokeredMessage][BrokeredMessage]. W związku z tym, że nie musisz toolearn jak tooreceive i Ignoruj tych wiadomości. Każdy obiekt (unikatowe kolejka lub temat) na [MessagingFactory] [ MessagingFactory] wystąpienia na klienta będzie można wykonywać polecenia ping, gdy są one uznawane za toobe niedostępny. Domyślnie to odbywa się raz na minutę. Wiadomości ping są traktowane jako toobe regularne komunikatów usługi Service Bus i może spowodować opłaty za przepustowości i komunikatów. Jak hello klienci wykrywają, że hello system jest dostępny, Zatrzymaj wiadomości powitania.

## <a name="hello-syphon"></a>Witaj syphon
Co najmniej jeden program wykonywalny w aplikacji hello aktywnie powinna działać hello syphon. Witaj syphon wykonuje długi sondowania odbierania, które to 15 minut. Gdy wszystkie obiekty są dostępne i masz 10 zaległości kolejki, hello aplikacji, która obsługuje wywołania syphon hello hello odbierania operacji 40 razy na godzinę, 960 razy dziennie i 28800 razy w ciągu 30 dni. Podczas hello syphon jest aktywnie przenoszenia wiadomości z kolejki głównej hello zaległości toohello, każdy komunikat napotyka powitania po opłaty (standardowe opłaty za rozmiaru wiadomości i przepustowości dotyczy wszystkich etapach):

1. Wyślij toohello zaległości.
2. Otrzymywać hello zaległości.
3. Wyślij toohello podstawowego.
4. Otrzymywać hello podstawowego.

## <a name="closefault-behavior"></a>Zamknij/błędów zachowanie
W aplikacji, która obsługuje hello syphon, raz hello podstawowej lub pomocniczej [MessagingFactory] [ MessagingFactory] błędów lub zostanie zamknięty bez jej partnerów również błędny/zamknięte i hello syphon wykrywa tego stanu , hello syphon działa. Jeśli inne hello [MessagingFactory] [ MessagingFactory] nie są zamknięte w ciągu 5 sekund hello syphon będzie fault Otwórz nadal hello [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Następne kroki
Zobacz [asynchroniczne wzorce i wysokiej dostępności do obsługi komunikatów] [ Asynchronous messaging patterns and high availability] szczegółowe omówienie asynchroniczne komunikatów usługi Service Bus. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
