---
title: "aaaApache Kafka zwiększenia skali - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure zarządzane dyski klastra Apache Kafka w usłudze Azure HDInsight tooincrease skalowalności."
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Konfigurowanie magazynu i skalowalności klastra Apache Kafka w usłudze HDInsight

Dowiedz się, jak używane tooconfigure hello liczba dysków zarządzanych przez Kafka Apache na HDInsight.

Kafka w usłudze HDInsight używa dysku lokalnym hello hello maszyn wirtualnych w klastrze usługi HDInsight hello. Ponieważ Kafka jest ciężka, bardzo We/Wy [dysków zarządzanych Azure](../virtual-machines/windows/managed-disks-overview.md) jest używane tooprovide wysokiej przepływności i zapewniają więcej pamięci masowej w każdym węźle. Jeśli tradycyjnych wirtualnych dysków twardych (VHD) są używane do Kafka, każdy węzeł jest ograniczona too1 TB. Z zarządzanego dysków, można użyć wielu dysków tooachieve 16 TB dla każdego węzła w klastrze hello.

Witaj następujący diagram zawiera porównanie Kafka w usłudze HDInsight przed dysków zarządzanych i Kafka w usłudze HDInsight z dyskami zarządzanego:

![Diagram przedstawiający porównanie platformy Kafka w usłudze HDInsight z użyciem jednego wirtualnego dysku twardego na maszynę wirtualną oraz z użyciem wielu dysków zarządzanych na maszynę wirtualną](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Konfigurowanie dysków zarządzanych: witryna Azure Portal

1. Wykonaj kroki hello hello [tworzenia klastra usługi HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello wspólne kroki toocreate klastra przy użyciu portalu hello. Nie ukończyć powitalnych tworzenia portalu.

2. Z hello __rozmiar klastra__ bloku, użyj hello __dyski dla każdego węzła procesu roboczego__ pola tooconfigure hello liczba dysków.

    > [!NOTE]
    > Witaj dysku zarządzanego typu może być albo __standardowe__ (HDD) lub __Premium__ (SSD). Dyski w warstwie Premium są używane przez maszyny wirtualne serii DS i GS. Wszystkie pozostałe typy maszyn wirtualnych korzystają z dysków standardowych.

    ![Obraz powitania bloku rozmiar klastra z dyskami hello na wyróżnione węzła procesu roboczego](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Konfigurowanie dysków zarządzanych: szablon usługi Resource Manager

toocontrol hello liczba dysków używanych przez hello węzłów procesu roboczego w klastrze Kafka hello Użyj następujących sekcji hello szablonu:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Możesz znaleźć pełną szablonu, który demonstruje sposób tooconfigure zarządzania dyskami [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat pracy z Kafka w usłudze HDInsight Zobacz hello w następujących dokumentach:

* [Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Blog usługi HDInsight zawierający informacje na temat dysków zarządzanych na platformie Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)