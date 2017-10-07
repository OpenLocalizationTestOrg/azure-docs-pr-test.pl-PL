---
title: "aaaInstall i używać Giraph w usłudze HDInsight (Hadoop) - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Giraph na HDInsight opartych na systemie Linux klastrów za pomocą akcji skryptu. Akcje skryptu zezwalaj klastrowi hello toocustomize podczas tworzenia, zmieniając konfigurację klastra lub instalowania usług i narzędzi."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="ba6f9-104">Zainstaluj Giraph w klastrach HDInsight Hadoop i użyj Giraph tooprocess dużych wykresów</span><span class="sxs-lookup"><span data-stu-id="ba6f9-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="ba6f9-105">Dowiedz się, jak tooinstall Apache Giraph w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="ba6f9-106">Hello funkcji Akcja skryptu HDInsight umożliwia toocustomize klastra przez uruchomienie skryptu bash.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="ba6f9-107">Skrypty można klastrów toocustomize używane podczas i po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba6f9-108">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ba6f9-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ba6f9-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ba6f9-111"><a name="whatis"></a>Co to jest Giraph</span><span class="sxs-lookup"><span data-stu-id="ba6f9-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="ba6f9-112">[Apache Giraph](http://giraph.apache.org/) pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="ba6f9-113">Wykresy modelu relacje między obiektami.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="ba6f9-114">Na przykład hello połączeń między routerami w dużych sieci, takich jak hello Internet lub relacje między osób w sieciach społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="ba6f9-115">Wykres przetwarzania pozwala tooreason o hello relacje między obiektami na wykresie, takich jak:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="ba6f9-116">Identyfikuje potencjalne znajomych oparte na bieżącej relacji.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="ba6f9-117">Identyfikowanie hello najkrótszy trasy między dwoma komputerami w sieci.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="ba6f9-118">Obliczanie rangę strony hello stron sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="ba6f9-119">Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane - Microsoft Support pomaga tooisolate i rozwiązać problemy toothese powiązane składniki.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="ba6f9-120">Niestandardowe składniki, takie jak Giraph, odbierania toohelp uzasadnione ekonomicznie Obsługa toofurther należy rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="ba6f9-121">Microsoft Support może być możliwe tooresolving hello problem.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="ba6f9-122">Jeśli nie, należy zapoznać się z Wspólnot typu open source wykryto głębokie doświadczenia z tej technologii.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="ba6f9-123">Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="ba6f9-124">Jakie skrypt hello wykonuje</span><span class="sxs-lookup"><span data-stu-id="ba6f9-124">What hello script does</span></span>

<span data-ttu-id="ba6f9-125">Ten skrypt wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="ba6f9-126">Instaluje Giraph zbyt`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="ba6f9-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="ba6f9-127">Witaj kopie `giraph-examples.jar` pliku magazynu toodefault (WASB) dla klastra:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="ba6f9-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="ba6f9-128"><a name="install"></a>Zainstaluj Giraph za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="ba6f9-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="ba6f9-129">Przykładowy skrypt tooinstall Giraph w klastrze usługi HDInsight jest dostępna w hello w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="ba6f9-130">Ta sekcja zawiera instrukcje jak toouse hello przykładowy skrypt podczas tworzenia klastra hello za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ba6f9-131">Akcja skryptu można zastosować za pomocą jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="ba6f9-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba6f9-132">Azure PowerShell</span></span>
> * <span data-ttu-id="ba6f9-133">Witaj wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ba6f9-133">hello Azure CLI</span></span>
> * <span data-ttu-id="ba6f9-134">Witaj zestawu .NET SDK usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba6f9-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="ba6f9-135">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba6f9-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="ba6f9-136">Można także zastosować tooalready akcji skryptu działające klastry.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="ba6f9-137">Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="ba6f9-138">Rozpocznij tworzenie klastra przy użyciu kroków hello [klastrów usługi HDInsight opartych na tworzenie Linux](hdinsight-hadoop-create-linux-clusters-portal.md), kroków tworzenia.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="ba6f9-139">Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **akcji skryptu**i podaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="ba6f9-140">**Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="ba6f9-141">**Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="ba6f9-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="ba6f9-142">**HEAD**: Sprawdź tego wpisu</span><span class="sxs-lookup"><span data-stu-id="ba6f9-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="ba6f9-143">**Proces ROBOCZY**: ten wpis należy pozostawić niezaznaczone</span><span class="sxs-lookup"><span data-stu-id="ba6f9-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="ba6f9-144">**DOZORCY**: ten wpis należy pozostawić niezaznaczone</span><span class="sxs-lookup"><span data-stu-id="ba6f9-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="ba6f9-145">**Parametry**: pozostaw to pole puste</span><span class="sxs-lookup"><span data-stu-id="ba6f9-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="ba6f9-146">U dołu hello hello **akcji skryptu**, użyj hello **wybierz** przycisk toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="ba6f9-147">Na koniec użyj hello **wybierz** u dołu hello hello **konfiguracji opcjonalnej** bloku toosave hello konfiguracji opcjonalnej informacji.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="ba6f9-148">Kontynuuj tworzenie klastra hello zgodnie z opisem w [klastrów usługi HDInsight opartych na tworzenie Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="ba6f9-149"><a name="usegiraph"></a>Jak używać Giraph w usłudze HDInsight?</span><span class="sxs-lookup"><span data-stu-id="ba6f9-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="ba6f9-150">Po utworzeniu klastra hello Użyj hello następujące kroki toorun SimpleShortestPathsComputation przykład Witaj dołączonego Giraph.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="ba6f9-151">W tym przykładzie użyto hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementacji do znajdowania hello najkrótszy ścieżki między obiektami na wykresie.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="ba6f9-152">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ba6f9-153">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ba6f9-154">Użyj hello następujące polecenie toocreate plik o nazwie **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="ba6f9-155">Użyj hello następującego tekstu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="ba6f9-156">Te dane w tym artykule opisano relacje między obiektami w ukierunkowanego wykresu, używając formatu hello `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="ba6f9-157">Każdy wiersz zawiera relację między `source_id` obiektu i co najmniej jeden `dest_id` obiektów.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="ba6f9-158">Witaj `edge_value` można traktować jako siły hello lub odległość hello połączenie między `source_id` i `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="ba6f9-159">Rysowane, i przy użyciu hello wartości (lub wagi) jako hello odległość między obiektami, hello danych może wyglądać powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt rysowane jako okręgi wiersze z różnymi odległość między](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="ba6f9-161">toosave hello pliku, użyj **Ctrl + X**, następnie **Y**, a na końcu **Enter** nazwę pliku hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="ba6f9-162">Użyj powitania po toostore hello danych na podstawowy magazyn dla klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="ba6f9-163">Uruchom przykład SimpleShortestPathsComputation Witaj przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="ba6f9-164">Parametry Hello używane w tym poleceniu są opisane w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="ba6f9-165">Parametr</span><span class="sxs-lookup"><span data-stu-id="ba6f9-165">Parameter</span></span> | <span data-ttu-id="ba6f9-166">Wyniki działania</span><span class="sxs-lookup"><span data-stu-id="ba6f9-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="ba6f9-167">Witaj plik jar zawierający hello przykłady.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="ba6f9-168">Klasa Hello używana toostart hello przykłady.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="ba6f9-169">przykład Witaj, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-169">hello example that is used.</span></span> <span data-ttu-id="ba6f9-170">W tym przykładzie oblicza hello najkrótszy ścieżki między ID 1 i innych identyfikatorów w grafie hello.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="ba6f9-171">Witaj headnode hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="ba6f9-172">toouse format wejściowy Hello hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="ba6f9-173">plik danych wejściowych Hello.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="ba6f9-174">format danych wyjściowych Hello.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-174">hello output format.</span></span> <span data-ttu-id="ba6f9-175">W tym przykładzie, Identyfikatora i wartości w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="ba6f9-176">Witaj lokalizacji wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="ba6f9-177">Liczba Hello toouse pracowników.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-177">hello number of workers toouse.</span></span> <span data-ttu-id="ba6f9-178">W tym przykładzie 2.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-178">In this example, 2.</span></span> |

    <span data-ttu-id="ba6f9-179">Aby uzyskać więcej informacji na temat tych i innych parametrów używane z próbek Giraph, zobacz hello [szybkiego startu Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="ba6f9-180">Po zakończeniu zadania hello hello wyniki są przechowywane w hello **/example/out/shotestpaths** katalogu.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="ba6f9-181">Hello nazwy pliku wyjściowego rozpoczynać się od **części-m -** i kończyć liczbę określającą hello pierwszy, drugi, itp. plik.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="ba6f9-182">Użyj następujących danych wyjściowych polecenia tooview hello hello:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="ba6f9-183">dane wyjściowe Hello powinna zostać wyświetlona podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ba6f9-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="ba6f9-184">przykład Witaj SimpleShortestPathComputation jest zakodowany toostart z obiektem ID 1 i Znajdź hello najkrótszy ścieżki tooother obiektów.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="ba6f9-185">dane wyjściowe Hello jest w formacie hello `destination_id` i `distance`.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="ba6f9-186">Witaj `distance` jest wartość hello (lub wagi) krawędzi hello pokonać między obiektu ID 1 i identyfikatora hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="ba6f9-187">Wizualizacja danych, można sprawdzić wyniki hello za podróży hello najkrótszy ścieżek między 1 Identyfikatora i wszystkie inne obiekty.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="ba6f9-188">Najkrótszy ścieżki Hello między ID 1 i 4 identyfikator wynosi 5.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="ba6f9-189">Ta wartość jest hello całkowita odległość między <span style="color:orange">ID 1 i 3</span>, a następnie <span style="color:red">identyfikator 3 i 4</span>.</span><span class="sxs-lookup"><span data-stu-id="ba6f9-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Rysowanie obiektów jako kółka za pomocą najmniejszej ścieżek między](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="ba6f9-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba6f9-191">Next steps</span></span>

* <span data-ttu-id="ba6f9-192">[Zainstalować i używać Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="ba6f9-193">[Zainstaluj Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ba6f9-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
