---
title: "Omówienie funkcji aaaAzure usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Omówienie i szczegółowe informacje o funkcjach usługi Azure Event Hubs"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Omówienie funkcji usługi Event Hubs

Usługa Azure Event Hubs jest skalowalna zdarzeń, usługa, która wysyła strumień i przetwarza duże ilości zdarzenia i dane, z małymi opóźnieniami i wysoką niezawodnością przetwarzania. Zobacz [co to jest usługa Event Hubs?](event-hubs-what-is-event-hubs.md) szczegółowe omówienie hello usługi.

W tym artykule opiera się na powitania informacji w hello [omówienie](event-hubs-what-is-event-hubs.md)i zawiera szczegółowe informacje techniczne i wdrożenia o składnikach usługi Event Hubs i funkcje.

## <a name="event-publishers"></a>Wydawcy zdarzeń

Każda jednostka, która wysyła Centrum zdarzeń tooan danych jest producent zdarzeń lub *wydawca zdarzeń*. Wydawcy zdarzeń mogą publikować zdarzenia przy użyciu protokołu HTTPS lub AMQP 1.0. Wydawcy zdarzeń Użyj tooidentify tokenu dostępu sygnatury dostępu Współdzielonego się tooan Centrum zdarzeń i można mieć unikatową tożsamość lub użyj wspólnego tokenu sygnatury dostępu Współdzielonego.

### <a name="publishing-an-event"></a>Publikowanie zdarzenia

