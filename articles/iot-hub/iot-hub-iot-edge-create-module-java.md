---
title: "aaaCreate moduł Azure IoT krawędzi z językiem Java | Dokumentacja firmy Microsoft"
description: "W tym samouczku ilustrację, jak toowrite cz danych konwertera modułu przy użyciu hello najnowszych pakietów Azure IoT krawędzi Maven."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="64981-103">Utwórz moduł Azure IoT krawędzi z językiem Java</span><span class="sxs-lookup"><span data-stu-id="64981-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="64981-104">W tym samouczku ilustrację, jak jeden może zbudować modułu Azure IoT Edge w języku Java.</span><span class="sxs-lookup"><span data-stu-id="64981-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="64981-105">W tym samouczku opisano konfigurowanie środowiska i w jaki sposób toowrite [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) przy użyciu najnowszych pakietów Azure IoT krawędzi Maven hello modułu konwertera danych.</span><span class="sxs-lookup"><span data-stu-id="64981-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64981-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64981-106">Prerequisites</span></span>

<span data-ttu-id="64981-107">W tej sekcji zostanie skonfigurowany środowiska do tworzenia modułu IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="64981-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="64981-108">Ma to zastosowanie tooboth *64-bitowym systemie Windows* i *64-bitowego systemu Linux (8 Ubuntu/Debian)* systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="64981-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="64981-109">wymagane jest Hello następującego oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="64981-109">hello following software is required:</span></span>

