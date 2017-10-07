---
title: "aaaAn wprowadzenie tooApache Kafka w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o Kafka Apache na HDInsight: co to jest, działanie i gdzie toofind przykłady i pierwsze kroki informacji."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Wprowadzenie do platformy Apache Kafka w usłudze HDInsight (wersja zapoznawcza)

[Apache Kafka](https://kafka.apache.org) jest open source rozproszonej przesyłania strumieniowego platforma, która może być używany w czasie rzeczywistym toobuild przesyłania strumieniowego, potoki danych i aplikacji. Kafka również zapewnia funkcje podobne tooa kolejki komunikatów, których można Publikuj i Subskrybuj toonamed strumieni danych brokera komunikatów. Kafka w usłudze HDInsight zapewnia zarządzanych, wysokiej skalowalności i wysokiej dostępności usługi w chmurze Microsoft Azure hello.

## <a name="why-use-kafka-on-hdinsight"></a>Dlaczego warto używać platformy Kafka w usłudze HDInsight?

Kafka zapewnia hello następujące funkcje:

* Wzorzec przesyłania komunikatów publikowania / subskrypcji: Kafka udostępnia interfejs API producent publikowania rekordów tooa Kafka tematu. powitania klienta interfejsu API jest używany podczas subskrybowania tooa tematu.

* Przetwarzanie strumienia: platforma Kafka jest często używana z systemem Apache Storm lub platformą Spark na potrzeby przetwarzania strumienia w czasie rzeczywistym. Kafka 0.10.0.0 (usługi HDInsight w wersji 3.5) wprowadzono interfejs API przesyłania strumieniowego, umożliwiający toobuild przesyłania strumieniowego rozwiązań bez konieczności Storm i Spark.

* Skalowanie w poziomie: Kafka partycje strumieni w węzłach klastra usługi HDInsight hello hello. Procesy użytkownika może być skojarzony z równoważeniem obciążenia tooprovide pojedynczych partycji, podczas używania rekordów.

* Dostarczanie w kolejności: w ramach każdej partycji rekordy są przechowywane w strumieniu hello w kolejności hello, że zostały odebrane. Skojarzenie jednego procesu klienta z jedną partycją pozwala zagwarantować, że rekordy są przetwarzane we właściwej kolejności.

* Odpornej na uszkodzenia: Partycji mogą być replikowane między węzłami tooprovide odporność na uszkodzenia.

* Integracja z usługą Azure zarządzanych dysków: zarządzane dyski zapewnia większej skali i przepływności hello dysków używanych przez hello maszyny wirtualne w klastrze HDInsight hello.

    Zarządzane dyski są domyślnie włączone dla Kafka w usłudze HDInsight i hello liczba dysków używanych w każdym węźle można skonfigurować podczas tworzenia usługi HDInsight. Aby uzyskać więcej informacji o usłudze Managed Disks, zobacz artykuł [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).

    Aby uzyskać informacje dotyczące konfigurowania usługi Managed Disks na platformie Kafka w usłudze HDInsight, zobacz artykuł [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Zwiększanie skalowalności platformy Kafka w usłudze HDInsight).

## <a name="use-cases"></a>Przypadki zastosowań

* **Obsługa wiadomości**: ponieważ obsługuje on hello komunikatów publikowania / subskrypcji, Kafka jest często używana jako brokera komunikatów.

* **Monitorowanie aktywności**: ponieważ Kafka umożliwia rejestrowanie w kolejności rekordów, można go tootrack używane i ponownie utwórz działań. Mogą to być na przykład działania użytkownika w witrynie sieci Web lub aplikacji.

* **Agregacja**: przy użyciu przetwarzania strumienia, możesz agregować informacji z różnych strumieni toocombine i scentralizowanie hello informacji w danych operacyjnych.

* **Przekształcanie**: przetwarzanie strumienia umożliwia łączenie i urozmaicanie danych z wielu tematów wejściowych w formie tematów wyjściowych.

## <a name="next-steps"></a>Następne kroki

Użyj następujących hello łączy toolearn jak toouse Kafka Apache na HDInsight:

* [Wprowadzenie do platformy Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md)

* [Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight](hdinsight-apache-spark-with-kafka.md)

* [Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
