---
title: "aaaTroubleshoot Hive za pomocą usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon dotyczące pracy z Apache Hive i usłudze Azure HDInsight."
keywords: "Azure HDInsight, Hive, często zadawane pytania, rozwiązywanie problemów z przewodnika, często zadawane pytania"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="4665d-104">Rozwiązywanie problemów z Hive za pomocą usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4665d-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="4665d-105">Dowiedz się więcej o hello najczęściej zadawane pytania i ich rozwiązania podczas pracy z Apache Hive ładunków w Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="4665d-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="4665d-106">Jak wyeksportować na potrzeby magazynu metadanych Hive i zaimportuj go w innym klastrze</span><span class="sxs-lookup"><span data-stu-id="4665d-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4665d-107">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4665d-107">Resolution steps</span></span>

1. <span data-ttu-id="4665d-108">Połącz toohello klastra usługi HDInsight przy użyciu klienta Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="4665d-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="4665d-109">Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="4665d-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="4665d-110">Uruchom następujące polecenie na powitania klastra usługi HDInsight, z którego mają potrzeby magazynu metadanych tooexport hello hello:</span><span class="sxs-lookup"><span data-stu-id="4665d-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="4665d-111">To polecenie generuje plik o nazwie allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="4665d-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="4665d-112">Skopiuj hello pliku alltables.sql toohello nowego klastra usługi HDInsight, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4665d-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="4665d-113">Kod Hello w hello kroki rozwiązania przyjęto założenie, że dane, które są ścieżki w nowym klastrze hello hello sam jako ścieżek danych hello na powitania stary klaster.</span><span class="sxs-lookup"><span data-stu-id="4665d-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="4665d-114">Jeśli ścieżki danych hello są różne, można ręcznie edytować tooreflect pliku alltables.sql hello wygenerowany wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="4665d-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="4665d-115">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="4665d-115">Additional reading</span></span>

- [<span data-ttu-id="4665d-116">Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="4665d-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="4665d-117">Jak znaleźć gałęzi dzienniki w klastrze</span><span class="sxs-lookup"><span data-stu-id="4665d-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="4665d-118">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4665d-118">Resolution steps</span></span>

1. <span data-ttu-id="4665d-119">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4665d-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="4665d-120">Aby uzyskać więcej informacji, zobacz **dodatkowe materiały**.</span><span class="sxs-lookup"><span data-stu-id="4665d-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="4665d-121">dzienniki klienta Hive tooview, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4665d-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="4665d-122">Dzienniki potrzeby magazynu metadanych Hive tooview, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4665d-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="4665d-123">Dzienniki Hiveserver tooview, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4665d-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="4665d-124">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="4665d-124">Additional reading</span></span>

- [<span data-ttu-id="4665d-125">Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="4665d-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="4665d-126">Jak uruchomić hello powłoki gałąź o określonej konfiguracji w klastrze</span><span class="sxs-lookup"><span data-stu-id="4665d-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="4665d-127">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4665d-127">Resolution steps</span></span>

1. <span data-ttu-id="4665d-128">Określ parę klucz wartość konfiguracji podczas uruchamiania hello powłoki Hive.</span><span class="sxs-lookup"><span data-stu-id="4665d-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="4665d-129">Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="4665d-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="4665d-130">toolist wszystkie konfiguracje skuteczne na gałąź powłoki, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4665d-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="4665d-131">Na przykład użyć powitania po powłoka poleceń programu Hive toostart z rejestrowaniem debugowania włączone na powitania konsoli:</span><span class="sxs-lookup"><span data-stu-id="4665d-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="4665d-132">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="4665d-132">Additional reading</span></span>

- [<span data-ttu-id="4665d-133">Właściwości konfiguracji gałęzi</span><span class="sxs-lookup"><span data-stu-id="4665d-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="4665d-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Jak analizować dane Tez DAG na ścieżkę krytyczną klastra</span><span class="sxs-lookup"><span data-stu-id="4665d-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4665d-135">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4665d-135">Resolution steps</span></span>
 
1. <span data-ttu-id="4665d-136">tooanalyze Apache Tez skierowany wykresu acyklicznego (DAG) na wykresie klastra o znaczeniu krytycznym, Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4665d-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="4665d-137">Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="4665d-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="4665d-138">W wierszu polecenia Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4665d-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="4665d-139">toolist innych analizatorów, które mogą być używane tooanalyze Tez DAG, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4665d-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="4665d-140">Należy podać przykład programu jako pierwszego argumentu hello.</span><span class="sxs-lookup"><span data-stu-id="4665d-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="4665d-141">Program prawidłowe nazwy zawierają:</span><span class="sxs-lookup"><span data-stu-id="4665d-141">Valid program names include:</span></span>
    - <span data-ttu-id="4665d-142">**ContainerReuseAnalyzer**: drukowanie szczegółów ponownemu kontenera w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="4665d-143">**CriticalPath**: Znajdź hello ścieżkę krytyczną do grupy DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="4665d-144">**LocalityAnalyzer**: drukowanie szczegółów miejscowości, w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="4665d-145">**ShuffleTimeAnalyzer**: analizowanie szczegóły godziny losowa hello w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="4665d-146">**SkewAnalyzer**: analizowanie hello pochylenia szczegółów w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="4665d-147">**SlowNodeAnalyzer**: drukowanie szczegółów węzła w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="4665d-148">**SlowTaskIdentifier**: szczegóły powolne zadania drukowania w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="4665d-149">**SlowestVertexAnalyzer**: drukowanie najwolniejsze szczegółów wierzchołków w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="4665d-150">**SpillAnalyzer**: szczegóły usuwania wycieków drukowania w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="4665d-151">**TaskConcurrencyAnalyzer**: drukowanie szczegółów współbieżności zadań hello w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="4665d-152">**VertexLevelCriticalPathAnalyzer**: Znajdź ścieżkę krytyczną hello na poziomie wierzchołków w grupie DAG</span><span class="sxs-lookup"><span data-stu-id="4665d-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="4665d-153">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="4665d-153">Additional reading</span></span>

- [<span data-ttu-id="4665d-154">Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="4665d-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="4665d-155">W jaki sposób pobierać dane Tez DAG z klastra</span><span class="sxs-lookup"><span data-stu-id="4665d-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="4665d-156">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4665d-156">Resolution steps</span></span>

<span data-ttu-id="4665d-157">Istnieją dwa sposoby toocollect hello Tez DAG danych:</span><span class="sxs-lookup"><span data-stu-id="4665d-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="4665d-158">Z wiersza polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4665d-158">From hello command line:</span></span>
 
    <span data-ttu-id="4665d-159">Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4665d-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="4665d-160">W wierszu polecenia hello uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4665d-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="4665d-161">Użyj hello Ambari Tez widoku:</span><span class="sxs-lookup"><span data-stu-id="4665d-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="4665d-162">Przejdź tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="4665d-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="4665d-163">Widok Przejdź tooTez (w obszarze hello Kafelki ikonę w prawym górnym rogu hello).</span><span class="sxs-lookup"><span data-stu-id="4665d-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="4665d-164">Wybierz hello ma tooview grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="4665d-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="4665d-165">Wybierz **pobierania danych**.</span><span class="sxs-lookup"><span data-stu-id="4665d-165">Select **Download data**.</span></span>

### <span data-ttu-id="4665d-166"><a name="additional-reading-end"></a>Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="4665d-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="4665d-167">Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="4665d-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






