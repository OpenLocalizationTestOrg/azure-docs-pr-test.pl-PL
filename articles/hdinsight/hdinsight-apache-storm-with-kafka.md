---
title: "aaaUse Kafka Apache z systemu Storm w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Apache Kafka jest instalowany z systemu Apache Storm w usłudze HDInsight. Dowiedz się, jak toowrite tooKafka, a następnie odczytu z niego, przy użyciu hello KafkaBolt i KafkaSpout składniki dostarczane z systemu Storm. Też dowiedzieć się, jak toouse hello toodefine framework strumienia i przesyłania topologii Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Apache Kafka (wersja zapoznawcza) za pomocą Storm w usłudze HDInsight

Dowiedz się, jak toouse tooread Apache Storm z i tooApache Kafka zapisu. Również w przykładzie pokazano, jak dane toosave z toohello topologii Storm systemu plików HDFS zgodnego pliku system używany przez usługi HDInsight.

> [!NOTE]
> kroki Hello w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Storm w usłudze HDInsight i Kafka w klastrze usługi HDInsight. Tych klastrów są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu hello toodirectly klastra Storm komunikować się z hello Kafka klastra.
> 
> Po zakończeniu kroków hello w tym dokumencie, pamiętaj toodelete hello klastrów tooavoid nadmiarowe opłat.

## <a name="get-hello-code"></a>Pobierz kod hello

