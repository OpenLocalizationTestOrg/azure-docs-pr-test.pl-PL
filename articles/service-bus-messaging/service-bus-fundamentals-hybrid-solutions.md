---
title: "aaaOverview podstawy usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toousing usługi Service Bus tooconnect oprogramowania tooother aplikacjami platformy Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure Service Bus

Czy aplikacja lub usługa działa w chmurze hello lub lokalnie, często wymaga toointeract z innych aplikacji lub usług. tooprovide toodo szeroko użyteczny sposób oferty, Microsoft Azure Service Bus. W tym artykule analizuje tę technologię, opisuje, co to jest i dlaczego warto toouse go.

## <a name="service-bus-fundamentals"></a>Podstawy usługi Service Bus

Różne sytuacje wymagają różnych stylów komunikacji. Czasami umożliwienie aplikacji wysyłania i odbierania komunikatów przy użyciu prostej kolejki jest hello najlepszym rozwiązaniem. W innych sytuacjach zwykła kolejka nie wystarcza i lepszym rozwiązaniem jest kolejka z mechanizmem publikowania i subskrybowania. W niektórych przypadkach potrzebne jest jedynie połączenie między aplikacjami, a kolejki nie są wymagane. Usługa Service Bus udostępnia wszystkie trzy opcje umożliwiające toointeract Twojej aplikacji na kilka różnych sposobów.

Usługa Service Bus to usługa w chmurze wielodostępne, co oznacza, że usługa hello jest współużytkowana przez wielu użytkowników. Każdy użytkownik, taki jak Twórca aplikacji tworzy *przestrzeni nazw*, następnie definiuje mechanizmy komunikacji hello potrzebne w tej przestrzeni nazw. Rysunek 1 pokazuje jak wygląda ta architektura.

![][1]

**Rysunek 1: Usługa Service Bus udostępnia usługę wielodostępną dla połączenia aplikacji za pośrednictwem hello chmury.**

W przestrzeni nazw można używać jednego lub większej liczby wystąpień trzech różnych mechanizmów komunikacji, z których każdy łączy aplikacje w inny sposób. dostępne są następujące opcje Hello:

* *Kolejki*, które umożliwiają komunikację jednokierunkową. Każda kolejka działa jako pośrednik (nazywany czasem *brokerem*), który przechowuje wysyłane wiadomości, dopóki nie zostaną odebrane. Każdy komunikat jest odbierany przez jednego adresata.
* *Tematy*, które zapewniają komunikację jednokierunkową przy użyciu *subskrypcji* (jeden temat może mieć wiele subskrypcji). Podobnie jak kolejki tematu działa jako broker, ale każda subskrypcja może opcjonalnie korzystać filtru tooreceive tylko wiadomości, spełniających określone kryteria.
* *Przekaźniki*, które zapewniają komunikację dwukierunkową. W przeciwieństwie do kolejek i tematów przekaźnik nie przechowuje transmitowanych komunikatów (nie jest brokerem). Zamiast tego po prostu przekazuje je w aplikacji docelowej toohello.

Podczas tworzenia kolejki, tematu lub przekaźnika tworzonemu elementowi nadawana jest nazwa. W połączeniu z przestrzenią nazw ta nazwa tworzy unikatowy identyfikator dla obiekt hello. Aplikacje można podać to nazwa tooService magistrali, a następnie użyj tej kolejki, tematu lub przekazywania toocommunicate ze sobą. 

toouse żadnego z tych obiektów w scenariuszu przekazywania hello, aplikacje systemu Windows można użyć usługi Windows Communication Foundation (WCF). Ta usługa jest określana jako [przekaźnik WCF](../service-bus-relay/relay-what-is-it.md). W przypadku kolejek i tematów aplikacje systemu Windows mogą używać interfejsów API obsługi komunikatów zdefiniowanych przez usługę Service Bus. toomake łatwiejsze toouse te obiekty z aplikacji z systemem innym niż Windows, firma Microsoft udostępnia zestawy SDK dla języka Java, Node.js i innych języków. Dostęp do kolejek i tematów można także uzyskać za pomocą [interfejsów API REST](/rest/api/servicebus/) i protokołu HTTP lub HTTPS. 

