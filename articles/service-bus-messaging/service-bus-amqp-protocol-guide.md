---
title: "aaaAMQP 1.0 w przewodniku protokołu usługi Azure Service Bus i usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Protokół przewodnik tooexpressions i opis protokołu AMQP 1.0 usługi Azure Service Bus i usługi Event Hubs"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Protokołu AMQP 1.0 w przewodniku protokołu usługi Azure Service Bus i usługi Event Hubs

Hello zaawansowane 1.0 protokołu usługi kolejkowania wiadomości jest standardowe protokoły ramek i transfer asynchronicznie, bezpiecznego i niezawodnego przesyłania komunikatów między dwiema stronami. Jest podstawowy protokół hello Azure Service Bus Messaging i usługi Azure Event Hubs. Obie te usługi również obsługuje protokół HTTPS. Witaj zastrzeżonych SBMP protokół, który jest również obsługiwany jest obecnie wycofywane na rzecz protokołu AMQP.

Protokołu AMQP 1.0 jest wynikiem hello współpraca z branży szerokie zgromadzone dostawców oprogramowania pośredniczącego, takie jak Microsoft i Red Hat z wieloma użytkownikami oprogramowanie pośredniczące obsługi wiadomości, takie jak Morgan Chase JP reprezentujący hello branży usług finansowych. forum normalizacji techniczne Hello specyfikacji protokołu i rozszerzenie protokołu AMQP hello jest OASIS i został osiągnięty posiadanie zatwierdzania międzynarodowe standardem ISO/IEC 19494.

## Cele

W tym artykule krótko podsumowano hello podstawowe koncepcje specyfikacji obsługi wiadomości powitania protokołu AMQP 1.0 wraz z zestawem małych specyfikacji rozszerzenia projektu, które są aktualnie zatwierdzony w Komisji techniczne OASIS AMQP hello oraz wyjaśniono, jak Azure Service Bus implementuje i tworzy z tymi specyfikacjami.

Celem Hello jest każdy Deweloper przy użyciu dowolnego istniejącego stosu klienta protokołu AMQP 1.0 na dowolnej toointeract stanie toobe platformy Azure Service Bus za pośrednictwem protokołu AMQP 1.0.

Typowe ogólnego przeznaczenia stosy protokołu AMQP 1.0, takie jak Apache protonów lub AMQP.NET Lite już implementuje wszystkie gesty core protokołu AMQP 1.0. Tych podstawowych gestów czasami są ujęte w wyższego poziomu API; Apache protonów nawet oferuje dwa, hello imperatywnych Messenger interfejsu API i hello reaktywne reaktora interfejsu API.

W następujących dyskusji hello przyjęto założenie, czy zarządzanie hello połączenia protokołu AMQP, sesje i obsługa łącza i hello transferu ramki i sterowanie przepływem są obsługiwane przez stos odpowiednich hello (takich jak Apache protonów-C) i nie wymagają określonych znacznie, jeśli istnieje Uwagi deweloperzy aplikacji. Abstrakcyjnie zakładamy hello istnienie kilka podstawowych interfejsu API, takich jak hello możliwości tooconnect i toocreate jakiegoś typu *nadawcy* i *odbiornika* abstrakcji obiektów, które następnie mają niektóre kształtu `send()`i `receive()` operacje, odpowiednio.

Omawiając zaawansowanych możliwości usługi Azure Service Bus, takich jak przeglądanie wiadomości lub zarządzania sesjami, te funkcje zostały omówione w kategoriach protokołu AMQP, ale także jako warstwowych pseudo-implementacji u góry tego zakładanego abstrakcji interfejsu API.

## Co to jest AMQP?

Protokół AMQP jest protokołem ramek i transferu. Ramek oznacza zawiera struktury, dla strumieni danych binarnych, które wpływają w żadnym kierunku połączenia sieciowego. Struktura Hello zapewnia nakreślenia różne bloków danych o nazwie *ramki*, toobe wymieniane między stronami hello połączony. możliwości transferu Hello upewnij się, ustanowić udostępnione opis o kiedy ramki są przekazywane, a podczas transferów uznaje się pełną zarówno komunikującymi się Stronami.

W przeciwieństwie do wersji wcześniej wygasłe projekt produkowane przez grupę roboczą hello protokołu AMQP, które są nadal używane przez kilka brokerzy wiadomości grupy roboczej hello ostateczne i standardowych protokołu AMQP 1.0 nie określają obecność hello brokera komunikatów lub dowolnej określonej topologii dla obiektów wewnątrz brokera komunikatów.

Protokół Hello może być używany w komunikacji symetrycznego peer-to-peer, interakcji z brokerzy komunikatów, obsługujące kolejek i publikowania/subskrypcji jednostek, tak jak w przypadku usługi Azure Service Bus. Może również służyć interakcji z infrastrukturą obsługi wiadomości gdzie wzorce interakcji hello różnią się od regularne kolejek, podobnie jak przypadku hello Azure Event Hubs. Centrum zdarzeń działa jak kolejki przy wysyłaniu tooit zdarzeń, ale więcej działa jak Usługa magazynu serial podczas zdarzenia są odczytywane z nieco jest podobny stacji taśm. powitania klienta odbiera przesunięcia do hello dostępnych danych strumienia i jest następnie udostępniany wszystkie zdarzenia z tym przesunięcia toohello najnowsze dostępne.

Witaj protokołu AMQP 1.0 jest zaprojektowana toobe rozszerzalny, umożliwiające dalsze specyfikacje tooenhance jego możliwości. Hello trzy rozszerzenia specyfikacje omówiony w niniejszym dokumencie ilustrację. Do komunikacji w ramach istniejącej infrastruktury protokołu HTTPS/Websocket, gdzie Konfigurowanie hello natywnego portów TCP protokołu AMQP może być trudne, specyfikacja powiązania definiuje sposób toolayer AMQP przez protokół WebSockets. Do interakcji z infrastrukturą obsługi wiadomości powitania żądania/odpowiedzi sposób dla celów zarządzania lub tooprovide zaawansowane funkcje, specyfikacja zarządzania AMQP hello definiuje hello wymagane podstawowe interakcji podstawowych. Integracji modelu autoryzacji federacyjnych, hello specyfikacji oświadczenia na podstawie zabezpieczeń protokołu AMQP definiuje sposób tooassociate i odnawiania tokenów autoryzacji skojarzone z łącza.

