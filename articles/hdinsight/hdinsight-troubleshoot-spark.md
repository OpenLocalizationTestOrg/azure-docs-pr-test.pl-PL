---
title: "aaaTroubleshoot Spark przy użyciu usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon dotyczące pracy z Apache Spark i usłudze Azure HDInsight."
keywords: "Usługa Azure HDInsight, Spark, często zadawane pytania, rozwiązywanie problemów z przewodnika, typowe problemy, konfiguracji aplikacji, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="fd92e-104">Rozwiązywanie problemów z Spark przy użyciu usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd92e-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="fd92e-105">Dowiedz się więcej o hello Najważniejsze problemy i rozwiązania ich podczas pracy z ładunków Apache Spark w Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="fd92e-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="fd92e-106">Jak skonfigurować aplikacji Spark przy użyciu Ambari w klastrach</span><span class="sxs-lookup"><span data-stu-id="fd92e-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="fd92e-107">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd92e-107">Resolution steps</span></span>

<span data-ttu-id="fd92e-108">wartości konfiguracji Hello do wykonania tej procedury wcześniej zostały ustawione w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd92e-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="fd92e-109">Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="fd92e-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="fd92e-110">Na liście hello klastrów, wybierz **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Wybierz klaster z listy](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="fd92e-112">Wybierz hello **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="fd92e-112">Select hello **Configs** tab.</span></span>

    ![Wybierz kartę Configs hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="fd92e-114">Na liście hello konfiguracji, wybierz **niestandardowe spark2-domyślne**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Wybierz niestandardowe spark — ustawienia domyślne](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="fd92e-116">Wyszukaj wartości hello ustawienie muszą tooadjust, takich jak **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="fd92e-117">W takim przypadku hello wartość **4608m** jest zbyt duża.</span><span class="sxs-lookup"><span data-stu-id="fd92e-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Wybierz pole spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="fd92e-119">Zestaw hello wartość toohello zalecane ustawienie.</span><span class="sxs-lookup"><span data-stu-id="fd92e-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="fd92e-120">Witaj wartość **2048m** jest zalecane dla tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fd92e-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Zmień wartość too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="fd92e-122">Zapisz hello wartość, a następnie zapisz hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fd92e-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="fd92e-123">Na pasku narzędzi hello, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-123">On hello toolbar, select **Save**.</span></span>

    ![Zapisz ustawienia hello i konfiguracji](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="fd92e-125">Użytkownik jest powiadamiany, jeśli wszystkie konfiguracje wymagają uwagi.</span><span class="sxs-lookup"><span data-stu-id="fd92e-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="fd92e-126">Zanotuj hello elementy, a następnie wybierz **kontynuować mimo to**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Wybierz kontynuować mimo to](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="fd92e-128">Wpisz notatkę o hello zmian konfiguracji, a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Wprowadź notatkę dotyczącą wprowadzone zmiany hello](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="fd92e-130">Zawsze, gdy konfiguracja jest zapisywana, zostanie wyświetlony monit toorestart hello usługi.</span><span class="sxs-lookup"><span data-stu-id="fd92e-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="fd92e-131">Wybierz **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-131">Select **Restart**.</span></span>

    ![Uruchom ponownie](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="fd92e-133">Potwierdź hello ponownego uruchomienia komputera.</span><span class="sxs-lookup"><span data-stu-id="fd92e-133">Confirm hello restart.</span></span>

    ![Wybierz upewnij się, uruchom ponownie wszystkie](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="fd92e-135">Możesz przejrzeć hello procesów, które są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="fd92e-135">You can review hello processes that are running.</span></span>

    ![Przejrzyj uruchomione procesy](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="fd92e-137">Można dodać konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="fd92e-137">You can add configurations.</span></span> <span data-ttu-id="fd92e-138">Liście hello konfiguracji wybierz **niestandardowe spark2-domyślne**, a następnie wybierz **Dodaj właściwość**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Wybierz opcję Dodaj właściwość](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="fd92e-140">Zdefiniuj nową właściwość.</span><span class="sxs-lookup"><span data-stu-id="fd92e-140">Define a new property.</span></span> <span data-ttu-id="fd92e-141">Za pomocą okna dialogowego dotyczące konkretnych ustawień, takich jak typ danych hello można zdefiniować jednej właściwości.</span><span class="sxs-lookup"><span data-stu-id="fd92e-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="fd92e-142">Alternatywnie można zdefiniować wiele właściwości, za pomocą jednej definicji w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="fd92e-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="fd92e-143">W tym przykładzie hello **spark.driver.memory** zdefiniowano właściwość z wartością **4g**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Zdefiniuj nową właściwość](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="fd92e-145">Zapisz konfigurację hello, a następnie ponownie uruchom usługę hello, zgodnie z opisem w kroku 6 i 7.</span><span class="sxs-lookup"><span data-stu-id="fd92e-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="fd92e-146">Te zmiany są całego klastra, ale może zostać zastąpiona po przesłaniu zadania Spark hello.</span><span class="sxs-lookup"><span data-stu-id="fd92e-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="fd92e-147">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="fd92e-147">Additional reading</span></span>

[<span data-ttu-id="fd92e-148">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd92e-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="fd92e-149">Jak skonfigurować aplikacji Spark przy użyciu notesu Jupyter w klastrze</span><span class="sxs-lookup"><span data-stu-id="fd92e-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="fd92e-150">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd92e-150">Resolution steps</span></span>

1. <span data-ttu-id="fd92e-151">Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="fd92e-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="fd92e-152">W pierwszej komórki hello notesu Jupyter hello, po hello **%% skonfigurować** dyrektywy, określ konfiguracje Spark hello prawidłowy format JSON.</span><span class="sxs-lookup"><span data-stu-id="fd92e-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="fd92e-153">Ustaw wartości rzeczywistych hello:</span><span class="sxs-lookup"><span data-stu-id="fd92e-153">Change hello actual values as necessary:</span></span>

    ![Dodaj konfigurację](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="fd92e-155">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="fd92e-155">Additional reading</span></span>

[<span data-ttu-id="fd92e-156">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd92e-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="fd92e-157">Jak skonfigurować aplikacji Spark przy użyciu programu Livy w klastrach</span><span class="sxs-lookup"><span data-stu-id="fd92e-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="fd92e-158">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd92e-158">Resolution steps</span></span>

1. <span data-ttu-id="fd92e-159">Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="fd92e-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="fd92e-160">Przesyłanie tooLivy aplikacji Spark hello przy użyciu klienta REST, takich jak cURL.</span><span class="sxs-lookup"><span data-stu-id="fd92e-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="fd92e-161">Użyj polecenia podobne następującego toohello.</span><span class="sxs-lookup"><span data-stu-id="fd92e-161">Use a command similar toohello following.</span></span> <span data-ttu-id="fd92e-162">Ustaw wartości rzeczywistych hello:</span><span class="sxs-lookup"><span data-stu-id="fd92e-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="fd92e-163">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="fd92e-163">Additional reading</span></span>

[<span data-ttu-id="fd92e-164">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd92e-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="fd92e-165">Jak skonfigurować Spark, przesłać spark aplikacji przy użyciu w klastrach</span><span class="sxs-lookup"><span data-stu-id="fd92e-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="fd92e-166">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd92e-166">Resolution steps</span></span>

1. <span data-ttu-id="fd92e-167">Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="fd92e-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="fd92e-168">Uruchom powłokę spark przy użyciu polecenia podobne następującego toohello.</span><span class="sxs-lookup"><span data-stu-id="fd92e-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="fd92e-169">Ustaw wartość rzeczywista hello hello konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fd92e-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="fd92e-170">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="fd92e-170">Additional reading</span></span>

[<span data-ttu-id="fd92e-171">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd92e-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="fd92e-172">Dlaczego Spark wyjątek OutofMemoryError aplikacji</span><span class="sxs-lookup"><span data-stu-id="fd92e-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="fd92e-173">Szczegółowy opis</span><span class="sxs-lookup"><span data-stu-id="fd92e-173">Detailed description</span></span>

<span data-ttu-id="fd92e-174">Witaj aplikacji Spark kończy się niepowodzeniem z hello następujące typy nieprzechwyconych wyjątków:</span><span class="sxs-lookup"><span data-stu-id="fd92e-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a><span data-ttu-id="fd92e-175">Prawdopodobna przyczyna</span><span class="sxs-lookup"><span data-stu-id="fd92e-175">Probable cause</span></span>

<span data-ttu-id="fd92e-176">Witaj najbardziej prawdopodobną przyczyną tego wyjątku jest, że nie ma wystarczającej ilości pamięci sterty jest przydzielona maszyny wirtualnej Java toohello (JVMs).</span><span class="sxs-lookup"><span data-stu-id="fd92e-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="fd92e-177">Te JVMs będą uruchamiane jako modułów lub sterowniki jako część hello aplikacji Spark.</span><span class="sxs-lookup"><span data-stu-id="fd92e-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="fd92e-178">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd92e-178">Resolution steps</span></span>

1. <span data-ttu-id="fd92e-179">Określ maksymalny rozmiar hello dojść Spark hello hello danych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fd92e-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="fd92e-180">Możesz wprowadzić wynik, na podstawie maksymalnego rozmiaru hello hello danych wejściowych, hello pośrednich danych wytworzonego przez przekształcania danych wejściowych hello i danych wyjściowych hello utworzonym podczas aplikacji hello jest dalsze przekształcania hello pośrednich danych.</span><span class="sxs-lookup"><span data-stu-id="fd92e-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="fd92e-181">Ten proces może zająć iteracyjną, jeśli nie możesz początkowej formalnego argumentu.</span><span class="sxs-lookup"><span data-stu-id="fd92e-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="fd92e-182">Upewnij się, ma toouse ma za mało zasobów pod względem pamięci i rdzeni aplikacji Spark hello tooaccommodate klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fd92e-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="fd92e-183">Można to określić, wyświetlając hello klastra metryki części hello interfejsie użytkownika YARN hello wartości z **pamięć używana** vs. **Całkowita liczba pamięci**, i **VCores używane** vs. **Łączna liczba VCores**.</span><span class="sxs-lookup"><span data-stu-id="fd92e-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="fd92e-184">Ustaw wartości tooappropriate konfiguracje, które nie może przekraczać 90% hello dostępnej pamięci i rdzeni powitania po Spark.</span><span class="sxs-lookup"><span data-stu-id="fd92e-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="fd92e-185">Witaj wartości powinny być również w ramach wymagań pamięci hello hello aplikacji Spark:</span><span class="sxs-lookup"><span data-stu-id="fd92e-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="fd92e-186">tooget hello ilość pamięci używana przez wszystkich modułów, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fd92e-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="fd92e-187">tooget hello suma pamięci używanej przez sterownik hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fd92e-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="fd92e-188">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="fd92e-188">Additional reading</span></span>

- [<span data-ttu-id="fd92e-189">Omówienie zarządzania pamięci Spark</span><span class="sxs-lookup"><span data-stu-id="fd92e-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="fd92e-190">Debugowanie aplikacji Spark w klastrze usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd92e-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