Jest ważne, toounderstand, która nawet, jeśli jest to Service Bus sama działa w chmurze hello (oznacza to, w centrach danych platformy Azure firmy Microsoft), aplikacje, które go używają można uruchamiane w dowolnym miejscu. Możesz użyć usługi Service Bus tooconnect aplikacji działających na platformie Azure, na przykład lub aplikacji uruchamianych wewnątrz własnego centrum danych. Umożliwia także go tooconnect aplikacji działających na platformie Azure lub innej platformy w chmurze z aplikacjami lokalnymi lub z tabletami i telefonami. Jest prawdopodobnie również tooconnect urządzeń gospodarstwa domowego, czujników i innych urządzeń tooa centralną aplikacją lub tooone innych. Usługa Service Bus jest mechanizm komunikacji w chmurze hello, który jest dostępny niemal z dowolnego miejsca. Sposób korzystania zależy Twoje aplikacje, które muszą toodo.

## <a name="queues"></a>Kolejki

Załóżmy, że zdecydujesz tooconnect dwie aplikacje przy użyciu kolejki usługi Service Bus. Na Rysunku 2 przedstawiono tę sytuację.

![][2]

**Rysunek 2. Kolejki usługi Service Bus zapewniają jednokierunkowe kolejkowanie asynchroniczne.**

Witaj proces jest prosty: Nadawca wysyła komunikat kolejki usługi Service Bus tooa, a odbiornik pobiera ten komunikat w późniejszym czasie. Kolejka może zawierać tylko jeden odbiornik, jak pokazano na rysunku 2. Lub wiele aplikacji może odczytywać hello samej kolejki. W hello ostatniej sytuacji każdy komunikat jest odczytywany przez tylko jeden odbiornik. W przypadku usługi multiemisji należy zamiast kolejki użyć tematu.

Każdy komunikat ma dwie części: zbiór właściwości, z których każda jest parą klucz/wartość, oraz ładunek komunikatu. ładunek Hello może być pliku binarnego, tekst lub nawet XML. Sposób ich używania zależy od tego, jakie aplikacja próbuje toodo. Na przykład aplikacja wysyłająca komunikat o ostatniej sprzedaży może zawierać właściwości hello **Seller = "Ava"** i **kwota = 10000**. Treść wiadomości powitania może zawierać zeskanowany obraz podpisanej umowy sprzedaży hello lub, jeśli nie istnieje, pozostać pusta.

Odbiornik może odczytywać komunikaty z kolejki usługi Service Bus na dwa różne sposoby. Witaj pierwsza opcja o nazwie  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, usuwa komunikat z kolejki hello i natychmiast go kasuje. Ta opcja jest proste, ale jeśli odbiornik hello ulegnie awarii przed zakończeniem przetwarzania wiadomość hello, wiadomość hello zostaną utracone. Ponieważ został usunięty z hello kolejki, żaden inny odbiornik do niego dostęp. 

Druga opcja Hello  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, jest przeznaczona toohelp z tym problemem. Podobnie jak **ReceiveAndDelete**, **PeekLock** odczytu usuwa komunikat z kolejki hello. Jednak nie usuwa wiadomość hello. Zamiast tego blokuje wiadomość hello, dzięki czemu odbiorcy tooother niewidoczne, następnie czeka na jedno z trzech zdarzeń:

* Jeśli procesy odbiornika hello pomyślnie hello komunikat, wywołuje metodę [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), i hello kolejka usuwa wiadomość hello. 
* Jeśli odbiornik hello decyduje o tym, że wiadomość hello nie może przetworzyć pomyślnie, wywołuje metodę [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). Hello kolejka następnie usuwa blokady hello wiadomość hello i ułatwia odbiorcy tooother dostępne.
* Jeśli hello odbiornik nie wywoła żadnej z tych metod w konfigurowalnych czasie (domyślnie 60 sekund), kolejka hello zakłada, że hello odbiornika nie powiodła się. W takim przypadku zachowuje się tak, jakby hello odbiornik wywołał **Abandon**, co odbiorniki dostępne tooother wiadomość hello.

Zwróć uwagę, co może się zdarzyć: hello sam komunikat może zostanie dostarczony dwukrotnie, być może tootwo różnych odbiorników. Aplikacje korzystające z kolejek usługi Service Bus muszą być przygotowane na to zdarzenie. toomake wykrywania duplikatów łatwiejsze, każdy komunikat ma unikatową [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) właściwość, która domyślnie pozostaje hello sama niezależnie od tego, ile razy wiadomość hello jest do odczytu z kolejki. 

