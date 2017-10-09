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
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="ac4dc-103">Przegląd interfejsu API węzła połączeń hybrydowych przekazywania</span><span class="sxs-lookup"><span data-stu-id="ac4dc-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="ac4dc-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ac4dc-104">Overview</span></span>

<span data-ttu-id="ac4dc-105">Witaj [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pakiet węzła dla połączeń hybrydowych przekazywania Azure jest zbudowany na i rozszerza hello ["ws"](https://www.npmjs.com/package/ws) pakietu NPM.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="ac4dc-106">Ten pakiet ponownie Eksportuje wszystkie eksportu pakietu, aby podstawowa i dodaje nowe eksportu, które umożliwiają integrację z funkcją połączeń hybrydowych usługi przekaźnika usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="ac4dc-107">Istniejące aplikacje który `require('ws')` można użyć tego pakietu z `require('hyco-ws')` zamiast tego, który umożliwia także scenariuszy hybrydowych, w których aplikacja może nasłuchiwać połączeń protokołu WebSocket lokalnie z "zaporą hello" i via połączeń hybrydowych było możliwe, wszystko na Witaj sam czas.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="ac4dc-108">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="ac4dc-108">Documentation</span></span>

<span data-ttu-id="ac4dc-109">Witaj interfejsy API są [udokumentowane w pakiecie głównej ws hello](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="ac4dc-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="ac4dc-110">W tym artykule opisano, jak ten pakiet różni się od tej linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="ac4dc-111">Witaj podstawowych różnic między pakiet podstawowy hello i to 'hyco-ws' jest dodaje nową klasę serwera wyeksportowane za pomocą `require('hyco-ws').RelayedServer`i kilka metod pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="ac4dc-112">Metody pomocnicze pakietu</span><span class="sxs-lookup"><span data-stu-id="ac4dc-112">Package helper methods</span></span>

<span data-ttu-id="ac4dc-113">Brak dostępnych kilka metod narzędzia na powitania eksportu pakietu, które można odwoływać się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ac4dc-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="ac4dc-114">metody pomocnicze Hello są do użycia z tym pakietem, ale można również przez serwer węzła umożliwiających odbiorników toocreate klientów sieci web lub urządzenie lub nadawcy.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="ac4dc-115">serwera Hello są używane przez przekazywanie ich identyfikatorów URI osadzaj tokenów krótkim okresie.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="ac4dc-116">Te identyfikatory URI można również z typowych stosy protokołu WebSocket, które nie obsługują nagłówków HTTP ustawienie na uzgadnianie protokołu WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="ac4dc-117">Osadzanie tokeny autoryzacji w hello obsługiwany przede wszystkim dotyczące tych scenariuszy użycia zewnętrznej biblioteki identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="ac4dc-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="ac4dc-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="ac4dc-119">Tworzy prawidłowego odbiornika połączenia hybrydowego przekaźnika usługi Azure identyfikatora URI dla hello podanej przestrzeni nazw i ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="ac4dc-120">Następnie można ten identyfikator URI z wersją przekazywania hello hello WebSocketServer klasy.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="ac4dc-121">`namespaceName`(wymagana) — Witaj nazwę kwalifikowaną domeny hello Azure przekazywania przestrzeni nazw toouse.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="ac4dc-122">`path`(wymagana) — Witaj nazwę istniejącego połączenia hybrydowego przekazywania Azure w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="ac4dc-123">`token`(opcjonalnie) - wcześniej wydanych przekazywanie tokenu który jest osadzony w odbiornika hello identyfikatora URI (zobacz poniższy przykład hello).</span><span class="sxs-lookup"><span data-stu-id="ac4dc-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="ac4dc-124">`id`(opcjonalnie) — identyfikator śledzenia, który umożliwia śledzenia end-to-end diagnostyki żądań.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="ac4dc-125">Witaj `token` wartość jest opcjonalna i należy używać tylko gdy nie jest ona nagłówki możliwe toosend HTTP wraz z hello uzgadnianie protokołu WebSocket, podobnie jak przypadku hello hello stosu protokołu WebSocket W3C.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="ac4dc-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="ac4dc-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="ac4dc-127">Tworzy prawidłowy wysyłania połączenia hybrydowego przekaźnika usługi Azure identyfikatora URI dla hello podanej przestrzeni nazw i ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="ac4dc-128">Tego identyfikatora URI można używać z dowolnego klienta protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="ac4dc-129">`namespaceName`(wymagana) — Witaj nazwę kwalifikowaną domeny hello Azure przekazywania przestrzeni nazw toouse.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="ac4dc-130">`path`(wymagana) — Witaj nazwę istniejącego połączenia hybrydowego przekazywania Azure w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="ac4dc-131">`token`(opcjonalnie) - wcześniej wydanych tokenu dostępu przekazywania, który jest osadzony w hello wysyłania identyfikatora URI (zobacz poniższy przykład hello).</span><span class="sxs-lookup"><span data-stu-id="ac4dc-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="ac4dc-132">`id`(opcjonalnie) — identyfikator śledzenia, który umożliwia śledzenia end-to-end diagnostyki żądań.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="ac4dc-133">Witaj `token` wartość jest opcjonalna i należy używać tylko gdy nie jest ona nagłówki możliwe toosend HTTP wraz z hello uzgadnianie protokołu WebSocket, podobnie jak przypadku hello hello stosu protokołu WebSocket W3C.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="ac4dc-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="ac4dc-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="ac4dc-135">Tworzy token Azure przekazywania dostępu sygnatury dostępu Współdzielonego dla hello podany identyfikator URI elementu docelowego, reguła sygnatury dostępu Współdzielonego i klucza sygnatury dostępu Współdzielonego reguły, który jest prawidłowy dla hello, biorąc pod uwagę liczbę sekund lub godzinę z hello bieżącego błyskawiczne w przypadku pominięcia argumentu wygaśnięcia hello.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="ac4dc-136">`uri`(wymagana) — Witaj identyfikator URI, dla których hello token jest toobe wystawione.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="ac4dc-137">Hello identyfikatora URI jest schemat HTTP hello znormalizowane toouse i informacji o ciągu zapytania jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="ac4dc-138">`ruleName`(wymagane) - SAS reguły nazwę albo jednostka hello reprezentowany przez podany identyfikator URI hello, lub dla hello nazw reprezentowany przez hello częścią hosta identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="ac4dc-139">`key`(wymagane) - prawidłowego klucza dla reguły SAS hello.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="ac4dc-140">`expirationSeconds`(opcjonalnie) - hello liczba sekund do hello wygenerowany token powinien wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="ac4dc-141">Jeśli nie określono domyślnego hello jest 1 godzina (3600).</span><span class="sxs-lookup"><span data-stu-id="ac4dc-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="ac4dc-142">Witaj wystawiony token przyznaje prawa hello skojarzone z hello określona reguła sygnatury dostępu Współdzielonego dla hello podany czas trwania.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="ac4dc-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="ac4dc-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="ac4dc-144">Ta metoda jest taką samą toohello `createRelayToken` metody opisane wcześniej, ale zwraca hello tokenu toohello poprawnie dołączany wejściowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="ac4dc-145">Klasa ws. RelayedServer</span><span class="sxs-lookup"><span data-stu-id="ac4dc-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="ac4dc-146">Witaj `hycows.RelayedServer` klasy jest alternatywnych toohello `ws.Server` klasy, która nie będzie nasłuchiwać na powitania sieci lokalnej, ale deleguje nasłuchiwania toohello usługi przekaźnika usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="ac4dc-147">Witaj dwie klasy są przeważnie kontraktu zgodny, oznacza to, że istniejących aplikacji przy użyciu hello `ws.Server` klasy mogą być łatwo toouse zmienione hello obsługiwanych przez przekaźnik wersji.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="ac4dc-148">główne różnice Hello są w Konstruktorze hello i hello dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="ac4dc-149">Konstruktor</span><span class="sxs-lookup"><span data-stu-id="ac4dc-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="ac4dc-150">Witaj `RelayedServer` konstruktor obsługuje inny zestaw argumentów niż hello `Server`, ponieważ nie jest autonomiczny odbiornika lub stanie toobe osadzone w istniejących ramach odbiornika HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="ac4dc-151">Dostępne są również mniej opcje ponieważ hello zarządzania protokołu WebSocket jest przede wszystkim delegowanego toohello usługi przekazywania.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="ac4dc-152">Argumenty konstruktora:</span><span class="sxs-lookup"><span data-stu-id="ac4dc-152">Constructor arguments:</span></span>

- <span data-ttu-id="ac4dc-153">`server`(wymagane) - hello w pełni kwalifikowana identyfikatora URI dla nazwy połączenia hybrydowego, na które toolisten zwykle skonstruowany przy hello WebSocket.createRelayListenUri() metody pomocnika.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="ac4dc-154">`token`(wymagana) — ten argument zawiera ciąg tokenu wcześniej wydanych lub funkcja wywołania zwrotnego, który można wywołać tooobtain ciąg tokenu.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="ac4dc-155">Opcja wywołania zwrotnego Hello jest preferowany, ponieważ umożliwia ona odnowienia tokenu.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="ac4dc-156">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="ac4dc-156">Events</span></span>

<span data-ttu-id="ac4dc-157">`RelayedServer`wystąpienia Emituj trzech zdarzeń, które włączenia należy toohandle żądań przychodzących, nawiązywać połączenia i wykrywania błędów.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="ac4dc-158">Należy zasubskrybować toohello `connect` toohandle komunikaty o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="ac4dc-159">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="ac4dc-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="ac4dc-160">Witaj `headers` zdarzenie jest wywoływane przed połączenia przychodzącego jest akceptowany, włączenie modyfikacji hello nagłówki toosend toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="ac4dc-161">połączenie</span><span class="sxs-lookup"><span data-stu-id="ac4dc-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="ac4dc-162">Emitowane po zaakceptowaniu nowego połączenia obiektu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="ac4dc-163">Obiekt Hello jest typu `ws.WebSocket`, identyczny z pakietem podstawowej hello.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="ac4dc-164">error</span><span class="sxs-lookup"><span data-stu-id="ac4dc-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="ac4dc-165">Jeśli serwer źródłowy hello emituje błąd, jest przekazywany w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="ac4dc-166">Pomocnicy</span><span class="sxs-lookup"><span data-stu-id="ac4dc-166">Helpers</span></span>

<span data-ttu-id="ac4dc-167">Uruchamianie toosimplify, który serwera obsługiwanych przez przekaźnik i natychmiast subskrypcji połączeń tooincoming hello pakietu przedstawia funkcji pomocnika proste, która jest również używana w przykładach hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ac4dc-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="ac4dc-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="ac4dc-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="ac4dc-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="ac4dc-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="ac4dc-170">Ta metoda wywołuje hello konstruktora toocreate nowe wystąpienie klasy hello RelayedServer i zasubskrybowaniem przez zdarzenie toohello "połączenia" hello, pod warunkiem wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="ac4dc-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="ac4dc-171">relayedConnect</span></span>

<span data-ttu-id="ac4dc-172">Po prostu dublowania hello `createRelayedServer` pomocnika w funkcji `relayedConnect` tworzy połączenie klienta i subskrybuje toohello zdarzenia "open" hello wynikowy gniazda.</span><span class="sxs-lookup"><span data-stu-id="ac4dc-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ac4dc-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac4dc-173">Next steps</span></span>
<span data-ttu-id="ac4dc-174">toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:</span><span class="sxs-lookup"><span data-stu-id="ac4dc-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="ac4dc-175">Co to jest usługa Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="ac4dc-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="ac4dc-176">Interfejsy API dostępne przekazywania</span><span class="sxs-lookup"><span data-stu-id="ac4dc-176">Available Relay APIs</span></span>](relay-api-overview.md)
