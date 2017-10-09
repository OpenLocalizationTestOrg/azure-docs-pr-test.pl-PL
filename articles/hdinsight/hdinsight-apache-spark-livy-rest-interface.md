---
title: "aaaUse klastra tooSpark zadania toosubmit Livy Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toosubmit interfejsu API REST Spark Apache Spark zadania zdalnie tooan klaster Azure HDInsight."
keywords: Platforma Apache spark rest api, livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="b51db-104">Użyj interfejsu API Apache Spark REST toosubmit zdalnego zadania tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b51db-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="b51db-105">Dowiedz się, jak toouse Livy, hello Apache interfejsu API REST Spark, która jest używana toosubmit zdalnego zadania tooan Azure HDInsight Spark klastra.</span><span class="sxs-lookup"><span data-stu-id="b51db-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="b51db-106">Szczegółowa dokumentacja zobacz [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="b51db-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="b51db-107">Można użyć Livy toorun interakcyjne Spark powłok lub przesłać Uruchom na Spark toobe zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="b51db-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="b51db-108">Ten artykuł zawiera informacje o przy użyciu programu Livy toosubmit partii zadań.</span><span class="sxs-lookup"><span data-stu-id="b51db-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="b51db-109">wstawki Hello w tym artykule Użyj toomake cURL końcowym Livy Spark toohello wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b51db-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="b51db-110">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="b51db-110">**Prerequisites:**</span></span>

* <span data-ttu-id="b51db-111">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b51db-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b51db-112">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b51db-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="b51db-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="b51db-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="b51db-114">W tym artykule wykorzystano toodemonstrate cURL jak wywołuje toomake interfejsu API REST względem klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b51db-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="b51db-115">Prześlij zadanie wsadowe Livy Spark</span><span class="sxs-lookup"><span data-stu-id="b51db-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="b51db-116">Przed wysłaniem wsadowym należy przekazać hello aplikacji jar w magazynie klastra hello skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="b51db-117">Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), narzędzie wiersza polecenia, toodo tak.</span><span class="sxs-lookup"><span data-stu-id="b51db-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="b51db-118">Brak danych tooupload można użyć różnych innych klientów.</span><span class="sxs-lookup"><span data-stu-id="b51db-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="b51db-119">Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b51db-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="b51db-120">**Przykłady**:</span><span class="sxs-lookup"><span data-stu-id="b51db-120">**Examples**:</span></span>

* <span data-ttu-id="b51db-121">Jeśli plik jar hello znajduje się w magazynie klastra hello (WASB)</span><span class="sxs-lookup"><span data-stu-id="b51db-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="b51db-122">Jeśli chcesz toopass hello jar filename i hello classname jako część pliku wejściowego (w tym przykładzie dane_wejściowe.txt zgodnie)</span><span class="sxs-lookup"><span data-stu-id="b51db-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="b51db-123">Dowiedz się o uruchomiona w klastrze hello partie Livy Spark</span><span class="sxs-lookup"><span data-stu-id="b51db-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="b51db-124">**Przykłady**:</span><span class="sxs-lookup"><span data-stu-id="b51db-124">**Examples**:</span></span>