Kolejki są przydatne w kilku sytuacjach. Umożliwiają one toocommunicate aplikacji, nawet wtedy, gdy nie są uruchomione na powitania sam czas, co jest szczególnie przydatne w przypadku aplikacji wsadowych i aplikacji dla urządzeń przenośnych. Kolejka z wieloma odbiornikami zapewnia również automatyczne równoważenie obciążenia, ponieważ wysłane wiadomości są rozkładane między te odbiorniki.

## <a name="topics"></a>Tematy

Przydatne, ponieważ są one, kolejki nie zawsze są odpowiednim rozwiązaniem hello. Czasami lepsze są tematy usługi Service Bus. Rysunek 3 ilustruje tę koncepcję.

![][3]

**Rysunek 3: Na podstawie filtru hello subskrybującą aplikację, może ona odbierać niektóre lub wszystkie wiadomości powitania wysyłane tooa tematu usługi Service Bus.**

A *tematu* przypomina wiele sposobów tooa kolejki. Nadawców przesłać tooa tematu wiadomości powitania tak samo przesyłania komunikatów tooa kolejki, czy wygląd tych wiadomości hello takie same jak w przypadku kolejek. Witaj różnicą jest to, że tematy umożliwiają każdej odbierania toocreate aplikacji własną *subskrypcji* , definiując *filtru*. Subskrybent następnie widzi tylko wiadomości powitania zgodne z filtrem. Przykładowo, Rysunek 3 przedstawia nadawcę i temat z trzema subskrybentami, z których każdy ma własny filtr:

* Subskrybent 1 odbiera tylko komunikaty, które zawierają właściwość hello *Seller = "Ava"*.
* Subskrybent 2 odbiera komunikaty, które zawierają właściwość hello *Seller = "Ruby"* i/lub zawierają *kwota* właściwości, której wartość jest większa niż 100 000. Być może Ruby jest hello Menedżera sprzedaży, więc chce toosee zarówno własną sprzedaż i wszystkie duże sprzedaży niezależnie od tego, kto ich dokonuje.
* Subskrybent 3 ustawił filtr zbyt*True*, co oznacza, że odbiera wszystkie komunikaty. Na przykład ta aplikacja może być odpowiedzialna za utrzymanie dziennika inspekcji i dlatego musi toosee wszystkie wiadomości powitania.

W przypadku kolejek subskrybenci tematu tooa można odczytywać komunikaty przy użyciu metody [ReceiveAndDelete lub PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). W przeciwieństwie do kolejek jednak pojedynczej wiadomości wysłane tooa tematu może zostać odebrany przez wiele subskrypcji. Takie podejście, często nazywane *Publikuj i Subskrybuj* (lub *pub/sub*), jest przydatne, gdy wiele aplikacji jest zainteresowanych hello tej wiadomości. Definiując hello właściwego filtru każdy subskrybent może korzystać do tylko hello częścią strumienia wiadomości powitania musi toosee.

## <a name="relays"></a>Przekaźniki

Kolejki i tematy zapewniają jednokierunkową asynchroniczną komunikację za pośrednictwem brokera. Ruch przepływa tylko w jednym kierunku i nie ma bezpośredniego połączenia między nadawcami a odbiornikami. Ale co zrobić, jeśli nie potrzebujesz tego połączenia? Załóżmy, że aplikacje muszą tooboth wysyłania i odbierania wiadomości, prawdopodobnie ma bezpośrednie połączenie między nimi i niepotrzebne komunikaty toostore brokera. tooaddress takich scenariuszy, Usługa Service Bus udostępnia *przekazuje*, jak pokazano na rysunku 4.

![][4]

**Rysunek 4. Przekaźnik usługi Service Bus zapewnia synchroniczną, dwukierunkową komunikację między aplikacjami.**

Witaj tooask oczywistym pytaniem o przekaźniki to: Dlaczego mam z niej korzystać? Nawet jeśli nie potrzebujesz kolejek, dlaczego warto udostępnić aplikacjom komunikowanie się za pośrednictwem usługi w chmurze zamiast bezpośredniej interakcji? odpowiedź Hello jest, że komunikacja bezpośrednia może być trudniejsza, niż się wydaje.

