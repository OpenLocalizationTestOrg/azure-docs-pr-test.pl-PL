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
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="b8c91-104">Wysoka dostępność danych dzięki platformie Apache Kafka (wersja zapoznawcza) w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b8c91-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="b8c91-105">Dowiedz się, jak skonfigurować repliki partycji dla tematów platformy Kafka w celu korzystania z bazowej konfiguracji regałów na sprzęt.</span><span class="sxs-lookup"><span data-stu-id="b8c91-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="b8c91-106">Ta konfiguracja zapewnia dostępność danych przechowywanych na platformie Apache Kafka w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b8c91-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="b8c91-107">Domeny błędów i domeny aktualizacji z platformą Kafka</span><span class="sxs-lookup"><span data-stu-id="b8c91-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="b8c91-108">Domena błędów to logiczna grupa bazowego sprzętu w centrum danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b8c91-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="b8c91-109">Wszystkie domeny błędów korzystają ze wspólnego źródła zasilania i przełącznika sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b8c91-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="b8c91-110">Maszyny wirtualne i dyski zarządzane, które implementują węzły w klastrze usługi HDInsight są rozdzielone między te domeny błędów.</span><span class="sxs-lookup"><span data-stu-id="b8c91-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="b8c91-111">Taka architektura ogranicza wpływ potencjalnych awarii sprzętu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="b8c91-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="b8c91-112">W każdym regionie świadczenia usługi Azure znajduje się określona liczba domen błędów.</span><span class="sxs-lookup"><span data-stu-id="b8c91-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="b8c91-113">Aby uzyskać listę domen i informacje o liczbie zawartych w nich domen błędów, zobacz dokument [Zestawy dostępności](../virtual-machines/linux/regions-and-availability.md#availability-sets).</span><span class="sxs-lookup"><span data-stu-id="b8c91-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8c91-114">Platforma Kafka nie uwzględnia domen błędów.</span><span class="sxs-lookup"><span data-stu-id="b8c91-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="b8c91-115">W przypadku utworzenia tematu na platformie Kafka wszystkie repliki partycji mogą być przechowywane w tej samej domenie błędów.</span><span class="sxs-lookup"><span data-stu-id="b8c91-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="b8c91-116">Aby rozwiązać ten problem, udostępniamy [narzędzie do ponownego równoważenia partycji platformy Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="b8c91-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="b8c91-117">Kiedy należy stosować ponowne równoważenie replik partycji</span><span class="sxs-lookup"><span data-stu-id="b8c91-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="b8c91-118">Aby zapewnić najwyższą dostępność danych na platformie Kafka, należy stosować ponowne równoważenie replik partycji dla tematu w następujących sytuacjach:</span><span class="sxs-lookup"><span data-stu-id="b8c91-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="b8c91-119">Po utworzeniu nowego tematu lub partycji</span><span class="sxs-lookup"><span data-stu-id="b8c91-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="b8c91-120">Po przeskalowaniu klastra w górę</span><span class="sxs-lookup"><span data-stu-id="b8c91-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="b8c91-121">Współczynnik replikacji</span><span class="sxs-lookup"><span data-stu-id="b8c91-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8c91-122">Zalecamy wybranie regionu świadczenia usługi Azure zawierającego trzy domeny błędów oraz użycie współczynnika replikacji o wartości 3.</span><span class="sxs-lookup"><span data-stu-id="b8c91-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="b8c91-123">Jeśli musisz wybrać region, który zawiera tylko dwie domeny błędów, użyj współczynnika replikacji o wartości 4, aby równomiernie rozłożyć repliki na dwie domeny błędów.</span><span class="sxs-lookup"><span data-stu-id="b8c91-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="b8c91-124">Aby zapoznać się z przykładem obejmującym tworzenie tematów i ustawianie współczynnika replikacji, zobacz dokument [Start with Kafka on HDInsight (Rozpoczynanie pracy z platformą Kafka w usłudze HDInsight)](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b8c91-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="b8c91-125">Jak zastosować ponowne równoważenie replik partycji</span><span class="sxs-lookup"><span data-stu-id="b8c91-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="b8c91-126">Aby ponownie zrównoważyć wybrane tematy, użyj [narzędzia do ponownego równoważenia partycji platformy Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="b8c91-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="b8c91-127">Narzędzie to należy uruchomić w sesji połączenia SSH z węzłem głównym klastra Kafka.</span><span class="sxs-lookup"><span data-stu-id="b8c91-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="b8c91-128">Aby uzyskać więcej informacji dotyczących nawiązywania połączenia z usługą HDInsight przy użyciu protokołu SSH, zobacz dokument [Używanie protokołu SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b8c91-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8c91-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8c91-129">Next steps</span></span>

* [<span data-ttu-id="b8c91-130">Scalability of Kafka on HDInsight (Skalowalność platformy Kafka w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b8c91-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="b8c91-131">Mirroring with Kafka on HDInsight (Dublowanie przy użyciu platformy Kafka w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b8c91-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)