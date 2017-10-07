---
title: "aaaUse akcji skryptu tooinstall Solr w usłudze HDInsight opartych na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Solr na platformie Hadoop, HDInsight opartych na systemie Linux klastrów za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="34b05-103">Zainstalować i używać Solr w klastrach HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="34b05-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="34b05-104">Dowiedz się, jak tooinstall Solr w usłudze Azure HDInsight za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="34b05-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="34b05-105">Solr to platforma wyszukiwania zaawansowanego i zapewnia możliwości wyszukiwania na poziomie przedsiębiorstwa na danych zarządzanych przez usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="34b05-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="34b05-106">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="34b05-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="34b05-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="34b05-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="34b05-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="34b05-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34b05-109">Witaj przykładowy skrypt jest używany w tym dokumencie instaluje Solr 4.9 z określonej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34b05-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="34b05-110">Chcąc tooconfigure hello Solr klaster z różnych kolekcji, odłamków, schematów, replik, itp., należy zmodyfikować skrypt hello i Solr plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="34b05-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="34b05-111"><a name="whatis"></a>Co to jest Solr</span><span class="sxs-lookup"><span data-stu-id="34b05-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="34b05-112">[Apache Solr](http://lucene.apache.org/solr/features.html) to platforma wyszukiwania przedsiębiorstwa, która umożliwia wydajne wyszukiwanie pełnotekstowe danych.</span><span class="sxs-lookup"><span data-stu-id="34b05-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="34b05-113">Gdy Hadoop umożliwia przechowywanie i zarządzania nimi czasach ogromne ilości danych, Apache Solr zapewnia możliwości wyszukiwania hello tooquickly pobierania hello danych.</span><span class="sxs-lookup"><span data-stu-id="34b05-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="34b05-114">Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34b05-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="34b05-115">Niestandardowe składniki, takie jak Solr, odbierania toohelp uzasadnione ekonomicznie Obsługa toofurther należy rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="34b05-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="34b05-116">Pomoc techniczna firmy Microsoft nie może być możliwe tooresolve problemów ze składnikami niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="34b05-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="34b05-117">Aby uzyskać pomoc może być konieczne tooengage hello typu open source społeczności.</span><span class="sxs-lookup"><span data-stu-id="34b05-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="34b05-118">Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="34b05-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="34b05-119">Jakie skrypt hello wykonuje</span><span class="sxs-lookup"><span data-stu-id="34b05-119">What hello script does</span></span>

<span data-ttu-id="34b05-120">Ten skrypt powoduje powitania po klastra usługi HDInsight toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="34b05-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="34b05-121">Instaluje Solr 4.9 do`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="34b05-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="34b05-122">Tworzy użytkownika, **solrusr**, która jest używana toorun hello Solr usługi</span><span class="sxs-lookup"><span data-stu-id="34b05-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="34b05-123">Ustawia **solruser** jako właściciel hello`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="34b05-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="34b05-124">Dodaje [Upstart](http://upstart.ubuntu.com/) konfiguracji, które jest uruchamiane automatycznie Solr.</span><span class="sxs-lookup"><span data-stu-id="34b05-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="34b05-125"><a name="install"></a>Zainstaluj Solr za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="34b05-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="34b05-126">Przykładowy skrypt tooinstall Solr w klastrze usługi HDInsight jest dostępna w hello w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="34b05-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="34b05-127">toocreate klaster ma zainstalowany Solr, użyj hello etapami hello [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="34b05-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="34b05-128">Podczas procesu tworzenia hello Użyj hello następujące kroki tooinstall Solr:</span><span class="sxs-lookup"><span data-stu-id="34b05-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="34b05-129">Z hello __klastra Podsumowanie__ bloku, settings__ select__Advanced, następnie __skryptu akcji__.</span><span class="sxs-lookup"><span data-stu-id="34b05-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="34b05-130">Użyj hello następujące informacje toopopulate hello formularza:</span><span class="sxs-lookup"><span data-stu-id="34b05-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="34b05-131">**Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="34b05-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="34b05-132">**Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="34b05-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="34b05-133">**HEAD**: Zaznaczenie tego pola wyboru</span><span class="sxs-lookup"><span data-stu-id="34b05-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="34b05-134">**Proces ROBOCZY**: Zaznaczenie tego pola wyboru</span><span class="sxs-lookup"><span data-stu-id="34b05-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="34b05-135">**DOZORCY**: Sprawdź tooinstall tej opcji w węźle dozorcy hello</span><span class="sxs-lookup"><span data-stu-id="34b05-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="34b05-136">**Parametry**: pozostaw to pole puste</span><span class="sxs-lookup"><span data-stu-id="34b05-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="34b05-137">U dołu hello hello **skryptu akcje** bloku, użyj hello **wybierz** przycisk toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34b05-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="34b05-138">Na koniec użyj hello **dalej** toohello tooreturn przycisk __podsumowanie klastra__</span><span class="sxs-lookup"><span data-stu-id="34b05-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="34b05-139">Z hello __klastra Podsumowanie__ wybierz pozycję __Utwórz__ toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="34b05-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="34b05-140"><a name="usesolr"></a>Jak używać Solr w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="34b05-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34b05-141">Procedura Hello w tej sekcji przedstawia podstawowe funkcje Solr.</span><span class="sxs-lookup"><span data-stu-id="34b05-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="34b05-142">Aby uzyskać więcej informacji na temat używania Solr, zobacz hello [lokacji Apache Solr](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="34b05-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="34b05-143">Dane indeksu</span><span class="sxs-lookup"><span data-stu-id="34b05-143">Index data</span></span>

<span data-ttu-id="34b05-144">Użyj hello następujące kroki tooadd przykładowe dane tooSolr, a następnie wykonasz zapytania:</span><span class="sxs-lookup"><span data-stu-id="34b05-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="34b05-145">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="34b05-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="34b05-146">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="34b05-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="34b05-147">Kroki opisane w dalszej części tego dokumentu, użyj protokołu SSL tunelu tooconnect toohello Solr interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="34b05-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="34b05-148">toouse tych kroków, musisz ustanowić SSL tunelowania, a następnie skonfiguruj toouse Twojego przeglądarki go.</span><span class="sxs-lookup"><span data-stu-id="34b05-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="34b05-149">Aby uzyskać więcej informacji, zobacz hello [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="34b05-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="34b05-150">Użyj hello następujące polecenia toohave Solr indeksu przykładowe dane:</span><span class="sxs-lookup"><span data-stu-id="34b05-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="34b05-151">Witaj następujące dane wyjściowe są zwracane toohello konsoli:</span><span class="sxs-lookup"><span data-stu-id="34b05-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="34b05-152">Witaj `post.jar` narzędzie dodaje hello **solr.xml** i **monitor.xml** dokumenty toohello indeksu.</span><span class="sxs-lookup"><span data-stu-id="34b05-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="34b05-153">Witaj Użyj następującego polecenia tooquery hello Solr interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="34b05-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="34b05-154">To polecenie wyszukuje **collection1** dokumenty dopasowania  **\*:\***  (zakodowane jako \*% 3A\* w ciągu zapytania hello).</span><span class="sxs-lookup"><span data-stu-id="34b05-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="34b05-155">powitania po dokumentu JSON jest przykładem hello odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="34b05-155">hello following JSON document is an example of hello response:</span></span>

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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="34b05-156">Przy użyciu pulpitu nawigacyjnego Solr hello</span><span class="sxs-lookup"><span data-stu-id="34b05-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="34b05-157">pulpit nawigacyjny Solr Hello jest interfejs użytkownika umożliwiający toowork z Solr za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="34b05-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="34b05-158">pulpit nawigacyjny Solr Hello nie jest uwidaczniana bezpośrednio na powitania Internet z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34b05-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="34b05-159">Można użyć tooaccess tunelu SSH go.</span><span class="sxs-lookup"><span data-stu-id="34b05-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="34b05-160">Aby uzyskać więcej informacji na temat używania tunelu SSH, zobacz hello [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="34b05-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="34b05-161">Po ustanowieniu tunelu SSH, użyj hello następujące kroki toouse hello Solr w pulpicie nawigacyjnym:</span><span class="sxs-lookup"><span data-stu-id="34b05-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="34b05-162">Określić nazwę hosta hello headnode głównej hello:</span><span class="sxs-lookup"><span data-stu-id="34b05-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="34b05-163">Użyj węzła głównego klastra toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="34b05-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="34b05-164">Na przykład `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="34b05-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="34b05-165">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="34b05-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="34b05-166">Użyj hello następujące polecenia tooget hello w pełni kwalifikowana nazwa hosta:</span><span class="sxs-lookup"><span data-stu-id="34b05-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="34b05-167">To polecenie zwraca wartość toohello podobne, następujące nazwy hosta:</span><span class="sxs-lookup"><span data-stu-id="34b05-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="34b05-168">Zapisz wartość hello zwrócona, ponieważ jest później używany.</span><span class="sxs-lookup"><span data-stu-id="34b05-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="34b05-169">W przeglądarce, za połączyć**http://HOSTNAME:8983/solr / #/**, gdzie **HOSTNAME** jest nazwą hello określone w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="34b05-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="34b05-170">Żądanie hello jest kierowany przez hello SSH tunelu toohello Solr interfejsu użytkownika sieci web w klastrze.</span><span class="sxs-lookup"><span data-stu-id="34b05-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="34b05-171">podobne toohello po obrazu zostanie wyświetlona strona Hello:</span><span class="sxs-lookup"><span data-stu-id="34b05-171">hello page appears similar toohello following image:</span></span>

    ![Obraz pulpitu nawigacyjnego Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="34b05-173">W okienku po lewej stronie powitania, użyj hello **selektora Core** tooselect listy rozwijanej **collection1**.</span><span class="sxs-lookup"><span data-stu-id="34b05-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="34b05-174">Kilka wpisów powinien je są wyświetlane poniżej **collection1**.</span><span class="sxs-lookup"><span data-stu-id="34b05-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="34b05-175">Z poniższych wpisów hello **collection1**, wybierz pozycję **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="34b05-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="34b05-176">Użyj hello następujące strony wyszukiwania hello toopopulate wartości:</span><span class="sxs-lookup"><span data-stu-id="34b05-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="34b05-177">W hello **q** tekst wprowadź  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="34b05-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="34b05-178">To zapytanie zwraca wszystkie dokumenty hello, które są indeksowane w Solr.</span><span class="sxs-lookup"><span data-stu-id="34b05-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="34b05-179">Jeśli chcesz toosearch dla określonego ciągu w dokumentach hello, można wprowadzić ten ciąg w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="34b05-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="34b05-180">W hello **wt** pole tekstowe, hello wybierz format danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="34b05-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="34b05-181">Domyślnie jest **json**.</span><span class="sxs-lookup"><span data-stu-id="34b05-181">Default is **json**.</span></span>

     <span data-ttu-id="34b05-182">Na koniec wybierz hello **wykonywanie zapytania** u dołu hello hello pate wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34b05-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="34b05-184">dane wyjściowe Hello zwraca powitalne dwa dokumenty dodania toohello wcześniej indeksu.</span><span class="sxs-lookup"><span data-stu-id="34b05-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="34b05-185">Witaj danych wyjściowych jest podobne toohello po dokumentu JSON:</span><span class="sxs-lookup"><span data-stu-id="34b05-185">hello output is similar toohello following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="34b05-186">Uruchamianie i zatrzymywanie Solr</span><span class="sxs-lookup"><span data-stu-id="34b05-186">Starting and stopping Solr</span></span>

<span data-ttu-id="34b05-187">Użyj następującego polecenia toomanually zatrzymywania i uruchamiania Solr hello:</span><span class="sxs-lookup"><span data-stu-id="34b05-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="34b05-188">Indeksowane dane kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="34b05-188">Backup indexed data</span></span>

<span data-ttu-id="34b05-189">Użyj hello następujące kroki tooback się Solr danych toohello domyślny magazyn dla klastra:</span><span class="sxs-lookup"><span data-stu-id="34b05-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="34b05-190">Połącz toohello klastra przy użyciu protokołu SSH, a następnie użyj następującego polecenia tooget hello hosta nazwę węzła głównego hello hello:</span><span class="sxs-lookup"><span data-stu-id="34b05-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="34b05-191">Użyj następującego polecenia toocreate migawkę danych hello indeksowane hello.</span><span class="sxs-lookup"><span data-stu-id="34b05-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="34b05-192">Zastąp **HOSTNAME** o nazwie hello zwrócony z hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="34b05-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="34b05-193">odpowiedź Hello jest podobne toohello po XML:</span><span class="sxs-lookup"><span data-stu-id="34b05-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="34b05-194">Zmień katalogi zbyt`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="34b05-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="34b05-195">Brak podkatalogu każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="34b05-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="34b05-196">Każdy katalog kolekcji zawiera `data` katalogu zawierającego migawkę hello hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="34b05-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="34b05-197">toocreate skompresowanego archiwum folder migawki hello, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="34b05-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="34b05-198">Zastąp hello `snapshot.20150806185338855` wartości o nazwie hello hello migawki kolekcji.</span><span class="sxs-lookup"><span data-stu-id="34b05-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="34b05-199">To polecenie tworzy archiwum o nazwie **snapshot.20150806185338855.tgz**, który zawiera zawartość hello hello **snapshot.20150806185338855** katalogu.</span><span class="sxs-lookup"><span data-stu-id="34b05-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="34b05-200">Następnie można przechowywać klastra hello archiwum toohello głównej pamięci masowej hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="34b05-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="34b05-201">Aby uzyskać więcej informacji na temat pracy z Solr tworzenia kopii zapasowej i przywracania, zobacz [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="34b05-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34b05-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34b05-202">Next steps</span></span>

* <span data-ttu-id="34b05-203">[Zainstaluj Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="34b05-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="34b05-204">Użyj tooinstall dostosowywania klastra, który Giraph na platformie Hadoop w HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="34b05-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="34b05-205">Giraph pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34b05-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="34b05-206">[Instalowanie aplikacji Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="34b05-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="34b05-207">Użyj Hue tooinstall dostosowywania klastrowania w klastrach HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="34b05-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="34b05-208">HUE jest zestaw aplikacji sieci Web użycia toointeract przy użyciu funkcji klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="34b05-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