* <span data-ttu-id="64981-110">[Klient Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="64981-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="64981-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="64981-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="64981-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="64981-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="64981-113">Otwieranie wiersza polecenia terminali okna i klonowania hello następujące repozytorium:</span><span class="sxs-lookup"><span data-stu-id="64981-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="64981-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="64981-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="64981-115">Ogólna architektura</span><span class="sxs-lookup"><span data-stu-id="64981-115">Overall architecture</span></span>

<span data-ttu-id="64981-116">Platforma Azure IoT krawędzi Hello silnie przyjmuje hello [architektura Neumanna Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="64981-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="64981-117">Co oznacza, że cały danej hello Azure IoT krawędzi architektury jest system, który przetwarza dane wejściowe i generuje dane wyjściowe; i każdego pojedynczego modułu jest również niewielki rozmiar podsystemu wejścia/wyjścia.</span><span class="sxs-lookup"><span data-stu-id="64981-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="64981-118">W tym samouczku wprowadzeniu hello następujące dwa moduły:</span><span class="sxs-lookup"><span data-stu-id="64981-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="64981-119">Moduł, który odbiera symulowanego [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sygnału i konwertuje ją na sformatowany [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="64981-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="64981-120">Moduł, który wyświetla hello Odebrano [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="64981-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="64981-121">Witaj poniższy obraz przedstawia hello typowe end-to-end przepływu danych dla tego projektu:</span><span class="sxs-lookup"><span data-stu-id="64981-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="64981-122">![Przepływ danych między modułami trzy](media/iot-hub-iot-edge-create-module/dataflow.png "dane wejściowe: symulowane cz modułu; Procesor: Konwertera modułu; Dane wyjściowe: Moduł drukarki")</span><span class="sxs-lookup"><span data-stu-id="64981-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="64981-123">Znajomość hello kodu</span><span class="sxs-lookup"><span data-stu-id="64981-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="64981-124">Struktura projekt maven</span><span class="sxs-lookup"><span data-stu-id="64981-124">Maven project structure</span></span>

<span data-ttu-id="64981-125">Ponieważ pakiety krawędzi IoT Azure są oparte na Maven, potrzebujemy toocreate typowe struktury projekt Maven, która zawiera `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="64981-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="64981-126">Witaj POM dziedziczy hello `com.microsoft.azure.gateway.gateway-module-base` pakiet, który deklaruje wszystkie zależności hello wymaganej przez projekt moduł, który zawiera pliki binarne środowiska wykonawczego hello, ścieżka pliku konfiguracji bramy hello oraz sposób wykonywania hello.</span><span class="sxs-lookup"><span data-stu-id="64981-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="64981-127">Możemy zaoszczędzić wiele czasu i wyeliminować toowrite potrzeby hello i wielokrotnie przepisywania setki wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="64981-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="64981-128">Potrzebujemy tooupdate plik pom.xml przez zadeklarowanie hello wymagane zależności/wtyczki i nazwę hello toobe pliku konfiguracji hello używany przez naszych modułu, jak pokazano w hello następującego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="64981-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="64981-129">Podstawową wiedzę na temat modułu krawędzi IoT Azure</span><span class="sxs-lookup"><span data-stu-id="64981-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="64981-130">Moduł Azure IoT krawędzi można traktować jako procesor danych, którego zadaniem jest: wejściowych go przetworzyć i generowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="64981-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="64981-131">dane wejściowe Hello może być danych z urządzenia (takie jak czujnik ruchu), wiadomości z innymi modułami lub jakikolwiek inny (na przykład liczba okresowo generowane przez czasomierz).</span><span class="sxs-lookup"><span data-stu-id="64981-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="64981-132">Hello jest podobne toohello danych wejściowych, może ją wywołać zachowanie sprzętu (na przykład hello migający LED), moduły tooother wiadomości lub jakikolwiek inny (na przykład konsola toohello drukowania).</span><span class="sxs-lookup"><span data-stu-id="64981-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="64981-133">Moduły komunikują się ze sobą przy użyciu `com.microsoft.azure.gateway.messaging.Message` klasy.</span><span class="sxs-lookup"><span data-stu-id="64981-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="64981-134">Witaj **zawartości** z `Message` jest tablica bajtów, które jest w stanie reprezentujący każdego typu danych, które chcesz.</span><span class="sxs-lookup"><span data-stu-id="64981-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="64981-135">**Właściwości** są również dostępne w hello `Message` i są po prostu mapowania ciąg ciąg.</span><span class="sxs-lookup"><span data-stu-id="64981-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="64981-136">Można traktować **właściwości** hello nagłówki żądania HTTP lub hello metadane pliku.</span><span class="sxs-lookup"><span data-stu-id="64981-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="64981-137">W kolejności toodevelop modułu Azure IoT krawędzi w języku Java, należy toocreate nowe klasy modułu, która dziedziczy `com.microsoft.azure.gateway.core.GatewayModule` i implementację metody abstrakcyjne hello wymagane `receive()` i `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="64981-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="64981-138">W tym momencie możesz również opcjonalne hello tooimplement `start()` lub `create()` również metody.</span><span class="sxs-lookup"><span data-stu-id="64981-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="64981-139">Witaj następującego fragmentu kodu pokazuje sposób tooget uruchamiania, tworzenia modułu Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="64981-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="64981-140">Moduł konwertera</span><span class="sxs-lookup"><span data-stu-id="64981-140">Converter module</span></span>

| <span data-ttu-id="64981-141">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="64981-141">Input</span></span>                    | <span data-ttu-id="64981-142">Procesor</span><span class="sxs-lookup"><span data-stu-id="64981-142">Processor</span></span>                              | <span data-ttu-id="64981-143">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="64981-143">Output</span></span>                 | <span data-ttu-id="64981-144">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="64981-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="64981-145">Komunikat danych temperatury</span><span class="sxs-lookup"><span data-stu-id="64981-145">Temperature data message</span></span> | <span data-ttu-id="64981-146">Analizowanie i utworzyć nowy komunikat JSON</span><span class="sxs-lookup"><span data-stu-id="64981-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="64981-147">Komunikat JSON struktury</span><span class="sxs-lookup"><span data-stu-id="64981-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="64981-148">Jest to typowe moduł Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="64981-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="64981-149">Akceptuje temperatury komunikaty z innymi modułami (sprzętowy moduł, lub w tym przypadku naszej symulowane modułu cz); a następnie normalizowane wiadomości powitania temperatury tooa strukturę JSON wiadomości (w tym dołączanie identyfikator wiadomości powitania, ustawienie właściwości hello czy potrzebujemy tootrigger hello temperatury alertu i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="64981-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="64981-150">Moduł drukarki</span><span class="sxs-lookup"><span data-stu-id="64981-150">Printer module</span></span>

| <span data-ttu-id="64981-151">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="64981-151">Input</span></span>                          | <span data-ttu-id="64981-152">Procesor</span><span class="sxs-lookup"><span data-stu-id="64981-152">Processor</span></span> | <span data-ttu-id="64981-153">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="64981-153">Output</span></span>                     | <span data-ttu-id="64981-154">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="64981-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="64981-155">Dowolny komunikat z innymi modułami</span><span class="sxs-lookup"><span data-stu-id="64981-155">Any message from other modules</span></span> | <span data-ttu-id="64981-156">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="64981-156">N/A</span></span>       | <span data-ttu-id="64981-157">Zaloguj się tooconsole wiadomość hello</span><span class="sxs-lookup"><span data-stu-id="64981-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="64981-158">Jest to proste i nie wymaga objaśnień, moduł, który wyświetla okno terminalu toohello wiadomości powitania odebrane.</span><span class="sxs-lookup"><span data-stu-id="64981-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="64981-159">Konfiguracja programu Azure IoT krawędzi</span><span class="sxs-lookup"><span data-stu-id="64981-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="64981-160">Hello ostatnim krokiem przed uruchomieniem modułów hello jest tooestablish hello połączenia między modułami i tooconfigure hello Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="64981-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="64981-161">Najpierw musimy toodeclare naszych ładujący Java (od momentu krawędzi IoT Azure obsługuje modułów ładujących różnych języków), którego można odwoływać się jego `name` w sekcjach hello później.</span><span class="sxs-lookup"><span data-stu-id="64981-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="64981-162">Po zadeklarowaniu możemy naszych ładowarki, firma Microsoft będzie również konieczne toodeclare również naszych modułów.</span><span class="sxs-lookup"><span data-stu-id="64981-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="64981-163">Podobne ładowarki hello toodeclaring, ich mogą się też odwoływać linie ich `name` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="64981-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="64981-164">Przy deklarowaniu modułu, potrzebujemy toospecify hello modułu ładującego on powinien używać (która powinna być hello jedną zdefiniowanego przed) i hello punktu wejścia (powinna być nazwą klasy znormalizowane hello naszych modułu) dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="64981-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="64981-165">Witaj `simulated_device` jest natywny moduł, który jest dostępny w hello Azure IoT krawędzi podstawowe środowisko uruchomieniowe pakietu.</span><span class="sxs-lookup"><span data-stu-id="64981-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="64981-166">Zawsze należy uwzględnić `args` w pliku JSON, nawet jeśli jest ona hello `null`.</span><span class="sxs-lookup"><span data-stu-id="64981-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="64981-167">Na końcu hello konfiguracji hello nawiązanie połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="64981-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="64981-168">Każde połączenie jest wyrażona w `source` i `sink`.</span><span class="sxs-lookup"><span data-stu-id="64981-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="64981-169">Powinna zarówno odwołujących się wstępnie zdefiniowanych modułów.</span><span class="sxs-lookup"><span data-stu-id="64981-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="64981-170">wiadomości powitania dane wyjściowe z `source` modułu zostaną przekazane wprowadzania toohello `sink` modułu.</span><span class="sxs-lookup"><span data-stu-id="64981-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a><span data-ttu-id="64981-171">Uruchomione moduły hello</span><span class="sxs-lookup"><span data-stu-id="64981-171">Running hello modules</span></span>

<span data-ttu-id="64981-172">Użyj `mvn package` toobuild wszystko do hello `target/` folderu.</span><span class="sxs-lookup"><span data-stu-id="64981-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="64981-173">`mvn clean package`jest także zalecana dla czystego kompilacji.</span><span class="sxs-lookup"><span data-stu-id="64981-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="64981-174">Użyj `mvn exec:exec` toorun hello Azure IoT Edge i przestrzegać wszystkich właściwości hello hello temperatury danych i czy konsoli drukowanej toohello według stałej stawki.</span><span class="sxs-lookup"><span data-stu-id="64981-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="64981-175">Jeśli chcesz, aby aplikacja hello tooterminate, naciśnij klawisz `<Enter>` klucza.</span><span class="sxs-lookup"><span data-stu-id="64981-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64981-176">Nie zaleca się toouse Ctrl + C tooterminate hello krawędzi IoT bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64981-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="64981-177">Ponieważ może to spowodować tooterminate procesu hello nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="64981-177">As this may cause hello process tooterminate abnormally.</span></span>

