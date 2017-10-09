---
title: "aaaOverview hello interfejsów API usługi Azure przekazywania węzła | Dokumentacja firmy Microsoft"
description: "Przegląd interfejsu API węzła przekazywania"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a>Przegląd interfejsu API węzła połączeń hybrydowych przekazywania

## <a name="overview"></a>Omówienie

Witaj [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pakiet węzła dla połączeń hybrydowych przekazywania Azure jest zbudowany na i rozszerza hello ["ws"](https://www.npmjs.com/package/ws) pakietu NPM. Ten pakiet ponownie Eksportuje wszystkie eksportu pakietu, aby podstawowa i dodaje nowe eksportu, które umożliwiają integrację z funkcją połączeń hybrydowych usługi przekaźnika usługi Azure hello. 

Istniejące aplikacje który `require('ws')` można użyć tego pakietu z `require('hyco-ws')` zamiast tego, który umożliwia także scenariuszy hybrydowych, w których aplikacja może nasłuchiwać połączeń protokołu WebSocket lokalnie z "zaporą hello" i via połączeń hybrydowych było możliwe, wszystko na Witaj sam czas.
  
## <a name="documentation"></a>Dokumentacja

Witaj interfejsy API są [udokumentowane w pakiecie głównej ws hello](https://github.com/websockets/ws/blob/master/doc/ws.md). W tym artykule opisano, jak ten pakiet różni się od tej linii bazowej. 

Witaj podstawowych różnic między pakiet podstawowy hello i to 'hyco-ws' jest dodaje nową klasę serwera wyeksportowane za pomocą `require('hyco-ws').RelayedServer`i kilka metod pomocniczych.

### <a name="package-helper-methods"></a>Metody pomocnicze pakietu

Brak dostępnych kilka metod narzędzia na powitania eksportu pakietu, które można odwoływać się w następujący sposób:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

metody pomocnicze Hello są do użycia z tym pakietem, ale można również przez serwer węzła umożliwiających odbiorników toocreate klientów sieci web lub urządzenie lub nadawcy. serwera Hello są używane przez przekazywanie ich identyfikatorów URI osadzaj tokenów krótkim okresie. Te identyfikatory URI można również z typowych stosy protokołu WebSocket, które nie obsługują nagłówków HTTP ustawienie na uzgadnianie protokołu WebSocket hello. Osadzanie tokeny autoryzacji w hello obsługiwany przede wszystkim dotyczące tych scenariuszy użycia zewnętrznej biblioteki identyfikatora URI. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Tworzy prawidłowego odbiornika połączenia hybrydowego przekaźnika usługi Azure identyfikatora URI dla hello podanej przestrzeni nazw i ścieżkę. Następnie można ten identyfikator URI z wersją przekazywania hello hello WebSocketServer klasy.

- `namespaceName`(wymagana) — Witaj nazwę kwalifikowaną domeny hello Azure przekazywania przestrzeni nazw toouse.
- `path`(wymagana) — Witaj nazwę istniejącego połączenia hybrydowego przekazywania Azure w tej przestrzeni nazw.
- `token`(opcjonalnie) - wcześniej wydanych przekazywanie tokenu który jest osadzony w odbiornika hello identyfikatora URI (zobacz poniższy przykład hello).
- `id`(opcjonalnie) — identyfikator śledzenia, który umożliwia śledzenia end-to-end diagnostyki żądań.

Witaj `token` wartość jest opcjonalna i należy używać tylko gdy nie jest ona nagłówki możliwe toosend HTTP wraz z hello uzgadnianie protokołu WebSocket, podobnie jak przypadku hello hello stosu protokołu WebSocket W3C.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Tworzy prawidłowy wysyłania połączenia hybrydowego przekaźnika usługi Azure identyfikatora URI dla hello podanej przestrzeni nazw i ścieżkę. Tego identyfikatora URI można używać z dowolnego klienta protokołu WebSocket.

- `namespaceName`(wymagana) — Witaj nazwę kwalifikowaną domeny hello Azure przekazywania przestrzeni nazw toouse.
- `path`(wymagana) — Witaj nazwę istniejącego połączenia hybrydowego przekazywania Azure w tej przestrzeni nazw.
- `token`(opcjonalnie) - wcześniej wydanych tokenu dostępu przekazywania, który jest osadzony w hello wysyłania identyfikatora URI (zobacz poniższy przykład hello).
- `id`(opcjonalnie) — identyfikator śledzenia, który umożliwia śledzenia end-to-end diagnostyki żądań.

Witaj `token` wartość jest opcjonalna i należy używać tylko gdy nie jest ona nagłówki możliwe toosend HTTP wraz z hello uzgadnianie protokołu WebSocket, podobnie jak przypadku hello hello stosu protokołu WebSocket W3C.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Tworzy token Azure przekazywania dostępu sygnatury dostępu Współdzielonego dla hello podany identyfikator URI elementu docelowego, reguła sygnatury dostępu Współdzielonego i klucza sygnatury dostępu Współdzielonego reguły, który jest prawidłowy dla hello, biorąc pod uwagę liczbę sekund lub godzinę z hello bieżącego błyskawiczne w przypadku pominięcia argumentu wygaśnięcia hello.

- `uri`(wymagana) — Witaj identyfikator URI, dla których hello token jest toobe wystawione. Hello identyfikatora URI jest schemat HTTP hello znormalizowane toouse i informacji o ciągu zapytania jest usuwany.
- `ruleName`(wymagane) - SAS reguły nazwę albo jednostka hello reprezentowany przez podany identyfikator URI hello, lub dla hello nazw reprezentowany przez hello częścią hosta identyfikatora URI.
- `key`(wymagane) - prawidłowego klucza dla reguły SAS hello. 
- `expirationSeconds`(opcjonalnie) - hello liczba sekund do hello wygenerowany token powinien wygaśnie. Jeśli nie określono domyślnego hello jest 1 godzina (3600).

Witaj wystawiony token przyznaje prawa hello skojarzone z hello określona reguła sygnatury dostępu Współdzielonego dla hello podany czas trwania.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Ta metoda jest taką samą toohello `createRelayToken` metody opisane wcześniej, ale zwraca hello tokenu toohello poprawnie dołączany wejściowy identyfikator URI.

### <a name="class-wsrelayedserver"></a>Klasa ws. RelayedServer

Witaj `hycows.RelayedServer` klasy jest alternatywnych toohello `ws.Server` klasy, która nie będzie nasłuchiwać na powitania sieci lokalnej, ale deleguje nasłuchiwania toohello usługi przekaźnika usługi Azure.

Witaj dwie klasy są przeważnie kontraktu zgodny, oznacza to, że istniejących aplikacji przy użyciu hello `ws.Server` klasy mogą być łatwo toouse zmienione hello obsługiwanych przez przekaźnik wersji. główne różnice Hello są w Konstruktorze hello i hello dostępnych opcji.

#### <a name="constructor"></a>Konstruktor  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Witaj `RelayedServer` konstruktor obsługuje inny zestaw argumentów niż hello `Server`, ponieważ nie jest autonomiczny odbiornika lub stanie toobe osadzone w istniejących ramach odbiornika HTTP. Dostępne są również mniej opcje ponieważ hello zarządzania protokołu WebSocket jest przede wszystkim delegowanego toohello usługi przekazywania.

Argumenty konstruktora:

- `server`(wymagane) - hello w pełni kwalifikowana identyfikatora URI dla nazwy połączenia hybrydowego, na które toolisten zwykle skonstruowany przy hello WebSocket.createRelayListenUri() metody pomocnika.
- `token`(wymagana) — ten argument zawiera ciąg tokenu wcześniej wydanych lub funkcja wywołania zwrotnego, który można wywołać tooobtain ciąg tokenu. Opcja wywołania zwrotnego Hello jest preferowany, ponieważ umożliwia ona odnowienia tokenu.

#### <a name="events"></a>Zdarzenia

`RelayedServer`wystąpienia Emituj trzech zdarzeń, które włączenia należy toohandle żądań przychodzących, nawiązywać połączenia i wykrywania błędów. Należy zasubskrybować toohello `connect` toohandle komunikaty o zdarzeniach. 

##### <a name="headers"></a>Nagłówki

```JavaScript 
function(headers)
```

Witaj `headers` zdarzenie jest wywoływane przed połączenia przychodzącego jest akceptowany, włączenie modyfikacji hello nagłówki toosend toohello klienta. 

##### <a name="connection"></a>połączenie

```JavaScript
function(socket)
```

Emitowane po zaakceptowaniu nowego połączenia obiektu WebSocket. Obiekt Hello jest typu `ws.WebSocket`, identyczny z pakietem podstawowej hello.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Jeśli serwer źródłowy hello emituje błąd, jest przekazywany w tym miejscu.  

#### <a name="helpers"></a>Pomocnicy

Uruchamianie toosimplify, który serwera obsługiwanych przez przekaźnik i natychmiast subskrypcji połączeń tooincoming hello pakietu przedstawia funkcji pomocnika proste, która jest również używana w przykładach hello w następujący sposób:

##### <a name="createrelayedlistener"></a>createRelayedListener

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Ta metoda wywołuje hello konstruktora toocreate nowe wystąpienie klasy hello RelayedServer i zasubskrybowaniem przez zdarzenie toohello "połączenia" hello, pod warunkiem wywołania zwrotnego.
 
##### <a name="relayedconnect"></a>relayedConnect

Po prostu dublowania hello `createRelayedServer` pomocnika w funkcji `relayedConnect` tworzy połączenie klienta i subskrybuje toohello zdarzenia "open" hello wynikowy gniazda.

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:
* [Co to jest usługa Azure Relay?](relay-what-is-it.md)
* [Interfejsy API dostępne przekazywania](relay-api-overview.md)
