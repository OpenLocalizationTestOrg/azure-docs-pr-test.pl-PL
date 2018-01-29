---
title: "Wysoka dostępność dzięki platformie Apache Kafka — usługa Azure HDInsight | Microsoft Docs"
description: "Dowiedz się, jak zapewnić wysoką dostępność dzięki platformie Apache Kafka w usłudze Azure HDInsight. Dowiedz się, jak przeprowadzić ponowne równoważenie replik partycji na platformie Kafka, tak aby znajdowały się one w różnych domenach błędów w regionie świadczenia usługi Azure, który udostępnia usługę HDInsight."
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
ms.date: 11/07/2017
ms.author: larryfr
ms.openlocfilehash: f7a4245435093358cac567cf08c8ce3979371c04
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-on-hdinsight"></a>Wysoka dostępność danych dzięki platformie Apache Kafka w usłudze HDInsight

Dowiedz się, jak skonfigurować repliki partycji dla tematów platformy Kafka w celu korzystania z bazowej konfiguracji regałów na sprzęt. Ta konfiguracja zapewnia dostępność danych przechowywanych na platformie Apache Kafka w usłudze HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Domeny błędów i domeny aktualizacji z platformą Kafka

Domena błędów to logiczna grupa bazowego sprzętu w centrum danych platformy Azure. Wszystkie domeny błędów korzystają ze wspólnego źródła zasilania i przełącznika sieciowego. Maszyny wirtualne i dyski zarządzane, które implementują węzły w klastrze usługi HDInsight są rozdzielone między te domeny błędów. Taka architektura ogranicza wpływ potencjalnych awarii sprzętu fizycznego.

W każdym regionie świadczenia usługi Azure znajduje się określona liczba domen błędów. Aby uzyskać listę domen i informacje o liczbie zawartych w nich domen błędów, zobacz dokument [Zestawy dostępności](../../virtual-machines/windows/regions-and-availability.md#availability-sets).

> [!IMPORTANT]
> Platforma Kafka nie uwzględnia domen błędów. W przypadku utworzenia tematu na platformie Kafka wszystkie repliki partycji mogą być przechowywane w tej samej domenie błędów. Aby rozwiązać ten problem, udostępniamy [narzędzie do ponownego równoważenia partycji platformy Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-to-rebalance-partition-replicas"></a>Kiedy należy stosować ponowne równoważenie replik partycji

Aby zapewnić najwyższą dostępność danych na platformie Kafka, należy stosować ponowne równoważenie replik partycji dla tematu w następujących sytuacjach:

* Po utworzeniu nowego tematu lub partycji

* Po przeskalowaniu klastra w górę

## <a name="replication-factor"></a>Współczynnik replikacji

> [!IMPORTANT]
> Zalecamy wybranie regionu świadczenia usługi Azure zawierającego trzy domeny błędów oraz użycie współczynnika replikacji o wartości 3.

Jeśli musisz wybrać region, który zawiera tylko dwie domeny błędów, użyj współczynnika replikacji o wartości 4, aby równomiernie rozłożyć repliki na dwie domeny błędów.

Aby zapoznać się z przykładem obejmującym tworzenie tematów i ustawianie współczynnika replikacji, zobacz dokument [Start with Kafka on HDInsight (Rozpoczynanie pracy z platformą Kafka w usłudze HDInsight)](apache-kafka-get-started.md).

## <a name="how-to-rebalance-partition-replicas"></a>Jak zastosować ponowne równoważenie replik partycji

Aby ponownie zrównoważyć wybrane tematy, użyj [narzędzia do ponownego równoważenia partycji platformy Kafka](https://github.com/hdinsight/hdinsight-kafka-tools). Narzędzie to należy uruchomić w sesji połączenia SSH z węzłem głównym klastra Kafka.

Aby uzyskać więcej informacji dotyczących nawiązywania połączenia z usługą HDInsight przy użyciu protokołu SSH, zobacz dokument [Używanie protokołu SSH z usługą HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="next-steps"></a>Następne kroki

* [Scalability of Kafka on HDInsight (Skalowalność platformy Kafka w usłudze HDInsight)](apache-kafka-scalability.md)
* [Mirroring with Kafka on HDInsight (Dublowanie przy użyciu platformy Kafka w usłudze HDInsight)](apache-kafka-mirroring.md)