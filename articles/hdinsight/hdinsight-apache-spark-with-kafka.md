---
title: "aaaApache Spark przesyłania strumieniowego z Kafka - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Spark Apache Spark toostream danych do lub wychodzący Kafka Apache przy użyciu DStreams. W tym przykładzie można przesyłać strumieniowo dane za pomocą notesu Jupyter z platformy Spark w usłudze HDInsight."
keywords: "przykład kafka, dozorcy kafka, spark, przesyłanie strumieniowe kafka, przesyłania strumieniowego przykład kafka spark"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Apache Spark przesyłania strumieniowego (DStream) przykład: Kafka (wersja zapoznawcza) w usłudze HDInsight

Dowiedz się, jak toouse Spark Apache Spark toostream danych do lub wychodzący Kafka Apache na HDInsight przy użyciu DStreams. W tym przykładzie użyto notesu Jupyter w klastrze Spark hello.
> [!NOTE]
> kroki Hello w tym dokumencie Tworzenie grupy zasobów platformy Azure, który zawiera zarówno Spark w usłudze HDInsight i Kafka w klastrze usługi HDInsight. Tych klastrów są oba znajdujących się w sieci wirtualnej platformy Azure, dzięki czemu hello toodirectly klastra Spark komunikować się z hello Kafka klastra.
>
> Po zakończeniu kroków hello w tym dokumencie, pamiętaj toodelete hello klastrów tooavoid nadmiarowe opłat.

## <a name="create-hello-clusters"></a>Tworzenie klastrów hello

Kafka Apache na HDInsight nie zapewnia dostępu toohello Kafka brokerzy za pośrednictwem hello publicznej sieci internet. Wszystko, co rozmów, muszą mieć tooKafka hello tej samej sieci wirtualnej platformy Azure jako węzły hello w hello Kafka klastra. W tym przykładzie zarówno hello Kafka, jak i klastry Spark znajdują się w sieci wirtualnej platformy Azure. Witaj poniższym diagramie przedstawiono sposób komunikacji przepływa między klastrami hello:

![Diagram klastry Spark i Kafka w sieci wirtualnej platformy Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Chociaż Kafka sam jest ograniczona toocommunication w ramach sieci wirtualnej hello, inne usługi w klastrze hello takich jak SSH i Ambari są dostępne za pośrednictwem hello internet. Aby uzyskać więcej informacji na powitania publicznego portów dostępnych z usługą HDInsight, zobacz [portów i identyfikatory URI używany przez HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Chociaż można utworzyć sieci wirtualnej platformy Azure, Kafka i Spark klastry ręcznie, jest łatwiejsze toouse szablonu usługi Azure Resource Manager. Użyj następujących hello kroki toodeploy sieci wirtualnej platformy Azure, Kafka, i Spark klastrów tooyour subskrypcji platformy Azure.

1. Użyj hello toosign przycisk w tooAzure i hello Otwórz szablon hello portalu Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Witaj szablonu usługi Azure Resource Manager znajduje się pod adresem **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > dostępność tooguarantee Kafka w usłudze HDInsight, klaster musi zawierać co najmniej trzech węzłów procesu roboczego. Ten szablon umożliwia tworzenie klastra Kafka, który zawiera trzy węzłów procesu roboczego.

    Ten szablon umożliwia tworzenie klastra usługi HDInsight 3,6 Kafka i Spark.

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

Po utworzeniu hello zasoby zostaną przekierowane tooa bloku hello grupę zasobów, która zawiera hello klastrów i pulpitu nawigacyjnego sieci web.

![Bloku grupy zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ spark** i **nazwę BAZOWĄ kafka**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu. Te nazwy można użyć w kolejnych krokach, podczas łączenia klastrów toohello.

## <a name="use-hello-notebooks"></a>Użyj notesów hello

Kod Hello na przykład hello opisanych w niniejszym dokumencie jest dostępny w [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Wykonaj kroki hello hello `README.md` pliku toocomplete w tym przykładzie.

## <a name="delete-hello-cluster"></a>Usuń klaster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Ponieważ hello kroków w tym dokumencie Tworzenie zarówno klastrów w hello tej samej grupy zasobów platformy Azure, można usunąć grupy zasobów hello w hello portalu Azure. Usuwanie grupy hello usuwa wszystkie zasoby utworzone, postępując w tym dokumencie, hello Azure Virtual Network i konto magazynu używane przez hello klastrów.

## <a name="next-steps"></a>Następne kroki

W tym przykładzie przedstawiono sposób toouse Spark tooread i zapisać tooKafka. Z Kafka, należy użyć następującego łącza toodiscover hello toowork inne sposoby:

* [Wprowadzenie do Apache Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md)
* [Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight](hdinsight-apache-storm-with-kafka.md)

