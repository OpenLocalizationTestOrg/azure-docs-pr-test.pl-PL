---
title: "aaaApache Spark strukturalnych przesyłania strumieniowego z Kafka - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Apache Spark dane przesyłane strumieniowo (DStream) tooget do lub wychodzący Apache Kafka. W tym przykładzie można przesyłać strumieniowo dane za pomocą notesu Jupyter z platformy Spark w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Użyj Spark strukturalnych przesyłania strumieniowego z Kafka (wersja zapoznawcza) w usłudze HDInsight

Dowiedz się, jak toouse strukturalnych przesyłania strumieniowego Spark tooread danych z Kafka Apache na Azure HDInsight.

Struktura przesyłania strumieniowego Spark jest aparatem przetwarzania strumienia oparty na Spark SQL. Umożliwia się, że możesz obliczenia przesyłania strumieniowego tooexpress hello taki sam jak partii obliczeń w danych statycznych. Aby uzyskać więcej informacji o strukturze przesyłania strumieniowego, zobacz hello [strukturalnych przesyłania strumieniowego przewodnik programowania w języku [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) w serwisie Apache.org.

> [!IMPORTANT]
> W tym przykładzie użyto Spark 2.1 w usłudze HDInsight 3,6. Strukturalne Streaming jest uznawany za __alfa__ 2.1 Spark.
>
> kroki Hello w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Spark w usłudze HDInsight i Kafka w klastrze usługi HDInsight. Tych klastrów są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu hello toodirectly klastra Spark komunikować się z hello Kafka klastra.
>
> Po zakończeniu kroków hello w tym dokumencie, pamiętaj toodelete hello klastrów tooavoid nadmiarowe opłat.

## <a name="create-hello-clusters"></a>Tworzenie klastrów hello

Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka brokerzy za pośrednictwem hello publicznej sieci internet. Wszystko, co rozmów, muszą mieć tooKafka hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra. W tym przykładzie zarówno hello Kafka, jak i klastry Spark znajdują się w sieci wirtualnej platformy Azure. Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:

![Diagram klastry Spark i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Witaj Kafka usługi jest ograniczone toocommunication w ramach sieci wirtualnej hello. Inne usługi w klastrze hello, takich jak SSH i Ambari, są dostępne za pośrednictwem hello internet. Aby uzyskać więcej informacji na powitania publicznego portów dostępnych z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Chociaż można utworzyć sieci wirtualnej platformy Azure, Kafka i Spark klastry ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager. Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure, Kafka, i Spark klastrów tooyour subskrypcji platformy Azure.

1. Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Ten szablon tworzy hello następujące zasoby:

    * Kafka w klastrze HDInsight 3.5.
    * Platforma Spark w klastrze HDInsight 3,6.
    * Sieci wirtualnej platformy Azure, zawierającą hello klastrów usługi HDInsight.

    > [!IMPORTANT]
    > Witaj strukturalnych notesu przesyłania strumieniowego w tym przykładzie wymaga platforma Spark w usłudze HDInsight 3,6. Jeśli używasz starszej wersji platformy Spark w usłudze HDInsight, wystąpią błędy, korzystając z hello notesu.

2. Witaj Użyj następujących informacji toopopulate hello wpisy na powitania **wdrożenie niestandardowe** bloku:
   
    ![Niestandardowe wdrożenie usługi HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Grupa zasobów**: Utwórz grupę lub wybierz istniejący. Ta grupa zawiera hello klastra usługi HDInsight.

    * **Lokalizacja**: Wybierz lokalizację tooyou geograficznie Zamknij.

    * **Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello hello Spark i Kafka klastrów. Na przykład wprowadzenie **hdi** tworzy Spark klastra o nazwie spark hdi__ i Kafka klastra o nazwie **kafka hdi**.

    * **Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello hello Spark i Kafka klastrów.

    * **Hasło logowania klastra**: hello hasła użytkownika administratora klastrów platformy Spark i Kafka hello.

    * **Nazwa użytkownika SSH**: hello toocreate użytkownika SSH hello Spark i Kafka klastrów.

    * **Hasło SSH**: hello hasło użytkownika SSH hello hello Spark i Kafka klastrów.

3. Witaj odczytu **warunków i postanowień**, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.

4. Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**. Trwa około 20 minut toocreate hello klastrów.

Po utworzeniu zasobów hello jesteś bloku grupy zasobów toohello przekierowane.

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ spark** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu. Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.

## <a name="get-hello-kafka-brokers"></a>Pobierz hello Kafka brokerzy

Witaj kodu w tym przykładzie łączy toohello Kafka broker hosty w hello Kafka klastra. toofind hello Kafka brokera hostów, użyj hello poniższy przykład programu PowerShell lub Bash:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> W tym przykładzie oczekuje `$PASSWORD` toocontain hello hasło do logowania do klastra hello, i `$CLUSTERNAME` toocontain nazwę hello hello Kafka klastra.
>
> W tym przykładzie użyto hello [jq](https://stedolan.github.io/jq/) narzędzie tooparse danych poza hello dokumentu JSON.

Witaj danych wyjściowych jest podobne toohello następującego tekstu:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Zapisz te informacje, ponieważ jest używany w hello następujące części tego dokumentu.

## <a name="get-hello-notebooks"></a>Pobierz notesów hello

Kod Hello na przykład hello opisanych w niniejszym dokumencie jest dostępny w [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Przekaż notesów hello

Użyj poniższych kroków tooupload hello notesów z tooyour projektu hello Spark w klastrze usługi HDInsight hello:

1. W przeglądarce sieci web Połącz toohello notesu Jupyter w klastrze Spark. W hello następującego adresu URL, Zastąp `CLUSTERNAME` o nazwie hello Kafka klastra:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Po wyświetleniu monitu wprowadź hello logowania do klastra (admin) i hasło użyte podczas tworzenia klastra hello.

2. Hello górny po prawej stronie powitania strony, użyj funkcji hello __przekazać__ hello tooupload przycisk __strumienia-Tweetów-To_Kafka.ipynb__ klastra toohello plików. Wybierz __Otwórz__ toostart hello przekazywania.

    ![Użyj hello przekazywania przycisk tooselect i przekazać Notes](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Wybierz plik KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Znajdź hello __strumienia-Tweetów-To_Kafka.ipynb__ wpis na liście hello notesów i wybierz __przekazać__ przycisk obok siebie.

    ![Przekazywanie hello użyj przycisku obok hello KafkaStreaming.ipynb wpis tooupload go toohello notesu serwera](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Powtórz kroki od 1 do 3 tooload hello __Spark-strukturę-przesyłania strumieniowego-od-Kafka.ipynb__ notesu.

## <a name="load-tweets-into-kafka"></a>Ładowanie tweetów do Kafka

Po hello pliki zostały przekazane, wybierz hello __strumienia-Tweetów-To_Kafka.ipynb__ wpis tooopen hello notesu. Wykonaj kroki hello hello notesu tooload tweetów do Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Przy użyciu strukturalnych przesyłania strumieniowego Spark tweetów procesu

Wybierz hello z hello strony głównej notesu Jupyter __Spark-strukturę-przesyłania strumieniowego-od-Kafka.ipynb__ wpisu. Wykonaj kroki hello hello notesu tooload tweetów z Kafka przy użyciu strukturalnych przesyłania strumieniowego Spark.

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już toouse Spark strukturalnych przesyłania strumieniowego, zobacz temat powitania po więcej informacji na temat pracy z platformy Spark i Kafka toolearn dokumentów:

* [Jak toouse Spark przesyłania strumieniowego (DStream) z Kafka](hdinsight-apache-spark-with-kafka.md).
* [Rozpoczynać notesu Jupyter i Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)