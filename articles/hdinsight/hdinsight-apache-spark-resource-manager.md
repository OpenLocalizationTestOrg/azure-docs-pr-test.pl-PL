---
title: "klaster zasobów aaaManage platformy Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zarządzanie zasobami klastry Spark w usłudze Azure HDInsight w celu zapewnienia lepszej wydajności."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight 

W tym artykule dowiesz się, jak skojarzonych z interfejsami hello tooaccess jak interfejsu użytkownika narzędzia Ambari, interfejsie użytkownika YARN i hello Spark historii serwera w klastrze Spark. Możesz także informacje dotyczące sposobu tootune hello konfiguracji klastra, aby zapewnić optymalną wydajność.

**Wymagania wstępne:**

Musi mieć następujące hello:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Jak uruchomić hello Interfejsu sieci Web Ambari?
1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.
2. W bloku klastra Spark powitania kliknij **pulpitu nawigacyjnego**. Po wyświetleniu monitu wprowadź poświadczenia administratora hello hello klastra Spark.

    ![Uruchamianie narzędzia Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Uruchom Menedżera zasobów")
3. Powinno to uruchomienie hello Interfejsu sieci Web Ambari, jak pokazano poniżej.

    ![Interfejs użytkownika sieci Web Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Jak uruchomić powitania serwera historii Spark?
1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).
2. Z hello klastra bloku, w obszarze **szybkie linki**, kliknij przycisk **pulpit nawigacyjny klastra**. W hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **Spark historii serwera**.

    ![Platforma Spark jest serwer historii](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark historii serwera")

    Po wyświetleniu monitu wprowadź poświadczenia administratora hello hello klastra Spark.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Jak uruchomić hello interfejsie użytkownika Yarn?
Możesz użyć hello interfejsie użytkownika YARN toomonitor aplikacji, które są aktualnie uruchomione w klastrze Spark hello.

1. W bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **YARN**.

    ![Uruchom interfejs użytkownika YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Można również będzie można uruchomić hello interfejsie użytkownika YARN z hello interfejsu użytkownika narzędzia Ambari. toolaunch hello interfejsu użytkownika narzędzia Ambari, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**. Hello interfejsu użytkownika narzędzia Ambari, kliknij **YARN**, kliknij przycisk **szybkie linki**, kliknij pozycję Menedżer zasobów active hello, a następnie kliknij przycisk **interfejsu użytkownika Menedżera ResourceManager**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Co to jest aplikacji Spark toorun konfiguracji klastra optymalne hello?
Parametry klucza Hello trzech, które mogą służyć do konfiguracji platformy Spark w zależności od wymagań aplikacji są `spark.executor.instances`, `spark.executor.cores`, i `spark.executor.memory`. Moduł wykonujący jest uruchomiona aplikacji Spark. Działa na powitania węzła procesu roboczego, a jest odpowiedzialny toocarry zadań hello aplikacji hello. Witaj domyślna liczba modułów i hello rozmiary Moduł wykonujący dla każdego klastra jest obliczany na podstawie hello liczba węzłów procesu roboczego i rozmiaru węzła procesu roboczego hello. Są one przechowywane w `spark-defaults.conf` na powitania głównymi węzłami klastra.

Witaj trzy parametry konfiguracji można skonfigurować na poziomie klastra hello (dla wszystkich aplikacji uruchomionych w klastrze hello) lub można określić dla każdej poszczególnych aplikacji.

### <a name="change-hello-parameters-using-ambari-ui"></a>Zmień parametry hello za pomocą interfejsu użytkownika narzędzia Ambari
1. Hello interfejsu użytkownika narzędzia Ambari kliknij **Spark**, kliknij przycisk **Configs**, a następnie rozwiń węzeł **niestandardowe spark — domyślne**.

    ![Ustawianie parametrów przy użyciu narzędzia Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. wartości domyślne Hello są dobrym toohave 4 aplikacji Spark działać jednocześnie w klastrze hello. Możesz zmiany tych wartości z hello interfejsu użytkownika, jak pokazano poniżej.

    ![Ustawianie parametrów przy użyciu narzędzia Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Kliknij przycisk **zapisać** zmian konfiguracji hello toosave. U góry hello hello strony, zostanie wyświetlony monit toorestart wszystkie hello uwzględnione usługi. Kliknij przycisk **ponownego uruchomienia**.

    ![Uruchom ponownie usługi](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Zmiana parametrów hello aplikacji uruchomionej w notesu Jupyter
Dla aplikacji działających w notesu Jupyter hello, można użyć hello `%%configure` Magiczna zmian konfiguracji hello toomake. W idealnym przypadku należy takie zmiany na początku hello aplikacji hello, przed uruchomieniem pierwszej komórki kodu. Dzięki tej konfiguracji hello jest stosowane toohello Livy sesji, gdy zostanie utworzony. Jeśli konfiguracja hello toochange na późniejszym etapie w aplikacji hello, należy użyć hello `-f` parametru. Jednakże wykonując, wszystkie postęp w hello aplikacji zostaną utracone.

Poniższy fragment Hello pokazuje, jak toochange hello konfiguracji dla aplikacji działających w oprogramowaniu Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Parametry konfiguracji muszą być przekazywane w postaci ciągu JSON i musi być w następnym wierszu powitania po hello magic, jak pokazano w kolumnie przykład hello.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Przedstawia spark parametry hello zmiany przesłane za pomocą aplikacji
Następujące polecenia znajduje się przykład sposobu toochange hello parametry konfiguracji, dla której zostało przesłane za pomocą aplikacji partii `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Zmień parametry hello aplikacji przesłane przy użyciu programu cURL
Następujące polecenia jest przykładem sposobu toochange hello parametry konfiguracji, dla której zostało przesłane za pomocą przy użyciu programu cURL aplikacji partii.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Jak zmienić tych parametrów, na serwerze Spark Thrift?
Spark Thrift serwer udostępnia klastra Spark tooa dostępu JDBC/ODBC i używane tooservice zapytań Spark SQL. Narzędzia takie jak usługi Power BI, Tableau itp. za pomocą toocommunicate protokołu ODBC zapytań Spark SQL tooexecute Spark Thrift serwera jako aplikacji Spark. Po utworzeniu klastra Spark, dwa wystąpienia hello Spark Thrift serwera jest uruchomiona, i jeden w każdym węźle głównym. Każdy serwer Thrift Spark jest widoczny jako aplikacji Spark w interfejsie użytkownika YARN hello.

Używa Spark Thrift serwera Spark Moduł wykonujący dynamicznej alokacji i dlatego hello `spark.executor.instances` nie jest używany. Zamiast tego Spark Thrift serwer używa `spark.dynamicAllocation.minExecutors` i `spark.dynamicAllocation.maxExecutors` toospecify hello Moduł wykonujący count. Witaj parametry konfiguracji `spark.executor.cores` i `spark.executor.memory` jest używany rozmiar modułu wykonującego hello toomodify. Te parametry można zmienić, jak pokazano poniżej.

* Rozwiń węzeł hello **zaawansowane spark-thrift-sparkconf** kategorii tooupdate hello parametry `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, i `spark.executor.memory`.

    ![Konfigurowanie Spark thrift serwera](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Rozwiń węzeł hello **niestandardowe spark-thrift-sparkconf** kategorii tooupdate hello parametru `spark.executor.cores`.

    ![Konfigurowanie Spark thrift serwera](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Jak zmienić hello sterownik pamięci hello Spark Thrift serwera?
Spark Thrift sterownik pamięci jest skonfigurowany too25% hello rozmiaru węzła głównego pamięci RAM, podane całkowity rozmiar pamięci RAM hello węzła głównego hello jest większa niż 14GB. Można użyć hello konfiguracji pamięci interfejsu użytkownika narzędzia Ambari toochange hello sterownika, jak pokazano poniżej.

* Hello interfejsu użytkownika narzędzia Ambari kliknij **Spark**, kliknij przycisk **Configs**, rozwiń węzeł **zaawansowane spark env**, a następnie podaj wartość hello **spark_thrift_cmd_opts**.

    ![Konfigurowanie Spark thrift serwera pamięci RAM](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>BI nie jest używany z klastrem Spark. Jak ponownie zająć zasobów hello?
Ponieważ używamy Spark dynamiczna alokacja hello tylko tych zasobów, które są używane przez serwer thrift są hello zasobów dla dwóch głównych aplikacji hello. tooreclaim tych zasobów, które należy zatrzymać hello Thrift serwera usługi działające na powitania klastra.

1. Witaj interfejsu użytkownika narzędzia Ambari, w okienku po lewej stronie powitania kliknij **Spark**.
2. Na następnej stronie powitania kliknij **Spark Thrift serwerów**.

    ![Uruchom ponownie serwer thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Powinny pojawić się dwa headnodes hello, na które hello Spark Thrift serwer jest uruchomiony. Kliknij jeden z hello headnodes.

    ![Uruchom ponownie serwer thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. Hello Następna strona zawiera listę wszystkich usług hello uruchomionych na tym headnode. Z listy powitania kliknij przycisk Dalej tooSpark przycisku rozwijanego powitania serwera Thrift, a następnie kliknij **zatrzymać**.

    ![Uruchom ponownie serwer thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Powtórz te czynności na powitania również inne headnode.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>Moje notesów Jupyter nie działają zgodnie z oczekiwaniami. Jak można ponownie uruchomić usługę hello?
Uruchom hello Interfejsu sieci Web Ambari, zgodnie z powyższym. W okienku nawigacji po lewej stronie powitania kliknij **Jupyter**, kliknij przycisk **akcji usługi**, a następnie kliknij przycisk **ponowne uruchomienie wszystkich**. Spowoduje to uruchomienie usługi Jupyter hello na wszystkich headnodes hello.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Jak sprawdzić, jeśli używam wszystkich zasobów?
Uruchom hello interfejsie użytkownika Yarn, zgodnie z powyższym. W tabeli metrykę klastra na ekranie powitania, sprawdź wartości **pamięć używana** i **całkowitej pamięci** kolumn. Jeśli wartości hello 2 są bardzo bliskiej, może nie być wystarczającej ilości zasobów toostart hello następnej aplikacji. Witaj dotyczy to również toohello **VCores używane** i **łącznie VCores** kolumn. Ponadto w hello widoku głównego, w przypadku aplikacji przebywanie w **ZAAKCEPTOWANE** stanu i nie są przenoszone do **systemem** ani **nie powiodło się** stanu, przyczyną może być również wskazanie czy nie otrzymuje toostart wystarczającej ilości zasobów.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Jak kill uruchomionej aplikacji toofree się zasobów?
1. W hello interfejsie użytkownika Yarn z lewego panelu powitania kliknij **systemem**. Z listy hello uruchomionych aplikacji, sprawdź toobe aplikacji hello skasowane i kliknij na powitania **identyfikator**.

    ![Kasowanie App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")

2. Kliknij przycisk **Kill aplikacji** na powitania prawym górnym rogu, następnie kliknij przycisk **OK**.

    ![Kasowanie App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")

## <a name="see-also"></a>Zobacz też
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>Dla analityków danych

* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Dla deweloperów platformy Spark

* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
