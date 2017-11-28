---
title: "Połączenia hybrydowe przekazywania aaaAzure protokołu przewodnik | Dokumentacja firmy Microsoft"
description: "Przewodnik protokołu Azure przekazywania połączeń hybrydowych było możliwe."
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Azure protokołu przekazywania połączeń hybrydowych
Azure przekazywania jest jednym z słupków kluczowych możliwości hello hello platformy Azure Service Bus. nowe Hello *połączeń hybrydowych* możliwość przekazywania jest bezpieczne, protokołu open zmiany, na podstawie HTTP i protokołu WebSockets. Zastępuje ona pierwsze hello, jednakowo o nazwie *usługi BizTalk Services* funkcji, który został utworzony na podstawie zastrzeżonym protokołem. integracji Hello połączeń hybrydowych usługi aplikacji Azure będzie toofunction jako — jest.

Połączeń hybrydowych umożliwia strumienia dwukierunkowe, binarnych komunikacji między dwiema aplikacjami sieciowym, w których jedną lub obie strony może znajdować się za NAT lub zaporą. W tym artykule opisano powitania klienta interakcji z przekaźnika połączeń hybrydowych hello nawiązywania połączeń klientów w odbiornik i ról nadawcy i jak odbiorników akceptować nowych połączeń.

## Model interakcji
przekazywania połączeń hybrydowych Hello łączy dwie strony zapewniając punktem spotkania w hello chmury Azure, który zarówno strony mogą odnaleźć i połączyć toofrom perspektywy własnych sieci. Tego punktu spotkania nazywa się "Połączenia hybrydowego" w tym i innych dokumentacji hello interfejsów API, a także w hello portalu Azure. Hello połączeń hybrydowych punktu końcowego usługi jest określane tooas hello "Usługa" hello pozostałej części tego artykułu. model interakcji Hello leans na nomenklaturę hello wyznaczane przez wiele innych sieci interfejsów API.

Brak odbiornika, najpierw wskazuje połączenia przychodzące toohandle gotowości, a następnie akceptuje, zgodnie z ich odbierania. Na hello druga Strona, brak połączenia klienta, który łączy do odbiornika hello, oczekiwano tego toobe połączenia zaakceptowane ustalania ścieżki komunikacja dwukierunkowa.
"Połącz", "Nasłuchiwania," i "Zaakceptuj", hello są takie same terminy znajdziesz w większości gniazda interfejsów API.

Każdy model komunikacji obsługiwanych przez przekaźnik ma albo strony wykonywania połączeń wychodzących na punkt końcowy usługi, co sprawia, że odbiornika"hello" również "client" w użyciu potocznej i może również spowodować inne przeciążenia terminologii. terminologia dokładne Hello, w związku z tym używanych dla połączeń hybrydowych było możliwe jest następujący:

programy powitania po obu stronach połączenia są nazywane "klientów", ponieważ są one usługi toohello klientów. Hello klienta, który oczekuje na i akceptuje połączenia "odbiornik" lub jest nazywany toobe rolę hello"odbiornika." powitania klienta, który inicjuje nowe połączenie do odbiornika za pomocą usługi hello jest nazywany hello "sender" lub "rolą nadawcy."

### Odbiornik interakcji
odbiornik Hello ma cztery interakcji z usługą hello; wszystkie szczegóły danych przesyłanych w sieci są opisane w dalszej części tego artykułu w sekcji odwołania hello.

#### Nasłuchiwanie
czy odbiornik jest gotowy tooaccept połączeń usługi toohello gotowości tooindicate, tworzy wychodzące połączenia obiektu WebSocket. Uzgadnianie połączenia Hello niesie hello nazwa połączenia hybrydowe skonfigurowany na powitania przekazywania w przestrzeni nazw i token zabezpieczający, który przyznaje hello "Nasłuchiwania" zgodny z nazwą.
Gdy hello protokołu WebSocket została zaakceptowana przez usługę hello, rejestracja hello jest zakończona i hello ustanowić protokołu WebSocket jest utrzymywane jako hello "kanał kontrolny" włączania wszystkich kolejnych interakcjach sieci web. Usługa Hello umożliwia się too25 odbiorników równoczesnych na połączenie hybrydowe. W przypadku co najmniej dwa odbiorniki aktywnego połączenia przychodzące są równoważone między je w kolejności losowej. odpowiedni dystrybucji nie jest gwarantowana.

