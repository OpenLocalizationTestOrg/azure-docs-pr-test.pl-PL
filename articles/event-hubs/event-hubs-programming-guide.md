---
title: "Przewodnik aaaProgramming dla usługi Azure Event Hubs | Dokumentacja firmy Microsoft"
description: "Pisanie kodu dla usługi Azure Event Hubs przy użyciu hello Azure .NET SDK."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Przewodnik programowania w usłudze Event Hubs

W tym artykule opisano kilka typowych scenariuszy w pisanie kodu przy użyciu usługi Azure Event Hubs i hello Azure .NET SDK. Przyjęto założenie, że wstępnie znasz i rozumiesz usługę Event Hubs. Omówienie koncepcji usługi Event hubs, zobacz hello [Przegląd usługi Event Hubs](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Wydawcy zdarzeń

Możesz wysłać Centrum zdarzeń tooan zdarzeń za pomocą protokołu HTTP POST lub za pośrednictwem połączenia protokołu AMQP 1.0. Witaj wybór które toouse, gdy jest zależna od hello konkretnego scenariusza. Połączenia protokołu AMQP 1.0 są mierzone jako połączenia obsługiwane przez brokera w Service Bus i są bardziej odpowiednie w scenariuszach z częstymi większymi ilościami wiadomości oraz wymaganiami dotyczącymi krótszych opóźnień, ponieważ zapewniają trwały kanał obsługi komunikatów.

Tworzenie i zarządzanie nimi Event Hubs przy użyciu hello [NamespaceManager][] klasy. Gdy przy użyciu platformy .NET hello zarządzanych interfejsów API, hello głównej konstruuje publikowania danych tooEvent koncentratory są hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) i [EventData][] klasy. [EventHubClient][] udostępnia kanał komunikacji protokołu AMQP hello przez który zdarzenia są wysyłane toohello Centrum zdarzeń. Witaj [EventData][] klasa reprezentuje zdarzenie i jest Centrum zdarzeń tooan toopublish używanych w wiadomości. Ta klasa zawiera treść hello, niektóre metadane i informacje nagłówka zdarzenia hello. Inne właściwości są dodawane toohello [EventData][] obiektów, kiedy przechodzi on przez Centrum zdarzeń.

## <a name="get-started"></a>Rozpoczęcie pracy

