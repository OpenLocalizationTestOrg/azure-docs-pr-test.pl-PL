---
title: "zdarzenia aaaProcess z centrów zdarzeń z systemu Storm w usłudze HDInsight przy użyciu języka Java | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprocess danych usługi Event Hubs przy użyciu topologii Java Storm tworzone z Maven."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)

Dowiedz się, jak toouse Azure Event Hubs z systemu Storm w usłudze HDInsight. W tym przykładzie używane składników opartych na języku Java tooread i zapisu danych w usłudze Azure Event Hubs.

Usługa Azure Event Hubs umożliwia tooprocess olbrzymich ilości danych z urządzeń, aplikacji i witryn sieci Web. Witaj spout Centrum zdarzeń umożliwia łatwe toouse Apache Storm w usłudze HDInsight tooanalyze tych danych w czasie rzeczywistym. Można również napisać tooEvent danych koncentratory z Storm przy użyciu powitalne centra zdarzeń dla elementów bolt.

## <a name="prerequisites"></a>Wymagania wstępne

* Apache Storm w klastrze usługi HDInsight w wersji 3,6. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z systemu Storm w klastrze usługi HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* [Centrum zdarzeń Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Oracle Java Developer Kit (JDK) w wersji 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) lub równoważnego, takich jak [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): Maven to system projektu kompilacji dla projektów języka Java.

* Edytor tekstu lub zintegrowane środowisko programistyczne (IDE).

    > [!NOTE]
    > Z edytora lub IDE może mieć określone funkcje do pracy z Maven, który nie jest opisany w tym dokumencie. Informacje dotyczące możliwości hello środowiska edytowania dokumentacji hello hello produktu, którego używasz.

    * Klient SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Witaj `ssh` i `scp` poleceń. Są to klastra usługi HDInsight toohello pliki toocopy używane. W systemie Windows możesz uzyskać je za pośrednictwem Bash w systemie Windows 10.

## <a name="understanding-hello-example"></a>Przykład Witaj opis

Witaj [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) przykład zawiera dwie topologie:

Witaj `resources/writer.yaml` topologii zapisuje tooan losowe dane Azure Event Hub. danych Hello jest generowany przez hello `DeviceSpout` składnika i Identyfikatora losowe urządzenia i wartość urządzenia. Dlatego symuluje ona część sprzętu, który emituje identyfikator ciągu i wartość liczbową.

Te `resources/reader.yaml` topologii odczytuje dane z Centrum zdarzeń (danych hello napisane przez EventHubWriter,) analizuje dane JSON hello, a następnie rejestruje hello `deviceId` i `deviceValue` danych.

dane Hello są sformatowane jako dokument JSON przed jest zapisywane tooEvent koncentratora i odczytywana przez czytnik hello jest analizowany poza JSON i do spójnych kolekcji. Hello JSON format jest następujący:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Konfiguracja projektu

Witaj `POM.xml` plik zawiera informacje o konfiguracji dla tego projektu Maven. Witaj interesujące jest:

#### <a name="event-hub-components"></a>Składniki Centrum zdarzeń

