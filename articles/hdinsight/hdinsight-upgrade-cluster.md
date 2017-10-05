---
title: "Uaktualnienia klastra usługi HDInsight do nowszej wersji-Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uaktualnić klaster usługi HDInsight do nowszej wersji."
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
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="49f15-103">Uaktualnij do nowszej wersji klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="49f15-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="49f15-104">Aby móc korzystać z najnowszych funkcji usługi HDInsight, zaleca się, że klastry usługi HDInsight można uaktualnić do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="49f15-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="49f15-105">Postępuj zgodnie z poniższych wytycznych, aby uaktualnić Twoje HDInsight cluster wersji.</span><span class="sxs-lookup"><span data-stu-id="49f15-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="49f15-106">Klastry usługi HDInsight w wersji 3.2 lub 3.3 zbliża się Data wycofania.</span><span class="sxs-lookup"><span data-stu-id="49f15-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="49f15-107">Aby uzyskać informacji na temat obsługiwanych wersji usługi hdinsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="49f15-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="49f15-108">Zadania uaktualniania</span><span class="sxs-lookup"><span data-stu-id="49f15-108">Upgrade tasks</span></span>
<span data-ttu-id="49f15-109">Poniżej przedstawiono przepływ pracy do uaktualnienia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="49f15-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Diagram przepływu pracy uaktualniania](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="49f15-111">Przeczytaj każdej sekcji tego dokumentu, aby zrozumieć zmiany, które mogą być wymagane w przypadku uaktualniania z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="49f15-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="49f15-112">Tworzenie klastra jako środowiska gwarancji testu/jakości.</span><span class="sxs-lookup"><span data-stu-id="49f15-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="49f15-113">Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [informacje o sposobie tworzenia klastrów usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="49f15-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="49f15-114">Skopiuj zadania istniejące źródła danych i wychwytywanie do nowego środowiska.</span><span class="sxs-lookup"><span data-stu-id="49f15-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="49f15-115">Zobacz [kopiowania danych do środowiska testowego](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="49f15-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="49f15-116">Należy przeprowadzić testy weryfikacji, aby upewnić się, że zadaniach działać zgodnie z oczekiwaniami w nowym klastrze.</span><span class="sxs-lookup"><span data-stu-id="49f15-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="49f15-117">Po upewnieniu się, że wszystko działa zgodnie z oczekiwaniami, należy zaplanować przestój do migracji.</span><span class="sxs-lookup"><span data-stu-id="49f15-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="49f15-118">Podczas tego przestojów wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="49f15-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="49f15-119">Utwórz kopię zapasową przejściowej danych przechowywanych lokalnie w węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="49f15-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="49f15-120">Jeśli na przykład dane przechowywane bezpośrednio na węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="49f15-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="49f15-121">Usuwanie istniejącego klastra.</span><span class="sxs-lookup"><span data-stu-id="49f15-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="49f15-122">Tworzenia klastra w tej samej podsieci sieci Wirtualnej z najnowszą (lub obsługiwanych) wersja usługi HDI przy użyciu tego samego magazynu danych domyślne używane poprzedniego klastra.</span><span class="sxs-lookup"><span data-stu-id="49f15-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="49f15-123">Dzięki temu nowego klastra kontynuować pracę z istniejących danych produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="49f15-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="49f15-124">Importuj wszystkie przejściowej dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="49f15-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="49f15-125">Uruchom zadania/Kontynuuj przetwarzanie przy użyciu nowego klastra.</span><span class="sxs-lookup"><span data-stu-id="49f15-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49f15-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49f15-126">Next Steps</span></span>
* [<span data-ttu-id="49f15-127">Informacje o sposobie tworzenia klastrów usługi HDInsight opartej na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="49f15-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="49f15-128">Połączenie do usługi HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="49f15-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="49f15-129">Zarządzanie klastrem opartych na systemie Linux przy użyciu narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="49f15-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

