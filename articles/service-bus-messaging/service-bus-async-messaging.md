---
title: "aaaService magistrali komunikatów asynchronicznych | Dokumentacja firmy Microsoft"
description: "Opis usługi Azure Service Bus asynchroniczną obsługę wiadomości."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Wzorce asynchronicznej obsługi komunikatów i wysoka dostępność

Asynchroniczne wiadomości może być wdrożonych w różnych sposobów. Z kolejki, tematy i subskrypcje usługi Azure Service Bus obsługuje asynchronism za pośrednictwem sklepu i mechanizmu przekazywania. W normalnych warunkach (synchroniczne) wysyłanie wiadomości tooqueues i tematy i odbieranie komunikatów z subskrypcji i kolejek. Aplikacje, które należy zapisać zależą od tych jednostek zawsze będzie dostępna. Po zmianie kondycji jednostki hello powodu tooa różnych okolicznościach, należy tooprovide sposób jednostki ograniczoną możliwość, która spełnia wymagania większości.

Aplikacje zazwyczaj używają tooenable asynchroniczne wzorce obsługi komunikatów kilka scenariuszy komunikacji. Można tworzyć aplikacje, w których klienci mogą wysyłać wiadomości tooservices, nawet wtedy, gdy usługa hello nie jest uruchomiona. Dla aplikacji, które występują seria komunikacji kolejka może pomóc hello poziomu obciążenia przez zapewnienie komunikacji toobuffer miejsce. Na koniec można uzyskać obciążenia prostą, ale skuteczne wiadomości toodistribute równoważenia między wieloma maszynami.

W kolejności toomaintain dostępności dowolnej z tych obiektów należy wziąć pod uwagę kilka różnych sposobów tych jednostek może pojawiania się niedostępne dla trwałego systemu obsługi wiadomości. Ogólnie rzecz biorąc widzimy jednostki hello stają się tooapplications niedostępne, możemy napisany w hello następujące sposoby:

* Nie można toosend wiadomości.
* Nie można tooreceive wiadomości.
* Toomanage jednostek (Tworzenie, pobieranie, aktualizować lub usuwać jednostek).
* Nie można toocontact hello usługi.

Dla każdego z tych błędów niepowodzenie różne tryby istnieje umożliwiających pracy tooperform toocontinue aplikacji na określonym poziomie zmniejszenie możliwości. Na przykład system, który może wysyłać wiadomości, ale nie otrzymały ich może nadal otrzymywać zamówień klientów, ale nie można przetworzyć zamówień. W tym temacie omówiono potencjalne problemy, które mogą wystąpić, oraz jak te problemy zostaną skorygowane. Usługa Service Bus ma wprowadzono szereg środki zaradcze, które należy wybrać w, i w tym temacie omówiono również powitalne hello zasady stosowania tych opcjonalnych środki zaradcze.

## <a name="reliability-in-service-bus"></a>Niezawodność w usłudze Service Bus
Istnieje kilka sposobów toohandle problemów wiadomości i jednostek, a istnieją wytyczne dotyczące hello odpowiedniego stosowania tych środki zaradcze. toounderstand hello wytycznych, należy najpierw zrozumieć, co może zakończyć się niepowodzeniem w magistrali usługi. Powodu toohello projektu systemu Azure wszystkie te problemy zwykle toobe krótkim okresie. Na wysokim poziomie hello różne przyczyny niedostępności wyglądają następująco:

* Ograniczanie z systemu zewnętrznego, od którego zależy usługi Service Bus. Ograniczanie występuje z interakcji z zasobami magazynu i zasobów obliczeniowych.
* Problem dotyczący systemu, od którego zależy usługi Service Bus. Na przykład określona część magazynu mogą wystąpić problemy.
* Błąd usługi Service Bus w podsystemie pojedynczego. W takiej sytuacji węźle obliczeń można uzyskać w stanie niespójnym i należy ponownie uruchomić się, powoduje wszystkich jednostek służy ona saldo tooload tooother węzłów. To z kolei może spowodować krótkim przetwarzania komunikatów powolne.
* Błąd usługi Service Bus w obrębie centrum danych Azure. Jest to "poważnej awarii" w którym hello system jest nieosiągalny na kilka minut lub kilka godzin.

> [!NOTE]
> termin Hello **magazynu** może oznaczać magazynu Azure i SQL Azure.
> 
> 

Usługa Service Bus zawiera szereg metody ich rozwiązywania tych problemów. Hello w następujących sekcjach omówiono w nim poszczególnych problemów i ich odpowiednie środki zaradcze.

