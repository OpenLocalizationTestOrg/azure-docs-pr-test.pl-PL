---
title: "aaaTroubleshoot Storm przy użyciu usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon przy użyciu platformy Apache Storm w usłudze Azure HDInsight."
keywords: "Azure HDInsight, Storm, często zadawane pytania, przewodnik, typowe problemy rozwiązywania problemów"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Rozwiązywanie problemów z Storm przy użyciu usługi Azure HDInsight

Więcej informacji na temat hello Najważniejsze problemy i ich rozwiązania do pracy z ładunków Apache Storm w Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Jak uzyskać dostęp do hello interfejsu użytkownika platformy Storm w klastrze
Masz dwie opcje do uzyskiwania dostępu do interfejsu użytkownika platformy Storm hello w przeglądarce:

### <a name="ambari-ui"></a>Interfejs użytkownika narzędzia Ambari
1. Przejdź toohello Ambari w pulpicie nawigacyjnym.
2. Liście hello usług wybierz **Storm**.
3. W hello **szybkie linki** menu, wybierz opcję **interfejsu użytkownika platformy Storm**.

### <a name="direct-link"></a>Bezpośrednie połączenie
Aby dostęp do hello interfejsu użytkownika platformy Storm w hello następującego adresu URL:

https://\<nazwę klastra DNS\>/stormui

Przykład:

 https://stormcluster.azurehdinsight.NET/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Jak przenieść informacje dotyczące punktu kontrolnego spout Centrum zdarzeń Storm z jednego topologii tooanother

Podczas opracowywania topologii, które zapoznały z usługi Azure Event Hubs przy użyciu hello pliku JAR spout Centrum zdarzeń HDInsight Storm, należy wdrożyć topologię, która ma hello takie same nazwy w nowym klastrze. Należy jednak zachować dane punktu kontrolnego hello zostało zatwierdzone tooApache dozorcy hello starego klastra.

### <a name="where-checkpoint-data-is-stored"></a>Gdzie są przechowywane dane punktu kontrolnego
Dane punktu kontrolnego dla przesunięcia jest przechowywany przez hello spout Centrum zdarzeń w dozorcy w dwie ścieżki katalogu głównego:
- Punkty kontrolne spout nietransakcyjne są przechowywane w /eventhubspout.
- Dane punktu kontrolnego transakcyjne spout jest przechowywany / transakcyjnych.

### <a name="how-toorestore"></a>Jak toorestore
tooget hello skrypty i biblioteki, czy można użyć danych tooexport poza dozorcy, a następnie zaimportować hello tooZooKeeper wstecz danych pod nową nazwą, zobacz [przykłady HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

Witaj lib znajduje się w nim pliki JAR, które zawierają hello implementację dla operacji importu/eksportu hello. Hello bash folder zawiera przykładowy skrypt, który demonstruje sposób tooexport danych z hello serwera dozorcy hello starego klastra, a następnie zaimportuj go toohello zapasowego serwera dozorcy hello w nowym klastrze.

Uruchom hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) skrypt z tooexport węzły dozorcy hello, a następnie importować dane. Witaj skryptu toohello poprawne Hortonworks Data Platform (HDP) wersja aktualizacji. (Pracujemy nad wprowadzeniem tych skryptów ogólnego w usłudze HDInsight. Ogólny skrypty można uruchomić z dowolnego węzła w klastrze hello bez modyfikacji przez użytkownika hello.)

polecenie export Hello zapisuje hello tooan Apache Hadoop Distributed plików systemowych (HDFS) ścieżka metadanych (w sklepie z magazynu obiektów Blob Azure lub usługi Azure Data Lake Store) w lokalizacji, które można ustawić.

### <a name="examples"></a>Przykłady

#### <a name="export-offset-metadata"></a>Eksportowanie metadanych przesunięcia
1. Użyj SSH toogo toohello dozorcy klastra w klastrze powitania od punktu kontrolnego które hello przesunięcie musi toobe wyeksportowane.
2. Hello uruchom następujące polecenie (po zaktualizowaniu hello ciąg wersji HDP) tooexport dozorcy przesunięcie /stormmetadta/zkdata toohello danych systemu plików HDFS ścieżki:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importuj metadane przesunięcia
1. Użyj SSH toogo toohello dozorcy klastra w klastrze powitania od punktu kontrolnego które hello przesunięcie musi toobe wyeksportowane.
2. Uruchom hello następujące polecenie (po zaktualizowaniu ciąg wersji hello HDP) tooimport dozorcy Przesunięcie danych z hello systemu plików HDFS ścieżki/stormmetadata/zkdata toohello dozorcy serwera na powitania klastra docelowego:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Usuwanie metadanych przesunięcia tak, aby rozpocząć topologie przetwarzania danych od początku hello lub ze znacznikiem czasu hello użytkownik wybierze
1. Użyj SSH toogo toohello dozorcy klastra w klastrze powitania od punktu kontrolnego które hello przesunięcie musi toobe wyeksportowane.
2. Uruchom hello następujące polecenie (po zaktualizowaniu ciąg wersji hello HDP) toodelete wszystkie dozorcy Przesunięcie danych w hello bieżący klaster:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Jak znaleźć plików binarnych systemu Storm w klastrze
Pliki binarne STORM dla bieżącego stosu HDP hello są /usr/hdp/current/storm-client. Lokalizacja Hello jest hello sam zarówno dla węzłów głównych i węzłów procesu roboczego.
 
