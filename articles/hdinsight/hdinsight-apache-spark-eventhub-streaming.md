---
title: "aaaUse Apache Spark przesyłania strumieniowego z usługą Event Hubs w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Tworzenie przykładowej przesyłania strumieniowego Apache Spark w sposób toosend danych strumienia tooAzure Centrum zdarzeń, a następnie odbierają te zdarzenia w klastrze Spark w usłudze HDInsight przy użyciu języka scala aplikacji."
keywords: "Apache spark przesyłania strumieniowego przesyłania strumieniowego spark, przykładowe spark, apache spark przesyłania strumieniowego, np. przykładowych azure Centrum zdarzeń, spark próbki"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Platforma Apache Spark przesyłania strumieniowego: klastra przetwarzania danych z usługi Azure Event Hubs z platformy Spark w usłudze HDInsight

W tym artykule możesz tworzyć Apache Spark przesyłania strumieniowego próbki, która obejmuje hello następujące kroki:

1. Korzystając z komunikatów tooingest autonomicznej aplikacji do usługi Azure Event Hub.

2. Z dwa różne podejścia możesz pobrać wiadomości powitania z Centrum zdarzeń w czasie rzeczywistym za pomocą aplikacji uruchomionej w klastrze Spark w usłudze Azure HDInsight.

3. Tworzenie potoków analitycznych przesyłania strumieniowego systemów magazynowania toodifferent danych toopersist lub uzyskiwanie szczegółowych informacji z danych na bieżąco hello.

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Przesyłanie strumieniowe Spark pojęcia

Aby uzyskać szczegółowy opis przesyłania strumieniowego Spark, zobacz [Apache Spark przesyłania strumieniowego omówienie](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). HDInsight oferuje hello tooa tej samej funkcji przesyłania strumieniowego Spark klastra na platformie Azure.  

## <a name="what-does-this-solution-do"></a>Do czego służy to rozwiązanie?

W tym artykule przedstawiono przykład przesyłania strumieniowego Spark toocreate wykonaj hello następujące kroki:

1. Tworzenie usługi Azure Event Hub, który będzie otrzymywał strumienia zdarzeń.