#### Zaakceptuj
Po otwarciu nowego połączenia w usłudze hello nadawcy usługi hello wybiera i powiadamia jednej aktywnej odbiorników hello na powitania połączenia hybrydowego. To powiadomienie jest wysyłane za pośrednictwem kanału open kontroli hello odbiornika toohello jako wiadomości JSON zawierający hello adres URL punktu końcowego protokołu WebSocket hello, który hello odbiornika musi połączyć toofor akceptować połączenia hello.

adres URL Hello można i mogą być używane bezpośrednio przez odbiornik hello bez konieczności wykonywania dodatkowych działań.
informacje Hello zakodowane jest prawidłowy tylko wtedy krótki okres czasu, zasadniczo tak długo, nadawcę hello chce toowait hello połączenia toobe ustanowić end-to-end, ale się tooa maksymalnie 30 sekund. Hello adres URL może służyć tylko dla jednego pomyślnego połączenia. Najszybciej, jak hello połączenia z hello spotkania nawiązuje adres URL, wszystkich dalszych działań w tym protokołu WebSocket jest przekazywany z protokołu WebSocket i toohello nadawcy, bez konieczności interwencji lub interpretacji przez usługę hello.

#### Renew
token zabezpieczający Hello, który należy odbiornika hello tooregister używane i obsługa kanał kontrolny może wygaśnie, gdy odbiornika hello jest aktywny. Witaj wygaśnięcia tokenu nie ma wpływu na bieżące połączenia, ale powodować toobe kanału kontroli hello porzuconych przez usługę hello na lub wkrótce po chwili hello wygaśnięcia. Operacja "odnowić" Hello jest JSON wiadomość hello odbiornika można tooreplace hello token skojarzony z hello kanału kontroli, aby wysłać hello kanału kontrolnego mogą być obsługiwane przez dłuższy czas.

#### Ping
Jeśli kanał kontrolny hello pozostanie bezczynny przez długi czas pośredników w sposób hello, takich jak obciążenia równoważenia lub NAT może porzucić hello połączenie TCP. Operacja "ping" Hello, pozwala uniknąć który wysyłając niewielką ilość danych kanałem hello przypomina o tym, wszyscy członkowie trasę sieciową hello tego połączenia hello oznacza toobe aktywności, i służy również jako "na żywo" testu dla odbiornika hello. Jeśli hello ping nie powiedzie się, kanał kontrolny hello należy traktować jako bezużyteczne i odbiornika hello powinni połączyć się ponownie.

### Nadawca interakcji
nadawca Hello ma tylko jeden interakcji z usługą hello: nawiązuje połączenie.

#### Połączenie
operacji "Połącz" Hello otwiera WebSocket w usłudze hello, udostępnienie nazwa hello hello połączenia hybrydowego i (opcjonalnie, ale wymagane domyślnie) przyznanie uprawnień "Wyślij" w ciągu zapytania hello tokenu zabezpieczającego. Usługa Hello użyje odbiornika hello w sposób opisany wcześniej hello i odbiornika hello tworzy połączenie spotkania, który jest połączony z tym protokołu WebSocket. Po zaakceptowaniu hello protokołu WebSocket wszystkich dalszych interakcji, w tym protokołu WebSocket są połączone odbiornika.

### Interakcja podsumowania
wynik Hello tego modelu interakcji jest powitania klienta nadawcy jest dostarczany z uzgadniania z WebSocket "Wyczyść", który jest połączony tooa odbiornika i wymaga nie dalsze preambles lub przygotowania. Ten model umożliwia praktycznie dowolny istniejącego obiektu WebSocket klienta implementacji tooreadily korzystanie z zalet hello usługi połączeń hybrydowych było możliwe, podając adres URL poprawnie skonstruowany do ich warstwy klienta protokołu WebSocket.

