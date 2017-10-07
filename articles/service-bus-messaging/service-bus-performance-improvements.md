---
title: "aaaBest wskazówki dotyczące poprawiania wydajności przy użyciu usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse usługi Service Bus toooptimize wydajności podczas wymiany obsługiwanych przez brokera komunikatów."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Najlepsze rozwiązania dotyczące poprawy wydajności przy użyciu usługi magistrali komunikatów

W tym artykule opisano sposób toouse [komunikatów usługi Azure Service Bus](https://azure.microsoft.com/services/service-bus/) toooptimize wydajności podczas wymiany obsługiwanych przez brokera komunikatów. Witaj w pierwszej części tego tematu opisano hello różnych mechanizmów, które są oferowane toohelp zwiększyć wydajność. druga część Hello znajdują się wskazówki dotyczące sposobu toouse usługi Service Bus w taki sposób, aby zaoferować hello najlepszą wydajność w danym scenariuszu.

W tym temacie hello termin "client" oznacza tooany jednostki, która uzyskuje dostęp do usługi Service Bus. Klient może zająć roli hello nadawcy i adresata. Witaj termin "sender" jest używana dla usługi Service Bus kolejka lub temat klienta, który wysyła wiadomości tooa usługi Service Bus kolejka lub temat. Witaj termin "odbiorcy" odnosi się tooa usługi Service Bus kolejki lub subskrypcji klienta, który odbiera komunikaty z kolejki usługi Service Bus lub subskrypcji.

Tych sekcjach przedstawiono kilka założenia, że Usługa Service Bus używa toohelp wydajnością.

## <a name="protocols"></a>Protokoły
Usługa Service Bus umożliwia toosend klientów i odbierania wiadomości za pomocą jednego z trzech protokołów:

1. Zaawansowane kolejkowania wiadomości protokołu (protokół AMQP)
2. Protokół (SBMP) do obsługi komunikatów usługi Service Bus
3. HTTP

AMQP i SBMP są bardziej wydajne, ponieważ ich obsługa hello tooService połączenia magistrali tak długo, jak istnieje hello fabryki obsługi komunikatów. Implementuje również przetwarzanie wsadowe i Odczyt z wyprzedzeniem. Chyba że jawnie wspomniano, cała zawartość w tym temacie założono, hello użycia protokołu AMQP lub SBMP.

## <a name="reusing-factories-and-clients"></a>Ponowne wykorzystywanie fabryk i klientów
Klient usługi Service Bus obiekty, takie jak [QueueClient] [ QueueClient] lub [MessageSender][MessageSender], są tworzone za pomocą [ MessagingFactory] [ MessagingFactory] obiektu, który udostępnia również wewnętrznego zarządzania połączenia. Fabryki obsługi komunikatów lub kolejki, tematu i subskrypcji klientów należy zamknąć nie po wysłać wiadomość, a następnie utwórz je po wysłaniu dalej wiadomości powitania. Zamykanie fabryki obsługi komunikatów usuwa usługi Service Bus toohello połączenia hello i nawiązaniem nowego połączenia podczas odtwarzania hello fabryki. Ustanowienie połączenia jest kosztowna operacja, trzeba będzie ponownie używając hello tej samej fabryki i klienta obiektów na wiele operacji. Można bezpiecznie użyć hello [QueueClient] [ QueueClient] obiekt do wysyłania wiadomości z równoczesnych operacji asynchronicznych i wiele wątków. 

## <a name="concurrent-operations"></a>Równoczesne wykonywanie operacji
Wykonywanie operacji (wysyłanie, odbierania, usuwanie, itp.) dopiero po pewnym czasie. Teraz obejmuje hello przetwarzania operacji hello przez hello usługi Service Bus opóźnienia toohello dodanie hello żądania i odpowiedzi hello. tooincrease hello liczbę operacji na czas, operacji musi być wykonywany współbieżnie. Można to zrobić na kilka różnych sposobów:

* **Operacje asynchroniczne**: powitania klienta planuje operacji przez wykonanie operacji asynchronicznych. następnym żądaniu Hello jest uruchamiana przed zakończeniem hello poprzedniego żądania. Witaj poniżej przedstawiono przykład operacja asynchronicznego wysyłania:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  To jest przykład asynchronicznego odbioru operacji:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Wiele fabryk**: wszystkich klientów (nadawcy w tooreceivers dodanie) utworzone przez hello tej samej fabryki udziału jednego połączenia TCP. przepustowość maksymalna wiadomość Hello jest ograniczona przez hello liczby operacji można przejść przez to połączenie TCP. Witaj przepływność, którą można uzyskać za pomocą pojedynczego fabryki znacznie zależy od czasami opóźnienia TCP i rozmiar wiadomości. tooobtain wyższe przepływności, należy używać wielu fabryki obsługi komunikatów.

## <a name="receive-mode"></a>Tryb odbierania
Podczas tworzenia kolejki lub subskrypcji klienta, można określić tryb odbierania: *blokady Peek* lub *odbieranie i usuwanie*. tryb odbierania domyślne Hello jest [PeekLock][PeekLock]. Podczas działania w tym trybie, powitania klienta wysyła tooreceive żądania z usługi Service Bus komunikat. Po odebraniu wiadomości powitania klienta hello wysyła wiadomość hello toocomplete żądania.

Gdy ustawienie hello tryb odbierania zbyt[ReceiveAndDelete][ReceiveAndDelete], oba kroki są łączone w ramach pojedynczego żądania. Zmniejsza to całkowita liczba operacji hello i może zwiększyć hello ogólną przepustowość wiadomości. To są bardziej wydajne efektem hello ryzyko utraty wiadomości.

Usługa Service Bus nie obsługuje transakcji dla operacji odbierania i usuwania. Ponadto semantyki peek blokady są wymagane dla wszelkie scenariusze, w których powitania klienta chce toodefer lub [utraconych](service-bus-dead-letter-queues.md) wiadomości.

## <a name="client-side-batching"></a>Przetwarzanie wsadowe po stronie klienta
Przetwarzanie wsadowe po stronie klienta umożliwia kolejka lub temat klienta toodelay hello wysyłanie wiadomości w danym okresie czasu. Jeśli klient hello wysyła dodatkowe komunikaty w trakcie tego okresu, przesyła wiadomości powitania w pojedynczej partii. Przetwarzanie wsadowe po stronie klienta powoduje także, że kolejka lub subskrypcji toobatch klienta wielu **Complete** żądań do pojedynczego żądania. Tworzenie plików wsadowych jest dostępna tylko dla asynchronicznego **wysyłania** i **Complete** operacji. Operacje synchroniczne są natychmiast wysyłane toohello usługi Service Bus. Przetwarzanie wsadowe nie nastąpić peek ani operacji pobrania nie jest przetwarzanie wsadowe wykonywane przez klientów.

Domyślnie klient używa się w przedziale partii 20ms. Można zmienić interwał partii hello ustawienie hello [BatchFlushInterval] [ BatchFlushInterval] właściwości przed utworzeniem hello fabryki obsługi komunikatów. To ustawienie dotyczy wszystkich klientów, które zostały utworzone przy użyciu tej fabryki.

Przetwarzanie wsadowe toodisable, ustaw hello [BatchFlushInterval] [ BatchFlushInterval] właściwości zbyt**TimeSpan.Zero**. Na przykład:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Przetwarzanie wsadowe nie ma wpływu na powitania liczba rozliczeniowy operacji obsługi wiadomości i jest dostępna tylko w przypadku hello Protokół klienta usługi Service Bus. Witaj protokołu HTTP nie obsługuje przetwarzanie wsadowe.

## <a name="batching-store-access"></a>Przetwarzanie wsadowe dostęp do sklepu
Przepływność hello tooincrease kolejki, tematu lub subskrypcji, usługi Service Bus partii wiele komunikatów, gdy zapisuje tooits wewnętrznego magazynu. Jeśli jest włączona kolejka lub temat, zapisywania komunikatów w magazynie hello będzie można umieścić w partii. Jeśli włączona dla kolejki lub subskrypcji, usuwania komunikatów z magazynu hello będzie można umieścić w partii. Po włączeniu dostępu do sklepu wsadów dla jednostki usługi Service Bus opóźnienia operacji zapisu magazynu dotyczących tego obiektu w górę too20ms. Operacji dodatkowego magazynu, które występują w danym przedziale czasu są dodawane toohello partii. Umieścić w zadaniu wsadowym wpływa jedynie na dostęp do magazynu **wysyłania** i **Complete** operacji; odbierania nie wpływ na operacje. Dostęp do sklepu wsadów jest właściwością w jednostce. Przetwarzanie wsadowe występuje we wszystkich jednostek, które umożliwiają dostęp do sklepu wsadowej.

Podczas tworzenia nowej kolejki, tematu lub subskrypcji, dostęp do sklepu wsadów jest domyślnie włączona. toodisable umieścić w zadaniu wsadowym dostęp do sklepu, zestaw hello [EnableBatchedOperations] [ EnableBatchedOperations] właściwości zbyt**false** przed utworzeniem hello jednostki. Na przykład:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Dostęp do sklepu wsadów nie ma wpływu na powitania liczba rozliczeniowy operacji obsługi wiadomości i jest właściwością kolejki, tematu lub subskrypcji. Nie zależy od hello odbierania trybu i hello protokół, który jest używany między klientem a hello usługi Service Bus.

## <a name="prefetching"></a>Odczyt z wyprzedzeniem
Odczyt z wyprzedzeniem umożliwia hello kolejki lub subskrypcji klienta tooload dodatkowych komunikatów z usługi hello podczas wykonywania operacji odbierania. powitania klienta przechowuje te wiadomości w lokalnej pamięci podręcznej. rozmiar pamięci podręcznej hello Hello jest określany przez hello [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] lub [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] właściwości. Każdy klient, który umożliwia odczyt z wyprzedzeniem zachowuje własną pamięci podręcznej. Pamięć podręczna nie jest współużytkowana przez klientów. Jeśli klient hello inicjuje operacji odbierania i pamięci podręcznej jest pusty, usługi hello przesyła partia komunikatów. Hello rozmiar wsadu hello jest równe hello rozmiar pamięci podręcznej hello lub 256 KB, w zależności od jest mniejsza. Hello pamięci podręcznej zawiera wiadomości powitania klienta inicjuje operacji odbierania, wiadomość hello jest pobierana z pamięci podręcznej hello.

Gdy komunikat jest prefetched, komunikat prefetched hello hello usługi blokad. W ten sposób prefetched wiadomość hello nie może zostać odebrany przez inny odbiornik. Jeśli odbiornik hello nie może ukończyć wiadomość hello przed wygaśnięciem blokady hello, wiadomość hello staje się odbiorniki tooother dostępne. Witaj prefetched kopia wiadomości powitania pozostaje w pamięci podręcznej hello. Hello odbiornika, który wykorzystuje hello wygasł buforowane kopiowania otrzymają Wystąpił wyjątek podczas próby toocomplete tej wiadomości. Domyślnie blokady wiadomość hello wygasa po 60 sekund. Ta wartość może być rozszerzonej too5 minut. zużycia hello tooprevent wygasłych komunikatów, rozmiar pamięci podręcznej hello powinien zawsze być mniejszy niż hello liczba wiadomości, które mogą być używane przez klienta w ramach interwał limitu czasu blokady hello.

Korzystając z okresu ważności blokady domyślne hello 60 sekund, wartość jest dobrą [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] hello 20 razy maksymalny przetwarza stawki wszystkich odbiorników hello fabryki. Na przykład fabrykę tworzy odbiorniki 3, a każdy odbiorca może przetwarzać się too10 komunikatów na sekundę. Liczba pobierania z wyprzedzeniem Hello nie może przekraczać 20 X 3 X 10 = 600. Domyślnie [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] jest zestaw too0, co oznacza pobrane nie dodatkowe wiadomości powitania usługi.

Odczyt z wyprzedzeniem zwiększa ogólną przepustowość kolejki lub subskrypcji Witaj, ponieważ redukuje hello ogólna liczba operacje dotyczące komunikatów lub rund wiadomości. Pobieranie pierwszą wiadomość hello, jednak będzie trwało dłużej (powodu toohello zwiększyć rozmiar komunikatu). Odbieranie komunikatów prefetched będzie przebiegać szybciej, ponieważ komunikaty te zostały już pobrane przez powitania klienta.

Hello time to live (TTL) właściwości wiadomości jest sprawdzana przez serwer hello w czasie hello hello serwer wysyła klientowi toohello wiadomość hello. Po odebraniu wiadomości powitania powitania klienta nie sprawdza właściwości czas wygaśnięcia wiadomości powitania. Zamiast tego mogą być odbierane wiadomości powitania nawet, jeśli czas wygaśnięcia wiadomości powitania minął podczas wiadomości powitania był buforowany przez powitania klienta.

Odczyt z wyprzedzeniem nie ma wpływu na powitania liczba rozliczeniowy operacji obsługi wiadomości i jest dostępna tylko w przypadku hello Protokół klienta usługi Service Bus. Witaj protokołu HTTP nie obsługuje odczyt z wyprzedzeniem. Odczyt z wyprzedzeniem jest dostępna dla operacji odbioru synchroniczne i asynchroniczne.

## <a name="express-queues-and-topics"></a>Express kolejek i tematów

Jednostki ekspresowe włączyć uzyskać wysoką przepustowość i mniejsze opóźnienia scenariuszy i są obsługiwane tylko w warstwie standardowa wiadomości powitania. Jednostki utworzone w [przestrzeniach nazw warstwy Premium](service-bus-premium-messaging.md) nie obsługują opcji express hello. Z jednostki ekspresowe Jeśli komunikat jest wysyłany tooa kolejka lub temat, wiadomość hello nie są natychmiast przechowywane w magazynie obsługi komunikatów hello. Zamiast tego są buforowane w pamięci. Jeśli wiadomość pozostaje w kolejce hello więcej niż kilka sekund, są automatycznie zapisywane toostable magazynu, w związku z tym ochrony przed utratą powodu tooan awarii. Pisanie wiadomości powitania w pamięci podręcznej zwiększa przepustowość i zmniejsza opóźnienia, ponieważ nie istnieje żadne toostable dostępu do magazynu na wiadomość powitania czasu hello są wysyłane. Komunikaty, które są używane w ciągu kilku sekund nie są zapisywane toohello magazynu do obsługi komunikatów. Witaj poniższy przykład tworzy express tematu.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Jeśli jednostki ekspresowe tooan jest wysyłany komunikat zawierający krytyczne informacje, które nie mogą być utracone, nadawca hello wymusić usługi Service Bus tooimmediately utrwalić magazynu toostable wiadomość hello przez ustawienie hello [ForcePersistence] [ ForcePersistence] właściwości zbyt**true**.

> [!NOTE]
> Jednostki ekspresowe nie obsługuje transakcji.

## <a name="use-of-partitioned-queues-or-topics"></a>Korzystanie z podzielonym na partycje kolejki i tematy
Wewnętrznie używa usługi Service Bus hello tego samego węzła i wiadomości tooprocess magazynu i przechowywać wszystkie komunikaty dla jednostki obsługi komunikatów (kolejki lub tematu). Partycjonowane kolejka lub temat, na powitania drugiej strony, będzie rozmieszczona na wielu węzłach i magazyny obsługi komunikatów. Partycjonowane kolejek i tematów nie tylko uzyskanie wyższej przepustowości niż regularne kolejek i tematów, charakteryzują wysokiej dostępności. toocreate partycjonowane jednostki, zestaw hello [parametr EnablePartitioning] [ EnablePartitioning] właściwości zbyt**true**, jak pokazano w hello poniższy przykład. Aby uzyskać więcej informacji na temat partycjonowane jednostki, zobacz [partycjonowane jednostki do obsługi komunikatów][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Korzystanie z wielu kolejek

Jeśli nie jest możliwe toouse, który partycjonowanej kolejka lub temat lub hello oczekuje się, że obciążenie nie mogą być obsługiwane przez partycjonowanej kolejka lub temat, należy użyć wiele jednostek obsługi komunikatów. Używając wiele jednostek, Utwórz dedykowane klienta dla każdej jednostki, zamiast hello sam klienta dla wszystkich jednostek.

## <a name="development-and-testing-features"></a>Programowanie i testowanie funkcji

Usługa Service Bus ma jedną funkcję używanego specjalnie z myślą o programowanie którego **nie mogą być używane w konfiguracjach produkcji**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Po dodaniu tematu toohello nowe reguły lub filtrów, można użyć [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify, który hello nowe wyrażenie filtru działa zgodnie z oczekiwaniami.

## <a name="scenarios"></a>Scenariusze
Witaj poniższych sekcjach opisano typowe scenariusze obsługi wiadomości i przedstawiają hello preferowanych ustawień usługi Service Bus. Przepływności są sklasyfikowane jako mały (mniej niż 1 komunikatów na sekundę), średni (1 komunikatów na sekundę lub większą, ale mniej niż 100 komunikatów na sekundę) i wysoki (100 wiadomości/sekundę lub większą). Hello liczby klientów są sklasyfikowane jako mała liczba godzin (5 lub mniej), umiarkowany (więcej niż 5 mniejsza niż lub równy too20) i duże (więcej niż 20).

### <a name="high-throughput-queue"></a>Kolejki wysokiej przepustowości
Cel: Zmaksymalizować przepustowość hello pojedynczej kolejki. Liczba Hello nadawcami a odbiornikami jest mała.

* Użyj kolejki partycjonowanej większą wydajność i dostępność.
* tooincrease hello ogólną szybkość wysyłania w kolejce hello, użyj wielu nadawców toocreate fabryk komunikatów. Dla każdego nadawcy użyj operacji asynchronicznych lub wiele wątków.
* Witaj tooincrease ogólną szybkość odbierania z kolejki hello, użyj wieloma odbiornikami toocreate fabryk komunikatów.
* Użyj zaletą tootake operacje asynchroniczne przetwarzanie wsadowe po stronie klienta.
* Ustaw hello przetwarzanie wsadowe interwału too50ms tooreduce hello liczba transmisji protokołu klienta usługi Service Bus. Użycie wielu nadawców zwiększyć hello przetwarzanie wsadowe too100ms interwału.
* Pozostaw włączony dostęp do magazynu wsadowej. Powoduje to zwiększenie hello ogólną szybkość z jaką komunikaty mogą być zapisywane w kolejce hello.
* Ustaw hello pobierania z wyprzedzeniem liczba too20 razy szybkości przetwarzania maksymalną hello wszystkich odbiorników fabryki. Pozwala to zmniejszyć liczbę hello transmisji protokołu klienta usługi Service Bus.

### <a name="multiple-high-throughput-queues"></a>Wielu kolejek wysokiej przepustowości
Cel: Zmaksymalizować ogólną przepustowość wielu kolejek. Przepływność Hello pojedynczej kolejki jest średni czy wysoki.

Maksymalna przepustowość tooobtain wiele kolejek, użyj ustawień hello opisane przepływność hello toomaximize pojedynczej kolejki. Ponadto przy użyciu różnych fabryki toocreate klientów, które wysłać lub odebrać z różnych kolejek.

### <a name="low-latency-queue"></a>Małe opóźnienia kolejki
Cel: Zminimalizować czas oczekiwania na trasie kolejka lub temat. Liczba Hello nadawcami a odbiornikami jest mała. Przepływność Hello kolejki hello jest mała lub średniego.

* Użyj kolejki podzielonym na partycje do zwiększenia dostępności.
* Wyłącz przetwarzanie wsadowe po stronie klienta. powitania klienta natychmiast wysyła komunikat.
* Wyłącz dostęp do sklepu wsadowej. Usługa Hello natychmiast zapisuje magazyn toohello wiadomości powitania.
* Jeśli przy użyciu jednego klienta, należy ustawić hello pobierania z wyprzedzeniem liczba too20 razy hello szybkości przetwarzania hello odbiornika. Jeśli wiele wiadomości do kolejki hello na powitania sam czas hello Protokół klienta usługi Service Bus przesyła je na powitania tym samym czasie. Powitania klienta odebrania następnej wiadomości powitania ten komunikat jest już w lokalnej pamięci podręcznej hello. pamięć podręczna Hello powinna być niewielka.
* Jeśli używasz wielu klientów, należy ustawić too0 liczba pobierania z wyprzedzeniem hello. Dzięki temu hello drugi klient może odbierać hello drugi komunikat, gdy pierwszy klient hello nadal przetwarza pierwszą wiadomość hello.

### <a name="queue-with-a-large-number-of-senders"></a>Kolejka z dużą liczbą nadawców
Cel: Zmaksymalizować przepustowość kolejka lub temat z dużą liczbą nadawcy. Każdy Nadawca wysyła komunikaty z wartością średnią. Witaj liczba odbiorcy jest mała.

Usługa Service Bus umożliwia się tooa równoczesnych połączeń too1000 jednostki do obsługi komunikatów (lub 5000 za pomocą protokołu AMQP). Ten limit jest wymuszane na poziomie przestrzeni nazw hello i kolejek/tematy/subskrypcje są ograniczone przez hello limit równoczesnych połączeń na przestrzeni nazw. W przypadku kolejek ta liczba jest udostępniana między nadawcami a odbiornikami. Jeśli wszystkie połączenia 1000 są wymagane dla nadawców, należy zastąpić hello kolejki z tematu i jedną subskrypcją. Temat akceptuje się too1000 równoczesnych połączeń od nadawcy, natomiast subskrypcji hello akceptuje dodatkowych 1000 równoczesnych połączeń od odbiorcy. Jeśli wymaganych jest więcej niż 1000 równoczesnych nadawców nadawców hello należy wysłać wiadomości toohello protokołu usługi Service Bus za pośrednictwem protokołu HTTP.

Przepływność toomaximize hello następujące:

* Użyj kolejki partycjonowanej większą wydajność i dostępność.
* Jeśli każdego nadawcy znajduje się w ramach innego procesu, należy użyć tylko jednej fabryki na proces.
* Użyj zaletą tootake operacje asynchroniczne przetwarzanie wsadowe po stronie klienta.
* Użyj domyślnej hello przetwarzanie wsadowe interwał 20ms tooreduce hello liczba transmisji protokołu klienta usługi Service Bus.
* Pozostaw włączony dostęp do magazynu wsadowej. Powoduje to zwiększenie hello ogólną szybkość z jaką komunikaty mogą być zapisywane na powitania kolejka lub temat.
* Ustaw hello pobierania z wyprzedzeniem liczba too20 razy szybkości przetwarzania maksymalną hello wszystkich odbiorników fabryki. Pozwala to zmniejszyć liczbę hello transmisji protokołu klienta usługi Service Bus.

### <a name="queue-with-a-large-number-of-receivers"></a>Kolejka z wieloma odbiornikami
Cel: Zmaksymalizować hello szybkość kolejki lub subskrypcji z dużą liczbą odbiorników odbioru. Każdy odbiorca odbiera komunikaty z umiarkowane szybkością. Liczba Hello nadawców jest mała.

Usługa Service Bus umożliwia się too1000 równoczesnych połączeń tooan jednostki. Jeśli kolejka wymaga więcej niż 1000 odbiorcy, należy zastąpić hello kolejki z tematu i subskrypcji. Każda subskrypcja może obsługiwać się too1000 równoczesnych połączeń. Alternatywnie odbiorcy mają dostęp do kolejki hello za pośrednictwem hello protokołu HTTP.

Przepływność toomaximize hello następujące:

* Użyj kolejki partycjonowanej większą wydajność i dostępność.
* Każdy odbiorca znajduje się w ramach innego procesu, należy użyć tylko jednej fabryki na proces.
* Odbiorniki można używać operacji synchroniczna lub asynchroniczna. Podany umiarkowany hello szybkość poszczególnych odbiornika odbioru, wykonać żądanie przetwarzanie wsadowe po stronie klienta nie ma wpływu na przepływność odbiorcy.
* Pozostaw włączony dostęp do magazynu wsadowej. Zmniejsza to hello całkowite obciążenie hello jednostki. Zmniejsza również hello ogólną szybkość z jaką komunikaty mogą być zapisywane na powitania kolejka lub temat.
* Ustaw wartość małej liczby tooa hello pobierania z wyprzedzeniem (na przykład PrefetchCount = 10). Zapobiega to odbiorcy ze stanu bezczynności podczas innym odbiornikom ma dużą liczbę komunikatów w pamięci podręcznej.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Temat z małą liczbą subskrypcji
Cel: Zmaksymalizować przepustowość hello tematu z mniejszą liczbą subskrypcji. Komunikat jest odbierany przez wiele subskrypcji, co oznacza, że hello łączyć odbierania współczynnik powyżej wszystkie subskrypcje jest większy niż hello szybkość wysyłania. Liczba Hello nadawców jest mała. Witaj liczba odbiorcy dla subskrypcji jest mała.

Przepływność toomaximize hello następujące:

* Skorzystaj z podzielonym na partycje tematu, aby uzyskać lepszą wydajność i dostępność.
* tooincrease hello ogólną szybkość wysyłania w temacie hello, użyj wielu nadawców toocreate fabryk komunikatów. Dla każdego nadawcy użyj operacji asynchronicznych lub wiele wątków.
* Witaj tooincrease ogólną szybkość odbierania z subskrypcji, użyj wieloma odbiornikami toocreate fabryk komunikatów. Dla każdego adresata użyj operacji asynchronicznych lub wiele wątków.
* Użyj zaletą tootake operacje asynchroniczne przetwarzanie wsadowe po stronie klienta.
* Użyj domyślnej hello przetwarzanie wsadowe interwał 20ms tooreduce hello liczba transmisji protokołu klienta usługi Service Bus.
* Pozostaw włączony dostęp do magazynu wsadowej. Powoduje to zwiększenie hello ogólną szybkość z jaką komunikaty mogą być zapisywane w temacie hello.
* Ustaw hello pobierania z wyprzedzeniem liczba too20 razy szybkości przetwarzania maksymalną hello wszystkich odbiorników fabryki. Pozwala to zmniejszyć liczbę hello transmisji protokołu klienta usługi Service Bus.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Temat z dużą liczbą subskrypcji
Cel: Zmaksymalizować przepustowość hello tematu z dużą liczbą subskrypcji. Komunikat jest odbierany przez wiele subskrypcji, co oznacza, że hello łączyć odbierania współczynnik powyżej wszystkie subskrypcje jest znacznie większa niż częstotliwość wysyłania hello. Liczba Hello nadawców jest mała. Witaj liczba odbiorcy dla subskrypcji jest mała.

Tematy z dużą liczbą subskrypcji zwykle ujawnić niski ogólną przepustowość, ile wszystkie komunikaty są routingiem tooall subskrypcji. Jest to spowodowane hello fakt, że każdy komunikat jest odbierany wiele razy, a wszystkie komunikaty, które znajdują się w temacie i wszystkie jego subskrypcje są przechowywane w hello sam magazynu. Zakłada się, liczba hello nadawców i liczby odbiorników dla subskrypcji jest mała. Usługa Service Bus obsługuje too2, 000 subskrypcji na temat.

Przepływność toomaximize hello następujące:

* Skorzystaj z podzielonym na partycje tematu, aby uzyskać lepszą wydajność i dostępność.
* Użyj zaletą tootake operacje asynchroniczne przetwarzanie wsadowe po stronie klienta.
* Użyj domyślnej hello przetwarzanie wsadowe interwał 20ms tooreduce hello liczba transmisji protokołu klienta usługi Service Bus.
* Pozostaw włączony dostęp do magazynu wsadowej. Powoduje to zwiększenie hello ogólną szybkość z jaką komunikaty mogą być zapisywane w temacie hello.
* Ustaw hello pobierania z wyprzedzeniem liczba razy too20 odbierania hello oczekiwano częstotliwość w sekundach. Pozwala to zmniejszyć liczbę hello transmisji protokołu klienta usługi Service Bus.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat optymalizacji wydajności usługi Service Bus, zobacz [partycjonowane jednostki do obsługi komunikatów][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
