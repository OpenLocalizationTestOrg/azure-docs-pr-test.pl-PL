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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="2880e-103">Konfigurowanie magazynu i skalowalności klastra Apache Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2880e-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="2880e-104">Dowiedz się, jak używane tooconfigure hello liczba dysków zarządzanych przez Kafka Apache na HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2880e-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="2880e-105">Kafka w usłudze HDInsight używa dysku lokalnym hello hello maszyn wirtualnych w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2880e-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="2880e-106">Ponieważ Kafka jest ciężka, bardzo We/Wy [dysków zarządzanych Azure](../virtual-machines/windows/managed-disks-overview.md) jest używane tooprovide wysokiej przepływności i zapewniają więcej pamięci masowej w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="2880e-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="2880e-107">Jeśli tradycyjnych wirtualnych dysków twardych (VHD) są używane do Kafka, każdy węzeł jest ograniczona too1 TB.</span><span class="sxs-lookup"><span data-stu-id="2880e-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="2880e-108">Z zarządzanego dysków, można użyć wielu dysków tooachieve 16 TB dla każdego węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="2880e-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="2880e-109">Witaj następujący diagram zawiera porównanie Kafka w usłudze HDInsight przed dysków zarządzanych i Kafka w usłudze HDInsight z dyskami zarządzanego:</span><span class="sxs-lookup"><span data-stu-id="2880e-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagram przedstawiający porównanie platformy Kafka w usłudze HDInsight z użyciem jednego wirtualnego dysku twardego na maszynę wirtualną oraz z użyciem wielu dysków zarządzanych na maszynę wirtualną](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="2880e-111">Konfigurowanie dysków zarządzanych: witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2880e-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="2880e-112">Wykonaj kroki hello hello [tworzenia klastra usługi HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello wspólne kroki toocreate klastra przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="2880e-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="2880e-113">Nie ukończyć powitalnych tworzenia portalu.</span><span class="sxs-lookup"><span data-stu-id="2880e-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="2880e-114">Z hello __rozmiar klastra__ bloku, użyj hello __dyski dla każdego węzła procesu roboczego__ pola tooconfigure hello liczba dysków.</span><span class="sxs-lookup"><span data-stu-id="2880e-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2880e-115">Witaj dysku zarządzanego typu może być albo __standardowe__ (HDD) lub __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="2880e-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="2880e-116">Dyski w warstwie Premium są używane przez maszyny wirtualne serii DS i GS.</span><span class="sxs-lookup"><span data-stu-id="2880e-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="2880e-117">Wszystkie pozostałe typy maszyn wirtualnych korzystają z dysków standardowych.</span><span class="sxs-lookup"><span data-stu-id="2880e-117">All other VM types use standard.</span></span>

    ![Obraz powitania bloku rozmiar klastra z dyskami hello na wyróżnione węzła procesu roboczego](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="2880e-119">Konfigurowanie dysków zarządzanych: szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2880e-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="2880e-120">toocontrol hello liczba dysków używanych przez hello węzłów procesu roboczego w klastrze Kafka hello Użyj następujących sekcji hello szablonu:</span><span class="sxs-lookup"><span data-stu-id="2880e-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="2880e-121">Możesz znaleźć pełną szablonu, który demonstruje sposób tooconfigure zarządzania dyskami [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="2880e-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2880e-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2880e-122">Next steps</span></span>

<span data-ttu-id="2880e-123">Aby uzyskać więcej informacji na temat pracy z Kafka w usłudze HDInsight Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="2880e-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="2880e-124">Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2880e-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="2880e-125">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2880e-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="2880e-126">Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2880e-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="2880e-127">Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2880e-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="2880e-128">Blog usługi HDInsight zawierający informacje na temat dysków zarządzanych na platformie Kafka</span><span class="sxs-lookup"><span data-stu-id="2880e-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)