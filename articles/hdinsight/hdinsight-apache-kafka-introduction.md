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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="56e58-103">Wprowadzenie do platformy Apache Kafka w usłudze HDInsight (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="56e58-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="56e58-104">[Apache Kafka](https://kafka.apache.org) jest open source rozproszonej przesyłania strumieniowego platforma, która może być używany w czasie rzeczywistym toobuild przesyłania strumieniowego, potoki danych i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56e58-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="56e58-105">Kafka również zapewnia funkcje podobne tooa kolejki komunikatów, których można Publikuj i Subskrybuj toonamed strumieni danych brokera komunikatów.</span><span class="sxs-lookup"><span data-stu-id="56e58-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="56e58-106">Kafka w usłudze HDInsight zapewnia zarządzanych, wysokiej skalowalności i wysokiej dostępności usługi w chmurze Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="56e58-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="56e58-107">Dlaczego warto używać platformy Kafka w usłudze HDInsight?</span><span class="sxs-lookup"><span data-stu-id="56e58-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="56e58-108">Kafka zapewnia hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="56e58-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="56e58-109">Wzorzec przesyłania komunikatów publikowania / subskrypcji: Kafka udostępnia interfejs API producent publikowania rekordów tooa Kafka tematu.</span><span class="sxs-lookup"><span data-stu-id="56e58-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="56e58-110">powitania klienta interfejsu API jest używany podczas subskrybowania tooa tematu.</span><span class="sxs-lookup"><span data-stu-id="56e58-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="56e58-111">Przetwarzanie strumienia: platforma Kafka jest często używana z systemem Apache Storm lub platformą Spark na potrzeby przetwarzania strumienia w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="56e58-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="56e58-112">Kafka 0.10.0.0 (usługi HDInsight w wersji 3.5) wprowadzono interfejs API przesyłania strumieniowego, umożliwiający toobuild przesyłania strumieniowego rozwiązań bez konieczności Storm i Spark.</span><span class="sxs-lookup"><span data-stu-id="56e58-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="56e58-113">Skalowanie w poziomie: Kafka partycje strumieni w węzłach klastra usługi HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="56e58-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="56e58-114">Procesy użytkownika może być skojarzony z równoważeniem obciążenia tooprovide pojedynczych partycji, podczas używania rekordów.</span><span class="sxs-lookup"><span data-stu-id="56e58-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="56e58-115">Dostarczanie w kolejności: w ramach każdej partycji rekordy są przechowywane w strumieniu hello w kolejności hello, że zostały odebrane.</span><span class="sxs-lookup"><span data-stu-id="56e58-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="56e58-116">Skojarzenie jednego procesu klienta z jedną partycją pozwala zagwarantować, że rekordy są przetwarzane we właściwej kolejności.</span><span class="sxs-lookup"><span data-stu-id="56e58-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="56e58-117">Odpornej na uszkodzenia: Partycji mogą być replikowane między węzłami tooprovide odporność na uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="56e58-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="56e58-118">Integracja z usługą Azure zarządzanych dysków: zarządzane dyski zapewnia większej skali i przepływności hello dysków używanych przez hello maszyny wirtualne w klastrze HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="56e58-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="56e58-119">Zarządzane dyski są domyślnie włączone dla Kafka w usłudze HDInsight i hello liczba dysków używanych w każdym węźle można skonfigurować podczas tworzenia usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="56e58-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="56e58-120">Aby uzyskać więcej informacji o usłudze Managed Disks, zobacz artykuł [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56e58-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="56e58-121">Aby uzyskać informacje dotyczące konfigurowania usługi Managed Disks na platformie Kafka w usłudze HDInsight, zobacz artykuł [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Zwiększanie skalowalności platformy Kafka w usłudze HDInsight).</span><span class="sxs-lookup"><span data-stu-id="56e58-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="56e58-122">Przypadki zastosowań</span><span class="sxs-lookup"><span data-stu-id="56e58-122">Use cases</span></span>

* <span data-ttu-id="56e58-123">**Obsługa wiadomości**: ponieważ obsługuje on hello komunikatów publikowania / subskrypcji, Kafka jest często używana jako brokera komunikatów.</span><span class="sxs-lookup"><span data-stu-id="56e58-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="56e58-124">**Monitorowanie aktywności**: ponieważ Kafka umożliwia rejestrowanie w kolejności rekordów, można go tootrack używane i ponownie utwórz działań.</span><span class="sxs-lookup"><span data-stu-id="56e58-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="56e58-125">Mogą to być na przykład działania użytkownika w witrynie sieci Web lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56e58-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="56e58-126">**Agregacja**: przy użyciu przetwarzania strumienia, możesz agregować informacji z różnych strumieni toocombine i scentralizowanie hello informacji w danych operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="56e58-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="56e58-127">**Przekształcanie**: przetwarzanie strumienia umożliwia łączenie i urozmaicanie danych z wielu tematów wejściowych w formie tematów wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="56e58-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56e58-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56e58-128">Next steps</span></span>

<span data-ttu-id="56e58-129">Użyj następujących hello łączy toolearn jak toouse Kafka Apache na HDInsight:</span><span class="sxs-lookup"><span data-stu-id="56e58-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="56e58-130">Wprowadzenie do platformy Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="56e58-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="56e58-131">Użyj toocreate MirrorMaker repliki Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="56e58-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="56e58-132">Używanie systemu Apache Storm z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="56e58-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="56e58-133">Używanie platformy Apache Spark z platformą Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="56e58-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="56e58-134">Łączenie się tooKafka za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="56e58-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