## Podstawowe scenariusze protokołu AMQP

W tej sekcji opisano hello podstawowe sposoby użycia protokołu AMQP 1.0 z usługi Azure Service Bus, w tym tworzenie połączeń, sesje i linki i przesyłania komunikatów tooand z jednostek usługi Service Bus, takich jak kolejki, tematy i subskrypcje.

Hello najbardziej autorytatywne źródło toolearn dotyczące sposobu działania protokołu AMQP jest specyfikacją hello protokołu AMQP 1.0, ale specyfikacji hello zostało zapisane implementacji przewodnik tooprecisely i nie tooteach hello protokołu. W tej sekcji koncentruje się na wprowadzenie tyle terminologii zgodnie z potrzebami dla opisujące, jak Usługa Service Bus używa protokołu AMQP 1.0. Na pełniejsze tooAMQP wprowadzenie, a także szersze omówienie protokołu AMQP 1.0, możesz przejrzeć [tego kursu wideo][this video course].

### Połączenia i sesji

Hello wywołania protokołu AMQP komunikacji programy *kontenery*; te zawierają *węzłów*, która hello komunikują się jednostek w tych kontenerach. Kolejki mogą być takie węzła. Protokół AMQP umożliwia Multipleksowanie, dzięki pojedynczego połączenia mogą być używane dla wielu ścieżek komunikacji między węzłami. na przykład klienta aplikacji mogą jednocześnie odbierać z jednego wysyłania tooanother kolejek i za pośrednictwem hello samo połączenie sieciowe.

![][1]

połączenie sieciowe Hello w związku z tym jest zakotwiczona hello kontenera. Zainicjowaniu przez kontener hello w roli klienta hello wprowadzania wychodzącego kontenera tooa połączenia gniazda TCP w hello odbiornika roli, która wykrywa i akceptuje połączenia TCP dla ruchu przychodzącego. uzgadniania połączenia Hello obejmuje negocjowania protokołu hello w wersji, deklarowanie lub negocjowania używanie hello Transport Level Security (TLS/SSL) i uzgadnianie uwierzytelnianie/autoryzacja w zakresie połączenia hello, która jest oparta na SASL.

Usługa Azure Service Bus wymaga użycia hello TLS przez cały czas. Obsługuje ona połączeń za pośrednictwem portu TCP 5671, zgodnie z którą hello połączenie TCP jest najpierw umieszczenia z protokołem TLS przed wprowadzeniem uzgadnianie protokołu AMQP hello i obsługuje także połączenia za pośrednictwem portu TCP 5672 zgodnie z którymi powitania serwera natychmiast oferuje obowiązkowe uaktualnienia przy użyciu modelu określone AMQP hello tooTLS połączenia. powiązanie protokołu AMQP Websocket Hello tworzy tunel za pośrednictwem portu TCP 443, który jest następnie połączeń 5671 tooAMQP równoważne.

Po skonfigurowaniu połączenia hello i TLS, usługi Service Bus oferuje dwie opcje mechanizmu SASL:

* ZWYKŁY SASL jest najczęściej używany do przekazywania serwera tooa poświadczenia użytkownika i hasło. Usługi Service Bus nie mają kont, ale nazwane [zasady zabezpieczenia dostępu do udostępnionych](service-bus-sas.md), która przyznaje prawa i są skojarzone z kluczem. Witaj Nazwa reguły jest używana jako hello nazwy użytkownika i klucz hello (jak tekst kodowany w formacie base64) są używane jako hello hasła. prawa Hello skojarzone z hello wybrane reguły określają operacje hello połączenia hello dozwolony.
* SASL ANONIMOWEGO jest używana do pomijanie SASL autoryzacji, jeśli powitania klienta chce toouse hello oświadczeń-— model zabezpieczeń oparty na (CBS) opisaną później. Po wybraniu tej opcji klienta można ustanowić połączenia anonimowe przez krótki czas podczas którego powitania klienta może komunikować się tylko z punktem końcowym CBS hello i wykonać hello CBS uzgadniania.

Po nawiązaniu połączenia transportowego hello kontenery hello każdego zadeklarować hello maksymalny rozmiar ramki są ujawniane toohandle, a po limit czasu bezczynności one będzie jednostronnie przerywaj nic się nie hello połączenia.

One zadeklarować, jak wiele równoczesnych kanały są obsługiwane. Kanał jest ścieżką jednokierunkowe, wychodzącego wirtualnego transferu na powitania połączenia. Sesja trwa kanału z każdej hello kontenery połączonych tooform dwukierunkową komunikację ścieżki.

Sesje oferują model sterowania przepływem na podstawie okna; Podczas tworzenia sesji, strony deklaruje liczbę ramek jest tooaccept gotowa do jej okna odbierania. Podczas hello strony exchange ramki, przesyłania ramek wypełnienia czy okno i transferów zatrzymać po zapełnieniu hello okna i dopóki okno hello pobiera resetowania lub rozszerzyć, przy użyciu hello *przepływ performative* (*performative*jest określenie protokołu AMQP hello gestów poziomu protokołu wymieniane między stronami hello dwa).

Ten model na podstawie okna jest grubsza analogiczny toohello TCP koncepcji sterowaniu przepływem na podstawie okna, ale na poziomie sesji hello wewnątrz hello gniazda. Witaj koncepcji zezwala na wiele równoczesnych sesji protokołu istnieje tak, aby ruch o wysokim priorytecie można presją poza ograniczeniem przepustowości normalnym ruchu, jak na autostrady lane express.

