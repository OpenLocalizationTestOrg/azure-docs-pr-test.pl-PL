---
title: aaaStart z Kafka Apache - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak Kafka Apache toocreate klastra w usłudze Azure HDInsight. Dowiedz się, jak toocreate tematów, subskrybentów i konsumentów."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Wprowadzenie do platformy Apache Kafka (wersja zapoznawcza) w usłudze HDInsight

Dowiedz się, jak toocreate i użyj [Apache Kafka](https://kafka.apache.org) klastra w usłudze Azure HDInsight. Kafka to rozproszona platforma przesyłania strumieniowego typu „open source”, dostępna z usługą HDInsight. Jest często używana jako broker komunikatu, ponieważ zapewnia funkcje podobne tooa publikacji / subskrypcji kolejki komunikatów.

> [!NOTE]
> Obecnie są dostępne dwie wersje platformy Kafka w usłudze HDInsight: 0.9.0 (HDInsight 3.4) i 0.10.0 (HDInsight 3.5 i 3.6). Hello kroków w tym dokumencie założono, że używasz Kafka na 3,6 HDInsight.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Tworzenie klastra platformy Kafka

Użyj hello następujące kroki toocreate Kafka w klastrze usługi HDInsight:

1. Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy**, **analizy i analiza**, a następnie wybierz **HDInsight**.
   
    ![Tworzenie klastra usługi HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. Z **podstawy**, wprowadź hello następujących informacji:

    * **Nazwa klastra**: Nazwa hello hello klastra usługi HDInsight.
    * **Subskrypcja**: Wybierz hello toouse subskrypcji.
    * **Nazwa użytkownika logowania klastra** i **hasło logowania klastra**: hello logowania podczas uzyskiwania dostępu do klastra hello za pośrednictwem protokołu HTTPS. Korzystania z tych usług tooaccess poświadczeń, takich jak hello Interfejsu sieci Web Ambari lub interfejsu API REST.
    * **Secure Shell (SSH) username**: hello logowania używany podczas uzyskiwania dostępu do klastra hello za pomocą protokołu SSH. Domyślnie jest hello takie samo jak hasło logowania klastra hello hello hasła.
    * **Grupa zasobów**: hello klastra hello toocreate grupy zasobów w.
    * **Lokalizacja**: hello regionu Azure toocreate hello klastra w.
   
 ![Wybieranie subskrypcji](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Wybierz **typ klastra**, a następnie hello ustaw następujące wartości z **konfiguracji klastra**:
   
    * **Typ klastra**: Kafka

    * **Wersja**: Kafka 0.10.0 (HDI 3.6)

    * **Warstwa klastra**: Standardowa
     
 Na koniec użyj hello **wybierz** przycisk toosave ustawienia.
     
 ![Wybieranie typu klastra](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Po wybraniu typu klastra hello, użyj hello __wybierz__ tooset hello klastra typ przycisku. Następnie użyj hello __dalej__ przycisk toofinish podstawową konfigurację.

5. W bloku **Magazyn** wybierz lub utwórz konto magazynu. Witaj czynności w tym dokumencie pozostaw hello innych pól na wartości domyślne hello. Użyj hello __dalej__ przycisk toosave magazynu konfiguracji.

    ![Ustaw hello ustawienia konta magazynu dla usługi HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. Z __aplikacji (opcjonalnie)__, wybierz pozycję __dalej__ toocontinue. W tym przykładzie nie są wymagane żadne aplikacje.

7. Z __rozmiar klastra__, wybierz pozycję __dalej__ toocontinue.

    > [!WARNING]
    > dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego.

    ![Zestaw hello Kafka rozmiar klastra](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Witaj **dyski dla każdego węzła procesu roboczego** kontroli hello skalowalność Kafka w usłudze HDInsight. Aby uzyskać więcej informacji, zobacz [Configure storage and scalability of Kafka on HDInsight (Konfigurowanie magazynu i skalowalności platformy Kafka w usłudze HDInsight)](hdinsight-apache-kafka-scalability.md).

8. Z __Zaawansowane ustawienia__, wybierz pozycję __dalej__ toocontinue.

9. Z hello **Podsumowanie**, należy przejrzeć konfigurację hello hello klastra. Użyj hello __Edytuj__ łączy toochange wszystkie ustawienia, które są nieprawidłowe. Na koniec użyj the__Create__ przycisk toocreate hello klastra.
   
    ![Podsumowanie konfiguracji klastra](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Może potrwać too20 minut toocreate hello klastra.

## <a name="connect-toohello-cluster"></a>Połącz toohello klastra

> [!IMPORTANT]
> Podczas wykonywania hello następujące kroki, musisz użyć klienta SSH. Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

Z tego klienta użyj klastra toohello tooconnect SSH:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Zastąp **SSHUSER** z nazwą użytkownika SSH hello podany podczas tworzenia klastra. Zastąp **CLUSTERNAME** o nazwie hello hello klastra.

Po wyświetleniu monitu wprowadź hasło hello, używanego hello konta SSH.

Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Pobierz hello dozorcy i brokera informacji o hoście

Podczas pracy z Kafka, musisz znać dwóch wartości host; Witaj *dozorcy* hostów i hello *brokera* hostów. Te hosty są używane przez hello Kafka interfejsu API i wiele narzędzi hello, które są dostarczane z Kafka.

Użyj następujących zmiennych środowiskowych toocreate kroki, które zawierają informacje dotyczące hosta hello hello. Te zmienne środowiskowe są używane w krokach hello w tym dokumencie.

1. Z klastra toohello połączenia SSH, użyj hello następujące polecenie tooinstall hello `jq` narzędzia. To narzędzie jest używane tooparse dokumentów JSON i jest przydatne podczas pobierania informacji o hoście brokera hello:
   
    ```bash
    sudo apt -y install jq
    ```

2. zmienne środowiskowe hello tooset informacje są pobierane z Ambari, hello Użyj następującego polecenia:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Ustaw `CLUSTERNAME=` toohello nazwę hello Kafka klastra. Ustaw `PASSWORD=` toohello hasło logowania (Administrator) używane podczas tworzenia klastra hello.

    Witaj następujący tekst jest przykładem zawartość hello `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Witaj następujący tekst jest przykładem zawartość hello `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Witaj `cut` polecenia jest używane tootrim hello listę hostów tootwo hosta. Nie trzeba tooprovide hello pełną listę hostów podczas tworzenia Kafka konsumenta lub producenta.
   
    > [!WARNING]
    > Nie należy polegać na powitania informacje zwrócone z tej sesji tooalways być dokładne. Skala klastra hello nowe brokerzy zostały dodane lub usunięte. Jeśli wystąpi błąd, a węzeł zostanie zastąpiony, mogą ulec zmianie nazwy hosta hello hello węzła.
    >
    > Należy pobrać informacji hostów dozorcy i brokera hello, tuż przed jego użyciem tooensure ma nieprawidłowe informacje.

## <a name="create-a-topic"></a>Tworzenie tematu

Platforma Kafka przechowuje strumienie danych w kategoriach nazywanych *tematami*. Programu SSH połączenia tooa klastra headnode można użyć skryptu dostarczonego z Kafka toocreate tematu:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

To polecenie łączy tooZookeeper przy użyciu informacji o hoście hello przechowywane w `$KAFKAZKHOSTS`, a następnie utworzyć temat Kafka o nazwie **testu**. Możesz sprawdzić, czy ten temat hello został utworzony przy użyciu hello następujące tematy toolist skryptu:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Hello dane wyjściowe tego polecenia Lista Kafka tematów, który zawiera hello **test** tematu.

## <a name="produce-and-consume-records"></a>Tworzenie i używanie rekordów

Platforma Kafka przechowuje *rekordy* w tematach. Rekordy są tworzone przez *producentów* i używane przez *odbiorców*. Producenci pobierają rekordy z *brokerów* platformy Kafka. Każdy węzeł procesu roboczego w klastrze usługi HDInsight jest brokerem platformy Kafka.

Użyj hello następujące kroki toostore rekordy na temat do testowania hello utworzony wcześniej, a następnie przeczytaj je za pomocą z klientem:

1. W sesji SSH hello Użyj skryptu dostarczonego z Kafka toowrite rekordów toohello tematu:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    Użytkownik nie są zwracane toohello monitu po wykonaniu tego polecenia. Zamiast tego wpisz kilka wiadomości SMS, a następnie użyć **klawisze Ctrl + C** toostop wysyłania toohello tematu. Każdy wiersz jest wysyłany jako oddzielny rekord.

2. Użyj skryptu dostarczonego z Kafka tooread rekordy z tematu hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    To polecenie pobiera hello rekordy z tematu hello i wyświetla je. Przy użyciu `--from-beginning` informuje toostart konsumenta powitania od początku hello strumienia hello, pobierane są wszystkie rekordy.

3. Użyj __klawisze Ctrl + C__ toostop powitania klienta.

## <a name="producer-and-consumer-api"></a>Interfejs API producenta i odbiorcy

Można również programowego tworzenia i wykorzystywania rekordów przy użyciu hello [API Kafka](http://kafka.apache.org/documentation#api). toobuild producent Java i konsumentów, użyj hello następujące kroki od środowiska deweloperskiego.

> [!IMPORTANT]
> Musi mieć hello następujące składniki zainstalowane w środowisku projektowania:
>
> * [Zestaw Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) lub równoważny, taki jak OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Klient SSH i hello `scp` polecenia. Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

1. Pobierz przykłady hello z [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Na przykład producent i konsument hello, użyj hello projektu w hello `Producer-Consumer` katalogu. Ten przykład zawiera następujące klasy hello:
   
    * **Uruchom** — uruchamia powitania klienta lub producenta.

    * **Producent** -magazynów 1 000 000 rekordów toohello tematu.

    * **Konsument** -odczytuje rekordy z hello tematu.

2. toocreate pakiet jar zmiany lokalizacji toohello katalogów hello `Producer-Consumer` hello katalogu i użyj następującego polecenia:

    ```
    mvn clean package
    ```

    To polecenie tworzy katalog o nazwie `target`, który zawiera plik o nazwie `kafka-producer-consumer-1.0-SNAPSHOT.jar`.

3. Użyj następujących hello polecenia toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` klastra usługi HDInsight tooyour pliku:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Zastąp **SSHUSER** hello użytkownika SSH dla klastra i Zastąp **CLUSTERNAME** o nazwie hello klastra. Po wyświetleniu monitu wprowadź hasło hello hello użytkownika SSH.

4. Raz hello `scp` polecenia zakończenie kopiowania pliku hello, Połącz toohello klastra przy użyciu protokołu SSH. Witaj Użyj następującego polecenia toowrite rejestruje toohello temat do testowania:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Po zakończeniu procesu hello, użyj poniższych tooread polecenie z tematu hello hello:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    rejestruje Hello Odczyt, wraz z liczbą rekordów, zostanie wyświetlony. Może pojawić się kilka więcej niż 1 000 000 rejestrowane jako wysłanej kilka tematu toohello rekordów za pomocą skryptu w poprzednim kroku.

6. Użyj __klawisze Ctrl + C__ tooexit powitania klienta.

### <a name="multiple-consumers"></a>Wielu odbiorców

Odbiorcy platformy Kafka używają grupy odbiorców podczas odczytywania rekordów. Przy użyciu hello same grupy z wielu klientów powoduje obciążenia zrównoważonym odczyty z tematu. Każdy odbiorca w grupie hello odbiera część hello rekordów. toosee przez ten proces w akcji, użyj hello następujące kroki:

1. Otwórz nowy klaster toohello sesji SSH, dzięki czemu masz dwa z nich. W każdej sesji, należy użyć hello następujących toostart konsumenta z hello tego samego Identyfikatora grupy odbiorców:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    To polecenie uruchamia konsumenta za pomocą Identyfikatora grupy hello `mygroup`.

    > [!NOTE]
    > Używanie poleceń hello w hello [uzyskać hello dozorcy i brokera informacji o hoście](#getkafkainfo) tooset sekcji `$KAFKABROKERS` dla tej sesji SSH.

2. Obejrzyj jako każdej sesji rekordy hello liczby otrzymywanych z hello tematu. Suma Hello zarówno sesji powinien hello tego samego zgodnie z wcześniej otrzymanej od jednego użytkownika.

Użycie przez klientów w ramach hello tej samej grupy jest obsługiwany za pomocą partycji hello hello tematu. Dla hello `test` tematu utworzonego wcześniej, ma osiem partycji. Otwórz osiem sesji SSH, uruchom klienta we wszystkich sesjach każdy odbiorca odczytuje rekordy z jednej partycji dla tematu hello.

> [!IMPORTANT]
> Grupa odbiorców nie może zawierać więcej wystąpień odbiorców niż partycji. W tym przykładzie jednej grupy konsumentów może zawierać zapasowej tooeight konsumentów, ponieważ jest hello liczby partycji w temacie hello. Może też istnieć wiele grup odbiorców — każda z nich może zawierać maksymalnie ośmiu odbiorców.

Rekordy przechowywane w Kafka są przechowywane w kolejności hello odbieranych w partycji. dostarczania uporządkowanego tooachieve rekordów *w partycji*, Utwórz grupę konsumenta, jeśli hello liczbą wystąpień klienta odpowiada hello liczby partycji. dostarczania uporządkowanego tooachieve rekordów *w temacie hello*, Utwórz grupę odbiorców z wystąpieniem tylko jednego użytkownika.

## <a name="streaming-api"></a>Interfejs API przesyłania strumieniowego

Witaj przesyłania strumieniowego interfejsu API dodano tooKafka w wersji 0.10.0; wcześniejszych wersji polegają na Apache Spark lub Storm do przetwarzania strumienia.

1. Jeśli nie zostało to jeszcze zrobione, Pobierz przykłady hello z [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour Środowisko deweloperskie. W przypadku przesyłania strumieniowego przykład hello, należy użyć hello projektu w hello `streaming` katalogu.
   
    Ten projekt zawiera tylko jedną klasę `Stream`, która odczytuje rekordy z hello `test` wcześniej utworzony temat. Zlicza wyrazy hello odczytu i emituje każdego tematu tooa word i licznik o nazwie `wordcounts`. Witaj `wordcounts` tematu jest tworzony w kolejnym kroku w tej sekcji.

2. Z wiersza polecenia hello w środowisku projektowania, zmień lokalizację toohello katalogów hello `Streaming` katalogu, a następnie hello Użyj następującego polecenia toocreate pakietu jar:

    ```bash
    mvn clean package
    ```

    To polecenie tworzy katalog o nazwie `target`, który zawiera plik o nazwie `kafka-streaming-1.0-SNAPSHOT.jar`.

3. Użyj następujących hello polecenia toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` klastra usługi HDInsight tooyour pliku:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Zastąp **SSHUSER** hello użytkownika SSH dla klastra i Zastąp **CLUSTERNAME** o nazwie hello klastra. Po wyświetleniu monitu wprowadź hasło hello hello użytkownika SSH.

4. Raz hello `scp` polecenia zakończenie kopiowania pliku hello, Połącz toohello klastra przy użyciu protokołu SSH, a następnie użyj hello następujące polecenia toocreate hello `wordcounts` tematu:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Następnie uruchom hello przesyłania strumieniowego procesu za pomocą następującego polecenia hello:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    To polecenie uruchamia hello przesyłania strumieniowego proces w tle hello.

6. Użyj hello następujące polecenie toohello wiadomości toosend `test` tematu. Komunikaty te są przetwarzane przez hello przesyłania strumieniowego przykładzie:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Witaj Użyj następującego polecenia tooview hello dane wyjściowe są zapisywane toohello `wordcounts` tematu przez hello przesyłania strumieniowego proces:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > tooview hello danych, musi podać hello tooprint konsumenta hello i toouse Deserializator hello hello klucza i wartości. Nazwa klucza Hello jest słowem hello i hello wartość klucza zawiera hello liczby.
   
    Witaj danych wyjściowych jest podobne toohello następującego tekstu:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > Liczba Hello zwiększa zawsze, gdy napotkano wyrazu.

7. Użyj hello __klawisze Ctrl + C__ tooexit hello konsumenta, a następnie użyj hello `fg` polecenia toobring hello wstecz toohello zadania przesyłania strumieniowego tła pierwszego planu. Użyj __klawisze Ctrl + C__ tooexit on również.

## <a name="delete-hello-cluster"></a>Usuń klaster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki

W tym dokumencie uzyskanych hello podstawowe informacje dotyczące pracy z Kafka Apache na HDInsight. Użyj następującego toolearn więcej informacji na temat pracy z Kafka hello:

* [Ensure high availability of your data with Kafka on HDInsight (Zapewnianie wysokiej dostępności danych dzięki platformie Kafka w usłudze HDInsight)](hdinsight-apache-kafka-high-availability.md)
* [Increase scalability by configuring managed disks with Kafka on HDInsight (Zwiększanie skalowalności przez konfigurowanie dysków zarządzanych przy użyciu platformy Kafka w usłudze HDInsight)](hdinsight-apache-kafka-scalability.md)
* [Dokumentacja platformy Apache Kafka](http://kafka.apache.org/documentation.html) na stronie kafka.apache.org.
* [Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
