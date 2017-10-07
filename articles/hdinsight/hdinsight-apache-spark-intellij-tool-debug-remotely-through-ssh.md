---
title: "Azure Toolkit for IntelliJ: aplikacji Spark debugować zdalnie za pośrednictwem SSH | Dokumentacja firmy Microsoft"
description: "Wskazówki krok po kroku w sposób toouse narzędzi HDInsight Tools w zestawie narzędzi Azure dla aplikacji toodebug IntelliJ zdalnie w usłudze HDInsight clusters za pośrednictwem SSH"
keywords: zdalne debugowanie intellij, zdalnego debugowania intellij, ssh, intellij, hdinsight, debugowania intellij, debugowania
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem SSH

Ten artykuł zawiera instrukcje krok po kroku toouse narzędzi HDInsight Tools w zestawie narzędzi Azure dla aplikacji toodebug IntelliJ zdalnie w klastrze usługi HDInsight. toodebug projektu, można również wyświetlić hello [aplikacji Spark w usłudze HDInsight debugowania narzędzi Azure for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) wideo.

**Wymagania wstępne**

* **Narzędzia HDInsight Tools w Azure Toolkit for IntelliJ**. To narzędzie jest częścią zestawu narzędzi Azure for IntelliJ. Aby uzyskać więcej informacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Azure Toolkit for IntelliJ**. Użyj tej aplikacji Spark toocreate zestawu narzędzi dla klastra usługi HDInsight. Aby uzyskać więcej informacji, postępuj zgodnie z instrukcjami hello [użyj narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Usługa HDInsight SSH z nazwy użytkownika i hasła zarządzania**. Aby uzyskać więcej informacji, zobacz [połączyć tooHDInsight (Hadoop) przy użyciu protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) i [używanie protokołu SSH tunelowania tooaccess Ambari web UI, JobHistory, NameNode, Oozie i innych sieci web UI](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Tworzenie aplikacji Spark Scala i skonfiguruj ją do zdalnego debugowania

1. Uruchom IntelliJ IDEA, a następnie utworzyć projekt. W hello **nowy projekt** okna dialogowego pozycję hello następujące:

   a. Wybierz **HDInsight**. 

   b. Wybierz język Java lub Scala szablon na podstawie preferencji użytkownika. Wybierz między hello następujące opcje:

      - **Platforma Spark w usłudze HDInsight (Scala)**

      - **Platforma Spark w usłudze HDInsight (Java)**

      - **Platforma Spark dla klastra usługi HDInsight wykonywania próbki (Scala)**

      W tym przykładzie użyto **Spark dla próbki Uruchom klastra usługi HDInsight (Scala)** szablonu.

   c. W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:

      - **Maven**, obsługę języka Scala Kreator tworzenia projektu

      -  **SBT**, do zarządzania hello zależności i budowania hello Scala projektu 

      ![Tworzenie projektu debugowania](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Wybierz **dalej**.     
 
3. W hello dalej **nowy projekt** oknie hello następujące:

   ![Wybierz hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Wprowadź nazwę projektu i lokalizacja projektu.

   b. W hello **SDK projektu** listy rozwijanej wybierz **Java 1.8** dla **Spark 2.x** klastra lub wybierz **Java 1.7** dla **Spark 1. x** klastra.

   c. W hello **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala hello integruje hello poprawnej wersji dla platformy Spark zestawy SDK i Scala. Jeśli hello klastra spark w wersji starszej niż 2.0, wybierz **Spark 1.x**. W przeciwnym razie wybierz **Spark 2.x.** W tym przykładzie użyto **Spark pkt 2.0.2 (Scala 2.11.8)**.

   d. Wybierz pozycję **Finish** (Zakończ).

4. Wybierz **src** > **głównego** > **scala** tooopen kodu w projekcie hello. W tym przykładzie użyto hello **SparkCore_wasbloTest** skryptu.

5. Witaj tooaccess **Edytuj konfiguracje** menu, wybierz hello ikonę w prawym górnym rogu hello. Z tego menu można utworzyć lub edytować hello konfiguracji do zdalnego debugowania.

   ![Edycja konfiguracji](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. W hello **konfiguracji uruchomienia/debugowania** okno dialogowe, wybierz opcję hello — znak plus (**+**). Następnie wybierz hello **Prześlij zadanie Spark** opcji.

   ![Dodawanie nowej konfiguracji](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Wprowadź informacje dotyczące **nazwa**, **klastra Spark**, i **Nazwa klasy głównym**. Następnie wybierz **konfiguracji zaawansowanej**. 

   ![Uruchom konfiguracje debugowania](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. W hello **Spark przesyłanie Advanced Configuration** okno dialogowe, wybierz opcję **Spark włączenia debugowania zdalnego**. Wprowadź nazwę użytkownika SSH hello, a następnie wprowadź hasło lub użyć pliku klucza prywatnego. toosave hello konfigurację, kliknij **OK**.

   ![Włączanie debugowania zdalnego Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. Hello konfiguracji jest teraz zapisać nazwą hello, podane. Szczegóły konfiguracji hello tooview, wybierz hello jest nazwa konfiguracji. Wybierz zmiany toomake **Edytuj konfiguracje**. 

10. Po ukończeniu hello ustawienia konfiguracji można uruchomić projektu hello względem klastra zdalnego hello lub wykonania zdalnego debugowania.

## <a name="learn-how-tooperform-remote-debugging"></a>Dowiedz się, jak tooperform debugowanie zdalne
### <a name="scenario-1-perform-remote-run"></a>Scenariusz 1: Wykonania zdalnego wykonywania

W tej sekcji zostanie przedstawiony zostanie sposób toodebug sterowniki i modułów.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Ustawianie punktów podziału, a następnie wybierz hello **debugowania** ikony.

   ![Wybierz ikonę debugowania hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Podczas wykonywania programu hello osiągnie punkt podziału hello, zobacz **sterownika** kartę i dwa **Moduł wykonujący** karty w hello **debugera** okienka. Wybierz hello **Program Wznów** toocontinue ikona uruchamiania kodu hello, który następnie osiągnie hello następnego punktu przerwania i koncentruje się na powitania odpowiadającego **Moduł wykonujący** kartę. Możesz przejrzeć dzienniki wykonywania hello na powitania odpowiadającego **konsoli** kartę.

   ![Karta debugowanie](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Scenariusz 2: Wykonaj debugowanie zdalne i naprawienie usterki
W tej sekcji zostanie przedstawiony zostanie sposób wartość zmiennej hello aktualizacji toodynamically przy użyciu hello IntelliJ debugowania dla prostego poprawkę możliwości. W hello poniższy przykład kodu ponieważ istnieje już plik docelowy hello jest zgłaszany wyjątek.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>debugowanie zdalne tooperform i naprawienie usterki
1. Skonfiguruj dwa punkty podziału, a następnie wybierz hello **debugowania** hello toostart ikona zdalnego debugowania procesu.

2. Kod Hello zatrzymuje się na powitania pierwszego punktu podziału, a parametr hello i informacje o zmiennych są wyświetlane w hello **zmienne** okienka. 

3. Wybierz hello **Program Wznów** toocontinue ikony. Kod Hello zatrzymuje się na powitania drugiego punktu. Witaj wyjątek zostanie przechwycony zgodnie z oczekiwaniami.

  ![Zgłoś błąd](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Wybierz hello **Program Wznów** ikonę ponownie. Witaj **HDInsight Spark przesyłanie** okno wyświetla błąd "zadanie uruchamianie nie powiodło się".

  ![Przesyłanie błędów](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. Wybierz wartość zmiennej hello aktualizacji toodynamically przy użyciu hello IntelliJ debugowania możliwości **debugowania** ponownie. Witaj **zmienne** okienko zostanie wyświetlony ponownie. 

6. Kliknij prawym przyciskiem myszy docelowy hello na powitania **debugowania** , a następnie wybierz **ustaw wartość**. Następnie wprowadź nową wartość dla zmiennej hello. Następnie wybierz **Enter** toosave hello wartość. 

  ![Ustaw wartość](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Wybierz hello **Program Wznów** program hello toorun toocontinue ikony. Tym razem nie jest wyjątek. Można zauważyć, że projekt hello działa pomyślnie bez żadnych wyjątków.

  ![Debugowanie bez wyjątku](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Następne kroki
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstracja
* Tworzenie projektu Scala (klip wideo): [tworzenie Spark Scala aplikacji](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark w usłudze BI: wykonaj interakcyjna analiza danych przy użyciu platformy Spark w usłudze HDInsight z narzędzi do analizy Biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w HDInsight tooanalyze tworzenia temperatury użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: Korzystanie z platformy Spark w usłudze HDInsight toobuild w czasie rzeczywistym przesyłania strumieniowego aplikacji](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem sieci VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark powitania dla usługi HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