Obecnie usługa Azure Service Bus używa dokładnie jednej sesji dla każdego połączenia. Maksymalny rozmiar ramki usługi Service Bus Hello jest 262 144 bajty (256 KB) dla usługi magistrali Standard i usługi Event Hubs. Jest 1 048 576 (1 MB) dla usługi Service Bus w warstwie Premium. Usługa Service Bus nie nakłada oknami ograniczania przepustowości określonego poziomu sesji, ale resetuje hello okna regularnie w ramach kontroli przepływu na poziomie łącza (zobacz [hello następnej sekcji](#links)).

Połączenia, kanałów i sesje są tymczasowych. Jeśli połączenie podstawowe hello zwija połączeń, musi przywróciła tunelu TLS, kontekst autoryzacji SASL i sesji.

### Linki

Protokół AMQP przesyła komunikaty za pośrednictwem łącza. Łącze jest ścieżką komunikacji utworzonych w sesji, która umożliwia przesyłania komunikatów w jednym kierunku; Witaj transfer stanu negocjacji znajduje się nad hello link i dwukierunkową między stronami hello połączone.

![][2]

Łącza mogą być tworzone przy użyciu albo kontenera, w dowolnym momencie, a w istniejącej sesji, dzięki czemu różne od wielu innych protokołów, w tym HTTP i MQTT, gdzie hello inicjowania transferu i ścieżki transferu jest wyłączne uprawnienie Tworzenie strony hello protokołu AMQP Połączenie gniazda Hello.

kontener Inicjowanie łącza Hello zadaje hello przeciwne tooaccept kontenera łącze i wybiera roli nadawcy i adresata. W związku z tym kontenera można zainicjować tworzenia jednokierunkowe lub komunikacja dwukierunkowa ścieżek hello ostatnie modelowane jako pary łącza.

Łącza są o nazwie i skojarzone z węzłów. Jak już wspomniano w początku hello, węzły są hello komunikacji jednostek wewnątrz kontenera.

W usłudze Service Bus węzeł jest równoważny tooa kolejki, tematu, subskrypcji lub podkolejki subskrypcji lub kolejki utraconych wiadomości. Nazwa węzła Hello używane w AMQP w związku z tym jest hello względnej nazwy podmiotu hello wewnątrz hello przestrzeń nazw magistrali usług. Jeśli nosi nazwę kolejki **Moja_kolejka**, jest to nazwa węzła jego protokołu AMQP. Subskrypcję tematu następuje hello Konwencji HTTP API przez są posortowane w kolekcji zasobów "subskrypcji" i w związku z tym subskrypcji **sub** lub temat **mytopic** ma nazwę węzła AMQP hello **sub-mytopic/subskrypcje**.

powitania klienta nawiązującego połączenie jest również wymagany toouse nazwa węzła lokalnego do tworzenia łączy; Magistrala usług nie jest przetestowanego o te nazwy węzła i nie zinterpretowane. Stosy klienta protokołu AMQP 1.0 jest powszechnie używany tooassure schematu, że nazwy tych węzłów tymczasowych są unikatowe w zakresie hello powitania klienta.

### Transfery

Po ustanowieniu łącza można przesyłać komunikaty za pośrednictwem tego łącza. W protokołu AMQP, transfer jest wykonywane z gestów jawne protokołu (hello *transferu* performative) który przenosi wiadomości z tooreceiver nadawcy za pośrednictwem łącza. Przeniesienie została ukończona, gdy jej "rozliczenia", co oznacza, że obie strony zostało ustanowione udostępnionego zrozumienia hello wynik ten transfer.

![][3]

W przypadku najprostszym hello nadawcy hello można wybrać wiadomości toosend "wstępnie rozliczane", co oznacza, że powitania klienta nie jest zainteresowana wyniku hello i odbiornika hello nie zapewnia żadnych swoją opinię na temat hello wynik operacji hello. Ten tryb jest obsługiwany przez usługi Service Bus na powitania poziom protokołu AMQP, ale nie są widoczne w żadnym z interfejsów API powitania klienta.

Witaj regularne zdarza się, czy komunikaty są wysyłane nierozliczonych i odbiornika hello następnie wskazuje zatwierdzenia lub odrzucenia przy użyciu hello *dyspozycji* performative. Odrzucenia występuje, gdy hello odbiornika nie może zaakceptować wiadomość hello jakiegokolwiek powodu hello odrzucenia komunikat zawiera informacje o przyczynie hello, który jest strukturą błąd wynika z protokołu AMQP. Jeśli wiadomości zostały odrzucone z powodu błędów toointernal wewnątrz usługi Service Bus, usługa hello zwraca dodatkowe informacje w tym struktura, która umożliwia zapewnienie diagnostyki personelu toosupport wskazówki, jeśli zgłaszasz żądania pomocy technicznej. Więcej informacji o błędach dowiesz się później.

Specjalna forma odrzucenia jest hello *wydane* o stanie, co oznacza, że odbiornik hello ma przeniesienia toohello zastrzeżenie technicznych, ale również zainteresowanie rozliczania hello transferu. Przypadek, że istnieje na przykład, gdy komunikat jest dostarczany tooa klienta usługi Service Bus i powitania klienta wybierze zbyt "abandon" wiadomość hello, ponieważ nie można wykonać hello pracy wynikające z przetwarzania wiadomość hello; dostarczanie wiadomości powitania sam nie jest uszkodzone. Hello jest odmianą elementu członkowskiego *zmodyfikować* stanie umożliwiającym komunikat toohello zmiany jego zwolnienia. Ten stan nie jest używany przez magistralę usług w chwili obecnej.

Hello Specyfikacja protokołu AMQP 1.0 definiuje dodatkowe dyspozycji stanu wywołuje *Odebrano*, pomagające w szczególności toohandle łącza odzyskiwania. Łącza odzyskiwania umożliwia przywracanie stanu hello łącze i wszelkie oczekujące wysyłki na nowe połączenie i sesji, gdy poprzednie połączenie hello i sesji zostały utracone.

Usługa Service Bus nie obsługuje odzyskiwania łącze; Jeśli klient hello utraci hello połączenia tooService magistrali nierozliczonych komunikat o transfer oczekujące, transfer tej wiadomości zostaną utracone i powitania klienta musi ponownie połączyć, ponownie ustanowić łącze hello i ponowić próbę transferu hello.

W efekcie usługi Service Bus i usługi Event Hubs "co najmniej raz" obsługuje transferów, których należy zapewnić wiadomość hello przechowywane i zaakceptowane hello nadawcy, ale nie obsługują "dokładnie jednokrotne" przeniesienia na poziom protokołu AMQP, gdzie hello system będzie podejmować toorecover hello Witaj łącza i kontynuować toonegotiate hello dostarczania stanu tooavoid dublowania hello transferu komunikatów.

wysyła toocompensate występowania duplikatów możliwe, Usługa Service Bus obsługuje wykrywania duplikatów jako opcjonalna funkcja w kolejek i tematów. Wykrywanie zduplikowanych rekordów hello identyfikatory komunikatów wszystkich wiadomości przychodzących podczas okno czasu zdefiniowanych przez użytkownika, a następnie dyskretnie hello porzucania przez wszystkie wiadomości wysyłane z takich samych identyfikatorów wiadomości w tym samym oknie.

### Przepływ sterowania

Ponadto sterowanie przepływem poziomu sesji toohello modelu, który poprzednio omówiona, każde łącze ma własną model kontroli przepływu. Sterowanie przepływem poziomu sesji uniemożliwia o toohandle zbyt wiele ramek na po sterowanie przepływem na poziomie łącza umieszcza aplikacji hello odpowiedzialnym za ile komunikatów go toohandle chce z łącza, a gdy hello kontenera.

![][4]

Łącze, transferów tylko zdarzyć, gdy hello nadawcy ma wystarczającą ilość *link środki*. Łącze kredyt jest ustawiony przez odbiornik hello przy użyciu hello licznik *przepływu* performative, która jest zakresem tooa łącza. Nadawca hello przypisany środki łącza, podejmuje toouse się tym środki przez dostarczanie wiadomości. Zmniejsza dostarczania każdy komunikat hello pozostałego kredytu łącza o 1. W przypadku wykorzystane środki łącze hello zatrzymać dostaw.

Jeśli usługi Service Bus jest w roli odbiornika hello, natychmiast udostępnia nadawcy hello z środki wystarczającą link, dzięki czemu można natychmiast wysyłać wiadomości. Jak używany środki łącze usługi Service Bus czasami wysyła *przepływ* salda środków łącze hello tooupdate performative toohello nadawcy.

W roli nadawcy hello usługi Service Bus wysyła wiadomości toouse się wszelkie środki oczekujących łącza.

Wywołanie "otrzymywać" na poziomie interfejsu API hello przekłada się na *przepływ* performative wysyłane tooService zużywa magistrali przez powitania klienta i usługi Service Bus, która środków przez pobieranie hello najpierw dostępne, odblokowany wiadomości z kolejki hello, blokowanie i przenoszenia go. Jeśli nie ma jeszcze dostępna w celu dostarczania, wszelkie zaległe środki w dowolnym łączu nawiązać z danego podmiotu pozostaje zarejestrowane w kolejności odbioru, czy komunikaty są zablokowane i przekazywane jako staną się dostępne, toouse wszelkie zaległe środki.

blokady wiadomość Hello jest zwolnione, gdy hello transfer jest rozliczany w jednym z terminala stanów hello *zaakceptowane*, *odrzucone*, lub *wydane*. wiadomości powitania zostanie usunięty z usługi Service Bus, gdy jest w stanie terminali hello *zaakceptowane*. Pozostaje w usłudze Service Bus i jest dostarczany toohello dalej odbiornik, gdy hello transfer osiągnie żadnego hello innych stanów. Po osiągnięciu hello dostarczania maksymalna liczba dozwolone dla jednostki hello odrzuceń toorepeated lub wersje usługi Service Bus automatycznie przenosi wiadomości powitania do kolejki utraconych wiadomości powitania jednostki.

Mimo że hello interfejsów API usługi Service Bus nie ujawniaj bezpośrednio takiej opcji dzisiaj, klienta protokołu AMQP niższego poziomu można użyć hello kredytów łącze modelu tooturn hello "ściągania style" interakcji wydawania jedną jednostkę środków dla każdego żądania odbierania model "wypychania style" przez wystawienie dużej liczby łącze środków na korzystanie z i będzie otrzymywać komunikatów udostępnianymi bez dalszej interakcji. Push jest obsługiwana przez hello [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) lub [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) ustawienia właściwości. Gdy są one inną niż zero, powitania klienta protokołu AMQP używa go jako hello środki łącza.

W tym kontekście jego ważne toounderstand który hello zegar hello ważności blokady hello na wiadomość powitania wewnątrz jednostki hello rozpoczyna się, gdy hello komunikat pochodzi z jednostki hello nie, kiedy wiadomość hello jest umieszczany umieszczonego hello. Zawsze, gdy powitania klienta wskazuje komunikaty tooreceive gotowości, wysyłając środki łącze, jest w związku z tym oczekiwanego toobe komunikatów aktywnie ściągania hello sieci i być gotowy toohandle je. W przeciwnym razie blokady wiadomość hello mogło wygasnąć przed wiadomość hello nawet została dostarczona. Użyj Hello łącze środki kontroli przepływu bezpośrednio powinien odzwierciedlać toodeal natychmiastowego gotowości hello z odbiornikiem toohello dostępne komunikaty wysyłane.

Podsumowując, hello poniższe sekcje zawierają schemat omówienie przepływu performative hello podczas interakcje interfejsu API. Każda sekcja zawiera opis różnych operacji logicznej. Niektóre z tych interakcji, może być "opóźnieniem," oznacza, że ich może być wykonana tylko na żądanie. Tworzenie nadawcy wiadomości nie może powodować interakcji sieci, dopóki pierwszą wiadomość hello jest wysyłane lub żądanie.

strzałki Hello w poniższej tabeli hello oznaczają kierunek przepływu performative hello.

#### Tworzenie odbiornika wiadomości

| Klient | Service Bus |
| --- | --- |
| --> dołączyć ()<br/>Nazwa = {Nazwa łącza}<br/>Obsługa = {dojścia liczbowych},<br/>Rola =**odbiornika**,<br/>Źródło = {nazwa jednostki}<br/>docelowy = {identyfikator klienta link}<br/>) |Klient dołącza tooentity jako odbiornik |
| Dołączanie jej końcu łącza hello odpowiedzi usługi Service Bus |<--dołączyć ()<br/>Nazwa = {Nazwa łącza}<br/>Obsługa = {dojścia liczbowych},<br/>Rola =**nadawcy**,<br/>Źródło = {nazwa jednostki}<br/>docelowy = {identyfikator klienta link}<br/>) |

