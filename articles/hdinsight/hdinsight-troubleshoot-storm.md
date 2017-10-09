---
title: "aaaTroubleshoot Storm przy użyciu usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon przy użyciu platformy Apache Storm w usłudze Azure HDInsight."
keywords: "Azure HDInsight, Storm, często zadawane pytania, przewodnik, typowe problemy rozwiązywania problemów"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="18263-104">Rozwiązywanie problemów z Storm przy użyciu usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="18263-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="18263-105">Więcej informacji na temat hello Najważniejsze problemy i ich rozwiązania do pracy z ładunków Apache Storm w Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="18263-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="18263-106">Jak uzyskać dostęp do hello interfejsu użytkownika platformy Storm w klastrze</span><span class="sxs-lookup"><span data-stu-id="18263-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="18263-107">Masz dwie opcje do uzyskiwania dostępu do interfejsu użytkownika platformy Storm hello w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="18263-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="18263-108">Interfejs użytkownika narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="18263-108">Ambari UI</span></span>
1. <span data-ttu-id="18263-109">Przejdź toohello Ambari w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="18263-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="18263-110">Liście hello usług wybierz **Storm**.</span><span class="sxs-lookup"><span data-stu-id="18263-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="18263-111">W hello **szybkie linki** menu, wybierz opcję **interfejsu użytkownika platformy Storm**.</span><span class="sxs-lookup"><span data-stu-id="18263-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="18263-112">Bezpośrednie połączenie</span><span class="sxs-lookup"><span data-stu-id="18263-112">Direct link</span></span>
<span data-ttu-id="18263-113">Aby dostęp do hello interfejsu użytkownika platformy Storm w hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="18263-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="18263-114">https://\<nazwę klastra DNS\>/stormui</span><span class="sxs-lookup"><span data-stu-id="18263-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="18263-115">Przykład:</span><span class="sxs-lookup"><span data-stu-id="18263-115">Example:</span></span>

 <span data-ttu-id="18263-116">https://stormcluster.azurehdinsight.NET/stormui</span><span class="sxs-lookup"><span data-stu-id="18263-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="18263-117">Jak przenieść informacje dotyczące punktu kontrolnego spout Centrum zdarzeń Storm z jednego topologii tooanother</span><span class="sxs-lookup"><span data-stu-id="18263-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="18263-118">Podczas opracowywania topologii, które zapoznały z usługi Azure Event Hubs przy użyciu hello pliku JAR spout Centrum zdarzeń HDInsight Storm, należy wdrożyć topologię, która ma hello takie same nazwy w nowym klastrze.</span><span class="sxs-lookup"><span data-stu-id="18263-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="18263-119">Należy jednak zachować dane punktu kontrolnego hello zostało zatwierdzone tooApache dozorcy hello starego klastra.</span><span class="sxs-lookup"><span data-stu-id="18263-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="18263-120">Gdzie są przechowywane dane punktu kontrolnego</span><span class="sxs-lookup"><span data-stu-id="18263-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="18263-121">Dane punktu kontrolnego dla przesunięcia jest przechowywany przez hello spout Centrum zdarzeń w dozorcy w dwie ścieżki katalogu głównego:</span><span class="sxs-lookup"><span data-stu-id="18263-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="18263-122">Punkty kontrolne spout nietransakcyjne są przechowywane w /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="18263-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="18263-123">Dane punktu kontrolnego transakcyjne spout jest przechowywany / transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="18263-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="18263-124">Jak toorestore</span><span class="sxs-lookup"><span data-stu-id="18263-124">How toorestore</span></span>
