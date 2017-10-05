---
title: "Użyj Apache Phoenix i SQuirreL z HBase - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą Apache Phoenix w usłudze HDInsight oraz jak zainstalować i skonfigurować SQuirreL na stacji roboczej do nawiązania połączenia klastra HBase w usłudze HDInsight."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="48c74-103">Apache Phoenix za pomocą klastrów HBase opartych na systemie Linux w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="48c74-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="48c74-104">Dowiedz się, jak używać [Apache Phoenix](http://phoenix.apache.org/) w usłudze HDInsight i sposobu użycia SQLLine.</span><span class="sxs-lookup"><span data-stu-id="48c74-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="48c74-105">Aby uzyskać więcej informacji na temat Phoenix, zobacz [Phoenix w ciągu 15 minut lub mniej](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="48c74-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="48c74-106">Dla gramatyki Phoenix [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="48c74-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="48c74-107">Aby uzyskać informacje o wersji Phoenix w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="48c74-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="48c74-108">Użyj SQLLine</span><span class="sxs-lookup"><span data-stu-id="48c74-108">Use SQLLine</span></span>
<span data-ttu-id="48c74-109">[SQLLine](http://sqlline.sourceforge.net/) to narzędzie wiersza polecenia do wykonania SQL.</span><span class="sxs-lookup"><span data-stu-id="48c74-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48c74-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="48c74-110">Prerequisites</span></span>
<span data-ttu-id="48c74-111">Przed użyciem SQLLine, należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="48c74-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="48c74-112">**Klaster HBase w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="48c74-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="48c74-113">Aby uzyskać informacje dotyczące udostępniania bazy danych HBase klastra, zobacz [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="48c74-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="48c74-114">**Połącz się z klastrem HBase przy użyciu protokołu remote desktop protocol**.</span><span class="sxs-lookup"><span data-stu-id="48c74-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="48c74-115">Aby uzyskać instrukcje, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu portalu Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="48c74-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="48c74-116">Po podłączeniu do klastra HBase, należy połączyć się z jedną dozorcy.</span><span class="sxs-lookup"><span data-stu-id="48c74-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="48c74-117">Każdy klaster usługi HDInsight ma trzy dozorcy.</span><span class="sxs-lookup"><span data-stu-id="48c74-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="48c74-118">**Aby dowiedzieć się, dozorcy nazwy hosta**</span><span class="sxs-lookup"><span data-stu-id="48c74-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="48c74-119">Otwórz Ambari, przechodząc do **https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="48c74-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="48c74-120">Wprowadź nazwę protokołu HTTP (klaster) użytkownika i hasło do logowania.</span><span class="sxs-lookup"><span data-stu-id="48c74-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="48c74-121">Kliknij przycisk **dozorcy** z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="48c74-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="48c74-122">Zobacz trzy **serwera dozorcy** na liście.</span><span class="sxs-lookup"><span data-stu-id="48c74-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="48c74-123">Kliknij jeden z **serwera dozorcy** na liście.</span><span class="sxs-lookup"><span data-stu-id="48c74-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="48c74-124">W okienku podsumowania znaleźć **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="48c74-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="48c74-125">Jest on podobny do *zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="48c74-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="48c74-126">**Aby użyć SQLLine**</span><span class="sxs-lookup"><span data-stu-id="48c74-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="48c74-127">Połącz z klastrem przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="48c74-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="48c74-128">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="48c74-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="48c74-129">Z SSH uruchom następujące polecenia, aby uruchomić SQLLine:</span><span class="sxs-lookup"><span data-stu-id="48c74-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="48c74-130">Uruchom następujące polecenia, aby utworzyć tabelę HBase i wstawić dane:</span><span class="sxs-lookup"><span data-stu-id="48c74-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="48c74-131">Aby uzyskać więcej informacji, zobacz [ręcznego SQLLine](http://sqlline.sourceforge.net/#manual) i [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="48c74-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48c74-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48c74-132">Next steps</span></span>
<span data-ttu-id="48c74-133">W tym artykule ma przedstawiono sposób użycia Apache Phoenix w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="48c74-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="48c74-134">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="48c74-134">To learn more, see:</span></span>

* <span data-ttu-id="48c74-135">[Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.</span><span class="sxs-lookup"><span data-stu-id="48c74-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="48c74-136">[Udostępnianie klastrów HBase w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]: Z integracji sieci wirtualnej klastrów HBase można wdrożyć w tej samej sieci wirtualnej jako aplikacje, dzięki czemu aplikacje mogą komunikować się z bazą danych HBase bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="48c74-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="48c74-137">[Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md): Dowiedz się, jak skonfigurować replikację bazy danych HBase między dwoma centrami danych Azure.</span><span class="sxs-lookup"><span data-stu-id="48c74-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="48c74-138">[Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]: Dowiedz się, jak to zrobić w czasie rzeczywistym [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) dużych danych przy użyciu bazy danych HBase w klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="48c74-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
