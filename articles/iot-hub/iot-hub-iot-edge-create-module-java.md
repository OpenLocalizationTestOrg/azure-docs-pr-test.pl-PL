---
title: "Utwórz moduł Azure IoT krawędzi z językiem Java | Dokumentacja firmy Microsoft"
description: "W tym samouczku ilustrację jak napisać cz modułu konwertera danych przy użyciu najnowszych pakietów Azure IoT krawędzi Maven."
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
ms.openlocfilehash: 0c430272225d79737baec2be15ed7c93991cdeac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="2395b-103">Utwórz moduł Azure IoT krawędzi z językiem Java</span><span class="sxs-lookup"><span data-stu-id="2395b-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="2395b-104">W tym samouczku ilustrację, jak jeden może zbudować modułu Azure IoT Edge w języku Java.</span><span class="sxs-lookup"><span data-stu-id="2395b-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="2395b-105">W tym samouczku opisano konfiguracji środowiska i jak napisać [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modułu konwertera danych przy użyciu najnowszych pakietów Azure IoT krawędzi Maven.</span><span class="sxs-lookup"><span data-stu-id="2395b-105">In this tutorial, we will walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2395b-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2395b-106">Prerequisites</span></span>

<span data-ttu-id="2395b-107">W tej sekcji zostanie skonfigurowany środowiska do tworzenia modułu IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="2395b-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="2395b-108">Dotyczy ona obu *64-bitowym systemie Windows* i *64-bitowego systemu Linux (8 Ubuntu/Debian)* systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="2395b-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="2395b-109">Następujące oprogramowanie jest wymagane:</span><span class="sxs-lookup"><span data-stu-id="2395b-109">The following software is required:</span></span>

* <span data-ttu-id="2395b-110">[Klient Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2395b-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="2395b-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="2395b-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="2395b-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="2395b-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="2395b-113">Otwórz okno terminala wiersza polecenia i klonowania repozytorium na następujący:</span><span class="sxs-lookup"><span data-stu-id="2395b-113">Open a command-line terminal window and clone the following repository:</span></span>

1. <span data-ttu-id="2395b-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="2395b-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="2395b-115">Ogólna architektura</span><span class="sxs-lookup"><span data-stu-id="2395b-115">Overall architecture</span></span>

<span data-ttu-id="2395b-116">Platforma Azure IoT krawędzi silnie przyjmuje [architektura Neumanna Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="2395b-116">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="2395b-117">Co oznacza, że całej architektury Azure IoT krawędzi system, który przetwarza dane wejściowe i generuje dane wyjściowe; i każdego pojedynczego modułu jest również niewielki rozmiar podsystemu wejścia/wyjścia.</span><span class="sxs-lookup"><span data-stu-id="2395b-117">Which means that the entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="2395b-118">W tym samouczku wprowadzeniu dwóch następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="2395b-118">In this tutorial, we will introduce the following two modules:</span></span>

1. <span data-ttu-id="2395b-119">Moduł, który odbiera symulowanego [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sygnału i konwertuje ją na sformatowany [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2395b-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="2395b-120">Moduł, który wyświetla odebranej [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2395b-120">A module which prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="2395b-121">Poniższa ilustracja przedstawia typowego przepływu end-to-end danych dla tego projektu:</span><span class="sxs-lookup"><span data-stu-id="2395b-121">The following image displays the typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="2395b-122">![Przepływ danych między modułami trzy](media/iot-hub-iot-edge-create-module/dataflow.png "dane wejściowe: symulowane cz modułu; Procesor: Konwertera modułu; Dane wyjściowe: Moduł drukarki")</span><span class="sxs-lookup"><span data-stu-id="2395b-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="2395b-123">Opis kodu</span><span class="sxs-lookup"><span data-stu-id="2395b-123">Understanding the code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="2395b-124">Struktura projekt maven</span><span class="sxs-lookup"><span data-stu-id="2395b-124">Maven project structure</span></span>

<span data-ttu-id="2395b-125">Ponieważ pakiety krawędzi IoT Azure są oparte na Maven, należy utworzyć typowe struktury projekt Maven, która zawiera `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="2395b-125">Since Azure IoT Edge packages are based on Maven, we need to create a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="2395b-126">Dziedziczy POM `com.microsoft.azure.gateway.gateway-module-base` pakiet, który deklaruje wszystkie zależności wymagane przez projekt moduł, który zawiera pliki binarne środowiska wykonawczego, ścieżka pliku konfiguracji bramy i sposób wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2395b-126">The POM inherits from the `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of the dependencies needed by a module project which includes the runtime binaries, the gateway configuration file path, and the execution behavior.</span></span> <span data-ttu-id="2395b-127">To możemy zaoszczędzić wiele czasu i wyeliminować potrzebę zapisać i ponownie setki wierszy kodu wielokrotnie.</span><span class="sxs-lookup"><span data-stu-id="2395b-127">This saves us lots of time and eliminate the need to write and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="2395b-128">Należy zaktualizować plik pom.xml przez zadeklarowanie wymagane zależności/dodatków plug-in i nazwę pliku konfiguracji, które mają być używane przez naszych modułu, jak pokazano w poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="2395b-128">We need to update the pom.xml file by declaring the required dependencies/plugins and the name of the configuration file to be used by our module as shown in the following code snippet.</span></span>

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

  <!-- Set the filename of the Azure IoT Edge configuration located
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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="2395b-129">Podstawową wiedzę na temat modułu krawędzi IoT Azure</span><span class="sxs-lookup"><span data-stu-id="2395b-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="2395b-130">Moduł Azure IoT krawędzi można traktować jako procesor danych, którego zadaniem jest: wejściowych go przetworzyć i generowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2395b-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="2395b-131">Dane wejściowe mogą być danych z urządzenia (takie jak czujnik ruchu), wiadomości z innymi modułami lub jakikolwiek inny (na przykład liczba okresowo generowane przez czasomierz).</span><span class="sxs-lookup"><span data-stu-id="2395b-131">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="2395b-132">Wynik jest podobny do danych wejściowych, może ją wywołać zachowanie sprzętu (na przykład migający LED), wiadomości do innych modułów lub jakikolwiek inny (na przykład drukowanie do konsoli).</span><span class="sxs-lookup"><span data-stu-id="2395b-132">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="2395b-133">Moduły komunikują się ze sobą przy użyciu `com.microsoft.azure.gateway.messaging.Message` klasy.</span><span class="sxs-lookup"><span data-stu-id="2395b-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="2395b-134">**Zawartości** z `Message` jest tablica bajtów, które jest w stanie reprezentujący każdego typu danych, które chcesz.</span><span class="sxs-lookup"><span data-stu-id="2395b-134">The **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="2395b-135">**Właściwości** dostępne są również `Message` i są po prostu mapowania ciąg ciąg.</span><span class="sxs-lookup"><span data-stu-id="2395b-135">**Properties** are also available in the `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="2395b-136">Można traktować **właściwości** jako nagłówków żądań HTTP lub metadane pliku.</span><span class="sxs-lookup"><span data-stu-id="2395b-136">You may think of **Properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="2395b-137">Aby opracować modułu Azure IoT krawędzi w języku Java, należy utworzyć nowe klasy modułu, która dziedziczy `com.microsoft.azure.gateway.core.GatewayModule` i wdrożenie wymaganych metody abstrakcyjne `receive()` i `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="2395b-137">In order to develop an Azure IoT Edge module in Java, you need to create a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement the required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="2395b-138">W tym momencie można też do zaimplementowania opcjonalny `start()` lub `create()` również metody.</span><span class="sxs-lookup"><span data-stu-id="2395b-138">At this point, you may also choose to implement the optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="2395b-139">Poniższy fragment kodu pokazano, jak rozpocząć tworzenie modułu Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="2395b-139">The following code snippet shows you how to get started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let the GatewayModule do the dirty work of initialization. It's also
       a good time to parse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire the resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time to release all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic to process the input message. This method is required. */
    // ...
    /* Use publish() method to do the output. You are
       allowed to publish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="2395b-140">Moduł konwertera</span><span class="sxs-lookup"><span data-stu-id="2395b-140">Converter module</span></span>

| <span data-ttu-id="2395b-141">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="2395b-141">Input</span></span>                    | <span data-ttu-id="2395b-142">Procesor</span><span class="sxs-lookup"><span data-stu-id="2395b-142">Processor</span></span>                              | <span data-ttu-id="2395b-143">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2395b-143">Output</span></span>                 | <span data-ttu-id="2395b-144">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="2395b-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="2395b-145">Komunikat danych temperatury</span><span class="sxs-lookup"><span data-stu-id="2395b-145">Temperature data message</span></span> | <span data-ttu-id="2395b-146">Analizowanie i utworzyć nowy komunikat JSON</span><span class="sxs-lookup"><span data-stu-id="2395b-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="2395b-147">Komunikat JSON struktury</span><span class="sxs-lookup"><span data-stu-id="2395b-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="2395b-148">Jest to typowe moduł Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="2395b-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="2395b-149">Akceptuje temperatury komunikaty z innymi modułami (sprzętowy moduł, lub w tym przypadku naszej symulowane modułu cz); a następnie normalizowane komunikatu temperatury w strukturze komunikat JSON (w tym dołączanie identyfikator komunikatu ustawienie właściwości czy musimy wyzwolenia alertu temperatury i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="2395b-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="2395b-150">Moduł drukarki</span><span class="sxs-lookup"><span data-stu-id="2395b-150">Printer module</span></span>

| <span data-ttu-id="2395b-151">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="2395b-151">Input</span></span>                          | <span data-ttu-id="2395b-152">Procesor</span><span class="sxs-lookup"><span data-stu-id="2395b-152">Processor</span></span> | <span data-ttu-id="2395b-153">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2395b-153">Output</span></span>                     | <span data-ttu-id="2395b-154">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="2395b-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="2395b-155">Dowolny komunikat z innymi modułami</span><span class="sxs-lookup"><span data-stu-id="2395b-155">Any message from other modules</span></span> | <span data-ttu-id="2395b-156">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="2395b-156">N/A</span></span>       | <span data-ttu-id="2395b-157">Zaloguj się do konsoli wiadomości</span><span class="sxs-lookup"><span data-stu-id="2395b-157">Log the message to console</span></span> | `PrinterModule.java` |

<span data-ttu-id="2395b-158">Jest to proste i nie wymaga objaśnień, moduł, który generuje odebrane wiadomości do okna terminala.</span><span class="sxs-lookup"><span data-stu-id="2395b-158">This is a simple, self-explanatory, module which outputs the received messages to the terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="2395b-159">Konfiguracja programu Azure IoT krawędzi</span><span class="sxs-lookup"><span data-stu-id="2395b-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="2395b-160">Ostatnim krokiem przed uruchomieniem modułów jest skonfigurowanie krawędzi IoT Azure oraz do zestawiania połączeń między modułami.</span><span class="sxs-lookup"><span data-stu-id="2395b-160">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="2395b-161">Najpierw należy zadeklarować naszych ładujący Java (od momentu krawędzi IoT Azure obsługuje modułów ładujących różnych języków), którego można odwoływać się jego `name` w sekcjach później.</span><span class="sxs-lookup"><span data-stu-id="2395b-161">First we need to declare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

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

<span data-ttu-id="2395b-162">Po zadeklarowaniu możemy naszych ładowarki, potrzebujemy będzie zadeklarować również naszych modułów.</span><span class="sxs-lookup"><span data-stu-id="2395b-162">Once we have declared our loaders, we will also need to declare our modules as well.</span></span> <span data-ttu-id="2395b-163">Podobnie jak deklarowanie ładowarki, ich mogą się też odwoływać linie ich `name` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2395b-163">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="2395b-164">Przy deklarowaniu modułu, należy określić moduł ładujący on powinien używać (który powinien być zdefiniowanego przed) i punktu wejścia (powinna być nazwa klasy znormalizowane naszych modułu) dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="2395b-164">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="2395b-165">`simulated_device` Modułu jest uwzględniony w pakiecie Azure IoT krawędzi core czasu wykonywania modułu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="2395b-165">The `simulated_device` module is a native module which is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="2395b-166">Zawsze należy uwzględnić `args` w formacie JSON plików, nawet jeśli jest ona `null`.</span><span class="sxs-lookup"><span data-stu-id="2395b-166">You should always include `args` in the JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="2395b-167">Po zakończeniu konfiguracji nawiązanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="2395b-167">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="2395b-168">Każde połączenie jest wyrażona w `source` i `sink`.</span><span class="sxs-lookup"><span data-stu-id="2395b-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="2395b-169">Powinna zarówno odwołujących się wstępnie zdefiniowanych modułów.</span><span class="sxs-lookup"><span data-stu-id="2395b-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="2395b-170">Komunikat dane wyjściowe z `source` modułu zostaną przekazane w danych wejściowych `sink` modułu.</span><span class="sxs-lookup"><span data-stu-id="2395b-170">The output message of `source` module will be forwarded to the input of `sink` module.</span></span>

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

## <a name="running-the-modules"></a><span data-ttu-id="2395b-171">Uruchomione moduły</span><span class="sxs-lookup"><span data-stu-id="2395b-171">Running the modules</span></span>

<span data-ttu-id="2395b-172">Użyj `mvn package` do tworzenia wszystko do `target/` folderu.</span><span class="sxs-lookup"><span data-stu-id="2395b-172">Use `mvn package` to build everything into the `target/` folder.</span></span> <span data-ttu-id="2395b-173">`mvn clean package`jest także zalecana dla czystego kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2395b-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="2395b-174">Użyj `mvn exec:exec` do uruchomienia krawędzi IoT Azure i powinno uwzględniać dane temperatury i wszystkie właściwości są podane w konsoli według stałej stawki.</span><span class="sxs-lookup"><span data-stu-id="2395b-174">Use `mvn exec:exec` to run the Azure IoT Edge and you should observe that the temperature data and all the properties are printed to the console at a fixed rate.</span></span>

<span data-ttu-id="2395b-175">Jeśli chcesz zakończyć tę aplikację, naciśnij klawisz `<Enter>` klucza.</span><span class="sxs-lookup"><span data-stu-id="2395b-175">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2395b-176">Użyj klawiszy Ctrl + C, aby przerwać aplikacji bramy krawędzi IoT jest niezalecane.</span><span class="sxs-lookup"><span data-stu-id="2395b-176">It is not recommended to use Ctrl + C to terminate the IoT Edge gateway application.</span></span> <span data-ttu-id="2395b-177">Ponieważ może to spowodować przerwanie wyjątkowo procesu.</span><span class="sxs-lookup"><span data-stu-id="2395b-177">As this may cause the process to terminate abnormally.</span></span>