Hello .NET klas, które obsługują usługi Event Hubs są zawarte w zestawie Microsoft.ServiceBus.dll hello. Witaj Najprostszym sposobem tooreference hello interfejsu API usługi Service Bus i tooconfigure aplikacji ze wszystkimi zależnościami usługi Service Bus hello jest toodownload hello [pakietu NuGet usługi Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Alternatywnie można użyć hello [Konsola Menedżera pakietów](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) w programie Visual Studio. toodo tak, wydać następujące polecenie w hello hello [Konsola Menedżera pakietów](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) okno:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Tworzenie centrum zdarzeń
Można użyć hello [NamespaceManager][] klasy toocreate Event Hubs. Na przykład:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

W większości przypadków zaleca się, że używasz hello [CreateEventHubIfNotExists][] tooavoid metody generowania wyjątków, jeśli usługa hello jest uruchamiana ponownie. Na przykład:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Wszystkie operacje tworzenia usługi Event Hubs, w tym [CreateEventHubIfNotExists][], wymagają **Zarządzaj** uprawnień w przestrzeni nazw hello zagrożona. Jeśli chcesz toolimit hello uprawnienia aplikacji wydawcy lub odbiorcy, możesz uniknąć tych utworzyć wywołania operacji w kodzie produkcyjnym, korzystając z poświadczeń z ograniczonymi uprawnieniami.

Witaj [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) klasa zawiera szczegółowe informacje o Centrum zdarzeń, w tym hello reguł autoryzacji, interwał przechowywania wiadomości powitania identyfikatory partycji, stan i ścieżkę. Możesz użyć tej klasy tooupdate hello metadanych w Centrum zdarzeń.

## <a name="create-an-event-hubs-client"></a>Tworzenie klienta usługi Event Hubs
Hello podstawowe klasy do interakcji z usługą Event Hubs jest [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Ta klasa udostępnia zarówno funkcje nadawcy, jak i odbiornika. Można utworzyć wystąpienia tej klasy przy użyciu hello [Utwórz](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) metody, jak pokazano w hello poniższy przykład.

```csharp
var client = EventHubClient.Create(description.Path);
```

Ta metoda używa informacji o połączeniu usługi Service Bus hello w pliku App.config hello, hello `appSettings` sekcji. Przykład Witaj `appSettings` XML używane informacje o połączeniu usługi Service Bus hello toostore, zobacz dokumentację hello hello [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) metody.

Innym rozwiązaniem jest toocreate powitania klienta z parametrów połączenia. Ta opcja działa dobrze w przypadku, gdy przy użyciu ról procesu roboczego platformy Azure, ponieważ ciąg hello można przechowywać w hello właściwości konfiguracji dla procesu roboczego hello. Na przykład:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

Parametry połączenia Hello będą hello takiego samego formatu wyświetlaną w pliku App.config hello hello wcześniejszych metod:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Na koniec jest również możliwe toocreate [EventHubClient][] obiekt z [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) wystąpienie, jak pokazano w hello poniższy przykład.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Jest to dodatkowe ważne toonote [EventHubClient][] obiekty utworzone na podstawie wystąpienia fabryki obsługi komunikatów będą ponownie wykorzystać hello samego podstawowego połączenia TCP. Z tego względu te obiekty mają limit przepływności po stronie klienta. Witaj [Utwórz](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) metody ponownie używa pojedynczej fabryki obsługi wiadomości. Jeśli potrzebujesz bardzo wysokiej przepływności od jednego nadawcy, możesz utworzyć wiele fabryk komunikatów i jeden obiekt [EventHubClient][] z każdej fabryki obsługi komunikatów.

## <a name="send-events-tooan-event-hub"></a>Wyślij Centrum zdarzeń tooan zdarzeń
Wyślij Centrum zdarzeń tooan zdarzeń przez utworzenie [EventData][] wystąpienia i wysłanie go za pośrednictwem hello [wysyłania](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) metody. Ta metoda przyjmuje jeden [EventData][] parametru wystąpienia i synchronicznie wysyła go tooan Centrum zdarzeń.

## <a name="event-serialization"></a>Serializacja zdarzeń
Witaj [EventData][] klasa ma [cztery przeciążone konstruktory](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) , które wymagają różnych parametrów, takich jak obiekt i serializator, tablica bajtów lub strumień. Możliwe jest również możliwe tooinstantiate hello [EventData][] klasy i ustaw strumień treści hello później. Korzystając z formatu JSON z [EventData][], można użyć **Encoding.UTF8.GetBytes()** tablicy bajtowej hello tooretrieve dla ciąg zakodowany w formacie JSON.

## <a name="partition-key"></a>Klucz partycji
Witaj [EventData][] klasa ma [PartitionKey][] właściwość, która umożliwia toospecify nadawcy hello wartość skrótu tooproduce przypisania partycji. Użycie klucza partycji gwarantuje wszystkie hello zdarzenia z tym samym kluczem są wysyłane hello toohello sam partycji w Centrum zdarzeń hello. Wspólne klucze partycji zawierają identyfikatory sesji użytkownika i unikatowe identyfikatory nadawcy. Witaj [PartitionKey][] właściwość jest opcjonalna i może zostać dostarczona przy użyciu hello [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) lub [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) metody. Jeśli nie zostanie określona wartość [PartitionKey][], wysyłane zdarzenia są rozproszone toopartitions przy użyciu modelu okrężnego.

### <a name="availability-considerations"></a>Zagadnienia dotyczące dostępności

Użycie klucza partycji jest opcjonalna i należy starannie rozważyć czy toouse jeden. W wielu przypadkach przy użyciu klucza partycji jest dobrym rozwiązaniem, jeśli zdarzenie kolejność jest ważna. Użycie klucza partycji, partycje wymagają dostępności w jednym węźle, a awarii wraz z upływem czasu; na przykład podczas obliczania ponownego uruchomienia węzłów i poprawki. W efekcie ustawiony identyfikator partycji i tej partycji przestanie być dostępny dla jakiegoś powodu, próba tooaccess hello danych w tej partycji zakończy się niepowodzeniem. Jeśli najważniejszych jest wysoka dostępność, nie należy określać klucz partycji. w takim przypadku zdarzenia będą wysyłane toopartitions przy użyciu modelu okrężnego hello opisanych powyżej. W tym scenariuszu utworzysz jawną wyboru między dostępności (Brak Identyfikatora partycji) i spójności (identyfikator partycji: zdarzenia tooa przypinanie).

Kolejnym zagadnieniem jest obsługa opóźnienia w przetwarzaniu zdarzeń. W niektórych przypadkach go może być lepiej toodrop danych i ponów niż tootry i nadąża z przetwarzaniem, który może powodować opóźnienia dalszego przetwarzania podrzędnego. Na przykład z giełdowych jest lepsze toowait pełną aktualne dane, ale w czatu na żywo lub scenariusza VOIP raczej trzeba danych hello szybkie, nawet jeśli nie jest ukończone.

Biorąc pod uwagę następujące zagadnienia dotyczące dostępności w tych scenariuszach użytkownik może wybrać jedną z powitania po strategii obsługi błędów:

- Stop (Zatrzymaj odczytywania z usługi Event Hubs, dopóki elementy zostały usunięte)
- Upuść (komunikaty nie są ważne, upuść je)
- Spróbuj ponownie (ponawiania powitalne wiadomości, jak widać dopasowania)
- [Utraconych](../service-bus-messaging/service-bus-dead-letter-queues.md) (Użyj innego toodead Centrum zdarzeń lub kolejki utraconych tylko wiadomości powitania nie może przetworzyć)

Więcej informacji oraz omówienie kompromisy powitania od dostępności i spójności, zobacz [dostępności i spójności w usłudze Event Hubs](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Operacje wysyłania partii zdarzeń
Wysyłanie zdarzeń w partiach może znacznie zwiększyć przepływność. Witaj [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) ma metodę **IEnumerable** parametr typu [EventData][] i wysyła hello całą partię jako Centrum zdarzeń toohello niepodzielną operację.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Należy pamiętać, że pojedyncza partia nie może przekraczać limitu 256 KB hello zdarzenia. Ponadto każdy komunikat w partii hello używa hello tej samej tożsamości wydawcy. Jest to hello odpowiedzialność hello tooensure nadawcy, który hello partii nie przekracza hello maksymalnego rozmiaru zdarzenia. Jeśli go przekroczy, zostanie wygenerowany błąd metody **Send** klienta.

## <a name="send-asynchronously-and-send-at-scale"></a>Wysyłanie asynchroniczne i wysyłanie na dużą skalę
Możesz również wysłać Centrum zdarzeń tooan zdarzeń asynchronicznie. Wysyłanie asynchroniczne może zwiększyć szybkość hello jaką klient jest w stanie toosend zdarzenia. Zarówno hello [wysyłania](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) i [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) metody są dostępne w wersjach asynchronicznych, które zwracają [zadań](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) obiektu. Gdy ta technika może zwiększyć przepływność, jego przyczyną może być również powitania klienta toocontinue toosend zdarzeń nawet wtedy, gdy jest ograniczany przez hello usługi Event Hubs i może skutkować błędami powitania klienta lub utratą komunikatów Jeśli nie została poprawnie zaimplementowana. Ponadto można użyć hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) właściwość opcjami ponawiania prób powitania klienta toocontrol klienta.

## <a name="create-a-partition-sender"></a>Tworzenie nadawcy dla partycji
Najbardziej typowe toosend zdarzenia tooan Centrum zdarzeń bez klucza partycji, ale w niektórych przypadkach może być zdarzeń toosend bezpośrednio tooa podane partycji. Na przykład:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) zwraca [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) obiektów służy partycji Centrum toopublish zdarzenia tooa konkretnego zdarzenia.

## <a name="event-consumers"></a>Odbiorcy zdarzeń
Usługa Event Hubs ma dwa podstawowe modele użycia zdarzeń: odbiorniki bezpośrednie i abstrakcje wyższego poziomu, takie jak klasa [EventProcessorHost][]. Odbiorniki bezpośrednie są odpowiedzialne za własną koordynację dostępu toopartitions w obrębie grupy odbiorców.

### <a name="direct-consumer"></a>Bezpośredni odbiorca
najbardziej bezpośrednim tooread sposób Hello z partycji w obrębie grupy odbiorców jest toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) klasy. toocreate jako wystąpienie tej klasy, należy użyć wystąpienia hello [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) klasy. W hello poniższy przykład należy określić identyfikator partycji: hello podczas tworzenia hello odbiornika dla grupy odbiorców hello.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Witaj [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) metoda ma kilka przeciążeń, które ułatwiają kontrolę nad tworzonym czytnikiem hello. Te metody obejmują Określanie przesunięcia jako ciągu lub sygnatury czasowej, a hello możliwości toospecify czy tooinclude to określone przesunięcie w hello zwrócił strumienia lub rozpocząć po nim. Po utworzeniu odbiornika hello, można uruchomić odbieranie zdarzeń na powitania zwrócił obiekt. Witaj [Receive](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) metoda ma cztery przeciążenia hello tego formantu otrzymywać parametrów operacji, takich jak rozmiar partii i czas oczekiwania. Używając asynchronicznych wersji tych metod tooincrease hello przepływności konsumenta hello. Na przykład:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Z zakresie tooa określonej partycji wiadomości powitania są odbierane w kolejności hello, w którym zostały wysłane toohello Centrum zdarzeń. Przesunięcie Hello jest ciąg tokenu tooidentify używanych komunikatów w partycji.

