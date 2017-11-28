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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="ade71-103">Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="ade71-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="ade71-104">Dowiedz się, jak toouse Azure Event Hubs z systemu Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ade71-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="ade71-105">W tym przykładzie używane składników opartych na języku Java tooread i zapisu danych w usłudze Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ade71-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="ade71-106">Usługa Azure Event Hubs umożliwia tooprocess olbrzymich ilości danych z urządzeń, aplikacji i witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ade71-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="ade71-107">Witaj spout Centrum zdarzeń umożliwia łatwe toouse Apache Storm w usłudze HDInsight tooanalyze tych danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="ade71-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="ade71-108">Można również napisać tooEvent danych koncentratory z Storm przy użyciu powitalne centra zdarzeń dla elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="ade71-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ade71-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ade71-109">Prerequisites</span></span>

* <span data-ttu-id="ade71-110">Apache Storm w klastrze usługi HDInsight w wersji 3,6.</span><span class="sxs-lookup"><span data-stu-id="ade71-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="ade71-111">Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z systemu Storm w klastrze usługi HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ade71-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ade71-112">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ade71-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ade71-113">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ade71-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ade71-114">[Centrum zdarzeń Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="ade71-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="ade71-115">[Oracle Java Developer Kit (JDK) w wersji 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) lub równoważnego, takich jak [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="ade71-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="ade71-116">[Maven](https://maven.apache.org/download.cgi): Maven to system projektu kompilacji dla projektów języka Java.</span><span class="sxs-lookup"><span data-stu-id="ade71-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="ade71-117">Edytor tekstu lub zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="ade71-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ade71-118">Z edytora lub IDE może mieć określone funkcje do pracy z Maven, który nie jest opisany w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="ade71-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="ade71-119">Informacje dotyczące możliwości hello środowiska edytowania dokumentacji hello hello produktu, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="ade71-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="ade71-120">Klient SSH.</span><span class="sxs-lookup"><span data-stu-id="ade71-120">An SSH client.</span></span> <span data-ttu-id="ade71-121">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ade71-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="ade71-122">Witaj `ssh` i `scp` poleceń.</span><span class="sxs-lookup"><span data-stu-id="ade71-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="ade71-123">Są to klastra usługi HDInsight toohello pliki toocopy używane.</span><span class="sxs-lookup"><span data-stu-id="ade71-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="ade71-124">W systemie Windows możesz uzyskać je za pośrednictwem Bash w systemie Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ade71-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="ade71-125">Przykład Witaj opis</span><span class="sxs-lookup"><span data-stu-id="ade71-125">Understanding hello example</span></span>

<span data-ttu-id="ade71-126">Witaj [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) przykład zawiera dwie topologie:</span><span class="sxs-lookup"><span data-stu-id="ade71-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="ade71-127">Witaj `resources/writer.yaml` topologii zapisuje tooan losowe dane Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ade71-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="ade71-128">danych Hello jest generowany przez hello `DeviceSpout` składnika i Identyfikatora losowe urządzenia i wartość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ade71-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="ade71-129">Dlatego symuluje ona część sprzętu, który emituje identyfikator ciągu i wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="ade71-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="ade71-130">Te `resources/reader.yaml` topologii odczytuje dane z Centrum zdarzeń (danych hello napisane przez EventHubWriter,) analizuje dane JSON hello, a następnie rejestruje hello `deviceId` i `deviceValue` danych.</span><span class="sxs-lookup"><span data-stu-id="ade71-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="ade71-131">dane Hello są sformatowane jako dokument JSON przed jest zapisywane tooEvent koncentratora i odczytywana przez czytnik hello jest analizowany poza JSON i do spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="ade71-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="ade71-132">Hello JSON format jest następujący:</span><span class="sxs-lookup"><span data-stu-id="ade71-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="ade71-133">Konfiguracja projektu</span><span class="sxs-lookup"><span data-stu-id="ade71-133">Project configuration</span></span>

<span data-ttu-id="ade71-134">Witaj `POM.xml` plik zawiera informacje o konfiguracji dla tego projektu Maven.</span><span class="sxs-lookup"><span data-stu-id="ade71-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="ade71-135">Witaj interesujące jest:</span><span class="sxs-lookup"><span data-stu-id="ade71-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="ade71-136">Składniki Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ade71-136">Event Hub components</span></span>

<span data-ttu-id="ade71-137">składnik Hello odczytuje i zapisuje centra zdarzeń tooAzure znajduje się w hello [repozytorium HDInsight](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="ade71-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="ade71-138">Witaj w następujących sekcjach hello `POM.xml` składniki hello ładowania pliku z tego repozytorium</span><span class="sxs-lookup"><span data-stu-id="ade71-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="ade71-139">Witaj EventHubs Storm Spout zależności</span><span class="sxs-lookup"><span data-stu-id="ade71-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="ade71-140">Plik xml definiuje zależność hello eventhubs pakiet, który zawiera spout do odczytywania z usługi Event Hubs i bolt do pisania tooit.</span><span class="sxs-lookup"><span data-stu-id="ade71-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="ade71-141">Plik xml konfiguruje hello wynik toogenerate projektu dla języka Java 8, który jest używany przez usługi HDInsight 3.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ade71-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="ade71-142">Witaj maven cień wtyczki</span><span class="sxs-lookup"><span data-stu-id="ade71-142">hello maven-shade-plugin</span></span>

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

<span data-ttu-id="ade71-143">Plik xml konfiguruje hello rozwiązania toopackage hello w danych wyjściowych do jar pełny.</span><span class="sxs-lookup"><span data-stu-id="ade71-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="ade71-144">Witaj jar zawiera hello kodu projektu i wymaganych zależności.</span><span class="sxs-lookup"><span data-stu-id="ade71-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="ade71-145">Służy również do:</span><span class="sxs-lookup"><span data-stu-id="ade71-145">It is also used to:</span></span>

* <span data-ttu-id="ade71-146">Zmień nazwy plików licencji hello zależności.</span><span class="sxs-lookup"><span data-stu-id="ade71-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="ade71-147">Wyklucz podpisów/zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ade71-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="ade71-148">Upewnij się, że wiele implementacji hello takie same interfejsu są scalane w jeden wpis.</span><span class="sxs-lookup"><span data-stu-id="ade71-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="ade71-149">Te ustawienia konfiguracji zapobiec wystąpieniu błędów w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ade71-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="ade71-150">Definicje topologii</span><span class="sxs-lookup"><span data-stu-id="ade71-150">Topology definitions</span></span>

<span data-ttu-id="ade71-151">W tym przykładzie użyto hello [strumień](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="ade71-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="ade71-152">Ta struktura używa topologii hello toodefine yaml programu.</span><span class="sxs-lookup"><span data-stu-id="ade71-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="ade71-153">Hello głównej korzyścią jest to, czy nie ma twardych kodowania hello topologii w kodzie języka Java.</span><span class="sxs-lookup"><span data-stu-id="ade71-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="ade71-154">Ponieważ definicji hello jest yaml programu, można ją zmienić przed przesłaniem hello topologii, bez konieczności toorecompile wszystko.</span><span class="sxs-lookup"><span data-stu-id="ade71-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="ade71-155">__Writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="ade71-155">__writer.yaml__:</span></span>

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

<span data-ttu-id="ade71-156">__Reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="ade71-156">__reader.yaml__:</span></span>

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

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="ade71-157">Opisz topologii hello Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ade71-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="ade71-158">W czasie wykonywania, hello `dev.properties` plik jest używany toopass hello Centrum zdarzeń konfiguracji toohello topologii.</span><span class="sxs-lookup"><span data-stu-id="ade71-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="ade71-159">Witaj poniższy przykład jest hello domyślną zawartość pliku hello:</span><span class="sxs-lookup"><span data-stu-id="ade71-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="ade71-160">Skonfiguruj zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="ade71-160">Configure environment variables</span></span>

<span data-ttu-id="ade71-161">Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalowania Java i hello JDK na deweloperskiej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="ade71-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="ade71-162">Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="ade71-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="ade71-163">**JAVA_HOME** -powinny wskazywać katalog toohello zainstalowanym hello środowiska uruchomieniowego (JRE).</span><span class="sxs-lookup"><span data-stu-id="ade71-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="ade71-164">Na przykład w systemie Unix lub Linux dystrybucji, powinien on wartość podobną zbyt`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="ade71-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="ade71-165">W systemie Windows czy ma on wartość podobną zbyt`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="ade71-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="ade71-166">**ŚCIEŻKA** -powinien zawierać hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="ade71-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="ade71-167">**JAVA_HOME** (lub równoważne ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="ade71-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="ade71-168">**JAVA_HOME\bin** (lub równoważne ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="ade71-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="ade71-169">katalog Hello zainstalowanym Maven</span><span class="sxs-lookup"><span data-stu-id="ade71-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="ade71-170">Konfigurowanie Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ade71-170">Configure Event Hub</span></span>

<span data-ttu-id="ade71-171">Centra zdarzeń to hello źródła danych w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ade71-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="ade71-172">Użyj hello następujące kroki toocreate Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ade71-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="ade71-173">Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **nowy** > **usługi Service Bus** > **Centrum zdarzeń**  >  **Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="ade71-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="ade71-174">Na powitania **dodać z nowym Centrum zdarzeń** ekranu, wprowadź **nazwy Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="ade71-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="ade71-175">Wybierz hello **Region** toocreate hello koncentratora, a następnie utworzyć przestrzeń nazw lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="ade71-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="ade71-176">Na koniec kliknij hello **strzałka** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ade71-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![1. strona kreatora](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="ade71-178">Wybierz hello sam **lokalizacji** jako Storm opóźnienia tooreduce serwera HDInsight oraz koszty.</span><span class="sxs-lookup"><span data-stu-id="ade71-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="ade71-179">Na powitania **Konfigurowanie Centrum zdarzeń** ekranu, wprowadź hello **liczba partycji** i **przechowywania wiadomości** wartości.</span><span class="sxs-lookup"><span data-stu-id="ade71-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="ade71-180">Na przykład użyj partycji liczbę 10 i przechowywania wiadomości 1.</span><span class="sxs-lookup"><span data-stu-id="ade71-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="ade71-181">Uwaga hello liczba partycji, ponieważ potrzebne później tej wartości.</span><span class="sxs-lookup"><span data-stu-id="ade71-181">Note hello partition count because you need this value later.</span></span>

    ![strona kreatora 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="ade71-183">Po hello Centrum zdarzeń zostało utworzone, wybierz hello przestrzeni nazw, wybierz **usługi Event Hubs**, a następnie wybierz hello Centrum zdarzeń, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ade71-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="ade71-184">Wybierz **Konfiguruj**, następnie utwórz dwa nowe zasady dostępu, używając hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ade71-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="ade71-185">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ade71-185">Name</span></span></th><th><span data-ttu-id="ade71-186">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="ade71-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="ade71-187">Składnik zapisywania</span><span class="sxs-lookup"><span data-stu-id="ade71-187">Writer</span></span></td><td><span data-ttu-id="ade71-188">Send</span><span class="sxs-lookup"><span data-stu-id="ade71-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="ade71-189">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="ade71-189">Reader</span></span></td><td><span data-ttu-id="ade71-190">Nasłuchiwanie</span><span class="sxs-lookup"><span data-stu-id="ade71-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="ade71-191">Po utworzeniu uprawnienia hello wybierz hello **zapisać** ikona u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ade71-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="ade71-192">Te zasady dostępu współdzielonego są używane tooread i zapisu tooEvent koncentratora.</span><span class="sxs-lookup"><span data-stu-id="ade71-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![zasady](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="ade71-194">Po zapisaniu hello zasad, należy użyć hello **generatora klucza dostępu współużytkowanego** u dołu hello hello strony tooretrieve hello klucza hello **zapisywania** i **czytnika** zasad.</span><span class="sxs-lookup"><span data-stu-id="ade71-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="ade71-195">Zapisz te klucze.</span><span class="sxs-lookup"><span data-stu-id="ade71-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="ade71-196">Pobieranie i tworzenie hello projektu</span><span class="sxs-lookup"><span data-stu-id="ade71-196">Download and build hello project</span></span>

1. <span data-ttu-id="ade71-197">Pobierz hello projektu z usługi GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="ade71-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="ade71-198">Możesz pobrać pakiet hello jako archiwum zip, lub użyj [git](https://git-scm.com/) tooclone hello projektu lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ade71-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="ade71-199">Modyfikowanie hello `dev.properties` pliku konfiguracji hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ade71-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="ade71-200">Użyj następującego projektu hello toobuild i pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="ade71-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="ade71-201">To polecenie pobiera wymaganych zależności, kompilacji, a następnie pakietów hello projektu.</span><span class="sxs-lookup"><span data-stu-id="ade71-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="ade71-202">dane wyjściowe Hello są przechowywane w hello **/target** katalogu jako **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="ade71-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="ade71-203">Test lokalnie</span><span class="sxs-lookup"><span data-stu-id="ade71-203">Test locally</span></span>

<span data-ttu-id="ade71-204">Ponieważ te topologie tylko odczytu i zapisu tooEvent koncentratory, można było je przetestować lokalnie, jeśli masz [środowisko projektowe Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="ade71-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="ade71-205">Użyj hello następujące kroki toorun lokalnie w środowisku testowym hello:</span><span class="sxs-lookup"><span data-stu-id="ade71-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="ade71-206">Uruchom moduł zapisujący hello:</span><span class="sxs-lookup"><span data-stu-id="ade71-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="ade71-207">Uruchom czytnika hello:</span><span class="sxs-lookup"><span data-stu-id="ade71-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="ade71-208">`--local`: Topologia hello wykonywania w trybie lokalnym (z systemem innym niż rozproszonych).</span><span class="sxs-lookup"><span data-stu-id="ade71-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="ade71-209">`-R /writer.yaml`: Załadować hello topologii definicji z hello `resources` spakowaniu hello jar.</span><span class="sxs-lookup"><span data-stu-id="ade71-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="ade71-210">Hello topologii w przypadku plików w systemie plików lokalne powitania, określ tooit ścieżka hello jako ostatni parametr hello.</span><span class="sxs-lookup"><span data-stu-id="ade71-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="ade71-211">`--filter dev.properties`: Użyj zawartość hello `dev.properties` toofill wartości hello w definicjach topologii hello.</span><span class="sxs-lookup"><span data-stu-id="ade71-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="ade71-212">Na przykład `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="ade71-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="ade71-213">Dane wyjściowe są rejestrowane toohello konsoli podczas uruchamiania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ade71-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="ade71-214">Użyj __klawisze Ctrl + C__ toostop hello topologii.</span><span class="sxs-lookup"><span data-stu-id="ade71-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="ade71-215">Wdrażanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="ade71-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="ade71-216">Użyj SCP toocopy hello jar pakietu tooyour klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ade71-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="ade71-217">Zastąp nazwę użytkownika hello użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="ade71-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="ade71-218">Zastąp NAZWAKLASTRA hello nazwy klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ade71-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="ade71-219">Jeśli użyto hasła do konta SSH, to tooenter zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="ade71-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="ade71-220">Jeśli z kontem hello jest używany klucz SSH, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello klucza pliku.</span><span class="sxs-lookup"><span data-stu-id="ade71-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="ade71-221">Na przykład: `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="ade71-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="ade71-222">To polecenie powoduje skopiowanie hello pliku toohello katalogu macierzystego użytkownika SSH w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="ade71-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="ade71-223">Po zakończeniu hello plików podczas przekazywania, użyj klastra usługi HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="ade71-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="ade71-224">Zastąp **USERNAME** hello nazwa logowania użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="ade71-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="ade71-225">Zastąp **CLUSTERNAME** z nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ade71-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="ade71-226">Jeśli użyto hasła do konta SSH, to tooenter zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="ade71-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="ade71-227">Jeśli z kontem hello jest używany klucz SSH, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello klucza pliku.</span><span class="sxs-lookup"><span data-stu-id="ade71-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="ade71-228">Witaj poniższy przykład załaduje hello klucza prywatnego z `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="ade71-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="ade71-229">Witaj Użyj następującego polecenia toostart hello topologii:</span><span class="sxs-lookup"><span data-stu-id="ade71-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="ade71-230">`--remote`: Przesyła hello topologii toohello usługi Nimbus, który uruchamia go na powitania węzłów procesu roboczego w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="ade71-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="ade71-231">tooview hello rejestrowane dane, przejdź toohttps://CLUSTERNAME.azurehdinsight.net/stormui, gdzie __CLUSTERNAME__ jest nazwą hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ade71-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="ade71-232">Wybierz topologie hello i przejść do szczegółów toohello składników.</span><span class="sxs-lookup"><span data-stu-id="ade71-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="ade71-233">Wybierz hello __portu__ wpis dla wystąpienia tooview składnika zarejestrowane informacje.</span><span class="sxs-lookup"><span data-stu-id="ade71-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="ade71-234">Użyj hello następujące topologie hello toostop polecenia:</span><span class="sxs-lookup"><span data-stu-id="ade71-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="ade71-235">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="ade71-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="ade71-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ade71-236">Next steps</span></span>

* [<span data-ttu-id="ade71-237">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ade71-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