* <span data-ttu-id="b51db-125">Jeśli chcesz tooretrieve wszystkie instancje Livy Spark hello uruchomiona w klastrze hello:</span><span class="sxs-lookup"><span data-stu-id="b51db-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="b51db-126">Jeśli chcesz, aby tooretrieve określonej partii o dany identyfikator partii</span><span class="sxs-lookup"><span data-stu-id="b51db-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="b51db-127">Usuwanie zadania wsadowego Livy Spark</span><span class="sxs-lookup"><span data-stu-id="b51db-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="b51db-128">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b51db-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="b51db-129">Livy Spark i wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="b51db-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="b51db-130">Livy przewiduje Spark zadania uruchomione w klastrze hello wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="b51db-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="b51db-131">Oto kilka przykładów.</span><span class="sxs-lookup"><span data-stu-id="b51db-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="b51db-132">Jeśli hello usługi Livy ulegnie awarii, gdy prześlesz zadania zdalnie tooa Spark klaster, hello zadanie nadal toorun w tle hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="b51db-133">Gdy Livy jest tworzenie kopii zapasowej, przywraca stan hello hello zadania i raporty go.</span><span class="sxs-lookup"><span data-stu-id="b51db-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="b51db-134">Notesów Jupyter w usłudze HDInsight są obsługiwane przez Livy w hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b51db-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="b51db-135">Jeśli notes działa zadanie Spark i ponownym pobiera hello usługi Livy notesu hello nadal toorun hello kodu komórek.</span><span class="sxs-lookup"><span data-stu-id="b51db-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="b51db-136">Pokaż przykład</span><span class="sxs-lookup"><span data-stu-id="b51db-136">Show me an example</span></span>
<span data-ttu-id="b51db-137">W tej sekcji możemy przyjrzeć się zadania wsadowego toosubmit przykłady toouse Livy Spark, monitorować postęp zadania hello hello, a następnie usuń go.</span><span class="sxs-lookup"><span data-stu-id="b51db-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="b51db-138">Witaj używamy w tym przykładzie jest aplikacja hello jedną opracowane w artykule hello [Utwórz autonomiczny Scala aplikacji i toorun w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="b51db-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="b51db-139">w tym miejscu kroki Hello założono, że:</span><span class="sxs-lookup"><span data-stu-id="b51db-139">hello steps here assume that:</span></span>

* <span data-ttu-id="b51db-140">Ma już kopiowane hello aplikacji jar toohello magazynu konta skojarzonego z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="b51db-141">Masz CuRL zainstalowany na komputerze hello, gdzie chcesz następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="b51db-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="b51db-142">Wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b51db-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="b51db-143">Daj nam najpierw sprawdź, czy Livy Spark jest uruchomiona w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="b51db-144">Firma Microsoft może zrobić, pobieranie listy uruchomionych partie.</span><span class="sxs-lookup"><span data-stu-id="b51db-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="b51db-145">Jeśli są uruchomione zadanie, używając programu Livy dla powitania po raz pierwszy, dane wyjściowe hello powinien zwrócić zero.</span><span class="sxs-lookup"><span data-stu-id="b51db-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="b51db-146">Należy pobrać dane wyjściowe podobne toohello po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="b51db-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b51db-147">Zwróć uwagę, jak ostatni wiersz hello w danych wyjściowych hello mówi **łącznie: 0**, które sugeruje nie uruchomionego partie.</span><span class="sxs-lookup"><span data-stu-id="b51db-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="b51db-148">Daj nam przesłać zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="b51db-148">Let us now submit a batch job.</span></span> <span data-ttu-id="b51db-149">powitania po fragment używa pliku wejściowego (dane_wejściowe.txt zgodnie) toopass hello jar nazwy i nazwy klasy hello jako parametry.</span><span class="sxs-lookup"><span data-stu-id="b51db-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="b51db-150">Jeśli używasz tych kroków z komputerem z systemem Windows, przy użyciu pliku wejściowego jest hello zalecane podejście.</span><span class="sxs-lookup"><span data-stu-id="b51db-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="b51db-151">Witaj parametrów w pliku hello **dane_wejściowe.txt zgodnie** są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b51db-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="b51db-152">Powinny pojawić się dane wyjściowe podobne toohello po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="b51db-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b51db-153">Zwróć uwagę, jak ostatni wiersz danych wyjściowych hello hello mówi **stanu: uruchamianie**.</span><span class="sxs-lookup"><span data-stu-id="b51db-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="b51db-154">Również mówi, **identyfikator: 0**.</span><span class="sxs-lookup"><span data-stu-id="b51db-154">It also says, **id:0**.</span></span> <span data-ttu-id="b51db-155">W tym miejscu **0** jest identyfikator hello wsadu.</span><span class="sxs-lookup"><span data-stu-id="b51db-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="b51db-156">Teraz można pobrać stanu hello tej partii określone przy użyciu identyfikatora hello partii.</span><span class="sxs-lookup"><span data-stu-id="b51db-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="b51db-157">Powinny pojawić się dane wyjściowe podobne toohello po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="b51db-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b51db-158">Witaj danych wyjściowych teraz wyświetlone **stanu: Sukces**, które sugeruje to zadanie hello zostało wykonane pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b51db-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="b51db-159">Jeśli chcesz, można usunąć hello partii.</span><span class="sxs-lookup"><span data-stu-id="b51db-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="b51db-160">Powinny pojawić się dane wyjściowe podobne toohello po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="b51db-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b51db-161">ostatni wiersz danych wyjściowych hello Hello pokazuje tej partii hello zostało pomyślnie usunięte.</span><span class="sxs-lookup"><span data-stu-id="b51db-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="b51db-162">Również usunięcie zadania, gdy jest on uruchomiony, kasuje hello zadania.</span><span class="sxs-lookup"><span data-stu-id="b51db-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="b51db-163">W przypadku usunięcia zadania, które zostało zakończone pomyślnie, lub w przeciwnym razie usuwa informacje o zadaniu hello całkowicie.</span><span class="sxs-lookup"><span data-stu-id="b51db-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="b51db-164">Przy użyciu programu Livy Spark w klastrach HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="b51db-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="b51db-165">Klaster HDInsight 3.5 domyślnie wyłącza pliki danych przykładowych tooaccess ścieżki pliku lokalnego lub słoików.</span><span class="sxs-lookup"><span data-stu-id="b51db-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="b51db-166">Firma Microsoft zachęca toouse hello `wasb://` ścieżka zamiast słoików tooaccess lub przykładowych danych plików z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="b51db-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="b51db-167">Jeśli chcesz toouse ścieżki lokalnej, należy zaktualizować hello Ambari konfiguracji odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="b51db-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="b51db-168">toodo tak:</span><span class="sxs-lookup"><span data-stu-id="b51db-168">toodo so:</span></span>

