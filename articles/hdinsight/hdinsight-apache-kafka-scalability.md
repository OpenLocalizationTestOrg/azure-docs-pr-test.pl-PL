---
title: "Zwiększenie skalowalności klastra Apache Kafka — Azure HDInsight | Microsoft Docs"
description: "Dowiedz się, jak skonfigurować zarządzane dyski klastra Apache Kafka w usłudze Azure HDInsight w celu zwiększenia skalowalności."
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
ms.openlocfilehash: 880a186a3d9a23b013294b0121e8265270d160cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="d72f3-103">Konfigurowanie magazynu i skalowalności klastra Apache Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d72f3-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="d72f3-104">Dowiedz się, jak skonfigurować liczbę zarządzanych dysków używanych przez klaster Apache Kafka w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d72f3-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="d72f3-105">Platforma Kafka w usłudze HDInsight używa dysku lokalnego maszyn wirtualnych w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d72f3-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="d72f3-106">Ze względu na duże obciążenie we/wy platformy Kafka usługa [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) jest używana do zapewnienia wysokiej przepływności i zwiększenia miejsca do magazynowania w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="d72f3-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="d72f3-107">Jeśli platforma Kafka korzysta z tradycyjnych wirtualnych dysków twardych (VHD), rozmiar każdego węzła nie przekracza 1 TB.</span><span class="sxs-lookup"><span data-stu-id="d72f3-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="d72f3-108">W przypadku dysków zarządzanych można użyć wielu dysków, aby osiągnąć 16 TB pamięci dla każdego węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d72f3-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="d72f3-109">Poniższy diagram przedstawia porównanie platformy Kafka w usłudze HDInsight przed użyciem dysków zarządzanych i platformy Kafka w usłudze HDInsight z dyskami zarządzanymi:</span><span class="sxs-lookup"><span data-stu-id="d72f3-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagram przedstawiający porównanie platformy Kafka w usłudze HDInsight z użyciem jednego wirtualnego dysku twardego na maszynę wirtualną oraz z użyciem wielu dysków zarządzanych na maszynę wirtualną](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="d72f3-111">Konfigurowanie dysków zarządzanych: witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d72f3-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="d72f3-112">Aby zapoznać się z typowymi czynnościami tworzenia klastra przy użyciu witryny, wykonaj kroki opisane w temacie [Tworzenie klastra usługi HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d72f3-112">Follow the steps in the [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="d72f3-113">Nie wykonuj procesu tworzenia w witrynie.</span><span class="sxs-lookup"><span data-stu-id="d72f3-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="d72f3-114">W bloku __Rozmiar klastra__ określ liczbę dysków w polu __Liczba dysków na węzeł procesu roboczego__.</span><span class="sxs-lookup"><span data-stu-id="d72f3-114">From the __Cluster size__ blade, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d72f3-115">Można wybrać typ dysku zarządzanego __Standardowy__ (HDD) lub __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="d72f3-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="d72f3-116">Dyski w warstwie Premium są używane przez maszyny wirtualne serii DS i GS.</span><span class="sxs-lookup"><span data-stu-id="d72f3-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="d72f3-117">Wszystkie pozostałe typy maszyn wirtualnych korzystają z dysków standardowych.</span><span class="sxs-lookup"><span data-stu-id="d72f3-117">All other VM types use standard.</span></span>

    ![Obraz bloku rozmiaru klastra z wyróżnionymi dyskami dla każdego węzła procesu roboczego](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="d72f3-119">Konfigurowanie dysków zarządzanych: szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d72f3-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="d72f3-120">Aby kontrolować liczbę dysków używanych przez węzły procesu roboczego w klastrze Kafka, użyj następującej sekcji szablonu:</span><span class="sxs-lookup"><span data-stu-id="d72f3-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="d72f3-121">Kompletny szablon przedstawiający sposób konfigurowania dysków zarządzanych można znaleźć pod adresem [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="d72f3-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d72f3-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d72f3-122">Next steps</span></span>

<span data-ttu-id="d72f3-123">Więcej informacji na temat pracy z klastrem Kafka w usłudze HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="d72f3-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="d72f3-124">Tworzenie repliki platformy Kafka w usłudze HDInsight przy użyciu narzędzia MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="d72f3-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="d72f3-125">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d72f3-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="d72f3-126">Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d72f3-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="d72f3-127">Nawiązywanie połączenia z platformą Kafka za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d72f3-127">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="d72f3-128">Blog usługi HDInsight zawierający informacje na temat dysków zarządzanych na platformie Kafka</span><span class="sxs-lookup"><span data-stu-id="d72f3-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)