<span data-ttu-id="18263-125">tooget hello skrypty i biblioteki, czy można użyć danych tooexport poza dozorcy, a następnie zaimportować hello tooZooKeeper wstecz danych pod nową nazwą, zobacz [przykłady HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="18263-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="18263-126">Witaj lib znajduje się w nim pliki JAR, które zawierają hello implementację dla operacji importu/eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="18263-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="18263-127">Hello bash folder zawiera przykładowy skrypt, który demonstruje sposób tooexport danych z hello serwera dozorcy hello starego klastra, a następnie zaimportuj go toohello zapasowego serwera dozorcy hello w nowym klastrze.</span><span class="sxs-lookup"><span data-stu-id="18263-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="18263-128">Uruchom hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) skrypt z tooexport węzły dozorcy hello, a następnie importować dane.</span><span class="sxs-lookup"><span data-stu-id="18263-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="18263-129">Witaj skryptu toohello poprawne Hortonworks Data Platform (HDP) wersja aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="18263-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="18263-130">(Pracujemy nad wprowadzeniem tych skryptów ogólnego w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18263-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="18263-131">Ogólny skrypty można uruchomić z dowolnego węzła w klastrze hello bez modyfikacji przez użytkownika hello.)</span><span class="sxs-lookup"><span data-stu-id="18263-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="18263-132">polecenie export Hello zapisuje hello tooan Apache Hadoop Distributed plików systemowych (HDFS) ścieżka metadanych (w sklepie z magazynu obiektów Blob Azure lub usługi Azure Data Lake Store) w lokalizacji, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="18263-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="18263-133">Przykłady</span><span class="sxs-lookup"><span data-stu-id="18263-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="18263-134">Eksportowanie metadanych przesunięcia</span><span class="sxs-lookup"><span data-stu-id="18263-134">Export offset metadata</span></span>
1. <span data-ttu-id="18263-135">Użyj SSH toogo toohello dozorcy klastra w klastrze powitania od punktu kontrolnego które hello przesunięcie musi toobe wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="18263-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="18263-136">Hello uruchom następujące polecenie (po zaktualizowaniu hello ciąg wersji HDP) tooexport dozorcy przesunięcie /stormmetadta/zkdata toohello danych systemu plików HDFS ścieżki:</span><span class="sxs-lookup"><span data-stu-id="18263-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="18263-137">Importuj metadane przesunięcia</span><span class="sxs-lookup"><span data-stu-id="18263-137">Import offset metadata</span></span>
1. <span data-ttu-id="18263-138">Użyj SSH toogo toohello dozorcy klastra w klastrze powitania od punktu kontrolnego które hello przesunięcie musi toobe wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="18263-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="18263-139">Uruchom hello następujące polecenie (po zaktualizowaniu ciąg wersji hello HDP) tooimport dozorcy Przesunięcie danych z hello systemu plików HDFS ścieżki/stormmetadata/zkdata toohello dozorcy serwera na powitania klastra docelowego:</span><span class="sxs-lookup"><span data-stu-id="18263-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="18263-140">Usuwanie metadanych przesunięcia tak, aby rozpocząć topologie przetwarzania danych od początku hello lub ze znacznikiem czasu hello użytkownik wybierze</span><span class="sxs-lookup"><span data-stu-id="18263-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="18263-141">Użyj SSH toogo toohello dozorcy klastra w klastrze powitania od punktu kontrolnego które hello przesunięcie musi toobe wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="18263-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="18263-142">Uruchom hello następujące polecenie (po zaktualizowaniu ciąg wersji hello HDP) toodelete wszystkie dozorcy Przesunięcie danych w hello bieżący klaster:</span><span class="sxs-lookup"><span data-stu-id="18263-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="18263-143">Jak znaleźć plików binarnych systemu Storm w klastrze</span><span class="sxs-lookup"><span data-stu-id="18263-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="18263-144">Pliki binarne STORM dla bieżącego stosu HDP hello są /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="18263-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="18263-145">Lokalizacja Hello jest hello sam zarówno dla węzłów głównych i węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="18263-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="18263-146">Może istnieć wiele plików binarnych dla określonej wersji HDP w /usr/hdp (na przykład /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="18263-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="18263-147">Hello /usr/hdp/current/storm-client folder jest symlinked toohello najnowszą wersję, która jest uruchomiona w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="18263-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="18263-148">Aby uzyskać więcej informacji, zobacz [klastra usługi HDInsight tooan Połącz przy użyciu protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) i [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="18263-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="18263-149">Jak ustalić hello topologii wdrożenia klastra Storm</span><span class="sxs-lookup"><span data-stu-id="18263-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="18263-150">Ustalenie wszystkie składniki, które są instalowane z HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="18263-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="18263-151">Klaster Storm składa się z czterech węzłów kategorii:</span><span class="sxs-lookup"><span data-stu-id="18263-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="18263-152">Węzły bramy</span><span class="sxs-lookup"><span data-stu-id="18263-152">Gateway nodes</span></span>
* <span data-ttu-id="18263-153">HEAD węzłów</span><span class="sxs-lookup"><span data-stu-id="18263-153">Head nodes</span></span>
* <span data-ttu-id="18263-154">Węzły dozorcy</span><span class="sxs-lookup"><span data-stu-id="18263-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="18263-155">Węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="18263-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="18263-156">Węzły bramy</span><span class="sxs-lookup"><span data-stu-id="18263-156">Gateway nodes</span></span>
<span data-ttu-id="18263-157">Węzeł bramy ma bramy i zwrotny serwer proxy usługi, która umożliwia dostęp publiczny tooan Ambari usługi zarządzania usługą active.</span><span class="sxs-lookup"><span data-stu-id="18263-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="18263-158">Obsługuje ona również Ambari wiodące wyborów.</span><span class="sxs-lookup"><span data-stu-id="18263-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="18263-159">HEAD węzłów</span><span class="sxs-lookup"><span data-stu-id="18263-159">Head nodes</span></span>
<span data-ttu-id="18263-160">STORM hello węzłów głównych, uruchom następujące usługi:</span><span class="sxs-lookup"><span data-stu-id="18263-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="18263-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="18263-161">Nimbus</span></span>
* <span data-ttu-id="18263-162">Serwer Ambari</span><span class="sxs-lookup"><span data-stu-id="18263-162">Ambari server</span></span>
* <span data-ttu-id="18263-163">Metryki Ambari serwera</span><span class="sxs-lookup"><span data-stu-id="18263-163">Ambari Metrics server</span></span>
* <span data-ttu-id="18263-164">Moduł zbierający metryki Ambari</span><span class="sxs-lookup"><span data-stu-id="18263-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="18263-165">Węzły dozorcy</span><span class="sxs-lookup"><span data-stu-id="18263-165">ZooKeeper nodes</span></span>
<span data-ttu-id="18263-166">Usługa HDInsight obejmuje trzy dozorcy kworum.</span><span class="sxs-lookup"><span data-stu-id="18263-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="18263-167">Witaj rozmiar kworum jest stała i nie można ponownie skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="18263-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="18263-168">Usługi STORM w klastrze hello są skonfigurowane tooautomatically Użyj hello dozorcy kworum.</span><span class="sxs-lookup"><span data-stu-id="18263-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="18263-169">Węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="18263-169">Worker nodes</span></span>
<span data-ttu-id="18263-170">STORM węzłów procesu roboczego Uruchom hello następujące usługi:</span><span class="sxs-lookup"><span data-stu-id="18263-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="18263-171">Nadzorca</span><span class="sxs-lookup"><span data-stu-id="18263-171">Supervisor</span></span>
* <span data-ttu-id="18263-172">Proces roboczy języka Java maszyn wirtualnych (JVMs), do uruchamiania topologii</span><span class="sxs-lookup"><span data-stu-id="18263-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="18263-173">Ambari agent</span><span class="sxs-lookup"><span data-stu-id="18263-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="18263-174">Jak znaleźć plików binarnych spout Centrum zdarzeń Storm do tworzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="18263-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="18263-175">Aby uzyskać więcej informacji o korzystaniu z topologii Storm — pliki JAR spout Centrum zdarzeń zobacz następujące zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="18263-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="18263-176">Topologia opartych na języku Java</span><span class="sxs-lookup"><span data-stu-id="18263-176">Java-based topology</span></span>
[<span data-ttu-id="18263-177">Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="18263-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="18263-178">C# — na podstawie topologii (Mono w klastrach HDInsight 3.4 + Linux Storm)</span><span class="sxs-lookup"><span data-stu-id="18263-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
<span data-ttu-id="18263-179">[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology) (Przetwarzanie zdarzeń usługi Azure Event Hubs przy użyciu systemu Storm w usłudze HDInsight — C#)</span><span class="sxs-lookup"><span data-stu-id="18263-179">[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)</span></span>
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="18263-180">Pliki binarne w przypadku klastrów Linux Storm HDInsight 3.5 + elementów spout Centrum zdarzeń Storm najnowsze</span><span class="sxs-lookup"><span data-stu-id="18263-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="18263-181">toolearn toouse hello najnowsze Storm zdarzenia koncentratora spout współpracujące z usługą HDInsight 3.5 + klastrów Linux Storm, zobacz hello mvn repozytorium [plik readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="18263-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="18263-182">Przykłady kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="18263-182">Source code examples</span></span>
<span data-ttu-id="18263-183">Zobacz [przykłady](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) jak tooread i zapisywania z Centrum zdarzeń platformy Azure przy użyciu topologii Apache Storm (napisany w języku Java) w klastrze usługi HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="18263-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="18263-184">Jak znaleźć pliki konfiguracji narzędzia Log4J Storm w klastrze</span><span class="sxs-lookup"><span data-stu-id="18263-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="18263-185">pliki konfiguracji tooidentify Apache Log4J Storm usług.</span><span class="sxs-lookup"><span data-stu-id="18263-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="18263-186">W węzłach głównych</span><span class="sxs-lookup"><span data-stu-id="18263-186">On head nodes</span></span>
<span data-ttu-id="18263-187">Witaj Nimbus Log4J konfiguracji są odczytywane z usr/hdp/\<wersji HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="18263-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="18263-188">Na węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="18263-188">On worker nodes</span></span>
<span data-ttu-id="18263-189">Konfiguracja przełożonego Log4J Hello są odczytywane z usr/hdp/\<wersji HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="18263-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="18263-190">plik konfiguracji procesu roboczego Log4J Hello są odczytywane z usr/hdp/\<wersji HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="18263-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="18263-191">Przykłady: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="18263-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

