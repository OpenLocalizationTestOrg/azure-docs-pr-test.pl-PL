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
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="78bf8-104">Wysoka dostępność danych dzięki platformie Apache Kafka (wersja zapoznawcza) w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="78bf8-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="78bf8-105">Dowiedz się, jak tooconfigure replik partycji dla Kafka tematy tootake zaletą używany sprzęt stojak konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="78bf8-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="78bf8-106">Ta konfiguracja zapewnia dostępność hello danych przechowywanych w Kafka Apache na HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78bf8-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="78bf8-107">Domeny błędów i domeny aktualizacji z platformą Kafka</span><span class="sxs-lookup"><span data-stu-id="78bf8-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="78bf8-108">Domena błędów to logiczna grupa bazowego sprzętu w centrum danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78bf8-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="78bf8-109">Wszystkie domeny błędów korzystają ze wspólnego źródła zasilania i przełącznika sieciowego.</span><span class="sxs-lookup"><span data-stu-id="78bf8-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="78bf8-110">maszyny wirtualne Hello i zarządzanych dysków, które implementuje hello węzłów w klastrze usługi HDInsight są rozproszone na tych domen błędów.</span><span class="sxs-lookup"><span data-stu-id="78bf8-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="78bf8-111">Taka architektura ogranicza hello potencjalny wpływ awarii sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="78bf8-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="78bf8-112">W każdym regionie świadczenia usługi Azure znajduje się określona liczba domen błędów.</span><span class="sxs-lookup"><span data-stu-id="78bf8-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="78bf8-113">Listę domen i hello liczba domen błędów, które zawierają, zobacz hello [zestawy dostępności](../virtual-machines/linux/regions-and-availability.md#availability-sets) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="78bf8-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78bf8-114">Platforma Kafka nie uwzględnia domen błędów.</span><span class="sxs-lookup"><span data-stu-id="78bf8-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="78bf8-115">Podczas tworzenia tematu w Kafka wszystkich replik partycji mogą być przechowywane w hello tej samej domenie błędów.</span><span class="sxs-lookup"><span data-stu-id="78bf8-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="78bf8-116">toosolve tego problemu firma Microsoft udostępnia hello [narzędzia Zrównoważ partycji Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="78bf8-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="78bf8-117">Gdy toorebalance partycji repliki</span><span class="sxs-lookup"><span data-stu-id="78bf8-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="78bf8-118">tooensure hello najwyższą dostępność danych Kafka, powinien rebalance hello replik partycji dla tematu na powitania po razy:</span><span class="sxs-lookup"><span data-stu-id="78bf8-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="78bf8-119">Po utworzeniu nowego tematu lub partycji</span><span class="sxs-lookup"><span data-stu-id="78bf8-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="78bf8-120">Po przeskalowaniu klastra w górę</span><span class="sxs-lookup"><span data-stu-id="78bf8-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="78bf8-121">Współczynnik replikacji</span><span class="sxs-lookup"><span data-stu-id="78bf8-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78bf8-122">Zalecamy wybranie regionu świadczenia usługi Azure zawierającego trzy domeny błędów oraz użycie współczynnika replikacji o wartości 3.</span><span class="sxs-lookup"><span data-stu-id="78bf8-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="78bf8-123">Jeśli należy użyć innego regionu, który zawiera tylko dwa domen błędów, należy równomiernie Użyj współczynnika replikacji 4 replik hello toospread na powitania dwóch domen błędów.</span><span class="sxs-lookup"><span data-stu-id="78bf8-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="78bf8-124">Na przykład tworzenie tematów i ustawienie hello replikacji współczynnik Zobacz hello [rozpoczynać Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="78bf8-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="78bf8-125">Jak toorebalance partycji repliki</span><span class="sxs-lookup"><span data-stu-id="78bf8-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="78bf8-126">Użyj hello [narzędzia Zrównoważ partycji Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance wybrane tematy.</span><span class="sxs-lookup"><span data-stu-id="78bf8-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="78bf8-127">To narzędzie musi być był uruchamiany z SSH sesji toohello węzła głównego klastra Kafka.</span><span class="sxs-lookup"><span data-stu-id="78bf8-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="78bf8-128">Aby uzyskać więcej informacji na łączenie tooHDInsight przy użyciu protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="78bf8-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78bf8-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78bf8-129">Next steps</span></span>

* [<span data-ttu-id="78bf8-130">Scalability of Kafka on HDInsight (Skalowalność platformy Kafka w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="78bf8-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="78bf8-131">Mirroring with Kafka on HDInsight (Dublowanie przy użyciu platformy Kafka w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="78bf8-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)