---
title: "aaaService — omówienie sieci szkieletowej niezawodnej podmiotów | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toohello usługi sieć szkieletowa modelu programowania Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Wprowadzenie tooService sieci szkieletowej Reliable Actors
Reliable Actors to platforma aplikacji sieci szkieletowej usług w oparciu hello [aktora wirtualnego](http://research.microsoft.com/en-us/projects/orleans/) wzorca. Hello niezawodnej API złośliwych użytkowników zapewnia jednowątkowe model programowania oparty na powitania skalowalność i niezawodność gwarancje udostępniane przez usługi sieć szkieletowa usług.

## <a name="what-are-actors"></a>Co to są złośliwych użytkowników?
Aktor jest jednostką izolowanym, niezależnie od zasobów obliczeniowych i stanu z jednowątkowego wykonywania. Witaj [wzorca aktora](https://en.wikipedia.org/wiki/Actor_model) to model obliczeniową dla systemów równoczesnych lub rozproszone, w którym dużej liczby uczestników te mogą być wykonywane jednocześnie i niezależnie od siebie nawzajem. Złośliwych użytkowników może komunikować się ze sobą i mogą utworzyć więcej złośliwych użytkowników.

### <a name="when-toouse-reliable-actors"></a>Gdy toouse Reliable Actors
Usługa sieci szkieletowej Reliable Actors jest implementacją wzorca projektowego hello aktora. Podobnie jak w przypadku dowolnego wzorcu projektowym oprogramowania hello decyzję, czy toouse określony wzorzec jest wykonywana w oparciu czy oprogramowania projektowania problem pasuje do wzorca hello.

Chociaż wzorca projektowego aktora hello może być dobrym tooa dopasowania liczba systemów rozproszonych problemy i scenariusze, dokładne rozważenie hello ograniczenia wzorca hello i wdrażanie framework hello, które muszą być wprowadzane. Stanowią ogólne wskazówki należy wziąć pod uwagę toomodel wzorca aktora hello problemów lub scenariuszu jeśli:

* Obszar problem obejmuje dużą liczbą (tysięcy lub więcej) jednostek mały, niezależne i izolowane stanu i logiki.
* Ma toowork z jednowątkowego obiektów, które nie wymagają znaczących interakcji z zewnętrznego składników, w tym badania stanu zestawu podmiotów.
* Swoich wystąpień aktora nie zablokuje wywołań nieprzewidywalne opóźnień wysyłając operacji We/Wy.

## <a name="actors-in-service-fabric"></a>Złośliwych użytkowników w sieci szkieletowej usług
W sieci szkieletowej usług, złośliwych użytkowników zostały wdrożone w ramach Reliable Actors hello: struktura aplikacji na podstawie wzorca aktora wbudowane nad [niezawodne usługi sieć szkieletowa usług](service-fabric-reliable-services-introduction.md). Każdej usługi niezawodnego aktora, jaki jest rzeczywiście podzielonym na partycje, stanowe niezawodnej usługi.

Każdy aktora jest zdefiniowany jako wystąpienie typu aktora, sposób identyczne toohello obiektu .NET jest wystąpieniem typu .NET. Na przykład może to być typ aktora, która implementuje funkcje hello kalkulatora i może istnieć wiele podmiotów tego typu rozproszonych w różnych węzłach w klastrze. Każdy taki aktora jest unikatowo identyfikowana przez identyfikator aktora.

### <a name="actor-lifetime"></a>Okres istnienia aktora
Sieć szkieletowa usług podmiotów są wirtualnych, co oznacza, że ich istnienia nie jest związany tootheir reprezentacji w pamięci. W związku z tym nie potrzebują oni toobe jawnie utworzone lub zniszczenia. środowisko uruchomieniowe Reliable Actors Hello automatycznie aktywuje hello aktora po raz pierwszy odbierze żądanie dla danego identyfikatora aktora. Jeśli aktora nie jest używany w danym okresie czasu, środowisko uruchomieniowe Reliable Actors hello pamięci zbiera hello obiektów w pamięci. Również zachowa wiedzy istnienia aktora hello konieczne toobe uaktywnić ponownie później. Aby uzyskać więcej informacji, zobacz [aktora cykl życia i odzyskiwanie pamięci](service-fabric-reliable-actors-lifecycle.md).

Ta warstwa abstrakcji okres istnienia aktora wirtualnego zawiera niektóre zastrzeżenia wyniku hello aktora wirtualnego modelu, a w rzeczywistości hello implementacji Reliable Actors w czasie odbiega od tego modelu.

* Aktor jest uaktywniany automatycznie (co powoduje aktora toobe obiektu skonstruowany) hello po raz pierwszy komunikat jest wysyłany identyfikator tooits aktora. Po pewnym opóźnieniem od czasu obiekt aktora hello jest bezużytecznych. W hello przyszłości ponownie, używając Identyfikatora aktora hello powoduje aktora nowego obiektu toobe skonstruowany. Okres istnienia obiektu hello outlives stanu aktora, gdy przechowywana w hello Menedżer stanu.
* Wywołaniem jakiejkolwiek jego metody aktora o identyfikatorze aktora aktywuje tego aktora. Z tego powodu aktora typy mają ich Konstruktor wywoływany niejawnie przez hello środowiska wykonawczego. Kod klienta nie można przekazać konstruktora typu parametry toohello aktora, mimo że parametry mogą być przekazywane konstruktora toohello aktora przez usługę hello. wynik Hello jest czy uczestników, mogą być zbudowane w stanie częściowo zainicjowany przez hello razem, gdy inne metody są wywoływane, jeśli aktora hello wymaga parametrów inicjowania z powitania klienta. Brak punktu wejścia jednym aktywacji hello aktora z powitania klienta.
* Mimo że Reliable Actors niejawnie Tworzenie obiektów aktora; masz tooexplicitly możliwości hello usunąć aktora i jego stan.

### <a name="distribution-and-failover"></a>Dystrybucji i trybu failover
tooprovide skalowalność i niezawodność sieci szkieletowej usług dystrybuuje złośliwych użytkowników w całej hello klastra i automatycznie migruje węzłów toohealthy te zgodnie z potrzebami. Jest to Abstrakcja za pośrednictwem [podzielonym na partycje, stanowe niezawodnej usługi](service-fabric-concepts-partitioning.md). Dystrybucji, skalowalności, niezawodności i automatycznej pracy awaryjnej są dostarczane ze względu na fakt hello podmiotów działają wewnątrz stanowe niezawodnej usługi o nazwie hello *usługi aktora*.

Podmioty są rozproszone na partycji hello hello usługi aktora, a te partycje są rozproszone na powitania węzłów w klastrze usługi sieć szkieletowa usług. Każda partycja usługi zawiera zestaw złośliwych użytkowników. Usługa Service Fabric zarządza dystrybucji i pracy awaryjnej hello partycji usługi.

Na przykład wdrożenie usługi aktora z partycjami dziewięć toothree, który węzłów za pomocą hello domyślne aktora partycji umieszczania może być dystrybuowane thusly:

![Niezawodne dystrybucji złośliwych użytkowników][2]

Witaj Framework aktora zarządza ustawieniami partycji schemat i klawisz zakresu dla Ciebie. Upraszcza niektóre opcje, ale również zajmuje kilka brany pod uwagę:

* Niezawodne usługi umożliwia toochoose schemat partycjonowania klucza zakresu (w przypadku używania zakres schemat partycjonowania), a liczba partycji. Reliable Actors jest schemat partycjonowania toohello ograniczony zakres (hello jednolity schemat Int64) i wymaga się, że używasz pełnego zakresu klucza hello Int64.
* Domyślnie podmiotów losowo są umieszczane w partycji co uniform dystrybucji.
* Ponieważ podmiotów losowo znajdują się, powinien oczekiwano, że operacje aktora zawsze wymagają komunikacji w sieci, w tym serializacji i deserializacji obiektu danych wywołania metody, ponoszenia opóźnienia i koszty.
* W zaawansowanych scenariuszach jest możliwe toocontrol aktora partycji umieszczania przy użyciu aktora Int64 identyfikatorów, które mapują toospecific partycji. Jednak to tak może spowodować niezrównoważonej dystrybucji podmiotów na partycje.

Więcej informacji dotyczących sposobu usługi aktora są podzielone na partycje, można znaleźć zbyt[partycjonowania pojęcia osób](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Komunikacja aktora
Interakcje aktora są definiowane w interfejs, który jest współużytkowany przez aktora hello, który implementuje interfejs hello i powitania klienta, który pobiera serwer proxy aktora tooan za pośrednictwem hello tego samego interfejsu. Ponieważ ten interfejs jest używane tooinvoke metody aktora asynchronicznie, co metoda w interfejsie hello musi być zwracanie zadań.

Wywołań metod i ich odpowiedzi ostatecznie spowodować żądania sieciowe klastra hello, tak hello argumentów i typy wyników hello zadań hello czy zwracają muszą umożliwiać serializację za pomocą platformy hello. W szczególności muszą być [serializacji kontraktu danych](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>Serwer proxy aktora Hello
Interfejs API klienta Reliable Actors Hello zapewnia komunikację między wystąpieniem aktora i klienta aktora. toocommunicate z aktorem, klient tworzy aktora obiekt serwera proxy, który implementuje interfejs aktora hello. powitania klienta współdziała z aktora hello za wywoływanie metod na powitania obiekt serwera proxy. Serwer proxy aktora Hello może służyć do komunikacji klient aktora i aktora aktora.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Należy pamiętać, że hello dwóch rodzajów informacji używane obiekt serwera proxy aktora hello toocreate są hello aktora identyfikator i nazwa aplikacji hello. Identyfikator aktora Hello unikatowo identyfikuje aktora hello, podczas gdy nazwa aplikacji hello identyfikuje hello [aplikacji usługi Service Fabric](service-fabric-reliable-actors-platform.md#application-model) wdrożonym hello aktora.

Witaj `ActorProxy`(C#) / `ActorProxyBase`klasy (Java) po stronie klienta hello wykonuje hello niezbędne rozpoznawania toolocate hello aktora według Identyfikatora i otwórz kanał komunikacji z nim. Ponowną toolocate hello aktora w przypadku hello błędy komunikacji oraz tryb failover. W związku z tym dostarczanie komunikatów ma hello następujące cechy:

* Dostarczanie komunikatów to optymalne rozwiązanie.
* Złośliwych użytkowników może odbierać komunikaty zduplikowane z hello tego samego klienta.

### <a name="concurrency"></a>Współbieżność
środowisko uruchomieniowe Reliable Actors Hello udostępnia model prosty dostęp za pośrednictwem Włącz do uzyskiwania dostępu do metody aktora. Oznacza to, że nie więcej niż jeden wątek może być aktywny wewnątrz kodu obiektu aktora w dowolnym momencie. Włącz dostęp przez Internet jest znacznie ułatwione równoczesnych systemów jako nie istnieje potrzeba mechanizmów synchronizacji dla dostępu do danych. Ponadto oznacza to, że systemy musi zostać zaprojektowana z uwagi dotyczące hello jednowątkowym dostępu charakter każdego wystąpienia aktora.

* Aktora pojedynczego wystąpienia nie może przetworzyć więcej niż jedno żądanie naraz. Wystąpienie aktora może spowodować wąskie gardło przepływności, jeżeli jest oczekiwany toohandle równoczesnych żądań.
* Złośliwych użytkowników można zakleszczenie od siebie wzajemnie, jeśli żądanie cykliczne między dwoma uczestnikami podczas zewnętrznych żądań tooone hello złośliwych użytkowników jednocześnie. Hello aktora środowiska uruchomieniowego zostanie automatycznie czas na aktora wywołuje i zgłosić wyjątek toohello wywołującego toointerrupt sytuacji możliwe zakleszczenie.

![Niezawodna komunikacja złośliwych użytkowników][3]

#### <a name="turn-based-access"></a>Włącz dostęp przez Internet
Włącz składa się z hello ukończenie metodę aktora w żądaniu tooa odpowiedzi od innych uczestników lub klientów lub hello ukończenie [czasomierza/monitu](service-fabric-reliable-actors-timers-reminders.md) wywołania zwrotnego. Mimo że te metody i wywołania zwrotne są asynchroniczne, hello złośliwych użytkowników w czasie wykonywania nie interleave je. Włącz muszą być całkowicie przed Włącz nowe jest dozwolone. Innymi słowy aktora metody lub czasomierza/monitu wywołania zwrotnego, które jest aktualnie wykonywany musi być w pełni ukończone przed metodą tooa wywołania lub wywołania zwrotnego jest dozwolone. Metoda lub wywołania zwrotnego jest uważany za toohave Zakończono wykonanie hello zwrócił z metody hello lub wywołania zwrotnego i hello zadań zwróconych przez metodę hello lub wywołanie zwrotne zostało zakończone. Warto akcentowania się, że ten współbieżności opartej na włączanie jest przestrzegana nawet między różnymi metodami, czasomierze i wywołania zwrotne.

Hello złośliwych użytkowników w czasie wykonywania wymusza współbieżności opartej na ruch przez uzyskiwanie blokady dla aktora początku hello Włącz i zwalniania blokady hello na końcu hello hello włączyć. W związku z tym współbieżności opartej na włączanie są wymuszane na podstawie na aktora, a nie przez złośliwych użytkowników. Metody aktora i wywołania zwrotne czasomierza/monitu mogą być wykonywane jednocześnie imieniu uczestników.

Witaj poniższy przykład przedstawia hello powyżej pojęcia. Należy wziąć pod uwagę aktora typu, który implementuje dwóch metod asynchronicznych (powiedzieć *metoda1* i *metoda2*), a czasomierza oraz monitu. Hello poniższym diagramie przedstawiono oś czasu wykonywania hello tych metod i wywołania zwrotne w imieniu dwóch uczestników (*ActorId1* i *ActorId2*) należących toothis typ aktora.

![Niezawodne podmiotów środowiska uruchomieniowego Włącz współbieżności opartej i dostępem][1]

Ten diagram jest zgodna z konwencjami te:

* Każdy pionowym wierszem przedstawia przepływ logiczny hello wykonania metody lub wywołania zwrotnego w imieniu aktora określonego.
* zdarzenia Hello oznaczone w każdym wierszu pionowy wystąpić w kolejności chronologicznej z nowszych zdarzeń występujących poniżej starsze.
* Różne kolory odpowiednich osób toodifferent osi czasu.
* Wyróżnianie to używane tooindicate hello duration, dla których hello blokady dla aktora jest przechowywany w imieniu metody lub wywołania zwrotnego.

Niektóre tooconsider ważne kwestie:

* Gdy *metoda1* jest wykonywane dla *ActorId2* w żądaniu tooclient odpowiedzi *xyz789*, inne żądanie klienta (*abc123*) dociera, który wymaga także *metoda1* toobe wykonywane przez *ActorId2*. Jednak hello drugiego wykonywania *metoda1* nie zaczyna się przed zakończeniem wykonywania wcześniejsze hello. Podobnie, przypomnienia zarejestrowany przez *ActorId2* uruchamiany podczas *metoda1* jest wykonywana w żądaniu tooclient odpowiedzi *xyz789*. Witaj monitu wywołania zwrotnego jest wykonywany tylko po obu wykonania *metoda1* są spełnione. Wszystko to jest ze względu na podstawie tooturn współbieżności wymuszany dla *ActorId2*.
* Podobnie, współbieżności opartej na ruch jest również wymuszane dla *ActorId1*, jak to pokazano przez wykonanie hello *metoda1*, *metoda2*, i hello wywołanie zwrotne czasomierza zastępczy *ActorId1* wykonywane w sposób szeregowego.
* Wykonywanie *metoda1* zastępczy *ActorId1* pokrywa się z jej wykonanie w imieniu *ActorId2*. Jest to spowodowane współbieżności opartej na włączanie są wymuszane tylko w obrębie aktora, a nie przez złośliwych użytkowników.
* W niektórych wykonania metody/wywołania zwrotnego hello hello `Task`(C#) / `CompletableFuture`(Java) zwracane przez zakończenie metody/wywołania zwrotnego hello, po powrocie hello metody. W niektórych innych hello asynchronicznej operacji zostało już zakończone przez czas hello zwraca metody hello/wywołania zwrotnego. W obu przypadkach blokady dla aktora hello jest zwalniany dopiero po zwraca zarówno hello metody/wywołania zwrotnego i zakończeniu operacji asynchronicznej hello.

#### <a name="reentrancy"></a>Wielobieżność
środowisko uruchomieniowe podmiotów Hello umożliwia ponowne wejście domyślnie. Oznacza to, że jeśli metoda aktora *aktora A* wywołuje metodę dla *B aktora*, który z kolei wywołuje innej metody w *aktora A*, że metoda jest dozwolona toorun. Jest to, ponieważ jest ona częścią hello tego samego kontekstu logicznej łańcuch wywołań. Wszystkie wywołania zegara i monitu rozpoczynać hello nowy kontekst wywołania logiczne. Zobacz hello [wielobieżność Reliable Actors](service-fabric-reliable-actors-reentrancy.md) więcej szczegółów.

#### <a name="scope-of-concurrency-guarantees"></a>Zakres gwarancji współbieżności
środowisko uruchomieniowe podmiotów Hello zapewnia te gwarancje współbieżności w sytuacjach, w którym kontroluje hello wywołania tych metod. Na przykład zapewnia te gwarancje dla wywołań metod hello, które są wykonywane w żądaniu klienta tooa odpowiedzi, a także wywołania zwrotne czasomierza i przypomnienia. Jeśli jednak hello aktora kodu bezpośrednio wywołuje tych metod poza mechanizmów hello udostępnianych przez hello złośliwych użytkowników w czasie wykonywania, następnie hello środowiska uruchomieniowego nie zawiera żadnej gwarancji współbieżności. Na przykład jeśli hello metoda jest wywoływana w kontekście hello niektórych zadań, która nie jest skojarzona z zadaniem hello zwracane przez metody aktora hello, następnie hello runtime nie może zagwarantować współbieżności. Jeśli metoda hello jest wywoływana z wątku tego aktora hello tworzy na jego własnej, a następnie środowiska uruchomieniowego hello także nie może zagwarantować współbieżności. W związku z tym operacje w tle tooperform złośliwych użytkowników należy używać [aktora czasomierze i przypomnieniami aktora](service-fabric-reliable-actors-timers-reminders.md) który przestrzegać współbieżności opartej na ruch.

## <a name="next-steps"></a>Następne kroki
* Rozpoczynanie pracy przez utworzenie pierwszej usługi Reliable Actors:
   * [Wprowadzenie do korzystania z Reliable Actors na platformie .NET](service-fabric-reliable-actors-get-started.md)
   * [Wprowadzenie do korzystania z Reliable Actors na języku Java](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
