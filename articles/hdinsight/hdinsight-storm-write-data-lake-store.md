---
title: aaaApache Storm zapisu tooStorage/Data Lake Store - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Apache Storm toowrite toohello zgodnego systemem plików HDFS magazynu dla usługi HDInsight. Azure magazynu lub usługi Azure Data Lake Store magazynowanie hello HDFS comptabile HDInsight. W tym dokumencie i skojarzone przykład Witaj, pokazują, jak hello HdfsBolt składnika mogą być używane toowrite toohello domyślny magazyn Storm w klastrze usługi HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Zapis tooHDFS z systemu Apache Storm w usłudze HDInsight

Dowiedz się, jak toouse Storm toowrite danych toohello zgodnego systemem plików HDFS magazynu używane przez Apache Storm w usłudze HDInsight. HDInsight można użyć zarówno usługi Azure Storage i Azure Data Lake przechowywane jako magazyn comptabile systemu plików HDFS. STORM udostępnia [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) składnik, który zapisuje tooHDFS danych. Ten dokument zawiera informacje o pisaniu z hello HdfsBolt tooeither typu magazynu. 

> [!IMPORTANT]
> przykład Witaj topologii używane w tym dokumencie opiera się na składnikach, które są dołączone do systemu Storm w usłudze HDInsight. Może wymagać modyfikacji toowork z usługi Azure Data Lake Store w przypadku użycia z innych klastrów platformy Apache Storm.

## <a name="get-hello-code"></a>Pobierz kod hello