Kod Hello na przykład hello używane w tym dokumencie jest dostępny w [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile tego projektu należy hello następującej konfiguracji dla swojego środowiska programowania:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej. HDInsight w wersji 3.5 lub nowszej wymagają Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Klient SSH (należy hello `ssh` i `scp` poleceń) — Aby uzyskać informacje, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Edytor tekstu lub IDE.

Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalowania Java i hello JDK na deweloperskiej stacji roboczej. Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.

* `JAVA_HOME`— powinna wskazywać katalog toohello hello JDK zainstalowanym.
* `PATH`— powinna zawierać hello następującej ścieżki:
  
    * `JAVA_HOME`(lub równoważne ścieżki hello).
    * `JAVA_HOME\bin`(lub równoważne ścieżki hello).
    * Hello katalog, w którym zainstalowano Maven.

## <a name="create-hello-clusters"></a>Tworzenie klastrów hello

Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka brokerzy za pośrednictwem hello publicznej sieci internet. Wszystko, co rozmów, muszą mieć tooKafka hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra. W tym przykładzie zarówno hello Kafka, jak i klastry Storm znajdują się w sieci wirtualnej platformy Azure. Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:

![Diagram klastrów Storm i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Inne usługi w klastrze hello, takich jak SSH i Ambari są dostępne za pośrednictwem hello internet. Aby uzyskać więcej informacji na powitania publicznego portów dostępnych z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Podczas tworzenia sieci wirtualnej platformy Azure, Kafka, i klastrów Storm ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager. Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure, Kafka, i klastrów Storm tooyour subskrypcji platformy Azure.

1. Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Tworzy hello następujące zasoby:
    
    * Grupy zasobów platformy Azure
    * Azure Virtual Network
    * Konto usługi Azure Storage
    * Kafka w usłudze HDInsight w wersji 3,6 (trzech węzłów procesu roboczego)
    * STORM w usłudze HDInsight w wersji 3,6 (trzech węzłów procesu roboczego)

  > [!WARNING]
  > dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego. Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.

2. Użyj hello następujące wskazówki toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Grupa zasobów**: Utwórz grupę lub wybierz istniejący. Ta grupa zawiera hello klastra usługi HDInsight.
   
    * **Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.

    * **Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello w przypadku klastrów Storm i Kafka hello. Na przykład wprowadzenie **hdi** jest tworzony klaster Storm o nazwie **storm hdi** i Kafka klastra o nazwie **kafka hdi**.
   
    * **Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello w przypadku klastrów Storm i Kafka hello.
   
    * **Hasło logowania klastra**: hello hasła użytkownika administratora w przypadku klastrów Storm i Kafka hello.
    
    * **Nazwa użytkownika SSH**: hello toocreate użytkownika SSH w przypadku klastrów Storm i Kafka hello.
    
    * **Hasło SSH**: hello hasło użytkownika SSH hello w przypadku klastrów Storm i Kafka hello.

3. Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.

4. Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**. Trwa około 20 minut toocreate hello klastrów.

Po utworzeniu zasobów hello hello bloku grupy zasobów hello jest wyświetlany.

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ storm** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu. Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.

## <a name="understanding-hello-code"></a>Znajomość hello kodu

Ten projekt zawiera dwie topologie:

* **KafkaWriter**: zdefiniowane przez hello **writer.yaml** pliku, ta topologia zapisuje tooKafka losowe zdań przy użyciu hello KafkaBolt dostarczane z systemu Apache Storm.

    Ta topologia używa niestandardowego **SentenceSpout** składnika toogenerate losowe zdań.

* **KafkaReader**: zdefiniowane przez hello **reader.yaml** pliku, ta topologia odczytuje dane z Kafka przy użyciu hello KafkaSpout dostarczane z systemu Apache Storm, a następnie dzienniki hello toostdout danych.

    Ta topologia używa hello Storm HdfsBolt toowrite danych toodefault magazynu dla klastra Storm hello.
### <a name="flux"></a>Strumień

topologie Hello są definiowane przy użyciu [strumień](https://storm.apache.org/releases/1.1.0/flux.html). Strumień została wprowadzona w systemie Storm 0.10.x i pozwala konfiguracji topologii hello tooseparate z hello kodu. Dla topologie, wykorzystujące framework strumień hello topologii hello jest zdefiniowany w pliku yaml programu. może to być zawarte w ramach topologii hello Hello yaml programu plik. Można także użyć podczas przesyłania topologii hello autonomiczny plik. Strumień obsługuje również podstawienie zmiennej w czasie wykonywania, który jest używany w tym przykładzie.

Witaj następujące parametry są ustawione w czasie wykonywania dla tych topologii:

* `${kafka.topic}`: Nazwa hello hello temat Kafka, który topologie hello odczytu/zapisu do.

* `${kafka.broker.hosts}`: hello hostem tego hello Kafka przekazuje informacje dotyczące uruchamiania na. informacje brokera Hello jest używany przez hello KafkaBolt podczas zapisywania tooKafka.

* `${kafka.zookeeper.hosts}`: hello hostów, które dozorcy działa na w hello Kafka klastra.

Aby uzyskać więcej informacji dotyczących topologii strumienia, zobacz [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Pobierz i skompiluj projekt hello

1. Na środowiska deweloperskiego pobrać projekt hello z [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), Otwórz wiersza polecenia i zmień lokalizację toohello katalogów został pobrany hello projektu.

2. Z hello **hdinsight-storm-java-kafka** katalogu, użyj hello następujące polecenia toocompile hello projektu i utworzenie pakietu wdrażania:

  ```bash
  mvn clean package
  ```

    proces pakietu Hello tworzy plik o nazwie `KafkaTopology-1.0-SNAPSHOT.jar` w hello `target` katalogu.

3. Użyj następującego polecenia toocopy hello pakietu tooyour Storm w klastrze usługi HDInsight hello. Zastąp **USERNAME** z nazwą użytkownika SSH hello hello klastra. Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello są używane podczas tworzenia klastra hello.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Po wyświetleniu monitu wprowadź hasło hello, które zostały użyte podczas tworzenia klastrów hello.

## <a name="configure-hello-topology"></a>Konfigurowanie topologii hello

1. Użyj jednej z hello następujące metody toodiscover hello Kafka brokera hostów:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Witaj Bash przykładzie założono, że `$CLUSTERNAME` zawiera nazwę hello hello klastra usługi HDInsight. Założono również, że [jq](https://stedolan.github.io/jq/) jest zainstalowany. Po wyświetleniu monitu wprowadź hasło hello hello klastra logowania konta.

    zwrócona wartość Hello jest podobne toohello następującego tekstu:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Może być więcej niż dwa hosty broker dla klastra, nie trzeba tooprovide pełną listę wszystkich tooclients hostów. Jedno lub dwa jest wystarczająca.

2. Użyj jednej z hello następujące metody toodiscover hello dozorcy Kafka hostów:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Witaj Bash przykładzie założono, że `$CLUSTERNAME` zawiera nazwę hello hello klastra usługi HDInsight. Założono również, że [jq](https://stedolan.github.io/jq/) jest zainstalowany. Po wyświetleniu monitu wprowadź hasło hello hello klastra logowania konta.

    zwrócona wartość Hello jest podobne toohello następującego tekstu:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Gdy istnieje więcej niż dwa węzły dozorcy, nie trzeba tooprovide pełną listę wszystkich tooclients hostów. Jedno lub dwa jest wystarczająca.

    Zapisz tę wartość, ponieważ jest używana później.

3. Edytuj hello `dev.properties` pliku w katalogu głównym hello hello projektu. Dodaj hello brokera i dozorcy hostów informacji toohello zgodnych wierszy w tym pliku. Witaj poniższy przykład jest konfigurowana przy użyciu hello przykładowe wartości z poprzednich kroków hello:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Zapisz hello `dev.properties` pliku, a następnie przy użyciu hello następujące polecenia tooupload go klaster Storm toohello:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Zastąp **USERNAME** z nazwą użytkownika SSH hello hello klastra. Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello są używane podczas tworzenia klastra hello.

## <a name="start-hello-writer"></a>Moduł zapisujący hello Start

1. Użyj powitania po klaster Storm toohello tooconnect przy użyciu protokołu SSH. Zastąp **USERNAME** z nazwą użytkownika SSH hello używany podczas tworzenia klastra hello. Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello używany podczas tworzenia klastra hello.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Po wyświetleniu monitu wprowadź hasło hello, które zostały użyte podczas tworzenia klastrów hello.
   
    Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Hello połączenia SSH używając hello następujące polecenia toocreate hello tematu Kafka używane przez hello topologii:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Zastąp `$KAFKAZKHOSTS` z hello dozorcy hosta pobrane w poprzedniej sekcji hello informacje.

2. Klaster Storm hello SSH połączenia toohello używając hello następujące polecenia toostart hello zapisywania topologii:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    Parametry Hello używane w tym poleceniu są:

    * `org.apache.storm.flux.Flux`: Za pomocą strumienia tooconfigure, a następnie uruchom tej topologii.

    * `--remote`: Prześlij hello tooNimbus topologii. Witaj topologia jest rozmieszczona na powitania węzłów procesu roboczego w klastrze hello.

    * `-R /writer.yaml`: Użycie hello `writer.yaml` pliku tooconfigure hello topologii. `-R`Wskazuje, że ten zasób jest uwzględniona w pliku jar hello. Znajduje się w katalogu głównym hello hello jar, więc `/writer.yaml` jest hello tooit ścieżki.

    * `--filter`: Wypełnić wpisów w hello `writer.yaml` topologii przy użyciu wartości w hello `dev.properties` pliku. Na przykład Witaj wartość hello `kafka.topic` wpis w pliku hello jest używany tooreplace hello `${kafka.topic}` wejścia w definicji topologii hello.

5. Po rozpoczęciu topologii hello, użyj następującego polecenia tooverify, że jest zapisywania danych toohello Kafka tematu hello:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Zastąp `$KAFKAZKHOSTS` z hello dozorcy hosta pobrane w poprzedniej sekcji hello informacje.

    To polecenie używa skryptu dostarczone z Kafka toomonitor hello tematu. Po chwili należy uruchomić, zwracanie losowe zdania, które zostały zapisane toohello tematu. Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Użyj klawiszy Ctrl + c toostop hello skryptu.

## <a name="start-hello-reader"></a>Czytnik hello Start

1. Klaster Storm hello SSH sesji toohello używając hello następujące polecenia toostart hello czytnika topologii:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Po uruchomieniu topologii hello Otwórz hello interfejsu użytkownika platformy Storm. Interfejs użytkownika sieci web znajduje się pod adresem https://storm-BASENAME.azurehdinsight.net/stormui. Zastąp __nazwę BAZOWĄ__ o nazwie podstawowej hello używane podczas tworzenia klastra hello. 

    Po wyświetleniu monitu użyj nazwy logowania administratora hello (domyślnie `admin`) i hasło używane podczas tworzenia klastra hello. Zostaną wyświetlone podobne toohello o następujące obraz strony sieci web:

    ![STORM interfejsu użytkownika](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Hello interfejsu użytkownika platformy Storm, zaznacz hello __czytnika kafka__ łącze w hello __podsumowanie topologii__ sekcji toodisplay informacji na temat hello __kafka czytnika__ topologii.

    ![Topologia sekcji podsumowania hello interfejsu użytkownika sieci web Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay informacji na temat wystąpień hello hello bolt rejestratora składników, wybierz hello __bolt rejestratora__ łącze w hello __elementów Bolt (czas wszystkich)__ sekcji.

    ![Rejestrator bolt link w sekcji elementów bolt hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. W hello __modułów__ wybierz łącze w hello __portu__ kolumny toodisplay rejestrowanie informacji o wystąpieniu hello składnika.

    ![Łącze modułów](./media/hdinsight-apache-storm-with-kafka/executors.png)

    Dziennik Hello zawiera dziennik hello dane odczytane ze hello Kafka tematu. Witaj informacji w dzienniku hello jest podobne toohello następującego tekstu:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Zatrzymywanie topologii hello

Z klastra Storm toohello sesji SSH należy użyć powitania po topologii Storm hello toostop polecenia:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Usuń klaster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Ponieważ hello kroków w tym dokumencie Tworzenie zarówno klastrów w hello tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów hello w hello portalu Azure. Usunięcie grupy zasobów hello usuwa wszystkie zasoby utworzone przez wykonanie tego dokumentu.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej przykładowe topologie, które mogą być używane z systemu Storm w usłudze HDInsight, zobacz [topologii Storm przykład i składniki](hdinsight-storm-example-topology.md).

Aby uzyskać informacje dotyczące wdrażania i monitorowania topologii na HDInsight opartych na systemie Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](hdinsight-storm-deploy-monitor-topology-linux.md)