#### Tworzenie nadawcy wiadomości

| Klient | Service Bus |
| --- | --- |
| --> dołączyć ()<br/>Nazwa = {Nazwa łącza}<br/>Obsługa = {dojścia liczbowych},<br/>Rola =**nadawcy**,<br/>Źródło = {klienta łącza id}<br/>docelowy = {nazwa jednostki}<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |<--dołączyć ()<br/>Nazwa = {Nazwa łącza}<br/>Obsługa = {dojścia liczbowych},<br/>Rola =**odbiornika**,<br/>Źródło = {klienta łącza id}<br/>docelowy = {nazwa jednostki}<br/>) |

#### Tworzenie nadawcy wiadomości (błąd)

| Klient | Service Bus |
| --- | --- |
| --> dołączyć ()<br/>Nazwa = {Nazwa łącza}<br/>Obsługa = {dojścia liczbowych},<br/>Rola =**nadawcy**,<br/>Źródło = {klienta łącza id}<br/>docelowy = {nazwa jednostki}<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |<--dołączyć ()<br/>Nazwa = {Nazwa łącza}<br/>Obsługa = {dojścia liczbowych},<br/>Rola =**odbiornika**,<br/>Źródło o wartości null,<br/>docelowy = null<br/>)<br/><br/><--odłączyć ()<br/>Obsługa = {dojścia liczbowych},<br/>zamknięte =**true**,<br/>błąd = {informacje o błędzie}<br/>) |

