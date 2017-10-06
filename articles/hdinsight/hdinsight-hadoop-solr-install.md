---
title: "aaaUse akcji skryptu tooinstall Solr na klastra usługi Hadoop - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster toocustomize HDInsight z Solr za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="21c99-103">Zainstalować i używać Solr w klastrach HDInsight opartych na systemie Windows</span><span class="sxs-lookup"><span data-stu-id="21c99-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="21c99-104">Dowiedz się, jak klaster toocustomize HDInsight opartych na systemie Windows z Solr za pomocą akcji skryptu i jak toouse Solr toosearch danych.</span><span class="sxs-lookup"><span data-stu-id="21c99-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c99-105">Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="21c99-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="21c99-106">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="21c99-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="21c99-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="21c99-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="21c99-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="21c99-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="21c99-109">Dla informacji o korzystaniu z opartą na systemie Linux klastrem Solr, zobacz [instalacji i używania Solr w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="21c99-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="21c99-110">Solr można zainstalować w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*.</span><span class="sxs-lookup"><span data-stu-id="21c99-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="21c99-111">Przykładowy skrypt tooinstall Solr w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="21c99-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="21c99-112">Witaj przykładowy skrypt działa tylko w przypadku klastra HDInsight w wersji 3.1.</span><span class="sxs-lookup"><span data-stu-id="21c99-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="21c99-113">Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="21c99-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="21c99-114">używane w tym temacie program Hello przykładowy skrypt tworzy klaster Solr opartych na systemie Windows z określonej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="21c99-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="21c99-115">Jeśli chcesz tooconfigure hello Solr klaster z różnych kolekcji, odłamków, schematów, replik, itp., należy zmodyfikować skrypt hello i pliki binarne Solr odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="21c99-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="21c99-116">**Pokrewne artykuły**</span><span class="sxs-lookup"><span data-stu-id="21c99-116">**Related articles**</span></span>

* [<span data-ttu-id="21c99-117">Zainstalować i używać Solr w klastrach HDinsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="21c99-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="21c99-118">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c99-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="21c99-119">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="21c99-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="21c99-120">[Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="21c99-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="21c99-121">Co to jest Solr?</span><span class="sxs-lookup"><span data-stu-id="21c99-121">What is Solr?</span></span>
<span data-ttu-id="21c99-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> to platforma wyszukiwania przedsiębiorstwa, która umożliwia wydajne wyszukiwanie pełnotekstowe danych.</span><span class="sxs-lookup"><span data-stu-id="21c99-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="21c99-123">Gdy Hadoop umożliwia przechowywanie i zarządzania nimi czasach ogromne ilości danych, Apache Solr zapewnia możliwości wyszukiwania hello tooquickly pobierania hello danych.</span><span class="sxs-lookup"><span data-stu-id="21c99-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="21c99-124">Zainstaluj Solr przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="21c99-124">Install Solr using portal</span></span>
1. <span data-ttu-id="21c99-125">Rozpocznij tworzenie klastra przy użyciu hello **Utwórz niestandardowy** opcji, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="21c99-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="21c99-126">Na powitania **akcji skryptu** strony kreatora powitania kliknij przycisk **dodać akcję skryptu** tooprovide szczegółowych informacji o hello akcji skryptu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="21c99-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="21c99-127">![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize akcji skryptu Użyj klastra")</span><span class="sxs-lookup"><span data-stu-id="21c99-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="21c99-128">Właściwość</span><span class="sxs-lookup"><span data-stu-id="21c99-128">Property</span></span></th><th><span data-ttu-id="21c99-129">Wartość</span><span class="sxs-lookup"><span data-stu-id="21c99-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="21c99-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="21c99-130">Name</span></span></td>
            <td><span data-ttu-id="21c99-131">Określ nazwę hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="21c99-131">Specify a name for hello script action.</span></span> <span data-ttu-id="21c99-132">Na przykład <b>zainstalować Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="21c99-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="21c99-133">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="21c99-133">Script URI</span></span></td>
            <td><span data-ttu-id="21c99-134">Określ hello identyfikator URI (Uniform Resource) toohello skrypt, który jest wywołana toocustomize hello klastra.</span><span class="sxs-lookup"><span data-stu-id="21c99-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="21c99-135">Na przykład <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="21c99-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="21c99-136">Typ węzła</span><span class="sxs-lookup"><span data-stu-id="21c99-136">Node Type</span></span></td>
            <td><span data-ttu-id="21c99-137">Określ hello węzłów, na których uruchomiono hello dostosowywania skryptu.</span><span class="sxs-lookup"><span data-stu-id="21c99-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="21c99-138">Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>tylko węzłów procesu roboczego</b>.</span><span class="sxs-lookup"><span data-stu-id="21c99-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="21c99-139">Parametry</span><span class="sxs-lookup"><span data-stu-id="21c99-139">Parameters</span></span></td>
            <td><span data-ttu-id="21c99-140">Określ parametry hello, jeśli są wymagane przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="21c99-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="21c99-141">Hello skryptu tooinstall Solr nie wymaga żadnych parametrów, więc można to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="21c99-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="21c99-142">Więcej niż jeden tooinstall akcji skryptu można dodać wiele składników w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="21c99-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="21c99-143">Po dodaniu hello skryptów, kliknij przycisk toostart znacznikiem wyboru hello tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="21c99-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="21c99-144">Korzystanie z platformy Solr</span><span class="sxs-lookup"><span data-stu-id="21c99-144">Use Solr</span></span>
<span data-ttu-id="21c99-145">Musi rozpoczynać się od indeksowanie Solr z niektórych plików danych.</span><span class="sxs-lookup"><span data-stu-id="21c99-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="21c99-146">Następnie można zapytania wyszukiwania toorun Solr hello indeksowania danych.</span><span class="sxs-lookup"><span data-stu-id="21c99-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="21c99-147">Wykonaj następujące kroki toouse Solr w klastrze HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="21c99-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="21c99-148">**Za pomocą protokołu RDP (Remote Desktop) tooremote do klastra usługi HDInsight hello Solr zainstalowane**.</span><span class="sxs-lookup"><span data-stu-id="21c99-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="21c99-149">Z hello portalu Azure włączenie pulpitu zdalnego dla klastra hello, utworzone za pomocą Solr hello zainstalowane, a następnie zdalnego w klastrze.</span><span class="sxs-lookup"><span data-stu-id="21c99-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="21c99-150">Aby uzyskać instrukcje, zobacz [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="21c99-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="21c99-151">**Indeks Solr, przekazując pliki danych**.</span><span class="sxs-lookup"><span data-stu-id="21c99-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="21c99-152">Indeks Solr, możesz zaznaczyć dokumentów w nim, który może być konieczne toosearch na.</span><span class="sxs-lookup"><span data-stu-id="21c99-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="21c99-153">tooindex Solr, użyj tooremote RDP do klastra hello Przejdź toohello pulpitu, otwórz wiersz polecenia hello Hadoop i przejdź zbyt**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="21c99-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="21c99-154">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="21c99-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="21c99-155">Zostanie wyświetlony hello następujące dane wyjściowe w konsoli hello:</span><span class="sxs-lookup"><span data-stu-id="21c99-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="21c99-156">Narzędzie post.jar Hello indeksuje Solr z dwa dokumenty przykładowe, **solr.xml** i **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="21c99-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="21c99-157">Narzędzie post.jar Hello i hello przykładowe dokumenty są dostępne z instalacją Solr.</span><span class="sxs-lookup"><span data-stu-id="21c99-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="21c99-158">**Użyj hello Solr pulpitu nawigacyjnego toosearch w hello indeksowane dokumenty**.</span><span class="sxs-lookup"><span data-stu-id="21c99-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="21c99-159">W toohello sesji protokołu RDP hello HDInsight klastra, Otwórz program Internet Explorer i uruchomić pulpitu nawigacyjnego Solr hello na **http://headnodehost:8983/solr / #/**.</span><span class="sxs-lookup"><span data-stu-id="21c99-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="21c99-160">W lewym okienku hello z hello **selektora Core** listy rozwijanej, wybierz pozycję **collection1**, a w ramach, kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="21c99-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="21c99-161">Jako przykład tooselect i powrotu wszystkie dokumenty hello w Solr, zawierają hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="21c99-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="21c99-162">W hello **q** tekst wprowadź  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="21c99-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="21c99-163">Zwróci wszystkie dokumenty hello, które są indeksowane w Solr.</span><span class="sxs-lookup"><span data-stu-id="21c99-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="21c99-164">Jeśli chcesz toosearch dla określonego ciągu w dokumentach hello, można wprowadzić ten ciąg w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="21c99-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="21c99-165">W hello **wt** pole tekstowe, hello wybierz format danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="21c99-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="21c99-166">Domyślnie jest **json**.</span><span class="sxs-lookup"><span data-stu-id="21c99-166">Default is **json**.</span></span> <span data-ttu-id="21c99-167">Kliknij przycisk **wykonać kwerendy**.</span><span class="sxs-lookup"><span data-stu-id="21c99-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="21c99-168">![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "uruchomić kwerendę na pulpicie nawigacyjnym Solr")</span><span class="sxs-lookup"><span data-stu-id="21c99-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="21c99-169">dane wyjściowe Hello zwraca hello dwa dokumenty, używane do indeksowania Solr.</span><span class="sxs-lookup"><span data-stu-id="21c99-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="21c99-170">Witaj dane wyjściowe podobne hello następującego:</span><span class="sxs-lookup"><span data-stu-id="21c99-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="21c99-171">**Zalecane: Kopia zapasowa hello indeksowane dane z tooAzure Solr magazynu obiektów Blob skojarzony z klastrem usługi HDInsight hello**.</span><span class="sxs-lookup"><span data-stu-id="21c99-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="21c99-172">Dobrym rozwiązaniem należy wykonać kopię zapasową danych hello indeksowana z węzłów klastra Solr hello na magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="21c99-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="21c99-173">Wykonaj hello, więc po toodo kroki:</span><span class="sxs-lookup"><span data-stu-id="21c99-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="21c99-174">Z sesji protokołu RDP hello Otwórz program Internet Explorer i toohello punktu następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="21c99-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="21c99-175">Powinna zostać wyświetlona odpowiedź następująco:</span><span class="sxs-lookup"><span data-stu-id="21c99-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="21c99-176">W sesji zdalnej hello Przejdź zbyt {SOLR_HOME}\{kolekcji} \data.</span><span class="sxs-lookup"><span data-stu-id="21c99-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="21c99-177">Dla klastra hello utworzony za pośrednictwem hello przykładowy skrypt, należy to **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="21c99-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="21c99-178">W tej lokalizacji powinna zostać wyświetlona folder migawki utworzone z nazwą podobne**migawki.* Sygnatura czasowa***.</span><span class="sxs-lookup"><span data-stu-id="21c99-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="21c99-179">Folder migawki hello zip, a następnie przekaż tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="21c99-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="21c99-180">Z wiersza polecenia platformy Hadoop hello należy przejść toohello lokalizację folderu migawek hello za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="21c99-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="21c99-181">To polecenie kopie hello zbyt/przykład/dane migawki/w kontenerze hello w domyślnej hello magazynu konta skojarzonego z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="21c99-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="21c99-182">Zainstaluj Solr przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="21c99-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="21c99-183">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="21c99-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="21c99-184">Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21c99-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="21c99-185">Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="21c99-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="21c99-186">Zainstaluj Solr przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="21c99-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="21c99-187">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="21c99-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="21c99-188">Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="21c99-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="21c99-189">Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="21c99-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="21c99-190">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="21c99-190">See also</span></span>
* [<span data-ttu-id="21c99-191">Zainstalować i używać Solr w klastrach HDinsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="21c99-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="21c99-192">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21c99-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="21c99-193">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="21c99-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="21c99-194">[Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="21c99-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="21c99-195">[Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark.</span><span class="sxs-lookup"><span data-stu-id="21c99-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="21c99-196">[Zainstalować język R w klastrach HDInsight][hdinsight-install-r]: Akcja skryptu próbki o instalowaniu R.</span><span class="sxs-lookup"><span data-stu-id="21c99-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="21c99-197">[Zainstaluj w klastrach HDInsight Giraph](hdinsight-hadoop-giraph-install.md): Akcja skryptu próbki o instalowaniu Giraph.</span><span class="sxs-lookup"><span data-stu-id="21c99-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