### <a name="throttling"></a>Ograniczanie przepływności
Z usługą Service Bus ograniczania umożliwia zarządzania szybkość współpracy wiadomości. Każdy węzeł poszczególne usługi Service Bus przechowuje wiele jednostek. Każdy z tych jednostek nawiązuje wymagań systemu hello pod względem Procesora, pamięci, magazynu i inne aspekty. Po wykryciu żadnego z tych aspektów użycia przekraczający zdefiniowanych progów, usługi Service Bus można odmówić danego żądania. obiekt wywołujący Hello uzyskuje [ServerBusyException] [ ServerBusyException] i ponownych prób po 10 sekundach.

Jako ograniczenie kod hello musi hello błąd odczytu i zatrzymuje wszystkie prób wiadomość hello co najmniej 10 sekund. Ponieważ hello błąd może wystąpić w części powitania klienta aplikacji oczekuje się, że każda niezależnie wykonuje hello logiki ponawiania próby. Kod Hello można zmniejszyć prawdopodobieństwo hello ograniczane przez włączenie partycjonowania na kolejka lub temat.

### <a name="issue-for-an-azure-dependency"></a>Problem dotyczący usługi Azure zależności
Inne składniki w obrębie platformy Azure od czasu do czasu może mieć problemy z usługi. Na przykład po uaktualnieniu systemu, w którym usługa Service Bus używa tego systemu tymczasowo może wystąpić zmniejszenie możliwości. toowork wokół tego rodzaju problemy, usługi Service Bus regularnie sprawdza i implementuje środki zaradcze. Efekty uboczne te czynniki są wyświetlane. Na przykład toohandle przejściowe problemy z magazynem, usługi Service Bus implementuje systemu, który pozwala spójnie toowork operacji wysyłania wiadomości. Powodu charakter toohello hello środki zaradcze wiadomość można podjąć tooappear minut too15 hello dotyczy kolejki lub subskrypcji i gotowość operacji odbioru. Ogólnie rzecz biorąc większość jednostek nie wystąpi ten problem. Jednak podane hello liczba jednostek w usłudze Service Bus na platformie Azure, to ograniczenie jest czasami potrzebne mały podzbiór klientów usługi Service Bus.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Błąd usługi Service Bus w podsystemie pojedynczego
Z dowolnej aplikacji okolicznościach może spowodować wewnętrznych składników usługi Service Bus toobecome niespójne. Gdy Usługa Service Bus wykrywa, zbiera dane z tooaid aplikacji hello w zdiagnozowaniu, co się stało. Po pobraniu danych hello, aplikacja hello jest uruchomiona ponownie w tooreturn próba jej tooa spójnego stanu. Ten proces odbywa się stosunkowo szybko i wyniki w jednostce znajdujących się niedostępny dla operacji się tooa toobe kilka minut, chociaż typowe dół razy są znacznie krótszy.

W takich przypadkach powitania klienta aplikacja generuje [System.TimeoutException] [ System.TimeoutException] lub [MessagingException] [ MessagingException] wyjątku. Usługa Service Bus zawiera ograniczenia tego problemu w formularzu hello logiki ponawiania próby automatycznego klienta. Po wyczerpaniu okres ponawiania hello i wiadomość hello nie zostanie dostarczona, można sprawdzić przy użyciu innych funkcji, takich jak [łączyć przestrzenie nazw][paired namespaces]. Przestrzenie nazw sparowanego mają inne uwagi, które zostały omówione w tym artykule.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Błąd usługi Service Bus w obrębie centrum danych Azure
najbardziej prawdopodobna przyczyna awarii w centrum danych Azure Hello jest niepowodzenia uaktualniania wdrożenia usługi Service Bus lub zależnego systemu. Miarę dojrzewania hello platformy, zmniejszył hello prawdopodobieństwo wystąpienia tego typu błędu. Błąd centrum danych również może się zdarzyć przyczyn, które obejmują następujące hello:

* Awaria elektrycznego (zasilacz i generowania zasilania znikają).
* Łączność (internet podziału między klientami a Azure).

