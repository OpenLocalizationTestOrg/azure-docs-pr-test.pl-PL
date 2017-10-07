---
title: "Azure Toolkit for IntelliJ: tworzenie aplikacji Spark dla klastra usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj hello Azure zestawu narzędzi dla aplikacji Spark toodevelop IntelliJ napisanych w języku Scala i przesłać je tooan klastra Spark w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Użyj narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight

Użyj hello Azure zestawu narzędzi dla aplikacji Spark toodevelop wtyczkę IntelliJ napisanych w języku Scala, a następnie prześlij je tooan klastra Spark w usłudze HDInsight bezpośrednio z hello IntelliJ zintegrowane środowisko programistyczne (IDE). Program hello wtyczki na kilka sposobów:

* Tworzenie i przesyłanie aplikacji Scala Spark w klastrze Spark w usłudze HDInsight.
* Dostęp do zasobów klastra Azure HDInsight Spark.
* Tworzenie i uruchamianie aplikacji Scala Spark lokalnie.

toocreate Twojego projektu, widok hello [tworzenie aplikacji Spark przy użyciu hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) wideo.

> [!IMPORTANT]
> Można użyć tej wtyczki toocreate i przesyłanie aplikacji tylko w przypadku klastra Spark w usłudze HDInsight w systemie Linux.
> 

## <a name="prerequisites"></a>Wymagania wstępne