składnik Hello odczytuje i zapisuje centra zdarzeń tooAzure znajduje się w hello [repozytorium HDInsight](https://github.com/hdinsight/mvn-rep). Witaj w następujących sekcjach hello `POM.xml` składniki hello ładowania pliku z tego repozytorium

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Witaj EventHubs Storm Spout zależności

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Plik xml definiuje zależność hello eventhubs pakiet, który zawiera spout do odczytywania z usługi Event Hubs i bolt do pisania tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Plik xml konfiguruje hello wynik toogenerate projektu dla języka Java 8, który jest używany przez usługi HDInsight 3.5 lub nowszej.

#### <a name="hello-maven-shade-plugin"></a>Witaj maven cień wtyczki

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

Plik xml konfiguruje hello rozwiązania toopackage hello w danych wyjściowych do jar pełny. Witaj jar zawiera hello kodu projektu i wymaganych zależności. Służy również do:

* Zmień nazwy plików licencji hello zależności.
* Wyklucz podpisów/zabezpieczeń.
* Upewnij się, że wiele implementacji hello takie same interfejsu są scalane w jeden wpis.

Te ustawienia konfiguracji zapobiec wystąpieniu błędów w czasie wykonywania.

#### <a name="topology-definitions"></a>Definicje topologii

W tym przykładzie użyto hello [strumień](https://storm.apache.org/releases/1.1.0/flux.html) framework. Ta struktura używa topologii hello toodefine yaml programu. Hello głównej korzyścią jest to, czy nie ma twardych kodowania hello topologii w kodzie języka Java. Ponieważ definicji hello jest yaml programu, można ją zmienić przed przesłaniem hello topologii, bez konieczności toorecompile wszystko.

__Writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__Reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Opisz topologii hello Centrum zdarzeń

W czasie wykonywania, hello `dev.properties` plik jest używany toopass hello Centrum zdarzeń konfiguracji toohello topologii. Witaj poniższy przykład jest hello domyślną zawartość pliku hello:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Skonfiguruj zmienne środowiskowe

Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalowania Java i hello JDK na deweloperskiej stacji roboczej. Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.

* **JAVA_HOME** -powinny wskazywać katalog toohello zainstalowanym hello środowiska uruchomieniowego (JRE). Na przykład w systemie Unix lub Linux dystrybucji, powinien on wartość podobną zbyt`/usr/lib/jvm/java-7-oracle`. W systemie Windows czy ma on wartość podobną zbyt`c:\Program Files (x86)\Java\jre1.7`
* **ŚCIEŻKA** -powinien zawierać hello następującej ścieżki:

  * **JAVA_HOME** (lub równoważne ścieżki hello)
  * **JAVA_HOME\bin** (lub równoważne ścieżki hello)
  * katalog Hello zainstalowanym Maven

## <a name="configure-event-hub"></a>Konfigurowanie Centrum zdarzeń

Centra zdarzeń to hello źródła danych w tym przykładzie. Użyj hello następujące kroki toocreate Centrum zdarzeń.

1. Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **nowy** > **usługi Service Bus** > **Centrum zdarzeń**  >  **Utwórz niestandardowy**.

2. Na powitania **dodać z nowym Centrum zdarzeń** ekranu, wprowadź **nazwy Centrum zdarzeń**. Wybierz hello **Region** toocreate hello koncentratora, a następnie utworzyć przestrzeń nazw lub wybierz istniejący. Na koniec kliknij hello **strzałka** toocontinue.

    ![1. strona kreatora](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Wybierz hello sam **lokalizacji** jako Storm opóźnienia tooreduce serwera HDInsight oraz koszty.

3. Na powitania **Konfigurowanie Centrum zdarzeń** ekranu, wprowadź hello **liczba partycji** i **przechowywania wiadomości** wartości. Na przykład użyj partycji liczbę 10 i przechowywania wiadomości 1. Uwaga hello liczba partycji, ponieważ potrzebne później tej wartości.

    ![strona kreatora 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Po hello Centrum zdarzeń zostało utworzone, wybierz hello przestrzeni nazw, wybierz **usługi Event Hubs**, a następnie wybierz hello Centrum zdarzeń, który został utworzony wcześniej.
5. Wybierz **Konfiguruj**, następnie utwórz dwa nowe zasady dostępu, używając hello następujących informacji:

    <table>
    <tr><th>Nazwa</th><th>Uprawnienia</th></tr>
    <tr><td>Składnik zapisywania</td><td>Send</td></tr>
    <tr><td>Czytelnik</td><td>Nasłuchiwanie</td></tr>
    </table>

    Po utworzeniu uprawnienia hello wybierz hello **zapisać** ikona u dołu hello hello strony. Te zasady dostępu współdzielonego są używane tooread i zapisu tooEvent koncentratora.

    ![zasady](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Po zapisaniu hello zasad, należy użyć hello **generatora klucza dostępu współużytkowanego** u dołu hello hello strony tooretrieve hello klucza hello **zapisywania** i **czytnika** zasad. Zapisz te klucze.

## <a name="download-and-build-hello-project"></a>Pobieranie i tworzenie hello projektu

1. Pobierz hello projektu z usługi GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Możesz pobrać pakiet hello jako archiwum zip, lub użyj [git](https://git-scm.com/) tooclone hello projektu lokalnie.

2. Modyfikowanie hello `dev.properties` pliku konfiguracji hello Centrum zdarzeń.

3. Użyj następującego projektu hello toobuild i pakietów hello:

        mvn package

    To polecenie pobiera wymaganych zależności, kompilacji, a następnie pakietów hello projektu. dane wyjściowe Hello są przechowywane w hello **/target** katalogu jako **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Test lokalnie

Ponieważ te topologie tylko odczytu i zapisu tooEvent koncentratory, można było je przetestować lokalnie, jeśli masz [środowisko projektowe Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Użyj hello następujące kroki toorun lokalnie w środowisku testowym hello:

1. Uruchom moduł zapisujący hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Uruchom czytnika hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Topologia hello wykonywania w trybie lokalnym (z systemem innym niż rozproszonych).
> * `-R /writer.yaml`: Załadować hello topologii definicji z hello `resources` spakowaniu hello jar. Hello topologii w przypadku plików w systemie plików lokalne powitania, określ tooit ścieżka hello jako ostatni parametr hello.
> * `--filter dev.properties`: Użyj zawartość hello `dev.properties` toofill wartości hello w definicjach topologii hello. Na przykład `${eventhub.read.policy.name}`.

Dane wyjściowe są rejestrowane toohello konsoli podczas uruchamiania lokalnego. Użyj __klawisze Ctrl + C__ toostop hello topologii.

## <a name="deploy-hello-topologies"></a>Wdrażanie topologii hello

1. Użyj SCP toocopy hello jar pakietu tooyour klastra usługi HDInsight. Zastąp nazwę użytkownika hello użytkownika SSH dla klastra. Zastąp NAZWAKLASTRA hello nazwy klastra usługi HDInsight:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Jeśli użyto hasła do konta SSH, to tooenter zostanie wyświetlony monit o hasło hello. Jeśli z kontem hello jest używany klucz SSH, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello klucza pliku. Na przykład: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    To polecenie powoduje skopiowanie hello pliku toohello katalogu macierzystego użytkownika SSH w klastrze hello.

2. Po zakończeniu hello plików podczas przekazywania, użyj klastra usługi HDInsight toohello tooconnect SSH. Zastąp **USERNAME** hello nazwa logowania użytkownika SSH. Zastąp **CLUSTERNAME** z nazwą klastra usługi HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Jeśli użyto hasła do konta SSH, to tooenter zostanie wyświetlony monit o hasło hello. Jeśli z kontem hello jest używany klucz SSH, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello klucza pliku. Witaj poniższy przykład załaduje hello klucza prywatnego z `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Witaj Użyj następującego polecenia toostart hello topologii:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Przesyła hello topologii toohello usługi Nimbus, który uruchamia go na powitania węzłów procesu roboczego w klastrze hello.

4. tooview hello rejestrowane dane, przejdź toohttps://CLUSTERNAME.azurehdinsight.net/stormui, gdzie __CLUSTERNAME__ jest nazwą hello klastra usługi HDInsight. Wybierz topologie hello i przejść do szczegółów toohello składników. Wybierz hello __portu__ wpis dla wystąpienia tooview składnika zarejestrowane informacje.

5. Użyj hello następujące topologie hello toostop polecenia:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Usuwanie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Następne kroki

* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)
