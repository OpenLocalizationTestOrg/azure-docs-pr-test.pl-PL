---
title: aaaApache Storm z comopnents Python - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate topologii Apache Storm, która używa składników języka Python."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: "Apache storm w języku python"
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Opracowywanie topologii Apache Storm w usłudze HDInsight przy użyciu języka Python

Dowiedz się, jak toocreate topologii Apache Storm, która używa składników języka Python. Apache Storm obsługuje wiele języków, nawet co toocombine składniki z kilku języków w topologii jeden. Witaj strumień framework (wprowadzona w systemie Storm 0.10.0) pozwala tooeasily tworzenia rozwiązania, które używają składników języka Python.

> [!IMPORTANT]
> Witaj informacje w tym dokumencie przetestowano korzystanie z systemu Storm w usłudze HDInsight 3,6. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

Witaj kod dla tego projektu jest dostępny w [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Wymagania wstępne

* Python 2.7 lub nowszej

* Java JDK 1.8 lub nowszej

* Maven 3

* (Opcjonalnie) Lokalne Środowisko deweloperskie Storm. Środowisko lokalne Storm jest potrzebne tylko wtedy, jeśli chcesz, aby lokalnie toorun hello topologii. Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).

## <a name="storm-multi-language-support"></a>Obsługa wielu języków STORM

Apache Storm została zaprojektowana toowork ze składnikami napisane przy użyciu dowolnego języka programowania. składniki Hello, trzeba zrozumieć, jak toowork z hello [Thrift definicji Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Dla języka Python moduł jest dostarczana jako część hello Apache Storm projektu, który pozwala interfejsu tooeasily z systemu Storm. Możesz znaleźć tego modułu w [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

STORM jest proces Java, który jest uruchamiany na powitania maszyny wirtualnej Java (JVM). Składniki napisanych w innych językach są wykonywane jako podprocesy. Witaj Storm komunikuje się z tych podprocesy przy użyciu JSON wiadomości wysyłane za pośrednictwem stdin/stdout. Więcej informacji dotyczących komunikacji między składnikami znajdują się w hello [protokołu Multi-lang](https://storm.apache.org/documentation/Multilang-protocol.html) dokumentacji.

## <a name="python-with-hello-flux-framework"></a>Python hello strumień Framework

framework strumień Hello umożliwia topologii Storm toodefine niezależnie od hello składników. Platforma strumień Hello korzysta z topologii Storm hello toodefine yaml programu. Witaj następujący tekst jest przykładem tooreference składnika Python w dokumencie yaml programu hello:

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

Witaj klasy `FluxShellSpout` jest używane toostart hello `sentencespout.py` skrypt, który implementuje hello spout.

Strumień oczekuje toobe skrypty języka Python hello w hello `/resources` katalogu wewnątrz hello jar zawierający hello topologii. Dlatego w tym przykładzie przechowuje hello skrypty języka Python w hello `/multilang/resources` katalogu. Witaj `pom.xml` zawiera ten plik przy użyciu następującego XML hello:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Jak wspomniano wcześniej, Brak `storm.py` pliku, który implementuje definicji Thrift hello Storm. Struktura strumień Hello obejmuje `storm.py` automatycznie po hello projekt jest budowany, dzięki czemu nie trzeba tooworry o tym go.

## <a name="build-hello-project"></a>Tworzenie projektu hello

Witaj katalog główny projektu hello używając hello następujące polecenie:

```bash
mvn clean compile package
```

To polecenie tworzy `target/WordCount-1.0-SNAPSHOT.jar` plik zawierający hello skompilowany topologii.

## <a name="run-hello-topology-locally"></a>Uruchom lokalnie hello topologii

Topologia hello toorun lokalnie, należy użyć hello następujące polecenie:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> To polecenie wymaga lokalne Środowisko deweloperskie Storm. Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)

Po uruchomieniu topologii hello, go emituje informacji toohello konsoli lokalnej podobne toohello następującego tekstu:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


Topologia hello toostop, użyj __klawisze Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Uruchom hello topologii Storm w usłudze HDInsight

1. Użyj hello następujące polecenie toocopy hello `WordCount-1.0-SNAPSHOT.jar` pliku tooyour Storm w klastrze usługi HDInsight:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Zastąp `sshuser` hello użytkownika SSH dla klastra. Zastąp `mycluster` hello nazwą klastra. Może być tooenter zostanie wyświetlony monit o hasło hello hello użytkownika SSH.

    Aby uzyskać więcej informacji o korzystaniu protokołów SSH i SCP, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Po przekazaniu pliku hello, podłącz toohello klastra przy użyciu protokołu SSH:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. W sesji SSH hello Użyj następującego polecenia toostart hello topologii w klastrze hello hello:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. W klastrze hello służy hello interfejsu użytkownika platformy Storm tooview hello topologii. Witaj interfejsu użytkownika platformy Storm znajduje się pod adresem https://mycluster.azurehdinsight.net/stormui. Zastąp `mycluster` z nazwą klastra.

> [!NOTE]
> Po rozpoczęciu topologii Storm uruchamia aż do zatrzymania. toostop hello topologii, użyj jednej z następujących metod hello:
>
> * Witaj `storm kill TOPOLOGYNAME` polecenia z wiersza polecenia hello
> * Witaj **Kill** przycisku na powitania interfejsu użytkownika platformy Storm.


## <a name="next-steps"></a>Następne kroki

Zobacz hello następujące dokumenty dla innych sposobów toouse Python z usługą HDInsight:

* [Jak toouse języka Python dla zadań MapReduce przesyłania strumieniowego](hdinsight-hadoop-streaming-python.md)
* [Jak toouse Python użytkownika określone funkcje (UDF) i Hive](hdinsight-python.md)