#### Komunikat o zamykaniu odbiornik/nadawcy

| Klient | Service Bus |
| --- | --- |
| --> odłączyć ()<br/>Obsługa = {dojścia liczbowych},<br/>zamknięte =**true**<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |<--odłączyć ()<br/>Obsługa = {dojścia liczbowych},<br/>zamknięte =**true**<br/>) |

#### Wyślij (Powodzenie)

| Klient | Service Bus |
| --- | --- |
| --> transfer (<br/>Identyfikator dostawy = {dojścia liczbowych},<br/>tag dostarczania = {binary dojścia}<br/>rozliczenia =**false**,, więcej =**false**,<br/>Stan =**null**,<br/>Wznów =**false**<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |<--(dyspozycji<br/>Rola odbiornik,<br/>najpierw = {identyfikator dostawy}<br/>ostatnio = {identyfikator dostawy}<br/>rozliczenia =**true**,<br/>Stan =**zaakceptowane**<br/>) |

#### Wyślij (błąd)

| Klient | Service Bus |
| --- | --- |
| --> transfer (<br/>Identyfikator dostawy = {dojścia liczbowych},<br/>tag dostarczania = {binary dojścia}<br/>rozliczenia =**false**,, więcej =**false**,<br/>Stan =**null**,<br/>Wznów =**false**<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |<--(dyspozycji<br/>Rola odbiornik,<br/>najpierw = {identyfikator dostawy}<br/>ostatnio = {identyfikator dostawy}<br/>rozliczenia =**true**,<br/>Stan =**odrzucone**()<br/>błąd = {informacje o błędzie}<br/>)<br/>) |

#### Receive

| Klient | Service Bus |
| --- | --- |
| --> (przepływu<br/>łącze kredytów = 1<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |< transfer ()<br/>Identyfikator dostawy = {dojścia liczbowych},<br/>tag dostarczania = {binary dojścia}<br/>rozliczenia =**false**,<br/>więcej =**false**,<br/>Stan =**null**,<br/>Wznów =**false**<br/>) |
| --> dyspozycji)<br/>Rola =**odbiornika**,<br/>najpierw = {identyfikator dostawy}<br/>ostatnio = {identyfikator dostawy}<br/>rozliczenia =**true**,<br/>Stan =**zaakceptowane**<br/>) |Żadna akcja ze strony |

#### Odbieranie komunikatu wielu

| Klient | Service Bus |
| --- | --- |
| --> (przepływu<br/>łącze kredytów = 3<br/>) |Żadna akcja ze strony |
| Żadna akcja ze strony |< transfer ()<br/>Identyfikator dostawy = {dojścia liczbowych},<br/>tag dostarczania = {binary dojścia}<br/>rozliczenia =**false**,<br/>więcej =**false**,<br/>Stan =**null**,<br/>Wznów =**false**<br/>) |
| Żadna akcja ze strony |< transfer ()<br/>Identyfikator dostawy = {dojścia liczbowych + 1},<br/>tag dostarczania = {binary dojścia}<br/>rozliczenia =**false**,<br/>więcej =**false**,<br/>Stan =**null**,<br/>Wznów =**false**<br/>) |
| Żadna akcja ze strony |< transfer ()<br/>Identyfikator dostawy = {dojścia liczbowych + 2},<br/>tag dostarczania = {binary dojścia}<br/>rozliczenia =**false**,<br/>więcej =**false**,<br/>Stan =**null**,<br/>Wznów =**false**<br/>) |
| --> dyspozycji)<br/>Rola odbiornik,<br/>najpierw = {identyfikator dostawy}<br/>ostatnio = {identyfikator dostawy + 2},<br/>rozliczenia =**true**,<br/>Stan =**zaakceptowane**<br/>) |Żadna akcja ze strony |