Hello spotkania połączenie WebSocket, który hello odbiornika uzyskuje się za pośrednictwem interakcji Akceptuj również jest czysty i można przekazać tooany istniejącego protokołu WebSocket serwera wdrażania z niektórych minimalnego dodatkowe abstrakcji, która odróżnia między "Akceptuj" operacje na ich framework odbiorników sieci lokalnej i zdalnej połączeń hybrydowych "Zaakceptuj" operacji.

## Odwołanie do protokołu

W tej sekcji opisano szczegóły hello interakcji protokołu hello opisanych powyżej.

Wszystkie połączenia obiektu WebSocket są wykonane na porcie 443 uaktualnienie z 1.1 HTTPS, który jest powszechnie usunięte przez niektóre framework WebSocket lub interfejsu API. Opis w tym miejscu jest przechowywana implementacji neutralne, bez sugerowanie dla określonej platformy.

### Protokół odbiornika
Protokół odbiornika Hello składa się z dwóch gestów połączenia i trzy operacje dotyczące komunikatów.

#### Połączenie kanału kontroli odbiornika
kanał kontrolny Hello jest otwarty z tworzenia połączenia obiektu WebSocket:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Witaj `namespace-address` jest nazwą FQDN hello nazw przekazywania Azure hello czy hosty hello połączenia hybrydowego zazwyczaj formę hello `{myname}.servicebus.windows.net`.

dostępne są następujące opcje parametru ciągu zapytania Hello.

| Parametr | Wymagane | Opis |
| --- | --- | --- |
| `sb-hc-action` |Tak |Witaj odbiornika roli Witaj parametru musi być **sb hc akcji = nasłuchiwania** |
| `{path}` |Tak |Witaj zakodowane w adresie URL ścieżki przestrzeni nazw z hello wstępnie tooregister połączenia hybrydowego tym odbiorniku na. To wyrażenie jest dołączany toohello stałej `$hc/` części ścieżki. |
| `sb-hc-token` |Tak\* |Witaj odbiornika należy podać prawidłową, zakodowane w adresie URL usługi magistrali udostępnionych Token dostępu hello przestrzeni nazw lub połączenie hybrydowe, który przyznaje hello **nasłuchiwania** prawo. |
| `sb-hc-id` |Nie |Ten identyfikator opcjonalne dostarczonych przez klienta umożliwia śledzenie diagnostyczne end-to-end. |

W przypadku niepowodzenia wykonania toohello ścieżka połączenia hybrydowego nie jest zarejestrowany lub token nieprawidłowe lub brakujące lub inny błąd hello połączenia obiektu WebSocket opinii błąd hello jest realizowane przy użyciu modelu opinii stanu HTTP 1.1 hello regularne. Opis stanu zawiera błąd — identyfikator śledzenia być przekazane do personelu pomocy technicznej platformy Azure:

| Kod | Błąd | Opis |
| --- | --- | --- |
| 404 |Nie można odnaleźć |Ścieżka połączenia hybrydowego Hello jest nieprawidłowa lub hello podstawowy adres URL jest nieprawidłowo sformułowany. |
| 401 |Brak autoryzacji |token zabezpieczający Hello jest brak lub źle sformułowany lub nieprawidłowy. |
| 403 |Dostęp zabroniony |token zabezpieczający Hello jest nieprawidłowa dla tej ścieżki do wykonania tej akcji. |
| 500 |Błąd wewnętrzny |Wystąpił problem w usłudze hello. |

Wyłączenie hello połączenia obiektu WebSocket celowo przez usługę powitania po jego został początkowo, hello przyczyna to przesyłane przy użyciu odpowiednich kod błędu protokołu WebSocket wraz z komunikat z opisem błędu, który również uwzględnia śledzenia IDENTYFIKATOR. Usługa Hello nie wyłączy kanału kontroli bez napotkania warunek błędu. Wszelkie czystego zamknięcia jest kontrolowane przez klienta.