- Klaster Apache Spark w usłudze HDInsight w systemie Linux. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
- Oracle Java Development Kit. Można ją zainstalować, korzystając z hello [witryny sieci Web programu Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. W tym artykule używa wersji 2017.1. Można ją zainstalować, korzystając z hello [JetBrains witryny sieci Web](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Zainstaluj zestaw narzędzi platformy Azure dla IntelliJ
Aby uzyskać instrukcje instalacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Zaloguj się tooyour subskrypcji platformy Azure

1. Uruchom hello IntelliJ IDE, a następnie otwórz Eksploratora Azure. Na powitania **widoku** menu, wybierz opcję **okna narzędzi**, a następnie wybierz **Eksploratora Azure**.
       
   ![łącze Eksploratora Azure Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Kliknij prawym przyciskiem myszy hello **Azure** węzeł, a następnie wybierz **logowania**.

3. W hello **Azure logowania** wybierz pozycję **Zaloguj się**, a następnie wprowadź poświadczenia platformy Azure.

    ![Hello Azure logowania — okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Po zalogowaniu hello **Wybierz subskrypcje** list okno dialogowe hello wszystkie subskrypcje platformy Azure, które są skojarzone z hello poświadczeń. Wybierz hello **wybierz** przycisku.

    ![Wybierz subskrypcje Hello — okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Na powitania **Eksploratora Azure** karcie, rozwiń **HDInsight** hello tooview klastry Spark w usłudze HDInsight, które są w ramach subskrypcji.
   
    ![Klastry HDInsight Spark w Eksploratorze Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello zasobów (na przykład konta magazynu) skojarzonych z hello klastra, można rozwinąć węzła nazwy klastra.
   
    ![Nazwa klastra węzłów](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Uruchamianie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight

1. Uruchom IntelliJ IDEA, a następnie utworzyć projekt. W hello **nowy projekt** okna dialogowego pozycję hello następujące: 

   a. Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.

   b. W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:

      * **Maven**, obsługę języka Scala Kreator tworzenia projektu
      * **SBT**, do zarządzania hello zależności i budowania hello Scala projektu

    ![okno dialogowe Nowy projekt Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Wybierz **dalej**.

3. Kreator tworzenia projektu Scala Hello automatycznie wykrywa, czy po zainstalowaniu hello Scala wtyczki. Wybierz **zainstalować**.

   ![Scala wtyczki wyboru](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Witaj toodownload Scala wtyczki, wybierz pozycję **OK**. Wykonaj hello instrukcje toorestart IntelliJ. 

   ![okno dialogowe instalacji Hello Scala wtyczki](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. W hello **nowy projekt** oknie hello następujące:  

    ![Wybieranie hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Wprowadź nazwę projektu i lokalizację.

   b. W hello **SDK projektu** listy rozwijanej wybierz **Java 1.8** dla klastra 2.x Spark hello, lub wybierz **Java 1.7** hello Spark 1.x klastra.

   c. W hello **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje hello poprawnej wersji dla platformy Spark zestawy SDK i Scala. Jeśli hello klastra Spark w wersji starszej niż 2.0, wybierz **Spark 1.x**. W przeciwnym razie wybierz **Spark2.x**. W tym przykładzie użyto **Spark pkt 2.0.2 (Scala 2.11.8)**.

6. Wybierz pozycję **Finish** (Zakończ).

7. Projekt Spark Hello automatycznie utworzy artefaktu. tooview hello artefaktu, hello następujące:

   a. Na powitania **pliku** menu, wybierz opcję **struktury projektu**.

   b. W hello **struktury projektu** okno dialogowe, wybierz opcję **artefakty** tooview hello domyślne artefaktu, który jest tworzony. Można również utworzyć własne artefaktu, wybierając hello — znak plus (**+**).

      ![Informacje o artefaktów w hello — okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Należy dodać kodu źródłowego aplikacji, wykonując następujące hello:

   a. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie wybierz **klasy Scala**.
      
      ![Polecenia służące do tworzenia klasy Scala w Eksploratorze projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. W hello **Utwórz nową klasę Scala** okna dialogowego polu, podaj nazwę, wybierz **obiektu** w hello **rodzaj** , a następnie wybierz **OK**.
      
      ![Tworzenie nowej klasy Scala, okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. W hello **MyClusterApp.scala** plików, Wklej hello następującego kodu. Witaj kod odczytuje dane hello z HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera hello wiersze, które mają tylko jedna cyfra hello siódmego kolumny w pliku CSV hello i zapisuje dane wyjściowe hello zbyt**/HVACOut** w obszarze hello domyślne kontener magazynu hello klaster.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Uruchom aplikację hello w klastrze Spark w usłudze HDInsight, wykonując następujące hello:

   a. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy nazwę projektu hello, a następnie wybierz **tooHDInsight przesyłanie aplikacji Spark**.
      
      ![polecenie tooHDInsight przesyłanie aplikacji Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Możesz są tooenter zostanie wyświetlony monit o poświadczenia subskrypcji platformy Azure. W hello **przesyłanie Spark** okno dialogowe, podaj hello następujące wartości, a następnie wybierz **przesyłania**.
      
      * Aby uzyskać **Spark klastrów (tylko w systemie Linux)**, wybierz hello klaster Spark w usłudze HDInsight, na którym ma zostać toorun aplikacji.

      * Wybierz artefakt z projektu IntelliJ hello, lub wybierz jedną z dysku twardego hello.

      * W hello **Nazwa klasy głównym** polu Wybierz hello wielokropka (**...** ), wybierz klasy głównym hello w kodzie źródłowym aplikacji, a następnie wybierz **OK**.

        ![okno dialogowe Wybieranie klasy głównym Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Kod aplikacji hello w tym przykładzie wymaga argumentów wiersza polecenia lub odwołać słoików lub pliki, można pozostawić hello pozostałe pola puste. Po podaniu wszystkich informacji hello hello — okno dialogowe powinno przypominać powitania po obrazu.
        
        ![okno dialogowe przesyłanie Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Witaj **przesyłanie Spark** u dołu hello hello powinien rozpocząć hello postęp wyświetlania. Mogą również wstrzymać aplikacja hello, wybierając przycisk hello red hello **przesyłanie Spark** okna.
      
      ![Witaj przesyłanie Spark okna](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn tooaccess hello dane wyjściowe zadania, zobacz hello "dostępu i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ" sekcji w dalszej części tego artykułu.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Uruchom lub debugowanie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight
Zalecamy również inny sposób przesyłania hello Spark aplikacji toohello klastra. Możesz to zrobić przez ustawienie parametrów hello w hello **konfiguracji uruchomienia/debugowania** IDE. Aby uzyskać więcej informacji, zobacz [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Dostęp i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ
Różne operacje można wykonywać za pomocą narzędzi Azure for IntelliJ.

### <a name="access-hello-job-view"></a>Wyświetl zadania hello dostępu
1. W Eksploratorze Azure rozwiń **HDInsight**, rozwiń nazwę klastra Spark hello, a następnie wybierz **zadania**.  

    ![Zadania widoku węzła](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. W okienku po prawej stronie powitania, hello **widoku zadania Spark** karcie są wyświetlane wszystkie aplikacje hello, które zostały uruchomione w klastrze hello. Wybierz nazwę hello aplikacji hello, dla której ma zostać toosee więcej szczegółów.

    ![Szczegóły aplikacji](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay podstawowe uruchomione zadania informacje, przesuń kursor myszy hello wykres zadania. Wykres etapy hello tooview i informacje, które generuje każde zadanie, wybierz węzeł na powitania wykres zadania.

    ![Szczegóły etap zadania](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview często używane dzienniki, taką jak *Stderr sterownika*, *Stdout sterownika*, i *informacji o katalogu*, wybierz pozycję hello **dziennika** kartę.

    ![Szczegóły dziennika](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. Można również wyświetlić hello historii Spark interfejsu użytkownika i hello interfejsie użytkownika YARN (na poziomie aplikacji hello), klikając łącze u góry okna hello hello.

### <a name="access-hello-spark-history-server"></a>Dostęp do serwera historii Spark hello
1. W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz użytkownika usługi Historia Spark**. 

2. Po wyświetleniu monitu wprowadź poświadczenia administratora klastra hello, które określona podczas konfigurowania klastra hello.

3. Na powitania Spark historii serwera pulpitu nawigacyjnego można użyć toolook Nazwa aplikacji hello aplikacji hello właśnie zakończono uruchomiona. W hello poprzedzających kodu, należy określić nazwę aplikacji hello przy użyciu `val conf = new SparkConf().setAppName("MyClusterApp")`. W związku z tym jest nazwa aplikacji Spark **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Uruchom hello Ambari portalu
1. W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz Portal zarządzania klastra (Ambari)**. 

2. Po wyświetleniu monitu wprowadź poświadczenia administratora hello hello klastra. Te poświadczenia zostały określone podczas procesu instalacji hello klastra.

### <a name="manage-azure-subscriptions"></a>Zarządzać subskrypcjami platformy Azure
Domyślnie zestaw narzędzi platformy Azure dla IntelliJ wymieniono klastry Spark hello wszystkie subskrypcje platformy Azure. W razie potrzeby można określić, które mają tooaccess subskrypcje hello. 

1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy hello **Azure** węzła głównego, a następnie wybierz **Zarządzaj subskrypcjami**. 

2. Okno dialogowe hello, wyczyść hello pola wyboru dalej toohello subskrypcje czy nie ma tooaccess, a następnie wybierz **Zamknij**. Możesz też wybrać **Wyloguj** Jeśli chcesz toosign poza subskrypcją platformy Azure.

## <a name="run-a-spark-scala-application-locally"></a>Uruchamianie aplikacji Spark Scala lokalnie
Umożliwia zestawu narzędzi platformy Azure dla aplikacji Spark Scala toorun IntelliJ lokalnie na stacji roboczej. aplikacji Hello zwykle nie wymagają dostępu toocluster zasoby, takie jak kontenery magazynu i można uruchomić i przetestować je lokalnie.

### <a name="prerequisite"></a>Wymagania wstępne
Gdy używasz lokalnych aplikacji Spark Scala hello na komputerze z systemem Windows, można uzyskać wyjątku, zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Wystąpił wyjątek Hello, ponieważ brakuje WinUtils.exe w systemie Windows. 

tooresolve ten błąd [Pobierz hello wykonywalnego](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) lokalizacji tooa **C:\WinUtils\bin**. Następnie należy dodać zmienną środowiskową hello **HADOOP_HOME**i ustaw wartość hello zmiennej hello zbyt**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Uruchamianie aplikacji Spark Scala lokalnej
1. Uruchom IntelliJ IDEA i tworzenia projektu. 

2. W hello **nowy projekt** okna dialogowego pozycję hello następujące:
   
    a. Wybierz **HDInsight** > **Spark dla próbki uruchamiania lokalnego HDInsight (Scala)**.

    b. W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:

      * **Maven**, obsługę języka Scala Kreator tworzenia projektu
      * **SBT**, do zarządzania hello zależności i budowania hello Scala projektu

    ![okno dialogowe Nowy projekt Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Wybierz **dalej**.
 
4. W następnym oknie hello hello następujące:
   
    a. Wprowadź nazwę projektu i lokalizację.

    b. W hello **SDK projektu** listy rozwijanej wybierz wersję Java, która jest nowsza niż wersja 1.7.

    c. W hello **wersji Spark** listy rozwijanej, wybierz hello wersję języka Scala, które mają toouse: Scala 2.11.x dla platformy Spark w wersji 2.0 lub Scala 2.10.x dla wersji 1.6 Spark.

    ![okno dialogowe Nowy projekt Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Wybierz pozycję **Finish** (Zakończ).

6. Przykładowy kod dodaje Hello szablonu (**LogQuery**) w obszarze hello **src** folderu, który można uruchomić lokalnie na komputerze.
   
    ![Lokalizacja LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Kliknij prawym przyciskiem myszy hello **LogQuery** aplikacji, a następnie wybierz **Uruchom "LogQuery"**. Na powitania **Uruchom** karty u dołu hello, zobacz dane wyjściowe podobne hello poniżej:
   
   ![Aplikacji Spark lokalnego wynik uruchomienia](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Konwertowanie istniejących IntelliJ IDEA toouse aplikacji Azure Toolkit for IntelliJ
Możesz przekonwertować hello istniejących Spark Scala aplikacji utworzonych w toobe IntelliJ IDEA zgodne z zestawu narzędzi Azure for IntelliJ. Następnie można użyć hello wtyczki toosubmit hello aplikacji tooan klastra Spark w usłudze HDInsight.

1. Dla istniejącej aplikacji Spark Scala, który został utworzony za pomocą IntelliJ IDEA Otwórz plik .iml skojarzone hello.

2. W katalogu głównym hello jest poziom **modułu** element podobnie następującej hello:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Edytuj hello element tooadd `UniqueKey="HDInsightTool"` tak hello **modułu** element wygląda hello:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Zapisz zmiany hello. Aplikacja teraz powinno być zgodne z narzędzi Azure dla IntelliJ. Można przetestować go, klikając prawym przyciskiem myszy nazwę projektu hello w obszarze Eksplorator projektów. menu podręczne Hello ma teraz opcję hello **tooHDInsight przesyłanie aplikacji Spark**.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Błąd podczas uruchamiania lokalnego: *Użyj większego rozmiaru sterty*
W wersji 1.6 Spark Jeśli używasz SDK Java 32-bitowych podczas przebiegu lokalnego, może wystąpić hello następujące błędy:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Te błędy się tak zdarzyć, ponieważ rozmiar stosu hello nie jest wystarczająco duży dla Spark toorun. Platforma Spark wymaga co najmniej 471 MB. (Aby uzyskać więcej informacji, zobacz [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Jeden prostym rozwiązaniem jest toouse SDK Java 64-bitowych. Możesz również zmienić ustawienia maszyny JVM hello w IntelliJ przez dodanie hello następujące opcje:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Dodawanie toohello opcje "Opcje maszyny Wirtualnej" pole w IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>Często zadawane pytania
Wybierz toosubmit aplikacji tooAzure Data Lake Store, **Interactive** tryb podczas procesu hello Azure logowania. W przypadku wybrania **automatycznego** tryb, możesz uzyskać wystąpił błąd.

![interakcyjny rejestrowanie](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Teraz możemy go rozwiązał. Możesz wybrać toosubmit Azure Data Lake klastra aplikacji przy użyciu dowolnej metody logowania.

## <a name="feedback-and-known-issues"></a>Opinie i znane problemy
Przeglądanie wyjść Spark bezpośrednio nie jest obecnie obsługiwana.

Jeśli masz jakiekolwiek sugestie lub opinii lub jeśli wystąpią problemy, korzystając z tego dodatku, wiadomość e-mail na adres hdivstool@microsoft.com.

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

### <a name="creating-and-running-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem sieci VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