W obu przypadkach awarii fizycznej lub włókna spowodował problem hello. toowork obejścia tego problemu i upewnij się, że nadal może wysyłać wiadomości, można użyć [łączyć przestrzenie nazw] [ paired namespaces] tooenable wiadomości toobe wysyłane tooa drugiej lokalizacji, podczas gdy lokalizacji głównej hello jest dobra ponownie. Aby uzyskać więcej informacji, zobacz [najlepszych rozwiązań dotyczących izolacji aplikacji przed awariami usługi Service Bus i awarii][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Sparowane przestrzenie nazw
Witaj [łączyć przestrzenie nazw] [ paired namespaces] funkcji obsługuje scenariusze, w którym jednostki magistrali usług lub wdrożenia w obrębie centrum danych staną się niedostępne. Gdy to zdarzenie występuje rzadko, systemów rozproszonych nadal muszą być przygotowane toohandle najgorszy scenariuszy przypadków. Zazwyczaj zdarzenie niektórych elementu, od którego zależy usługi Service Bus występują krótkoterminowej problem. dostępność aplikacji toomaintain podczas wystąpienia awarii usługi Service Bus użytkownicy mogą korzystać z dwóch osobnych obszarów nazw, najlepiej w centrach danych, toohost ich jednostek obsługi komunikatów. Witaj pozostałej części tej sekcji używa powitania po terminologii:

* Głównej przestrzeni nazw: hello przestrzeni nazw, z którą aplikacja współdziała do wysyłania i odbierania operacji.
* Dodatkowej przestrzeni nazw: hello przestrzeni nazw, która działa jako głównej przestrzeni nazw toohello kopii zapasowej. Logiki aplikacji nie wchodzi w interakcję z tą przestrzenią nazw.
* Interwał trybu failover: hello ilość czasu tooaccept normalne błędy przed aplikacji hello zmienia się z hello głównej przestrzeni nazw toohello dodatkowej przestrzeni nazw.

Łączyć przestrzenie nazw obsługują *wysyłania dostępności*. Wysłanie wiadomości powitania od możliwości toosend zachowuje dostępności. dostępności wysyłania toouse, aplikacja musi spełniać hello następujące wymagania:

1. Komunikaty są odbierane tylko z hello głównej przestrzeni nazw.
2. Komunikaty wysyłane tooa podane kolejka lub temat mogą dotrzeć poza kolejnością.
3. W ramach sesji może być momencie nadejścia nowych wiadomości poza kolejnością. To jest podział z normalną funkcjonalność sesji. Oznacza to, że aplikacja korzysta z sesji toologically grupy wiadomości.
4. Stan sesji jest utrzymywany tylko na powitania głównej przestrzeni nazw.
5. przejdzie w tryb online i rozpoczęcia akceptowanie komunikatów, zanim kolejki dodatkowej hello dostarcza wszystkich wiadomości do kolejki głównej hello mogą Hello kolejki głównej.

Hello w następujących sekcjach omówiono w nim hello interfejsów API, implementowania hello interfejsów API i przedstawiono przykładowy kod, który używa funkcji hello. Należy pamiętać, że rozliczeń wpływ na skojarzone z tą funkcją.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Witaj MessagingFactory.PairNamespaceAsync interfejsu API
Funkcja par nazw Hello obejmuje hello [PairNamespaceAsync] [ PairNamespaceAsync] metody na powitania [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] klasy:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Po ukończeniu zadania hello parowanie przestrzeni nazw hello jest również tooact gotowy na jakichkolwiek [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], lub [TopicClient] [ TopicClient] utworzone za pomocą hello [MessagingFactory] [ MessagingFactory] wystąpienia. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] jest hello klasę podstawową dla hello różnego rodzaju parowania, które są dostępne w [MessagingFactory] [ MessagingFactory] obiektu. Obecnie hello tylko w klasie pochodnej jest jedną o nazwie [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], który implementuje wymagań dotyczących dostępności wysyłania hello. [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] ma zestaw konstruktorów kompilacji na siebie. Spojrzenie na powitania konstruktora z hello większości parametrów, można zrozumieć zachowania hello hello innych konstruktorów.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Te parametry mają następujące znaczenie hello:

* *secondaryNamespaceManager*: zainicjowana [NamespaceManager] [ NamespaceManager] wystąpienie dodatkowej przestrzeni nazw hello tego hello [PairNamespaceAsync] [ PairNamespaceAsync] metoda może używać tooset hello dodatkowej nazw. Menedżer przestrzeni nazw Hello jest używane tooobtain hello Lista kolejek w przestrzeni nazw hello i toomake się, że istnieją hello wymagane zaległości kolejki. Jeśli te kolejki nie istnieją, są tworzone. [NamespaceManager] [ NamespaceManager] wymaga hello możliwości toocreate token z hello **Zarządzaj** oświadczeń.
* *messagingFactory*: hello [MessagingFactory] [ MessagingFactory] wystąpienia hello dodatkowej przestrzeni nazw. Witaj [MessagingFactory] [ MessagingFactory] toosend używany jest obiekt i, jeśli hello [EnableSyphon] [ EnableSyphon] właściwość jest ustawiona zbyt**true** , odbierania wiadomości z kolejki zaległości hello.
* *backlogQueueCount*: hello liczba zaległości kolejki toocreate. Ta wartość musi wynosić co najmniej 1. Podczas wysyłania wiadomości toohello zaległości, jeden z tych kolejek jest wybierany losowo. Jeśli ustawisz too1 wartość hello następnie tylko jedna kolejka kiedykolwiek można. Jeśli hello jeden zaległości kolejki generuje błędy, powitania klienta nie jest możliwe tootry kolejki zaległości różnych i może się nie powieść toosend wiadomości. Zalecamy ustawienie tej wartości toosome większą wartość i domyślne hello wartość too10. Można zmienić tej tooa wyższe lub niższe wartości w zależności od ilości danych aplikacji wysyła na dzień. Każdej kolejki zaległości może pomieścić się too5 GB wiadomości.
* *failoverInterval*: hello ilość czasu, w którym będzie akceptować błędów w głównej przestrzeni nazw hello przed przełączeniem żadnych pojedynczej jednostki za pośrednictwem toohello dodatkowej przestrzeni nazw. Tryb failover odbywa się na zasadzie jednostki przez jednostki. Jednostki w jednej przestrzeni nazw, często na żywo w różnych węzłach w ramach usługi Service Bus. Błąd w jednej jednostce nie oznacza awarii w innym. Tę wartość można ustawić za[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toohello toofailover dodatkowej natychmiast po awarii z pierwszą, nieprzejściowego. Błędy wyzwalających czasomierza trybu failover hello są [MessagingException] [ MessagingException] w których hello [IsTransient] [ IsTransient] właściwość ma wartość false, lub [System.TimeoutException][System.TimeoutException]. Pozostałe wyjątki, takich jak [unauthorizedaccessexception —] [ UnauthorizedAccessException] nie powodują trybu failover, ponieważ wskazują ten klient hello jest niepoprawnie skonfigurowany. A [ServerBusyException] [ ServerBusyException] jest nie trybu failover Przyczyna ponieważ wzorzec poprawne hello jest toowait 10 sekund, Wyślij wiadomość hello ponownie.
* *enableSyphon*: wskazuje, że tego konkretnego parowanie powinny również syphon wiadomości powitania dodatkowej przestrzeni nazw toohello wstecz głównej przestrzeni nazw. Ogólnie rzecz biorąc, aplikacji, które wysyłają komunikaty powinni ustawić wartość zbyt**false**; aplikacji, który odbiera komunikaty powinni ustawić wartość zbyt**true**. Hello przyczyną tego błędu jest często, czy mniej odbiorcy wiadomości od nadawcy wiadomości. W zależności od liczby hello odbiorcy możesz wybrać toohave pojedynczą aplikacją wystąpienia dojścia hello syphon obowiązków. Przy użyciu wiele odbiorników implikacje rozliczeń dla każdej kolejki zaległości.

toouse hello kodu, Tworzenie podstawowego [MessagingFactory] [ MessagingFactory] wystąpienie dodatkowej [MessagingFactory] [ MessagingFactory] wystąpienie pomocniczego [NamespaceManager] [ NamespaceManager] wystąpienia, a [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] wystąpienia. Wywołanie Hello może być tak proste, jak hello następujące:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Gdy hello zadanie zwrócone przez hello [PairNamespaceAsync] [ PairNamespaceAsync] ukończeniu metody, wszystko jest skonfigurowany i gotowy toouse. Przed zwróceniem hello zadanie może nie została ukończona wszystkie Praca w tle hello niezbędne do hello parowanie toowork prawo. W związku z tym nie należy uruchamiać wysyłania wiadomości do momentu zwraca hello zadań. W przypadku wystąpienia błędów, takich jak nieprawidłowych poświadczeń lub błąd toocreate hello zaległości kolejki te wyjątki będą zgłaszane po ukończeniu zadania hello. Po zwraca zadanie hello, sprawdź, czy kolejek hello zostały znalezione lub utworzone przez sprawdzenie hello [BacklogQueueCount] [ BacklogQueueCount] właściwości na Twojej [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] wystąpienia. Hello poprzedzających kodu tej operacji wygląda następująco:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello asynchroniczną obsługę wiadomości w usłudze Service Bus, przeczytaj więcej szczegółów na temat [łączyć przestrzenie nazw][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
