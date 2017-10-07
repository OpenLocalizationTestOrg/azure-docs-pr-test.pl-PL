---
title: "aaaCreate moduł Azure IoT krawędzi za pomocą języka Node.js | Dokumentacja firmy Microsoft"
description: "W tym samouczku ilustrację, jak toowrite cz danych konwertera modułu przy użyciu hello najnowszych pakietów NPM krawędzi IoT Azure i narzędzia Yeoman generatora."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Utwórz moduł Azure IoT krawędzi za pomocą języka Node.js

W tym samouczku ilustrację jak toocreate modułu Azure IoT Edge w JS.

W tym samouczku będziemy zapoznaj się z artykułem Konfigurowanie środowiska i w jaki sposób toowrite [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) przy użyciu najnowszych pakietów NPM krawędzi IoT Azure hello modułu konwertera danych.

## <a name="prerequisites"></a>Wymagania wstępne

W tej sekcji służy do konfigurowania środowiska do tworzenia modułu IoT krawędzi. Ma to zastosowanie tooboth *64-bitowym systemie Windows* i *64-bitowego systemu Linux (Ubuntu) 14 +* systemów operacyjnych.

wymagane jest Hello następującego oprogramowania:
* [Klient Git](https://git-scm.com/downloads).
* [Węzeł LTS](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Architektura

Platforma Azure IoT krawędzi Hello silnie przyjmuje hello [architektura Neumanna Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Co oznacza, że cały danej hello Azure IoT krawędzi architektury to system, który przetwarza dane wejściowe i generuje dane wyjściowe; i każdego pojedynczego modułu jest również niewielki rozmiar podsystemu wejścia/wyjścia. W tym samouczku wprowadzeniu hello następujące dwa moduły:

1. Moduł, który odbiera symulowanego [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sygnału i konwertuje ją na sformatowany [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.
2. Moduł, który wyświetla hello Odebrano [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.

Witaj poniższy obraz przedstawia hello przepływu danych tooend typowe zakończenia dla tego projektu:

![Przepływ danych między modułami trzy](media/iot-hub-iot-edge-create-module/dataflow.png "dane wejściowe: symulowane cz modułu; Procesor: Konwertera modułu; Dane wyjściowe: Moduł drukarki")

## <a name="set-up-hello-environment"></a>Konfigurowanie środowiska hello
Poniżej zostanie przedstawiony zostanie sposób tooquickly konfigurowania środowiska toostart toowrite pierwszy modułu konwertera cz z JS.

### <a name="create-module-project"></a>Utwórz projekt modułu
1. Otwórz okno wiersza polecenia, uruchom `yo az-iot-gw-module`.
2. Wykonaj kroki hello na powitania ekranu toofinish hello inicjowania modułu projektu.

### <a name="project-structure"></a>Struktura projektu
Projekt modułu JS składa się z hello następujące składniki:

`modules`-hello dostosowane pliki źródłowe modułu JS. Zastąp domyślną hello `sensor.js` i `printer.js` z plikami modułu.

`app.js`-hello wpisu pliku toostart hello krawędzi wystąpienia.

`gw.config.json`-hello konfiguracji pliku toocustomize hello modułów toobe załadowanych przez krawędzi.

`package.json`-hello metadane dla modułu projektu.

`README.md`-hello podstawowe dokumentacji dla modułu projektu.


### <a name="package-file"></a>Plik pakietu

To `package.json` deklaruje wszystkich hello metadane wymagane przez projekt moduł zawierający hello nazwę, wersję, zapis, skrypty, środowisko uruchomieniowe i rozwoju zależności.

Następujący kod fragment kodu przedstawia sposób tooconfigure dla konwertera cz przykładowe projektu.
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a>Plik wejściowy
Witaj `app.js` definiuje hello sposób tooinitialize hello krawędzi wystąpienia. W tym miejscu nie potrzebujemy toomake zmiany.

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a>Interfejs modułu
Moduł Azure IoT krawędzi można traktować jako procesor danych, którego zadaniem jest: wejściowych go przetworzyć i generowania danych wyjściowych.

dane wejściowe Hello może być danych z urządzenia (takie jak czujnik ruchu), wiadomości z innymi modułami lub jakikolwiek inny (na przykład liczba okresowo generowane przez czasomierz).

Hello jest podobne toohello danych wejściowych, może ją wywołać zachowanie sprzętu (na przykład hello migający LED), moduły tooother wiadomości lub jakikolwiek inny (na przykład konsola toohello drukowania).

Moduły komunikują się ze sobą przy użyciu `message` obiektu. Witaj **zawartości** z `message` jest umożliwiającej reprezentujący każdego typu danych, które chcesz tablicy bajtów. **Właściwości** są również dostępne w hello `message` i są po prostu mapowania ciąg ciąg. Można traktować **właściwości** hello nagłówki żądania HTTP lub hello metadane pliku.

W kolejności toodevelop modułu Azure IoT krawędzi w JS, potrzebujesz toocreate nowego obiektu modułu, który implementuje metody hello wymagane `receive()`. W tym momencie możesz również opcjonalne hello tooimplement `create()` lub `start()`, lub `destroy()` również metody. Witaj, tworzenia szkieletu obiektu modułu JS pokazuje Hello następującego fragmentu kodu.

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a>Moduł konwertera
| Dane wejściowe                    | Procesor                              | Dane wyjściowe                 | Plik źródłowy            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Komunikat danych temperatury | Analizowanie i utworzyć nowy komunikat JSON | Komunikat JSON struktury | `converter.js` |

Jest to typowe moduł Azure IoT krawędzi. Akceptuje temperatury komunikaty z innymi modułami (sprzętowy moduł, lub w tym przypadku naszej symulowane modułu cz); a następnie normalizowane wiadomości powitania temperatury tooa strukturę JSON wiadomości (w tym dołączanie identyfikator wiadomości powitania, ustawienie właściwości hello czy potrzebujemy tootrigger hello temperatury alertu i tak dalej).

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a>Moduł drukarki
| Dane wejściowe                          | Procesor | Dane wyjściowe                     | Plik źródłowy          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Dowolny komunikat z innymi modułami | Nie dotyczy       | Zaloguj się tooconsole wiadomość hello | `printer.js` |

Ten moduł jest proste, nie wymaga objaśnień, który wyświetla okno terminalu toohello hello odebrane wiadomości (właściwości, zawartości).

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Konfiguracja
Hello ostatnim krokiem przed uruchomieniem modułów hello jest tooestablish hello połączenia między modułami i tooconfigure hello Azure IoT krawędzi.

Najpierw musimy toodeclare naszych `node` modułu ładującego (od momentu krawędzi IoT Azure obsługuje modułów ładujących różnych języków), które można odwoływać się jego `name` w sekcjach hello później.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Po zadeklarowaniu możemy naszych ładowarki, również potrzebujemy toodeclare również naszych modułów. Podobne ładowarki hello toodeclaring, ich mogą się też odwoływać linie ich `name` atrybutu. Przy deklarowaniu modułu, potrzebujemy toospecify hello modułu ładującego on powinien używać (która powinna być hello jedną zdefiniowanego przed) i hello punktu wejścia (powinna być nazwą klasy znormalizowane hello naszych modułu) dla każdego modułu. Witaj `simulated_device` moduł jest modułem macierzystym, który znajduje się w hello Azure IoT krawędzi podstawowe środowisko uruchomieniowe pakietu. Obejmują `args` w pliku JSON, nawet jeśli jest ona hello `null`.

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

Na końcu hello konfiguracji hello nawiązanie połączenia hello. Każde połączenie jest wyrażona w `source` i `sink`. Powinna zarówno odwołujących się wstępnie zdefiniowanych modułów. wiadomości powitania dane wyjściowe z `source` modułu jest przekazywany wprowadzania toohello `sink` modułu.

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-hello-modules"></a>Uruchomione moduły hello
1. `npm install`
2. `npm start`

Jeśli chcesz, aby aplikacja hello tooterminate, naciśnij klawisz `<Enter>` klucza.

> [!IMPORTANT]
> Nie zaleca się toouse Ctrl + C tooterminate hello krawędzi IoT aplikacji. Ponieważ w ten sposób może spowodować tooterminate procesu hello nieprawidłowo.
