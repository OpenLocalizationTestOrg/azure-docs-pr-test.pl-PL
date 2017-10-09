---
title: "aaaUse interakcyjne Hive w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse interakcyjne (gałąź na LLAP) Hive w usłudze HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="453d5-103">Użyj interaktywnego Hive w usłudze HDInsight (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="453d5-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="453d5-104">Interakcyjne gałęzi rejestru ()</span><span class="sxs-lookup"><span data-stu-id="453d5-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="453d5-105">[Na żywo długich i procesu](https://cwiki.apache.org/confluence/display/Hive/LLAP)) jest nowy HDInsight [typ klastra](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="453d5-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="453d5-106">Interakcyjne Hive umożliwia buforowanie pamięci sprawia, że zapytań programu Hive bardziej interakcyjne i szybsze.</span><span class="sxs-lookup"><span data-stu-id="453d5-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="453d5-107">Ta nowa funkcja sprawia, że HDInsight jedną hello na świecie większości wydajność, elastyczne i otwórz rozwiązania typu Big Data w chmurze hello z pamięci podręcznej w pamięci (przy użyciu Hive i Spark) i zaawansowane analizy za pośrednictwem głęboką integrację z usługami R.</span><span class="sxs-lookup"><span data-stu-id="453d5-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="453d5-108">klastra interakcyjne Hive Hello różni się od hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="453d5-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="453d5-109">Zawiera on tylko hello Hive usługi.</span><span class="sxs-lookup"><span data-stu-id="453d5-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="453d5-110">MapReduce, Pig, Sqoop, Oozie i innych usług, są usuwani ze tego typu klastra wkrótce.</span><span class="sxs-lookup"><span data-stu-id="453d5-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="453d5-111">Hello usługi Hive w klastrze interakcyjne Hive hello jest dostępny tylko za pośrednictwem hello widoku Hive narzędzia Ambari, Beeline i ODBC programu Hive.</span><span class="sxs-lookup"><span data-stu-id="453d5-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="453d5-112">Nie są dostępne za pośrednictwem konsoli Hive, Templeton, wiersza polecenia platformy Azure i programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="453d5-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="453d5-113">Tworzenie klastra interakcyjne Hive</span><span class="sxs-lookup"><span data-stu-id="453d5-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="453d5-114">Interakcyjne gałęzi klastra jest obsługiwana tylko w klastrach opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="453d5-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="453d5-115">Aby uzyskać informacje dotyczące tworzenia klastrów usługi HDInsight, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="453d5-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="453d5-116">Wykonanie gałąź z gałęzi interakcyjne</span><span class="sxs-lookup"><span data-stu-id="453d5-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="453d5-117">Istnieją różne opcje, w jaki sposób można wykonywać zapytań programu Hive:</span><span class="sxs-lookup"><span data-stu-id="453d5-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="453d5-118">Uruchom Hive za pomocą hello widoku Hive narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="453d5-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="453d5-119">Witaj informacji o korzystaniu z Hive View hello, zobacz [hello użyj widoku Hive z usługą Hadoop w usłudze HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="453d5-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="453d5-120">Uruchom przy użyciu Beeline gałęzi</span><span class="sxs-lookup"><span data-stu-id="453d5-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="453d5-121">Hello informacji na temat używania Beeline w usłudze HDInsight, zobacz [używanie Hive z usługą Hadoop w usłudze HDInsight z Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="453d5-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="453d5-122">Możesz użyć Beeline hello headnode lub węzłem krawędzi puste.</span><span class="sxs-lookup"><span data-stu-id="453d5-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="453d5-123">Zaleca się użycie Beeline z węzłem krawędzi puste.</span><span class="sxs-lookup"><span data-stu-id="453d5-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="453d5-124">Informacje dotyczące tworzenia klastra usługi HDInsight z pustym edgenode, zobacz [użycia węzłów pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="453d5-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="453d5-125">Uruchom gałęzi przy użyciu Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="453d5-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="453d5-126">Hello informacji na temat używania ODBC programu Hive, zobacz [tooHadoop łączenie programu Excel z sterownik Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="453d5-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="453d5-127">**Witaj toofind JDBC ciąg połączenia:**</span><span class="sxs-lookup"><span data-stu-id="453d5-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="453d5-128">Logowanie przy użyciu następującego adresu URL hello tooAmbari: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="453d5-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="453d5-129">Kliknij przycisk **Hive** z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="453d5-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="453d5-130">Kliknij przycisk hello wyróżnione ikona toocopy hello URL:</span><span class="sxs-lookup"><span data-stu-id="453d5-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![JDBC LLAP interakcyjne Hive HDInsight Hadoop](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="453d5-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="453d5-132">See also</span></span>
* <span data-ttu-id="453d5-133">[Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Dowiedz się, jak klastrów toocreate interakcyjne Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="453d5-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="453d5-134">[Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight z Beeline](hdinsight-hadoop-use-hive-beeline.md): Dowiedz się, jak zapytań Hive toosubmit Beeline toouse.</span><span class="sxs-lookup"><span data-stu-id="453d5-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="453d5-135">[Połącz Excel tooHadoop sterownik Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md): Dowiedz się, jak tooconnect tooHive programu Excel.</span><span class="sxs-lookup"><span data-stu-id="453d5-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