Projekt Hello zawierający Ta topologia jest dostępny do pobrania z [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile tego projektu należy hello następującej konfiguracji dla swojego środowiska programowania:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej. HDInsight w wersji 3.5 lub nowszej wymagają Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalowania Java i hello JDK na deweloperskiej stacji roboczej. Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.

* `JAVA_HOME`— powinna wskazywać katalog toohello hello JDK zainstalowanym.
* `PATH`— powinna zawierać hello następującej ścieżki:
  
    * `JAVA_HOME`(lub równoważne ścieżki hello).
    * `JAVA_HOME\bin`(lub równoważne ścieżki hello).
    * Hello katalog, w którym zainstalowano Maven.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Jak toouse hello HdfsBolt z usługą HDInsight

> [!IMPORTANT]
> Przed użyciem hello HdfsBolt z systemu Storm w usłudze HDInsight, musisz najpierw użyć pliki jar toocopy wymagana akcja skryptu do hello `extpath` systemu STORM. Aby uzyskać więcej informacji, zobacz hello [Konfigurowanie klastra hello](#configure) sekcji.

Witaj HdfsBolt wykorzystuje schemat pliku hello jak zapewnić toounderstand toowrite tooHDFS. Z usługą HDInsight użyj jednej z hello następujące programy:

* `wasb://`: Używany przy użyciu konta usługi Azure Storage.
* `adl://`: Używane z usługi Azure Data Lake Store.

Witaj poniższej tabeli przedstawiono przykłady użycia hello pliku schematu dla różnych scenariuszy:

| Schemat | Uwagi |
| ----- | ----- |
| `wasb:///` | Witaj domyślne konto magazynu jest kontenera obiektów blob na koncie magazynu Azure |
| `adl:///` | Witaj domyślne konto magazynu jest katalogiem w usłudze Azure Data Lake Store. Podczas tworzenia klastra należy określić katalog hello w usługi Data Lake Store jest głównym hello hello klastra systemu plików HDFS. Na przykład Witaj `/clusters/myclustername/` katalogu. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Konto magazynu platformy Azure (dodatkowe) innych niż domyślne skojarzone z klastrem hello. |
| `adl://STORENAME/` | katalog główny Hello hello używane przez klaster hello usługi Data Lake Store. Ten program umożliwia tooaccess danych, który znajduje się poza katalogiem hello, zawierający system plików klastra hello. |

Aby uzyskać więcej informacji, zobacz hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) odwołania w serwisie Apache.org.

### <a name="example-configuration"></a>Przykładowa konfiguracja

Witaj następujące yaml programu znajduje się fragment hello `resources/writetohdfs.yaml` dołączony przykład Witaj. Ten plik definiuje topologii Storm hello przy użyciu hello [strumień](https://storm.apache.org/releases/1.1.0/flux.html) framework Apache STORM.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Ta yaml programu definiuje hello następujące elementy:

* `syncPolicy`: Określa, kiedy pliki są zsynchronizowane opróżnionych toohello systemu plików. W tym przykładzie każdy krotek 1000.
* `fileNameFormat`: Definiuje hello ścieżkę i nazwę wzorca toouse podczas zapisywania plików. W tym przykładzie zostanie podana ścieżka hello w środowisku uruchomieniowym przy użyciu filtru i rozszerzenie pliku hello jest `.txt`.
* `recordFormat`: Definiuje hello wewnętrzny format plików hello zapisywane. W tym przykładzie pola są rozdzielone hello `|` znaków.
* `rotationPolicy`: Określa, kiedy toorotate plików. W tym przykładzie jest wykonywane bez obrotu.
* `hdfs-bolt`: Używa hello poprzednie składniki jako parametry konfiguracji hello `HdfsBolt` klasy.

Aby uzyskać więcej informacji na powitania strumień framework, zobacz [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Konfigurowanie klastra hello

Domyślnie Storm w usłudze HDInsight nie zawiera składników hello HdfsBolt używa toocommunicate z magazynu Azure lub usługi Data Lake Store w Storm w ścieżce. Użyj następujących hello skryptu akcji tooadd toohello te składniki `extlib` katalogu systemu STORM w klastrze:

| Identyfikator URI skryptu | Węzły tooapply go do | Parametry || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, przełożonego | None |

Uzyskać informacji na temat używania tego skryptu z klastrem, zobacz hello [HDInsight dostosować klastry za pomocą akcji skryptu](./hdinsight-hadoop-customize-cluster-linux.md) dokumentu.

## <a name="build-and-package-hello-topology"></a>Topologia hello kompilacji i pakietu

1. Pobierz hello przykładowy projekt z [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour Środowisko deweloperskie.

2. W wierszu polecenia terminal lub sesję powłoki, zmień katalogi toohello głównym hello pobrane projektu. toobuild i pakietu hello topologii, należy użyć następującego polecenia hello:
   
        mvn compile package
   
    Po zakończeniu kompilacji hello i opakowanie jest nowy katalog o nazwie `target`, który zawiera plik o nazwie `StormToHdfs-1.0-SNAPSHOT.jar`. Ten plik zawiera topologii hello skompilowany.

## <a name="deploy-and-run-hello-topology"></a>Wdrażanie i uruchamianie hello topologii

1. Użyj powitania po klastra usługi HDInsight toohello polecenia toocopy hello topologii. Zastąp **użytkownika** z nazwą użytkownika SSH hello są używane podczas tworzenia klastra hello. Zastąp **CLUSTERNAME** o nazwie hello hello klastra.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Po wyświetleniu monitu wprowadź hasło hello używany podczas tworzenia użytkownika SSH hello hello klastra. Jeśli używasz klucza publicznego zamiast hasła, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello pasujących do klucza prywatnego.
   
   > [!NOTE]
   > Aby uzyskać więcej informacji na temat używania `scp` z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Po ukończeniu przekazywania hello Użyj powitania po klastra usługi HDInsight toohello tooconnect przy użyciu protokołu SSH. Zastąp **użytkownika** z nazwą użytkownika SSH hello są używane podczas tworzenia klastra hello. Zastąp **CLUSTERNAME** o nazwie hello hello klastra.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Po wyświetleniu monitu wprowadź hasło hello używany podczas tworzenia użytkownika SSH hello hello klastra. Jeśli używasz klucza publicznego zamiast hasła, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello pasujących do klucza prywatnego.
   
   Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Po nawiązaniu połączenia użyj hello następujące polecenie toocreate plik o nazwie `dev.properties`:

        nano dev.properties

4. Witaj Użyj następującego tekstu jako zawartość hello hello `dev.properties` pliku:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > W tym przykładzie przyjęto założenie, że klaster używa konta usługi Azure Storage jako hello domyślny magazyn. Jeśli klaster używa usługi Azure Data Lake Store, użyj `hdfs.url: adl:///` zamiast tego.
    
    toosave hello pliku, użyj __Ctrl + X__, następnie __Y__, a na końcu __Enter__. Witaj wartości w tym pliku Ustaw adres URL Sklepu usługi Data Lake hello i hello nazwę katalogu, którego dane są zapisywane.

3. Witaj Użyj następującego polecenia toostart hello topologii:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    To polecenie uruchamia topologii hello przy użyciu framework strumień hello przesyłając węzeł Nimbus toohello hello klastra. Topologia Hello jest definiowana za pomocą hello `writetohdfs.yaml` pliku hello jar. Witaj `dev.properties` plik jest przekazywany jako filtru, a wartości hello zawartych w pliku hello są odczytywane przez hello topologii.

## <a name="view-output-data"></a>Widok danych wyjściowych

tooview hello dane hello Użyj następującego polecenia:

    hdfs dfs -ls /stormdata/

Zostanie wyświetlona lista plików hello utworzone przez tej topologii.

Witaj poniżej znajduje się przykład hello danych zwróconej przez poprzednie polecenia hello:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Zatrzymywanie topologii hello

STORM topologie działają aż do zatrzymania lub klaster hello jest usunięty. toostop hello topologii hello Użyj następującego polecenia:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Usuwanie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Następne kroki

Teraz, gdy wiesz już, jak toouse Storm toowrite tooAzure magazynu i usługi Azure Data Lake Store, odnajdywanie innych [Storm przykłady dla usługi HDInsight](hdinsight-storm-example-topology.md).