Może istnieć wiele plików binarnych dla określonej wersji HDP w /usr/hdp (na przykład /usr/hdp/2.5.0.1233/storm). Hello /usr/hdp/current/storm-client folder jest symlinked toohello najnowszą wersję, która jest uruchomiona w klastrze hello.

Aby uzyskać więcej informacji, zobacz [klastra usługi HDInsight tooan Połącz przy użyciu protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) i [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Jak ustalić hello topologii wdrożenia klastra Storm
Ustalenie wszystkie składniki, które są instalowane z HDInsight Storm. Klaster Storm składa się z czterech węzłów kategorii:

* Węzły bramy
* HEAD węzłów
* Węzły dozorcy
* Węzłów procesu roboczego
 
### <a name="gateway-nodes"></a>Węzły bramy
Węzeł bramy ma bramy i zwrotny serwer proxy usługi, która umożliwia dostęp publiczny tooan Ambari usługi zarządzania usługą active. Obsługuje ona również Ambari wiodące wyborów.
 
### <a name="head-nodes"></a>HEAD węzłów
STORM hello węzłów głównych, uruchom następujące usługi:
* Nimbus
* Serwer Ambari
* Metryki Ambari serwera
* Moduł zbierający metryki Ambari
 
### <a name="zookeeper-nodes"></a>Węzły dozorcy
Usługa HDInsight obejmuje trzy dozorcy kworum. Witaj rozmiar kworum jest stała i nie można ponownie skonfigurować.
 
Usługi STORM w klastrze hello są skonfigurowane tooautomatically Użyj hello dozorcy kworum.
 
### <a name="worker-nodes"></a>Węzłów procesu roboczego
STORM węzłów procesu roboczego Uruchom hello następujące usługi:
* Nadzorca
* Proces roboczy języka Java maszyn wirtualnych (JVMs), do uruchamiania topologii
* Ambari agent
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Jak znaleźć plików binarnych spout Centrum zdarzeń Storm do tworzenia aplikacji
 
Aby uzyskać więcej informacji o korzystaniu z topologii Storm — pliki JAR spout Centrum zdarzeń zobacz następujące zasoby hello.
 
### <a name="java-based-topology"></a>Topologia opartych na języku Java
[Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>C# — na podstawie topologii (Mono w klastrach HDInsight 3.4 + Linux Storm)
[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology) (Przetwarzanie zdarzeń usługi Azure Event Hubs przy użyciu systemu Storm w usłudze HDInsight — C#)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Pliki binarne w przypadku klastrów Linux Storm HDInsight 3.5 + elementów spout Centrum zdarzeń Storm najnowsze
toolearn toouse hello najnowsze Storm zdarzenia koncentratora spout współpracujące z usługą HDInsight 3.5 + klastrów Linux Storm, zobacz hello mvn repozytorium [plik readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Przykłady kodu źródłowego
Zobacz [przykłady](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) jak tooread i zapisywania z Centrum zdarzeń platformy Azure przy użyciu topologii Apache Storm (napisany w języku Java) w klastrze usługi HDInsight Azure.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Jak znaleźć pliki konfiguracji narzędzia Log4J Storm w klastrze
 
pliki konfiguracji tooidentify Apache Log4J Storm usług.
 
### <a name="on-head-nodes"></a>W węzłach głównych
Witaj Nimbus Log4J konfiguracji są odczytywane z usr/hdp/\<wersji HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Na węzłów procesu roboczego
Konfiguracja przełożonego Log4J Hello są odczytywane z usr/hdp/\<wersji HDP\>/storm/log4j2/cluster.xml.
 
plik konfiguracji procesu roboczego Log4J Hello są odczytywane z usr/hdp/\<wersji HDP\>/storm/log4j2/worker.xml.
 
Przykłady: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