| Stan WS | Opis |
| --- | --- |
| 1001 |Ścieżka połączenia hybrydowego Hello została usunięta lub wyłączona. |
| 1008 |token zabezpieczający Hello wygasł, w związku z tym naruszenia zasad autoryzacji hello. |
| 1011 |Wystąpił problem w usłudze hello. |

### Zaakceptuj uzgadniania
Witaj "zaakceptować" powiadomienie jest wysyłane przez odbiornik toohello usługi hello w kanale kontroli uprzednio ustanowionym jako wiadomość JSON do ramki protokołu WebSocket. Nie ma odpowiedzi toothis.

wiadomość Hello zawiera obiekt JSON o nazwie "Zaakceptuj", który definiuje następujące właściwości w tym momencie hello:

* **adres** — Witaj toobe ciągu adresu URL używany do ustanawiania hello protokołu WebSocket toothe usługi tooaccept połączenia przychodzącego.
* **Identyfikator** — Witaj Unikatowy identyfikator dla tego połączenia. Jeśli identyfikator hello zostało dostarczone przez powitania klienta nadawcy, jest hello nadawcy podana wartość, w przeciwnym razie wartość wygenerowana przez system.
* **connectHeaders** — wszystkie nagłówki HTTP, które zostały dostarczone punktu końcowego przekazywania toohello przez nadawcę hello, który obejmuje również hello protokół s-WebSocket i nagłówków rozszerzeń-s-protokołu WebSocket.

#### Akceptowanie komunikatu

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Hello adres URL podany w hello komunikat JSON jest używany przez odbiornik hello ustanowienie tekst hello protokołu WebSocket dla akceptowanie lub odrzucanie hello nadawcy gniazda.

#### Akceptowanie hello gniazda
tooaccept, odbiornika hello ustanawia adresem toohello podane połączenia obiektu WebSocket.

Jeśli hello "Zaakceptuj" komunikatów posiada `Sec-WebSocket-Protocol` nagłówka, oczekiwano tego odbiornika hello akceptuje tylko hello protokołu WebSocket Jeśli obsługuje tego protokołu. Ponadto ustawia nagłówek hello jako hello nawiązuje protokołu WebSocket.

Witaj dotyczy to również toohello `Sec-WebSocket-Extensions` nagłówka. Jeśli struktura hello obsługuje rozszerzenie, należy ustawić hello nagłówka toohello po stronie serwera odpowiedzi hello wymagane `Sec-WebSocket-Extensions` uzgadniania hello rozszerzenia.

adres URL Hello musi być używany jako — jest ustalania hello akceptowania gniazda, ale zawiera następujące parametry:

| Parametr | Wymagane | Opis |
| --- | --- | --- |
| `sb-hc-action` |Tak |Akceptowania gniazda, musi być parametrem hello`sb-hc-action=accept` |
| `{path}` |Tak |(zobacz następny akapit hello) |
| `sb-hc-id` |Nie |Zobacz opis poprzedniego **identyfikator**. |

`{path}`jest hello zakodowane w adresie URL ścieżki przestrzeni nazw z hello wstępnie połączenia hybrydowego, w których tooregister tego odbiornika. To wyrażenie jest dołączany toothe stałej `$hc/` części ścieżki. 

Witaj `path` wyrażenie może zostać rozszerzona z sufiksem i znajdujący się po oddzielający ukośnik hello zarejestrowaną nazwę wyrażenia ciągu zapytania. Pozwala to hello nadawcy klienta toopass wysyłania argumenty toohello akceptują odbiornika, gdy nie jest możliwe tooinclude HTTP nagłówków. Hello oczekiwania jest tego odbiornika hello analizuje framework części ścieżki stałym hello i zarejestrowana nazwa hello ze ścieżki i sprawia, że reszta hello prawdopodobnie bez żadnych argumentów ciągu zapytania poprzedzony `sb-`, aplikacja toohello dostępne dla przy wyborze czy tooaccept hello połączenia.

Aby uzyskać więcej informacji zobacz następujące sekcji "Nadawcy protokół" hello.

Jeśli występuje błąd, hello usługa może odpowiedzieć w następujący sposób:

| Kod | Błąd | Opis |
| --- | --- | --- |
| 403 |Dostęp zabroniony |Witaj adres URL jest nieprawidłowy. |
| 500 |Błąd wewnętrzny |Wystąpił problem w usłudze hello |

Po ustanowieniu połączenia hello powitania serwera zamknięty, hello protokołu WebSocket kiedy nadawcy hello protokołu WebSocket przebiega w dół lub z powitania po stanu:

| Stan WS | Opis |
| --- | --- |
| 1001 |powitania klienta nadawcy zamyka hello połączenia. |
| 1001 |Ścieżka połączenia hybrydowego Hello została usunięta lub wyłączona. |
| 1008 |token zabezpieczający Hello wygasł, w związku z tym naruszenia zasad autoryzacji hello. |
| 1011 |Wystąpił problem w usłudze hello. |

#### Odrzucanie hello gniazda
Odrzuca gniazda powitania po komunikat kontrolny "Zaakceptuj" hello wymaga uzgadniania podobne, tak aby hello kod stanu i opis stanu przekazywania przyczynę odrzucenia hello mogą przepływać z powrotem toohello nadawcy.

Wybór projektu protokołu Hello tutaj jest toouse uzgadniania protokołu WebSocket (która jest zaprojektowana tooend w stanie błędu zdefiniowanych), implementacjach klienta odbiornika można kontynuować toorely na kliencie protokołu WebSocket i nie trzeba stosować dodatkowe, bez systemu operacyjnego klienta HTTP.

gniazdo hello tooreject powitania klienta przyjmuje hello adres URI z komunikatu "Zaakceptuj" hello i dołącza dwa tooit parametry ciągu zapytania, w następujący sposób:

| Param | Wymagane | Opis |
| --- | --- | --- |
| statusCode |Tak |Kod stanu HTTP. |
| StatusDescription |Tak |Człowieka czytelny przyczynę odrzucenia hello. |

powitalne wynikowy identyfikator URI jest następnie używany tooestablish połączenia obiektu WebSocket.

Po zakończeniu poprawnie, to uzgadnianie celowo kończy się niepowodzeniem z kodem błędu HTTP 410, ponieważ WebSocket nie została ustanowiona. Jeśli jakaś nieprawidłowość, hello następujące kody opisano hello błąd:

| Kod | Błąd | Opis |
| --- | --- | --- |
| 403 |Dostęp zabroniony |Witaj adres URL jest nieprawidłowy. |
| 500 |Błąd wewnętrzny |Wystąpił problem w usłudze hello. |

### Odbiornik odnowienia tokenu
Po hello odbiornika token o tooexpire go można zastąpić, wysyłając usługi toohello wiadomości tekstowych ramki za pośrednictwem hello ustanowić kanał kontrolny. Komunikat zawiera obiekt JSON o nazwie `renewToken`, który definiuje następujące właściwości w tym momencie hello:

* **Token** — tokenu dostępu udostępnionego magistrali usługi prawidłowy, zakodowane w adresie URL dla przestrzeni nazw lub połączenie hybrydowe, który przyznaje hello **nasłuchiwania** prawo.

#### komunikat renewToken

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

W przypadku niepowodzenia weryfikacji tokenu hello odmowa dostępu, a usługa w chmurze hello zamyka kanał kontrolny hello protokołu WebSocket z powodu błędu. W przeciwnym razie jest żadnej odpowiedzi.

| Stan WS | Opis |
| --- | --- |
| 1008 |token zabezpieczający Hello wygasł, w związku z tym naruszenia zasad autoryzacji hello. |

## Protokół nadawcy
Protokół nadawcy Hello jest identyczne toohello sposobu odbiornik zostanie nawiązane.
Celem Hello jest maksymalną przezroczystość hello end-to-end protokołu WebSocket. adres Hello nawiązać hello toois, który różni się takie same jak w przypadku hello odbiornika, ale hello "Akcja" i tokenu musi różne uprawnienia:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Witaj *przestrzeń nazw adresów* hello pełni kwalifikowanej nazwy domeny czy hosty hello połączenia hybrydowego zazwyczaj formę hello nazw przekaźnika usługi Azure hello jest `{myname}.servicebus.windows.net`.

