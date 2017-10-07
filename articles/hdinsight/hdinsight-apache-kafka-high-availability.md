---
title: "dostępność aaaHigh z Kafka Apache - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooensure wysokiej dostępności z Kafka Apache na Azure HDInsight. Dowiedz się, jak toorebalance partycji replik w Kafka, dzięki czemu są one w domenach różnych usterek w ramach hello region platformy Azure, który zawiera usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Wysoka dostępność danych dzięki platformie Apache Kafka (wersja zapoznawcza) w usłudze HDInsight

Dowiedz się, jak tooconfigure replik partycji dla Kafka tematy tootake zaletą używany sprzęt stojak konfiguracji. Ta konfiguracja zapewnia dostępność hello danych przechowywanych w Kafka Apache na HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Domeny błędów i domeny aktualizacji z platformą Kafka

Domena błędów to logiczna grupa bazowego sprzętu w centrum danych platformy Azure. Wszystkie domeny błędów korzystają ze wspólnego źródła zasilania i przełącznika sieciowego. maszyny wirtualne Hello i zarządzanych dysków, które implementuje hello węzłów w klastrze usługi HDInsight są rozproszone na tych domen błędów. Taka architektura ogranicza hello potencjalny wpływ awarii sprzętu fizycznego.

W każdym regionie świadczenia usługi Azure znajduje się określona liczba domen błędów. Listę domen i hello liczba domen błędów, które zawierają, zobacz hello [zestawy dostępności](../virtual-machines/linux/regions-and-availability.md#availability-sets) dokumentacji.

> [!IMPORTANT]
> Platforma Kafka nie uwzględnia domen błędów. Podczas tworzenia tematu w Kafka wszystkich replik partycji mogą być przechowywane w hello tej samej domenie błędów. toosolve tego problemu firma Microsoft udostępnia hello [narzędzia Zrównoważ partycji Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Gdy toorebalance partycji repliki

tooensure hello najwyższą dostępność danych Kafka, powinien rebalance hello replik partycji dla tematu na powitania po razy:

* Po utworzeniu nowego tematu lub partycji

* Po przeskalowaniu klastra w górę

## <a name="replication-factor"></a>Współczynnik replikacji

> [!IMPORTANT]
> Zalecamy wybranie regionu świadczenia usługi Azure zawierającego trzy domeny błędów oraz użycie współczynnika replikacji o wartości 3.

Jeśli należy użyć innego regionu, który zawiera tylko dwa domen błędów, należy równomiernie Użyj współczynnika replikacji 4 replik hello toospread na powitania dwóch domen błędów.

Na przykład tworzenie tematów i ustawienie hello replikacji współczynnik Zobacz hello [rozpoczynać Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md) dokumentu.

## <a name="how-toorebalance-partition-replicas"></a>Jak toorebalance partycji repliki

Użyj hello [narzędzia Zrównoważ partycji Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance wybrane tematy. To narzędzie musi być był uruchamiany z SSH sesji toohello węzła głównego klastra Kafka.

Aby uzyskać więcej informacji na łączenie tooHDInsight przy użyciu protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

## <a name="next-steps"></a>Następne kroki

* [Scalability of Kafka on HDInsight (Skalowalność platformy Kafka w usłudze HDInsight)](hdinsight-apache-kafka-scalability.md)
* [Mirroring with Kafka on HDInsight (Dublowanie przy użyciu platformy Kafka w usłudze HDInsight)](hdinsight-apache-kafka-mirroring.md)