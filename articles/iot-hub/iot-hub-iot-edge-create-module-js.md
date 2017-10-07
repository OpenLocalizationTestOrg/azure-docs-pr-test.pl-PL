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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="b247e-103">Utwórz moduł Azure IoT krawędzi za pomocą języka Node.js</span><span class="sxs-lookup"><span data-stu-id="b247e-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="b247e-104">W tym samouczku ilustrację jak toocreate modułu Azure IoT Edge w JS.</span><span class="sxs-lookup"><span data-stu-id="b247e-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="b247e-105">W tym samouczku będziemy zapoznaj się z artykułem Konfigurowanie środowiska i w jaki sposób toowrite [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) przy użyciu najnowszych pakietów NPM krawędzi IoT Azure hello modułu konwertera danych.</span><span class="sxs-lookup"><span data-stu-id="b247e-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b247e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b247e-106">Prerequisites</span></span>

<span data-ttu-id="b247e-107">W tej sekcji służy do konfigurowania środowiska do tworzenia modułu IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="b247e-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="b247e-108">Ma to zastosowanie tooboth *64-bitowym systemie Windows* i *64-bitowego systemu Linux (Ubuntu) 14 +* systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="b247e-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="b247e-109">wymagane jest Hello następującego oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="b247e-109">hello following software is required:</span></span>
* <span data-ttu-id="b247e-110">[Klient Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b247e-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="b247e-111">[Węzeł LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="b247e-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="b247e-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="b247e-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="b247e-113">Architektura</span><span class="sxs-lookup"><span data-stu-id="b247e-113">Architecture</span></span>

<span data-ttu-id="b247e-114">Platforma Azure IoT krawędzi Hello silnie przyjmuje hello [architektura Neumanna Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="b247e-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="b247e-115">Co oznacza, że cały danej hello Azure IoT krawędzi architektury to system, który przetwarza dane wejściowe i generuje dane wyjściowe; i każdego pojedynczego modułu jest również niewielki rozmiar podsystemu wejścia/wyjścia.</span><span class="sxs-lookup"><span data-stu-id="b247e-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="b247e-116">W tym samouczku wprowadzeniu hello następujące dwa moduły:</span><span class="sxs-lookup"><span data-stu-id="b247e-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="b247e-117">Moduł, który odbiera symulowanego [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sygnału i konwertuje ją na sformatowany [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="b247e-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="b247e-118">Moduł, który wyświetla hello Odebrano [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="b247e-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="b247e-119">Witaj poniższy obraz przedstawia hello przepływu danych tooend typowe zakończenia dla tego projektu:</span><span class="sxs-lookup"><span data-stu-id="b247e-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="b247e-120">![Przepływ danych między modułami trzy](media/iot-hub-iot-edge-create-module/dataflow.png "dane wejściowe: symulowane cz modułu; Procesor: Konwertera modułu; Dane wyjściowe: Moduł drukarki")</span><span class="sxs-lookup"><span data-stu-id="b247e-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="b247e-121">Konfigurowanie środowiska hello</span><span class="sxs-lookup"><span data-stu-id="b247e-121">Set up hello environment</span></span>
<span data-ttu-id="b247e-122">Poniżej zostanie przedstawiony zostanie sposób tooquickly konfigurowania środowiska toostart toowrite pierwszy modułu konwertera cz z JS.</span><span class="sxs-lookup"><span data-stu-id="b247e-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="b247e-123">Utwórz projekt modułu</span><span class="sxs-lookup"><span data-stu-id="b247e-123">Create module project</span></span>
1. <span data-ttu-id="b247e-124">Otwórz okno wiersza polecenia, uruchom `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="b247e-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="b247e-125">Wykonaj kroki hello na powitania ekranu toofinish hello inicjowania modułu projektu.</span><span class="sxs-lookup"><span data-stu-id="b247e-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="b247e-126">Struktura projektu</span><span class="sxs-lookup"><span data-stu-id="b247e-126">Project structure</span></span>
<span data-ttu-id="b247e-127">Projekt modułu JS składa się z hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="b247e-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="b247e-128">`modules`-hello dostosowane pliki źródłowe modułu JS.</span><span class="sxs-lookup"><span data-stu-id="b247e-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="b247e-129">Zastąp domyślną hello `sensor.js` i `printer.js` z plikami modułu.</span><span class="sxs-lookup"><span data-stu-id="b247e-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="b247e-130">`app.js`-hello wpisu pliku toostart hello krawędzi wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b247e-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="b247e-131">`gw.config.json`-hello konfiguracji pliku toocustomize hello modułów toobe załadowanych przez krawędzi.</span><span class="sxs-lookup"><span data-stu-id="b247e-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="b247e-132">`package.json`-hello metadane dla modułu projektu.</span><span class="sxs-lookup"><span data-stu-id="b247e-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="b247e-133">`README.md`-hello podstawowe dokumentacji dla modułu projektu.</span><span class="sxs-lookup"><span data-stu-id="b247e-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="b247e-134">Plik pakietu</span><span class="sxs-lookup"><span data-stu-id="b247e-134">Package file</span></span>

<span data-ttu-id="b247e-135">To `package.json` deklaruje wszystkich hello metadane wymagane przez projekt moduł zawierający hello nazwę, wersję, zapis, skrypty, środowisko uruchomieniowe i rozwoju zależności.</span><span class="sxs-lookup"><span data-stu-id="b247e-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="b247e-136">Następujący kod fragment kodu przedstawia sposób tooconfigure dla konwertera cz przykładowe projektu.</span><span class="sxs-lookup"><span data-stu-id="b247e-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="b247e-137">Plik wejściowy</span><span class="sxs-lookup"><span data-stu-id="b247e-137">Entry file</span></span>
<span data-ttu-id="b247e-138">Witaj `app.js` definiuje hello sposób tooinitialize hello krawędzi wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b247e-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="b247e-139">W tym miejscu nie potrzebujemy toomake zmiany.</span><span class="sxs-lookup"><span data-stu-id="b247e-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="b247e-140">Interfejs modułu</span><span class="sxs-lookup"><span data-stu-id="b247e-140">Interface of module</span></span>
<span data-ttu-id="b247e-141">Moduł Azure IoT krawędzi można traktować jako procesor danych, którego zadaniem jest: wejściowych go przetworzyć i generowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b247e-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="b247e-142">dane wejściowe Hello może być danych z urządzenia (takie jak czujnik ruchu), wiadomości z innymi modułami lub jakikolwiek inny (na przykład liczba okresowo generowane przez czasomierz).</span><span class="sxs-lookup"><span data-stu-id="b247e-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="b247e-143">Hello jest podobne toohello danych wejściowych, może ją wywołać zachowanie sprzętu (na przykład hello migający LED), moduły tooother wiadomości lub jakikolwiek inny (na przykład konsola toohello drukowania).</span><span class="sxs-lookup"><span data-stu-id="b247e-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="b247e-144">Moduły komunikują się ze sobą przy użyciu `message` obiektu.</span><span class="sxs-lookup"><span data-stu-id="b247e-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="b247e-145">Witaj **zawartości** z `message` jest umożliwiającej reprezentujący każdego typu danych, które chcesz tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="b247e-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="b247e-146">**Właściwości** są również dostępne w hello `message` i są po prostu mapowania ciąg ciąg.</span><span class="sxs-lookup"><span data-stu-id="b247e-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="b247e-147">Można traktować **właściwości** hello nagłówki żądania HTTP lub hello metadane pliku.</span><span class="sxs-lookup"><span data-stu-id="b247e-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="b247e-148">W kolejności toodevelop modułu Azure IoT krawędzi w JS, potrzebujesz toocreate nowego obiektu modułu, który implementuje metody hello wymagane `receive()`.</span><span class="sxs-lookup"><span data-stu-id="b247e-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="b247e-149">W tym momencie możesz również opcjonalne hello tooimplement `create()` lub `start()`, lub `destroy()` również metody.</span><span class="sxs-lookup"><span data-stu-id="b247e-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="b247e-150">Witaj, tworzenia szkieletu obiektu modułu JS pokazuje Hello następującego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="b247e-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="b247e-151">Moduł konwertera</span><span class="sxs-lookup"><span data-stu-id="b247e-151">Converter module</span></span>
| <span data-ttu-id="b247e-152">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="b247e-152">Input</span></span>                    | <span data-ttu-id="b247e-153">Procesor</span><span class="sxs-lookup"><span data-stu-id="b247e-153">Processor</span></span>                              | <span data-ttu-id="b247e-154">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="b247e-154">Output</span></span>                 | <span data-ttu-id="b247e-155">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="b247e-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="b247e-156">Komunikat danych temperatury</span><span class="sxs-lookup"><span data-stu-id="b247e-156">Temperature data message</span></span> | <span data-ttu-id="b247e-157">Analizowanie i utworzyć nowy komunikat JSON</span><span class="sxs-lookup"><span data-stu-id="b247e-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="b247e-158">Komunikat JSON struktury</span><span class="sxs-lookup"><span data-stu-id="b247e-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="b247e-159">Jest to typowe moduł Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="b247e-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="b247e-160">Akceptuje temperatury komunikaty z innymi modułami (sprzętowy moduł, lub w tym przypadku naszej symulowane modułu cz); a następnie normalizowane wiadomości powitania temperatury tooa strukturę JSON wiadomości (w tym dołączanie identyfikator wiadomości powitania, ustawienie właściwości hello czy potrzebujemy tootrigger hello temperatury alertu i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="b247e-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="b247e-161">Moduł drukarki</span><span class="sxs-lookup"><span data-stu-id="b247e-161">Printer module</span></span>
| <span data-ttu-id="b247e-162">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="b247e-162">Input</span></span>                          | <span data-ttu-id="b247e-163">Procesor</span><span class="sxs-lookup"><span data-stu-id="b247e-163">Processor</span></span> | <span data-ttu-id="b247e-164">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="b247e-164">Output</span></span>                     | <span data-ttu-id="b247e-165">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="b247e-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="b247e-166">Dowolny komunikat z innymi modułami</span><span class="sxs-lookup"><span data-stu-id="b247e-166">Any message from other modules</span></span> | <span data-ttu-id="b247e-167">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="b247e-167">N/A</span></span>       | <span data-ttu-id="b247e-168">Zaloguj się tooconsole wiadomość hello</span><span class="sxs-lookup"><span data-stu-id="b247e-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="b247e-169">Ten moduł jest proste, nie wymaga objaśnień, który wyświetla okno terminalu toohello hello odebrane wiadomości (właściwości, zawartości).</span><span class="sxs-lookup"><span data-stu-id="b247e-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="b247e-170">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b247e-170">Configuration</span></span>
<span data-ttu-id="b247e-171">Hello ostatnim krokiem przed uruchomieniem modułów hello jest tooestablish hello połączenia między modułami i tooconfigure hello Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="b247e-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="b247e-172">Najpierw musimy toodeclare naszych `node` modułu ładującego (od momentu krawędzi IoT Azure obsługuje modułów ładujących różnych języków), które można odwoływać się jego `name` w sekcjach hello później.</span><span class="sxs-lookup"><span data-stu-id="b247e-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="b247e-173">Po zadeklarowaniu możemy naszych ładowarki, również potrzebujemy toodeclare również naszych modułów.</span><span class="sxs-lookup"><span data-stu-id="b247e-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="b247e-174">Podobne ładowarki hello toodeclaring, ich mogą się też odwoływać linie ich `name` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="b247e-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="b247e-175">Przy deklarowaniu modułu, potrzebujemy toospecify hello modułu ładującego on powinien używać (która powinna być hello jedną zdefiniowanego przed) i hello punktu wejścia (powinna być nazwą klasy znormalizowane hello naszych modułu) dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="b247e-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="b247e-176">Witaj `simulated_device` moduł jest modułem macierzystym, który znajduje się w hello Azure IoT krawędzi podstawowe środowisko uruchomieniowe pakietu.</span><span class="sxs-lookup"><span data-stu-id="b247e-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="b247e-177">Obejmują `args` w pliku JSON, nawet jeśli jest ona hello `null`.</span><span class="sxs-lookup"><span data-stu-id="b247e-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="b247e-178">Na końcu hello konfiguracji hello nawiązanie połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="b247e-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="b247e-179">Każde połączenie jest wyrażona w `source` i `sink`.</span><span class="sxs-lookup"><span data-stu-id="b247e-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="b247e-180">Powinna zarówno odwołujących się wstępnie zdefiniowanych modułów.</span><span class="sxs-lookup"><span data-stu-id="b247e-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="b247e-181">wiadomości powitania dane wyjściowe z `source` modułu jest przekazywany wprowadzania toohello `sink` modułu.</span><span class="sxs-lookup"><span data-stu-id="b247e-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="b247e-182">Uruchomione moduły hello</span><span class="sxs-lookup"><span data-stu-id="b247e-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="b247e-183">Jeśli chcesz, aby aplikacja hello tooterminate, naciśnij klawisz `<Enter>` klucza.</span><span class="sxs-lookup"><span data-stu-id="b247e-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b247e-184">Nie zaleca się toouse Ctrl + C tooterminate hello krawędzi IoT aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b247e-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="b247e-185">Ponieważ w ten sposób może spowodować tooterminate procesu hello nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="b247e-185">As this way may cause hello process tooterminate abnormally.</span></span>
