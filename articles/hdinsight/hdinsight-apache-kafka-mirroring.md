---
title: Tematy Apache Kafka aaaMirror - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Apache Kafka dublowania funkcji toomaintain repliki Kafka w klastrze usługi HDInsight przy dublowania tematy tooa dodatkowej klastra."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Tematy Apache Kafka tooreplicate MirrorMaker za pomocą Kafka w usłudze HDInsight (wersja zapoznawcza)

Dowiedz się, jak toouse Apache Kafka przez dublowanie funkcji tooreplicate tematy tooa dodatkowej klastra. Dublowanie mogą być uruchomione jako ciągły proces wykonywany lub sporadycznie używane jako metody migracji danych z jednego klastra tooanother.

W tym przykładzie dublowanie jest używane tooreplicate tematy między dwoma klastrami usługi HDInsight. Obu klastrach znajdują się w sieci wirtualnej platformy Azure w hello tego samego regionu.

> [!WARNING]
> Dublowanie nie należy traktować jako oznacza tooachieve odporności na uszkodzenia. przesunięcia tooitems Hello w temacie różnią się między hello klastrów źródłowych i docelowych, więc klienci nie mogą używać hello dwa zamiennie.
>
> Jeśli masz obawy odporność na uszkodzenia, należy ustawić replikacji hello tematów w ramach klastra. Aby uzyskać więcej informacji, zobacz [wprowadzenie Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>Jak działa Kafka dublowania

Dublowania działa przy użyciu hello MirrorMaker narzędzia (część Apache Kafka) tooconsume rekordy z tematów w klastrze źródłowym hello, a następnie utwórz kopię lokalną w klastrze docelowym hello. MirrorMaker używa jednej (lub więcej) *konsumentów* odczytanej z klastra źródłowego hello, a *producent* który zapisuje toohello klastra lokalnego (docelowy).

powitania po diagram przedstawia proces lustrzane hello:

![Diagram hello dublowania procesu](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka usługi za pośrednictwem hello publicznej sieci internet. Kafka producentów i konsumentów, musi być w hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra. W tym przykładzie zarówno hello źródła Kafka, jak i klastrów docelowych znajdują się w sieci wirtualnej platformy Azure. Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:

![Diagram źródłowy i docelowy Kafka klastrów w sieci wirtualnej platformy Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

Witaj klastrów źródłowych i docelowych mogą być różne w hello liczby węzłów i partycji, różni się od przesunięcia w tematach hello również. Dublowania przechowuje hello wartości klucza, który jest używany do partycjonowania, więc na podstawie na klucz jest zachowana kolejność rekordów.

### <a name="mirroring-across-network-boundaries"></a>Dublowanie bariery sieciowe

Jeśli potrzebujesz toomirror między klastrami Kafka w różnych sieciach, istnieją hello następujące dodatkowe zagadnienia:

* **Bram**: hello sieci muszą być stanie toocommunicate na powitania TCPIP poziom.

* **Rozpoznawanie nazw**: hello Kafka klastrów w każdej sieci musi być możliwe tooconnect tooeach innych przy użyciu nazwy hostów. Może to wymagać się, że serwer systemu nazw domen (DNS) w każdej sieci, który jest skonfigurowany toohello żądań tooforward innych sieci.

    Podczas tworzenia sieci wirtualnej platformy Azure, zamiast hello podane automatyczne DNS z sieci hello, należy określić niestandardowy DNS serwera i hello adres IP serwera hello. Po hello utworzenia sieci wirtualnej należy następnie utwórz maszynę wirtualną platformy Azure, który korzysta z tego adresu IP, a następnie zainstalować i skonfigurować oprogramowanie DNS na nim.

    > [!WARNING]
    > Utworzyć i skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej hello hello niestandardowy serwer DNS. Nie istnieje konfiguracja dodatkowe wymagane dla usługi HDInsight toouse powitania serwera DNS skonfigurowanego dla hello sieci wirtualnej.

Aby uzyskać więcej informacji na łącząca dwie sieci wirtualne platformy Azure, zobacz [skonfigurować połączenia do wirtualnymi](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Tworzenie Kafka klastrów

Podczas tworzenia sieci wirtualnej platformy Azure i Kafka klastrów ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager. Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure i dwa Kafka tooyour klastrów subskrypcji platformy Azure.

1. Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego. Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.

2. Witaj Użyj następujących informacji toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:
    
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Grupa zasobów**: Utwórz grupę lub wybierz istniejący. Ta grupa zawiera hello klastra usługi HDInsight.

    * **Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.
     
    * **Podstawowa nazwa klastra**: Ta wartość jest używana jako podstawowej nazwy hello hello Kafka klastrów. Na przykład wprowadzenie **hdi** tworzy klastry o nazwie **hdi źródła** i **dest hdi**.

    * **Nazwa użytkownika logowania klastra**: klastrów Kafka hello nazwa użytkownika administratora dla hello źródłowym i docelowym.

    * **Hasło logowania klastra**: klastrów Kafka hello hasła użytkownika administratora dla hello źródłowym i docelowym.

    * **Nazwa użytkownika SSH**: klastrów Kafka toocreate użytkownika SSH hello hello źródłowego i docelowego.

    * **Hasło SSH**: klastrów Kafka hello hasła dla użytkownika SSH hello hello źródłowym i docelowym.

3. Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.

4. Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**. Trwa około 20 minut toocreate hello klastrów.

Po utworzeniu hello zasoby zostaną przekierowane tooa bloku hello grupę zasobów, która zawiera hello klastrów i pulpitu nawigacyjnego sieci web.

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ źródła** i **nazwę BAZOWĄ dest**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu. Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.

## <a name="create-topics"></a>Tworzenie tematów

1. Połącz toohello **źródła** klastra przy użyciu protokołu SSH:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Zastąp **sshuser** z nazwą użytkownika SSH hello używany podczas tworzenia klastra hello. Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello używany podczas tworzenia klastra hello.

    Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj następujących hello polecenia toofind hello dozorcy hosty do klastra źródłowego hello:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Utworzono hello Użyj następującego polecenia tooverify, który hello tematu:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    odpowiedź Hello zawiera `testtopic`.

4. Witaj Użyj następujących informacji o hoście dozorcy hello tooview dla tego (hello **źródła**) klastra:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    To polecenie zwróci informacje toohello podobne następującego tekstu:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Zapisz te informacje. W następnej sekcji hello jest używany.

## <a name="configure-mirroring"></a>Konfigurowanie funkcji dublowania

1. Połącz toohello **docelowego** klastra przy użyciu innej sesji SSH:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Zastąp **sshuser** z nazwą użytkownika SSH hello używany podczas tworzenia klastra hello. Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello używany podczas tworzenia klastra hello.

    Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj hello następujące polecenie toocreate `consumer.properties` pliku, który opisuje sposób toocommunicate z hello **źródła** klastra:

    ```bash
    nano consumer.properties
    ```

    Witaj Użyj następującego tekstu jako zawartość hello hello `consumer.properties` pliku:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Zastąp **SOURCE_ZKHOSTS** z hello dozorcy hostuje informacje z hello **źródła** klastra.

    Ten plik zawiera opis powitania klienta informacji toouse podczas odczytywania ze źródła hello Kafka klastra. Aby uzyskać więcej informacji o konfiguracji konsumenta, zobacz [Configs konsumenta](https://kafka.apache.org/documentation#consumerconfigs) na kafka.apache.org.

    toosave hello pliku, użyj **Ctrl + X**, **Y**, a następnie **Enter**.

3. Przed skonfigurowaniem producent hello, który komunikuje się z klastrem docelowego hello, należy znaleźć brokera hello hosty dla hello **docelowego** klastra. Użyj następującego polecenia tooretrieve hello te informacje:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Zastąp `$PASSWORD` z hasłem konta (Administrator) logowania hello hello klastra.

    Zastąp `$CLUSTERNAME` o nazwie hello hello klastra docelowego.

    Te polecenia zwracają informacje podobne toohello poniżej:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Użyj powitania po toocreate `producer.properties` pliku, który opisuje sposób toocommunicate z hello **docelowego** klastra:

    ```bash
    nano producer.properties
    ```

    Witaj Użyj następującego tekstu jako zawartość hello hello `producer.properties` pliku:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Zastąp **DEST_BROKERS** hello brokera informacje z poprzedniego kroku hello.

    Aby uzyskać więcej informacji o konfiguracji producenta, zobacz [Configs producent](https://kafka.apache.org/documentation#producerconfigs) na kafka.apache.org.

## <a name="start-mirrormaker"></a>Uruchom MirrorMaker

1. Z toohello połączenia SSH hello **docelowego** klastra, użyj powitania po procesie MirrorMaker hello toostart polecenia:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    Parametry Hello używana w tym przykładzie są:

    * **--consumer.config**: Określa plik hello, który zawiera właściwości konsumenta. Te właściwości są używane toocreate konsumenta odczytująca hello *źródła* Kafka klastra.

    * **--producer.config**: Określa plik hello, który zawiera właściwości producenta. Te właściwości są używane toocreate producenta, która zapisuje toohello *docelowego* Kafka klastra.

    * **--dozwolonych**: listę tematów, które MirrorMaker replikuje z hello źródła klastra toohello docelowego.

    * **--num.streams**: hello liczba toocreate wątków konsumenta.

 Uruchamianie MirrorMaker zwraca informacje toohello podobne następującego tekstu:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. Z toohello połączenia SSH hello **źródła** klastra, użyj następującego polecenia toostart producent hello i wysyłanie komunikatów toohello tematu:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Zastąp `$PASSWORD` hasłem logowania (Administrator) hello hello źródła klastra.

    Zastąp `$CLUSTERNAME` o nazwie hello hello źródła klastra.

     Po przyjeździe do pustego wiersza z kursorem, wpisz w kilku wiadomości SMS. Ustawienia te są wysyłane toohello tematu na powitania **źródła** klastra. Na koniec użyj **klawisze Ctrl + C** tooend hello producent procesu.

3. Z toohello połączenia SSH hello **docelowego** klastra, użyj **klawisze Ctrl + C** hello tooend MirrorMaker procesu. Następnie użyj hello następujące polecenia tooverify tego hello `testtopic` tematu został utworzony, a dane w temacie hello został toothis replikowanych dublowania:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Zastąp `$PASSWORD` hasłem logowania (Administrator) hello hello klastra docelowego.

    Zastąp `$CLUSTERNAME` o nazwie hello hello klastra docelowego.

    Witaj listę tematów zawiera teraz `testtopic`, który jest tworzony podczas MirrorMaster odzwierciedla hello tematu z docelowym toohello klastra źródłowego hello. wiadomości powitania pobrane z tematu hello są takie same jak został wprowadzony w klastrze źródłowym hello hello.

## <a name="delete-hello-cluster"></a>Usuń klaster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Ponieważ hello kroków w tym dokumencie Tworzenie zarówno klastrów w hello tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów hello w hello portalu Azure. Usunięcie grupy zasobów hello usuwa wszystkie zasoby utworzone, postępując w tym dokumencie, hello Azure Virtual Network i konto magazynu używane przez hello klastrów.

## <a name="next-steps"></a>Następne kroki

W tym dokumencie przedstawiono sposób toouse MirrorMaker toocreate repliki Kafka klastra. Z Kafka, należy użyć następującego łącza toodiscover hello toowork inne sposoby:

* [Dokumentację Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) na cwiki.apache.org.
* [Wprowadzenie do Apache Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md)
* [Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
