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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Utwórz moduł Azure IoT krawędzi z językiem Java

W tym samouczku ilustrację, jak jeden może zbudować modułu Azure IoT Edge w języku Java.

W tym samouczku opisano konfigurowanie środowiska i w jaki sposób toowrite [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) przy użyciu najnowszych pakietów Azure IoT krawędzi Maven hello modułu konwertera danych.

## <a name="prerequisites"></a>Wymagania wstępne

W tej sekcji zostanie skonfigurowany środowiska do tworzenia modułu IoT krawędzi. Ma to zastosowanie tooboth *64-bitowym systemie Windows* i *64-bitowego systemu Linux (8 Ubuntu/Debian)* systemów operacyjnych.

wymagane jest Hello następującego oprogramowania:

* [Klient Git](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Otwieranie wiersza polecenia terminali okna i klonowania hello następujące repozytorium:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Ogólna architektura

Platforma Azure IoT krawędzi Hello silnie przyjmuje hello [architektura Neumanna Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Co oznacza, że cały danej hello Azure IoT krawędzi architektury jest system, który przetwarza dane wejściowe i generuje dane wyjściowe; i każdego pojedynczego modułu jest również niewielki rozmiar podsystemu wejścia/wyjścia. W tym samouczku wprowadzeniu hello następujące dwa moduły:

1. Moduł, który odbiera symulowanego [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sygnału i konwertuje ją na sformatowany [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.
2. Moduł, który wyświetla hello Odebrano [JSON](https://en.wikipedia.org/wiki/JSON) wiadomości.

Witaj poniższy obraz przedstawia hello typowe end-to-end przepływu danych dla tego projektu:

![Przepływ danych między modułami trzy](media/iot-hub-iot-edge-create-module/dataflow.png "dane wejściowe: symulowane cz modułu; Procesor: Konwertera modułu; Dane wyjściowe: Moduł drukarki")

## <a name="understanding-hello-code"></a>Znajomość hello kodu

### <a name="maven-project-structure"></a>Struktura projekt maven

Ponieważ pakiety krawędzi IoT Azure są oparte na Maven, potrzebujemy toocreate typowe struktury projekt Maven, która zawiera `pom.xml` pliku.

Witaj POM dziedziczy hello `com.microsoft.azure.gateway.gateway-module-base` pakiet, który deklaruje wszystkie zależności hello wymaganej przez projekt moduł, który zawiera pliki binarne środowiska wykonawczego hello, ścieżka pliku konfiguracji bramy hello oraz sposób wykonywania hello. Możemy zaoszczędzić wiele czasu i wyeliminować toowrite potrzeby hello i wielokrotnie przepisywania setki wierszy kodu.

Potrzebujemy tooupdate plik pom.xml przez zadeklarowanie hello wymagane zależności/wtyczki i nazwę hello toobe pliku konfiguracji hello używany przez naszych modułu, jak pokazano w hello następującego fragmentu kodu.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Podstawową wiedzę na temat modułu krawędzi IoT Azure

Moduł Azure IoT krawędzi można traktować jako procesor danych, którego zadaniem jest: wejściowych go przetworzyć i generowania danych wyjściowych.

dane wejściowe Hello może być danych z urządzenia (takie jak czujnik ruchu), wiadomości z innymi modułami lub jakikolwiek inny (na przykład liczba okresowo generowane przez czasomierz).

Hello jest podobne toohello danych wejściowych, może ją wywołać zachowanie sprzętu (na przykład hello migający LED), moduły tooother wiadomości lub jakikolwiek inny (na przykład konsola toohello drukowania).

Moduły komunikują się ze sobą przy użyciu `com.microsoft.azure.gateway.messaging.Message` klasy. Witaj **zawartości** z `Message` jest tablica bajtów, które jest w stanie reprezentujący każdego typu danych, które chcesz. **Właściwości** są również dostępne w hello `Message` i są po prostu mapowania ciąg ciąg. Można traktować **właściwości** hello nagłówki żądania HTTP lub hello metadane pliku.

W kolejności toodevelop modułu Azure IoT krawędzi w języku Java, należy toocreate nowe klasy modułu, która dziedziczy `com.microsoft.azure.gateway.core.GatewayModule` i implementację metody abstrakcyjne hello wymagane `receive()` i `destroy()`. W tym momencie możesz również opcjonalne hello tooimplement `start()` lub `create()` również metody. Witaj następującego fragmentu kodu pokazuje sposób tooget uruchamiania, tworzenia modułu Azure IoT krawędzi.

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

### <a name="converter-module"></a>Moduł konwertera

| Dane wejściowe                    | Procesor                              | Dane wyjściowe                 | Plik źródłowy            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Komunikat danych temperatury | Analizowanie i utworzyć nowy komunikat JSON | Komunikat JSON struktury | `ConverterModule.java` |

Jest to typowe moduł Azure IoT krawędzi. Akceptuje temperatury komunikaty z innymi modułami (sprzętowy moduł, lub w tym przypadku naszej symulowane modułu cz); a następnie normalizowane wiadomości powitania temperatury tooa strukturę JSON wiadomości (w tym dołączanie identyfikator wiadomości powitania, ustawienie właściwości hello czy potrzebujemy tootrigger hello temperatury alertu i tak dalej).

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

### <a name="printer-module"></a>Moduł drukarki

| Dane wejściowe                          | Procesor | Dane wyjściowe                     | Plik źródłowy          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Dowolny komunikat z innymi modułami | Nie dotyczy       | Zaloguj się tooconsole wiadomość hello | `PrinterModule.java` |

Jest to proste i nie wymaga objaśnień, moduł, który wyświetla okno terminalu toohello wiadomości powitania odebrane.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Konfiguracja programu Azure IoT krawędzi

Hello ostatnim krokiem przed uruchomieniem modułów hello jest tooestablish hello połączenia między modułami i tooconfigure hello Azure IoT krawędzi.

Najpierw musimy toodeclare naszych ładujący Java (od momentu krawędzi IoT Azure obsługuje modułów ładujących różnych języków), którego można odwoływać się jego `name` w sekcjach hello później.

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

Po zadeklarowaniu możemy naszych ładowarki, firma Microsoft będzie również konieczne toodeclare również naszych modułów. Podobne ładowarki hello toodeclaring, ich mogą się też odwoływać linie ich `name` atrybutu. Przy deklarowaniu modułu, potrzebujemy toospecify hello modułu ładującego on powinien używać (która powinna być hello jedną zdefiniowanego przed) i hello punktu wejścia (powinna być nazwą klasy znormalizowane hello naszych modułu) dla każdego modułu. Witaj `simulated_device` jest natywny moduł, który jest dostępny w hello Azure IoT krawędzi podstawowe środowisko uruchomieniowe pakietu. Zawsze należy uwzględnić `args` w pliku JSON, nawet jeśli jest ona hello `null`.

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

Na końcu hello konfiguracji hello nawiązanie połączenia hello. Każde połączenie jest wyrażona w `source` i `sink`. Powinna zarówno odwołujących się wstępnie zdefiniowanych modułów. wiadomości powitania dane wyjściowe z `source` modułu zostaną przekazane wprowadzania toohello `sink` modułu.

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

## <a name="running-hello-modules"></a>Uruchomione moduły hello

Użyj `mvn package` toobuild wszystko do hello `target/` folderu. `mvn clean package`jest także zalecana dla czystego kompilacji.

Użyj `mvn exec:exec` toorun hello Azure IoT Edge i przestrzegać wszystkich właściwości hello hello temperatury danych i czy konsoli drukowanej toohello według stałej stawki.

Jeśli chcesz, aby aplikacja hello tooterminate, naciśnij klawisz `<Enter>` klucza.

> [!IMPORTANT]
> Nie zaleca się toouse Ctrl + C tooterminate hello krawędzi IoT bramy aplikacji. Ponieważ może to spowodować tooterminate procesu hello nieprawidłowo.