2. Uruchom aplikacja autonomiczna lokalnego, który generuje zdarzenia i wypchnięcia jej toohello Azure Event Hub. Witaj przykładowej aplikacji, w tym jest opublikowana w [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Zdalne uruchamianie przesyłania strumieniowego aplikacji w klastrze Spark, które odczytuje wydarzeń transmisji strumieniowej z Azure Centrum zdarzeń i przeprowadzania różnych przetwarzania danych/analizy.

## <a name="create-an-azure-event-hub"></a>Tworzenie Centrum zdarzeń platformy Azure

1. Zaloguj się na toohello [Azure Portal](https://ms.portal.azure.com)i kliknij przycisk **nowy** na powitania lewym górnym rogu ekranu hello.

2. Kliknij pozycję **Internet rzeczy**, a następnie kliknij pozycję **Event Hubs**.

    ![Tworzenie Centrum zdarzeń do przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "tworzenia Centrum zdarzeń do przesyłania strumieniowego przykład Spark")

3. W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw. Wybierz hello cenowym (Basic lub Standard). Ponadto Wybierz subskrypcję platformy Azure, lokalizacji i grupy zasobów w zasobów hello toocreate. Kliknij przycisk **Utwórz** toocreate hello w przestrzeni nazw.

      ![Podaj nazwę Centrum zdarzeń przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Podaj nazwę Centrum zdarzeń przesyłania strumieniowego przykład Spark")

    > [!NOTE]
    > Użytkownik powinien wybierz hello takie same **lokalizacji** jako klastra Apache Spark w HDInsight tooreduce opóźnienia i koszty.
    >
    >

4. Hello centra zdarzeń w przestrzeni nazw kliknij na liście hello nowo utworzonego w przestrzeni nazw.      


5. W bloku przestrzeni nazw hello, kliknij **usługi Event Hubs**, a następnie kliknij przycisk **+ Centrum zdarzeń** toocreate z nowym Centrum zdarzeń.
   
    ![Tworzenie Centrum zdarzeń do przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "tworzenia Centrum zdarzeń do przesyłania strumieniowego przykład Spark")

6. Wpisz nazwę Centrum zdarzeń, too10 liczba partycji hello zestawu i too1 przechowywania komunikatów. Firma Microsoft nie są archiwizacji z wiadomości powitania w tym rozwiązaniu, pozostaw rest hello jako domyślne, a następnie kliknij przycisk **Utwórz**.
   
    ![Podaj szczegóły zdarzenia koncentratora do przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "podanie szczegółów Centrum zdarzeń przesyłania strumieniowego przykład Spark")

7. nowo utworzone Centrum zdarzeń Hello znajduje się w bloku Centrum zdarzeń hello.
    
     ![Wyświetlanie Centrum zdarzeń, na przykład przesyłania strumieniowego Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Widok Centrum zdarzeń dla hello Spark przykład przesyłania strumieniowego")

8. W bloku przestrzeni nazw hello (nie hello określonym Centrum zdarzeń blok), kliknij **zasady dostępu współużytkowanego**, a następnie kliknij przycisk **RootManageSharedAccessKey**.
    
     ![Ustawianie zasad Centrum zdarzeń, na przykład przesyłania strumieniowego Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Centrum zdarzeń ustawić zasady dla hello Spark przykład przesyłania strumieniowego")

9. Kliknij przycisk hello toocopy przycisku Kopiuj hello **RootManageSharedAccessKey** głównej Schowka o toohello ciąg połączenia i klucza. Zapisz te toouse później w samouczku hello.
    
     ![Wyświetlanie kluczy zasad Centrum zdarzeń, na przykład przesyłania strumieniowego Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "klucze zasad Centrum zdarzeń widoku hello Spark przykład przesyłania strumieniowego")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Wysyłanie wiadomości tooAzure Centrum zdarzeń przy użyciu języka Scala przykładowej aplikacji

W tej sekcji użyjesz lokalnego Scala aplikacja autonomiczna, który generuje strumienia zdarzeń i wysyła je z tooAzure Centrum zdarzeń, który został utworzony wcześniej. Ta aplikacja jest dostępna w witrynie GitHub pod [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). w tym miejscu w krokach Hello założono, ma to repozytorium GitHub już rozwidlone.

1. Upewnij się, że masz następujące hello zainstalowany na komputerze hello gdzie uruchomić tę aplikację.

    * Oracle Java Development kit. Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. Możesz pobrać go z [tutaj](https://maven.apache.org/download.cgi). Dostępne są instrukcje tooinstall Maven [tutaj](https://maven.apache.org/install.html).

2. Otwórz wiersz polecenia i przejdź do lokalizacji toohello sklonować repozytorium GitHub hello hello przykładowej Scala aplikacji i uruchom następujące polecenie toobuild hello aplikacji hello.

        mvn package

3. Hello jar dane wyjściowe aplikacji hello **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, utworzony na podstawie **/target** katalogu. Możesz użyć tego JAR w dalszej części tego artykułu tootest hello kompletnego rozwiązania.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Utwórz komunikatów tooreceive aplikacji z Centrum zdarzeń do klastra Spark 

Mamy dwa tooconnect metod przesyłania strumieniowego Spark i usługi Azure Event Hubs, połączenie oparte na odbiorcy i oparte na DStream bezpośrednie połączenie. Na podstawie DStream bezpośrednio wprowadzono na stycznia 2017 w wersji hello 2.0.3. Ma tooreplace hello oryginalnego odbiornika połączenia jako jest więcej wydajności i wydajne zasobów. Znaleziono więcej szczegółów w [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). Bezpośrednie DStream obsługuje tylko Spark 2.0 +.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Tworzenie aplikacji hello zależności toospark eventhubs łącznik

Firma Microsoft opublikuje również hello przemieszczania wersji Spark-EventHubs w witrynie GitHub. toouse hello przemieszczania Spark EventHubs, pierwszym krokiem hello jest wersja tooindicate GitHub zgodnie z hello źródło repozytorium, dodając powitania po toopom.xml wpis:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

Następnie można dodać następujące zależności tooyour projektu tootake hello wersji wstępnej, hello.

Zależność narzędzia maven

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

Zależności SBT

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Bezpośrednie połączenie DStream

Można pobrać plik jar wbudowanych zawierający przykłady użycia bezpośredniego DStream w [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).

Plik jar Hello zawiera trzy przykłady, których kodu źródłowego są dostępne pod adresem [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Biorąc [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) na przykład:

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

W hello powyżej przykład `eventhubParameters` są hello parametrów określonych tooa EventHubs SIS i że masz toopass on toohello `createDirectStreams` interfejs API, który konstruuje przestrzeni nazw usługi Event Hubs tooa mapowania obiektu DStream bezpośredniego. Za pośrednictwem obiektu DStream bezpośredniego hello należy wywołać wszystkich API DStream dostarczonych przez strukturę interfejsu API platformy Spark przesyłania strumieniowego. W tym przykładzie mamy obliczania częstotliwość hello każdego wyrazu w odstępach czasu hello ostatniej partii micro 3.

### <a name="receiver-based-connection"></a>Odbiornik połączenia

Spark, przesyłanie strumieniowe przykładowej aplikacji napisanych w języku Scala, który odbiera zdarzenia i miejsc docelowych toodifferent hello trasy, znajduje się w temacie [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Wykonaj kroki hello poniżej aplikacji hello tooupdate dla danej konfiguracji Centrum zdarzeń i Utwórz hello jar danych wyjściowych.

1. Uruchom IntelliJ IDEA i z hello uruchomić ekranu wybierz **wyewidencjonowania z kontroli wersji** , a następnie kliknij przycisk **Git**.
   
    ![Apache Spark przesyłania strumieniowego przykład — Pobierz źródła z repozytorium Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark przesyłania strumieniowego przykład — Pobierz źródła z repozytorium Git")

2. W hello **klonowania repozytorium** okno dialogowe, podaj hello tooclone repozytorium Git toohello adres URL z, określ hello tooclone katalogu do, a następnie kliknij **klonowania**.
   
    ![Apache Spark przesyłania strumieniowego przykład — klonować z Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark przesyłania strumieniowego przykład — klonować z Git")
3. Wykonaj monity hello dopóki projektu hello jest całkowicie sklonować. Naciśnij klawisz **Alt + 1** tooopen hello **widoku projektu**. Powinien on przypominać następujące hello.
   
    ![Apache Spark przesyłania strumieniowego przykład — widok projektu](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark przesyłania strumieniowego przykład — widok projektu")
4. Upewnij się, że kod aplikacji hello jest skompilowana przy użyciu Java8. tooensure tego, kliknij **pliku**, kliknij przycisk **struktury projektu**, a na powitania **projektu** karcie, upewnij się, że ustawiono zbyt poziomie język projektu**8 - wyrażeń lambda, typ adnotacje, itp.**.
   
    ![Apache Spark przesyłania strumieniowego przykład — zestaw kompilatora](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark przesyłania strumieniowego przykład — zestaw kompilatora")
5. Otwórz hello **pom.xml** i upewnij się, że wersja Spark hello jest poprawna. W obszarze `<properties>` węzła, Znajdź powitania po fragment i zweryfikować hello Spark wersji.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. Aplikacja Hello wymaga jar zależności, nazywany **jar sterownik JDBC**. Jest to wymagane toowrite wiadomości powitania odebranych z Centrum zdarzeń do bazy danych Azure SQL. Możesz pobrać ten jar (4.1 lub nowszym) z [tutaj](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Dodaj odwołanie toothis jar hello biblioteki projektu. Wykonaj następujące kroki hello:
     
     1. Z którym masz aplikacji hello, Otwórz okno IntelliJ IDEA, kliknij przycisk **pliku**, kliknij przycisk **struktury projektu**, a następnie kliknij przycisk **biblioteki**. 
     2. Kliknij hello dodać ikonę (![dodać ikonę](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), kliknij przycisk **Java**, a następnie przejdź toohello której pobrano jar sterownik JDBC hello. Wykonaj hello monity tooadd hello jar pliku toohello projektu biblioteki.

         ![Dodaj brakujące zależności](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Dodaj brakujące słoików zależności")
     3. Kliknij przycisk **Zastosuj**.

7. Utwórz plik jar hello danych wyjściowych. Wykonaj następujące kroki hello.

   1. W hello **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** a następnie kliknij przycisk hello oraz symboli. Na powitania wyskakującym oknie dialogowym kliknij pozycję **JAR**, a następnie kliknij przycisk **z modułów z zależnościami**.      
       
       ![Przykład strumieniowych Apache Spark — tworzenie JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "przykład strumieniowych Apache Spark — tworzenie JAR")
   2. W hello **utworzyć JAR z modułów** okna dialogowego, kliknij przycisk wielokropka hello (![wielokropka](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) przed hello **klasy głównym**.
   3. W hello **Wybierz klasy głównym** okno dialogowe, wybierz jedno z dostępnych klas hello a następnie kliknij przycisk **OK**.
      
       ![Apache Spark przesyłania strumieniowego przykład — wybierz klasę dla jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark przesyłania strumieniowego przykład — wybierz klasę dla jar")
   4. W hello **utworzyć JAR z modułów** okna dialogowego polu należy upewnić się, ta opcja hello zbyt**wyodrębnić docelowy toohello JAR** jest zaznaczone, a następnie kliknij przycisk **OK**. Spowoduje to utworzenie jednego JAR z wszystkie zależności.
      
       ![Przykład strumieniowych Apache Spark — tworzenie jar z modułów](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "przykład strumieniowych Apache Spark — tworzenie jar z modułów")
   5. Witaj **układu dane wyjściowe** karta zawiera listę wszystkich słoików hello, które są dołączane jako część hello projekt Maven. Można wybrać i hello Usuń te, na którym hello Scala aplikacji nie ma żadnych zależności bezpośrednich. Dla aplikacji hello jest tworzone w tym miejscu, należy usunąć wszystkie elementy oprócz hello ostatnią (**danych wyjściowych kompilacji spark-przesyłania strumieniowego danych trwałości — przykłady**). Wybierz toodelete słoików hello, a następnie kliknij przycisk hello **usunąć** ikona (![ikona usuwania](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Apache Spark przesyłania strumieniowego przykład — usuń wyodrębnione słoików](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark przesyłania strumieniowego przykład — usuń wyodrębnione słoików")
      
       Upewnij się, że **kompilacji w upewnij** pole jest zaznaczone, co zapewnia, że jar hello jest tworzony za każdym razem, gdy projekt hello jest utworzony lub zaktualizowany. Kliknij przycisk **Zastosuj**.
   6. W hello **układu dane wyjściowe** karty u dołu hello hello **dostępne elementy** okno, masz hello SQL JDBC jar, że dodane starszych toohello projektu biblioteki. Należy dodać ten toohello **układu dane wyjściowe** kartę. Kliknij prawym przyciskiem myszy plik jar hello, a następnie kliknij przycisk **Wyodrębnij do głównego dane wyjściowe**.
      
       ![Apache Spark przesyłania strumieniowego przykład — jar zależności wyodrębniania](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark przesyłania strumieniowego przykład — jar zależności wyodrębniania")  
      
       Witaj **układu dane wyjściowe** kartę powinna wyglądać następująco.
      
       ![Apache Spark przesyłania strumieniowego przykład — karta ostateczne dane wyjściowe](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark przesyłania strumieniowego przykład — karta ostateczne dane wyjściowe")        
      
       W hello **struktury projektu** okno dialogowe, kliknij przycisk **Zastosuj** , a następnie kliknij przycisk **OK**.    
   7. Na pasku menu hello, kliknij przycisk **kompilacji**, a następnie kliknij przycisk **projektu należy**. Możesz również kliknąć **artefaktów kompilacji** toocreate hello jar. Hello jar dane wyjściowe utworzony na podstawie **\classes\artifacts**.
      
       ![Przykład strumieniowych Apache Spark - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "przykład strumieniowych Apache Spark - output JAR")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Zdalne uruchamianie aplikacji hello w klastrze Spark przy użyciu programu Livy

W tym artykule jest używane Livy toorun hello Apache Spark przesyłania strumieniowego aplikacji zdalnie w klastrze Spark. Aby uzyskać szczegółowe omówienie na jak klastra toouse Livy z Spark w usłudze HDInsight, zobacz [przesyłania zadania zdalnie tooan Apache Spark klastra w usłudze Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md). Przed rozpoczęciem działania aplikacji do przesyłania strumieniowego Spark hello istnieje kilka rzeczy, które należy wykonać:

1. Uruchom zdarzenia toogenerate aplikacji autonomicznej lokalne powitania i wysyłane tooEvent koncentratora. Witaj Użyj następującego polecenia toodo tak:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Przesyłanie strumieniowe jar hello kopiowania (**spark-przesyłania strumieniowego data trwałości examples.jar**) toohello magazynu obiektów Blob Azure skojarzonego z klastrem hello. Dzięki temu tooLivy dostępny jar hello. Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), więc toodo, narzędzie wiersza polecenia. Istnieje wiele innych klientów za pomocą tooupload danych. Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).
3. Zainstaluj narzędzie CURL na komputerze hello, w którym działają te aplikacje z. Używamy hello tooinvoke CURL Livy punkty końcowe toorun hello zadania zdalnie.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Uruchom hello Spark przesyłania strumieniowego aplikacji tooreceive hello zdarzeń do obiektu Blob magazynu Azure jako tekst

Otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL, a następnie uruchom hello następujące polecenie (zastąp nazwę użytkownika/hasło i klaster nazwa):

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Witaj parametrów w pliku hello **inputBlob.txt** są zdefiniowane w następujący sposób:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Daj nam zrozumieć, jakie są parametry hello w pliku wejściowym hello:

* **plik** jest plik jar hello ścieżki toohello aplikacji hello konta magazynu platformy Azure skojarzone z klastrem hello.
* **className** jest hello nazwy klasy hello w hello jar.
* **argumenty** hello lista argumentów wymaganych przez klasę hello
* **numExecutors** hello liczba rdzeni używane przez przesyłania strumieniowego aplikacji hello toorun Spark. Zawsze należy co najmniej dwa razy hello liczby partycji Centrum zdarzeń.
* **executorMemory**, **executorCores**, **driverMemory** są zasoby tooassign wymagane parametry używane toohello przesyłania strumieniowego aplikacji.

> [!NOTE]
> Nie trzeba toocreate hello dane wyjściowe foldery (EventCheckpoint, EventCount/EventCount10) używane jako parametry. przesyłanie strumieniowe aplikacji Hello utworzy je.
>
>

Po uruchomieniu polecenia hello, powinny pojawić się dane wyjściowe podobne do następujących hello:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Zanotuj identyfikator partii hello hello ostatni wiersz danych wyjściowych hello (w tym przykładzie jest '1'). tooverify, który hello aplikacji zostanie wykonane pomyślnie, można sprawdzić konta magazynu Azure skojarzony z klastrem hello i powinna zostać wyświetlona hello **/EventCount/EventCount10** folder utworzony istnieje. Ten folder powinien zawierać obiektów blob, które przechwytuje hello liczbą zdarzeń przetwarzane w ramach hello okres określony dla parametru hello **partii interwał w sekundach**.

Aplikacja przesyłania strumieniowego Spark Hello będzie nadal toorun, do momentu jego zakończenia. toodo tak, użycie hello następujące polecenie:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Uruchamianie aplikacji hello tooreceive hello zdarzeń do obiektu Blob magazynu Azure jako JSON
Otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL, a następnie uruchom hello następujące polecenie (zastąp nazwę użytkownika/hasło i klaster nazwa):

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Witaj parametrów w pliku hello **inputJSON.txt** są zdefiniowane w następujący sposób:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Parametry Hello są podobne toowhat, określone dla hello tekst wyjściowy hello poprzedniego kroku. Ponownie nie trzeba toocreate hello dane wyjściowe foldery (EventCheckpoint, EventCount/EventCount10) używane jako parametry. przesyłanie strumieniowe aplikacji Hello utworzy je.

 Po uruchomieniu polecenia hello, można sprawdzić konta magazynu Azure skojarzony z klastrem hello i powinna zostać wyświetlona hello **/EventStore10** folder utworzony istnieje. Otwórz każdy plik i jest poprzedzony prefiksem **części -** i powinna zostać wyświetlona hello zdarzenia przetwarzane w formacie JSON.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Uruchamianie aplikacji hello tooreceive hello zdarzeń w tabeli programu Hive
Witaj toorun aplikacji przesyłania strumieniowego Spark strumieni zdarzeń do gałęzi tabeli, możesz muszą niektóre dodatkowe składniki. Są to:

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* gałąź site.xml

Witaj **JAR** pliki są dostępne w klastrze Spark w usłudze HDInsight w `/usr/hdp/current/spark-client/lib`. Witaj **hive-site.xml** znajduje się w temacie `/usr/hdp/current/spark-client/conf`.

Można użyć [WinScp](http://winscp.net/eng/download.php) toocopy za pośrednictwem tych plików z komputera lokalnego tooyour hello klastra. Następnie można użyć tych plików przez tooyour konta magazynu skojarzone z klastrem hello toocopy narzędzia. Aby uzyskać więcej informacji dotyczących sposobu tooupload pliki toohello konta magazynu, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).

Po skopiowaniu przez tooyour plików hello kontem magazynu platformy Azure, otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL, a następnie uruchom hello następujące polecenie (zastąp nazwę użytkownika/hasło i klaster nazwa):

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Witaj parametrów w pliku hello **inputHive.txt** są zdefiniowane w następujący sposób:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Parametry Hello są podobne toowhat, określone dla hello tekst wyjściowy w poprzednich krokach hello. Ponownie, nie trzeba dane wyjściowe hello toocreate folderów (EventCheckpoint, EventCount/EventCount10) lub hello tabeli Hive (EventHiveTable10), które są używane jako parametry wyjściowe. przesyłanie strumieniowe aplikacji Hello utworzy je. Należy pamiętać, że hello **słoików** i **pliki** opcja zawiera pliki JAR toohello ścieżek i hello hive-site.xml skopiowanego toohello konta magazynu.

Pomyślnie utworzono tooverify, który hello tabelę programu hive, możesz SSH na powitania klastra i wykonywania zapytań programu Hive. Aby uzyskać instrukcje, zobacz [używanie Hive z usługą Hadoop w usłudze HDInsight przy użyciu protokołu SSH](hdinsight-hadoop-use-hive-ssh.md). Po nawiązaniu połączenia przy użyciu protokołu SSH, można uruchomić następujące polecenie tooverify hello tej tabeli Hive hello **EventHiveTable10**, zostanie utworzona.

    show tables;

Powinny być widoczne następujące dane wyjściowe podobne toohello:

    OK
    eventhivetable10
    hivesampletable

Można również uruchomić zapytania SELECT tooview zawartość hello hello tabeli.

    SELECT * FROM eventhivetable10 LIMIT 10;

Powinny pojawić się dane wyjściowe podobne do następujących hello:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Uruchamianie aplikacji hello tooreceive hello zdarzeń w tabeli bazy danych Azure SQL
Przed uruchomieniem tego kroku, upewnij się, że masz utworzony bazę danych Azure SQL. Aby uzyskać instrukcje, zobacz [Utwórz bazę danych SQL w minutach](../sql-database/sql-database-get-started.md). toocomplete to sekcja, potrzebne są wartości dla nazwy bazy danych, nazwę serwera bazy danych i hello poświadczenia administratora bazy danych jako parametry. Mimo że nie trzeba toocreate hello bazy danych tabeli. Witaj przesyłania strumieniowego aplikacji Spark utworzy który.

Otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL i uruchom następujące polecenie hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Witaj parametrów w pliku hello **inputSQL.txt** są zdefiniowane w następujący sposób:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify, który hello aplikacji zostanie wykonane pomyślnie, możesz połączyć toohello bazy danych Azure SQL przy użyciu programu SQL Server Management Studio. Aby uzyskać instrukcje dotyczące toodo, który zobacz [uzyskuj tooSQL bazy danych programu SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md). Po przejściu toohello połączenia bazy danych, można przejść toohello **EventContent** tabeli, która została utworzona przez hello przesyłania strumieniowego aplikacji. Danych hello tooget szybkie zapytania jest uruchamiane z hello tabeli. Uruchom następujące zapytanie hello:

    SELECT * FROM EventCount

Powinny pojawić się dane wyjściowe podobne toohello poniżej:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)
* [Projekt połączenie oparte na odbiorcy i bezpośredniego DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
