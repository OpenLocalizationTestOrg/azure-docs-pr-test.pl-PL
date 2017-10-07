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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Rozwiązywanie problemów z Spark przy użyciu usługi Azure HDInsight

Dowiedz się więcej o hello Najważniejsze problemy i rozwiązania ich podczas pracy z ładunków Apache Spark w Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Jak skonfigurować aplikacji Spark przy użyciu Ambari w klastrach

### <a name="resolution-steps"></a>Kroki rozwiązania

wartości konfiguracji Hello do wykonania tej procedury wcześniej zostały ustawione w usłudze HDInsight. Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. Na liście hello klastrów, wybierz **Spark2**.

    ![Wybierz klaster z listy](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Wybierz hello **Configs** kartę.

    ![Wybierz kartę Configs hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. Na liście hello konfiguracji, wybierz **niestandardowe spark2-domyślne**.

    ![Wybierz niestandardowe spark — ustawienia domyślne](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Wyszukaj wartości hello ustawienie muszą tooadjust, takich jak **spark.executor.memory**. W takim przypadku hello wartość **4608m** jest zbyt duża.

    ![Wybierz pole spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Zestaw hello wartość toohello zalecane ustawienie. Witaj wartość **2048m** jest zalecane dla tego ustawienia.

    ![Zmień wartość too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Zapisz hello wartość, a następnie zapisz hello konfiguracji. Na pasku narzędzi hello, wybierz **zapisać**.

    ![Zapisz ustawienia hello i konfiguracji](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Użytkownik jest powiadamiany, jeśli wszystkie konfiguracje wymagają uwagi. Zanotuj hello elementy, a następnie wybierz **kontynuować mimo to**. 

    ![Wybierz kontynuować mimo to](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Wpisz notatkę o hello zmian konfiguracji, a następnie wybierz **zapisać**.

    ![Wprowadź notatkę dotyczącą wprowadzone zmiany hello](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Zawsze, gdy konfiguracja jest zapisywana, zostanie wyświetlony monit toorestart hello usługi. Wybierz **ponownego uruchomienia**.

    ![Uruchom ponownie](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Potwierdź hello ponownego uruchomienia komputera.

    ![Wybierz upewnij się, uruchom ponownie wszystkie](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Możesz przejrzeć hello procesów, które są uruchomione.

    ![Przejrzyj uruchomione procesy](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. Można dodać konfiguracje. Liście hello konfiguracji wybierz **niestandardowe spark2-domyślne**, a następnie wybierz **Dodaj właściwość**.

    ![Wybierz opcję Dodaj właściwość](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Zdefiniuj nową właściwość. Za pomocą okna dialogowego dotyczące konkretnych ustawień, takich jak typ danych hello można zdefiniować jednej właściwości. Alternatywnie można zdefiniować wiele właściwości, za pomocą jednej definicji w każdym wierszu. 

    W tym przykładzie hello **spark.driver.memory** zdefiniowano właściwość z wartością **4g**.

    ![Zdefiniuj nową właściwość](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Zapisz konfigurację hello, a następnie ponownie uruchom usługę hello, zgodnie z opisem w kroku 6 i 7.

Te zmiany są całego klastra, ale może zostać zastąpiona po przesłaniu zadania Spark hello.

### <a name="additional-reading"></a>Dodatkowe materiały

[Przesyłanie zadań Spark w klastrach HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Jak skonfigurować aplikacji Spark przy użyciu notesu Jupyter w klastrze

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).

2. W pierwszej komórki hello notesu Jupyter hello, po hello **%% skonfigurować** dyrektywy, określ konfiguracje Spark hello prawidłowy format JSON. Ustaw wartości rzeczywistych hello:

    ![Dodaj konfigurację](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Dodatkowe materiały

[Przesyłanie zadań Spark w klastrach HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Jak skonfigurować aplikacji Spark przy użyciu programu Livy w klastrach

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Przesyłanie tooLivy aplikacji Spark hello przy użyciu klienta REST, takich jak cURL. Użyj polecenia podobne następującego toohello. Ustaw wartości rzeczywistych hello:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Dodatkowe materiały

[Przesyłanie zadań Spark w klastrach HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Jak skonfigurować Spark, przesłać spark aplikacji przy użyciu w klastrach

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Zobacz toodetermine konfiguracje Spark, które muszą wartości zestawu i toowhat toobe [co powoduje Spark wyjątek OutofMemoryError aplikacji](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Uruchom powłokę spark przy użyciu polecenia podobne następującego toohello. Ustaw wartość rzeczywista hello hello konfiguracji: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Dodatkowe materiały

[Przesyłanie zadań Spark w klastrach HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Dlaczego Spark wyjątek OutofMemoryError aplikacji

### <a name="detailed-description"></a>Szczegółowy opis

Witaj aplikacji Spark kończy się niepowodzeniem z hello następujące typy nieprzechwyconych wyjątków:

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

### <a name="probable-cause"></a>Prawdopodobna przyczyna

Witaj najbardziej prawdopodobną przyczyną tego wyjątku jest, że nie ma wystarczającej ilości pamięci sterty jest przydzielona maszyny wirtualnej Java toohello (JVMs). Te JVMs będą uruchamiane jako modułów lub sterowniki jako część hello aplikacji Spark. 

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Określ maksymalny rozmiar hello dojść Spark hello hello danych w aplikacji. Możesz wprowadzić wynik, na podstawie maksymalnego rozmiaru hello hello danych wejściowych, hello pośrednich danych wytworzonego przez przekształcania danych wejściowych hello i danych wyjściowych hello utworzonym podczas aplikacji hello jest dalsze przekształcania hello pośrednich danych. Ten proces może zająć iteracyjną, jeśli nie możesz początkowej formalnego argumentu. 

2. Upewnij się, ma toouse ma za mało zasobów pod względem pamięci i rdzeni aplikacji Spark hello tooaccommodate klastra usługi HDInsight hello. Można to określić, wyświetlając hello klastra metryki części hello interfejsie użytkownika YARN hello wartości z **pamięć używana** vs. **Całkowita liczba pamięci**, i **VCores używane** vs. **Łączna liczba VCores**.

3. Ustaw wartości tooappropriate konfiguracje, które nie może przekraczać 90% hello dostępnej pamięci i rdzeni powitania po Spark. Witaj wartości powinny być również w ramach wymagań pamięci hello hello aplikacji Spark: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget hello ilość pamięci używana przez wszystkich modułów, uruchom następujące polecenie hello: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget hello suma pamięci używanej przez sterownik hello, uruchom następujące polecenie hello:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Dodatkowe materiały

- [Omówienie zarządzania pamięci Spark](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Debugowanie aplikacji Spark w klastrze usługi HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

