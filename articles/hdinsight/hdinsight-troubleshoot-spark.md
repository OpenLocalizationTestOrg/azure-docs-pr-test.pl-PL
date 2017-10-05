---
title: "Rozwiązywanie problemów z Spark przy użyciu usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na często zadawane pytania na temat pracy z Apache Spark i usłudze Azure HDInsight."
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
ms.openlocfilehash: cfed5f0f4f703821e83e3d365810c0e5ad22f035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="1cca7-104">Rozwiązywanie problemów z Spark przy użyciu usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cca7-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="1cca7-105">Dowiedz się więcej o Najważniejsze problemy i rozwiązania ich podczas pracy z ładunków Apache Spark w Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="1cca7-105">Learn about the top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="1cca7-106">Jak skonfigurować aplikacji Spark przy użyciu Ambari w klastrach</span><span class="sxs-lookup"><span data-stu-id="1cca7-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="1cca7-107">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1cca7-107">Resolution steps</span></span>

<span data-ttu-id="1cca7-108">Wartości konfiguracji do wykonania tej procedury wcześniej zostały ustawione w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1cca7-108">The configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="1cca7-109">Aby określić, które Spark konfiguracje trzeba ustawić i jakie wartości, zobacz [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="1cca7-109">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="1cca7-110">Na liście klastrów, wybierz **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-110">In the list of clusters, select **Spark2**.</span></span>

    ![Wybierz klaster z listy](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="1cca7-112">Wybierz **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="1cca7-112">Select the **Configs** tab.</span></span>

    ![Wybierz kartę Configs](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="1cca7-114">Na liście konfiguracji, wybierz **niestandardowe spark2-domyślne**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-114">In the list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Wybierz niestandardowe spark — ustawienia domyślne](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="1cca7-116">Wyszukaj ustawienie wartości, które należy dopasować, takich jak **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-116">Look for the value setting that you need to adjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="1cca7-117">W takim przypadku wartość **4608m** jest zbyt duża.</span><span class="sxs-lookup"><span data-stu-id="1cca7-117">In this case, the value of **4608m** is too high.</span></span>

    ![Wybierz pole spark.executor.memory](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="1cca7-119">Wartość to ustawienie zalecane.</span><span class="sxs-lookup"><span data-stu-id="1cca7-119">Set the value to the recommended setting.</span></span> <span data-ttu-id="1cca7-120">Wartość **2048m** jest zalecane dla tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1cca7-120">The value **2048m** is recommended for this setting.</span></span>

    ![Zmień wartość na 2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="1cca7-122">Zapisz wartość, a następnie zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="1cca7-122">Save the value, and then save the configuration.</span></span> <span data-ttu-id="1cca7-123">Na pasku narzędzi wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-123">On the toolbar, select **Save**.</span></span>

    ![Zapisz ustawienia i Konfiguracja](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="1cca7-125">Użytkownik jest powiadamiany, jeśli wszystkie konfiguracje wymagają uwagi.</span><span class="sxs-lookup"><span data-stu-id="1cca7-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="1cca7-126">Należy pamiętać, elementy, a następnie wybierz **kontynuować mimo to**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-126">Note the items, and then select **Proceed Anyway**.</span></span> 

    ![Wybierz kontynuować mimo to](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="1cca7-128">Wpisz notatkę o zmiany konfiguracji, a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-128">Write a note about the configuration changes, and then select **Save**.</span></span>

    ![Wprowadź notatkę dotyczącą wprowadzone zmiany](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="1cca7-130">Zawsze, gdy konfiguracja jest zapisywana, zostanie wyświetlony monit ponownie uruchom usługę.</span><span class="sxs-lookup"><span data-stu-id="1cca7-130">Whenever a configuration is saved, you are prompted to restart the service.</span></span> <span data-ttu-id="1cca7-131">Wybierz **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-131">Select **Restart**.</span></span>

    ![Uruchom ponownie](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="1cca7-133">Upewnij się, ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="1cca7-133">Confirm the restart.</span></span>

    ![Wybierz upewnij się, uruchom ponownie wszystkie](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="1cca7-135">Możesz przejrzeć procesów, które są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="1cca7-135">You can review the processes that are running.</span></span>

    ![Przejrzyj uruchomione procesy](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="1cca7-137">Można dodać konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="1cca7-137">You can add configurations.</span></span> <span data-ttu-id="1cca7-138">Na liście konfiguracji, wybierz **niestandardowe spark2-ustawienia domyślne**, a następnie wybierz **Dodaj właściwość**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-138">In the list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Wybierz opcję Dodaj właściwość](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="1cca7-140">Zdefiniuj nową właściwość.</span><span class="sxs-lookup"><span data-stu-id="1cca7-140">Define a new property.</span></span> <span data-ttu-id="1cca7-141">Za pomocą okna dialogowego dotyczące konkretnych ustawień, takich jak typ danych można zdefiniować jednej właściwości.</span><span class="sxs-lookup"><span data-stu-id="1cca7-141">You can define a single property by using a dialog box for specific settings such as the data type.</span></span> <span data-ttu-id="1cca7-142">Alternatywnie można zdefiniować wiele właściwości, za pomocą jednej definicji w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="1cca7-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="1cca7-143">W tym przykładzie **spark.driver.memory** zdefiniowano właściwość z wartością **4g**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-143">In this example, the **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Zdefiniuj nową właściwość](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="1cca7-145">Zapisz konfigurację, a następnie uruchom ponownie usługę, zgodnie z opisem w kroku 6 i 7.</span><span class="sxs-lookup"><span data-stu-id="1cca7-145">Save the configuration, and then restart the service as described in steps 6 and 7.</span></span>

<span data-ttu-id="1cca7-146">Te zmiany są całego klastra, ale może zostać zastąpiona po przesłaniu zadania Spark.</span><span class="sxs-lookup"><span data-stu-id="1cca7-146">These changes are cluster-wide but can be overridden when you submit the Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="1cca7-147">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="1cca7-147">Additional reading</span></span>

[<span data-ttu-id="1cca7-148">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cca7-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="1cca7-149">Jak skonfigurować aplikacji Spark przy użyciu notesu Jupyter w klastrze</span><span class="sxs-lookup"><span data-stu-id="1cca7-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="1cca7-150">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1cca7-150">Resolution steps</span></span>

1. <span data-ttu-id="1cca7-151">Aby określić, które Spark konfiguracje trzeba ustawić i jakie wartości, zobacz [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="1cca7-151">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="1cca7-152">W pierwszej komórki notesu Jupyter po **%% skonfigurować** dyrektywy, określ konfiguracje Spark prawidłowy format JSON.</span><span class="sxs-lookup"><span data-stu-id="1cca7-152">In the first cell of the Jupyter notebook, after the **%%configure** directive, specify the Spark configurations in valid JSON format.</span></span> <span data-ttu-id="1cca7-153">Ustaw rzeczywistymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="1cca7-153">Change the actual values as necessary:</span></span>

    ![Dodaj konfigurację](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="1cca7-155">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="1cca7-155">Additional reading</span></span>

[<span data-ttu-id="1cca7-156">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cca7-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="1cca7-157">Jak skonfigurować aplikacji Spark przy użyciu programu Livy w klastrach</span><span class="sxs-lookup"><span data-stu-id="1cca7-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="1cca7-158">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1cca7-158">Resolution steps</span></span>

1. <span data-ttu-id="1cca7-159">Aby określić, które Spark konfiguracje trzeba ustawić i jakie wartości, zobacz [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="1cca7-159">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="1cca7-160">Przesyłanie aplikacji Spark Livy przy użyciu klienta REST, takich jak cURL.</span><span class="sxs-lookup"><span data-stu-id="1cca7-160">Submit the Spark application to Livy by using a REST client like cURL.</span></span> <span data-ttu-id="1cca7-161">Polecenie podobne do następującego.</span><span class="sxs-lookup"><span data-stu-id="1cca7-161">Use a command similar to the following.</span></span> <span data-ttu-id="1cca7-162">Ustaw rzeczywistymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="1cca7-162">Change the actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="1cca7-163">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="1cca7-163">Additional reading</span></span>

[<span data-ttu-id="1cca7-164">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cca7-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="1cca7-165">Jak skonfigurować Spark, przesłać spark aplikacji przy użyciu w klastrach</span><span class="sxs-lookup"><span data-stu-id="1cca7-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="1cca7-166">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1cca7-166">Resolution steps</span></span>

1. <span data-ttu-id="1cca7-167">Aby określić, które Spark konfiguracje trzeba ustawić i jakie wartości, zobacz [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="1cca7-167">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="1cca7-168">Uruchom powłokę spark przy użyciu polecenia podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="1cca7-168">Launch spark-shell by using a command similar to the following.</span></span> <span data-ttu-id="1cca7-169">Ustaw wartość rzeczywistą konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="1cca7-169">Change the actual value of the configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="1cca7-170">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="1cca7-170">Additional reading</span></span>

[<span data-ttu-id="1cca7-171">Przesyłanie zadań Spark w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cca7-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="1cca7-172">Dlaczego Spark wyjątek OutofMemoryError aplikacji</span><span class="sxs-lookup"><span data-stu-id="1cca7-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="1cca7-173">Szczegółowy opis</span><span class="sxs-lookup"><span data-stu-id="1cca7-173">Detailed description</span></span>

<span data-ttu-id="1cca7-174">Aplikacji Spark kończy się niepowodzeniem z następujących typów nieprzechwyconych wyjątków:</span><span class="sxs-lookup"><span data-stu-id="1cca7-174">The Spark application fails, with the following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="1cca7-175">Prawdopodobna przyczyna</span><span class="sxs-lookup"><span data-stu-id="1cca7-175">Probable cause</span></span>

<span data-ttu-id="1cca7-176">Najbardziej prawdopodobną przyczyną tego wyjątku jest, że nie ma wystarczającej ilości pamięci sterty jest przydzielona do maszyny wirtualnej Java (JVMs).</span><span class="sxs-lookup"><span data-stu-id="1cca7-176">The most likely cause of this exception is that not enough heap memory is allocated to the Java virtual machines (JVMs).</span></span> <span data-ttu-id="1cca7-177">Te JVMs będą uruchamiane jako modułów lub sterowniki jako część aplikacji Spark.</span><span class="sxs-lookup"><span data-stu-id="1cca7-177">These JVMs are launched as executors or drivers as part of the Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="1cca7-178">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1cca7-178">Resolution steps</span></span>

1. <span data-ttu-id="1cca7-179">Maksymalny rozmiar danych Spark dojść do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cca7-179">Determine the maximum size of the data the Spark application handles.</span></span> <span data-ttu-id="1cca7-180">Możesz wprowadzić wynik, na podstawie maksymalnego rozmiaru danych wejściowych, pośrednich danych, który jest generowany przez przekształcania danych wejściowych i danych wyjściowych, który jest generowany, gdy aplikacja jest dalsze przekształcanie pośrednich danych.</span><span class="sxs-lookup"><span data-stu-id="1cca7-180">You can make a guess based on the maximum size of the input data, the intermediate data that's produced by transforming the input data, and the output data that's produced when the application is further transforming the intermediate data.</span></span> <span data-ttu-id="1cca7-181">Ten proces może zająć iteracyjną, jeśli nie możesz początkowej formalnego argumentu.</span><span class="sxs-lookup"><span data-stu-id="1cca7-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="1cca7-182">Upewnij się, że klaster usługi HDInsight, który ma być używana ma wystarczające zasoby pamięci i rdzeni, aby zmieścił się w aplikacji Spark.</span><span class="sxs-lookup"><span data-stu-id="1cca7-182">Make sure that the HDInsight cluster that you're going to use has enough resources in terms of memory and cores to accommodate the Spark application.</span></span> <span data-ttu-id="1cca7-183">Można to określić, wyświetlając sekcji metryki klastra w interfejsie użytkownika YARN dla wartości **pamięć używana** vs. **Całkowita liczba pamięci**, i **VCores używane** vs. **Łączna liczba VCores**.</span><span class="sxs-lookup"><span data-stu-id="1cca7-183">You can determine this by viewing the cluster metrics section of the YARN UI for the values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="1cca7-184">Ustaw następujące konfiguracje Spark na odpowiednie wartości, które nie może przekraczać 90% dostępnej pamięci i rdzeni.</span><span class="sxs-lookup"><span data-stu-id="1cca7-184">Set the following Spark configurations to appropriate values, which should not exceed 90% of the available memory and cores.</span></span> <span data-ttu-id="1cca7-185">Wartości powinny być dobrze w wymagania dotyczące pamięci aplikacji Spark:</span><span class="sxs-lookup"><span data-stu-id="1cca7-185">The values should be well within the memory requirements of the Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="1cca7-186">Aby uzyskać łączna ilość pamięci używana przez wszystkich modułów, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1cca7-186">To get the total memory used by all executors, run the following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="1cca7-187">Aby uzyskać suma pamięci używanej przez sterownik, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1cca7-187">To get the total memory used by the driver, run the following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="1cca7-188">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="1cca7-188">Additional reading</span></span>

- [<span data-ttu-id="1cca7-189">Omówienie zarządzania pamięci Spark</span><span class="sxs-lookup"><span data-stu-id="1cca7-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="1cca7-190">Debugowanie aplikacji Spark w klastrze usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="1cca7-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

