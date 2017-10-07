---
title: "aaaApache Storm przykładową topologię Java - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate topologii Apache Storm w języku Java przez utworzenie przykładowego słowa liczba topologii."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Apache storm, przykład storm apache storm w języku java, przykład topologii storm"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Tworzenie topologii Apache Storm w języku Java

Dowiedz się, jak toocreate topologii opartych na języku Java Apache STORM. Możesz utworzyć topologii Storm, która implementuje aplikacji liczba programu word. Możesz użyć Maven toobuild i pakietów hello projektu. Następnie dowiesz się, jak przy użyciu topologii hello toodefine hello framework strumienia.

> [!NOTE]
> framework strumień Hello jest dostępna w Storm 0.10.0 lub nowszej. STORM 0.10.0 jest dostępna w HDInsight 3.3 i 3.4.

Po wykonaniu czynności hello w tym dokumencie można wdrożyć hello tooApache topologii Storm w usłudze HDInsight.

> [!NOTE]
> Ukończoną wersję przykłady topologii Storm hello utworzone w tym dokumencie znajduje się w temacie [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Wymagania wstępne

* [Java Developer Kit (JDK) w wersji 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven to system projektu kompilacji dla projektów języka Java.

* Edytor tekstu lub IDE.

## <a name="configure-environment-variables"></a>Skonfiguruj zmienne środowiskowe

Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalacji języka Java i hello JDK. Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.

* **JAVA_HOME** -powinny wskazywać katalog toohello zainstalowanym hello środowiska uruchomieniowego (JRE). Na przykład w systemie Unix lub Linux dystrybucji, powinien on wartość podobną zbyt`/usr/lib/jvm/java-7-oracle`. W systemie Windows czy ma on wartość podobną zbyt`c:\Program Files (x86)\Java\jre1.7`

* **ŚCIEŻKA** -powinien zawierać hello następującej ścieżki:

  * **JAVA_HOME** (lub równoważne ścieżki hello)

  * **JAVA_HOME\bin** (lub równoważne ścieżki hello)

  * katalog Hello zainstalowanym Maven

## <a name="create-a-maven-project"></a>Utwórz projekt Maven

Z wiersza polecenia hello, użyj hello następujące polecenie toocreate projekt Maven o nazwie **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> Jeśli używasz programu PowerShell, należy otoczyć`-D` parametry z cudzysłowami podwójnymi.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

To polecenie tworzy katalog o nazwie `WordCount` w bieżącej lokalizacji hello, który zawiera podstawowe projekt Maven. Witaj `WordCount` katalog zawiera hello następujące elementy:

* `pom.xml`: Zawiera ustawienia hello projekt Maven.
* `src\main\java\com\microsoft\example`: Zawiera kod aplikacji.
* `src\test\java\com\microsoft\example`: Zawiera testy dla aplikacji. 

### <a name="remove-hello-generated-example-code"></a>Usuń wygenerowane hello przykładowy kod

Usuń hello wygenerowanych testów i pliki aplikacji hello:

* **src\test\java\com\microsoft\example\AppTest.Java**
* **src\main\java\com\microsoft\example\App.Java**

## <a name="add-maven-repositories"></a>Dodaj repozytoria Maven

HDInsight jest oparta na powitania Hortonworks Data Platform (HDP), dlatego firma Microsoft zaleca używanie hello Hortonworks repozytorium toodownload zależności dla projektów Apache Storm. W hello __pom.xml__ plików, Dodaj następujące XML po hello hello `<url>http://maven.apache.org</url>` wiersza:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Dodawanie właściwości

Maven umożliwia toodefine wartości Poziom projektu o nazwie właściwości. W hello __pom.xml__, Dodaj następujące tekstu po hello hello `</repositories>` wiersza:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

Tę wartość można teraz używać w innych częściach hello `pom.xml`. Na przykład podczas określania wersji hello składników systemu Storm, można użyć `${storm.version}` zamiast twardych kodowania wartość.

## <a name="add-dependencies"></a>Dodaj zależności

Dodawanie zależności dla składników systemu Storm. Otwórz hello `pom.xml` plik i dodać hello następującego kodu w hello `<dependencies>` sekcji:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

W czasie kompilacji Maven korzysta z tej informacji toolook `storm-core` hello Maven repozytorium. Najpierw wyszukiwana w repozytorium hello na komputerze lokalnym. Jeśli nie są pliki hello, Maven pobiera ich z publicznego repozytorium Maven hello i przechowuje je w repozytorium lokalne powitania.

> [!NOTE]
> Powiadomienie hello `<scope>provided</scope>` wiersza w tej sekcji. To ustawienie określa, że Maven tooexclude **storm core** z pliki JAR, które są tworzone, ponieważ są dostarczane przez hello system.

## <a name="build-configuration"></a>Konfiguracja kompilacji

Maven dodatków plug-in pozwalają toocustomize hello kompilacji etapach hello projektu. Na przykład sposobu kompilowania projektu hello lub jak toopackage go do pliku JAR. Otwórz hello `pom.xml` plik i dodać hello następującego kodu bezpośrednio nad hello `</project>` wiersza.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Ta sekcja jest używane tooadd dodatków plug-in, zasobów i innych opcji konfiguracji kompilacji. Pełną dokumentację hello **pom.xml** plików, zobacz [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Dodawanie wtyczki

Dla topologii Apache Storm w języku Java, hello [wtyczki Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) jest przydatne, ponieważ umożliwia tooeasily uruchomić topologii hello lokalnie w środowisku projektowania. Dodaj następujące toohello hello `<plugins>` sekcji hello `pom.xml` pliku tooinclude hello Exec Maven wtyczki:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Inny przydatne dodatek jest hello [Apache Maven kompilatora wtyczki](http://maven.apache.org/plugins/maven-compiler-plugin/), która jest używana toochange opcje kompilacji. zmiany Hello hello wersję Java, używającego Maven hello źródłowa i docelowa dla aplikacji.

* Dla usługi HDInsight __3.4 lub starszym__, ustaw źródło hello i docelowymi too__1.7__ wersji języka Java.

* Dla usługi HDInsight __3.5__, ustaw źródło hello i docelowymi too__1.8__ wersji języka Java.

Dodaj następującego tekstu w hello hello `<plugins>` sekcji hello `pom.xml` pliku tooinclude hello Apache Maven kompilatora wtyczki. W tym przykładzie określa 1.8, tak aby hello docelowej usługi HDInsight w wersji 3.5.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Konfigurowanie zasobów

sekcja zasobów Hello umożliwia tooinclude-code zasobów takich jak pliki konfiguracji wymagane przez składniki w topologii hello. Na przykład dodać hello następującego tekstu w hello `<resources>` sekcji hello "plik pom.xml.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

W tym przykładzie dodaje hello katalogu zasobów w katalogu głównym hello hello projektu (`${basedir}`) jako lokalizację, która zawiera zasoby i obejmuje hello plik o nazwie `log4j2.xml`. Ten plik jest używany tooconfigure informacjach jest rejestrowane przez hello topologii.

## <a name="create-hello-topology"></a>Tworzenie topologii hello

Topologia opartych na języku Java Apache Storm składa się z trzech składników, które należy utworzyć (lub odwołania) jako zależność.

* **Spouts**: odczytuje dane z zewnętrznego źródła i emituje strumieni danych w topologii hello.

* **Bolts**: przetwarza strumieni emitowane przez elementach spout lub innych elementów bolt i emituje jeden lub więcej strumieni.

* **Topologia**: definiuje sposób hello spouts i elementów bolt ułożone i zapewnia punkt wejścia hello hello topologii.

### <a name="create-hello-spout"></a>Utwórz elementy spout hello

Witaj tooreduce wymagania dotyczące konfigurowania zewnętrznych źródeł danych, następujące elementy spout po prostu emituje losowe zdań. Jest zmodyfikowanej wersji spout, udostępniana z hello [przykłady z projektu Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Na przykład spout, która odczytuje z zewnętrznego źródła danych Zobacz jedną z hello następujące przykłady:
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): spout przykład, która odczytuje z serwisem Twitter
> * [STORM Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): spout, która odczytuje z Kafka

Dla hello spout, Utwórz plik o nazwie `RandomSentenceSpout.java` w hello `src\main\java\com\microsoft\example` hello katalogu i użyj następującego kodu języka Java jako zawartość hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Mimo że ta topologia używa tylko jeden spout, inne mogą zawierać kilka, które do topologii hello strumieniowe źródło danych z różnych źródeł.

### <a name="create-hello-bolts"></a>Tworzenie elementów bolt hello

Elementów bolt obsługi hello przetwarzania danych. Ta topologia używa dwóch elementów bolt:

* **SplitSentence**: dzieli zdań hello emitowane przez **RandomSentenceSpout** do poszczególnych wyrazów.

* **WordCount**: zlicza, ile razy podczas każdego wyrazu.

> [!NOTE]
> Można to zrobić niczego, na przykład obliczeń, trwałości lub mówić składniki tooexternal elementów bolt.

Utwórz dwa nowe pliki `SplitSentence.java` i `WordCount.java` w hello `src\main\java\com\microsoft\example` katalogu. Użyj hello następującego tekstu jako zawartość hello hello plików:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Zdefiniuj topologię hello

Topologia Hello wiąże elementach spout hello i bolts ze sobą do wykresu, który definiuje sposób dane przepływają między składnikami hello. Umożliwia także wskazówki równoległości, Storm używane podczas tworzenia wystąpienia hello składników w klastrze hello przez.

Witaj poniższy obraz jest diagram podstawowy wykresu hello składników dla tej topologii.

![Diagram przedstawiający hello spouts i bolts rozmieszczenie](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement hello topologii, Utwórz plik o nazwie `WordCountTopology.java` w hello `src\main\java\com\microsoft\example` katalogu. Użyj następującego kodu języka Java jako hello zawartość pliku hello hello:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Konfigurowanie rejestrowania

STORM używa Apache Log4j toolog informacji. Jeśli rejestrowanie nie zostanie skonfigurowane, topologii hello emituje informacje diagnostyczne. toocontrol, co jest rejestrowane, Utwórz plik o nazwie `log4j2.xml` w hello `resources` katalogu. Użyj powitania po jako zawartość hello hello pliku XML.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Plik XML Konfiguruje nowy rejestratora dla hello `com.microsoft.example` klasy, która obejmuje składniki hello w tym przykładzie topologii. poziom Hello jest ustawiany tootrace dla tego rejestratora, który przechwytuje informacje rejestrowania emitowane przez składniki w tej topologii.

Witaj `<Root level="error">` sekcji konfiguruje hello główny poziom rejestrowania (wszystko, co nie `com.microsoft.example`) informacje o błędzie tooonly dziennika.

Aby uzyskać więcej informacji na temat konfigurowania rejestrowanie dla narzędzia Log4j, zobacz [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> STORM w wersji 0.10.0 i wyższe użycie narzędzia Log4j 2.x. Starsze wersje storm używane Log4j 1.x, którego użyć innego formatu dla konfiguracji dziennika. Uzyskać informacji o konfiguracji starsze hello, zobacz [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Test hello lokalnie topologii

Po zapisaniu plików hello, należy użyć hello następujące polecenia tootest hello topologii lokalnie.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Podczas wykonywania, topologii hello Wyświetla informacje o uruchamianiu. Witaj następujący tekst jest przykład danych wyjściowych liczba word hello:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Ten przykładowy dziennik wskazuje wyrazie hello "i" zostały wyemitowane 113 razy. Witaj liczba nadal toogo się tak długo, jak działa topologia hello ponieważ hello spout stale emituje hello tego samego zdań.

Brak interwału 5 sekund między emisji słów i liczby. Witaj **WordCount** składnik został skonfigurowany tooonly Emituj informacje, gdy dociera krotką znacznikową. Żąda tego znaczników krotek tylko są przeprowadzane co pięć sekund.

## <a name="convert-hello-topology-tooflux"></a>Konwertuj hello topologii tooFlux

Strumień jest nowa struktura dostępne z systemu Storm 0.10.0 lub nowszy, co pozwala tooseparate konfiguracji z wdrożenia. Składniki nadal są zdefiniowane w języku Java, ale topologii hello jest definiowana za pomocą pliku yaml programu. Pakiet definicji topologii domyślnej z projektu lub podczas przesyłania topologii hello przy użyciu pliku autonomicznym. Podczas przesyłania tooStorm topologii hello, można użyć zmiennych środowiskowych lub wartości toopopulate pliki konfiguracji w hello definicji topologii yaml programu.

Plik yaml programu Hello definiuje toouse składniki hello hello topologii i hello przepływ danych między nimi. Plik yaml programu można dodać jako część pliku jar hello lub skorzystać z zewnętrznego pliku yaml programu.

Aby uzyskać więcej informacji na strumienia, zobacz [framework strumienia (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Termin tooa [usterek (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) z systemu Storm 1.0.1, może być konieczne tooinstall [środowisko projektowe Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun strumień lokalnie topologii.

1. Przenieś hello `WordCountTopology.java` pliku poza hello projektu. Wcześniej ten plik zdefiniowany hello topologii, ale nie jest wymagane ze strumienia.

2. W hello `resources` katalogu, Utwórz plik o nazwie `topology.yaml`. Użyj hello następującego tekstu jako hello zawartość tego pliku.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Wprowadź następujące zmiany toohello hello `pom.xml` pliku.
   
   * Dodaj następujące nowe zależności w hello hello `<dependencies>` sekcji:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Dodaj następujące wtyczki toohello hello `<plugins>` sekcji. Tej wtyczki obsługuje hello tworzenia pakietu (plik jar) dla projektu hello i zastosowanie niektórych przekształcenia tooFlux określonych podczas tworzenia pakietu hello.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * W hello **wtyczki exec-maven** `<configuration>` sekcji, zmień wartość hello `<mainClass>` zbyt`org.apache.storm.flux.Flux`. To ustawienie umożliwia uruchomionych topologii hello lokalnie w rozwoju toohandle strumienia.

   * W hello `<resources>` Dodaj powitania po toohello `<includes>`. Plik XML zawiera hello yaml programu pliku, który definiuje topologii hello jako część hello projektu.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Topologia strumień hello testu lokalnie

1. Użyj następującego toocompile hello i wykonaj hello strumień topologii za pomocą programu Maven:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Jeśli używasz programu PowerShell, hello Użyj następującego polecenia:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Jeśli topologii korzysta z usługi bits Storm 1.0.1, to polecenie nie powiedzie się. Ten błąd jest spowodowany przez [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). Zamiast tego [zainstalować Storm w środowisku projektowania](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) i hello Użyj następujących informacji.

    Jeśli masz [zainstalowane Storm w środowisku projektowania](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), można użyć hello zamiast tego następujące polecenia:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Witaj `--local` parametr działa topologia hello w trybie lokalnym na środowiska deweloperskiego. Witaj `-R /topology.yaml` parametr używa hello `topology.yaml` pliku zasobu z hello jar pliku toodefine hello topologii.

    Podczas wykonywania, topologii hello Wyświetla informacje o uruchamianiu. przykład danych wyjściowych hello znajduje się w Hello następującego tekstu:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Brak 10-sekundowe opóźnienie między partie zarejestrowane informacje.

2. Utwórz kopię hello `topology.yaml` plik z projektu hello. Nazwa hello nowy plik `newtopology.yaml`. W hello `newtopology.yaml` pliku, znajdź następujący hello sekcji i zmienić wartość hello `10` zbyt`5`. Zlicza ta modyfikacja zmiany hello odstęp między emitowania partii programu word z too5 10 sekund.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    Lub, jeśli masz Storm środowiska programowania:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Zmień hello `/path/to/newtopology.yaml` utworzony w poprzednim kroku hello toohello ścieżki toohello newtopology.yaml pliku. To polecenie używa hello newtopology.yaml jako hello topologii definicji. Ponieważ firma Microsoft nie obejmują hello `compile` parametru Maven używa wersji hello projektu hello utworzony w poprzednich krokach.

    Raz hello rozpoczyna topologii, można zauważyć, że hello czas między emitowany partie została zmieniona wartość hello tooreflect newtopology.yaml. Aby było widać, konfigurację można zmienić za pomocą pliku yaml programu bez konieczności toorecompile hello topologii.

Aby uzyskać więcej informacji na temat tych i innych funkcji hello strumień framework, zobacz [strumienia (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

Trident to Abstrakcja wysokiego poziomu zapewnianej przez Storm. Obsługuje ona stanowe przetwarzania. główną zaletą Trident Hello jest, że go gwarantuje, że każdy komunikat, który przechodzi topologii hello jest przetwarzany tylko raz. Bez użycia języka Trident, topologii można tylko gwarantuje, że komunikaty są przetwarzane co najmniej raz. Istnieją także inne różnice, takich jak wbudowanych składników, które mogą być używane zamiast tworzenia elementów bolt. W rzeczywistości elementów bolt są zastępowane przez składniki mniej ogólny, takie jak filtry, rzutowania i funkcje.

Trident aplikacje mogą być tworzone przy użyciu projekty Maven. Użyj hello tego samego basic kroki przedstawione w tym artykule — tylko kod hello różni się. Trident również nie (obecnie) można używać z hello framework strumienia.

Aby uzyskać więcej informacji na temat języka Trident, zobacz hello [omówienie API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).

Na przykład aplikację języka Trident, zobacz [trendów tematy z systemu Apache Storm w usłudze HDInsight w usłudze Twitter](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Następne kroki

Wiesz już, jak toocreate topologii Storm za pomocą języka Java. Teraz Dowiedz się, jak:

* [Wdrażanie i zarządzanie nimi topologii Apache Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology.md)

* [Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Można znaleźć więcej przykład topologii Storm po przejściu na stronę [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).