Należy zauważyć, że pojedyncza partycja w obrębie grupy odbiorców w żadnym momencie nie może mieć połączonych więcej niż 5 współbieżnych czytników. Jak czytniki nawiązują połączenie lub rozłączają, ich sesje mogą pozostać aktywne przez kilka minut, zanim usługa hello rozpozna, że zostały odłączone. W tym czasie ponowne łączenie tooa partycji może zakończyć się niepowodzeniem. Aby uzyskać kompletny przykład pisania aplikacji bezpośredniego odbiornika usługi Event hubs, zobacz hello [odbiorniki bezpośrednie centra zdarzeń](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) próbki.

### <a name="event-processor-host"></a>Host procesora zdarzeń
Witaj [EventProcessorHost][] klasy przetwarza dane z usługi Event Hubs. Podczas tworzenia czytników zdarzeń na platformie .NET hello należy używać tej implementacji. Klasa [EventProcessorHost][] udostępnia bezpieczne wątkowo, wieloprocesowe, bezpieczne środowisko uruchomieniowe dla implementacji procesora zdarzeń, które umożliwia także tworzenie punktów kontrolnych i zarządzanie dzierżawą partycji.

Witaj toouse [EventProcessorHost][] klasy, można zaimplementować [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Ten interfejs zawiera trzy metody:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

przetwarzanie zdarzeń toostart wystąpienia [EventProcessorHost][], zapewniając hello odpowiednie parametry Centrum zdarzeń. Następnie wywołaj metodę [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister Twojego [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implementacji ze środowiskiem uruchomieniowym hello. W tym momencie hello host będzie podejmować tooacquire dzierżawy na każdej partycji w Centrum zdarzeń hello za pomocą "zachłannego" algorytmu. Te dzierżawy będą trwać przez dany przedział czasu, a następnie muszą być odnowione. Jak nowe węzły wystąpień procesów roboczych w takim przypadku przejdzie w tryb online, ich rezerwacje dzierżawy i w czasie ładowania hello przewiduje między węzłami jako każdej próby tooacquire więcej dzierżaw.

![Host procesora zdarzeń](./media/event-hubs-programming-guide/IC759863.png)

W miarę upływu czasu zostaje ustalona równowaga. Ta dynamiczna funkcja umożliwia skalowania automatycznego na podstawie procesora CPU tooconsumers toobe stosowane do skalowania w górę i w dół. Ponieważ usługa Event Hubs nie ma bezpośredniej koncepcji liczby komunikatów, średnie wykorzystanie procesora CPU jest często hello najlepszym mechanizmem toomeasure wstecz skali zaplecza lub odbiorcy. Jeśli wydawcy zaczną toopublish, który może przetwarzać więcej zdarzeń niż konsumentów, hello zwiększenie użycia procesora CPU przez odbiorców może być używane toocause automatyczne skalowanie liczby wystąpień procesu roboczego.

Witaj [EventProcessorHost][] klasa implementuje również mechanizm Azure opartej na magazynie punkty kontrolne. Jest to hello magazynów mechanizmu przesunięcie na podstawie partycji, dzięki czemu każdy odbiorca może określić, jakie hello ostatni punkt kontrolny od poprzedniego odbiorcy hello. Ponieważ partycje przechodzą między węzłami za pośrednictwem dzierżaw, jest to mechanizm synchronizacji hello, który ułatwia przesunięcie obciążenia.

## <a name="publisher-revocation"></a>Odwołanie wydawcy
Ponadto toohello zaawansowane funkcje środowiska wykonawczego [EventProcessorHost][], usługa Event Hubs umożliwia odwołanie wydawcy w kolejności tooblock dostępu określonych wydawców do wysyłania zdarzeń tooan zdarzenia koncentratora. Te funkcje są szczególnie przydatne, jeśli naruszono bezpieczeństwo tokenu wydawcy lub aktualizacja oprogramowania powoduje nieuprawnione toobehave niewłaściwie. W takich przypadkach tożsamości wydawcy hello, która jest częścią jego tokenu sygnatury dostępu Współdzielonego, można zablokować publikowania zdarzeń.

Aby uzyskać więcej informacji o odwołaniu wydawcy i toosend tooEvent Hubs jako wydawca, zobacz temat hello [zdarzeń koncentratory dużej skali bezpieczne publikowanie](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) próbki.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji o scenariuszach usługi Event Hubs, odwiedź te linki:

* [Omówienie interfejsu API usługi Event Hubs](event-hubs-api-overview.md)
* [Co to jest usługa Event Hubs](event-hubs-what-is-event-hubs.md)
* [Availability and consistency in Event Hubs](event-hubs-availability-and-consistency.md) (Dostępność i spójność w usłudze Event Hubs)
* [Dokumentacja interfejsu API hosta procesora zdarzeń](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