Załóżmy, że chcesz tooconnect dwóch lokalnych aplikacji, których obie działają wewnątrz firmowych centrów danych. Każda z tych aplikacji znajduje się za zaporą, a każde centrum danych prawdopodobnie używa translatora adresów sieciowych (NAT). Witaj Zapora blokuje przychodzące dane na wszystkie, oprócz kilku portów i NAT oznacza, czy maszyna hello, które każda aplikacja jest uruchomiona na nie ma stałego adresu IP osiągalnego bezpośrednio z poza hello centrum danych. Bez dodatkowej pomocy połączenie tych aplikacji za pośrednictwem hello publicznego Internetu jest problematyczne.

Przekaźnik usługi Service Bus może w tym pomóc. toocommunicate dwukierunkowo przez przekaźnik, każda aplikacja ustanawia wychodzące połączenie TCP z usługą Service Bus, a następnie utrzymuje je otwarte. Cała komunikacja między dwiema aplikacjami hello przechodzi przez te połączenia. Ponieważ każde połączenie zostało nawiązane z wewnątrz centrum danych hello, hello zapora zezwala na przychodzący ruch tooeach aplikacji bez konieczności otwierania nowych portów. To podejście zapewnia również obejście problemu translatora adresów Sieciowych hello, ponieważ każda aplikacja ma spójny punkt końcowy w chmurze hello w całej komunikacji hello. Dzięki wymianie danych za pośrednictwem przekaźnika hello, hello aplikacje mogą uniknąć hello problemów, które w przeciwnym razie spowodowałyby komunikacji trudne. 

przekazuje usługi Service Bus toouse, aplikacje na powitania Windows Communication Foundation (WCF). Usługa Service Bus udostępnia wiązania WCF, które stał się proste dla toointeract aplikacji systemu Windows za pomocą przekaźników. Aplikacje, które już używają WCF można zwykle określ jedną z tych powiązań, a następnie komunikować tooeach innych za pośrednictwem przekaźnika. Jednak inaczej niż w przypadku kolejek i tematów korzystanie z przekaźników z aplikacji innych niż aplikacje systemu Windows, o ile jest to możliwe, wymaga nieco pracy programistycznej, ponieważ nie są udostępniane żadne biblioteki standardowe.

W przeciwieństwie do kolejek i tematów aplikacje nie tworzą jawnie przekaźników. Zamiast tego podczas aplikacji, która chce tooreceive komunikaty, ustanawia połączenie TCP z usługą Service Bus, przekaźnik jest tworzony automatycznie. Po rozłączeniu hello hello przekaźnik jest usuwany. tooenable przekazywania hello toofind aplikacji utworzone przez określony odbiornik usługi Service Bus udostępnia rejestr, który umożliwia aplikacji toolocate konkretnego przekaźnika według nazwy.

Przekaźniki są odpowiednim rozwiązaniem hello, gdy będziesz potrzebować bezpośrednia komunikacja między aplikacjami. Rozważmy na przykład system rezerwacji linii lotniczych uruchomiony w lokalnym centrum danych, który musi być dostępny z kiosków odprawy, urządzeń przenośnych i innych komputerów. Aplikacje uruchomione w tych systemach mogą polegać na przekaźnikach usługi Service Bus w hello toocommunicate chmury, wszędzie tam, gdzie mogą być uruchomione.

## <a name="summary"></a>Podsumowanie

Łączenie aplikacji zawsze było częścią tworzenia kompletnych rozwiązań, a zakres scenariuszy, które wymagają aplikacje i usługi toocommunicate ze sobą hello jest ustawiana tooincrease więcej aplikacji i urządzeń, są połączone toohello internet. Zapewniając technologie chmurowe służące osiągnięciu komunikacji za pośrednictwem kolejki, tematy i przekaźniki, usługi Service Bus ma toomake tooimplement łatwiejsze tej istotnej funkcji i szerzej dostępna.

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już podstawy hello Azure Service Bus, wykonaj te więcej toolearn łącza.

* Jak toouse [kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* Jak toouse [tematów usługi Service Bus](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Jak toouse [przekaźnika usługi Service Bus](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Przykłady usługi Service Bus](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
