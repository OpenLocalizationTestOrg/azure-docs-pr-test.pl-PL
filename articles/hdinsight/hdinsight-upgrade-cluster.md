---
title: "wersja nowsza tooa klastra usługi HDInsight aaaUpgrade-Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooUpgrade HDInsight cluster tooa nowszej wersji."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="215e5-103">Uaktualnij tooa klastra usługi HDInsight w nowszej wersji</span><span class="sxs-lookup"><span data-stu-id="215e5-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="215e5-104">Zaletą tootake hello najnowszych funkcji usługi HDInsight, zaleca się klastrów usługi HDInsight toolatest uaktualnionej wersji.</span><span class="sxs-lookup"><span data-stu-id="215e5-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="215e5-105">Wykonaj hello poniżej tooupgrade wskazówki dotyczące Twojej wersji klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="215e5-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="215e5-106">Klastry usługi HDInsight w wersji 3.2 lub 3.3 zbliża się Data wycofania.</span><span class="sxs-lookup"><span data-stu-id="215e5-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="215e5-107">Aby uzyskać informacji na temat obsługiwanych wersji usługi hdinsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="215e5-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="215e5-108">Zadania uaktualniania</span><span class="sxs-lookup"><span data-stu-id="215e5-108">Upgrade tasks</span></span>
<span data-ttu-id="215e5-109">Witaj przepływu pracy tooupgrade klastra usługi HDInsight ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="215e5-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Diagram przepływu pracy uaktualniania](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="215e5-111">Przeczytaj sekcję tego dokumentu toounderstand zmiany, które mogą być wymagane w przypadku uaktualniania z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="215e5-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="215e5-112">Tworzenie klastra jako środowiska gwarancji testu/jakości.</span><span class="sxs-lookup"><span data-stu-id="215e5-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="215e5-113">Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [Dowiedz się, jak toocreate opartych na systemie Linux klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="215e5-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="215e5-114">Kopia istniejącego zadania, źródła danych i wychwytywanie toohello nowego środowiska.</span><span class="sxs-lookup"><span data-stu-id="215e5-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="215e5-115">Zobacz [tooTest skopiować dane środowisko](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="215e5-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="215e5-116">Sprawdzania poprawności testowania toomake się upewnić, że zadaniach działać zgodnie z oczekiwaniami w nowym klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="215e5-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="215e5-117">Po upewnieniu się, że wszystko działa zgodnie z oczekiwaniami, należy zaplanować przestój hello migracji.</span><span class="sxs-lookup"><span data-stu-id="215e5-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="215e5-118">Podczas tego przestoju hello następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="215e5-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="215e5-119">Utwórz kopię zapasową przejściowej dane przechowywane lokalnie na hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="215e5-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="215e5-120">Jeśli na przykład dane przechowywane bezpośrednio na węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="215e5-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="215e5-121">Usuń hello istniejącego klastra.</span><span class="sxs-lookup"><span data-stu-id="215e5-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="215e5-122">Tworzenie klastra w hello hello tej samej sieci Wirtualnej podsieci o najnowszych (lub obsługiwanych) HDI wersji przy użyciu tego samego magazynu danych domyślne hello poprzedniego klastra używane.</span><span class="sxs-lookup"><span data-stu-id="215e5-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="215e5-123">Dzięki temu hello nowego klastra toocontinue rywalizacja istniejących danych produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="215e5-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="215e5-124">Importuj wszystkie przejściowej dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="215e5-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="215e5-125">Uruchom zadania/Kontynuuj przetwarzania przy użyciu hello nowego klastra.</span><span class="sxs-lookup"><span data-stu-id="215e5-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="215e5-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="215e5-126">Next Steps</span></span>
* [<span data-ttu-id="215e5-127">Dowiedz się, jak toocreate opartych na systemie Linux klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="215e5-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="215e5-128">Połącz tooHDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="215e5-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="215e5-129">Zarządzanie klastrem opartych na systemie Linux przy użyciu narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="215e5-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