Żądanie hello może zawierać dowolne dodatkowe nagłówków HTTP, w tym te zdefiniowane przez aplikację. Wszystkie podane nagłówki przepływu toohello odbiornika i znajduje się na powitania `connectHeader` obiektu hello **zaakceptować** komunikatu kontroli.

Opcje parametru ciągu zapytania Hello są następujące:

| Param | Wymagana? | Opis |
| --- | --- | --- |
| `sb-hc-action` |Tak |Dla roli nadawcy hello hello parametr musi być `action=connect`. |
| `{path}` |Tak |(zobacz następny akapit hello) |
| `sb-hc-token` |Tak\* |Witaj odbiornika należy podać prawidłową, zakodowane w adresie URL usługi magistrali udostępnionych Token dostępu hello przestrzeni nazw lub połączenie hybrydowe, który przyznaje hello **wysyłania** prawo. |
| `sb-hc-id` |Nie |Opcjonalny identyfikator, który umożliwia śledzenie diagnostyczne end-to-end i staje się dostępna toohello odbiornika podczas hello zaakceptować uzgadniania. |

Witaj `{path}` jest hello zakodowane w adresie URL ścieżki przestrzeni nazw z hello wstępnie połączenia hybrydowego, w których tooregister tego odbiornika. Witaj `path` wyrażenie można rozszerzyć z sufiksem i toocommunicate wyrażenia ciągu zapytania dalej. Jeśli hello połączenia hybrydowego jest zarejestrowany w ścieżce hello `hyco`, hello `path` wyrażenie może być `hyco/suffix?param=value&...` następuje parametrów ciągu zapytania hello zdefiniowane w tym miejscu. Pełne wyrażenie może wyglądać następująco:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Witaj `path` wyrażenie jest przekazywana odbiornika toohello hello adresu URI zawarte w komunikat kontrolny "Zaakceptuj" hello.

W przypadku niepowodzenia wykonania toohello ścieżka połączenia hybrydowego nie jest zarejestrowany, token nieprawidłowe lub brakujące lub inny błąd hello połączenia obiektu WebSocket opinii błąd hello jest realizowane przy użyciu modelu opinii stanu HTTP 1.1 hello regularne. Opis stanu zawiera błąd śledzenia identyfikator, który może być przekazywane do personelu pomocy technicznej platformy Azure:

| Kod | Błąd | Opis |
| --- | --- | --- |
| 404 |Nie można odnaleźć |Ścieżka połączenia hybrydowego Hello jest nieprawidłowa lub hello podstawowy adres URL jest nieprawidłowo sformułowany. |
| 401 |Brak autoryzacji |token zabezpieczający Hello jest brak lub źle sformułowany lub nieprawidłowy. |
| 403 |Dostęp zabroniony |token zabezpieczający Hello jest nieprawidłowy dla tej ścieżki, a dla tej akcji. |
| 500 |Błąd wewnętrzny |Wystąpił problem w usłudze hello. |

Jeśli celowo hello połączenia obiektu WebSocket zostanie zamknięta przez usługę powitania po jego został wstępnie skonfigurowany, powodem hello jest przekazane za pomocą odpowiednich kod błędu protokołu WebSocket wraz z komunikat z opisem błędu, który również uwzględnia Identyfikator śledzenia.

| Stan WS | Opis |
| --- | --- |
| 1000 |odbiornik Hello Zamknij hello gniazda. |
| 1001 |Ścieżka połączenia hybrydowego Hello została usunięta lub wyłączona. |
| 1008 |token zabezpieczający Hello wygasł, w związku z tym naruszenia zasad autoryzacji hello. |
| 1011 |Wystąpił problem w usłudze hello. |

## Następne kroki
* [Często zadawane pytania dotyczące usługi Relay](relay-faq.md)
* [Tworzenie przestrzeni nazw](relay-create-namespace-portal.md)
* [Wprowadzenie do programu .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Wprowadzenie do programu Node](relay-hybrid-connections-node-get-started.md)