### Komunikaty

Witaj poniższe sekcje zawierają opis właściwości z sekcje wiadomość hello standardowe protokołu AMQP, które są używane przez usługi Service Bus oraz sposobu mapowania ich toohello zestaw interfejsu API usługi Service Bus.

#### nagłówek

| Nazwa pola | Sposób użycia | Nazwa interfejsu API |
| --- | --- | --- |
| trwałe |- |- |
| Priorytet |- |- |
| czas wygaśnięcia |Czas toolive dla tego komunikatu |[Wartość TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| pierwszy przejmującą |- |- |
| Liczba dostarczania |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| Nazwa pola | Sposób użycia | Nazwa interfejsu API |
| --- | --- | --- |
| Identyfikator komunikatu |Zdefiniowane przez aplikację, dowolnych identyfikator dla tego komunikatu. Używane do wykrywania duplikatów. |[Identyfikator komunikatu](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| Identyfikator użytkownika |Identyfikator aplikacji zdefiniowane przez użytkownika nie jest interpretowany przez magistralę usług. |Nie jest dostępny za pośrednictwem hello interfejsu API usługi Service Bus. |
| zbyt|Identyfikator docelowego zdefiniowanym przez aplikację nie interpretowany przez magistralę usług. |[Aby](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| Temat |Identyfikator celu zdefiniowanym przez aplikację wiadomości, nie jest interpretowany przez magistralę usług. |[Etykiety](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| odpowiedź zbyt|Wskaźnik ścieżki odpowiedzi zdefiniowanym przez aplikację nie interpretowany przez magistralę usług. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| Identyfikator korelacji |Identyfikator korelacji zdefiniowanym przez aplikację nie interpretowany przez magistralę usług. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| Typ zawartości |Zdefiniowane przez aplikację wskaźnika typu zawartości dla treści hello, nie jest interpretowany przez magistralę usług. |[Typ zawartości](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| kodowanie zawartości |Zdefiniowane przez aplikację kodowania zawartości wskaźnik hello treści nie interpretowany przez magistralę usług. |Nie jest dostępny za pośrednictwem hello interfejsu API usługi Service Bus. |
| czas w przypadku wygaśnięcia bezwzględne |Deklaruje, w których bezwzględną hello błyskawicznych komunikat wygasa. Ignorowane w danych wejściowych (nagłówek zaobserwowano TTL) autorytatywne w danych wyjściowych. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| Godzina utworzenia |Deklaruje, w których czas hello wiadomość została utworzona. Nie są używane przez usługi Service Bus |Nie jest dostępny za pośrednictwem hello interfejsu API usługi Service Bus. |
| Identyfikator grupy |Zdefiniowane przez aplikację identyfikator powiązany zestaw komunikatów. Używane dla sesji usługi Service Bus. |[Identyfikator sesji](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| grupy sekwencji |Licznik identyfikowanie numer sekwencji względną hello wiadomość hello wewnątrz sesji. Ignorowane przez magistralę usług. |Nie jest dostępny za pośrednictwem hello interfejsu API usługi Service Bus. |
| Odpowiedz do grupy identyfikator |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Zaawansowane możliwości usługi Service Bus

W tej sekcji omówiono zaawansowanych możliwości usługi Azure Service Bus, oparte na tooAMQP rozszerzenia projektu, w obecnie opracowywane w hello Komitet Techniczny OASIS dla protokołu AMQP. Usługa Service Bus implementuje hello najnowsze wersje tych projektów i przyjmuje zmiany wprowadzone w jak te wersje robocze osiągnąć standardowych.

> [!NOTE]
> Zaawansowane operacje komunikatów magistrali usług są obsługiwane za pomocą wzorca żądanie/odpowiedź. Szczegóły Hello te operacje są opisane w dokumencie hello [protokołu AMQP 1.0 w usłudze Service Bus: opartych na protokole żądanie odpowiedź operacji](service-bus-amqp-request-response.md).
> 
> 

### Protokół AMQP zarządzania

Hello specyfikacji zarządzania AMQP jest hello pierwszy rozszerzeń projekt hello omówione w tym miejscu. Określenie tej wartości definiuje zestaw gestów protokołu w warstwie ponad hello protokołu AMQP, umożliwiające interakcje z hello infrastruktury do obsługi komunikatów za pośrednictwem protokołu AMQP. Specyfikacja Hello definiuje ogólne operacje takie jak *utworzyć*, *odczytu*, *aktualizacji*, i *usunąć* zarządzania jednostek wewnątrz infrastrukturą obsługi wiadomości i zestaw operacji zapytania.

Wszystkie te gesty wymagają żądanie/odpowiedź współdziałanie powitania klienta infrastruktury obsługi wiadomości powitania, a w związku z tym specyfikacji hello definiuje sposób toomodel interakcji wzorca u góry AMQP: powitania klienta łączy toohello obsługi wiadomości infrastruktura, inicjuje sesję, a następnie tworzy parę łącza. Na jedno łącze powitania klienta działa jako nadawcy i na powitania innych działa jako odbiornik, co powoduje utworzenie pary linki, które mogą działać jako kanału dwukierunkowego.

| Operacja logiczna | Klient | Service Bus |
| --- | --- | --- |
| Utworzenie żądania odpowiedzi ścieżki |--> dołączyć ()<br/>Nazwa = {*nazwę łącza*},<br/>Obsługa = {*liczbowych dojście*},<br/>Rola =**nadawcy**,<br/>źródło =**null**,<br/>docelowy = "Zarządzanie myentity / $"<br/>) |Żadna akcja ze strony |
| Utworzenie żądania odpowiedzi ścieżki |Żadna akcja ze strony |\<--dołączyć ()<br/>Nazwa = {*nazwę łącza*},<br/>Obsługa = {*liczbowych dojście*},<br/>Rola =**odbiornika**,<br/>Źródło o wartości null,<br/>docelowy = "myentity"<br/>) |
| Utworzenie żądania odpowiedzi ścieżki |--> dołączyć ()<br/>Nazwa = {*nazwę łącza*},<br/>Obsługa = {*liczbowych dojście*},<br/>Rola =**odbiornika**,<br/>Źródło = "Zarządzanie myentity / $",<br/>docelowy = "identyfikator myclient$"<br/>) | |
| Utworzenie żądania odpowiedzi ścieżki |Żadna akcja ze strony |\<--dołączyć ()<br/>Nazwa = {*nazwę łącza*},<br/>Obsługa = {*liczbowych dojście*},<br/>Rola =**nadawcy**,<br/>Źródło = "myentity"<br/>docelowy = "identyfikator myclient$"<br/>) |

Posiadanie tej pary łącza, wykonania żądania i odpowiedzi hello jest prosta: żądanie jest komunikat wysłany jednostki tooan wewnątrz hello infrastruktury obsługi wiadomości, która obsługuje usługę tego wzorca. W tym komunikacie żądania hello *odpowiedzi* w hello *właściwości* sekcji ustawiono toohello *docelowej* identyfikator hello łącza, na które odpowiedzi hello toodeliver. Hello jednostki obsługi przetwarza żądania hello, a następnie dostarcza hello odpowiedzi na powitania połączenie, którego *docelowej* identyfikator odpowiada hello wskazanych *odpowiedzi* identyfikator.

Oczywiście wzorzec Hello wymaga, aby powitania klienta kontenera i hello generowane przez klientów identyfikator docelowy odpowiedzi hello były unikatowe przez wszystkich klientów, a także trudne toopredict ze względów bezpieczeństwa.

wymiany wiadomości powitania używane przez protokół zarządzania hello i innych protokołów tego hello Użyj tego samego wzorca odbywa się na poziomie aplikacji hello; nie definiują nowe gesty poziomu protokołu AMQP. Jest zamierzone, dzięki czemu aplikacje mogą korzystać natychmiastowego tych rozszerzeń z zgodne stosy protokołu AMQP 1.0.

Usługi Service Bus nie obecnie implementuje hello funkcji podstawowych specyfikacji zarządzania hello, ale hello wzorzec żądań i odpowiedzi w specyfikacji zarządzania hello jest podstawowym hello oświadczenia na podstawie zabezpieczeń funkcji i dla prawie wszystkich Witaj, zaawansowane funkcje omówione w hello następujące sekcje.

### Autoryzacji opartej na oświadczeniach

Projekt specyfikacji protokołu AMQP oświadczeń — na podstawie-autoryzacji (CBS) Hello oparty na powitania zarządzania specyfikacji żądanie/odpowiedź wzorzec i opisano model ogólnych jak toouse federacyjnych tokeny zabezpieczające z protokołu AMQP.

model zabezpieczeń domyślne Hello AMQP omówione w wprowadzenie hello jest oparta na SASL i integruje się z uzgadniania połączenia protokołu AMQP hello. Używanie SASL ma korzystać hello, który zapewnia rozszerzonego modelu, dla którego zdefiniowano zestaw mechanizmów z mogą korzystać każdego protokołu, który formalnie leans na SASL. Wśród tych mechanizmów są "Zwykły" przesyłania nazwy użytkownika i hasła, zabezpieczenia na poziomie tooTLS toobind "EXTERNAL", "ANONYMOUS" tooexpress hello Brak jawnych uwierzytelniania/autoryzacji i szerokiej gamy dodatkowe mechanizmy, które umożliwiają przekazywanie tokenów lub poświadczenia uwierzytelniania lub autoryzacji.

Integracja SASL protokołu AMQP firmy ma dwie wady:

* Wszystkie poświadczenia i tokeny są zakresami toohello połączenia. Infrastruktury komunikatów może być tooprovide zróżnicowane kontroli dostępu na podstawie na jednostki; na przykład dzięki czemu elementu nośnego hello tokenu toosend tooqueue A, ale nie tooqueue B. Kontekst autoryzacji hello zakotwiczony hello połączenia jest niemożliwe toouse pojedynczego połączenia i jeszcze na użytek tokenów dostępu różnych A kolejek i B.
* Tokeny dostępu są zwykle prawidłowe tylko przez ograniczony czas. Ważność ta wymaga hello użytkownika tooperiodically ponownie pozyskać tokeny i zapewnia możliwość toorefuse wystawcy tokenów toohello wystawiania świeże token, jeśli zostały zmienione uprawnienia dostępu użytkownika hello. Połączenia protokołu AMQP może trwać przez dłuższy czas. Witaj modelu SASL zapewnia tylko tooset szansy tokenu w czasie połączenia, co oznacza, że hello infrastruktury obsługi wiadomości, albo ma toodisconnect powitania klienta po wygaśnięciu tokenu hello lub potrzebuje tooaccept hello ryzyko umożliwienia dalszego komunikacji z Klient kto ma prawa dostępu zostały odwołane w hello tymczasowe.

Hello Specyfikacja protokołu AMQP CBS implementowanych przez usługi Service Bus umożliwia obejście elegancki dla obu tych problemów: umożliwia tooassociate tokenów dostępu z każdego węzła i tooupdate te tokeny, zanim wygasną, bez zakłócania pracy przepływu wiadomości powitania klienta.

CBS definiuje węzłem zarządzanie wirtualnym o nazwie *$cbs*, toobe hello infrastruktury obsługi wiadomości. węzła zarządzania Hello akceptuje tokeny w imieniu innych węzłów w hello infrastruktury do obsługi komunikatów.

gest protokołu Hello jest żądanie/odpowiedź programu exchange hello specyfikacją zarządzania. Czy oznacza hello klienta ustanawia pary powiązania z hello *$cbs* węzeł, a następnie przekazuje żądanie na hello wychodzące, a następnie czeka na odpowiedź hello na hello łączy przychodzących.

komunikat żądania Hello ma następujące właściwości aplikacji hello:

| Klucz | Optional (Opcjonalność) | Typ wartości | Wartość zawartości |
| --- | --- | --- | --- |
| Operacja |Nie |Ciąg |**Put token** |
| type |Nie |Ciąg |Typ Hello token hello dotyczy żądanie put. |
| name |Nie |Ciąg |stosuje Hello "audience" toowhich hello tokenu. |
| wygaśnięcia |Tak |sygnatura czasowa |czas wygaśnięcia Hello hello tokenu. |

Witaj *nazwa* właściwość identyfikuje jednostki hello, z których hello token jest włączona. W usłudze Service Bus tego hello ścieżki toohello kolejki i tematu/subskrypcji. Witaj *typu* właściwość identyfikuje typ tokenu hello:

| Typ tokenu | Opis elementu tokenu | Typ treści | Uwagi |
| --- | --- | --- | --- |
| amqp:jwt |Tokenu Web JSON (JWT) |Wartość AMQP (ciąg) |Jeszcze niedostępne. |
| amqp:SWT |Simple Web Token (SWT) |Wartość AMQP (ciąg) |Obsługiwane tylko w przypadku SWT tokenów wystawionych przez AAD/ACS |
| servicebus.Windows.NET:sastoken |Token SAS magistrali usług |Wartość AMQP (ciąg) |- |

Tokeny przyznaje prawa. Usługa Service Bus zna trzech podstawowych praw: "Wyślij" umożliwia wysyłanie "Nasłuchiwania" umożliwia odbieranie i "Manage" umożliwia manipulowanie jednostek. SWT tokeny wystawione przez usługi AAD/ACS jawnie zawierają te uprawnienia jako oświadczenia. Tokeny sygnatury dostępu Współdzielonego usługi magistrali zapoznaj toorules skonfigurowany dla przestrzeni nazw hello lub jednostki, a te zasady są skonfigurowane z uprawnieniami. Token podpisujący hello kluczem hello skojarzone z tej reguły w związku z tym sprawia, że hello tokenu hello express odpowiednich praw. token Hello skojarzony z jednostki przy użyciu *put token* hello zezwala połączone toointeract klienta z podmiotem hello na powitania prawa tokenu. Łącza, gdzie ma powitania klienta na powitania *nadawcy* rola wymaga hello "Send" prawo; biorąc na powitania *odbiornika* roli wymaga prawa "Nasłuchiwania" hello.

Hello komunikat odpowiedzi zawiera następujące hello *właściwości aplikacji* wartości

| Klucz | Optional (Opcjonalność) | Typ wartości | Wartość zawartości |
| --- | --- | --- | --- |
| Kod stanu |Nie |int |Kod odpowiedzi HTTP **[specyfikacją RFC2616]**. |
| Opis stanu |Tak |Ciąg |Opis stanu hello. |

powitania klienta można wywołać *put token* wielokrotnie i dla dowolnej jednostki w infrastrukturze obsługi wiadomości powitania. tokeny Hello są zakresami toohello bieżącego klienta i zakotwiczony hello w bieżącym połączeniu, znaczenie powitania serwera spadnie zachowanych tokenów z po spadku hello połączenia.

Bieżąca implementacja usługi Service Bus Hello zezwala tylko CBS w połączeniu z hello SASL metody "ANONYMOUS". Połączenie SSL/TLS musi zawsze istnieć wcześniejsze toohello SASL uzgadniania.

Hello mechanizmu ANONIMOWY w związku z tym musi być obsługiwana przez hello wybranego klienta protokołu AMQP 1.0. Dostęp anonimowy oznacza, że hello uzgadnianie początkowego połączenia, w tym tworzenie początkowej sesji hello odbywa się bez wiedzy, kto jest tworzenie hello połączenia magistrali usług.

Po nawiązaniu połączenia hello i sesji podłączania hello łączy toohello *$cbs* węzła i wysyłanie hello *put token* żądania są hello tylko dozwolone operacji. Nieprawidłowy token musi być ustawiona pomyślnie za pomocą *put token* żądania dla jednego z węzłów jednostki w ciągu 20 sekund po nawiązaniu połączenia hello, w przeciwnym razie hello jednostronnie rozłączeniu przez magistralę usług.

powitania klienta jest następnie odpowiedzialny za rejestrowanie informacji o wygaśnięciu tokenu. Po wygaśnięciu tokenu usługi Service Bus niezwłocznie porzuca wszystkie linki na powitania połączenia toohello odpowiednich jednostek. tooprevent tego hello klienta można zastąpić hello token dla węzła hello nową w dowolnym momencie za pośrednictwem wirtualnej hello *$cbs* węzła zarządzania z hello takie same *put token* gestu i bez pobierania w hello sposób ładunku hello ruch tego przepływów w różnych łączy.

## Następne kroki

toolearn więcej informacji na temat protokołu AMQP, odwiedź hello następującego łącza:

* [Omówienie protokołu AMQP magistrali usług]
* [Obsługa protokołu AMQP 1.0 tematów i kolejek usługi Service Bus na partycje]
* [Protokół AMQP w usłudze Service Bus dla systemu Windows Server]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Omówienie protokołu AMQP magistrali usług]: service-bus-amqp-overview.md
[Obsługa protokołu AMQP 1.0 tematów i kolejek usługi Service Bus na partycje]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Protokół AMQP w usłudze Service Bus dla systemu Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
