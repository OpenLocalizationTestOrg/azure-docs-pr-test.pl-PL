---
title: aaaUse Apache Phoenix i SQuirreL z HBase - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Apache Phoenix w usłudze HDInsight i w jaki sposób tooinstall i skonfigurować SQuirreL na stacji roboczej klastra HBase tooan tooconnect w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="8ba16-103">Apache Phoenix za pomocą klastrów HBase opartych na systemie Linux w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ba16-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="8ba16-104">Dowiedz się, jak toouse [Apache Phoenix](http://phoenix.apache.org/) w usłudze HDInsight i w jaki sposób toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="8ba16-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="8ba16-105">Aby uzyskać więcej informacji na temat Phoenix, zobacz [Phoenix w ciągu 15 minut lub mniej](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="8ba16-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="8ba16-106">Aby hello Phoenix gramatyki, zobacz [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="8ba16-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="8ba16-107">Aby hello Phoenix informacje o wersji w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8ba16-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="8ba16-108">Użyj SQLLine</span><span class="sxs-lookup"><span data-stu-id="8ba16-108">Use SQLLine</span></span>
<span data-ttu-id="8ba16-109">[SQLLine](http://sqlline.sourceforge.net/) jest tooexecute narzędzia wiersza polecenia SQL.</span><span class="sxs-lookup"><span data-stu-id="8ba16-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8ba16-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ba16-110">Prerequisites</span></span>
<span data-ttu-id="8ba16-111">Przed użyciem SQLLine, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="8ba16-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="8ba16-112">**Klaster HBase w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8ba16-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="8ba16-113">Aby uzyskać informacje dotyczące udostępniania bazy danych HBase klastra, zobacz [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="8ba16-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="8ba16-114">**Połącz klaster HBase toohello za pośrednictwem protokołu RDP hello**.</span><span class="sxs-lookup"><span data-stu-id="8ba16-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="8ba16-115">Aby uzyskać instrukcje, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="8ba16-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="8ba16-116">Po ustanowieniu połączenia klastra HBase tooan należy tooone tooconnect z hello dozorcy.</span><span class="sxs-lookup"><span data-stu-id="8ba16-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="8ba16-117">Każdy klaster usługi HDInsight ma trzy dozorcy.</span><span class="sxs-lookup"><span data-stu-id="8ba16-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="8ba16-118">**toofind limit nazwy hosta dozorcy hello**</span><span class="sxs-lookup"><span data-stu-id="8ba16-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="8ba16-119">Otwórz Ambari, przeglądając zbyt**https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="8ba16-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="8ba16-120">Wprowadź HTTP (klaster) hello toologin nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="8ba16-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="8ba16-121">Kliknij przycisk **dozorcy** z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="8ba16-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="8ba16-122">Zobacz trzy **serwera dozorcy** na liście.</span><span class="sxs-lookup"><span data-stu-id="8ba16-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="8ba16-123">Kliknij jeden z hello **serwera dozorcy** na liście.</span><span class="sxs-lookup"><span data-stu-id="8ba16-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="8ba16-124">W okienku podsumowania hello Znajdź hello **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="8ba16-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="8ba16-125">Podobnie jest zbyt*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="8ba16-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="8ba16-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="8ba16-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="8ba16-127">Połącz toohello klastra przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="8ba16-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="8ba16-128">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8ba16-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8ba16-129">Z SSH uruchom następujące polecenia toorun SQLLine hello:</span><span class="sxs-lookup"><span data-stu-id="8ba16-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="8ba16-130">Uruchom następujące polecenia toocreate hello tabeli HBase i wstawić dane:</span><span class="sxs-lookup"><span data-stu-id="8ba16-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="8ba16-131">Aby uzyskać więcej informacji, zobacz [ręcznego SQLLine](http://sqlline.sourceforge.net/#manual) i [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="8ba16-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ba16-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ba16-132">Next steps</span></span>
<span data-ttu-id="8ba16-133">W tym artykule wiesz już, jak toouse Apache Phoenix w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ba16-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="8ba16-134">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="8ba16-134">toolearn more, see:</span></span>

* <span data-ttu-id="8ba16-135">[Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.</span><span class="sxs-lookup"><span data-stu-id="8ba16-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="8ba16-136">[Udostępnianie klastrów HBase w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]: Z integracji sieci wirtualnej klastrów HBase może być wdrożone toohello sam wirtualnych sieci jako aplikacje tak aplikacje mogą komunikować się z HBase bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="8ba16-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="8ba16-137">[Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md): Dowiedz się, jak replikacji bazy danych HBase tooconfigure między dwoma centrami danych Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba16-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="8ba16-138">[Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]: Dowiedz się, jak toodo w czasie rzeczywistym [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) dużych danych przy użyciu bazy danych HBase w klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ba16-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
