---
title: "Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać zarządzanie zasobami klastry Spark w usłudze Azure HDInsight w celu zapewnienia lepszej wydajności."
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
ms.openlocfilehash: 952fa15162a40bccb3f8c7a88508556757ca6675
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight 

W w tym artykule przedstawiono sposób uzyskać dostępu do interfejsów, takich jak Ambari interfejsie użytkownika YARN interfejsu użytkownika, i serwerze historii Spark skojarzone z klastrem Spark. Możesz także informacje dotyczące sposobu dostosowywania konfiguracji klastra, aby zapewnić optymalną wydajność.

**Wymagania wstępne:**

Należy dysponować następującymi elementami:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-the-ambari-web-ui"></a>Jak uruchomić interfejs użytkownika sieci Web Ambari?
1. W [Portalu Azure](https://portal.azure.com/) na tablicy startowej kliknij kafelek klastra Spark (jeśli został przypięty do tablicy startowej). Możesz także przejść do klastra, wybierając polecenia **Przeglądaj wszystko** > **Klastry usługi HDInsight**.
2. W bloku klastra Spark kliknij **pulpitu nawigacyjnego**. Po wyświetleniu monitu wprowadź poświadczenia administratora klastra Spark.

    ![Uruchamianie narzędzia Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Uruchom Menedżera zasobów")
3. Powinno to uruchomienie Interfejsu sieci Web Ambari, jak pokazano poniżej.

    ![Interfejs użytkownika sieci Web Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")   

## <a name="how-do-i-launch-the-spark-history-server"></a>Jak uruchomić serwera historii Spark?
1. W [Portalu Azure](https://portal.azure.com/) na tablicy startowej kliknij kafelek klastra Spark (jeśli został przypięty do tablicy startowej).
2. W bloku klastra w obszarze **szybkie linki**, kliknij przycisk **pulpit nawigacyjny klastra**. W **pulpit nawigacyjny klastra** bloku, kliknij przycisk **Spark historii serwera**.

    ![Platforma Spark jest serwer historii](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark historii serwera")

    Po wyświetleniu monitu wprowadź poświadczenia administratora klastra Spark.

## <a name="how-do-i-launch-the-yarn-ui"></a>Jak uruchomić interfejs użytkownika Yarn?
Interfejs użytkownika YARN służy do monitorowania aplikacji, które są aktualnie uruchomione w klastrze Spark.

1. W bloku klastra, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **YARN**.

    ![Uruchom interfejs użytkownika YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Alternatywnie można również uruchomić interfejsie użytkownika YARN z poziomu interfejsu użytkownika narzędzia Ambari. Aby uruchomić interfejs użytkownika narzędzia Ambari w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**. W interfejsie użytkownika narzędzia Ambari, kliknij przycisk **YARN**, kliknij przycisk **szybkie linki**, kliknij pozycję Menedżer zasobów aktywne, a następnie kliknij przycisk **interfejsu użytkownika Menedżera ResourceManager**.
   >
   >

## <a name="what-is-the-optimum-cluster-configuration-to-run-spark-applications"></a>Co to jest Konfiguracja klastra optymalne do uruchamiania aplikacji Spark?
Są trzy parametry kluczy, które mogą służyć do konfiguracji platformy Spark w zależności od wymagań aplikacji `spark.executor.instances`, `spark.executor.cores`, i `spark.executor.memory`. Moduł wykonujący jest uruchomiona aplikacji Spark. Działa w węźle procesu roboczego, a odpowiada do wykonywania zadań dla aplikacji. Domyślna liczba modułów i rozmiary Moduł wykonujący dla każdego klastra jest obliczany na podstawie liczby węzłów procesu roboczego i rozmiaru węzła procesu roboczego. Są one przechowywane w `spark-defaults.conf` na głównymi węzłami klastra.

Parametry trzech konfiguracji można skonfigurować na poziomie klastra (dla wszystkich aplikacji, które są uruchamiane w klastrze) lub można określić dla każdej poszczególnych aplikacji.

### <a name="change-the-parameters-using-ambari-ui"></a>Zmień parametry za pomocą interfejsu użytkownika narzędzia Ambari
1. W interfejsie użytkownika narzędzia Ambari kliknij **Spark**, kliknij przycisk **Configs**, a następnie rozwiń węzeł **niestandardowe spark — domyślne**.

    ![Ustawianie parametrów przy użyciu narzędzia Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. Wartości domyślne są warto mieć 4 Spark aplikacje są uruchamiane jednocześnie w klastrze. Możesz zmiany tych wartości, przy użyciu interfejsu użytkownika, jak pokazano poniżej.

    ![Ustawianie parametrów przy użyciu narzędzia Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Kliknij przycisk **zapisać** można zapisać zmian konfiguracji. W górnej części strony pojawi się monit o ponowne uruchomienie wszystkich odpowiednich usług. Kliknij przycisk **ponownego uruchomienia**.

    ![Uruchom ponownie usługi](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-the-parameters-for-an-application-running-in-jupyter-notebook"></a>Zmień parametry dla aplikacji działających w notesu Jupyter
W przypadku aplikacji uruchomionych w notesu Jupyter, można użyć `%%configure` magic zmian konfiguracji. W idealnym przypadku należy takie zmiany na początku aplikacji, przed uruchomieniem pierwszej komórki kodu. Dzięki temu, że konfiguracja zostanie zastosowana do sesji programu Livy, gdy zostanie utworzony. Jeśli chcesz zmienić konfigurację na późniejszym etapie w aplikacji, należy użyć `-f` parametru. Jednak przez grozi postępu wszystkich w aplikacji zostaną utracone.

Poniższy fragment pokazano, jak zmiana konfiguracji dla aplikacji działających w oprogramowaniu Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Parametry konfiguracji muszą być przekazywane w postaci ciągu JSON i musi być w następnym wierszu po magic, jak pokazano w przykładzie kolumny.

### <a name="change-the-parameters-for-an-application-submitted-using-spark-submit"></a>Zmiana, którą przesłać spark parametry przesłane za pomocą aplikacji
Następujące polecenia są przykładem zmienić parametry konfiguracji, dla której zostało przesłane za pomocą aplikacji partii `spark-submit`.

    spark-submit --class <the application class to execute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-the-parameters-for-an-application-submitted-using-curl"></a>Zmień parametry dla aplikacji przesłane przy użyciu programu cURL
Następujące polecenia są przykładem zmienić parametry konfiguracji, dla której zostało przesłane za pomocą przy użyciu programu cURL aplikacji partii.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<the application class to execute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Jak zmienić tych parametrów, na serwerze Spark Thrift?
Spark Thrift Server JDBC/ODBC udostępnia klastra Spark i służy do zapytań Spark SQL usługi. Narzędzia takie jak usługi Power BI, Tableau itp. Używanie protokołu ODBC do komunikowania się z serwerem Thrift Spark do wykonywania zapytań Spark SQL jako aplikacji Spark. Po utworzeniu klastra Spark są uruchamiane dwa wystąpienia serwera Spark Thrift, jeden w każdym węźle głównym. Każdy serwer Thrift Spark jest widoczny jako aplikacji Spark w Interfejsie użytkownika YARN.

Platforma Spark Thrift serwer używa Spark Moduł wykonujący dynamicznej alokacji i dlatego `spark.executor.instances` nie jest używany. Zamiast tego Spark Thrift serwer używa `spark.dynamicAllocation.minExecutors` i `spark.dynamicAllocation.maxExecutors` można określić liczbę Moduł wykonujący. Parametry konfiguracji `spark.executor.cores` i `spark.executor.memory` służy do zmiany rozmiaru Moduł wykonujący. Te parametry można zmienić, jak pokazano poniżej.

* Rozwiń węzeł **zaawansowane spark-thrift-sparkconf** kategorię, aby zaktualizować parametry `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, i `spark.executor.memory`.

    ![Konfigurowanie Spark thrift serwera](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Rozwiń węzeł **niestandardowe spark-thrift-sparkconf** kategorię, aby zaktualizować parametr `spark.executor.cores`.

    ![Konfigurowanie Spark thrift serwera](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-the-driver-memory-of-the-spark-thrift-server"></a>Jak zmienić pamięci sterownika serwera Spark Thrift?
Pamięć sterownik Spark Thrift serwera jest skonfigurowany do 25% rozmiar pamięci RAM węzła głównego, pod warunkiem że całkowity rozmiar pamięci RAM węzła głównego jest większa niż 14 GB. Interfejs użytkownika narzędzia Ambari służy do zmiany konfiguracji pamięci sterownika, jak pokazano poniżej.

* W interfejsie użytkownika narzędzia Ambari kliknij **Spark**, kliknij przycisk **Configs**, rozwiń węzeł **zaawansowane spark env**, a następnie podaj wartość dla **spark_thrift_cmd_opts**.

    ![Konfigurowanie Spark thrift serwera pamięci RAM](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-the-resources-back"></a>BI nie jest używany z klastrem Spark. Jak ponownie podjąć zasobów?
Ponieważ używamy Spark dynamiczna alokacja tylko zasoby, które są używane przez serwer thrift są zasoby wzorców dwóch aplikacji. Aby odzyskać te zasoby należy zatrzymać usługi serwera Thrift działające w klastrze.

1. W interfejsie użytkownika narzędzia Ambari, w lewym okienku kliknij **Spark**.
2. Na następnej stronie kliknij **Spark Thrift serwerów**.

    ![Uruchom ponownie serwer thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Powinny pojawić się dwa headnodes, na których działa serwera Spark Thrift. Kliknij jeden z headnodes.

    ![Uruchom ponownie serwer thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. Dalej znajduje się lista wszystkich usług, które są uruchomione na tym headnode. Na liście kliknij przycisk listy rozwijanej obok Spark Thrift serwera, a następnie kliknij przycisk **zatrzymać**.

    ![Uruchom ponownie serwer thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Powtórz te kroki dla innych headnode również.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-the-service"></a>Moje notesów Jupyter nie działają zgodnie z oczekiwaniami. Jak można ponownie uruchomić usługę?
Uruchamianie Interfejsu sieci Web Ambari, jak pokazano powyżej. W okienku nawigacji po lewej stronie kliknij **Jupyter**, kliknij przycisk **akcji usługi**, a następnie kliknij przycisk **ponowne uruchomienie wszystkich**. Spowoduje to uruchomienie usługi Jupyter na wszystkich headnodes.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Jak sprawdzić, jeśli używam wszystkich zasobów?
Uruchom interfejs użytkownika Yarn, jak pokazano powyżej. W tabeli metrykę klastra u góry ekranu, sprawdź wartości **pamięć używana** i **całkowitej pamięci** kolumn. Jeśli wartości 2 są bardzo bliskiej, może nie być wystarczającej ilości zasobów, aby uruchomić następnej aplikacji. To samo dotyczy **używane VCores** i **łącznie VCores** kolumn. Ponadto w widoku głównego, w przypadku aplikacji przebywanie w **ZAAKCEPTOWANE** stanu i nie są przenoszone do **systemem** ani **nie powiodło się** stanu, przyczyną może być również wskazanie, że nie otrzymuje wystarczającej liczby zasobów, aby uruchomić.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-to-free-up-resource"></a>Jak kill działającej aplikacji w celu zwolnienia zasobów?
1. W interfejsie użytkownika Yarn z lewego panelu, kliknij przycisk **systemem**. Z listy uruchomionych aplikacji, należy określić aplikację, aby skasowane i kliknij pozycję **identyfikator**.

    ![Kasowanie App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")

2. Kliknij przycisk **Kill aplikacji** w prawym górnym rogu, następnie kliknij polecenie **OK**.

    ![Kasowanie App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")

## <a name="see-also"></a>Zobacz też
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>Dla analityków danych

* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Dla deweloperów platformy Spark

* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
