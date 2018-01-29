---
title: Dziennika analizy dla Apache Kafka - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak używać usługi Operations Management Suite do analizowania dzienników z klastra Apache Kafka w usłudze Azure HDInsight."
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
ms.date: 11/07/2017
ms.author: larryfr
ms.openlocfilehash: 440133da32f4565aa247b273984b3affe18379ec
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
---
# <a name="analyze-logs-for-apache-kafka-on-hdinsight"></a>Analizowanie dzienników dla Kafka Apache na HDInsight

Jak analizować dzienniki generowane przez Kafka Apache na HDInsight przy użyciu programu Microsoft Operations Management Suite.

## <a name="enable-oms-for-kafka"></a>Włącz OMS dla Kafka

Procedurę włączania analizy dzienników dla usługi HDInsight są takie same dla wszystkich klastrów usługi HDInsight. Aby zrozumieć, jak utworzyć i skonfigurować wymagane usługi, użyj następujących łączy:

1. Tworzenie obszaru roboczego analizy dzienników. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z obszaru roboczego analizy dzienników](https://docs.microsoft.com/azure/log-analytics) dokumentu.

2. Utwórz Kafka w klastrze usługi HDInsight. Aby uzyskać więcej informacji, zobacz [rozpoczynać Kafka Apache na HDInsight](apache-kafka-get-started.md) dokumentu.

3. Konfigurowanie klastra Kafka w analizy dzienników. Aby uzyskać więcej informacji, zobacz [analizy dzienników używany do monitorowania usługi HDInsight](../hdinsight-hadoop-oms-log-analytics-tutorial.md) dokumentu.

    > [!NOTE]
    > Można również skonfigurować klaster, aby użyć analizy dzienników przy użyciu `Enable-AzureRmHDInsightOperationsManagementSuite` polecenia cmdlet. To polecenie cmdlet wymaga następujących informacji:
    >
    > * Nazwa klastra usługi HDInsight.
    > * Identyfikator obszaru roboczego analizy dzienników. Identyfikator obszaru roboczego można znaleźć w obszarze roboczym pakietu OMS obszaru roboczego analizy dzienników.
    > * Klucz podstawowy połączenia OMS. Aby znaleźć klucz podstawowy, wybierz wystąpienie analizy dziennika, a następnie __portalu OMS__. Wybierz z portalu OMS __ustawienia__, __połączonych źródeł__, a następnie __serwerów z systemem Linux__.


> [!IMPORTANT]
> może potrwać około 20 minut, zanim dane są dostępne dla analizy dzienników.

## <a name="query-logs"></a>Dzienniki zapytania

1. Z [portalu Azure](https://portal.azure.com), wybierz obszar roboczy analizy dzienników.

2. Wybierz __dziennika wyszukiwania__. W tym miejscu można wyszukiwać dane zbierane z Kafka. Poniżej przedstawiono niektóre przykładowe wyszukiwania:

    * Użycie dysku:`Type=Perf ObjectName="Logical Disk" (CounterName="Free Megabytes")  InstanceName="_Total" Computer='hn*-*' or Computer='wn*-*' | measure avg(CounterValue) by   Computer interval 1HOUR`
    * Użycie procesora CPU:`Type:Perf CounterName="% Processor Time" InstanceName="_Total" Computer='hn*-*' or Computer='wn*-*' | measure avg(CounterValue) by Computer interval 1HOUR`
    * Wiadomości przychodzących na sekundę:`Type=metrics_kafka_CL ClusterName_s="your_kafka_cluster_name" InstanceName_s="kafka-BrokerTopicMetrics-MessagesInPerSec-Count" | measure avg(kafka_BrokerTopicMetrics_MessagesInPerSec_Count_value_d) by HostName_s interval 1HOUR`
    * Przychodzące bajty na sekundę:`Type=metrics_kafka_CL HostName_s="wn0-kafka" InstanceName_s="kafka-BrokerTopicMetrics-BytesInPerSec-Count" | measure avg(kafka_BrokerTopicMetrics_BytesInPerSec_Count_value_d) interval 1HOUR`
    * Wychodzące bajty na sekundę:`Type=metrics_kafka_CL ClusterName_s="your_kafka_cluster_name" InstanceName_s="kafka-BrokerTopicMetrics-BytesOutPerSec-Count" |  measure avg(kafka_BrokerTopicMetrics_BytesOutPerSec_Count_value_d) interval 1HOUR`

    > [!IMPORTANT]
    > Zastąp wartości zapytania Twoje informacje dotyczące klastra. Na przykład `ClusterName_s` należy ustawić nazwę klastra. `HostName_s`należy ustawić nazwę domeny z węzłem procesu roboczego w klastrze.

    Możesz też wprowadzić `*` aby wyszukać wszystkie typy rejestrowanych. Obecnie dostępne dla zapytań są następujące dzienniki:

    | Typ dziennika | Opis |
    | ---- | ---- |
    | Dziennik\_kafkaserver\_CL | Server.log brokera Kafka |
    | Dziennik\_kafkacontroller\_CL | Controller.log brokera Kafka |
    | metryki\_kafka\_CL | Metryki Kafka JMX |

    ![Obraz wyszukiwania użycia procesora CPU](./media/apache-kafka-log-analytics-operations-management/kafka-cpu-usage.png)
 
 ## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących analizy dzienników, zobacz [Rozpoczynanie pracy z obszaru roboczego analizy dzienników](../../log-analytics/log-analytics-get-started.md) dokumentu.

Aby uzyskać więcej informacji na temat pracy z Kafka można znaleźć w następujących dokumentach:

 * [Dublowany Kafka między klastrami usługi HDInsight](apache-kafka-mirroring.md)
 * [Zwiększenie skalowalności Kafka w usłudze HDInsight](apache-kafka-scalability.md)
 * [Użyj przesyłania strumieniowego (DStreams) z Kafka Spark](../hdinsight-apache-spark-with-kafka.md)
 * [Korzystanie z platformy Spark strukturę przesyłania strumieniowego z Kafka](../hdinsight-apache-kafka-spark-structured-streaming.md)