1. <span data-ttu-id="b51db-169">Odwiedź portal Ambari toohello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="b51db-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="b51db-170">Witaj Interfejsu sieci Web Ambari jest dostępna w klastrze usługi HDInsight w https://**CLUSTERNAME**. azurehdidnsight.net, gdzie CLUSTERNAME jest nazwą hello klastra.</span><span class="sxs-lookup"><span data-stu-id="b51db-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="b51db-171">Lewy pasek nawigacyjny hello, kliknij **Livy**, a następnie kliknij przycisk **Configs**.</span><span class="sxs-lookup"><span data-stu-id="b51db-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="b51db-172">W obszarze **domyślne livy** Dodaj nazwę właściwości hello `livy.file.local-dir-whitelist` i ustawić jej wartości także**"/"** Jeśli chcesz tooallow pełny dostęp toofile systemu.</span><span class="sxs-lookup"><span data-stu-id="b51db-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="b51db-173">Jeśli chcesz tooallow dostępu tylko tooa określonego katalogu, podaj hello ścieżka toothat katalog jako wartość hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="b51db-174">Przesyłanie zadań Livy klastra w ramach sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b51db-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="b51db-175">Jeśli łączysz się tooan klastra Spark w usłudze HDInsight z wewnątrz sieci wirtualnej platformy Azure, możesz połączyć bezpośrednio tooLivy w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="b51db-176">W takim przypadku hello adres URL dla punktu końcowego programu Livy jest `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="b51db-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="b51db-177">W tym miejscu **8998** jest hello port, na którym jest uruchomiony Livy na powitania headnode klastra.</span><span class="sxs-lookup"><span data-stu-id="b51db-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="b51db-178">Aby uzyskać więcej informacji na uzyskiwanie dostępu do usług na portach niepubliczne, zobacz [porty używane przez usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="b51db-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b51db-179">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="b51db-179">Troubleshooting</span></span>

<span data-ttu-id="b51db-180">Poniżej przedstawiono niektóre problemy, które możesz napotkać podczas przy użyciu programu Livy zdalnego zadania przesyłania tooSpark klastrów.</span><span class="sxs-lookup"><span data-stu-id="b51db-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="b51db-181">Za pomocą zewnętrznego jar z hello dodatkowego magazynu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="b51db-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="b51db-182">**Problem:** zadania Livy Spark odwołuje się do zewnętrznego jar z konta magazynu dodatkowe hello skojarzony z klastrem hello, hello zadanie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b51db-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="b51db-183">**Rozwiązanie:** upewnij się, że jar hello ma toouse jest dostępna w magazynie domyślne hello skojarzony z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b51db-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="b51db-184">Następny krok</span><span class="sxs-lookup"><span data-stu-id="b51db-184">Next step</span></span>

* [<span data-ttu-id="b51db-185">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b51db-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b51db-186">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b51db-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