Zdarzenie można opublikować za pośrednictwem protokołu AMQP 1.0 lub HTTPS. Usługa Event Hubs zapewnia [bibliotek klienta i klasy](event-hubs-dotnet-framework-api-overview.md) publikowania Centrum zdarzeń tooan zdarzeń od klientów platformy .NET. W przypadku innych środowisk uruchomieniowych i platform można używać dowolnego klienta protokołu AMQP 1.0, na przykład [Apache Qpid](http://qpid.apache.org/). Zdarzenia można publikować indywidualnie lub w partiach. Jedna publikacja (wystąpienie danych zdarzeń) ma limit wynoszący 256 KB, niezależnie od tego, czy jest to pojedyncze zdarzenie, czy partia. Publikowanie zdarzenia większych niż ten próg powoduje błąd. Jest najlepszym rozwiązaniem dla wydawców toobe niebranie pod uwagę partycji w Centrum zdarzeń hello i określ tooonly *klucza partycji* (wprowadzony w następnej sekcji hello) lub tożsamości za pomocą ich tokenu sygnatury dostępu Współdzielonego.

Witaj wybór toouse protokołu AMQP lub HTTPS jest toohello określonego scenariusza użycia. Protokół AMQP wymaga ustanowienia trwałego gniazda dwukierunkowego hello dodanie tootransport zabezpieczeń na poziomie (TLS) lub SSL/TLS. Protokół AMQP ma wyższe koszty sieci podczas inicjowania sesji hello jednak HTTPS wymaga protokołu SSL dodatkowe obciążenie dla każdego żądania. Protokół AMQP charakteryzują się wyższą wydajnością dla częstych wydawców.

![Usługa Event Hubs](./media/event-hubs-features/partition_keys.png)

Usługa Event Hubs zapewnia, że wszystkie zdarzenia udostępnianie wartość klucza partycji są dostarczane w kolejności i toohello sam partycji. Jeśli klucze partycji są używane z zasadami wydawcy, następnie hello tożsamości wydawcy hello i hello wartość klucza partycji hello muszą być zgodne. W przeciwnym razie wystąpi błąd.

### <a name="publisher-policy"></a>Zasady wydawcy

Usługa Event Hubs umożliwia szczegółową kontrolę nad wydawcami zdarzeń za pomocą *zasad wydawcy*. Zasady wydawcy to funkcje środowiska wykonawczego toofacilitate dużej liczby niezależnych wydawców zdarzeń. Dzięki zasadom wydawcy każdy wydawca używa swojego unikatowego identyfikatora podczas publikowania zdarzenia tooan Centrum zdarzeń, przy użyciu następującego mechanizmu hello:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

Nie masz toocreate nazw wydawców, ale muszą one odpowiadać tokenu sygnatury dostępu Współdzielonego hello używany podczas publikowania zdarzenia, w kolejności tooensure niezależnych tożsamości wydawcy. Podczas używania zasad wydawcy, hello **PartitionKey** wartość toohello nazwę wydawcy. toowork poprawnie, te wartości muszą być zgodne.

## <a name="capture"></a>Przechwytywanie

[Przechwyć centra zdarzeń](event-hubs-capture-overview.md) umożliwia przesyłanie strumieniowe danych w usłudze Event Hubs hello przechwytywania tooautomatically i zapisaniu tooyour wybór konta magazynu obiektów Blob lub konta usługi Azure Data Lake usługi. Można włączyć przechwytywania z hello portalu Azure, a następnie określ minimalny rozmiar i przechwytywania hello tooperform okno czasu. Za pomocą przechwytywania centra zdarzeń, można określić własne konto magazynu obiektów Blob Azure i kontener lub konta usługi Azure Data Lake usługi, które jest używane toostore hello przechwycone dane. Przechwycone dane są zapisywane w formacie Apache Avro hello.

## <a name="partitions"></a>Partycje

Usługa Event Hubs zapewnia strumieniowe przesyłanie za pomocą partycjonowanego wzorca odbiorców w ramach którego każdy odbiorca odczytuje tylko konkretny podzbiór, lub partycję, strumienia wiadomości powitania komunikatów. Ten wzorzec umożliwia skalowanie w poziomie przetwarzania zdarzeń oraz udostępnia inne funkcje dotyczące strumienia, które są niedostępne w przypadku kolejek i tematów.

Partycja to uporządkowana sekwencja zdarzeń przechowywana w centrum zdarzeń. Nadejściu nowszych zdarzeń są dodawane toohello na końcu sekwencji. Partycję można traktować jako „dziennik zatwierdzania”.

![Usługa Event Hubs](./media/event-hubs-features/partition.png)

Usługi Event Hubs przechowuje dane przez skonfigurowany czas przechowywania, która dotyczy wszystkich partycji w Centrum zdarzeń hello. Zdarzenia wygasają czasowo — nie można ich jawnie usunąć. Ponieważ partycje są niezależne i zawierają własne sekwencje danych, często rosną z różną szybkością.

![Usługa Event Hubs](./media/event-hubs-features/multiple_partitions.png)

Hello liczby partycji jest określany podczas tworzenia i musi należeć do zakresu od 2 do 32. Liczba partycji Hello nie jest włączone, więc skali długoterminowej należy rozważyć podczas ustawiania liczby partycji. Partycje są mechanizm organizacji danych, który dotyczy toohello równoległości podrzędne wymaganym podczas używania aplikacji. Hello liczbę partycji w Centrum zdarzeń bezpośrednio dotyczy toohello liczbę jednoczesnych czytników spodziewasz się toohave. Skontaktowanie się z team centra zdarzeń hello może zwiększyć hello liczby partycji przekracza 32.

Partycje są możliwe do identyfikacji i mogą być wysyłane toodirectly, wysyłanie bezpośrednio tooa partycji nie jest zalecane. Zamiast tego można użyć konstrukcji wyższego poziomu wprowadzonych w hello [wydawca zdarzeń](#event-publishers) i [pojemności](#capacity) sekcje. 

Partycje są wypełnione sekwencją danych zdarzenia, które zawiera treść hello hello zdarzenia, zbiór właściwości zdefiniowane przez użytkownika i metadane, takie jak jego przesunięcie w partycji hello i numer w sekwencji strumienia hello.

Aby uzyskać więcej informacji o partycji i hello kompromis między dostępności i niezawodności, zobacz hello [Podręcznik programowania usługi Event Hubs](event-hubs-programming-guide.md#partition-key) i hello [dostępności i spójności w usłudze Event Hubs](event-hubs-availability-and-consistency.md) artykułu .

### <a name="partition-key"></a>Klucz partycji

Można użyć [klucza partycji](event-hubs-programming-guide.md#partition-key) toomap danych zdarzeń przychodzących na określone partycje hello w celu organizowania danych. Witaj klucz partycji to wartość dostarczone przez nadawcę przekazywana do Centrum zdarzeń. Jest on przetworzony przez statyczną funkcję tworzenia skrótu, który tworzy hello przypisania partycji. Jeśli nie określisz klucza partycji podczas publikowania zdarzenia, używane jest przypisanie działania okrężnego.

Hello wydawca zdarzeń ma informacje tylko o kluczu partycji, są publikowane hello partycji toowhich hello zdarzenia. To oddzielenie klucza od partycji powoduje hello nadawca nie musi tooknow zbyt dużo o przetwarzaniu podrzędnym hello. Na urządzeniu lub użytkownikowi unikatową tożsamość sprawia, że stanowi dobry klucz partycji, ale inne atrybuty, takie jak lokalizacja geograficzna może być również używane toogroup powiązanych zdarzeń w jedną partycję.

## <a name="sas-tokens"></a>Tokeny sygnatur dostępu współdzielonego

Usługa Event Hubs używa *sygnatury dostępu współdzielonego*, które są dostępne na poziomie koncentratora hello przestrzeń nazw i zdarzeń. Token sygnatury dostępu współdzielonego jest generowany na podstawie klucza sygnatury dostępu współdzielonego i jest skrótem SHA adresu URL zakodowanym w określonym formacie. Przy użyciu nazwy hello hello klucza (zasady) i tokenu hello, Event Hubs można ponownie wygenerować skrót hello i w związku z tym uwierzytelniać hello nadawcy. Zwykle tokeny sygnatury dostępu współdzielonego dla wydawców zdarzeń są tworzone jedynie z uprawnieniami do **wysyłania** w określonym centrum zdarzeń. Ten mechanizm adresu URL tokenu sygnatury dostępu Współdzielonego stanowi podstawę hello identyfikacji wydawcy wprowadzoną w hello zasad wydawcy. Aby uzyskać więcej informacji na temat pracy z sygnaturą dostępu współdzielonego, zobacz [Shared Access Signature Authentication with Service Bus](../service-bus-messaging/service-bus-sas.md) (Uwierzytelnianie za pomocą sygnatury dostępu współdzielonego przy użyciu usługi Service Bus).

## <a name="event-consumers"></a>Odbiorcy zdarzeń

Każda jednostka, która odczytuje dane zdarzenia z centrum zdarzeń, jest *odbiorcą zdarzenia*. Połączenie wszystkich użytkowników usługi Event Hubs za pomocą sesji protokołu AMQP 1.0 hello i zdarzenia są dostarczane za pośrednictwem sesji hello staną się one dostępne. Witaj, klient nie potrzebuje toopoll dostępność danych.

### <a name="consumer-groups"></a>Grupy odbiorców

Witaj mechanizmu publikowania/subskrypcji usługi Event hubs jest włączany za pomocą *grupy konsumentów*. Grupa odbiorców stanowi widok (stan, pozycja lub przesunięcie) całego centrum zdarzeń. Grupy konsumentów włączyć wiele aplikacji odbiorczych tooeach mieć osobny widok strumienia zdarzeń hello i tooread hello strumienia niezależnie we własnym tempie i z własnych przesunięcia.

W architekturze przetwarzania strumieni każda aplikacja podrzędna tooa grupy odbiorców. Jeśli chcesz pamięci masowej termin toolong toowrite zdarzeń, ta aplikacja edytora magazynu odpowiada grupie odbiorców. Przetwarzanie złożonych zdarzeń może być wtedy wykonywane przez inną, oddzielną grupę odbiorców. Dostęp do partycji można uzyskać tylko za pośrednictwem grupy odbiorców. Może istnieć maksymalnie 5 współbieżnych czytników na partycji dla każdej grupy konsumentów; jednak **zaleca się, że istnieje tylko jeden odbiornik active na partycji dla każdej grupy odbiorców**. W Centrum zdarzeń zawsze jest domyślna grupa odbiorców i tworzenia grup konsumentów too20 dla Centrum zdarzeń warstwy standardowa.

Witaj Oto przykłady Konwencji identyfikatora URI grupy odbiorców hello:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Witaj poniższej ilustracji przedstawiono architekturę przetwarzania strumienia usługi Event Hubs hello:

![Usługa Event Hubs](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Przesunięcia strumienia

*Przesunięcie* jest hello pozycja zdarzenia w partycji. Przesunięcie można traktować jako kursor po stronie klienta. Witaj przesunięcie jest bajtem numerowanie hello zdarzenia. To przesunięcie umożliwia zdarzeń toospecify konsumenta (czytnik) punktu w strumieniu zdarzeń hello, od którego ma toobegin odczytywanie zdarzeń. Przesunięcie hello można określić jako sygnaturę czasową lub wartość przesunięcia. Odbiorcy są zobowiązani do przechowywania własnych wartości przesunięcia poza usługą Event Hubs hello. W ramach partycji każde zdarzenie zawiera przesunięcie.

![Usługa Event Hubs](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Tworzenie punktów kontrolnych

*Tworzenie punktów kontrolnych* jest procesem, za pomocą którego czytniki oznaczają lub zatwierdzają swoją pozycję w sekwencji zdarzeń partycji. Tworzenie punktów kontrolnych spoczywa hello powitania klienta i występuje na podstawie każdej partycji w obrębie grupy odbiorców. Tę odpowiedzialność oznacza, że dla każdej grupy odbiorców każdy czytnik partycji musi śledzić bieżącej pozycji w strumieniu zdarzeń hello i może poinformować usługi hello gdy uzna, strumień danych hello pełną.

Jeśli czytnik rozłączy się od partycji, po swoim ponownym połączeniu rozpoczyna odczyt punktu kontrolnego hello, który został wcześniej przesłany przez hello ostatni czytnik tej partycji w danej grupie odbiorców. Gdy hello czytnik nawiązuje połączenie, przekazuje tego przesunięcia toohello zdarzenia koncentratora toospecify hello lokalizacji które odczytu toostart. W ten sposób można użyć procesu tworzenia punktów kontrolnych tooboth oznaczenia zdarzeń jako "ukończona" przez aplikacje podrzędne, a występuje tooprovide odporności, jeśli na pracę awaryjną między czytnikami działającymi na różnych komputerach. Są to dane tooolder tooreturn możliwe, określając niższe przesunięcie z tego procesu tworzenia punktów kontrolnych. Dzięki temu mechanizmowi tworzenie punktów kontrolnych zapewnia zarówno odporność na pracę w trybie failover, jak i powtarzanie strumienia zdarzeń.

### <a name="common-consumer-tasks"></a>Typowe zadania odbiorców

Wszystkie usługi Event Hubs konsumentów połączenie za pomocą sesji protokołu AMQP 1.0, stan dwukierunkowy kanał komunikacji. Każda partycja zawiera sesję protokołu AMQP 1.0, która ułatwia transport zdarzeń rozdzielonych według partycji hello.

#### <a name="connect-tooa-partition"></a>Połącz tooa partycji

Łącząc toopartitions jest typowe toouse praktyki dzierżawa mechanizm toocoordinate czytnika połączeń toospecific partycji. Dzięki temu możliwe jest dla każdej partycji w konsumenta grupy toohave tylko jeden aktywny czytnik. Tworzenie punktów kontrolnych, dzierżawę i zarządzania nimi czytników są uproszczone przy użyciu hello [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) klasy dla klientów platformy .NET. Witaj hosta procesora zdarzeń to inteligentny agent odbiorcy.

#### <a name="read-events"></a>Zdarzenia odczytywania

Po otwarciu sesji protokołu AMQP 1.0 i łącze dla określonej partycji, zdarzenia są dostarczane klienta toohello protokołu AMQP 1.0 przez hello usługi Event Hubs. Ten mechanizm dostarczania zapewnia wyższą przepływność i mniejsze opóźnienia niż mechanizmy oparte na ściąganiu, na przykład HTTP GET. Zdarzenia są wysyłane toohello klienta, każde wystąpienie danych zdarzenia zawiera ważne metadane, takie jak hello przesunięcie i numer sekwencji, które są używane toofacilitate tworzenia punktów kontrolnych sekwencji zdarzeń hello.

Dane zdarzenia:
* Przesunięcie
* Numer sekwencyjny
* Treść
* Właściwości użytkownika
* Właściwości systemu

To przesunięcie hello toomanage Twojego odpowiedzialności.

## <a name="capacity"></a>Pojemność

Usługa Event Hubs ma wysoce Skalowalna architektura równoległa i istnieje kilka kluczowych czynników tooconsider podczas doboru wielkości i skalowania.

### <a name="throughput-units"></a>Jednostki przepływności

Witaj pojemność przepływności usługi Event hubs jest kontrolowana przez *jednostek przepływności*. Jednostki przepływności to zakupione wcześniej jednostki pojemności. Pojedyncza jednostka przepływności obejmuje następujące pojemności hello:

* Transfer danych przychodzących: się too1 MB na sekundę lub 1000 zdarzeń na sekundę (zależności miało miejsce wcześniej)
* Transfer danych wychodzących: się too2 MB na sekundę

Poza pojemność hello hello zakupionych jednostek przepływności, transfer danych przychodzących jest ograniczany i [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) jest zwracany. Transfer danych wychodzących nie generowania wyjątków ograniczania przepływności, ale jest nadal ograniczone toohello pojemność hello zakupionych jednostek przepływności. Jeśli wystąpią wyjątki szybkości publikowania lub są oczekiwane toosee większy transfer danych wychodzących, należy się toocheck liczbę jednostek przepływności zakupionych dla przestrzeni nazw hello. Możesz zarządzać jednostek przepływności na powitania **skali** bloku hello przestrzeniach nazw hello [portalu Azure](https://portal.azure.com). Można również zarządzać jednostek przepływności, programowo przy użyciu hello [interfejsów API centra zdarzeń](event-hubs-api-overview.md).

Jednostki przepływności są rozliczane co godzinę i są kupowane wcześniej. Po zakupieniu jednostki przepływności są rozliczane za co najmniej jedną godzinę. W górę too20 jednostek przepływności można zakupić dla przestrzeni nazw usługi Event Hubs i są współdzielone przez wszystkie usługi Event Hubs w przestrzeni nazw hello.

Można kupić więcej jednostek przepływności w blokach po 20 jednostek przepływności too100, kontaktując się z pomocy technicznej platformy Azure. Ponadto możesz kupować bloki po 100 jednostek przepływności.

Firma Microsoft zaleca, aby równoważyć przepływności jednostki i partycji tooachieve optymalnej skali. Jedna partycja ma maksymalną skalę wynoszącą jedną jednostkę przepływności. Witaj liczba jednostek przepływności powinna być mniejsza lub równa toohello liczbę partycji w Centrum zdarzeń.

Aby uzyskać szczegółowe informacje o cenach centra zdarzeń, zobacz [cennik usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat usługi Event Hubs odwiedź hello następującego łącza:

* Wprowadzenie do [usługi Event Hubs — samouczek][Event Hubs tutorial]
* [Przewodnik programowania w usłudze Event Hubs](event-hubs-programming-guide.md)
* [Availability and consistency in Event Hubs](event-hubs-availability-and-consistency.md) (Dostępność i spójność w usłudze Event Hubs)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)
* [Przykłady centra zdarzeń][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Przykłady centra zdarzeń]: https://github.com/Azure/azure-event-hubs/tree/master/samples
